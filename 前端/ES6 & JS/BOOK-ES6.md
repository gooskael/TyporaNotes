[TOC]

[ESMAScript 6 入门](https://es6.ruanyifeng.com/)

****

### 1. ES6 简介

> 标准委员会最终决定，标准在每年的 6 月份正式发布一次，作为当年的正式版本。接下来的时间，就在这个版本的基础上做改动，直到下一年的 6 月份，草案就自然变成了新一年的版本。这样一来，就不需要以前的版本号了，只要用年份标记就可以了。
>
> 因此，ES6 既是一个历史名词，也是一个泛指，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等，而 ES2015 则是正式名称，特指该年发布的正式版本的语言标准。

```shell
// 查看 Node.js 默认没有打开的 ES6 实验性语法
$ node --v8-options | grep harmony
```

****

#### babel 转码器

> Babel 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在老版本的浏览器执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。

##### babel/register

> `@babel/register`模块改写`require`命令，为它加上一个钩子。此后，每当使用`require`加载`.js`、`.jsx`、`.es`和`.es6`后缀名的文件，就会先用 Babel 进行转码。

****

### 2. `let` & `const`

#### 1. `let`

> `let`声明的变量，**只在let命令所在的代码块内有效**。
>
> `var`声明的变量，在**全局范围**内都有效。
>
> ```js
> {
>   let a = 10;
>   var b = 1;
> }
> 
> a // a is not defined
> b // 1
> ```

> 根据`let`命令的这个特性，适合在`for`循环定义计数器
>
> ```js
> for(let i=0; i<10; i++){
>   // ...
> }
> ```
>
> 变量`i`是`let`声明的，当前的`i`只在本轮循环有效，所以每一次循环的`i`其实都是一个新的变量。
>
> 你可能会问，**如果每一轮循环的变量`i`都是重新声明的，那它怎么知道上一轮循环的值，从而计算出本轮循环的值？**这是因为 JavaScript 引擎内部会记住上一轮循环的值，初始化本轮的变量`i`时，就在上一轮循环的基础上进行计算。

###### let 和 var 的区别

1. `let`命令声明只在本代码块内有效，`var`命令声明在全局范围内有效。
2. `let`命令不存在[变量提升](./ES6问题汇总.md=>1.var变量的提升)，并且`let`命令不允许重复声明变量

###### 暂时性死区

> TDZ（temporal dead zone，[暂时性死区](./ES6问题汇总.md=>1.var变量的提升)）：只要块级作用域内存在`let`命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
>
> 在使用`let`命令声明变量的时候，注意不要被外部所声明的变量迷惑：
>
> ```js
> var tmp = 10;
> if (true) {
>   tmp = 100; //ReferenceError: tmp is not defined
>   let tmp;
> }
> ```
>
> ```js
> function bar(x = y, y = 2) {
>   return [x, y];
> }
> bar(); // 报错，y在使用前未声明
> 
> function bar(x = 2, y = x) {
>   return [x, y];
> }
> bar(); // [2, 2]
> ```

#### 2. 块级作用域

> 为什么需要块级作用域的原因是：
>
> 1. [函数/变量提升](./ES6问题汇总.md=>1.var变量的提升)可能会导致函数内部变量覆盖外部变量从而导致非预期结果。
>
>    > ```js
>    > var tmp = new Date();
>    > 
>    > function f() {
>    >   console.log(tmp);
>    >   if(false) {
>    >     var tmp = 'hello world';
>    >   }
>    > }
>    > 
>    > //上述代码变量和函数提升之后解释并执行的结果为：
>    > function f() {
>    >   console.log(tmp); //undefined
>    >   if(false) {
>    >     var tmp = 'hello world';
>    >   }
>    > }
>    > var tmp;
>    > tmp = new Date();
>    > ```
>
> 2. 用来计数的循环变量泄露为全局变量
>
> ```js
> var s = 'hello';
> 
> for (var i = 0; i < s.length; i++) {
>   console.log(s[i]);
> }
> // 变量i只用来控制循环，但是循环结束后，它并没有消失，泄露成了全局变量。
> console.log(i); // 5
> ```

#### ES6的块级作用域

> ES6中`let`实际上为JS新增了块作用域，每一层都是单独的作用域。
>
> 块级作用域`{}`
>
> ```js
> function f1() {
>   let n = 5;
>   if (true) {
>     let n = 10;
>   }
>   console.log(n); // 5
> }
> ```
>
> ```javascript
> // 内层作用域 可以定义 外层作用域 的同名变量
> {{{{
>   let insane = 'Hello World';
>   {let insane = 'Hello World'}
> }}}};
> ```

##### ES5、ES6的块域函数声明(了解)

> 避免在块域里面声明函数。

```js
// 情况一
if (true) {
  function f() {}
}

// 情况二
try {
  function f() {}
} catch(e) {
  // ...
}
```

`ES5`：上面两种函数声明对于ES5来说都是非法的。但是，浏览器没有遵守这个规定，**为了兼容以前的旧代码，还是支持在块级作用域之中声明函数**，因此上面两种情况实际都能运行，不会报错。

> ```javascript
> function f() { console.log('I am outside!'); }
> (function () {
>   if (false) {
>     // 重复声明一次函数f
>     function f() { console.log('I am inside!'); }
>   }
>   f();
> }());
> 
> // ES5环境下，JS引擎会解释并执行成：
> function f() { console.log('I am outside!'); }
> (function () {
>   function f() { console.log('I am inside!'); }
>   if (false) {
>   }
>   f(); // I am inside!
> }());
> ```

`ES6`：引入了块级作用域，明确允许在块级作用域之中声明函数。ES6 规定，块级作用域之中，函数声明语句的行为类似于`let`，在块级作用域之外不可引用。

> - 允许在块级作用域内声明函数。
> - 函数声明类似于`var`，即会提升到全局作用域或函数作用域的头部。
> - 同时，函数声明还会提升到所在的块级作用域的头部。
>
> 上面三条规则只对 ES6 的浏览器实现有效，其他环境的实现不用遵守，还是将块级作用域的函数声明当作`let`处理。

> ```js
> function f() { console.log('I am outside!'); }
> (function () {
>   if (false) {
>     // 重复声明一次函数f
>     function f() { console.log('I am inside!'); }
>   }
>   f();
> }());
> 
> // ES6环境下，JS引擎会解释并执行成：
> function f() { console.log('I am outside!'); }
> (function () {
>   var f = undefined;
>   if (false) {
>     function f() { console.log('I am inside!'); }
>   }
>   f();
> }());
> ```
>
> 















