Book12-面向过程建模
---

# 1. 过程建模：世界是复杂过程的集合
1. 过程建模是分析需求获取活动获得的信息，发现系统的功能以及和外界的交互，建立能够实现系统功能的过程分解模型，形成系统的过程模型。
2. 复杂过程逐步分解为小过程，并建立过程之间的联系

## 1.1. 数据流图

### 1.1.1. DFD图基本元素
1. 外部实体：待构建系统之外的人、组织、设备或其他软件系统，不受系统的控制，联合构成外部上下文环境
2. 过程：施加于数据的动作或行为，被转换、被存储或被分布
3. 数据流：数据的运动，是系统与其环境之间或者系统内两个过程之间的通信形式，可以完成数据流合并和组合
4. 数据存储：软件系统内部的收集和保存

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/47.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/48.png) |
| ---------------------- | ---------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/49.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/50.png) |

### 1.1.2. 简单的示例图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/51.png)


### 1.1.3. 规则
1. 过程是对数据的处理，必须有输入，也必须有输出，而且输入数据集和输出数据集应该存在差异
2. 数据流必须和过程关联

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/52.png)

3. 唯一标识(过程动词，数据和实体名词)

## 1.2. 分层结构

### 1.2.1. 上下文图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/53.png)

1. (用例图)转换为上下文图
2. 上下文图：数据流图最高层次的图

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/54.png)

### 1.2.2. 图：0层图
1. 上下文图单一过程的描述
2. 单一过程的第一次功能分解
3. 系统的功能概图
4. 简洁、清晰

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/1.png)

### 1.2.3. 图：N层图
1. 更细节的分解，父图与子图
2. 低于0层图的子图一般不显示**外部实体**
3. 平衡、分解停止条件：原始过程和数据

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/55.png)

## 1.3. 层次结构的建立
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/2.png)

1. 整个过程是循环往复的。

### 1.3.1. 创建上下文图
1. 明确系统的功能范围

### 1.3.2. 发现并建立DFD片段
1. 从获取的用户需求中寻找和发现系统的功能要求，然后加以归纳和概括，在0层图中描述。
2. 先构建DFD片段，然后概括归纳得到0层图
3. DFD片段是系统对某个事件的响应过程的数据流图描述，是系统中发生的重要事件创建的。

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/3.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/4.png) |
| --------------------- | --------------------- |

### 1.3.3. 根据数据流图片段组合产生0层图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/5.png)

1. 上图是比较简单的一个拼接例子
2. 比较复杂的参考图12-8
3. 准则
   1. 没有语法错误
   2. 具有良好的语义
   3. 保持数据一致性
   4. 控制复杂度

### 1.3.4. 对0层图的过程进行功能分解，产生N层图
1. 将单个复杂的过程变为多个更加具体、更加精确和更加细节化的过程。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/6.png)

2. 注意分解的平衡性：要求数据流子图的**输入流、输出流**必须和父过程的输入、输出流保持一致。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/7.png)

3. 终止条件
   1. 过程已经简化为一个选择、计算或数据库操作
   2. 所有数据存储都是单一实体
   3. 用户不关系比子图更细节的内容，或子图已经足够支撑了
   4. 每个数据流不需要更加细分了
   5. ...

# 2. 逻辑说明——微规格说明
1. 微规格说明是用来描述过程处理逻辑的技术，包括结构化自然语言、行为图和决策表/树

## 2.1. 结构化自然语言
1. 结构化英语(不是伪代码)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/8.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/9.png)

## 2.2. 行为图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/10.png)

## 2.3. 决策表
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/11.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/12.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/14.png)

## 2.4. 决策树
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/13.png)

## 2.5. 方法选择
1. 结构化英语：存在很多重复行动，或与用户交流是重要的。
2. 决策表：存在条件、行动和规则的复杂组合，或要求完备性。
3. 决策树：条件或行动顺序很重要，或者表很稀疏

# 3. 数据说明——数据字典
1. 数据字典会有组织地流出数据流图中涉及的所有数据元素(数据流和数据存储)，并定义其描述信息。
2. 要求描述数据元素精确，会使用BNF的严格说明技术。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/15.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/16.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/17.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/18.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/19.png)

# 4. DFD的验证
1. 验证数据流图的语法
2. 验证数据流图的结构
3. 验证数据流图的语义

# 5. 实例：电梯控制系统
课本311页

# 6. 模块结构图

## 6.1. 功能分解图
1. 又称功能层次图(FHD)，一个图自上而下显示系统的功能分解。
2. 不包含先后顺序，仅仅是列举

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/20.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/21.png) |
| ---------------------- | ---------------------- |

## 6.2. 过程依赖图
1. 描述功能和过程之间的依赖关系。
   1. 数据依赖：一个过程需要另一个过程产生的数据
   2. 资源依赖：一个过程需要另一个过程产生的资源
   3. 约束依赖：一个过程需要另一个过程设置的约束条件。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book12/22.png)

1. 实心圆点：过程可选
2. 箭头方向：依赖方向
3. 三角叉：可能多次出现。