docker常用命令部分
---
1. 日常工作的环境，docker1.13.1版本完全可以满足工作需求了,若需要求其它版本，则指定docker的yum源去指定安装更高版本。

命令|功能
--|--
`yum -y upgrade`|升级
`yum -y install wget`|安装wget
`yum -y install yum-utils`|安装`yum-config-manager`|工具和安装相关的存储驱动服务
`sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo` | 添加docker仓库文件docker-ce.repo仓库
`yum install  docker-ce`|安装docker-ce算是客户端工具吧
`yum list docker-ce --showduplicates|grep "doc"|sort -r`| 查看相关docker-ce仓库里的docker版本有哪些
`yum -y install docker-ce-18.06.3.ce-3.el7`|选择安装的docker版本
`systemctl start docker` | 启动docker 
`sudo systemctl start dockersudo systemctl enable docker` | 启动 并加入开机启动

# 1. Docker本身命令
命令|功能
--|--
`docker version`|版本
`docker info`|系统信息
`docker logs`|日志信息
`service docker status`|故障检测
`docker sudo service docker start|stop`|启动关闭
`docker ps`|查看当前运行的容器
`docker ps -a`|查看所有的容器
`docker ps -a -q`|查看全部容器启用的id和信息
`docker ps -as`|查看全部容器占据的空间
`docker top`|查看一个正在运行的容器进程
`sudo docker inspect -f '{{.id}}'[id]`|查看容器的示例id
`docker inspect`|检查镜像或者容器的参数，默认返回JSON格式
`docker.run`|创建容器


# 2. 参考
1. <a href = "https://blog.csdn.net/TOP__ONE/article/details/101426455">docker容器</a>