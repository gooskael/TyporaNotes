[TOC]



### 1. 什么是脚手架vue cli

脚手架提供一个方便进行项目新建、管理的一个前端。



[vue cli的超详细教程--安装](https://blog.csdn.net/qq_40741855/article/details/87077521)

[vue 利用vue ui创建项目--安装、使用](https://blog.csdn.net/weixin_40688217/article/details/88321322)

---

### 2. MAC安装vue cli和使用

在安装cli之前，需要安装webpack，关于webpack的作用，参考[我为什么要使用webpack](https://www.jianshu.com/p/9f2d0b64f3b8)

> *我们可以将HTML、CSS和JavaScript代码放在同一个.vue文件当中，强大的Webpack可以将这些代码分离出来，并分别与其他同类型的代码打包到一起。而我们不需要管Webpack内部是如何运作的，只需要知道单文件组件形式确实会为我们的工作带来极大的便利性。*



#### 安装webpack

```shell
$ sudo npm install webpack -g //如果出现代理proxy问题，翻墙再执行即可
```

​            ![img](./images/vue-cli安装~1.png)            

**执行完毕之后出现的error，提供后续检查。**

```shell
$ webpack -v //查看版本 检查是否安装完成
//如果出现需要安装webpack-cli，需要自己手动安装，不要自动安装，因为自动安装没有-g全局
$ sudo npm install webpack-cli -g
```

---

### 3. 安装vue cli

```shell
$ sudo npm install -g @vue/cli //下载最新版本vue cli
```

![img](./images/vue-cli安装~2.jpg)            

**执行完毕出现的error，提供后续检查使用。**目前觉得可能是升级了系统之后终端提示的，后续检查再看：

```shell
The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
```

```shell
$ vue -V //查看版本 检查是否安装完成
$ vue -h //查看帮助
$ which vue //查看路径 -> /usr/local/bin/vue
```

---

### 4. 使用vue ui

```shell
$ vue ui //打开网页版vue项目管理页面，注意关闭终端则会断开链接
```

参考[vue 利用vue ui创建项目](https://blog.csdn.net/weixin_40688217/article/details/88321322)中的步骤，

- 选择samstephen > VUE-UI文件夹创建项目

- 包管理器“默认”；更多选项都不勾选；初始化git仓库勾选

- 选择手动配置，**babel**、**router**、**使用配置文件**、Linter/formatter格式太严苛，别安装

- 不要选择history mode（别勾选，使用哈希模式）[history mode](https://router.vuejs.org/guide/essentials/history-mode.html#example-server-configurations)

- 保存/不保存预设都行

  > 配置完成之后项目会自行创建，在终端上可以看到相关的记录，但是可能会出现error
  >
  > 参考[NPM Error: gyp: No Xcode or CLT version detected!](https://www.cnblogs.com/zhennann/p/12272058.html)
  >
  > ```shell
  > $ Xcode-select --install //下载相关的Xcode-cli即可
  > ```

- 点击左侧插件栏目，点击添加新的插件“vue-cli-plugin-element”，右下角安装此插件

  > 此处看视频有弹幕说可以在终端上执行npm install element

- 配置插件"vue-cli-plugin-element"，fully import改成import on demand，项目简洁一点

- 在server中运行项目，项目出错

  ​            ![img](./images/vue-cli安装~3.png)            

在vue-ui里运行始终会出问题，直接在vscode里打开项目，在终端console上运行即可

```shell
$ npm run serve
```

---

### 5. 终端创建vue项目

```shell
$ cd 指定目录 //会在该目录底下创建文件
$ vue create projectName
```

```shell
//在vscode上打开文件，打开终端，运行项目
$ npm run serve
```

- [x] `Babel` 主要是对es6语法转换成兼容的js 
- [ ] `TypeScript` 支持使用TypeScript语法来编写代码
- [ ] `PWA` [PWA](https://developers.google.com/web/progressive-web-apps/) 支持
- [x] `Router` 支持vue路由配置插件
- [x] `Vuex` 支持vue程序状态管理模式
- [ ] `CSS Pre-processors` 支持css预处理器
- [ ] `Linter / Formatter` 支持代码风格检查和格式化 
- [ ] `Unit Testing` 单元测试
- [ ] `E2E Testing` E2E测试

---

### 6. 一个vue项目怎么运行起来？

