Tec2-安装Hadoop和Spark
---

# 1. 本机Java配置以及安装的目标版本
1. Java:jdk1.8.0_251
2. WIN10
3. Hadoop:目标安装版本为3.1.3
4. Scala:目标安装版本为2.11.12
5. Spark:目标安装版本为3.0.0(适用于Hadoop 2.7.0以上版本)

# 2. 安装JDK
1. 提前安装好JDK 8/11，根据自己的需要进行安装即可

# 3. 安装运行Hadoop

## 3.1. 下载Hadoop
1. <a href = "https://mirror.bit.edu.cn/apache/hadoop/common/">下载网址</a>
2. 本教程的Hadoop版本下载地址:https://mirror.bit.edu.cn/apache/hadoop/common/hadoop-3.1.3/hadoop-3.1.3.tar.gz

## 3.2. 下载Winutils-3.1.0
1. 因为Hadoop在2.0之前是完全运行在Linux系统上的，所以在之后如果想要在Windows上安装需要我们下载相应的exe才可以。
2. <a href = "https://github.com/stormbroken/apache-hadoop-3.1.0-winutils">下载地址</a>，可以使用fork的方式到自己的仓库然后下载，也可以直接选择下载ZIP文件。

## 3.3. 解压Hadoop
1. 将刚刚下载的以tar.gz的文件以**管理员权限**进行解压
2. 如果不使用管理权限解压是无法解决so文件的解压的。
3. 将刚刚下载的Wintuils-3.1.0的bin文件夹下的所有的文件赋值到Hadoop解压后的bin文件夹下。

## 3.4. 配置Hadoop的系统变量
1. 新建`HADOOP_HOME`的系统变量，其变量值为刚刚`Hadoop`解压的文件夹，比如`D:\hadoop`
2. 为Path添加新的变量值:`%HADOOP_HOME%\bin`

## 3.5. 检查Hadoop的安装情况
1. 查看版本:`hadoop version`
2. 启动Hadoop:`HADOOP_HOME/sbin/start-all.cmd`

## 3.6. 运行问题

### 3.6.1. 系统找不到JAVA_HOME的路径
1. 原因:JAVA安装的位置的路径中包含有空格
2. 修改`bin\hadoop.cmd`文件中的JAVA_HOME的值:注意需要同时修改`etc\hadoop\hadoop-env.cmd`中的JAVA_JOME的值
```cmd
set JAVA_HOME=C:\PROGRA~1\Java\jdk1.8.0_251(your jdk name)
```

### 3.6.2. `java.lang.ClassNotFoundException: org.apache.hadoop.yarn.server.timelineservice.collector`
1. Hadoop启动报错，缺少`hadoop-yarn-server-timelineservice jar`包
2. 解决方案:从`Hadoop\share\hadoop\yarn\timelineservice`下`hadoop-yarn-server-timelineservice-x.x.x.jar`复制到`Hadoop\share\hadoop\yarn\lib`目录下。

### 3.6.3. NameNode进程无法启动，报`org.apache.hadoop.hdfs.server.common.InconsistentFSStateException`
1. 重启Hadoop的时候，控制台正常打印日志，但是jps显示没有namenode进程，可以发现存储数据的目录不存在或者目录不可访问
2. 解决方案:重新格式化文件系统
   1. 停止hadoop的进程:`HADOOP_HOME/sbin/stop-all.sh`
   2. 重新格式化文件系统:`HADOOP_HOME/bin/hdfs namenode -format`
   3. 启动Hadoop:`HADOOP_HOME/sbin/start-all.sh`

### 3.6.4. NameNode无法启动，日志提示`file:/// has no authority`
1. 运行Hadoop的过程中显示:`file:/// has no authority`
2. 修改`etc\hadoop\core-site.xml`的配置
```xml
<property>
    <name>fs.default.name</name>
    <value>hdfs://localhost:8020</value>
</property>
```

# 4. 安装运行Spark

## 4.1. 下载安装Scala
1. <a href = "https://www.scala-lang.org/download/all.html">Scala安装</a>
2. 注:一定要提前安装好JDK，并设置JAVA_HOME的系统变量。
3. 本教程安装使用的是2.11.12版本的Scala
4. Windows可以选择
   1. 方案一:<a href = "https://downloads.lightbend.com/scala/2.11.12/scala-2.11.12.zip">下载Scala-2.11.12.zip</a>然后解压缩后，手动配置系统变量
   2. 方案二:<a href = "https://downloads.lightbend.com/scala/2.11.12/scala-2.11.12.msi">使用Windows安装程序</a>，之后根据安装程序的指引完成安装即可。
5. 检查安装效果:在cmd中输入`scala`即可以查看版本

## 4.2. 下载Spark
1. <a href = "http://spark.apache.org/downloads.html">选择下载地址</a>
2. <a href = "https://www.apache.org/dyn/closer.lua/spark/spark-3.0.0/spark-3.0.0-bin-hadoop2.7.tgz">本教程的Spark的下载地址</a>
  
## 4.3. 安装Spark
1. 将刚刚下载的压缩包就压缩到你想要的解压缩的位置(也就是安装位置)
2. 进入到安装目录下`\bin`在cmd命令下运行`spark-shell`，正常运行结果如下

![](img/spark/1.png)

# 5. 运行Spark
1. 首先需要有IDEA，并且安装了Scala的Plugin
2. 创建一个Scala的IDEA项目
   
![](img/spark/2.png)

3. 选择相应的JDK和Scala SDK，创建HelloWorld项目
4. 创建一个名字为Hello的Scala Object，产生Hello.scala的文件。
5. 编辑这个文件
```scala
object Hello {
  def main(args: Array[String]): Unit = {
    println("Hello World");
  }
}
```
6. IDEA中运行正常

![](img/spark/3.png)

7. 使用`File->Project Structure->Artifacts`生成META-INF文件夹

![](img/spark/4.png)
![](img/spark/5.png)

8. 打包JAR：选择Build->Build Artifact->Build

![](img/spark/6.png)


9.  将压缩后的jar文件使用spark-submit来执行:`spark-submit --class Hello HelloWorld.jar`

# 6. 参考
1. <a href = "https://www.cnblogs.com/java-spring/p/11744195.html">在windows上搭建hadoop开发环境</a>
2. <a href = "https://blog.csdn.net/weixin_39723337/article/details/86482536">hadoop启动报错java.lang.ClassNotFoundException: org.apache.hadoop.yarn.server.timelineservice.collector</a>
3. <a href = "https://blog.csdn.net/qq_32641659/article/details/87894610">hadoop异常处理之nameNode进程无法启动，报org.apache.hadoop.hdfs.server.common.InconsistentFSStateException</a>
4. <a href = "https://www.cnblogs.com/chevin/p/11064854.html">Windows上安装运行Spark</a>
5. <a href = "https://blog.csdn.net/freecrystal_alex/article/details/78296851">intellij idea 打可运行scala jar 包的两种方式</a>