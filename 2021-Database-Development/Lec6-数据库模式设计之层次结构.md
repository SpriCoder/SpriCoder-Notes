
0.1. Lec6-数据库模式设计之层次结构
---

# 1. 处理层次结构（Hierarchical Data）
1. 树状结构（Tree Structures）
   1. 历史
      1. 层次数据库
      2. 网状数据库：灵活但是还是存在困难
      3. 关系型数据库
         1. 在效率、灵活等方面找到了一个平衡点
         2. 没有必要将配置文件存储到数据库中，存储在文件系统也是很好的一个选择
   2. 直到关系理论出现，数据库设计是"科学（science）"而非"工艺（craft）"
      1. 层次性数据广泛存在（XML，LDAP，BOM…）
   3. 层次结构复杂度在于
      1. 访问树的方式

# 2. 树状结构 VS. 主从结构
1. 父子结构（parent/child link）--tree structure
2. 主从结构（master/detail relationship）：通过外键，来形成主从结构
3. 差异
   1. 树状结构保存只需要一张表：代表层次的树。所有节点的类型都相同，节点的属性都相似，表(节点)和自己有主从关系而不是其他表
   2. 深度：主从结构没有深度的概念
   3. 所有权：主从结构可以明确外键完整性约束，但是树状结构不需要定义所有权
   4. 多重父节点：单一父节点描述父子关系(子节点引用父节点)，先解决单一父节点的树
4. 参考书籍：Fabian Pascal：Practical Issues in Database Management（Addion Wesley）

# 3. 层次结构的实际案例
1. Risk exposure
2. 档案位置
3. 原料使用
4. ……
5. 不同的案例具有不同的基本特征
6. 通常，树中的节点数量偏小。实际上，这也是树的优点，便于高效检索

```sql
select building.name building,
  floor.name floor,
  room.name room,
  alley.name alley,
  cabinet.name cabinet,
  shelf.name shelf,
  box.name box,
  folder.name folder
from inventory,
  location folder,
  location box,
  location shelf,
  location cabinet,
  location alley,
  location room,
  location floor,
  location building
where inventory.id = 'AZE087564609'
  and inventory.folder = folder.id
  and folder.located_in = box.id
  and box.located_in = shelf.id
  and shelf.located_in = cabinet.id
  and cabinet.located_in = alley.id
  and alley.located_in = room.id
  and room.located_in = floor.id
  and floor.located_in = building.id
```

# 4. 用SQL数据库描述树结构
1. 只要对象的类型相同，而对象的层树可变，其关系就应该被建模为树结构
2. 在数据库设计中，树通常三种模型
   1. Adjacency model 邻接模型
      1. 层次中父节点id作为子节点id的一个属性pid，不能确定兄弟节点的排序
      2. 难以处理的，是递归的
   2. Materialized path model 物化路径模型
      1. 将树中间的每一个节点和在树中的位置描述成数据的结合
      2. 是所有子节点的祖先节点的id的串联(1.2.3)
      3. 能够知道兄弟节点之间的排名，家谱
   3. Nested set model 嵌套集合模型 1996
      1. 每一个节点被赋予了一对数字(left number, right number)
      2. 父节点的左数字和右数字之间包含了它所有的子节点的左数字、右数字
3. <a href = "http://www.kessler-web.co.uk">数据来源</a>

# 5. 树的实际实现

## 5.1. 邻接模型
1. ADJACENCY_MODEL

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/1.png)

2. 表的每一行描述一个部队，parent_id指向树中的上级部队

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/2.png)

## 5.2. 物化路径模型
1. MATERIALIZED_PATH_MODEL

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/3.png)

2. 表中有两个索引，在materialized_path上的唯一性索引以及在commander上的索引，正确的设计应该增加id字段。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/4.png)

## 5.3. 嵌套集合模型
1. NESTED_SETS_MODEL

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/5.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/6.png)

# 6. 用SQL访问树的结构
1. 为了检查效率和性能,分别用不同模型解决如下两个问题:
2. 法国将军Dominique Vandamme指挥哪些部队，以缩排方式或简单列表的方式显示他们。注意，所有的commander字段都构建了索引 (简称Vandamme查询)
3. Scottish Highlanders的每个团各属于哪个部队(自底向上的查询)。在部队的名称.(description字段).上没有索引， 唯- -的方法是在description字段中查找"Highland" 字符串，在没有任何全文索引的情况下，这个问题简称highland问题
   1. 注:层次结构Corp-division-brigade regiment
   2. Oracle

## 6.1. 自顶向下查询：Vandamme 查询

### 6.1.1. 邻接模型
1. `connect by < a column of the current row > = prior a column of the previous row`
2. `connect by < a column of the previous row > = prior a column of the current row`

```sql
select lpad(description, length(description) + level) description, commander
from adjacency_ model
connect by parent_ id = prior id
start with commander = 'Général de Division Dominique Vandamme'
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/7.png)

- 邻接矩阵：递归实现

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/8.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/9.png)

- 添加排序：加粗部分完成排序（优化器会避免出现重复计算）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/10.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/11.png)

- 那么MySQL呢？两个方法
   1. 手动union
   2. 在一个查询汇总多次连接
   3. 前提都是已知深度（人工获取）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/12.png)

### 6.1.2. 物化路径模型
1. 查询编写不困难
2. 计算由路径导出的层次不方便
3. 假设mp_depth()函数返回当前节点深度

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/13.png)

### 6.1.3. 嵌套集合模型
1. 很简单，某节点的后代的 left_num 和 right_num 都会在该节点的 left_num 和right_num 范围内

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/14.png)

2. 缩排怎么办？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/15.png)

### 6.1.4. 比较各模型下的Vandamme模型
1. 返回40条记录，循环执行各个查询5000次，比较每秒返回的记录数
2. 邻接模型最高：parentId
3. 物化路径模型
   1. 计算深度：字符串相关操作效率低
   2. 缩排：反复处理字符串效率低
4. 嵌套集合模型：
   1. 查找子代完胜其他模型
   2. 缩排成本太高了
   3. 改进：每个节点都冗余存储深度，但是维护成本高：树结构不改变、不需要所有节点排序时最好。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/16.png)

## 6.2. 自底向上访问：Highland查询
1. 在 description 字段中查找“ Highland ”字符串
2. 必然导致完整的表扫描：无法使用索引
3. 不同模型下 Highland 查询的差异

### 6.2.1. 邻接模型
Connect by 非常容易实现：Connect by不是关系操作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/17.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/18.png)

### 6.2.2. 物化路径模型
- 仅找出适当的记录并缩排显示算容易
  - 重复记录的问题
  - 顺序的问题

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/19.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/20.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/21.png)

### 6.2.3. 嵌套集合模型
1. 动态计算深度依旧是个问题
2. 不要显示人造根节点
3. 硬编码最大深度（为了缩排显示）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/22.png)

### 6.2.4. 比较各种模型下的Highland查询
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/23.png)

由于邻接模型中会有重复语句，我们可以使用有效结果的行数来衡量

### 6.2.5. 一些问题
1. 物化路径不该是KEY，即使他们有唯一性：主键最好不要经常被更新
2. 物化路径不该暗示任何兄弟节点的排序
3. 所选择的编码方式不需要完全中立

# 7. 聚合来自树的值
- 一共有2个大部分
  - 保存叶节点的值
  - 计算某个值散布在整个树中的百分比

## 7.1. 对保存于叶节点的值做聚合
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/24.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/25.png)

## 7.2. 计算每一层的人数

### 7.2.1. 计算每一层的人数（邻接模型）
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/26.png)

### 7.2.2. 计算每一层的人数（物化路径）
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/27.png)

### 7.2.3. 不同模型的性能
- 执行查询5000次，比较单位时间返回的记录数

## 7.3. 散布在各层的百分比
1. 假设我们经营魔药。每种魔药由多种成分（ ingredient ）组成，处方 recipe 列出成分及百分比。处方可以共享某种“基础魔药”，以复合成分 compound ingredient ）的形式表示。
2. 百分比被分到了每一个部分中

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/28.png)

3. 某一种可以选择的建模方法
   1. Components 表为通用类型
   2. 它有 recipes 和 basic_ingredients 两种子类型
   3. Composition 表保存处方成分（可以是处方或基本成分及其数量）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/29.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/30.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Database-Development/img/lec6/31.png)

## 7.4. 树状结构的问题
1. 本章的方法，在数据量很少的情况下效果令人满意
2. 对大数据量的处理“像老爷车一样慢”
3. 同样可以采用非规范化模型、或基于触发器的扁平化数据模型。
4. 不建议对关系模型“屡遭诟病的缓慢本性”反规范化，这很容易遮掩程序设计中的问题。
5. 不过， SQL 确实缺乏处理树结构的强大的、可伸缩的手段。