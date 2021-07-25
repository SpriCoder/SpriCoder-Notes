Lecture6-分类
---

[TOC]

# 1. 分类
1. 在分类问题中，可以将某个域中的每个实体置于一组离散的类别中的一个中：是/否，朋友/敌人，好/坏/无所谓，蓝色/红色/绿色等。
2. 给定一个带有标签的实体的训练集，制定一个将标签分配给测试集中的实体的规则

## 1.1. 分类引入
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/2.png)

1. 可能有一个简单的分隔符(例如，二维的直线或一般的超平面)，也可能没有
2. 可能存在各种"噪音"
3. 可能有"数据重叠"
4. 不应被低维的几何直觉所欺骗
5. 一些分类器显式表示分隔符(例如，直线)，而对于其他分类器，隐式完成分隔
6. 一些分类器只是决定一个对象在哪个类中

## 1.2. 物体的表示
1. 每个要分类的对象都表示为一对(x，y)：
   1. 其中x是对象的描述(请参见以下幻灯片中的数据类型示例)
   2. 其中y是一个标签(现在假定为二分类)
2. 机器学习分类器的成功或失败通常取决于选择正确的对象描述
   1. 描述的选择也可以看作是学习中的问题，实际上，我们将在以后的讲座中讨论选择描述的自动化过程
   2. 但是这里经常需要良好的直觉

## 1.3. 数据类型
1. 数据处理方式:向量化数据
   1. 物理特征
   2. 行为特征:文字、发布信息的情况
   3. 上下文:你所在的环境
   4. 历史:过去的印迹(足迹)
2. 我们现在假设这样的向量在表中明确表示，之后我们将使用这种假设
3. 数据表现的形式
   1. 文本和超文本
   2. 邮件
   3. 蛋白质序列
   4. Unix系统调用的顺序
   5. 网络层:图
   6. 图片:识别目标物

## 1.4. 训练和验证
1. 数据集(标签样本)会被划分为三部分
   1. 训练集
   2. 验证集
   3. 测试集

### 1.4.1. 训练
1. 估计训练集上的参数
2. 调整验证集上的超参数
3. 在训练集上报告结果
4. 缺少任何这些都会导致过拟合的产生

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/3.png)

### 1.4.2. 统计问题
1. 想要一个对测试数据表现良好的分类器
2. 过度拟合：非常紧密地拟合训练数据，但不能很好地概括
3. 误差线：想要对准确性进行现实(保守)的估计

## 1.5. 分类的实例

### 1.5.1. Spam Filter 垃圾邮件识别器
1. 输入:email
2. 输出:垃圾邮件/不是垃圾邮件
3. 初始化:
   1. 获得很多的样例邮件，已经被标记为spam或者是ham
   2. 想要去预测一个新的未来的邮件是不是垃圾邮件
4. 特点:以下的属性被用来区分邮件是不是垃圾邮件
   1. 词:FREE!
   2. 文本模式:$dd，CAPS
   3. 非文本:发送方

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/1.png)

### 1.5.2. 数字识别
1. 输入:图片或者像素网格
2. 输出:数字0-9
3. 初始化:
   1. 获得很多的样例图片，每一个被标记为一个数字
   2. 想要去预测一个新的未来的数字图片中的数字
4. 特点:以下的属性被用来区分当前图片中的数字
   1. 像素:(6,8)是ON
   2. 形状模式:数字组成、纵横比、循环检测数字
5. 当前状态:和人相似
6. 分类是提前设置好的，有限的，目标明确的。

## 1.6. 实际分类任务的其他示例
1. 欺诈检测(输入：帐户活动，类别：欺诈/无欺诈)
2. 网页垃圾邮件检测(输入：HTML /渲染页面，类别：垃圾邮件/火腿)
3. 语音识别和说话者识别(输入：波形，类别：音素或单词)
4. 医学诊断(输入：症状，类别：疾病)
5. 自动作文评分器(输入：文档，课程：成绩)
6. 客户服务电子邮件路由和文件夹
7. 社交网络中的链接预测
8. 药物设计中的催化活性

## 1.7. 分类的应用领域
1. 二分类问题
2. 多分类问题(Eg, 兔子，老虎，牛)
   1. 直接分类
   2. 划分为多个并列的二分类问题合并(Eg, 兔子和虎、虎和牛、兔子和牛)
   3. 划分为多个串行的二分类问题(Eg.非虎，非兔)
3. 非专属类别
4. 排位

## 1.8. 分类效果的评价标准

### 1.8.1. 分类准确率
指模型正确地预测新的或先前未见过的数据的类标号的能力，通常分类算法寻找的是分类准确率高的分类模型，分类准确率在一般情况下可以满足分类器模型的比较

### 1.8.2. 计算复杂度
1. 计算复杂度决定着算法执行的速度和占用的资源，它依赖于具体的实现细节和软硬件环境。
2. 由于数据挖掘中的操作对象是海量的数据库，因而空间和时间的复杂度是非常重要的问题

### 1.8.3. 可解释性
分类结果只有可解释性好，容易理解，才能更好地用于决策支持，结果的可解释性越好，算法受欢迎的程度越高

### 1.8.4. 可伸缩性
一个模型是可伸缩的，是指在给定内存和磁盘空间等可用的系统资源的前提下，算法的运行时间应当随数据库大小线性增加

### 1.8.5. 强壮性或鲁棒性
指在数据集中含有噪声和缺失值的情况下，分类器正确分类数据的能力

### 1.8.6. 累积增益图
1. 累积增益图会在给定的类别中显示通过把个案总数的百分比作为目标而增益的个案总数的百分比。对角线是"基线"曲线，曲线离基线的上方越远，增益越大。
2. 累积增益图通过选择对应于大量收益的百分比选择分类标准值，然后将百分比与适当分界值映射。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/51.png)

### 1.8.7. 不平衡数据分类
1. 不平衡数据是指训练样本数量在类间分布不平衡，具体地说就是在同一数据集中某些类的样本数远大于其他类的样本数
   1. 样本数少的类为少数类(正类)
   2. 样本数多的类为多数类(负类)
2. 具有不平衡类分布的数据集出现在很多的实际应用中，很多重要信息隐藏在少数类中
3. 在这种类中。少数类的正确分类比多数类的正确分类更有价值，比如1%的的信用卡交易是欺诈。

### 1.8.8. 使用混淆系数矩阵
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/52.png)

- 不平衡数据分类问题中，我们不关注正确分类的负例
- 实际正例数(P) = TP + FN
- 实际负例数(N) = FP + TN
- 实例总数C = P + N

1. 分类准确率，对测试集分类时，分类正确样本的百分比

$$
Accuracy = \frac{正确预测数}{样本总数} = \frac{TP + TN}{C}
$$

2. 错误率，对测试集分类时，错误分类的样本占样本总数的百分比

$$
Errorrate = 1- Accuracy = 1 - \frac{TP + TN}{C} = \frac{FN + FP}{C}
$$

3. 精度(真负率)，为正确分类的正例占分类结果为正例的样本个数的比例

$$
p = \frac{TP}{TP + FP}
$$

4. 召回率(真正率)，为正确分类的正例个数占实际正例个数的比例

$$
r = \frac{被正确分类的正例样本个数}{实际正例样本个数} = \frac{TP}{TP+FN}
$$

5. $F_1$度量，表示精度或召回率的调和平均值:$F_1 = \frac{2rp}{r+p}$，$F_1$度量趋向于接近精度或召回率中的较小者。
6. 精度和召回率是评价不平衡数据分类模型的两个常用度量，可以构造一个为基线模型，最大化其中一个度量，发现精度高，容易导致召回率低，召回率高容易导致精度低，而$F_1$度量平衡了这两个部分的效果。

# 2. 分类算法
- Bayes
- Decision Tree
- SVM：支持向量机，最受工业认可
- KNN
- Logistic Regression
- 判别分析
- 感知机
- 增强和其他评估方
- BPNN(BP神经网络)
- 深度学习
- 随机森林
- 集成学习：比如有100个算法模型，然后投票决定是什么

# 3. 朴素贝叶斯

## 3.1. 条件概率
1. 指在事件B发生的情况下，事件A发生的概率，用$P(A|B)$表示，读作在B条件下的A的概率

## 3.2. 全概率公式
$P(A) = P(A|B_1) + P(A|B_2) + ... + P(A|B_N)$

## 3.3. 贝叶斯公式
1. 后验概率 = 先验概率 * 调整因子
2. $P(A|B)=P(A)*\frac{P(B|A)}{P(B)}$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/4.png)

## 3.4. 贝叶斯的例子
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/5.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/6.png)

## 3.5. 朴素贝叶斯的概率模型
1. 一个待分类项:$X = f_1, f_2, f_3,..., f_n$
2. 类别集合:$C_1, C_2, ...,C_m$
3. 需要计算:$P(C_1|X), P(C_2|X), ...,P(C_m|X)$
4. $P(f_1|C_1), P(f_2|C_1),..., P(f_n|C_1), P(f_1|C_2), ...,P(f1|C_m),...,P(f_n|C_m)$
5. 如果$P(C_k|X) = max(P(C_1|X), P(C_2|X), ...,P(C_m|X))$,则$X \in C_k, P(C_i|X) = \frac{P(X|C_i) * P(C_i)}{P(X)}$
6. $P(X|C_i)P(C_i) = P(f_1|C_i)*P(f_2|C_i),...,P(f_n|C_i)P(C_i) = P(C_i)\prod\limits_{j=1}\limits^nP(f_i|C_i)$

## 3.6. 朴素贝叶斯流程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/7.png)

# 4. 决策树
1. 决策树结点和有向边组成
2. 结点有内部结点和叶节点两种类型
3. 内部结点表示一个特征，叶节点表示一个类

## 4.1. 决策树的示例
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/10.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/9.png) |
| -------------------- | ------------------- |

## 4.2. 决策树之ID3算法

### 4.2.1. 信息熵
1. 对于有k个类别的分类问题，假定样本集合D中第k类样本所占的比例是$p_k$(k=1, 2, 3, ...,k)，则样本集合D的信息熵为:

$$
Ent(D) = -\sum\limits^k\limits_{k=1}p_k*\log_2 p_k
$$

2. 是刻画系统整体的混乱程度的量，信息熵越大，系统越混乱。

### 4.2.2. 信息增益
> 在决策树的分类问题中，信息增益是针对一个特征T，计算原有数据的信息熵与引用特征后的信息熵之差，信息增益的定义为:

$$
Gain(D, a) = Ent(D) - \sum\limits^V\limits_{v=1} \frac{|D^k|}{|D|} * Ent(D^v)
$$

### 4.2.3. 信息熵和信息增益的计算示例
> 根节点的信息熵

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/12.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/11.png)

> 部分特征的信息增益

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/13.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/14.png) |
| -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/15.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/16.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/17.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/18.png) |

> 最终计算结果:使用信息增益最大的特征作为本节点，其取值作为其他几个子节点

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/19.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/20.png) |
| -------------------- | -------------------- |

### 4.2.4. ID3算法过程描述
1. 计算给定样本分类所需的信息熵
2. 计算每个特征的信息熵、信息增益
3. 从所有特征列中选出信息增益最大的特征作为根节点或者内部结点-划分结点，其子节点分别为该特征的可能取值
4. 根据划分结点的不同取值来查分数据集为对应子节点，然后删去当前的特征列，在计算剩余列的信息熵，如果有信息增益就重复第二步直到划分结束
5. 划分结束的标志:子集只有一个类别标签，停止划分。

### 4.2.5. ID3算法的不足
1. ID3没考虑连续特征，比如长度、密度都是连续值，无法在ID3运用。
2. ID3用信息增益作为标准容易偏向取值较多的特征。然而在相同条件下，取值比较多的特征比取值少的特征信息增益大。比如一个变量有2个值，各为1/2，另一个变量为3个值，各为1/3，其实他们都是完全不确定的变量，但是取3个值比取2个值的信息增益大。如何校正这个问题？
3. ID3算法没考虑缺失值问题。
4. 没考虑过拟合问题。

## 4.3. C4.5算法
1. C4.5算法是ID3算法的改进，C4.5克服了ID3的两个缺点
   1. 不能处理连续特征
   2. 用信息增益选择属性时偏向于选择分支较多的特征值，即取值多的特征
2. <a href = "https://blog.csdn.net/zjsghww/article/details/51638126">C4.5算法实例</a>

### 4.3.1. 将连续的特征离散化
1. 将n个连续的样本按值从小到大排列，得到数据$a_1, a_2, ..., a_n$
2. 取相邻两样本值的平均数，会得到$n-1$个划分点，其中第i个划分点$T_i = \frac{a_i + a_{i+1}}{2}$
3. 对这n-1个点，分别计算每一个点作为二元分类点时的信息增益，选择信息增益最大的点作为该连续特征的二元离散分类点
4. 用信息增益比选择最佳划分
5. 注意这里还不使用信息增益率

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/21.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/22.png) |
| -------------------- | -------------------- |

### 4.3.2. 信息增益率
> 信息增益率是信息增益与特征熵的比，特征数越多的特征对应的特征熵越大。

$$
\begin{array}{l}
   Gain(D,a) = Ent(D) - \sum\limits^k\limits_{v=1}Ent(D^v) \\
   Gain_{ratio}(D,a) = \frac{Gain(D,a)}{Iv(a)} \\
   IV(a) = -\sum\limits^V\limits_{v=1}\frac{|D^v|}{|D|}\log_2\frac{|D^V|}{|D|}
\end{array}
$$

### 4.3.3. 对于缺失值处理的问题
1. 主要解决两个问题
   1. 样本某些特征缺失的情况下选择划分的属性
   2. 选定了划分属性，对于在该属性上缺失特征的样本的处理
2. 第一个问题:C4.5的想法是将数据分为两部分，每一个部分都设置权重(初始为1)，然后划分数据，一部分有特征A的D1，一部分没有特征A的数据D2，然后对于没有确实特征A的数据集D1来和对应A特征的各个特征值一起计算加权重后的信息增益比，最后乘以一个系数(系数=无特征A缺失的样本加权后所占加权总样本的比例)
3. 第二个问题:可以将缺失特征的样本同时划分入所有的子节点，不过该样本的权重按照各个子样本的数量比例来分类，比如缺失特征A的样本a之前权重为1，特征有3个特征值A1，A2，A3，分别对应的无A特征的样本个数为2，3，4，则a同时划入A1，A2，A3，对应权重调节为2/9、3/9、4/9

### 4.3.4. C4.5算法的不足与改进
1. 决策树算法很容易过拟合，所以决策树需要剪枝，而C4.5的剪枝方法有优化空间
   1. 预剪枝:生成决策树的时候决定是否剪枝
   2. 后剪枝:生成决策树，再通过交叉检验进行剪枝
2. 生成多叉树，不如二叉树计算快
3. 只能用于分类
4. 使用了熵模型，对于连续属性还有大量排序，如果为了检查模型并不希望牺牲太多准确性，使用基尼系数代替熵模型。

## 4.4. CART算法
1. Classification And Regression Tree，即分类回归树算法，简称CART算法，使用基尼系数代替信息增益比
2. 基尼系数代表了模型的不纯度，基尼系数越小，不纯度越低，特征越好，和信息增益率相反
3. 步骤:
   1. 用样本递归划分进行建树过程
   2. 用验证数据进行剪枝
4. 找出信息增益大于平均水平的，然后再找信息增益率最大的。

### 4.4.1. GINI指数
- 假设有n个类别，第k个类别的概率为$p_k$，概率分布的基尼系数表达式:

$$
\begin{array}{l}
   Gini(p) = \sum\limits^{n}\limits_{k=1}p_k(1-p_k) \\
   = 1 - \sum\limits^{n}\limits_{k=1}p_k^2 \\
\end{array}
$$

- 如果是二分类问题，第一个样本输出概率为p，概率分布的基尼系数表达式特化为$Gini(p) = 2p(1-p)$
- 对于样本D，个数为|D|，假设有n个类别，第k个类别的数量为$|C_k|$，则样本D的基尼系数表达式

$$
Gini(D) = 1 - \sum\limits_{k=1}\limits^{K}(\frac{|C_k|}{|D|})^2
$$

- 对于样本D，个数为|D|，根据特征A的某个值a，把D分为$|D_1|$和$|D_2|$，在特征A的条件下，样本D的基尼系数表达式为

$$
Gini(D, A) = \frac{|D_1|}{|D|}Gini(D_1) + \frac{|D2|}{|D|}Gini(D_2)
$$

### 4.4.2. 算法具体流程
1. 输入:训练集D，基尼系数的阈值，样本个数阈值
2. 输出:决策树T
3. 算法步骤
   1. 对当前节点的数据集D，如果样本容量小于阈值或没有特征，则返回决策子树，当前节点停止递归
   2. 计算样本集D的基尼系数，如果基尼系数小于阈值，则返回决策子树，当前节点停止递归
   3. 计算当前节点现有的各个特征的各个特征值对数据集D的基尼系数。
   4. 计算出来的各个特征的各个特征值对数据集D的基尼系数中，选择基尼系数最小的特征A和对应的特征值a，根据这个最优特征和最优特征值，把数据集划分为两部分$D_1$和$D_2$，同时建立当前节点的左右节点，左节点的数据集为$D_1$，右节点的数据集为$D_2$
   5. 对左右的字节点递归调用1-4步骤

### 4.4.3. CART例子一
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/48.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/49.png)

- 注意上面公式的最后一个

### 4.4.4. 连续特征的处理
1. 思想和C4.5完全一致的，都是将连续的特征离散化，只是将信息增益率替换成了Gini指数
2. 和ID3、C4.5的不同的是，如果当前节点为连续属性，则该属性在后面还可以参与节点的产生选择过程。

### 4.4.5. 离散数据的处理
1. 大致思路是不断二分类
2. 比如

$$
\begin{array}{l}
   A \to \{A1\},\{A2,A3\} \\
   A \to \{A2\},\{A1,A3\} \\
   A \to \{A3\},\{A1,A2\} \\
\end{array}
$$

3. 然后找到上面的基尼系数最小的组合，建立二叉树节点，然后继续划分剩下的特征

### 4.4.6. CART例子二
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/23.png)

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/24.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/25.png) |
| -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/26.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/27.png) |

## 4.5. 剪枝
1. CART树的剪枝:用验证数据集对生成的树进行剪枝并选择最优子树，损失函数最小作为剪枝的标准
2. CART分类树的剪枝策略是在度量损失的时候用基尼系数
3. (了解)CART回归树的剪枝策略是在度量损失的时候使用均方差
4. 剪枝后的CART树，通过交叉检验验证剪枝的效果，选择泛化能力最好的剪枝策略。

### 4.5.1. 剪枝损失函数
$C_a(T_i)=C(T_t) +\alpha|T_t|$

- $\alpha$是正则化参数，$C(T_t)$是训练数据的预测误差，$|T_t|$是树T的子节点个数
  - 当$\alpha = 0$时，生成的CART树记为最优子树
  - 当$\alpha \to \infty$时，正则化强度最大
- $\alpha$固定，最后的子树固定

### 4.5.2. 剪枝思路
1. 对于位于节点t的任意一棵子树
   1. 如果没有剪枝，损失函数为$C_a(T_i)=C(T_t) +\alpha|T_t|$
   2. 如果剪枝后，仅保留根节点，则损失函数为$C_a(T_i)=C(T_t) +\alpha$
2. 当$\alpha=0$或者很小的时候，$C_a(T_i) < C_a(T)$
3. 当$\alpha$增大一定程度时，$C_a(T_i) = C_a(T)$
4. 当$\alpha$继续增大时，则满足$\alpha = \frac{C(T) -C(T_i)}{|T_i|-1}$
5. $T_i$和T有相同的损失函数，但T节点更少，因此可以对子树T_t进行剪枝，也就是将它的子节点全部剪掉，变成叶子节点T

### 4.5.3. 交叉验证策略
如果我们将所有节点是否剪枝的值$\alpha$计算出来，然后针对不同$\alpha$剪枝后的最优子树做交叉验证，得到最好的$\alpha$，用对应的最优子树作为最终结果

### 4.5.4. 剪枝算法过程
1. 输入:原始决策树T
2. 输出:最优决策树$T_{\alpha}$
3. 算法过程
   1. 初始化$\alpha_{min} = \infty$，最优子树集合$w = {T}$
   2. 从叶节点开始自上而下计算内部结点t的训练误差损失函数$C_a(T_t)$(回归树为均方差，分类树为基尼系数)，叶节点树$|T_t|$，以及正则化阈值$\alpha = \min\{\frac{C(T) -C(T_i)}{|T_i|-1}, \alpha_{\min}\}$
   3. 得到所有节点的$\alpha$值为集合M
   4. 从M中选择最大的值$\alpha_k$，自上而下的访问子树t的内部节点，如果$\frac{C(T) -C(T_i)}{|T_i|-1} \leq a_k$时，进行剪枝，并决定叶节点的t的值，对于分类树，这就是概率最高的类别
   5. 最优子树集合$w=w \cup T_k，M = M - {a_k}$
   6. 如果M不为空，则回到步骤4，否则就已经得到了所有的可选最优子树集合w
   7. 采用交叉验证在w选择最优子树$T_a$

# 5. KNN算法
- KNN算法又被称为最近邻算法
- 算法思想:一个样本与数据集中的k个样本最相似，如果这k个样本中大多数属于一个类别，那么这个样本也属于这个类别

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/28.png)

## 5.1. 距离度量
1. 选择两个实例相似性时，一般使用的是欧氏距离，Lp距离定义$L_p(x_i, x_j) = (\sum\limits_{l=1}\limits^n|x_{i}^{(l)} - x_j^{(l)}|^p)^{\frac{1}{p}}$
2. 其中$x_i\in R^n, x_j \in R^n$，其中$L_{\infty}$定义为$L\infty(x_i, x_j) = max_{l}|x_i^{(l)}-x_j^{(l)}|$，其中p是一个变参数
   1. $p=1$，就是曼哈顿距离(对应L1范数)
   2. $p=2$，就是欧式距离(对应L2范数)
   3. $p \to \infty$，就是切比雪夫距离

$$
L_1定义为|x|=\sum\limits_{i=1}\limits^n|x_i|，其中x=\begin{bmatrix}
   x_1 \\ x_2 \\ . \\ . \\ . \\ x_n
\end{bmatrix} \in R^n
$$

$$
L_2定义为|x|=\sqrt{\sum\limits_{i=1}\limits^{n}x_i^2}，其中x=\begin{bmatrix}
   x_1 \\ x_2 \\ . \\ . \\ . \\ x_n
\end{bmatrix} \in R^n
$$

$$
\begin{array}{l}
   n维空间点a(x_{11},x_{12},...x_{1n})与b(x_{21}, x_{22}, ..., x_{2n}) \\
   d_{12} = \max(|x_{1i}-x_{2i}|)
\end{array}
$$

## 5.2. K值的选择
1. 近似误差:对现有训练集的训练误差
2. 估计误差:对测试集的测试误差，估计误差小，说明对未知数据的预测能力好
3. K值较小，则是在较小的邻域中的训练实例进行预测，容易导致过拟合。
   1. 学习的近似误差会减小:只有输入实例较近的训练实例才会对预测结果起作用
   2. 学习的估计误差会增大:预测结果会对紧邻的实例点敏感，但是如果是噪声会导致预测出错
4. K值较大，则是在较大的邻域中的训练实例进行预测
   1. 学习的估计误差会减小
   2. 学习的近似误差会增大
5. K值一般选择样本数量的平方根

## 5.3. 算法描述
1. 计算已知类别数据集中点与当前点之间的距离
2. 按照距离增次序排序
3. 选取与当前点距离最小的k个点
4. 统计前k个点所在的类别出现的频率
5. 返回前k个点出现频率最高的类别作为当前点的预测分类
   1. 投票法:可以选择K个点出现频率最高的类别作为预测结果
   2. 平均法:可以计算K个点的实值输出标记的平均值作为预测结果
   3. 加权平均法:根据距离远近完成加权平均等方法

## 5.4. 算法优点
1. 简单有效
2. 重新训练代价低
3. 算法复杂度低
4. 适合类域交叉样本
5. 适用大样本自动分类

## 5.5. 算法缺点
1. 惰性学习
2. 类别分类不标准化
3. 输出可解释性不强
4. 不均衡性
5. 计算量较大

## 5.6. KNN算法的Sklearn实现
> Sklearn KNN声明

```py
def KNeighborsClassifier(n_neighbors = 5,
                       weights='uniform',
                       algorithm = '',
                       leaf_size = '30',
                       p = 2,
                       metric = 'minkowski',
                       metric_params = None,
                       n_jobs = None
                       )
```
1. n_neighbors：KNN 中的"K"，一般默认值为5。
   1. K值较小，就相当于用较小的领域中的训练实例进行预测，训练误差近似误差小(偏差小)，泛化误差会增大(方差大)，换句话说，K值较小就意味着整体模型变得复杂，容易发生过拟合；
   2. K值较大，就相当于用较大领域中的训练实例进行预测，泛化误差小(方差小)，但缺点是近似误差大(偏差大)，换句话说，K值较大就意味着整体模型变得简单，容易发生欠拟合；一个极端是K等于样本数m，则完全没有分类，此时无论输入实例是什么，都只是简单的预测它属于在训练实例中最多的类，模型过于简单。
2. weights(权重)：最普遍的 KNN 算法无论距离如何，权重都一样，但有时候我们想搞点特殊化，比如距离更近的点让它更加重要。这时候就需要 weight 这个参数了，这个参数有三个可选参数的值，决定了如何分配权重。参数选项如下
   1. uniform：不管远近权重都一样，就是最普通的 KNN 算法的形式。
   2. distance：权重和距离成反比，距离预测目标越近具有越高的权重。
   3. 自定义函数：自定义一个函数，根据输入的坐标值返回对应的权重，达到自定义权重的目的。
3. leaf_size：这个值控制了使用kd树或者球树时，停止建子树的叶子节点数量的阈值。
   1. 值越小，生成的kd树和球树越大，层数越深，建树时间越长。随着样本的数量增加，这个值也在增加，但是过大可能会过拟合，需要通过交叉检验来选择。
   2. 默认值为30
4. algorithm：在 sklearn 中，要构建 KNN 模型有三种构建方式，而当 KD 树也比较慢的时候，则可以试试球树来构建 KNN。参数选项如下：
   1. brute:蛮力实现直接计算距离比较，适用于小数据集
   2. kd_tree:使用 KD 树构建 KNN 模型，适用于比较大数据集
   3. ball_tree:使用球树实现 KNN，适用于KD树解决起来更复杂
   4. auto:默认参数，自动选择合适的方法构建模型.不过当数据较小或比较稀疏时，无论选择哪个最后都会使用 'brute'
5. p：和metric结合使用的，当metric参数是"minkowski"的时候，p=1为曼哈顿距离， p=2为欧式距离。默认为p=2。
6. metric：指定距离度量方法，一般都是使用欧式距离。
   1. euclidean：欧式距离，$p=2$
   2. manhattan：曼哈顿距离，$p=1$
   3. chebyshev：切比雪夫距离，$p=\infty，D(x, y) = \max|x_i - y_i|(i = 1, 2, ..., n)$
   4. minkowski：闵可夫斯基距离，默认参数，$\sqrt[q]{\sum\limits_{i=1}\limits^n(|x_i-y_i|)^p}$
7. n_jobs：指定多少个CPU进行运算，默认是-1，也就是全部都算。
8. radius：限定半径，默认为1，半径的选择与样本分布有关，可以通过交叉检验来选择一个比较小的半径
9. outlier_labe:int类型，主要用于预测时，如果目标点半径内没有任何训练集的样本点时，应该标记的类别，不建议选择默认值 None,因为这样遇到异常点会报错。一般设置为训练集里最多样本的类别。

### 5.6.1. KNN进行鸢尾花数据集分类
1. 通过对比效果来找到合适的K值。

```py
from sklearn.datasets import load_iris
from sklearn.model_selection  import cross_val_score
import matplotlib.pyplot as plt
from sklearn.neighbors import KNeighborsClassifier

#读取鸢尾花数据集
iris = load_iris()
x = iris.data
y = iris.target
k_range = range(1, 31)
k_error = []
#循环，取k=1到k=31，查看误差效果
for k in k_range:
    knn = KNeighborsClassifier(n_neighbors=k)
    #cv参数决定数据集划分比例，这里是按照5:1划分训练集和测试集
    scores = cross_val_score(knn, x, y, cv=6, scoring='accuracy')
    k_error.append(1 - scores.mean())

#画图，x轴为k值，y值为误差值
plt.plot(k_range, k_error)
plt.xlabel('Value of K for KNN')
plt.ylabel('Error')
plt.show()
```

2. 执行KNN算法

```py
import matplotlib.pyplot as plt
from numpy import *
from matplotlib.colors import ListedColormap
from sklearn import neighbors, datasets

n_neighbors = 11

# 导入一些要玩的数据
iris = datasets.load_iris()
x = iris.data[:, :2]  # 我们只采用前两个feature,方便画图在二维平面显示
y = iris.target


h = .02  # 网格中的步长

# 创建彩色的图
cmap_light = ListedColormap(['#FFAAAA', '#AAFFAA', '#AAAAFF'])
cmap_bold = ListedColormap(['#FF0000', '#00FF00', '#0000FF'])


#weights是KNN模型中的一个参数，上述参数介绍中有介绍，这里绘制两种权重参数下KNN的效果图
for weights in ['uniform', 'distance']:
    # 创建了一个knn分类器的实例，并拟合数据。
    clf = neighbors.KNeighborsClassifier(n_neighbors, weights=weights)
    clf.fit(x, y)

    # 绘制决策边界。为此，我们将为每个分配一个颜色
    # 来绘制网格中的点 [x_min, x_max]x[y_min, y_max].
    x_min, x_max = x[:, 0].min() - 1, x[:, 0].max() + 1
    y_min, y_max = x[:, 1].min() - 1, x[:, 1].max() + 1
    xx, yy = np.meshgrid(np.arange(x_min, x_max, h),
                         np.arange(y_min, y_max, h))
    Z = clf.predict(np.c_[xx.ravel(), yy.ravel()])

    # 将结果放入一个彩色图中
    Z = Z.reshape(xx.shape)
    plt.figure()
    plt.pcolormesh(xx, yy, Z, cmap=cmap_light)

    # 绘制训练点
    plt.scatter(x[:, 0], x[:, 1], c=y, cmap=cmap_bold)
    plt.xlim(xx.min(), xx.max())
    plt.ylim(yy.min(), yy.max())
    plt.title("3-Class classification (k = %i, weights = '%s')"
              % (n_neighbors, weights))

plt.show()
```

# 6. 集成学习
- 集成学习并不是简单地将数据集在多个不同分类器上重复训练，而是对数据集进行扰动
- 一个分类训练中的错误还可以被下一个分类器进行利用
- 分类器预测错误的原因是未知的实例与学习的实例的分布有区别，通过扰动，分类器可以学习到更加一般的模型，从而消除单个分类器产生的偏差，而得到更为精准的模型。

## 6.1. 什么是集成学习法(Ensemble learning)
1. 集成学习法通过多个分类学习方法聚集一起来提高分类准确率，提高模型的稳定性
2. 通常情况下，一个集成分类器的分类型能要好于单个分类器
3. 集成学习法由训练数据构建一组基分类器(base classifier)，然后通过对每个基分类器的预测进行投票来实现分类。
4. 在构建分类器的过程中，一般有两种集成方法
   1. 一种是使用训练集的不同自己训练得到不同的基分类器
   2. 另一种方法是使用同一个训练集的不同属性子集训练得到不同的基分类器

## 6.2. 集成学习的基本思想
在原始数据集上构建多个分类器，然后在分类未知样本时聚集它们的预测结果。

## 6.3. 构建集成分类器的过程描述

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/50.png)

- 上图是集成学习法的逻辑结构图

## 6.4. 构建集成分类器的方法

### 6.4.1. 通过处理训练数据集
1. 它根据某种抽样分布，通过对原始数据进行再抽样来得到多个训练集然后使用特定的学习算法为每个训练集建立一个分类器。
2. 典型的处理训练数据集的组合方法有装袋(bagging)和提升(boosting)

### 6.4.2. 通过处理输入特征
1. 在这种方法中，通过选择输入特征的自己来形成每个训练集。一些研究表明，对那些含有大量冗余特征的数据集，这种方法的性能非常好。
2. 随机森林(Random forest)就是一种处理输入特征的组合方法

### 6.4.3. 通过处理类标号
1. 这种方法适用于类数足够多的情况。通过将类标号随机划分成两个不相交的子集A0和A1，把训练数据变换为二类问题，类标号属于子集A0的训练样本指派到类0，而那些类标号属于子集A1的训练样本指派到类1。
2. 然后使用重新标记过的数据来训练一个基分类器，重复重新标记类和构建模型步骤多次，就得到一组基分类器
3. 当遇到一个检验样本时，使用每个基分类器Ci预测它的类标号。
   1. 如果被预测为类0，则所有属于A0的类都得到一票
   2. 如果被预测为类1，则所有属于A1的类都得到一票
4. 最后统计选票，将检验样本指派到得票最高的类。

### 6.4.4. 通过处理学习算法
1. 在同一个训练集上执行不同算法而得到不同的模型。

## 6.5. 集成分类器方法的优缺点
1. 优点:集成分类器的应用，克服了单一分类器的诸多缺点，比如对样本的敏感性，难以提高分类精度等
2. 缺点:集成分类器的性能优于单个分类器，必须满足基分类器之间完全独立，但时间上很难保证基分类器之间完全独立

# 7. SVM 支持向量机

## 7.1. 线性划分和非线性划分
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/29.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/30.png) |
| -------------------- | -------------------- |

## 7.2. 分类标注的起源：逻辑回归
1. 逻辑回归的目的是从特征学习出一个0/1分类模型，而这个模型是将特征的线性组合作为自变量，由于自变量的取值范围是负无穷到正无穷，因此我们使用sigmoid函数将自变量映射到(0, 1)上，映射后的值被认为是属于y=1的规律。

$$
\begin{array}{l}
   sigmoid(x) = \frac{1}{ 1 + e^{-x}} \\
   h_\theta(x) = g(\theta^Tx) = \frac{1}{1+e^{-\theta^Tx}}
\end{array}
$$

2. $h_\theta(x)$只和$\theta^Tx$有关，如果$\theta^Tx>0.5$，则$h_\theta(x)>0.5$
3. 希望模型达到的目标就是让训练集中y=1的特征$\theta^Tx>>0$，而y=0的特征$\theta^Tx<<0$
4. 对于更高维的情况，我们可以得到下式$\theta^Tx = w^Tx + b$

## 7.3. 函数间隔(Functional margin)与几何间隔(Geometrical margin)

### 7.3.1. 函数间隔
1. 函数间隔$\hat{\gamma} = y(w^Tx+b) = yf(x)$
2. 超平面(w, b)关于T中所有样本点的最小函数间隔即为超平面(w, b)关于训练数据集T的函数间隔

$$
\hat{\gamma} = \min\hat{\gamma},(i = 1, ..., n)
$$

3. 函数间隔存在问题，如果成比例修改w和b会导致函数间隔的值f(x)变为原来2倍。

### 7.3.2. 几何间隔
1. 我们对于点x，令其垂直投影到超平面上的点$x_0$，w是垂直于超平面的向量，$\gamma$是样本x到分类间隔的距离

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/53.png)

2. 有$x = x_0 + \gamma\frac{w}{||w||}$，其中||w||是范数
3. 又因为$x_0$在平面上，所以$f(x_0)=0$，代入超平面的方程可以计算出

$$
\gamma = \frac{f(x)}{||w||}
$$

4. 为了获取$\gamma$的绝对值，使其乘以其类别，得到几何间隔

$$
\hat{\gamma} = y\gamma = \frac{\hat{\gamma}}{||w||}
$$

## 7.4. 最大分离器Maximum Margin Classifier的定义
1. 最大间隔分类器的目标函数为$\max\hat{\gamma}$
2. 其他满足条件:$y_i(w^Tx_i + b) = \hat{\gamma_i}\geq\hat{\gamma}, i = 1,...,n$
3. 如果函数间隔$\hat{\gamma}$为1，上述目标函数在转化为

$$
\max\frac{1}{||w||}, s.t.\ y_i(w^Tx_i + b) \geq 1, i = 1, ..., n
$$

## 7.5. 如何寻找到最优超平面
1. 最大化距离:最大化距离可以为模型带来比较好的泛化能力

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/31.png)

2. 支持向量的图形化表示

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/32.png)

3. 最初优化问题:我们选择最大间距作为这个优化问题的最优解，也就是使得$\frac{2}{||w||}$的值最大，并且满足一下两个约束条件
   1. $(wx+b) \geq 1, \forall$ x in class 1
   2. $(wx+b) \leq -1, \forall$ x in class 2

4. 线性分类器
   1. $w^Tx + b = 0$
   2. $f(x) = w^Tx +b$

## 7.6. 决策边界

### 7.6.1. 线性分类边界
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/33.png)

### 7.6.2. 非线性分类边界
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/34.png)

> 使用二次曲线进行划分

## 7.7. 支持向量机
1. 我们想要通过一条尽可能好的直线(超平面)将两类不同的物体分开。
2. 数据:
   1. 训练集:$(x_1,y_1),...,(x_n,y_n)$
   2. 对于每一个例i:
      1. $x_i = \{x_i^{(1)}, ... , x_i^{(d)}\}$，$x_i^{(j)}是实数$
      3. $y_i \in \{-1, +1\}$
   3. 向量内积:$w*x = \sum\limits_{j=1}\limits^{d}w^{(j)}*x^{(j)}$
   4. 什么是被$w$定义的最佳的线性分类器?

### 7.7.1. 最大距离
1. 距分离超平面的距离对应于预测的"置信度"
2. 在下图中，我们认为A和B是左侧类的概率比C大。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/35.png)

3. Margin $\gamma$:距离分类直线或超平面最近的一个点的距离。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/36.png)

3. 之所以以这种方式定义边距，是因为理论上的边界以及依赖于边距值的泛化误差范围的存在。

### 7.7.2. 为什么最大距离是好的
1. 点积:$A * B = ||A|| * ||B|| * \cos \theta$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/37.png)

2. $\gamma$和间距是线性正相关，所以是可以的

### 7.7.3. 距离如何表示

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/38.png)

### 7.7.4. 最大距离的求解
1. 预测值 = $sign(w*x+b)$
2. 置信度(Confidence) = $(w*x + b)y$
3. 对于第i个数据点:$\gamma_i = (w*x_i + b)y_i$
4. 解决的问题:$\max\limits_w\min\limits_i\gamma_i$
5. 重新解释为:求解$\max\limits_{w,\gamma}\gamma s.t.\forall i, y_i(w*x_i + b) \geq \gamma$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/39.png)

## 7.8. 规范超平面
1. 转化问题:$(2wx + 2b)y = 2\gamma$
2. 一般化w:$\gamma = (\frac{w}{||w||} * x + b) y$
3. 当然提供**支持向量**$x_j$在差平面上被定义为$w*x_j + b = \pm 1$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/40.png)

- 前提条件
$$
\begin{array}{l}
   x_1 = x_2 + 2 \gamma\frac{w}{||w||} \\
\ \\
   w * x_1 + b = +1 \\
   w * x_2 + b = -1 \\
\end{array}
$$

- 计算$\gamma$

$$
\begin{array}{l}
   w * x_1 + b = + 1 \\
   w (x_2 + 2\gamma\frac{w}{||w||}) + b = + 1 \\
   \ \\
   w * x_2 + b + 2\gamma\frac{w}{||w||} = + 1 \\
   \ \\
   \gamma = \frac{||w||}{w * w} = \frac{1}{||w||} \\   
\end{array}
$$

## 7.9. 通过上述化简后最大距离
$$
\arg \max\gamma = arg \arg\min\frac{1}{||w||} = \arg\min\frac{1}{2}||w||^2
$$

- 支持向量机的强约束条件:

$$
\min\limits_w\frac{1}{2}||w||^2 \\
s.t. \forall i, y_i(w * x_i + b) \geq 1
$$

## 7.10. 非线性分析
1. 如果数据不是线性可分的，那么我们需要添加惩罚项C

$$
\min\limits_w\frac{1}{2}||w||^2 + C \\
\ \\
s.t. \forall i, y_i(w * x_i + b) \geq 1
$$

2. 通过交叉检验法确定C的值
3. 所有的错误并不是一样的坏
4. 引入宽松量$\xi_i$

$$
\min\limits_{w,b,\xi_i \geq 0} \frac{1}{2} * ||w||^2 + C*\sum\limits_{i=1}\limits^{n}\xi_i \\
\ \\
s.t. \forall i, y_i(w*x_i + b) \geq 1 - \xi_i
$$

5. 如果$x_i$位于错误的一边，那么他将会有惩罚项$\xi_i$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/41.png)

### 7.10.1. Slack Penalty C
1. 当C是无穷时，我们只希望通过w和b来分开数据
2. 当C是0时，我们无论设置$\xi_i$是多少，w都是0，也就是忽略了数据

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/42.png)

### 7.10.2. 支持向量机的自然形式
$$
\arg\min\limits_{w,b}\frac{1}{2}w*w + C*\sum_{i=1}^{n}\max\{0,1-y_i(w*x_i+b)\}
$$

- $w * w$:距离
- $C$:正则化参数
- $\sum_{i=1}^{n}\max\{0,1-y_i(w*x_i+b)\}$:经验损失L(我们如何拟合训练数据)
- SVM使用"Hinge Loss":max{0, 1-z}

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/43.png)

## 7.11. 如何计算距离
$$
\min\limits_{w,b}\frac{1}{2}w*w + C*\sum_{i=1}^{n}\xi_i \\
s.t. 
\forall i,y_i*(x_i * w + b) \geq 1 - \xi_i
$$

- 使用二次求解器
  - 最小化二次函数
  - 受到线性约束
- 问题:求解器对于大数据效率低下！

$f(w,b) = \frac{1}{2} w * w + C*\sum_{i=1}^{n}\max\{0,1-y_i(w*x_i+b)\}$

- 如何最小化凸函数g(z):切线
- 使用梯度下降法

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/44.png)

## 7.12. 如何计算w
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/45.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/46.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/47.png)

# 8. 深入SVM

## 8.1. 从线性可分到线性不可分到线性不可分

### 8.1.1. 从原始问题到对偶问题求解
1. 等价问题转化

$$
\max\frac{1}{||w||}, s.t.\ y_i(w^Tx_i + b) \geq 1, i = 1, ..., n \\
转化为 \\
\min \frac{1}{2}||w||^2, s.t.\ y_i(w^Tx_i + b) \geq 1, i = 1, ..., n \\
$$

1. 我们可以看到目标函数是二次的，约束条件是线性的，所以其实一个凸二次规划问题。
2. 由于问题的特殊性，我们可以根据拉格朗日对偶性对换到对偶变量的优化问题，即通过求解与原问题等价的对偶问题得到原始问题的最优解，优点如下
   1. 对偶问题更容易求解。
   2. 便于引入核函数，推广到非线性分类问题。
3. 拉格朗日对偶性：通过给每一个约束条件加上一个拉格朗日乘子$\alpha$

$$
L(w, b, \alpha) = \frac{1}{2}||w||^2 - \sum\limits_{i=1}\limits^n\alpha_i*(y_i(w^T*x_i + b) - 1) \\
\theta(w) = \max\limits_{\alpha_i\geq 0}L(w, b ,\alpha) \\
$$

4. 容易验证，如果某个约束条件不满足，则$\theta(w) = \infty$，当所有的约束条件满足时，则有$\theta(w) = \frac{1}{2}||w||^2$，即最初要最小化的值。
5. 即将问题转化为求解

$$
\min\limits_{w, b}\theta(w) = \min\limits_{w, b}\max\limits_{\alpha_i\geq 0}L(w, b ,\alpha) = p^*
$$

6. 这样是不容易求解的我们将最大和最小进行交换，得到

$$
\max\limits_{\alpha_i\geq 0}\min\limits_{w, b}L(w, b ,\alpha) = d^*
$$

7. 我们可以知道有$d^*\leq p^*$(在满足K.K.T.条件时等价)，对偶问题更容易求解，下面先求L对w和b的极小，再求L对$\alpha$的极大

### 8.1.2. K.K.T.条件
1. 一般最优化数学模型能表示为如下标准形式

$$
\min f(x) \\
s.t. h_j(x) = 0, j = 1, ..., p\\
g_k(x)\leq 0, k = 1, ..., q \\
x \in X \subset R^n \\
$$

- f(x)是需要最小化的函数，h(x)是等式约束，g(x)是不等式约束，p和q分别为等式约束和不等式约束的数量。

2. 凸优化:$X\subset R^n$是一凸集，f:X->R为一凸函数，凸优化就是要找出一点$x^* \in X$，使得每一个$x \in X$满足$f(x^*) \leq f(x)$
3. KKT条件的意义:是一个非线性规划问题能有最优解的必要和充分条件。

> KKT条件：对之前的标准形式最优化数学模型，如果满足
> 1. $h_j(x^*) = 0, j = 1, ..., p，g_k(x^*) \leq 0, k = 1, ..., q$
> 2. $\triangle f(x^*) + \sum\limits_{j=1}\limits^p\lambda_j\triangle h_j(x^*) + \sum\limits_{j=1}\limits^p\mu_k\triangle g_k(x^*) = 0, \lambda_j \neq 0, u_k \geq 0, \mu_kg_k(x^*) = 0$
> 作为满足KKT条件

### 8.1.3. 对偶问题求解的三个步骤
1. 第一步：固定$\alpha$，对w和b分别求偏导，带回L并化简(最后一步，注意$\sum\limits_{i=1}\limits^n\alpha_iy_i = 0$)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/56.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/55.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/54.png)

2. 第二步：求对$\alpha$的极大

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/57.png)

3. 第三步：计算完成$L(w, b, \alpha)$关于w和b的最小化，以及与$\alpha$的极大之后，最后就是使用SMO算法求解对偶问题中的拉格朗日乘子$\alpha$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/58.png)

### 8.1.4. 线性不可分问题
1. 对于一个数据点进行分类，实际上是将x代入$f(x) = w^Tx+b$计算出结果，根据正负号进行类别划分。

$$
\begin{array}{l}
   \because w^* = \sum\limits_{i=1}\limits^{n}\alpha_iy_ix_i \\
   \therefore f(x) = (\sum\limits_{i=1}\limits^{n}\alpha_iy_ix_i)^T x + b \\
   = \sum\limits_{i=1}\limits^{n}\alpha_iy_i<x_i, x> + b   
\end{array}
$$

2. 也就是对新点预测，只需要计算其与训练数据点的内积即可：非支持向量对应的$\alpha=0$，这些点不影响分类

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/59.png)

## 8.2. SVM：核函数：kernel

### 8.2.1. 特征空间的隐式映射：核函数
1. 对于非线性情况，SVM选择一个核函数K(·,·)，通过将数据映射到高维空间，来解决在原始空间中线性不可分的问题。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/61.png)

2. 非线性分类器模型:$f(x) = \sum\limits_{i=1}\limits^Nw_i\phi(x)+b$，建立非线性份分类器步骤
   1. 首先用非线性映射将数据变换到一个特征空间F：重点
   2. 在特征空间使用线性分类器进行分类
3. 非线性决策规则:

$$
f(x) = \sum\limits_{i=1}\limits^l\alpha_iy_i<\phi(x_i), \phi(x)>+b
$$

### 8.2.2. 核函数：如何处理非线性数据
1. 将非线性数据映射为线性数据

#### 8.2.2.1. 二维空间描述
$$
a_1X_1+a_2X_1^2+a_3X_2+a_4X_2^2+a_5X_1X_2+a_6=0
$$

#### 8.2.2.2. 从二维空间到五维空间映射
$$
Z_1=X_1,Z_2=X_1^2,Z_3=X_3,Z_4=X_4,Z_5=X_1X_2
$$

#### 8.2.2.3. 五维空间描述(线性超平面)
$$
\sum\limits_{i=1}\limits^5a_iZ_i + a_6 = 0
$$

#### 8.2.2.4. 计算方法
> 假设有两个变量$x_1 = (\eta_1, \eta_2)^T, x_2 = (\xi_1,\xi_2)^T$

1. 方法一：映射后的内积为

$$
<\phi(x_1), \phi(x_2)> = \eta_1\xi_1 + \eta_1^2\xi_1^2 + \eta_2\xi_2 + \eta_2^2\xi_2^2 + \eta_1\eta_2\xi_1\xi_2
$$

2. 方法二：平方，在低维空间计算，如果遇到维度爆炸，前一种可能无法计算

$$
\begin{array}{l}
   (<x_1, x_2> + 1)^2 = 2\eta_1\xi_1 + \eta_1^2\xi_1^2 + 2\eta_2\xi_2 + \eta_2^2\xi_2^2 + 2\eta_1\eta_2\xi_1\xi_2 + 1 \\
   等价于 \\
   \phi(x_1, x_2) = (\sqrt{2}x_1, x_1^2, \sqrt{2}x_2,x_2^2,\sqrt{2}x_1x_2,1)^T \\   
\end{array}
$$

### 8.2.3. 核函数
1. 计算两个向量在隐式映射过后的空间中的内积的函数叫做核函数
2. 上例中为$K(x_1, x_2) = (<x_1, x_2> + 1)^2$
3. 分类函数为:$f(x) = \sum\limits_{i=1}\limits^Na_iy_iK(x_i, x)+b$

### 8.2.4. 常见核函数
1. 多项式核:$K(x_1, x_2) = (<x_1, x_2> + R)^d$，空间维度为$C_{m+d}^d$，原始空间维度为m
2. 高斯核:$K(x_1,x_2) = \exp^{-\frac{||x_1-x_2||^2}{2\delta^2}}$，$\delta$影响高次特征上权重衰减的速度

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/60.png)

3. 线性核:$K(x_1,x_2) = <x_1, x_2>$

## 8.3. 使用松弛变量处理outliers方法
1. 如果有些情况下数据有噪声，我们称偏离正常位置很远的数据点为outlier

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/62.png)

2. 噪声点对目前的SVM有比较大的影响，我们通过允许数据点在一定程度上偏离超平面来解决这个问题。
3. 原本约束条件为:$y_i(w^Tx_i+b)\geq 1,i =1,...,n$
4. 新的约束条件为:$y_i(w^Tx_i+b)\geq 1 - \xi_i,i =1,...,n$
5. $\xi_i$是松弛变量，对应数据点$x_i$允许偏离函数间隔的距离，对应的我们应该修正我们的优化问题：$\min \frac{1}{2}||w||^2 + C\sum\limits_{i = 1}\limits^n\xi_i$
   1. 参数C:控制目标函数"寻找margin最大的超平面"和"保证数据点偏差量最小"之间的权重，实现确定好的变量。
   2. 参数$\xi$是需要优化的变量
6. 新的拉格朗日函数如下

$$
L(w, b, \xi, \alpha, r) = \frac{1}{2}||w||^2 + C\sum\limits_{i=1}\limits^n\xi_i - \sum\limits_{i=1}\limits^n\alpha_i(y_i(w^Tx_i+b) - 1 + \xi_i) - \sum\limits_{i=1}\limits^nr_i\xi_i
$$

7. 分析方法和上面相同

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/63.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec6/64.png)

# 9. 证明SVM
1. 比较复杂，参见参考五

# 10. 参考
1. <a href = "https://www.cnblogs.com/keye/p/10267473.html">决策树算法原理(ID3，C4.5)</a>
2. <a href = "https://www.cnblogs.com/lovephysics/p/7231294.html">决策树(ID3 )原理及实现</a>
3. <a href = "https://www.cnblogs.com/keye/p/10564914.html">决策树算法原理(CART分类树)</a>
4. <a href = "https://blog.csdn.net/sinat_30353259/article/details/80901746">机器学习之KNN(k近邻)算法详解</a>
5. 《支持向量机通俗导论(理解SVM的三层境界)》
6. <a href = "https://blog.csdn.net/laobai1015/article/details/82763033">SVM的Python实现</a>
7. <a href = "https://www.cnblogs.com/shenxiaolin/p/8854838.html">Sklearn实现鸢尾花数据集</a>
8. <a href = "https://www.cnblogs.com/listenfwind/p/10685192.html">深入浅出KNN算法(二) sklearn KNN实践</a>
9. <a href = "https://blog.csdn.net/qq_40195360/article/details/86714337">【实现思路好】KNN 原理及参数总结</a>