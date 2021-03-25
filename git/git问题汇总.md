[TOC]

### 0. git初始化项目以及仓库

[git连接gitlab远程仓库](https://blog.csdn.net/lkt_anhua/article/details/78835226)

1. 在git仓库网站（如`gitlab`中`createProject`，填入相关的`projectName` 、 `description`。

   > ```shell
   > // 初始化成一个可维护的git仓库文件
   > $ git init
   > // 添加origin字段所代表的仓库远程地址,即赋值一个url给origin
   > $ git remote add origin git@···
   > // 将所有修改及新加的文件变化提交到暂存区
   > $ git add . 
   > // commit，并且输入commit的内容
   > $ git commit -m 'Initial commit'
   > // 将本地main分支和远程仓库origin建立连接
   > $ git push -u origin main
   > ```
   >

2. 根据提示完成初始化git项目、并push即可。

​	在这个过程中，可能`git remote xxxxxxxxx`的时候出错，可以查看已连接仓库、删除已连接仓库。或者有更改远程仓库链接的需要。

> ```shell
> // 查看已经连接的远程仓库
> $ git remote -v
> // 断开连接
> $ git remote rm origin
> // 添加新的仓库链接
> $ git remote add origin git@···
> // 设置本地main提交到origin为默认提交远程分支
> $ git push -u origin main
> ```

​	测试是否成功：

```shell
ssh -T git@gitlab.com
```

****

### 1. 查看git的用户、密码及修改操作

[查看git的用户名和密码](https://www.cnblogs.com/xihailong/p/13354628.html)

```shell
$ git config user.name
$ git config user.password
$ git config user.email
$ git config --list
```

```shell
$ git config --global --replace-all user.name 'newName'
$ git config --global --replace-all user.password 'newPwd'
```

`user.name`是身份识别，在第一次使用git的时候设置好之后后续就没有必要再进行设置了。在`push/pull`的时候都会以该`user.name`标识。因此在`log`里面所记载的本机对代码仓库的操作，都是以该`user.name`进行记载。

****

### 2. ssh以及测试git clone

[git删除持久化存储的账号密码.git-credentials](https://www.cnblogs.com/maopixin/p/12054614.html)

​	1.ssh实际就是通过本地的`id_rsa.pub`以及仓库用户设置好的ssh进行对比，如果对比为相同的话，那么就能进行免密克隆（无需再进行密码确认）。

​	ssh生成：利用email生成一对私钥和公钥

> ```shell
> // 利用email生成一个私钥和公钥
> $ ssh-keygen -t rsa -C 'email'
> ```
>
> ```shell
> $ cd ~/.ssh
> $ ls 
> // 可以看到生成的一对ssh
> > id_rsa	id_rsa.pub
> ```

​	ssh查看以及用户ssh设置确认：可以通过进入`~/.ssh`查看是否已经有`id_rsa.pub`，然后确认一下用户所添加的`ssh`是否与本机的一致。用户添加的`ssh`可以在相应的git仓库网站的用户`Settings` > `ssh`查看，本机的使用`cat`查看。

> ```shell
> $ cd ~/.ssh
> $ ls
> > id_rsa	id_rsa.pub
> $ cat id_rsa.pub
> > ssh-rsa ******* email
> ```

- [x] ssh有什么用？

  ssh是一个安全协议，以非对称加密实现身份验证。本机产生id_rsa(私钥) id_rsa.pub(公钥)，将公钥上传到github上。pull的时候公钥用于对数据进行加密，私钥用于对数据进行解密，push的时候私钥用于对数据进行签名，公钥用于对签名进行验证。

****

​	2.`git clone`：克隆的时候有两种方式，一种是通过ssh，一种是通过https，即`clone with SSH`&`clone with HTTPS`。

​	`clone with SSH`：一般私有仓库都使用SSH，保证了私有性。但是不可能每次pull和push都去验证用户信息，即不可能每一次操作都需要用户密码输入，因此生成`id_rsa`和`id_rsa.pub`方便进行日常的`pull/push`等代码管理操作。

​	`clone with HTTPS`：一般开源项目具有公有特性。一方面如果每个参与者的数据的拉取都进行加密解密的话，代价将会非常大。另外一个方面，对于众多提交者，代码应该由管理者去审核是否merge,同时代码也没有必要保持传输过程中的私有可靠。所以可以采用HTTP明文传输或者HTTPS也可以。如果私有仓库通过`HTTPS`来克隆的话，输入用户的仓库网站的账号密码即可进行克隆。

****

​	3.mac自带的钥匙串访问系统支持免密。

​	(`command+space`搜索`钥匙串访问`，查询`git`即可看到相关的钥匙串)

```shell
$ git clone https://git.weixin.qq.com/wx_wx***************/glorySystem.git
```

​	比如上面的`git clone`命令，会去`钥匙串访问`系统中的数据进行对比，找到位置为`https://git.weixin.qq.com`的账号密码进行使用。如果能够登录，则直接完成克隆；如果**钥匙串管理的账号密码有误**，就会产生：

```shell
fatal: Authentication failed for 'https://git.weixin.qq.com/wx_wx421c68eb8d43725d/glorySystem.git/'
```

****

​	4.不使用ssh的情况，直接附加用户名以及密码进行克隆：

```shell
$ git clone http://username:password@remote
// e.g. username: abc@qq.com, pwd:test, git地址: git@xxx.com/test.git
$ git clone http://abc%40qq.com:test@git@xxx.com/test.git
```

​	需要注意的是，用户名以及密码中一定要转义，比如`@`转义后就是`%40`。

#### git clone 失败原因分析及解决方案

​	0.对于clone下来的项目，不要轻易改变`git remote -v`的地址。

​	上述可以看到，git clone失败的原因：

1. 本机`id_rsa.pub`与仓库网站的用户SSH设置不符。先检查仓库网站用户的SSH设置以本机`id_rsa.pub`是否一致，如果不一致可以`1.添加SSH`；`2.利用附加用户名以及密码的方式克隆`。

2. 本机使用了`git-credentials`来管理（代替`ssh`的另一种方式），实现可持久化的存储管理。比如如下操作可能添加了`git-credentials`把附加用户名以及密码进行脚本管理：

   ```shell
   $ cat ~/.git-credentials
   > http://username:password@git.xxx.cn
   ```

   检查是否是这个原因需要检查`git-credentials`文件：

   ```shell
   // 查看持久化存储的方式
   $ git config --list | grep credential
   > credential.helper=osxkeychain
   > credential.helper=store
   ```

   `osxkeychain`就是mac自带的钥匙串 

   `store`说明是文件存储地址在 `~/.git-credentials`，那么就需要查看一下这个可持久化的存储是否是影响`git clone`失败的原因。通过cat来查看一下内容比较即可。

   ```shell
   $ cat ~/.git-credentials
   > http://username:password@git.xxx.cn
   > https://xxxx:xxxx@github.com
   ```

   解决方法还是`1.通过vim进行相关文本内容的修改或者删除`，`2.利用附加用户名以及密码的方式克隆`

   对于第一个解决办法，更粗暴的是直接unset：

   ```shell
   $ git config --system --unset credential.helper
   ```

3. 有时候使用`clone with HTTPS`的时候，提示输入密码，但是输入密码之后还是有错误。是因为如上面的`3.mac自带的钥匙串访问系统支持免密`描述的一样，会在对应的目标网站有相应的账号密码。如果`id_rsa.pub`对应的账号并不是能够查看该代码仓库的账号，就会报错。因此直接通过`利用附加用户名以及密码的方式克隆`即可。

​	**总结起来**：就是查看`ssh`与`id_rsa.pub`是否对应 > 查看管理账号密码钥匙串是否正确 > 不行就直接使用`附加用户名以及密码的方式克隆`。

****

### 3. SSL 443报错

- [x] 问题报错：Failed to connect to github.com port 443
- [x] 解决方案：取消代理。一般是翻墙克隆下来会出现的问题。

```shell
$ git config --global --unset http.https://github.com.proxy
$ git config --global --unset https.https://github.com.proxy
```

****

#### 4. fatal: the remote end hung up unexpectedly

- [x] 问题报错：error: RPC failed; curl 92 HTTP/2 stream 0 was not closed cleanly: CANCEL (err 8)
- [x] 解决方案：增加缓存空间（亲测可用） 或 更改为ssh地址（未测试过）。参考[fatal](https://blog.csdn.net/qq_34466755/article/details/113748527)。

```shell
$ git config --global http.postBuffer 524288000
// 记得在console中git push更不容易出错
$ git push
```

****

### 5. Git push

```shell
$ git push origin
```

上面命令表示，将当前分支推送到origin主机的对应分支。如果当前分支只有一个追踪分支，那么主机名都可以省略。即直接`git push`。

```shell
$ git push -u origin main
$ git push -u <主机> <本地分支>
```

上面命令将本地的main分支推送到origin主机，同时**指定origin为默认主机**，后面就可以不加任何参数使用git push了。

`git push`：不带任何参数的git push，默认只推送当前分支，这叫做simple方式。

#### git push -u origin main & --set-upstream-to

- [x] 参考[git push的-u参数具体含义](https://www.zhihu.com/question/20019419/answer/48434769)

> ​	1.upstream不是针对远程仓库的，而是针对branch的。但是upstream和有几个远程库没有必然联系。比如远程库A上有3个分支branch1、branch2、branch3。远程库B上有3个分支branchx、branchy、branchz。本地仓库有2个分支local1和local2。那么当初始状态时，local1和local2和任何一个分支都没有关联，也就是没有upstream。当通过git branch --set-upstream-to A/branch1 local1命令执行后，会给local1和branch1两个分支建立关联，也就是说local1的upstream指向的是branch1。 => **upstream建立了本地分支和远程分支的fetch对应关系**

> ​	2.使用了upstream之后：这样的好处就是在local1分支上执行git push（git pull同理）操作时不用附加其它参数，Git就会自动将local1分支上的内容push到branch1上去。同样，local2分支也可以和远程库A和远程库B上的任何一个分支建立关联，只要给local2分支设置了upstream，就可以在local2分支上用git push（git pull同理）方便地与目标分支推拉数据。 => **upstream建立联系之后就可以使用simple方式直接`git push/pull`而不用添加参数**

- [x] e.g. 我要把本地分支mybranch1与远程仓库origin里的分支mybranch1建立关联。

  途径1：

  ```shell
  // 首先，你要切换到mybranch1分支上
  $ git checkout mybranch1
  // 和远程仓库建立联系，并且设置为默认提交仓库分支
  $ git push -u origin mybranch1
  ```

  途径2：

  ```shell
  $ git branch --set-upstream-to=origin/mybranch1 mybranch1
  $ git push origin mybranch1
  ```

即：`git push -u origin mybranch1` === `git push origin mybranch1` + `git branch --set-upstream-to=origin/mybranch1 mybranch1`。

****

