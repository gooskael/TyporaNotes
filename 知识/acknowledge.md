[TOC]

### 1. 颜色三种表示方式

#### `#000000` 及  `rgb` & `rgba`

<img src="/Users/samstephen/Library/Mobile Documents/com~apple~CloudDocs/TyporaNotes/知识/images/rgba.png" alt="image-20210313145659218" style="zoom:50%;" align="left"/>

​	最简单的两种是使用`rgb`以及十六进制的表示方法`#000000`。其中`rgba`是添加了表示透明度的字段，`0`表示全透明，`1`表示不透明。

#### `hsl`

<img src="./images/HSL.png" alt="image-20210313144959788" style="zoom:50%;" align="left"/>

​	`HSL`即`hue色相`、`saturation饱和度`和`lightness亮度`。同时HSL提供透明度属性`alpha`，从`0%`全透明到`100%`不透明。

```css
* {
  background: hsl(120deg, 100%, 50%, 100%);
}
```

****

### 2. 正则表达式

参考：1.[test和match的用法](https://blog.csdn.net/weixin_39818813/article/details/79731542)；2.[bilibili：JavaScript 10个常用正则表达式](https://www.bilibili.com/video/BV1QK4y1K72U) 3.[测试网站RegExr](https://regexr.com)。

#### 2.1 基础

##### 1. `?`、`+`、`*`及`{n,m}`

​	针对前面的一个字符，如果有括号括起来就算是一个字符整体。

`?`：匹配0｜1次，即最多只能出现一次。如果出现在`?`、`+`、`*`后面，表示由贪婪（最大匹配）变成非贪婪（最小匹配）。

`+`：匹配1-n次，即最少出现一次。

`*`：匹配0-n次。

`{n,m}`：匹配最少n次，最多m次；也可直接使用一个参数`{k}`，即匹配k次(包括这一次)。

****

##### 2. `\d`、`\w`、`\s`、`\S`、`.`

`\d`：(digit)表示`[0-9]`，在Javascript中可用，在其他语言中慎用。

`\w`：表示字母`[a-zA-Z]`、数字`[0-9]`和下划线`[_]`。

`\s`：匹配**所有空白符**，包括换行，等价于 `[ \f\n\r\t\v]`(注意有空格)。

`\S`：匹配任何非空白字符。等价于`[^ \f\n\r\t\v]`(注意有空格)。

`.`：表示换行符`\n`以外的所有字符。

****

##### 3. `^`、`$`、`|`、`\`

`^`：在中括号`[]`外面表示开始标志；在中括号里面使用表示`非`。

`$`：结束符号。`/[0-9]$/g`。

`|`：或者。注意这个符号是以**前后一串字符**为单位，比如`/0[1-9]|[12][0-9]|3[01]$/g`。

`\`：转义字符。如想要匹配`.`、`/`，就需要转义成`\.`、`\/`。

****

##### 4. `()`、`\1`、`?:`

- [x] 有时候我们不仅需要查看字符串是否匹配规则，还想要在匹配的同时获取一些数据。这时候使用`()`就可以选择获得内容；`\1`表示第一个括号获取的内容，`\2`表示第二个括号获取的内容······；但是有时候我们使用括号是因为作为一个整体，而并不想要获取里面的内容，就需要使用`?:`。

<img src="./images/选择.png" alt="image-20210314175013894" style="zoom:50%;" align="left"/>

`?:`：可以看到使用`?:`之后，本选择组`()`的内容不会再进行选择记录，但是不影响本选择组里面的选择组。即屏蔽了右侧`group #3`的内容，但是并不影响原本的`group #4`；屏蔽之前有4组选择组，屏蔽之后`group #3`去除，`group #4`变为`group#3`。使用`?:` 的原因是，我们并不需要原本`group #3`的内容，但是由于`|`或者的判断，需要将前后的一长串字符作为判断单位；因此这时候需要选择组的作用，但不需要选择组的内容。

`\1`：`\1`是当前匹配字段和`group #1`所匹配的字段。可以看到将后面的`/div`改成了`/di`之后，`group #1`的内容就变成了`di`。如果我们不使用`\1`，而复制粘贴相同的规则，可以看到各自判断各自的内容：`group #1`的内容是`div`，`group #4`的内容是`di`。按照正确的使用场景，应该各自判断获取内容，然后再进行判断是否内容一致，内容不一致说明标签匹配错误；一致才能说明标签使用正确。

<img src="./images/不使用选择.png" alt="image-20210314175613767" style="zoom:50%;" align="left"/>

****

#### 2.2 常用正则表达式

<img src="./images/正则-1.png" alt="image-20210314153817732" style="zoom:50%;" align="left"/>

```js
// 手机号码
let phoneReg = /^1[3-9][0-9]{9}$/g;
// QQ号码, js里面\d等同于[0-9]，如果是其他语言要注意，\d包括除了0-9之外的其他数字字符 
let qqAcountReg = /^[1-9]\d{4,9}/g; // \d <=> [0-9]
// 十六进制颜色匹配
let colorReg = /#?([0-9a-fA-F]{6}|[0-9a-fA-F]{3})$/g; // #000000; 000000; #000;
// 邮箱地址
let mailReg = /^([a-zA-Z0-9_\-\.])+@([a-zA-Z0-9_\-\.])+\.([A-Za-z]{2,4})$/g;
// URL
let urlReg = /^((https?|ftp|file):\/\/)?([\da-z\.\-]+)\.([a-z\.]{2,4})([\/\.\-\w]*)*\/?$/g;
// html标签/爬虫
let elReg = /^<([a-z]+)([^>]*)(?:>(.*)<\/([a-z]+)>|\s+\/>)$/gm; // m表示匹配多行，各行都按照该规则匹配
// ipv4
let ipv4Reg = /^(([01]?[0-9][0-9]?|2[0-4][0-9]|25[0-5])\.){3}([01]?[0-9][0-9]?|2[0-4][0-9]|25[0-5])$/g;
// 日期 2021-03-01
let dateReg = /^[0-9]{4}-(0[1-9]|1[0-2])-(0[1-9]|12[0-9]|3[01])$/g;
// 身份证 正则部分(还需要通过权重判断)
let idReg = /^[1-9][0-9]{5}(18|19|[23][0-9])[0-9]{2}(0[1-9]|1[0-2])(0[1-9]|[12][0-9]|3[01])[0-9]{3}[0-9xX]$/g;
```

`身份证权重计算`：

```js
// 身份证前17位与各自权重相乘得出总数，取余之后根据相应的数组得出最后一位；
// 根据上面的生成规则对比即可得出身份证是否正确
// 1.身份证号前17位的权重因子
const factor = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
// 2.身份证号最后一位校验位的对应11的余数
const parity = [1, 0, 'X', 9, 8, 7, 6, 5, 4, 3, 2]; 
// 假如idCard为输入的身份证号码
var idCard = '';
// code为身份证最后一位校验码
let code = idCard.substring(17);
// 根据权重因子计算出总数
let sum = 0;
for (let i = 0; i < 17; i++) {
  sum += str[i] * factor[i];
}
// 判断是否正确
if (parity[sum % 11].toString() !== code.toUpperCase()) {
	return false;
}
```

****

#### 2.3 `text | match`判断是否符合规定的正则：

```js
let phoneReg = /^1[3-9][0-9]{9}$/g;
let phoneNum = '13120030000';
// test是regExp的方法，参数是字符串，返回值返回true｜false
if (!phoneReg.test(phoneNum)) {
	return false;
}
// match是String的方法，参数是正则表达式，返回值是数组
if(phoneNum.match(phoneReg) === null) {
  return false;
}
```

****

### 3. cookie、session、token

参考：[前后端接口鉴权全解 Cookie/Session/Token 的区别](https://mp.weixin.qq.com/s/OG7LSVzYbMzgMEfMPu4fUQ)。

#### 0. 出现缘由

​	http是无状态协议，指的是：resource作为一个仅供访问的资源，其指责只负责把可以访问的资源放好，然后无论谁想要访问就直接访问就行。每一次访问都按照一个独立的请求，无法分辨上一次请求的发送者和这一次请求的发送者是否为同一个。这个独立请求，即无状态。

​	如果能加上用户状态就可以进行会话跟踪，维护一个状态，使会话更加高效。

​	既然协议本身无状态，不能分辨链接，那就在请求头部手动带着上下文信息吧，因此就出现了cookie。例如登录之后，服务器给你一个标志，就存在 cookie 里，之后再连接时，都会**自动**带上 cookie，服务器便分清谁是谁。

​	由于现在前端有两个storage（local、session）和两种数据库（websql、IndexedDB），因此现在cookie的作用就是在连接的时候**证明客户端的身份**。

- [x] 缺陷：cookie 还可以用于跟踪一个用户，这就产生了隐私问题，于是也就有了“禁用 cookie”这个选项

#### 1. cookie和session是什么

1. **cookie**：在客户端存放的数据，指的是浏览器中存储的一种数据，仅仅是浏览器实现的一种数据存储功能。是存储session、session id、token的容器。

> ​	cookie由服务器生成，发送给浏览器客户端，浏览器把cookie以key-value（sessionId='xxxxxxx'）的形式保存在浏览器中。

- [x] `cookie敏感信息泄漏`: js可以读写cookie｜页面植入恶意代码，通过读cookie，提取用户的敏感信息 => `HttpOnly设置禁止JS访问cookie，只有http可以访问cookie`
- [x] `模拟用户风险`: 浏览器特性（页面登录状态时，所有页面下的js代码访问该页面域名下的所有接口，浏览器都会自动带上cookie字段）；这时候如果在没关闭该浏览页面的情况下，打开了另一个恶意网站，恶意网站就会获取你的这个cookie，然后模拟成正常的网页访问，从而通过你这个“未关闭”的页面调用到网页内的接口，进行恶意操作（删除等） => `双cookie验证`
- [x] `引入session`：cookie只能存放4K的数据，而且如果所有数据都存放在客户端，一方面比较隐私的数据容易暴露，一方面客户端这边的任务比较多。服务端使用session。

2. **session**：在服务端的数据。客户端和服务端通过`sessionId`进行交互，客户端通过cookie存放该`sessionId`，服务端存放一个完整的session数据，通过`sessionId`来锁定该session。

> 1. `sessionId`: session用来存储用户信息（比如用户的id），为不同的用户生成不同的信息“身份标识”（session ID）并维护，session1|session2···。客户端每次发送请求带上cookie，服务器就能通过“身份标识”锁定到对应的session，然后获取访问用户的相关信息。session 理解为信息，而 session id 是获取信息的钥匙，通常是一串唯一的哈希码。
>
> 2. `生命周期`: 
>
>    `create session`: 客户端第一次连接服务端的时候，服务端根据客户端创建对应的session
>
>    `connecting`: 服务器给了一个标志之后，客户端之后再连接都会自动带上cookie，**自动**！
>
>    `destroy session`: 客户端和服务器断开连接，服务器就会销毁该session。

- [x] `session丢失`：如果服务器做了负载均衡，那么下一个操作请求到了另一台服务器的时候，session会丢失。
- [x] `session存储优化`: 但是如果访问量太大，服务器就要存储成千上万个session。需要注意的是，如果客户端访问服务器A，session就放在服务器A上，但是如果这时候想要访问服务器B，这时候服务器B并没有session，因此只能从服务器A拷贝一份过去。这样子就占用了很多资源，因此后来想到的办法就是建立一个缓存，所有session都存放在缓存中，然后所有的服务器都通过访问缓存去获取session（增加了单点故障的可能性）。

#### 2. cookie和session的区别

1. 安全性：session存储在服务端，cookie存储在客户端。
2. 存储值的类型不同：cookie只支持存储字符串数据，想要存储其他类型的数据，需要stringify；session可以存放任意类型的数据
3. 有效期不同：cookie可设置为长时间保持（比如默认登录功能），session一般失效时间较快，客户端关闭（默认情况下）或者session超时都会失效
4. 存储大小不同：单个cookie保存的数据不能超过4K，session存储空间很大，但是如果访问量过多，会过度占用服务器的资源

#### 3. cookie设置方式

​	安全起见，cookie都是依靠`set-cookie`设置，修改成不允许JavaScript设置cookie(HttpOnly)。

```java
Set-Cookie: <cookie-name>=<cookie-value>
	// expires: 设置 cookie 的过期时间（时间戳），这个时间是客户端时间
Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>
	// max-age: 设置 cookie 的保留时长（秒数），同时存在 Expires 和 Max-Age 的话，Max-Age优先
Set-Cookie: <cookie-name>=<cookie-value>; Max-Age=<non-zero-digit>
	// domain: 设置生效的域名，默认就是当前域名，不包含子域名
Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>
	// path: 设置生效路径，`/` 全匹配
Set-Cookie: <cookie-name>=<cookie-value>; Path=<path-value>
	// Secure: 设置 cookie 只在 https 下发送，防止中间人攻击
Set-Cookie: <cookie-name>=<cookie-value>; Secure
  // HttpOnly: 设置禁止 JavaScript 访问 cookie，防止XSS
Set-Cookie: <cookie-name>=<cookie-value>; HttpOnly
	// SameSite: 设置跨域时不携带 cookie，防止CSRF  
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Strict
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=Lax
Set-Cookie: <cookie-name>=<cookie-value>; SameSite=None; Secure
```

> - [x] Q: SameSite 选项需要根据实际情况讨论，因为 SameSite 可能会导致即使你用 CORS 解决了**跨越问题**，依然会因为请求没自带 cookie 引起一系列问题
>
>   A: 其实因为 Chrome 在某一次更新后把没设置 `SameSite` 默认为 `Lax`，你不在服务器手动把 `SameSite` 设置为 `None` 就不会自动带 cookie 了。

- [x] `cookie使用`：在发送 cookie 时，并不会把上面提到的 `Expires` 等配置传到服务器，因为服务器在设置后就不需要关心这些信息了，只要现代浏览器运作正常，收到的 cookie 就是没问题的。

- [x] `expires`、`max-age`：存储过期时间，通常在服务器设置。服务器会把生成代表该用户的相应信息内容发送过来，然后客户端存储在本地，即本地cookie。cookie会一直存在本地，但是由于过期时间，如果过了过期时间，再拿这个cookie发过去给服务端，就变成无用的信息了。

****

#### 4. session存储

​	session 信息可以储存在客户端，如 cookie-session，也可以储存在服务器，如 express-session。使用 session ID 就是把 session 放在服务器里，用 cookie 里的 id 寻找服务器的信息。

##### 客户端存储：cookie-session

​	把所有信息加密后塞到 cookie 里。其中涉及到 cookies 库。在设置 session 时其实就是调用 cookies.set，把信息写到 set-cookie 里，再返回浏览器。**换言之，取值和赋值的本质都是操作 cookie**。

​	浏览器在接收到 set-cookie 头后，会把信息写到 cookie 里。在下次发送请求时，信息又通过 cookie 原样带回来，所以服务器什么东西都不用存，只负责获取和处理 cookie 里的信息，这种实现方法不需要 session ID。

​	所谓的“将 session 信息放到客户端”，因为 base64 编码并不是加密，这就跟明文传输没啥区别，所以**请不要在客户端 session 里放用户密码之类的机密信息**。

```js
// 简单地设置 session 的过期日期和登录人就基本能用了
{
  "exp": 293581432798542,
  "usr": "admin"
}
```

- [x] 修改cookie：

```js
// 这是一段使用 cookie-session 中间件为请求添加 cookie 的代码：
const express = require('express')
var cookieSession = require('cookie-session')
const app = express()
app.use(
  cookieSession({
    name: 'session',
    keys: [
      /* secret keys */
      'key',
    ],
    // Cookie Options
    maxAge: 24 * 60 * 60 * 1000, // 24 hours
  })
)
app.get('/', function(req, res) {
  req.session.test = 'hey'
  res.json({
    wow: 'crazy',
  })
})

app.listen(3001)
```

​	在通过 `app.use(cookieSession())` 使用中间件之前，请求是不会设置 cookie 的，添加后再访问（并且在设置 req.session 后，若不添加 session 信息就没必要、也没内容写到 cookie 里），就能看到服务器响应头部新增了下面两行，分别写入 session 和 session.sig：

```shell
Set-Cookie: session=eyJ0ZXN0IjoiaGV5In0=; path=/; expires=Tue, 23 Feb 2021 01:07:05 GMT; httponly
Set-Cookie: session.sig=QBoXofGvnXbVoA8dDmfD-GMMM6E; path=/; expires=Tue, 23 Feb 2021 01:07:05 GMT; httponly
```

​	然后你就能在 DevTools 的 Application 标签看到 cookie 成功写入。session 的值 `eyJ0ZXN0IjoiaGV5In0=` 通过 base64 解码即可得到 `{"test":"hey"}`。

​	说回第二个值 session.sig，它是一个 27 字节的 SHA1 签名，用以**校验 session 是否被篡改**，是 cookie 安全的又一层保障。

- [x] `cookie-session缺陷`：即使现代浏览器和服务器做了一些约定，例如使用 https、跨域限制、还有上面提到 cookie 的 httponly 和 sameSite 配置等，保障了 cookie 安全。但是想想，传输安全保障了，如果有人偷看你电脑里的 cookie，密码又恰好存在 cookie，那就能无声无息地偷走密码。相反的，只放其他信息或是仅仅证明“已登录”标志的话，只要退出一次，这个 cookie 就失效了，算是降低了潜在危险。

##### 服务器存储：session-express

​	既然要储存在服务器，那么 express-session 就需要一个容器 store，它可以是内存、redis、mongoDB 等等等等，内存应该是最快的，但是重启程序就没了，redis 可以作为备选，用数据库存 session 的场景感觉不多。

> ​	源码实现：
>
> 1. `store.get(sessionID)`以`sessionID`作为参数调用容器数据
>
> 2. `Store.prototype.createSession` 这个是根据 req 和 sess 参数在 req 中设置 session 属性。其中的index的inflate函数（填充函数）就是`store.get()`
>
> ​	在监测到客户端送来的 cookie 之后，可以从 cookie 获取 sessionID，再使用 id 在 store 中获取 session 信息，挂到 `req.session` 上，经过这个中间件，你就能顺利地使用 req 中的 session。

- [x] 修改session：

  1. 根据sessionID锁定session，由于session-express是以某种方式存储（内存、数据库），就直接在存储的地方修改内容即可。
  2. 在请求没有sessionID的情况下，通过 `store.generate` 创建新的 session，在你写 session 的时候，cookie 可以不改变，只要根据原来的 cookie 访问内存里的 session 信息就可以了。

  ```js
  var express = require('express')
  var parseurl = require('parseurl')
  var session = require('express-session')
  
  var app = express()
  
  app.use(
    session({
      secret: 'keyboard cat',
      resave: false,
      saveUninitialized: true,
    })
  )
  
  app.use(function(req, res, next) {
    if (!req.session.views) {
      req.session.views = {}
    }
  
    // get the url pathname
    var pathname = parseurl(req).pathname
  
    // count the views
    req.session.views[pathname] = (req.session.views[pathname] || 0) + 1
  
    next()
  })
  
  app.get('/foo', function(req, res, next) {
    res.json({
      session: req.session,
    })
  })
  
  app.get('/bar', function(req, res, next) {
    res.send('you viewed this page ' + req.session.views['/bar'] + ' times')
  })
  
  app.listen(3001)
  ```

****

##### 两种存储方式对比

1. 时间空间：储存在**客户端**的情况，解放了服务器存放 session 的内存，但是每次都带上一堆 base64 处理的 session 信息，如果量大的话传输就会很缓慢；储存在**服务器**相反，用服务器的内存拯救了带宽。

2. 退出登录的实现和结果：

   **服务器**：储存在服务器的情况就很简单，如果 `req.session.isLogin = true` 是登录，那么 `req.session.isLogin = false` 就是退出。

   **客户端**：但是状态存放在客户端要做到真正的“即时退出登录”就很困难了。你可以在 session 信息里加上过期日期，也可以直接依靠 cookie 的过期日期，过期之后，就当是退出了。但是如果你不想等到 session 过期，现在就想退出登录！怎么办？认真想想你会发现，仅仅依靠客户端储存的 session 信息真的没有办法做到。即使你通过 `req.session = null` 删掉客户端 cookie，那也只是删掉了，但是如果有人曾经把 cookie 复制出来了，那他手上的 cookie 直到 session 信息里的过期时间前，都是有效的。 => 你没办法立即废除一个 session，这可能会造成一些隐患。

#### token

​	其实本质上 token 的功能就是和 session ID 一模一样。你把 session ID 说成 session token 也没什么问题。其中的区别在于，session id **一般**存在 cookie 里，自动带上；token **一般**是要你主动放在请求中。

> **session、session id 以及 token 都是很意识流的东西，只要你明白他是什么、怎么用就好了，怎么称呼不太重要。**
>
> e.g. JWT（JSON Web Token）！他是一个 token！但是里面放着 session 信息！放在客户端，并且可以随你选择放在 cookie 或是手动添加在 Authorization！但是他就叫 token！
>
> 所以，个人觉得你不能通过存放的位置判断是 token 或是 session id，也不能通过内容判断是 token 或是 session 信息。
>
> session 和 token 的区别就是**新旧技术的区别**。

​	cookie保存session Id，让客户端轻松；但是服务端存放很多session，让服务端不堪重负；是否有一种办法，只让客户端存储这些信息？但是如果只是客户端存放这些信息，服务端就没办法验证身份的合法性，关键点在于「验证」身份。

​	token：用户登录系统，服务器给用户发送一个token，里面包含了用户的userID。下一次用户在通过http请求访问服务器的时候，只要把token放在header中发送。不过这和cookie和session的沟通方式没有本质的区别，因为还是可以被伪造 => 数据签名加密token（SHA256+私钥加密···），服务器加密发送，接收的时候再进行解密。

​	但是这样子服务端就不用保存sessionId来进行配对了，只负责生成token和验证token，使用时间计算解密token来换取服务器的空间，减轻负载。

> Token 在权限证明上真的很重要，不可泄漏，谁拿到 token，谁就是“主人”。所以要做一个 Token 系统，刷新或删除 Token 是必须要的，这样在尽快弥补 token 泄漏的问题。

****

#### JWT

​	JWT（JSON Web Token）就是一个token，使用的是客户端存储的方式。

##### 结构

​	Header.Payload.Signature

```js
// header
{
  "alg": "HS256", // alg 代表签名算法，HMAC、SHA256、RSA 等
  "typ": "JWT" // typ 说明 token 类型是 JWT
}
// 然后将其 base64 编码。
```

```js
// payload
{
  "sub": "1234567",
  "name": "Sam",
  "admin": "true"
}
// Payload 是放置 session 信息的位置，最后也要将这些信息进行 base64 编码，
// 结果就和上面客户端储存的 session 信息差不多。

// 不过 JWT 有一些约定好的属性，被称为 Registered claims，包括：
// iss (issuer)：签发人
// exp (expiration time)：过期时间
// sub (subject)：主题
// aud (audience)：受众
// nbf (Not Before)：生效时间
// iat (Issued At)：签发时间
// jti (JWT ID)：编号
```

```js
// signature
HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)

// 使用 Header 里 alg 的算法和自己设定的密钥 secret 编码 base64UrlEncode(header) + "." + base64UrlEncode(payload)
// 最后将三部分通过 . 组合在一起
```

​	在验证用户，顺利登录后，会给用户返回 JWT。因为 JWT 的信息没有加密，所以别往里面放密码。

- [x] 缺点：JWT 也因为信息储存在客户端造成无法让自己失效的问题，这算是 JWT 的一个缺点。

****

#### OAuth2.0

[以后再整理](https://mp.weixin.qq.com/s/OG7LSVzYbMzgMEfMPu4fUQ)



## 双cookie验证？



### UN

