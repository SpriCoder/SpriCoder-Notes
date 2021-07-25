Docker
---

# 1. 什么是Docker
1. Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从 Apache2.0 协议开源。(2013年出现)
2. Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。
3. 容器是完全使用沙箱机制，相互之间不会有任何接口(类似 iPhone 的 app),更重要的是容器性能开销极低。
4. Docker 从 17.03 版本之后分为 CE(Community Edition: 社区版) 和 EE(Enterprise Edition: 企业版)
5. 我们将所有封装成为一个镜像，每次运行以下就可以

## 1.1. 应用场景
1. Web 应用的自动化打包和发布。
2. 自动化测试和持续集成、发布。
3. 在服务型环境中部署和调整数据库或其他的后台应用。
4. 从头编译或者扩展现有的 OpenShift 或 Cloud Foundry 平台来搭建自己的 PaaS 环境。

## 1.2. Docker产品
1. Docker Desktop:开发者使用的工具
2. Docker Hub:可以去拉取的东西。

# 2. 容器技术基础
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/1.png)

1. Docker技术:
   1. 容器技术
      1. 有效分配与管理物理资源
      2. 实现资源隔离
   2. 镜像技术
      1. 打破"代码即应用"的观念
      2. 从系统环境开始，自下而上打包应用(所有依赖都已经打包了)
2. Docker容器引擎是基于LXC
3. 通过namespace进行进程隔离：命名空间是在多个用户之间划分群集资源的方法

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/2.png)

## 2.1. Docker Engine
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/3.png)

## 2.2. 组件清单
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/4.png)

1. 我们可以自己搭建私有的镜像仓库
2. 也可以使用Docker Hub上的景象

## 2.3. Docker文件系统和Dockerfile
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/5.png)

1. copy-on-write

## 2.4. Docker网络模式

### 2.4.1. Bridge模式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/6.png)

1. 网桥连通:内部有自己的IP地址

### 2.4.2. Host模式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/7.png)

1. 端口使用和主机相同的端口

### 2.4.3. 容器模式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/8.png)

1. A容器有自己的网络空间
2. B容器会共享A容器的所有的网络空间

### 2.4.4. None
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/9.png)

1. 没有网络

## 2.5. Docker存储驱动驱动
1. 默认使用DeviceMapper

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/10.png)

## 2.6. 演示
1. docker file
```
FROM daocloud.io/ms_platform/dmp-maven:latest
LABEL maintainer = "grissom.wang@daocloud.io"
WORKDIR /project (工作目录)
ADD ./projecy
RUN mvn install -Dmaven.test.skip=true
CMD["mvn"]
```
2. docker Build:生成镜像
```
docker build .
```
3. 启动镜像
```
docker run -d -name
```

# 3. 容器编排与调度
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/11.png)

1. 适应微服务架构
2. Compose自动部署成为多份
3. Kubernetes

## 3.1. 容器的编排
1. 容器引擎完成容器编排。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/12.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/13.png)

2. 实例数量少于规定数量
   1. 自动启动容器
   2. 从Worker算法找到一个节点来启动
   3. 上面的是控制节点的工作
3. 节点之间通过gossip网络保证一致性
4. 编排通过Compose文件来管理，这个文件包括
   1. 容器之间的关系
   2. 容器的版本
   3. 网络、存储、依赖的服务

## 3.2. Kubernetes
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/14.png)

1. Borg:基于namespace和cgroup实现
2. Broglet:跑一组容器的结点(Master用来管理)
3. Scheduler:调度算法、亲和性等
4. Google的想法就是开源的方法，然后在开源基础上发展自己的东西

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/15.png)

1. Pod:表示一个比较的紧密的容器(共享网络空间和存储，对外只有一个IP),label:进行标签化
2. Kubelet:完成管理
3. API Server\Replication Controller:控制管理
   1. Deployment：
   2. StatefulSet：
   3. DeamonSet：
   4. Job：
   5. CronJob：
4. Service:服务
5. Node:节点
6. Kubernetes Master：主节点
7. 避免pod被调度到不合适的节点:
   1. Taints
   2. Tolerations
8. ETCD:存储状态数据

# 4. CNCF
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/16.png)

1. 右侧上面两个是已经成熟的产品
   1. Kubernetes
   2. Prometheus:监控:监控容器和应用等等

# 5. Docker与Devops
1. 交付原来是代码
2. 现在使用容器和镜像来进行交付(标准化)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/Docker/img/17.png)


# 6. 参考
<a href = "https://www.runoob.com/docker/docker-tutorial.html"></a>

# 7. 实例
1. 多步构建允许在Dockerfile中使用多个FROM指令。两个FROM指令之间的所有指令会生产一个中间镜像，最后一个FROM指令之后的指令将生成最终镜像。中间镜像中的文件可以通过`COPY --from=<image-number>`指令拷贝，其中`image-number`为镜像编号，0为第一个基础镜像。没有被拷贝的文件都不会存在于最终生成的镜像，这样可以减小镜像大小，同时避免出现安全问题。