Tec4-情感分析
---

# 1. TextBlob - 英文分析
- 如果没有库，需要先安装:`pip install textblob`
```py
# -*- coding: utf-8 -*-

from textblob import TextBlob

text = "I am happy today. I feel sad today."
blob = TextBlob(text)
# 完成分句
print(blob.sentences)
# [Sentence("I am happy today."), Sentence("I feel sad today.")]

# 第一句的情感分析
first = blob.sentences[0].sentiment
print(first)
# Sentiment(polarity=0.8, subjectivity=1.0)

# 第二句的情感分析
second = blob.sentences[1].sentiment
print(second)
# Sentiment(polarity=-0.5, subjectivity=1.0)

# 整体的情感分析
all = blob.sentiment
print(all)
# Sentiment(polarity=0.15000000000000002, subjectivity=1.0)
```

2. 情感极性(polarity)，范围为[-1, 1]，-1代表完全负面，1代表完全正面。
3. 主观性(subjectivity)
4. <a href = "https://github.com/sloria/TextBlob">TextBlob官方文档</a>

# 2. SnowNLP - 中文分析
- 安装库的代码:`pip install snownlp`

```py
# -*- coding: utf-8 -*-
from snownlp import SnowNLP

s = SnowNLP(u'粉红墙上画凤凰，凤凰画在粉红墙。 红凤凰、粉凤凰，红粉凤凰花凤凰')

# 分词
print(s.words)
# ['粉红', '墙上', '画', '凤凰', '，', '凤凰画', '在', '粉红', '墙', '。', '红', '凤凰', '、', '粉', '凤凰', '，', '红粉', '凤凰', '花', '凤凰']

# 词形标签
for x, y in s.tags:
    print(x, y)

# 粉红 b
# 墙上 s
# 画 n
# 凤凰 n
# ， w
# 凤凰画 c
# 在 p
# 粉红 b
# 墙 n
# 。 w
# 红 a
# 凤凰 n
# 、 w
# 粉 b
# 凤凰 n
# ， w
# 红粉 n
# 凤凰 n
# 花 v
# 凤凰 n

p = s.sentiments
print(p)
# 0.496377766757237
```

- `s.sentiments`表示的是这句话为正向的概率

## 2.1. snownlp的原理
- sentiment类的源码:
```py
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import os
import codecs

from .. import normal
from .. import seg
from ..classification.bayes import Bayes

data_path = os.path.join(os.path.dirname(os.path.abspath(__file__)),
                         'sentiment.marshal')

class Sentiment(object):

    def __init__(self):
        self.classifier = Bayes()

    def save(self, fname, iszip=True):
        self.classifier.save(fname, iszip)

    def load(self, fname=data_path, iszip=True):
        self.classifier.load(fname, iszip)

    def handle(self, doc):
        words = seg.seg(doc)
        words = normal.filter_stop(words)
        return words

    def train(self, neg_docs, pos_docs):
        data = []
        for sent in neg_docs:
            data.append([self.handle(sent), 'neg'])
        for sent in pos_docs:
            data.append([self.handle(sent), 'pos'])
        self.classifier.train(data)

    def classify(self, sent):
        ret, prob = self.classifier.classify(self.handle(sent))
        if ret == 'pos':
            return prob
        return 1-prob

classifier = Sentiment()
classifier.load()

def train(neg_file, pos_file):
    neg_docs = codecs.open(neg_file, 'r', 'utf-8').readlines()
    pos_docs = codecs.open(pos_file, 'r', 'utf-8').readlines()
    global classifier
    classifier = Sentiment()
    classifier.train(neg_docs, pos_docs)

def save(fname, iszip=True):
    classifier.save(fname, iszip)

def load(fname, iszip=True):
    classifier.load(fname, iszip)

def classify(sent):
    return classifier.classify(sent)
```

- `train`:用于训练一个情感分类器
- `classify`:用于预测的函数
- `handle`函数会被以上两个用到，主要工作是
  - 对输入文本分词
  - 去停用词

## 2.2. 分类核心
1. 情感分类的基本模型是贝叶斯模型Bayes
2. 训练的核心代码:

```py
def train(self, data):
    # data 中既包含正样本，也包含负样本
    for d in data: # data中是list
        # d[0]:分词的结果，list
        # d[1]:正/负样本的标记
        c = d[1]
        if c not in self.d:
            self.d[c] = AddOneProb() # 类的初始化
        for word in d[0]: # 分词结果中的每一个词
            self.d[c].add(word, 1)
    # 返回的是正类和负类之和
    self.total = sum(map(lambda x: self.d[x].getsum(), self.d.keys())) # 取得所有的d中的sum之和
```

3. 贝叶斯模型的使用是贝叶斯定理算概率的公式了的对应代码

```py
def classify(self, x):
    tmp = {}
    for k in self.d: # 正类和负类
        tmp[k] = log(self.d[k].getsum()) - log(self.total) # 正类/负类的和的log函数-所有之和的log函数
        for word in x:
            tmp[k] += log(self.d[k].freq(word)) # 词频，不存在就为0
    ret, prob = 0, 0
    for k in self.d:
        now = 0
        try:
            for otherk in self.d:
                now += exp(tmp[otherk]-tmp[k])
            now = 1/now
        except OverflowError:
            now = 0
        if now > prob:
            ret, prob = k, now
    return (ret, prob)
```

# 3. 参考
1. <a href = "https://blog.csdn.net/ziyonghong/article/details/83928347">自然语言处理的情感分析之TextBlob& SnowNLP</a>