### 0. git初始化项目以及仓库

[git连接gitlab远程仓库](https://blog.csdn.net/lkt_anhua/article/details/78835226)

1. 在git仓库网站（如`gitlab`中`createProject`，填入相关的`projectName` 、 `description`。

   > ```shell
   > $ git init
   > $ git add . 
   > $ git commit -m ''
   > 
   > ```
   >
   > 

2. 根据提示完成初始化git项目、并push即可。

​	在这个过程中，可能`git remote xxxxxxxxx`的时候出错，可以查看已连接仓库、删除已连接仓库。

> ```shell
> // 查看已经连接的远程仓库
> git remote -v
> // 断开连接
> git remote rm origin
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