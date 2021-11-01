[TOC]

### Docker

以下学习主要看bilibili上的[2020 Docker最新超详细版教程通熟易懂](https://www.bilibili.com/video/BV1sK4y1s7Cj?p=1)--千锋Java学习营

#### Docker介绍

##### 1.1 引言

> 1. 我本地运行环境没问题，但是别人的代码就不能运行
>
>    A：环境不一致。 --集装箱保证环境一致
>
> 2. 哪个哥们又写死循环了，怎么这么卡？
>
>    在多用户的操作系统下，会互相影响。 --隔离性
>
> 3. 淘宝在双11的时候，用户量暴增。
>
>    运维成本过高的问题。 --标准化命令可以一个命令添加部署很多服务器
>
> 4. 学习一门技术，学习安装成本过高
>
>    关于安装软件成本过高  --我打包成集装箱，你只需要到中央仓库提取即可

##### 1.2 Docker由来

> 一帮年轻人创业，创办了一家公司，2010年的专门做PAAS平台。
>
> 到了2013年的时候，像亚马逊，微软，Google都开始做PAAS平台。
>
> 2013年，将公司内的核心技术对外开源，核心技术就是Docker。
>
> 到了2014年的时候，得到了C轮融资$4000W。
>
> 到了2015年的时候，得到了D轮融资$9500W。

##### 1.3 Docker思想

> 比如我现在在Linux系统安装了一个Mysql，然后现在你也需要。我只需要把我安装好的环境打包成一个集装箱，并且把它送到中央仓库里，你只需要去中央仓库拿就好了。

> 1. 集装箱：会将所有需要的内容放到不同的集装箱，谁需要这些环境就直接拿到这个集装箱就可以了。
>
> 2. 标准化：
>
>    1. 运输的标准化：Docker有一个码头，所有上传的集装箱都放在了这个码头上，当谁需要某一个环境，就直接指派Docker去搬运这个集装箱就可以了。
>    2. 命令的标准化：Docker提供了一些列的命令，帮助我们去获取集装箱等等操作。
>    3. 提供了REST的API：衍生出了很多的图形化界面，如Rancher。
>
> 3. 隔离性：
>
>    Docker在运行集装箱内的内容时，会在Linux的内核中，单独地开辟一片空间，这片空间不会影响到其他程序。

> - 注册中心。（超级码头，上面放的就是集装箱）
> - 镜像。（集装箱）
> - 容器。（运行起来的镜像）

#### Docker的基本操作

##### 2.1 安装docker

-- linux系统下

```shell
# 1.下载关于Docker的依赖环境
$ yum -y install yum-utils device-mapper-persistent-data lvm2
```

---

```shell
# 2.设置一下下载docker的镜像源
$ yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

----

```shell
# 3.安装docker
$ yum makecache fast
$ yum -y install docker-ce
```

----

```shell
# 4.启动，并设置为开机自动启动，测试
# 启动Docker服务
$ systemctl start docker
# 设置开机自动启动
$ systemctl enable docker
# 测试
$ docker --version
$ docker run hello-world
```

-- macOS系统下

详细见[hyperledger fabric教程](https://hyperledger-fabric.readthedocs.io/en/release-2.0/prereqs.html)中prerequisites中的[docker下载](https://www.docker.com/get-started)

##### 2.2 Docker的中央仓库（注册中心）

> 1. Docker官方的中央仓库：这个仓库是镜像最全，但是下载速度较慢，在国外。hub.docker.com
> 2. 国内的镜像网站：[网易蜂巢](c.163.com/hub)，[daoCloud](hub.daocloud.io) (推荐)··· ···
> 3. 在公司内部会采用私服的方式拉取镜像。

##### 2.3 镜像的操作

```shell
# 1.拉取镜像到本地
$ docker pull 镜像名称[:tag]   #这里的[]的意思是可以写可以不写，不写的时候会有默认
# 举个例子
$ docker pull daocloud.io/library/tomcat:8.5.15-jre8
```

----

```shell
# 2.查看所有镜像
$ docker images
```

----

```shell
# 3.删除本地镜像
$ docker rmi 镜像的唯一标识（image ID，可以是前几个字母就行） # rmi的意思是remove image
```

----

```shell
# 4.镜像的导入导出（不规范）
# 导出成文件，通过qq等方式下载再倒入
$ docker save -o 导出成的文件 镜像id # docker save -o ./eg.image b8
# 加载本地的镜像文件
$ docker load -i 镜像文件 # docker load -i eg.image
# 修改镜像名称。由于加载本地文件之后，名称和版本都是<none>，需要手动更改
$ docker tag 镜像id 新镜像名称:版本
# docker tag b8 tomcat:8.5 名称是tomcat 版本是8.5
```

##### 2.4 容器的操作

```shell
# 1.运行容器。如果本地有，直接运行；无则会下载再运行
# 简单操作
$ docker run 镜像的标识｜镜像名称[:tag] 
# 常用的参数
$ docker run -d -p 宿主机端口:容器端口 --name 容器名称 镜像的标识｜镜像名称[:tag]
# -d:代表后台运行容器
# -p 宿主机端口:容器端口 :为了映射当前Linux的端口和容器的端口（比如我想通过windows访问tomcat，需要通过windows访问Linux，再通过Linux访问容器端口从而找到最终访问的地点）
# --name 容器名称：指定容器的名称
```

```shell
# 2.查看运行的container
$ docker ps [-a] [-q]
# -a：查看所有容器，包括并没有在运行的
# -q：只查看容器的标识
```

```shell
# 3.查看容器的日志
$ docker logs -f ID
# -f：可以滚动查看日志的最后几行
```

```shell
# 4.进入到容器内部
$ docker exec -it ID bash
$ ls # 查看容器内部文件
# 再进入bin目录可以查看该容器的一些执行和结束文件
$ cd bin
# 最好不要使用shtdown.sh
```

```shell
# 5.停止运行的container
$ docker stop ID 
$ docker stop $(docker ps -qa) #停止全部容器
# 删除container(只能删除已停止的容器)
$ docker rm ID 
$ docker rm $(docker ps -qa) #删除全部容器
```

```shell
# 6.启动容器
$ docker start ID
```



### 问题

#### Q1:PAAS平台是什么东西？

> PaaS平台即Platform-as-a-Service，把应用服务的运行和开发环境作为一种服务提供的商业模式。实际上是指将软件研发的平台作为一种服务，以SaaS（Software-as-a-Service）的模式提交给用户。

>在传统的观念中，平台是向外提供服务的基础。一般来说，平台作为应用系统部署的基础，是由应用服务提供商搭建和维护的，而PaaS颠覆了这种概念，由专门的平台服务提供商搭建和运营该基础平台，并将该平台以服务的方式提供给应用系统运营商。

> PaaS的实质是将互联网的资源服务化为可编程接口，为第三方开发者提供有商业价值的资源和服务平台。

#### Q2:融资ABCD轮？天使轮融资？

> ABCD轮融资对应第一二三四轮。

> 天使投资(Angel Investment)，是指个人出资协助具有专门技术或独特概念而缺少自有资金的创业家进行创业，并承担创业中的高风险和享受创业成功后的高收益。天使投资一般只提供“第一轮”的小额投资。“天使”只是利用了自己的积蓄，不足以支持较大规模的资金需要，因此那些处于最初发展阶段的创业计划能够得到他们的青睐。

#### Q3:批量操作容器在WINDOWS上无法运行？

> ```shell
> $ docker stop $(docker ps -pa)
> $ docker rm $(docker ps -pa)
> # 针对所有容器的操作$(docker ps -pa)在windows上无法运行
> ```
>
> 可以通过gitbash或者批处理解决？？？

### 计划

- [ ] 学习部署一下apache、mysql、nginx、tomcat

