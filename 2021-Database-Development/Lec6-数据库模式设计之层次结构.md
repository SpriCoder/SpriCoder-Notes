
Lec6-数据库模式设计之层次结构
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

