[TOC]



### 1. var变量的提升

[var变量的提升](https://www.cnblogs.com/shmilynanmei/p/9151769.html)

###### `var`函数提升&变量提升

> 首先js引擎在读取js代码时会进行两个步骤，第一个步骤是解释，第二个步骤是执行。
>
> **解释**：就是会先通篇扫描所有的js代码，然后把所有声明提升到顶端，第二步才是执行。
>
> **IMPO**：声明包括`函数声明`和`变量声明`，而且注意的是只把声明提升了，赋值等其他的内容还是按照原顺序。

> 所谓的`变量提升`，就是**把变量声明提升到当前执行环境的最顶端**(本级域内的最顶端)。
>
> ```js
> console.log(a); //undefined
> var a = 10;
> 
> //上述的这段代码首先经过js引擎的解释，解释成：
> var a;
> console.log(a); //undefined
> a = 10;
> ```
>
> 除了`变量声明提升`，还有`函数声明提升`，并且后者提升在前者提升上面。
>
> ```js
> foo();
> function foo() {
>   console.log('aaa');
> }
> 
> //上述的这段代码，解释成：
> function foo() {
> 	console.log('aaa');
> }
> foo(); //aaa
> ```
>
> ```js
> foo();
> foo = function foo() {
>   console.log('aaa');
> }
> 
> //上述的这段代码，解释成：
> var foo; //声明提升，从赋值语句中直接解释出来的
> foo(); //foo is not a function
> foo = function() {
>   console.log('aaa');
> }
> ```
>
> ```js
> console.log(foo); // (1)
> var foo = 10;
> function foo() {
>   console.log(10); // (2)
> }
> console.log(foo); // (3)
> 
> //上述的代码解释成：
> function foo() {
>   console.log(10);
> } //函数声明在最上面
> var foo; //变量声明
> console.log(foo) //(1) foo(){ console.log(10); }
> foo = 10;
> function foo() {
>   console.log(10); //(2) 10
> } 
> console.log(foo); //(3) 10
> ```

###### `let`无变量提升 & 暂时性死区

> `let`命令要求必须在使用变量之前就把变量声明完毕，如果按照var的方式，会报错而不是返回`undefined`
>
> ```js
> console.log(a); //ReferenceError: a is not defined
> let a = 10; 
> ```
>
> 因为在使用`let`命令声明变量的时候，必须保证变量的声明在变量使用之前，即如果使用了`let`命令，顺序必须严格按照`声明变量 -> 使用变量`的顺序，如果不按照顺序就会进行报错。因此在一下情况下，就算在外部定义了一个全局作用的变量，如果在内部使用了`let`命令，就会隔绝外部的作用，也必须在本域内严格按照`声明变量 -> 使用变量`。
>
> ```js
> var tmp = 10;
> if (true) {
>   tmp = 100; //ReferenceError: tmp is not defined
>   let tmp;
> }
> ```
>
> 在上面的这种情况下，首先遍历代码找到`let`命令：`let tmp;`。然后隔绝了`tmp`全局定义的作用，即`tmp`被绑定在本区域内--if函数内部，于是外部`var`声明的全局性就无法作用在该函数内部。这时候判断`tmp = 100;`是在`let`命令声明变量之前，就会报错Error。

****

### 2. typeof

`typeof`是js中用来检测一个变量的类型的。

****

### 3. IIFE

[说一说JS的IIFE](https://www.cnblogs.com/yiven/p/8462666.html)

> IIFE（Immediately Invoked Function Expression，立即调用的函数表达式），声明函数的同时立即调用这个函数，是JS为了弥补`var`命令声明的时候可能引起的作用域泄漏的问题解决方式。
>
> 写法： `()()` / `(())`，在第一个左括号后添加想要立即执行的函数。
>
> ```js
> // ()()
> (function foo(){
>   var a = 3;
>   console.log(a);
> })()
> ```
>
> ```js
> // (())
> (function foo(){
>   var a = 3;
>   console.log(a);
> }())
> ```
>
> 使用IIFE就可以解决变量作用域泄漏的问题：
>
> ```js
> var a = 2;
> (function IIFE(global){
>     var a = 3;
>     console.log(a); // 3
>     console.log(global.a); // 2
> })(window);
> 
> console.log(a); // 2
> ```
>
> 

### 4. 浅拷贝和深拷贝

[浅谈JS中的浅拷贝和深拷贝](https://www.cnblogs.com/chengxs/p/10788442.html)

`浅拷贝`：拷贝开销小，拷贝完之后双方会互相影响。

```js
// 赋值：会影响
arr1 = [1, 2];
arrNew = arr1; // 浅拷贝 arrNew: [1, 2]
arrNew[0] = 2; // arr1 = arrNew = [2, 2]

// 拓展：当数组的子属性是对象的时候，操作对象元素会影响
var arr3 = [{name: 'A', age: '10'}, {name: 'B', age: '20'}];
var arr4 = [{name: 'C', age: '30'}, {name: 'D', age: '40'}];
var arrOb = [...arr3, ...arr4];
// 操作对象不会影响
arrOb[0] = 0;  // arr3: [{name: 'A', age: '10'}, {name: 'B', age: '20'}];
// 操作对象的元素会影响
arrOb[0].name = 'F'; // arr3: [{name: 'F', age: '10'}, {name: 'B', age: '20'}];
```

`深拷贝`：拷贝开销大，拷贝完之后双方不会相互影响。

```js
// 使用slice可以深拷贝
arr1 = [1, 2, 3 ,4];
arr = arr1.slice(0,4); //arr: [1, 2, 3, 4]
```

### 

<img src="/Users/samstephen/Library/Application Support/typora-user-images/image-20210107134128940.png" alt="image-20210107134128940" style="zoom:50%;" align="left"/>