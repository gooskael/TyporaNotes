[TOC]

### vs code

[用VSCode编写python](https://www.cnblogs.com/xjnotxj/p/10342251.html)

Icon(Setting) > Extensions > 左下角显示python编辑器



### Jupyter Notebook

[Jupyter Notebook介绍、安装及使用教程](https://www.jianshu.com/p/91365f343585)

#### 安装

```shell
#升级pip到最新版本
$ pip3 install --upgrade pip
```

```shell
#安装jupyter
$ pip3 install jupyter
#可能会出现一些错误，多下载几遍就行(翻墙看看)
```

```shell
#帮助
$ jupyter notebook --help
```

#### 文件存放路径

1. 复制存放文件的文件夹路径

   /Users/samstephen/python/jupyter

2. 查询配置文件路径

   ```shell
   #获取配置文件路径
   $ jupyter notebook --generate-config
   ##############################################################
   # 这条命令虽然可以用于查看配置文件所在的路径，
   # 但主要用途是是否将这个路径下的配置文件替换为默认配置文件。
   # 若文件已经存在或被修改，使用这个命令之后会出现询问
   # “Overwrite /Users/raxxie/.jupyter/jupyter_notebook_config.py with default config? [y/N]”，即“用默认配置文件覆盖此路径下的文件吗？”，
   # 如果按“y”，则完成覆盖，那么之前所做的修改都将失效；
   # 如果只是为了查询路径，那么一定要输入“N”。
   ################################################################
   ```

   /Users/samstephen/.jupyter/jupyter_notebook_config.py

   ```shell
   # 如果通过一步步进入文件夹，.jupyter是隐藏文件夹，-a可以查看隐藏文件夹
   $ ls -a
   ```

3. 修改配置文件

   ```shell
   # 编辑配置文件
   $ vim /Users/samstephen/.jupyter/jupyter_notebook_config.py
   ```

   a) 查找修改处：进入配置文件后，不要进行任何操作，直接输入/c.NotebookApp.notebook_dir，紧接着按Enter键，会直接跳转到改查找字符串的行首。

   b) 按i进入编辑模式，将文件存放路径/Users/samstephen/python/jupyter复制到引号中间。

   c) 取消行首的注释符号"#"

   d) 完成编辑保存退出。按ESC，输入:wq，按enter。

#### 启动jupyter notebook

```shell
# 默认启动方式，根据配置文件存放路径启动，默认端口号8888
$ jupyter notebook
```

```shell
# 指定端口启动，jupyter每启动一个窗口会在8888基础上不断+1
$ jupyter notebook --port 9999
```

```shell
# 启动，但是暂时不打开主页窗口，会返回一个打开该主页的地址
$ jupyter notebook --no-browser
```



