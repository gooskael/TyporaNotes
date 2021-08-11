[TOC]



## 1. Array

### 1 `arr.splice`

​	参考[JS中的splice方法](https://www.cnblogs.com/tian874540961/p/10246332.html)；

```js
arr.splice(m, n); // 从index为m开始操作，删除n个元素
arr.splice(m, 0, ...arr1); // 在m之后插入arr1
```

### 2 `arr.sort()`：参考[sort(function(a,b){return a -b})函数排序问题](https://blog.csdn.net/qq_43058026/article/details/104531495)；

```js
arr.sort((a,b) => a-b); //从小到大排序，箭头函数实现「大的往后移」
```

### 3 `arr.reduce()`

​	返回一个值，即数组的sum，但是不会对原数组进行更改。

### 4 `arr.includes()`

​	包含某个值。

### 5 `arr.find|arr.findIndex`

​	参考[find&findIndex](https://www.cnblogs.com/pwindy/p/13081171.html)。

```js
arr.find(value => value === 1)
arr.find((value, index) => index === 1) // 返回value

arr.findIndex(value => value === 1) // 返回index

// 对象
const arr = [{id:1, name: 'a'}, {id:2, name: 'b'}];
let index = arr.findIndex((value) => value.name === 'a')
let name = arr[index].name
```

### 6 `arr.join()`

​	把数组每个相邻元素之间使用一个符号连接起来。

```js
let arr = [1, 2, 3, 4];
arr.join('-'); // 1-2-3-4
```

### 7 `arr.slice()`

```js
let arr = [11, 22, 33, 44, 55];
console.log(arr.slice(0,3)) // [11, 22, 33]
```

### 8 `arr.reverse()`

```js
let arr = [1, 2, 3];
arr.reverse(); // [3, 2, 1]
```

### 9 `arr.map` & `forEach`

​	都不会改变原数组。参考：[forEach 和 map 和 for方法的区别](https://www.cnblogs.com/chaoyuehedy/p/6905422.html)。

```js
arr.map((value, index, arr) => {
  
})
```

****

## 2. String

### 1 JSON.stringify()

```js
let arr = [1, 2, 3];
let str = JSON.stringify(arr);
```

****

### 2 str.repeat(time)

```js
result = '';
result += 'hey'.repeat(3); // heyheyhey
```

****

### 3 str.localeCompare()

```js
// 比较字符串
let str1 = 'string';
let str2 = 'strinh';
str1.localeCompare(str2); // -1

## 3. Math

### 1 `Math.floor` & `Math.ceil` & `Math.around`

​	向下取整和向上取整、四舍五入

### 2 `Math.max` & `Math.min`

​	注意输入的参数是`(1, 2, 3, 4)`这样的，因此传入数组的时候需要展开符号`...`。

```js
arr = [1, 2, 3, 4];
let maxNum = Math.max(...arr); // 4
```

### 3 `Math.pow`

​	n的x次方表达式。

```js
let sNum = Math.pow(2, 31); // 2的31次方
let aNum = Math.pow(2, -31); // 2的-31次方
```

### 4 `Math.abs`

​	取绝对值。

****

## 4. Map

​	参考：[map](https://www.cnblogs.com/yuer20180726/p/11387699.html)。

​	有`has`、`set`、`get`、`keys`。

### Map.keys

```js
// 获取所有keys
let map = new Map();
// ···进行了一系列操作
const keysArr = [...map.keys()].sort((a,b) => a-b);
```



### Q: Java - hashmap hashset

[github - hashMap](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E5%AE%B9%E5%99%A8.md#%E9%80%82%E9%85%8D%E5%99%A8%E6%A8%A1%E5%BC%8F)

[hashmap & hashset](https://blog.csdn.net/woshiluoye9/article/details/56667810)

```js
let map = new Map();
// 存储方式是二维数组
map.set('key1', 'value1'); // set
map.set('key2', 'value2');
map.set('key3', 'value3');
[
  ["key1", "value1"],
  ["key2", "value2"],
  ["key3", "value3"]
]

// map遍历
for(let item of mapItem) {
  let key = item[0];
  let value = item[1];
}

// 一般使用方法
map.get('key1');
map.has('key1');
map.set('key', 'value');
map.keys(); // 返回包含所有key的iterator
```

## problems pending

[KMP](http://www.ruanyifeng.com/blog/2013/05/Knuth–Morris–Pratt_algorithm.html)

