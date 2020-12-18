###### `wx.getSetting`

该API可以查看已经获取的用户权限

```js
wx.getSetting({
  success: (res) => {
    console.log(res);
  }
})
```

> 比如使用`open-type="getUserInfo"`的`button`获取了登录权限之后，就会出现字段`scope.userInfo: true`

****

###### `wx.login`

`wx.login`主要是用来获取`res.code`，搭配官方提供的接口来获取`openId`。见[小程序开发问题汇总.md / 12.wx的openId以及wx.login + res.code](../小程序开发问题汇总.md)

****

