[TOC]

本文档内容来自书籍[HTML5+CSS3+JavaScript入门与应用](刘爱江 靳智良编著)

### 网页与网站

1. > 网页(web page)是网站中使用HTML等标记语言编写而成的单个文档。

2. > 网站(web site)就是多个网页的集合，即根据一定的规则，将用于展示特定内容的相关网页，通过超链接构成一个整体。网站的目录结构包括HTML(页面)、Images(图片)、CSS(样式表)、Assets(素材)。

3. > 当前网页的标准是**DOM**(Document Obeject Model，文档对象模型)和**ECMAScript**。根据W3C DOM规范，**DOM是一种与浏览器、平台和语言相关的接口，使得用户可以访问页面其他的标准组件**。

[虚拟DOM和真实DOM](../VUE/vue问题汇总.md)



### HTML与CSS3、XHTML、HTML5

#### HTML & CSS3

- > 在web标准布局的页面中，**表现部分和结构部分是各自独立的**。
  >
  > 结构部分是用HTML或XHTML编写的，
  >
  > 表现部分是用可以调用的CSS文件实现的。

- > CSS3式CSS技术的升级版本，也是对CSS2的扩展。

```html
<link href="style.css" type="text/css" rel="stylesheet" /> <!-- 调用样式代码-->
<table ··· >
  <tr><td><div class="unnamed1">
    sample
    </div></td></tr>
```

```css
.unnamed1{
  background-position:center;
  text-align:center;
  color:#CC0000;
}
```

###### 此处代码有待验证

#### HTML & XHTML

- > HTML的全称是HyperText Markup Language(超文本标记语言)。
  >
  > 注意，初学者不要把HTML语言和Java，C#等编程语言混淆起来(把HTML想得很复杂)，**HTML只是一种标记语言**。简单地说，**HTML文件就是普通文本加上HTML标记，只是不同的标记能表示不同的效果。**

- > XHTML的全称是eXtensible HyperText Markup Language(可扩展的超文本标记语言)。
  >
  > XHTML致力于消除HTML的不规范。要求：
  >
  > 1. 整个文档有且只有一个根元素。
  > 2. 每个元素都由开始标签和结束标签组成。(<h2> </h2>)
  > 3. 元素与元素之间应该合理嵌套。(<h2> </p>不合理)
  > 4. 元素的属性必须有属性值，而且属性值应该是用引号(单/双)括起来。



#### HTML & HTML5

- > 现有的HTML页面大量存在一下4种不符合规范的内容。
  >
  > 1. 元素标签大小写混乱。如(<span></sPaN>)
  > 2. 元素没有合理结束。如<li> hi
  > 3. 元素中使用了属性，但是没有指定属性值。如<input type="text" disabled>
  > 4. 为元素的属性指定值时未加引号。如<input type=text>

- > HTML5干脆承认它们是符合规范的。
  >
  > HTML5兼容HTML。HTML5的语法是为了保证与之前的HTML语法达到最大限度的兼容而设计的。

##### HTML5可省略的标记

> 具体来划分，可以讲HTML5的标记分为“不允许写结束标记”“可以省略结束标记”和“开始标记与结束标记均可省略“三种类型。
>
> 1.不允许写结束标记。如<input />
>
> br、col、img、input、link、meta
>
> area、basel、command、embed、hr、keygen、param、source、track、wbr
>
> 2.可以省略结束标记。如<li>
>
> li、p、tr、td、th
>
> dt、dd、rt、rp、optgroup、option、colgroup、thead、tbody、tfoot
>
> 3.开始标记与结束标记均可省略。如<body>
>
> html、head、body、colgroup、tbody

##### HTML5具有布尔值的属性

> disabled和readonly属性的值都是布尔值。
>
> 如果想要将属性值设置为false，那么可以不使用该属性。
>
> 如果要将具有布尔值的属性值设置为true，有一下四种方法。
>
> 1. 只写属性不写属性值
> 2. 将属性的属性值指定为true
> 3. 将属性值指定为空字符串
> 4. 将属性值指定为当前属性，即属性值等于属性名

可以看到布尔值默认为false，设置true则分为隐式、显式、半显式、自显式（对应1-4）

##### HTML5引号的省略

> 在HTML中为属性指定属性值时，属性值两遍既可以用双引号，也可以用单引号。
>
> HTML5在此基础上进行了更改，当**属性值不包括空字符串、<、>、单引号、双引号和空格**等字符时，属性值两遍的引号可以省略。