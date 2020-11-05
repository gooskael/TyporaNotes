[TOC]

### Eclipse

#### JDK安装

> JDK(Java Development ToolKit)，是使用最广泛的Java SDK(Software Development ToolKit)。

参考[mac系统下如何配置jdk以及安装eclipse](https://blog.csdn.net/weixin_40318474/article/details/82455833)

参考[【Eclipse】Mac版下载安装配置](https://blog.csdn.net/hutuyaoniexi/article/details/94300592)

```shell
$ java -version
//显示需要安装JDK，点击“更多信息“在https://www.oracle.com/java/technologies/javase-jdk15-downloads.html上进行下载javase15版本。
//安装完毕后再输入一次
//显示java version的信息即可
```

##### 配置环境(似乎没必要，直接在eclipse的preference里直接操作即可)

```shell
//进入目录
$ cd Users/samstephen 
//查看是否存在.bash_profile，由于已存在，打开文件进行配置即可
$ ls -a
$ open -e .bash_profile
```

```shell
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-15.jdk/Contents/Home
PATH=$JAVA_HOME/bin:$PATH:.
CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.
export JAVA_HOME
export PATH
export CLASSPATH
```

```shell
:wq
```

#### 配置elipse

##### 应用JDK

eclipse > preferences > Java > Inßstalled JREs > 勾选 > apply

##### 取消拼写检查

> eclipse的拼写检查比较弱智，后续如果想要重新勾选也可

eclipse > preferences > 搜索框搜索“spelling” > 取消“enable”

##### 确定UTF-8编码

eclipse > preferences > General > Workspace > "Default (UTF-8)" > apply

#### 字体配置

help > Eclipse Marketplace > search > "color" 索引到“Eclipse Color Theme 1.0.0” > install

- [ ] Q：似乎重启了之后还是不能应用该主题

