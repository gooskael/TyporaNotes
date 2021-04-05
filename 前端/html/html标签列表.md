[TOC]

参考[html标签列表](https://www.runoob.com/tags/html-reference.html)



### 常用标签及用法

#### a 超链接/锚点 anchor

```html
<a href="#"> 这是不会跳转的超链接，但是可以点击</a>
<a href="https://www.baidu.com/"> 这是会跳转到相应页面的链接 </a>
```

##### 通过嵌套实现其他形式超链接

```html
<!-- 实现图片超链接 -->
<a href="#">
	<img src="../image/demo.jpg" width="100" height="100" />
</a>
<!-- 由于html5不再支持<a>的“coords”(x1,y1,x2,y2)和“shape”(circle|rect) -->
```

##### 跳转到本页面的某个位置

```html
<!-- 跳转到本页面的某个位置 -->
<a href = "#destination">跳转到对应id位置</a>
<h2 id = "destination">
  这是想要跳转到的位置
</h2>
```

#### base 默认地址

```html
<head>
  <base href="http://www.oa.cn/" target="_blank" /> <!-- 网址 -->
  <base href="../html/"> <!-- 本地文件 -->
</head>
<body>
  <a href="index.html"> 跳转到../html/index.html </a>
</body>
```

#### b 加粗字体

```html
<b> 加粗字体 </b>
```

#### blockquote 引用

```html
<blockquote>
  这是一段长引用，顶格，不带缩进
  <p> 引用第一段的文字，会自动带缩进 </p>
  <p> 引用第二段的文字，会自动带锁紧 </p>
</blockquote>
```

#### body 主体

```html
<body>
  <div></div>
  <article></article>
</body>
```

```html
<!-- 属性，都建议使用样式取代属性赋值 -->
<body
      bgcolor="yellow" //背景颜色
      background="../image/demo_image.jpg" //背景图片，会覆盖背景颜色
      link="blue" //链接的默认颜色
      alink="yellow" //点击链接元素后会变化成该颜色 >
</body>
```

```html
<!-- 属性，使用CSS样式 -->
<body style="background-color:yellow"></body>
<body style="background-image:url(../../images/earth.jpg)"></body>
<style>
  a:link{color:blue}
  a:active{color:yellow}
</style>
```

###### a:link不起作用？

> ```a:link```的含义是，没有点击过的时候。但是注意，电脑本身会有缓存，因此如果不清缓存，那么历史点击过的话，也算是已经点击过了。这时候就没有```a:link```发挥作用的时候了。

#### br 换行

```html
<br />
```

#### button 按键

````html
<button>
  这是一个按键
</button>
````

#### cite 引用

```html
<cite> 这是一段引用，会显示成斜体 </cite>
```

#### p 段落

```html
<!-- html5已经废弃align属性，要使用css样式 -->
<p style="text-align:left|right|center|justify">
  justify表示对行进行伸展，这样每行都可以有相等的宽度（就像在报纸和杂志中）。
</p>
```

#### ```table```

```rule``` ：规定内侧边框的哪个部分是可见的。

```html
<table rule="rows"></table> //则横向的边框是可以看见，其他边框隐藏
```

