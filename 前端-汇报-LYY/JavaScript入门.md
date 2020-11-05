### JavaScript入门

[TOC]



#### 什么是JavaScript？

JavaScript 是一种<u>轻量级的脚本语言</u>。所谓“脚本语言”（script language），指的是它<u>不具备开发操作系统的能力</u>，而是只用来<u>编写控制其他大型应用程序（比如浏览器）的“脚本”</u>。

JavaScript 也是一种<u>嵌入式（embedded）</u>语言。它本身提供的核心语法不算很多，只能用来做一些数学和逻辑运算。JavaScript 本身不提供任何与 I/O（输入/输出）相关的 API，都要<u>靠宿主环境（host）提供</u>，所以 JavaScript 只合适嵌入更大型的应用程序环境，去调用宿主环境提供的底层 API。

目前，已经嵌入 JavaScript 的宿主环境有多种，最常见的环境就是<u>浏览器</u>，另外还有<u>服务器环境</u>，也就是 Node 项目。

从语法角度看，JavaScript 语言是一种“对象模型”语言。<u>各种宿主环境通过这个模型，描述自己的功能和操作接口，从而通过 JavaScript 控制这些功能</u>。但是，JavaScript 并不是纯粹的“面向对象语言”，还支持其他编程范式（比如函数式编程）。

JavaScript 的核心语法部分相当精简，只包括两个部分：<u>基本的语法构造</u>（比如操作符、控制结构、语句）和<u>标准库</u>（就是一系列具有各种功能的对象比如`Array`、`Date`、`Math`等）。除此之外，各种宿主环境提供额外的 API（即只能在该环境使用的接口），以便 JavaScript 调用。以浏览器为例，它提供的额外 API 可以分成三大类。

- 浏览器控制类：操作浏览器
- DOM 类：操作网页的各种元素
- Web 类：实现互联网的各种功能

如果宿主环境是服务器，则会提供各种操作系统的 API，比如文件操作 API、网络通信 API等等。这些你都可以在 Node 环境中找到。

#### JavaScript与ECMAScript

ECMAScript 只用来标准化 JavaScript 这种语言的基本语法结构，可以理解为是JavaScript的一个标准。

#### 基本语法

https://wangdoc.com/javascript/basic/grammar.html

##### 定义变量

```javascript
var a = 1;
var b; // undefined
b = 'aaa';
a = 'test'; // JavaScript是一种动态类型语言，变量可以随时改变类型
```

##### `==`和`===`

`==` 会先将数据进行类型转换，然后再用严格相等运算符"==="比较。

```javascript
'' == '0'          // false
0 == ''            // true
0 == '0'            // true
false == 'false'    // false
false == '0'        // true
false == undefined  // false
false == null      // false
null == undefined  // true
' \t\r\n ' == 0    // true
```

`===` 严格相等，会比较两个值的类型和值

推荐使用 `===` 进行判断。



#### ES6新语法

ES6入门教程：https://es6.ruanyifeng.com/

##### let和const关键字

```js
let a = 1;
const b = 2;
```

##### 深拷贝数组

```js
let list1 = [1, 2, 3];
let list2 = [...list1, 5];
```

##### 对象解构

```js
let testObj = {foo: "aaa", bar: "bbb"};
let {foo} = testObj;
```



#### 参考资料

函数式编程初探 阮一峰：https://www.ruanyifeng.com/blog/2012/04/functional_programming.html

MDN JavaScript教程： https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript

现代JavaScript教程：https://zh.javascript.info/

JavaScript的基本语法：https://wangdoc.com/javascript/basic/grammar.html

JavaScript秘密花园：https://bonsaiden.github.io/JavaScript-Garden/zh/