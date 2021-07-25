Tec1-TF-IDF
---

# 1. TF-IDF算法
1. **TF-IDF(term frequency–inverse document frequency，词频-逆向文件频率)**是一种用于信息检索(information retrieval)与文本挖掘(text mining)的常用**加权技术**。
2. TF-IDF是一种统计方法，用以评估一字词对于一个文件集或一个语料库中的其中一份文件的重要程度。**字词的重要性随着它在文件中出现的次数成正比增加，但同时会随着它在语料库中出现的频率成反比下降。**
3. **TF-IDF的主要思想是**：如果某个单词在一篇文章中出现的频率TF高，并且在其他文章中很少出现，则认为此词或者短语具有很好的类别区分能力，适合用来分类。

## 1.1. TF是词频(Term Frequency)
1. 词频(TF)表示词条(关键字)在文本中出现的频率。
2. 这个数字通常会被归一化(一般是词频除以文章总词数), 以防止它偏向长的文件。
3. 公式:$TF_{ij} = \frac{n_{i,j}}{\sum_{k}n_{k,j}}$或$TF_{w} = \frac{在某一类中词条w出现的次数}{该类中所有的词条条目}$
4. $n_{i,j}$是该词在$d_{j}$中出现的次数，分母则是文件$d_{j}$中所有词汇出现的次数总和。

## 1.2. IDF是逆向文件频率(Inverse Document Frequency)
1. **逆向文件频率 (IDF)**：某一特定词语的IDF，可以由**总文件数目除以包含该词语的文件的数目，再将得到的商取对数得到。**
2. 如果包含词条t的文档越少, IDF越大，则说明词条具有很好的类别区分能力。
3. 公式:$IDF_{i} = \log{\frac{|D|}{\{j: t_{i}\in d_{j}\}}}$
4. 其中|D|是语料库中的文件总数，$|{j:t_{i}\in d_{j}|$表示包含词语$t_{i}$的文件综述，但是如果词语不在语料库中，会导致分母为0，因此一般情况下使用$1 + |{j:t_{i}\in d_{j}|$
5. 所以公式是$IDF = \log{\frac{语料库的文档总数}{包含词条w的文档数 + 1}}$

## 1.3. TF-IDF的计算
1. $TF-IDF = TF * IDF$

# 2. TF-IDF应用
1. 搜索引擎
2. 关键词抽取
3. 文本相似度
4. 文本摘要

# 3. TF-IDF的实现
  
## 3.1. NLTK的实现
```python
from nltk.text import TextCollection
from nltk.tokenize import word_tokenize
 
#首先，构建语料库corpus
sents=['this is sentence one','this is sentence two','this is sentence three']
sents=[word_tokenize(sent) for sent in sents] #对每个句子进行分词
print(sents)  #输出分词后的结果
corpus=TextCollection(sents)  #构建语料库
print(corpus)  #输出语料库
 
#计算语料库中"one"的tf值
tf=corpus.tf('one',corpus)    # 1/12
print(tf)
 
#计算语料库中"one"的idf值
idf=corpus.idf('one')      #log(3/1)
print(idf)
 
#计算语料库中"one"的tf-idf值
tf_idf=corpus.tf_idf('one',corpus)
print(tf_idf)
```

## 3.2. Sklearn实现TF-IDF
```python
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.feature_extraction.text import TfidfTransformer
 
x_train = ['TF-IDF 主要 思想 是','算法 一个 重要 特点 可以 脱离 语料库 背景',
           '如果 一个 网页 被 很多 其他 网页 链接 说明 网页 重要']
x_test=['原始 文本 进行 标记','主要 思想']
 
#该类会将文本中的词语转换为词频矩阵，矩阵元素a[i][j] 表示j词在i类文本下的词频
vectorizer = CountVectorizer(max_features=10)
#该类会统计每个词语的tf-idf权值
tf_idf_transformer = TfidfTransformer()
#将文本转为词频矩阵并计算tf-idf
tf_idf = tf_idf_transformer.fit_transform(vectorizer.fit_transform(x_train))
#将tf-idf矩阵抽取出来，元素a[i][j]表示j词在i类文本中的tf-idf权重
x_train_weight = tf_idf.toarray()
 
#对测试集进行tf-idf权重计算
tf_idf = tf_idf_transformer.transform(vectorizer.transform(x_test))
x_test_weight = tf_idf.toarray()  # 测试集TF-IDF权重矩阵
 
print('输出x_train文本向量：')
print(x_train_weight)
print('输出x_test文本向量：')
print(x_test_weight)
```

## 3.3. jieba实现TF-IDF算法
```python
import jieba.analyse
 
text='关键词是能够表达文档中心内容的词语，常用于计算机系统标引论文内容特征、信息检索、系统汇集以供读者检阅。关键词提取是文本挖掘领域的一个分支，是文本检索、文档比较、摘要生成、文档分类和聚类等文本挖掘研究的基础性工作'
 
keywords=jieba.analyse.extract_tags(text, topK=5, withWeight=False, allowPOS=())
# topK默认为20，withWeight表示是否一并返回关键词权重，默认为false，allowPOS仅包括指定词性的词，默认为空，不筛选
print(keywords)
```

# 4. TF-IDF算法的不足
1. TF-IDF的简单结构不能有效反映单词的重要程度和特征词的分布情况，无法进行权值调整。
2. 在文本已经分类的情况下，精度不高，因为可能很多重合的关键词都被覆盖。
3. 没有考虑特征词位置因素对文本的区分度
4. 对于文档中出现次数较少的重要人名和地名信息提取效果不佳。

# 5. 参考
1. <a href = "https://blog.csdn.net/asialee_bird/article/details/81486700">TF-IDF算法介绍及实现</a>
2. <a href = "https://image.hanspub.org/pdf/CSA20130100000_81882762.pdf">改进:TF-IWF算法论文</a>