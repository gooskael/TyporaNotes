### 使用Vant库

[小程序使用vant库](https://www.jianshu.com/p/fab40523e35a)

一：安装vant

```shell
// 进入到项目目录
$ cd dir
// 下载vant
npm init -y
npm install
npm i @vant/weapp -S --production
```

> 在npm下载vant的时候，出现找不到package.json。
>
> ```shell
> // 使用-y会自动添加一些需要的字段
> npm init -y
> ```
>
> 再重新npm下载即可。

二：修改`app.json`

```json
// 去除"style": "v2"
- "style": "v2"
```

三：构建npm & 引用

`工具` => `构建npm`

```js
"usingComponents": {
    "vant-button": "@vant/weapp/button/index"
}
```

