## ionic-vue 快速上手

官网地址：https://ionicframework.com/docs/

安装ionic所需要的工具

```sh
npm install -g @ionic/cli
```

创建一个ionic-vue项目

```sh
ionic start myApp blank --type vue
```

创建之后进入项目文件夹，运行项目

```sh
cd myApp
ionic serve
```

打包项目

```sh
ionic build
```

使用capacitor添加对Android的支持

```sh
npx cap add android
```

使用capacitor启动Android Studio

```sh
npx cap open android
```

IOS同理

```sh
npx cap add ios
npx cap open ios
```

ionic组件库：https://ionicframework.com/docs/components

