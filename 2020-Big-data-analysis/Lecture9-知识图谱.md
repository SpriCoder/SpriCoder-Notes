Lecture9-知识图谱
---

[TOC]

# 1. 知识图谱
1. 知识图谱概念
2. 知识图谱内涵
3. 知识图谱优势
4. 知识图谱价值
5. 典型知识图谱

# 2. 知识图谱概念
1. 知识图谱(Knowledge Graph)本质上是一种**大规模语义网络** (semantic network)，富含实体(entity)、概念(concepts) 及其之间的各种语义关系 (semantic relationships)
   1. 作为一种语义网络，是大数据时代知识表示的重要方式之一
   2. 作为一种技术体系，是大数据时代知识工程的代表性进展
2. 知识图谱示例子。知识图谱富含实体、概念、属性、关系等信息

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/1.png)


## 2.1. 知识图谱分类
1. 领域(行业)知识图谱 (Domain specific Knowledge Graph)：聚焦于特定领域或者行业的知识图谱
2. 企业知识图谱(Enterprise knowledge graph)：贯穿企业各业务部门的知识图谱

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/2.png)

## 2.2. 知识图谱的源头
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/4.png)

## 2.3. 知识图谱应用
1. 2012年5月，Google收购Metaweb 公司，并正式发布知识图谱
2. 搜索核心需求：让搜索通往答案，但是机器无法理解搜索关键词，也很难精准回答。
3. 根本问题
   1. 缺乏大规模背景知识
   2. 传统知识表示难以满足需求

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/3.png)

# 3. 知识图谱内涵
1. 开放和封闭的知识图谱:开放是可以添加知识进来，而封闭的则不可以
2. 定义本体:在作知识图谱之前一定要先明确是开放还是封闭的

## 3.1. KG组成：Node-Entity
1. Entity/Objects/Instances:维基百科：实体就是东西,它本身，作为主体或作为对象存在，实际上或潜在地，具体地或抽象地，物理地或非物理地存在。
2. Concept:概念
   1. 在形而上学，尤其是本体论中，概念是存在的基本类别。
   2. 类别的(心理)表示
3. Category:类别有共同点的实体组；
4. Type/class:类型/类别，WIKITIONARY：基于共享特征的分组；一类。

## 3.2. KG组成：Node-Entity例子
1. Date：特朗普 出生日期 1946年6月14日
2. String：特朗普 简介"唐纳德·特朗普(Donald Trump)，第45任美国总统，1946 年6月14日生于纽约，美国共和党籍政治家"
3. Numeric：特朗普 年龄 71

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/6.png)

- 每一个信息都是node，这个node是可以被重用的，比如年龄71的点

## 3.3. KG组成：Edge
1. Relation:
   1. 侧重实体(indvidual)之间的关系
   2. 例子:
      1. 坐着：坐在桌子上的苹果
      2. 更高：华盛顿纪念碑比白宫高
2. Property/Attribute/Quality(属性)
   1. 描述对象的特征/质量
   2. 例子：对象的大小，颜色，重量，成分等

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/5.png)

# 4. 知识图谱源起
  
## 4.1. 知识工程(KE)的缘起-Symbolism，符号主义
1. 符号主义的主要观点
   1. 认知即计算
   2. 知识是信息的一种形式,是构成智能的基
   3. 知识表示、知识推理、知识运用是人工智能的核心

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/7.png)

2. 物理符号系统
   1. 物理符号系统具有一般智能操作的必要和充分手段
   2. 可以将思维视为根据正式规则对信息进行操作的设备。
3. GOFAI(老式人工智能，由John Haugeland提出)，专注于此类高水平符号，例如`<dog>`和`<tail>`
4. AI System = Knowledge + Reasoning

## 4.2. 代表人物和时间节点
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/8.png)

1. KE(知识工程)是一门工程学科，涉及将知识集成到计算机系统中，以解决通常需要高水平专业知识的复杂问题。 参考维基百科
2. 知识工程是以知识为处理对象，研究知识系统的知识表示、处理和应用的方法和开发工具的学科的方法和开发工具的学科

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/9.png)

> 传统知识工程在规则明确、边界清晰、应用封闭的应用场景取得了巨大成功

## 4.3. 传统KE的基本特点
1. 自上而下:严重依赖专家和人的干预
   1. 规模有限
   2. 质量存疑

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/10.png)

## 4.4. 传统KE的主要挑战:知识获取困难
1. 隐性知识、过程知识等**难以表达**，专家**不一定愿意分享出来**，不同专家之间的知识可能**不一致**。
   1. 如何表达做蛋炒饭的知识？
   2. 老中医看病用到了哪些知识。
2. 领域知识的**形式化**表达较为困难。
3. 专家知识不可避免地存在**主观性**，比如都是做一个方向的，表达方式、研究路径可能不一致。
4. 知识表达难以完备，缺漏是常态。

## 4.5. 传统KE的主要挑战:知识应用困难
1. 应用易于超出预先设定的知识边界
2. 很多应用需要常识的支撑
   1. 难以处理异常情况
   2. 难以处理不确定性推理
3. 知识更新困难

- Example:`Can pig fly?`
- Rule:鸟是可以飞的

> 行业应用中的知识需求难以封闭于预设的领域知识边界内

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/11.png)

## 4.6. 互联网应用催生大数据世代知识工程(BigKE)
1. 大规模开放性应用
   1. 永远不知道用户下一个搜索关键字是什么
   2. "创造101"、"吃鸡"、"纸片人"、"蛙儿"
2. 精度要求不高:搜索引擎从来不需要保证每个搜索的理解和检索都是正确的
3. 应用/推理简单
4. 大部分搜索理解与回答只需要实现简单的推理
   1. 简单推理：姚明的身高是多少，一跳就可以解决
   2. 复杂推理：姚明老婆的婆婆的儿子有多高，需要几跳才可以解决
5. 互联网时代的大规模开放性应用需要全新的知识表示，**谷歌知识图谱**诞生，知识工程迈入大数据时代

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/12.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/13.png) |
| -------------------- | -------------------- |

## 4.7. 数据驱动的大规模自动化知识获取
1. 自下而上：网页文本、搜索日志、购买记录

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/14.png)

## 4.8. 大数据时代的机遇——众包技术
1. 众包与群智成为大规模知识获取的一条新路径

> 案例1: 基于知识问答验证码的知识获取:复旦大学知识工场实验室提供知识验证码服务，通过众包的方式对现有知识进行验证

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/15.png)

> 案例2:基于众包的Taxonomy构建，DBpedia通过众包方式构建了DBpedia Ontology

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/16.png)

## 4.9. 大数据世代的机遇——高质量UGC
1. Web2.0时代到未，产生大量的高质量UGC(User Generated Content)
   1. 提供获得得广大用户一致认可的**高质量数据源**
   2. 维基百科, 百度百科
2. 为自动挖掘知识提供了**高质量数据源**
3. 为构建抽取模型提供了**高质量样本**

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/17.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/18.png) |
| -------------------- | -------------------- |

# 5. 知识图谱优势

## 5.1. 大规模
1. 对实体和概念的更大覆盖


| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/19.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/20.png) |
| -------------------- | -------------------- |

## 5.2. 语义丰富
> 覆盖更多语义关系

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/21.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/22.png) |
| -------------------- | -------------------- |

1. 高质量数据
   1. 大数据：多种来源的交叉验证
   2. 众包：质量保证

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/23.png)

## 5.3. 友好的结构
> 结构化的组织

1. 通过RDF
2. 按图

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/24.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/25.png) |
| -------------------- | -------------------- |

# 6. 越来越多的知识图谱应运而生

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/28.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/27.png) |
| -------------------- | -------------------- |

# 7. 知识图谱的价值

## 7.1. 未来已至:人类已经进入智能时代
1. **大数据的日益积累、计算能力的快速增长**为人类进入智能时代奠定了基础
2. 大数据为智能技术的发展带来了前所未有的数据红利
3. 机器**计算智能、感知智能**达到甚至超越人类

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/29.png)

## 7.2. 智能化升级与转型
1. 智能化升级与转型已经成为各行各业的普遍诉求
2. 从信息化走向智能化是必然趋势
3. AI+成为AI赋能传统行业的基本模式
4. 战略意义
   1. 全方位、深度渗透到各行各业、各个环节
   2. 颠覆性影响，重塑行业形态，甚至社会形态

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/30.png)

## 7.3. 认知智能是智能化的关键
> 理解与解释是后深度学习时代人工智能的核心使命之一

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/31.png)

## 7.4. 知识图谱使能认知智能
1. **机器理解数据**的本质：建立从数据到知识库中实体、概念、关系的映射
2. **机器解释现象**的本质：利用知识库中实体、概念、关系解释现象的过程

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/32.png)

## 7.5. 知识图谱使能机器语言认知
1. 对机器的语言理解需要知识库
   1. 大规模
   2. 语义丰富
   3. 友好的结构
   4. 高质量
2. 传统知识表示不能满足这些要求，但是KG可以
   1. 本体
   2. 语义网络/框架
   3. 文字
3. **NLP + KB = NLU**
   1. NLP =自然语言处理
   2. NLU =自然语言理解

## 7.6. 知识图谱使能可解释人工智能
> 解释取决于人类认知的基本框架；概念、属性、关系是认知的基石。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/33.png)

## 7.7. 知识引导成为解决问题的主要方式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/34.png)

1. **数据驱动**利用**统计模式**解决问题
2. 单纯依赖**统计模式**难以有效解决很多实际问题

## 7.8. 知识将显著增强机器学习能力
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/35.png)

1. 降低机器学习模型的大样本依赖，提高学习的经济性
2. 提高机器学习模型对于先验知识的利用效率
3. 增强机器学习模型与先验知识的一致性

## 7.9. 知识将成为比数据更为重要的资产
1. 大数据时代是得数据者得天下
2. 人工智能时代是得知识者得天下
3. 数据是石油，知识就是石油的萃取物
4. Knowledge is power in AI

# 8. 典型知识图谱

## 8.1. 知识图谱分类
1. 自动化程度
2. 数据来源结构化程度
3. 跨语言
4. 通用/specific

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/36.png)

## 8.2. Cyc
1. 简介:常识知识图谱
2. 特点:通过人工方法将上百万条人类常识编码成机器可用的形式，用以进行智能推断
3. 规模:目前ResearchCyc知识图谱中包含了700万条断言(事实和规则)，涉及63万个概念，38000种关系
4. http://www.cyc.com/

## 8.3. WordNet
1. 简介:基于认知语言学的英语词典
2. 样例:S(n) car, auto, automobile, machine, motorcar (a motor vehicle with four wheels; usually propelled by an internal combustion engine) "he needs a car to get to work"
3. 特点:以同义词集合( synset )作为一个基本单元
4. 规模:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/37.png)

## 8.4. ConceptNet
1. 简介:大型的多语言常识知识库
2. 特点:知识来源丰富
   1. 众包(Crowd-Sourcing)
   2. 资源(例如Wiktionary 和Open Mind Common Sense)
   3. 带目的的游戏(如Verbosity 和 nadya.jp)
   4. 专家创建的资源(如WordNet 和JMDict)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/39.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/38.png)

3. http://conceptnet.io/

## 8.5. Freebase/Wikidata
1. 简介:
   1. Freebase 所有知识采用结构化的表示形式，可由机器和人编辑
   2. Wikidata是维基百科的姐妹工程，同样可由机器和人自由编辑
   3. 2016年8月31日，Freebase宣布关闭， 所有数据汇入Wikidata
2. 样例："Donald Trump"
3. 特点
   1. 众包构建
   2. 结构化三元组
4. 统计：Wikidata目前包含49,915,906个实体

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/40.png)

## 8.6. DBpedia
1. 从维基百科页面中自动抽取出结构化的知识，构建而成的大型通用百科图谱
2. 样例:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/41.png)

3. 特点
   1. 多语
   2. 自动构建
4. 统计
   1. 共收录有 127 种不同语言共计2800万实体
   2. 其中英文实体数量最大，为 467 万
5. http://wiki.dbpedia.org/

## 8.7. Google KG
1. 简介：谷歌知识图谱于2012 年发布，被认为是搜索引擎的一次重大革新
2. 样例："Nanjing University"
3. 特点：
   1. 规模巨大
   2. 用于增强搜索引擎的搜索能力
4. 统计：5700万实体，180亿关系

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/42.png)

# 9. 领域知识图谱

## 9.1. 什么是领域知识图谱
1. 知识图是一个大规模的语义网络，由实体/概念以及它们之间的语义关系组成
2. 特定领域的知识图

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/43.png)

## 9.2. NoKG(Not Only KG)
1. 传统知识工程，专家构建，代价高昂， 规模有限；知识边界易于突破，难以适应大数据时代开放应用到规模化需求
2. 大规模开放应用需要"大"知识(大规模知识库)
3. Small Knowledge + Big Data = Big Knowledge，知识图谱引领知识工程

## 9.3. DKG与GKG的区别
1. DKG，Domain-specific Knowledge Graph，领域知识图谱
2. GKG，General-purpose Knowledge Graph，通用知识图谱
3. DKG和GKG在知识表示、获取与应用等方面有着显著差异

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/45.png)

## 9.4. DKG和GKG的关系
1. DKG是从GKD通过隐喻获得的

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/46.png)

2. GKG对于DKG有着显著支撑作用

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/47.png)

## 9.5. 领域行业应用对于知识需求难以闭合
1. 行业应用中的知识需求难以封闭于预设的领域知识边界内。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/48.png)

## 9.6. 为何需要符号化表示的知识图谱
1. 符号表示与分布式表示是两种重要的知识表示形式
2. 已经有两条边了，我们需要通过知识图谱推理补齐第三条边

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/49.png)

## 9.7. 为什么需要领域知识图谱
1. 大数据时代需要知识引擎释放大数据价值形成行业认知能力实现简单工作自动化
2. 人工智能时代需要机器智脑实现自然人机交互

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/50.png)

## 9.8. 将领域知识赋予机器，解放人类脑力
1. 领域知识的积累与沉淀是智能化的必经路径

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/51.png)

## 9.9. 领域知识图谱系统的生命周期
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/52.png)

## 9.10. DKG如何构建
> 实体发现可能会用到分类聚类方法

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/53.png)

## 9.11. DKG如何评价
1. 质量准
2. 规模全
3. 实时新

## 9.12. DKG如何存储
1. 数据库选型依据
   1. 操作复杂度
      1. 全局计算
      2. 多步遍历
      3. 复杂子图
   2. 知识库规模
      1. 节点
      2. 关系
      3. 密度
2. 三元组中存储哪些信息？关联事实
 
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/54.png)

## 9.13. DKG如何查询
1. SPARQL
   1. 优点：表达能力强、可推理
   2. 缺点：较复杂、难书写、 复杂查询执行代价高昂
2. SQL
   1. 优点：简单，普及
   2. 缺点：表达能力相对较弱

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/55.png)

## 9.14. DKG应用
1. 搜索
2. 推荐
3. 问答
4. 解释
5. 决策

## 9.15. DKG落地案例
1. 农业知识图谱开源项目

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/56.png)

## 9.16. DKG还存在哪些挑战
1. 知识表示
2. 知识获取
3. 知识应用

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/57.png)

# 10. 知识图谱问答

## 10.1. IBM Watson
1. 目前应用于医疗行业

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/58.png)

## 10.2. 智能搜索
1. 知识卡片：根据查询实体，返回实体关联的知识信息
2. 知识问答：直接明了地返回问答结果

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/59.png)

## 10.3. 问答系统发展历程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/60.png)

## 10.4. 问答系统概述
1. 概述
   - 问答系统(Question Answering system),指的是回答人提出的自然语言问题的系统
2. 问答系统的价值
   1. 逐渐取代基于关键字搜索的交互方式
   2. 跨越人机语义鸿沟的重要尝试
   3. 检验机器智能的重要方式
3. 问答系统的分类
   1. 结构化知识问答：知识图谱问答
   2. 非结构化知识问答
      1. 机器阅读理解(machine reading comprehension)：基于单一文档
      2. 信息检索问答(IR-QA)：跨文档

## 10.5. 问答系统问题分类
1. 事实型问题：姚明的身高多少?
2. 是非型问题：珠穆朗玛峰是不是世界第一高峰？
3. 对比型问题：姚明和郭敬明谁更高？
4. 原因/结果/方法型问题：人民币贬值之后会发生什么
5. 观点型问题：你对人民币破7这个事情怎么看？
6. 对话型问题：您好，我想办理A套餐

## 10.6. 问答系统三种范式
1. 基于信息检索的问答
   1. 资源：QA对
   2. 策略：计算用户问句与问答数据库中问题之间的相似度
   3. 核心：相似度计算
2. 基于知识库的问答
   1. 资源：结构化好的知识元组
   2. 策略：问句解析与查询转换
   3. 核心：问句知识抽取与知识库子图查询
3. 基于阅读理解的问答
   1. 资源：单篇文档且答案包含在文档中
   2. 策略：识别答案的边界，包括起始位置和结束位置
   3. 核心：边界识别

## 10.7. 问答系统核心问题
1. 信息检索问答
   1. 问句向量表示
      1. 基于传统TF-IDF的向量表示
      2. 基于主题的向量表示
      3. 基于预训练的向量表示(doc2vec, word2vec)
      4. 基于深度学习的向量表示
   2. 问句相似度计算
      1. Cosine向量表示
      2. 编辑距离
      3. Siamese network
2. 知识图谱问答
   1. 问句解析
      1. 意图识别
      2. 论元解析
   2. 多轮问答
      1. 会话状态管理
      2. 缺失值填充

## 10.8. 知识图谱问答的常规做法
1. 基于模板匹配的语义解析
   1. 思想
      1. 人工编写+模板学习与人工审核生成模板
      2. 实体识别与实体关系识别
      3. 查询模板匹配
   2. 优点
      1. 基于子图结构匹配，准确率高
   3. 缺点
      1. 以实体/属性/关系识别为前提
      2. 识别误差导致查询模板召回率低
2. 基于复述的语义解析
   1. 思想
      1. 人工根据具体查询需求，编写生成规则
      2. 基于规则生成标准问句集合
      3. 基于语义相似度进行模板匹配
      4. 基于模板匹配进行论元解析
   2. 优点：基于语义相似度，查询模板匹配召回率高
   3. 缺点：需要构造大量候选实例，匹配准确率不高

## 10.9. 问答系统架构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/61.png)

## 10.10. 问句解析
1. 问句预处理：基于概念、实体、属性和操作符进行分词
2. 问句实体项识别
   1. 概念、实体、属性
   2. 操作符(><=)
   3. 日期实体
   4. 数值实体
3. 实体三元组生成
   1. 实体+属性、属性+对象值
   2. 属性值+概念
   3. 属性+数值
   4. 操作符+属性+值
   5. 概念+属性+值

## 10.11. 基于模板规则的问句解析
1. 方法步骤
   1. "冷启动"阶段，不用训练，快速生效，适度泛化
   2. 内置实体抽取+ 用户自定义实体库+ 规则模板语籵：播放刘德华冰币
   3. 模板：[播放][singer][song]
   4. 模板质量判定：语籵是否自动生成模板

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/62.png)

## 10.12. 基于统计的问句解析
1. 思想：对于跨领域实体时，需要借助统计信息完成实体链接和意图分类
2. Eg:我要去看花千骨的免费版

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/63.png)

## 10.13. 基于深度学习的方法
1. 概述：近几年卷积神经网络(CNN)和循环神经网络(RNN)在NLP领域任务中表现出来的语言表示能力， 越来越多的研究人员尝试深度学习的方法完成问答领域的关键任务，包括问题分
2. 过程
   1. (question classification)，语义匹配与答案选择
   2. (answer selection)，答案自动生成
   3. (answer generation);即对用户输入解析、答案查询与检索等环节进行优化。
3. 优点：实现"端到端＂的问答：把问题与答案均使用复杂的特征向量表示，使用深度学习来计算问题与答案的相似度
4. 不足：不支持复杂的查询;需要比较长的训练过程，不适用于现实应用场景中的知识更新后的实时查询

## 10.14. 智能问答面临的问题和挑战
1. 复杂query的解析
   1. 多意图:"帮我播放音乐，打开窗户"
   2. xxx:"如果明天下币，提醒我关窗户"
   3. 其他:"帮我建一个明天C罗比赛的提醒
2. 复杂多轮及上下文
   1. 任务型、问答、闲聊等多种技能的自由切换以及上下文传递
   2. U:明天西甲的比赛
   3. A:为你找到如下比赛:(屏幕显示"皇马对巴萨"等三场比赛)
   4. U:帮我建一个第二场比赛的提醒

# 11. KG embedding

## 11.1. 推荐论文
1. <a href = "https://link.zhihu.com/?target=https%3A//ieeexplore.ieee.org/abstract/document/8047276">Knowledge Graph Embedding: A Survey of Approaches and Applications</a>
2. <a href = "https://link.zhihu.com/?target=http%3A//nlp.csai.tsinghua.edu.cn/~lzy/publications/knowledge_2016.pdf">知识表示学习研究进展，刘知远</a>

## 11.2. 简介
1. KG Embedding主要是把实体(entities)和关系(relations)嵌入(Embed)到一个连续向量空间里面
2. KG Embedding主要包含三个步骤：
   1. 对实体(entities)和关系(relations)进行表示
   2. 定义得分函数(scoring function)
   3. 实体和关系的表示进行学习

## 11.3. 模型
1. KG Embedding方法被划分为两类

### 11.3.1. 距离变换模型(Translational distance models)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/64.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/65.png)

### 11.3.2. 语义匹配模型
1. 模型有RESCAL、DistMult和HolE

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/66.png)

2. 还有SME、NTN、MLP和NAM等方式

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/67.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/68.png)

### 11.3.3. 不同模型的复杂度比较
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/69.png)

## 11.4. 训练
1. 模型训练有两种：基于开放世界假设和基于闭合世界假设

### 11.4.1. 开发世界假设，Training under Open World Assumption，OWA
1. KGS只包含真实的事实，$D^+$只存储正例
2. logistic loss:$\min\limits_{\theta}\sum\limits_{r \in D^+ \cup D^-}log(1 + exp(-y_{hrt} * f_r(h, t)))$
3. pairwise ranking loss：$\min\limits_{\theta}\sum\limits_{r^+ \in D^+}\sum\limits_{r^- \in D^-}\max(0, \gamma - f_r(h, t) + f_{r'}(h',t'))$

### 11.4.2. 闭合世界假设，Training under Cloesd World Assumption，CMA
1. 没有包含在$D^+$中的样例都是错误的
2. squared loss:$\min\limits_{\theta}\sum\limits_{h, t\in E, r\infty R(y_{hrt} - f_r(h, t))^2$

## 11.5. 其他参考信息
1. 实体类型，Entity Types
2. 关系路径，Relation Paths
3. 背景描述，Textual Descriptions
4. 逻辑规则， Logical Rules
5. 实体属性，Entity Attributes
6. 临时信息，Temporal Information
7. 图的结构，Graph Structures

## 11.6. 应用
1. In-KG Applications：
   1. 链接预测，知识图谱补全，Link Prediction，[公式]，[公式]，[公式]
   2. 三元组分类，Triple Classifification，判断三元组事实[公式]是否为真
   3. 实体分类，Entity Classifification，将实体归类为不同的实体 语义类别
   4. 实体判别，Entity resolution，判断两个实体是否为同一个目标
2. Out-of-KG Applications：
   1. 关系抽取， Relation Extraction
   2. 问答系统，Question Answering
   3. 推荐系统， Recommender Systems

## 11.7. TransE算法
1. 三元组的表示:(h, r, t)含义为(头实体，关系，尾实体)
2. 目标：我们找到正确的三元组，即: h + r = t
3. 算法过程描述

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec9/70.png)

4. 注意：
   1. 我们需要关注的是之前的项和后面的项之间的关系，如果正确了则给予正反馈，否则基于负反馈。
   2. SGD的收敛效果没有GD，但是这个可以有效的避免过拟合情况的出现。

## 11.8. TransH算法
<a href = "https://blog.csdn.net/MonkeyDSummer/article/details/85273843">TransH 算法详解</a>

# 12. 实践项目参考
1. <a href = "https://blog.csdn.net/qq_35273499/article/details/80259821">项目实战：如何构建知识图谱</a>
2. <a href = "https://blog.csdn.net/hadoopdevelop/article/details/84787934?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param">知识图谱完整项目实战(附源码)(2)</a>
3. <a href = "https://github.com/smoothnlp/SmoothNLP">github:smoothNLP开源项目</a>

# 13. 知识图谱数据集介绍
1. <a href = "https://zhuanlan.zhihu.com/p/133649429">【知识工程】知识图谱常用实验数据集Freebase、WordNet概述</a>

# 14. 参考
1. <a href = "https://zhuanlan.zhihu.com/p/102391664">知识表示-KG Embedding</a>
2. <a href = "https://www.jianshu.com/p/995cc0b8ebe5">最全知识图谱介绍:关键技术、开放数据集、应用案例汇总</a>
3. <a href = "https://blog.csdn.net/MonkeyDSummer/article/details/85253813">TransE算法详解</a>
4. <a href = "https://blog.csdn.net/u011274209/article/details/50991385">TransE算法(Translating Embedding)(主要是注解)</a>