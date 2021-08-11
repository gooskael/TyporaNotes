[TOC]

[ESMAScript 6 入门](https://es6.ruanyifeng.com/)

****

# C01 - ECMAScript 6 简介

## 1.1 ES6 简介

> 标准委员会最终决定，标准在每年的 6 月份正式发布一次，作为当年的正式版本。接下来的时间，就在这个版本的基础上做改动，直到下一年的 6 月份，草案就自然变成了新一年的版本。这样一来，就不需要以前的版本号了，只要用年份标记就可以了。
>
> 因此，ES6 既是一个历史名词，也是一个泛指，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等，而 ES2015 则是正式名称，特指该年发布的正式版本的语言标准。

```shell
// 查看 Node.js 默认没有打开的 ES6 实验性语法
$ node --v8-options | grep harmony
```

## 1.2 babel 转码器

> Babel 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在老版本的浏览器执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。

### `babel/register`

> `@babel/register`模块改写`require`命令，为它加上一个钩子。此后，每当使用`require`加载`.js`、`.jsx`、`.es`和`.es6`后缀名的文件，就会先用 Babel 进行转码。

****

# C02 - let 和 const 命令

## 2.1 `let`

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

###  let 和 var 的区别

1. `let`命令声明只在本代码块内有效，`var`命令声明在全局范围内有效。
2. `let`命令不存在[变量提升](./ES6问题汇总.md=>1.var变量的提升)，并且`let`命令不允许重复声明变量

### 暂时性死区

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

## 2.2 块级作用域

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

### ES6的块级作用域

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

### ES5、ES6的块域函数声明(了解)

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

****

# C03 - 解构赋值

## 3.1 数组

```js
// 正常的“模式匹配”
let [a, b, c] = [1, 2, 3] // a=1, b=2, c=3
let [a, [[b], c]] = [1, [[2], 3]] // a=1, b=2, c=3
let [ , , c] = [1, 2, 3] // c=3
let [x, , y] = [1, 2, 3] // x=1, y=3
// 搭配扩展符
let [x, ...y] = [1, 2, 3] // x=1, y=[2, 3]

// 解构不成功，赋值undefined
let [x, y, ...z] = [1] // x=1, y=undefined, z=[]
let [x] = [] // x=undefined

// 不完全解构
let [x, y] = [1, 2, 3] // x=1, y=2

// 默认值，只有严格等于undefined时生效
let [foo = true] = []; // foo = true
let [foo = true] = [undefined] // foo = true
let [foo = true] = [null] // foo = null
```

****

## 3.2 对象

```js
// 和数组解构不同，对象解构不需要次序一致，只要变量和属性同名
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo // 'aaa'
bar // 'bbb'

// 也可以不同名，左侧foo为模式，右侧newFoo为变量
let { foo: newFoo, bar } = { foo: 'aaa', bar: 'bbb' };
newFoo // 'aaa'
bar // 'bbb'

// 解构不成功，赋值undefined
let { foo } = { bar: 'bbb' }
foo // undefined

// 默认值，对象的属性值严格等于undefined时生效
const { x = 3 } = { x: undefined }; // x = 3
const { x = 3 } = { x: null }; // x = null
```

:exclamation: `{x} = {x: 1}` 会报错，因为 JavaScript 引擎会将 `{x}` 理解成一个代码块。

****

## 3.3 其他解构

字符串：

```js
const [a, b, c, d, e] = 'hello';
// a: 'h' ·····

let {length: len} = 'hello';
len // 5
```

数值和布尔值：如果等号右边是数值和布尔值，则会先转为对象。

```js
let { toString: s } = 123; // s = '123'
let { toString: s } = true; // s = 'true'

// undefined 和 null 无法转为对象，报错
let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
```

函数：

```js
// 简单解构
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3

// 默认值
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]

// undefined触发默认值
[1, undefined, 3].map((x = 'yes') => x); // [1, 'yes', 3]
```

## 3.4 用途

### 1. 交换变量值

```js
[x, y] = [y, x];
```

### 2. 函数返回多个值

```js
function example() {
	return [1, 2, 3]; // 返回数组
  return { foo: 1, bar: 2 } // 返回对象
}
let [a, b, c] = example();
let { foo, bar } = example();
```

### 3. 提取 JSON 数据

```js
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;
console.log(id, status, number);
```

### 4. 遍历 Map 结构

```js
// 获取 key 和 value
for(let [key, value] of map) { }

// 获取 key
for(let [key] of map) {}

// 获取 value
for(let [ , value] of map) {}
```

### 5. 输入模块的指定方法

```js
const { SourceMapConsumer, SourceNode } = require("source-map");
```



# C09 - 数组的扩展

## 9.1 扩展运算符 `...`

​	将一个数组转为用逗号隔开的**参数序列**。

:exclamation:注意是展开成序列，如果要变成数组，还需要添加`[]`。

```js
...[1, 2, 3, 4] => 1, 2, 3, 4
```

### 展开成函数参数列表

```js
// 主要用于函数调用，将数组转换为arguments参数列表：
Math.max(...[1, 2, 3, 4]); // 求max值的
arr1.push(...[1, 2, 3]); // push一个数组
new Date(...[2015, 1, 1]); // 数组记录日期
```

### 复制数组

​	都是浅拷贝。

```js
const a1 = [1, 2];

// ES5
const a2 = a1.concat();
// ES6
const a2 = [...a1];
```

### 合并数组

```js
arr1 = [1, 2];
arr2 = [3];
arr3 = [4, 5];

// ES5，使用concat
arr.concat(arr1, arr2);

// ES6
[...arr1, ...arr2, ...arr3];
```

### 解构赋值

​	解构赋值必须把`...`放在参数的最后一个位置。

```js
const [first, ...rest] = [1, 2, 3, 4];
first // 1
rest // [2, 3, 4]

const [first, ...rest] = [];
first // undefined
rest // []
```

### 字符串转换成数组

```js
[...'hello'] // ["h", "e", "l", "l", "o"]

// 另：JS会将32位Unicode字符识别为2个字符，采用...就没有这个问题
'x\uD83D\uDE80y'.length // 4
[...'x\uD83D\uDE80y'].length // 3
```

### Iterator - pending

****

## 9.2 Array.from()

​	接受三个参数。

```js
// arg[0], 调用该方法的对象
// arg[1], 传入的 map 方法
// arg[2], map 方法的 this 指针
Array.from(obj, x => x * x, this);
```

#### 类似数组的对象

​	所谓类似数组的对象（array-like object），本质特征只有一点，即必须有 length 属性。常见的包括 `NodeList对象` 和 `argument对象`。`[Arguments] { '0': [2, 7, 10], '1': 9}`。

```js
// array-like object
// key-value 取 value 形成 Array
let arrayLike = {
  '0': 'a',
  '1': 'b',
  '2': 'c',
  length: 3
};

let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']

// 任何有length属性的对象，都可以通过 Array.from 方法转为数组
Array.from({ length: 3}); // [ undefined, undefined, undefined ]
```

### 可遍历(iterable)对象

​	只要是部署了 Iterator 接口的数据结构（包括ES6新增的 Set 和 Map），都能将其转为数组。

```js
Array.from('hello'); // [ 'h', 'e', 'l', 'l', 'o' ]
Array.from(new Set(['a', 'b'])); // ['a', 'b']
Array.from([1, 2, 3]); // [1, 2, 3] // 返回原数组
```

****

## 9.3 Array.of()

​	主要是用来弥补`Array()`构造函数的不足，即参数个数的不同会有行为差异。`Array.of()` 总是根据 arguments 返回一个数组。

```js
// Array()
// 只有一个参数时，表示声明数组的长度
Array(); // []
Array(3); // [ , , ]  // 返回都是空位
// 多个参数时，表示数组
Array(1,2,3,4); // [1, 2, 3, 4]

// Array.of() 始终生成数组
Array.of(); // []
Array.of(undefined) // [undefined]
Array.of(3); // [3]
Array.of(1,2,3,4); // [1, 2, 3, 4]
```

****

## 9.4 copyWithin()

​	将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。使用这个方法，会**修改当前数组**。`Array.prototype.copyWithin(target, start = 0, end = this.length)`。

```js
// target: 从该位置开始替换数据，保留之前的
// start: 从该位置开始作为copy源
// end; 到该位置作为copy源的尾部（不包含）
[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
```

## 9.5 find() & findIndex()

`find`找出第一个符合条件的数组成员，如果没有符合条件的成员，则返回`undefined`。

`findIndex`返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。

第一个参数接收回调函数，第二个参数绑定回调函数的`this`对象。

```js
// find
[1, 4, -5, 10].find( n => n < 0) // -5
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10

// findIndex
[1, 4, -5, 10].find( n => n < 0) // 2
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 2

// 绑定this对象
function f(v){
  return v > this.age;
}
let person = {name: 'John', age: 20};
[10, 12, 26, 15].find(f, person);    // 26
```

:exclamation:这两个方法都可以发现`NaN`，弥补了数组的`indexOf`方法的不足。

```js
[NaN].indexOf(NaN)
// -1

[NaN].findIndex(y => Object.is(NaN, y))
// 0
```

****

## 9.6 fill()

```js
['a', 'b', 'c'].fill(7) // [7, 7, 7]
new Array(3).fill(7) // [7, 7, 7]

// 可以指定起始和终止位置
['a', 'b', 'c'].fill(7, 1, 2) // ['a', 7, 'c']

// 如果填充的是对象，那么被赋值的是同一个内存地址的对象，不是深拷贝对象
let arr = new Array(3).fill({ name: 'Mike'});
arr[0].name = 'Ben'; // [{ name: 'Ben'}, { name: 'Ben'}, { name: 'Ben'}]
```

****

## 9.7 entries(), keys() & values()

```js
// keys 遍历键名
// values 遍历键值
// entries 遍历键值对
for(let index of ['a', 'b'].keys()) {
  // 0, 1
}

for(let item of ['a', 'b'].values()) {
  // 'a', 'b'
}

for(let [index, elem] of ['a', 'b'].entries()) {
  // 0 "a", 1 "b"
}
```

****

## 9.8 includes()

​	判断是否含有某值，返回布尔值，可以判断 `NaN`。

```js
// 接受第二个参数，如果为负数则倒数，如果负数超出长度则重置为0
[1, 2, NaN].includes(NaN) // true
[1, 2, 3].includes(3, -1) // true
[1, 2, 3].includes(1, -4) // true
```

****

## 9.9 flat() & flatMap()

```js
// flat() 用于将数组降维拉平，跳过空位
[1, 2, [3, [4, 5]]].flat() // [1, 2, 3, [4, 5]]
[1, 2, [3, [4, 5]]].flat(2) // [1, 2, 3, 4, 5]
[1, 2, [3, [4, [5, 6]]].flat(Infinity) // [1, 2, 3, 4, 5, 6]
 
// flatMap 相当于 .map() + .flat()
[2, 3, 4].flatMap(x => [x, x * 2]) // [2 ,4 , 3, 6, 4, 8]
// [[2, 4], [3, 6], [4, 8]].flat()
```

****

## 9.10 数组空位

​	数组的空位指，数组的某一个位置没有任何值。比如，`Array`构造函数返回的数组都是空位。

```js
// ES6中，明确将空位转为 undefined
Array.from(['a', , 'b']) // ['a', undefined, 'b']
[...['a', , 'b']] // ['a', undefined, 'b']

// entries, keys, values
[...[ ,'a'].entries()] // [[0, undefined], [1, "a"]]
[...[ ,'a'].keys()] // [0, 1]
[...[ ,'a'].values()] // [undefined, "a"]

// find, findIndex
[,'a'].find(x => true) // undefined
[,'a'].findIndex(x => true) // 0

// copyWithin, fill, for...of 会把空位考虑为正常元素
[ , 'a', 'b', , ].copyWithin(2,0) // [ , 'a', , 'a']
new Array(3).fill('a') // ['a', 'a', 'a']
let arr = [, ,];
for (let i of arr) {
  console.log(1);
} // 1 1
```

- [x] `let arr = [ , 'a', 'b', , ]`，length为4，一般最后的`,`后如果没内容，则认定没有元素
- [x] `let arr = new Array(3)`，则类似`let arr = [ , , ,]`。
- [x] 一般不要显式使用空位，应该避免出现空位。



# 14. Set 和 Map

## 14.1 Set

​	Set 类似数组，但是成员的值都是唯一的，没有重复的值。

:exclamation: 向 Set 加入值的时候，不会发生类型转换，即 `5` 和 `'5'` 不同。但 `NaN` 和 `NaN` 是相同的。

```js
// NaN 在set中相同， 空对象 {} 不同
const s = new Set();
s.add(NaN).add(NaN); // size = 1，认定 NaN 和 NaN相同
s.add({}).add({}); // size = 3, 认定 {} 和 {} 是两个不同的对象
```

### 1. 用法：

```js
// 通过构造函数生成
const empty = new Set();
const filled = new Set([1, 1, 2, 3, 3, 4]) // [...filled] = [1, 2, 3, 4]

// add 添加，delete 删除，clear 清空
empty.add(1).add(2).add(3) // 可以连续添加， [...set] = [1, 2, 3]
empty.delete(1) // 删除成功会返回true [...set] = [2, 3]
empty.clear() // 清除所有成员，没有返回值 [...set] = []

// has，查询，返回布尔值
s.has(1) // false
```

### 2. 遍历：

:exclamation: `Set` 的遍历顺序就是插入顺序。且没有键名，只有键值（或者说键名和键值是同一个值）。

```js
// keys和values表现一致，因为键名和键值一致
let set = new Set([1, 2, 3]);
for(let item of set.keys()) {} // 1, 2, 3
for(let item of set.values()) {} // 1, 2, 3

// entries
for(let item of set.entries()) {} // [1, 1], [2, 2], [3, 3]

// 默认遍历器是values
for(let x of set) { } // 即let item of set.keys()

// forEach，value和key是一样的值
set.forEach((value, key) => console.log(key + ' : ' + value))
```

### 3. 应用：

```js
// 去除数组的重复成员和字符串重复字符
[...new Set(array)]
[...new Set('ababbc')].join('') // 'abc'

// 去除重复，另一种方法
function dedupe(array) {
  return Array.from(new Set(array));
}
dedupe([1, 1, 2, 3]) // [1, 2, 3]

// 并集、交集、差
let union = new Set([...a, ...b]); // 并
let intersect = new Set([...a].filter(x => b.has(x))); // 交
let difference = new Set([...a].filter(x => !b.has(x))); // a相对于b的差集
```

### 4. 改变原set

```js
let set = new Set([1, 2, 3]);

// 1. map
set = new Set([...set].map(val => val * 2));
// 2.Array.from 中的 map
set = new Set(Array.from(set, val => val * 2));
```

