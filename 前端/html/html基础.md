[TOC]

本文档内容来自书籍[HTML5+CSS3+JavaScript入门与应用](刘爱江 靳智良编著)

### HTML根元素

> 一个HTML文档中包含的任何内容都是HTML元素，这些元素的根是html。
>
> 浏览器在遇到html根元素时将它理解为HTML文档。

#### HTML4.01 & HTML5

html4.01需要声明xmlns属性，用于对HTML文档进行验证。

```html
<html xmlns="http://www.w3.org/1999/xhtml" lang="zh-cn"></html>
```

html5中该属性可以省略，以下为定义html5的声明(不区分大小写)。

```html
<!DOCTYPE html> 
<!DOCTYPE HTML> 
<!doctype html> 
<!Doctype Html>
```

#### lang属性

> 使用**lang**属性可以定义HTML文档使用的语言，默认值是en
>
> ```html
> <html lang="en"></html>
> ```



### HTML头部元素

```html
<head>
  <base>
  <link>
  <meta>
  <title></title>
  <style></style>
</head>

<body>
  <script></script>
</body>
```



#### base元素

> 在HTML5中建议把base作为head的第一个字元素，这样head中的其他元素就可以使用base的信息了。
>
> ```html
> <head>
>   <base href="http://www.oa.cn/" target="_blank" /> <!-- 网址 -->
>   <base href="../html/"> <!-- 本地文件 -->
> </head>
> <body>
>   <a href="index.html"> 首页 </a>
> </body>
> ```
>
> 在这里将默认的URL设置为www.oa.cn，因此首页的真实链接URL是www.oa.cn/index.html
>
> 将默认的本地文件地址设置为../html，因此真实的本地文件地址为../html/index.html

#### link元素

> link元素常用语链接外部样式表。
>
> ```html
> <link rel="stylesheet" type="text/css" href="menu.css" /> <!-- 样式表 -->
> <link rel="icon" href="demo_icon.gif" type="image/gif" sizes="16x16" /> <!-- 图标 -->
> ```
>
> HTML5中的link元素不再支持charset、rev和target属性。
>
> 新增sezes属性，仅适用于rel属性为icon的情况，用于定义图标的尺寸。

#### meta元素

```html
<!-- charset 指定字符编码 -->
<meta charset="UTF-8" .\/>

<!-- name指定为keywords，定义针对搜索引擎的关键词 -->
<meta name="keywords" content="HTML,CSS,XML,XHTML,JavaScript" />

<!-- name指定为description，定义对页面的描述 -->
<meta name="description" content="测试内容。" />

<!-- name指定为revised，定义页面的最新版本 -->
<meta name="revised" content="David,2018/8/8/" />

<!-- http-equiv指定为refresh，指定每5秒刷新一次页面 -->
<meta http-equiv="refresh" content="5" />

<!-- http-equiv指定为X-UA-Compatible，指定兼容模式 -->
<meta http-equiv="X-UA-Compatible" content="id=edge" />
```

关于兼容模式X-UA-Compatible，参考[标签中http-equiv属性的属性值X-UA-Compatible详解](https://blog.csdn.net/changjiangbuxi/article/details/26054755)

#### script元素

>script元素通常用于**定义一段JavaScript脚本**，或者**链接外部的脚本文件**。

```html
<script type="text/javascript" async="async"> <!-- async定义当脚本可用时是否立即异步执行 -->
	document.write("Hello HTML5");
</script>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> <!-- 官方CDN -->
<script src="../js/admin-win.js"></script> <!-- 引入本地js文件 -->
```

#### style元素

> style元素用于定义页面所用到的CSS样式代码。
>
> ```html
> <style type="text/css"> <!-- type可以省略 -->
>   h1{color:red}
>   p{color:black}
>   button{color:green}
> </style>
> ```
>
> 在HTML5中，为style元素增加了scoped属性，该属性可以为文档的指定部分定义样式，而不是整个文档。使用scoped属性后所规定的样式只能应用于style元素的父元素及其子元素。

###### 尚存问题

指定部分定义样式是什么意思？私有模块 ？参考[vue中慎用style的scoped属性](https://blog.csdn.net/qq_39043923/article/details/88687046)

此处的style元素的父元素及其子元素的定义是什么意思？

#### title元素

> title元素定义的标题将显示在浏览器的标题栏、收藏夹以及搜索引擎的结果中。
>
> 一个文档中钙元素只能出现一次。
>
> ```html
> <head>
>   <title> 关于html学习 </title>
> </head>
> ```



### 结构元素

> 在HTML5以前，如果定义一个文档块结构只能通过div元素来实现，通过为不同的div元素设置不同的id来表示不同的含义。由于整个代码全部是div元素，导致缺乏明确的语义元素。
>
> HTML5增加了一些与文档结构关联的结构元素，如页眉、页脚和内容区块等。

#### header元素

> header元素通常用来放置整个页面或页面内的一个内容区块的标题，也可以包含网站logo图片、数据表格和搜索表单等内容。

```html
<header></header>

<div id="header"></div> <!-- 等价 -->
```

#### article元素

> article元素代表文档、页面或者应用程序中独立的、完整的、可以独自被外部引用的内容。它可以是一篇博客或者报纸、刊物中的文章、一篇论坛帖子、一段用户评论、独立的插件，或者其他任何独立的内容。
>
> article元素可以单独使用，也可以和其他元素结合使用。
>
> article元素通常可以有自己的标题，标题一般放在header元素中；有时还可以有脚注，脚注一般放在footer元素中。
>
> article元素是一个容器，也可以和其他元素结合使用。

###### 尚不理解

#### section元素

> section元素用于对网站或应用程序中页面的内容**进行分块**。
>
> section元素通常由内容和标题组成。
>
> 但是section元素并非一个普通的容器元素，当一个容器需要被直接定义样式或通过脚本定义行为时，推荐使用div元素，而不是section元素。
>
> 在使用section元素时，需要注意以下三点。
>
> 1. 不要将section元素用作设置样式的页面容器，那是div元素的工作。
> 2. 如果article元素、aside元素或nav元素更符合使用条件，那么不要使用section元素。
> 3. 不要为没有标题的内容区块使用section元素。

> 在HTML5中，article元素可以看作是一种特殊的section元素，但它比section元素更强调独立性，即section元素强调分段或分块，而article强调独立性。具体来说，如果一块内容相对来说比较独立、完整，应该使用article元素；但是如果想要将一块内容分成多段，应该使用section元素。

参考[HTML5中div section article的区别](https://www.qianduan.net/html5-differences-in-the-div-section-article/)

> div section article ，语义是从无到有，逐渐增强的。div 无任何语义，仅仅用作样式化或者脚本化的钩子(hook)，对于一段主题性的内容，则就适用 section，而假如这段内容可以脱离上下文，作为完整的独立存在的一段内容，则就适用 article。

参考[HTML5之section与article与div](https://blog.csdn.net/u010028980/article/details/8737377)

> 当一个区域没有语义时果断用div标签！
>
> 有语义就要分情况了：
>
> 1. 一个博文用article，然后用section将不同的段落分隔开。
> 2. 博文下面的评论用section，然后用article将每个评论分开。
> 3. 这个区域是提供阅读的文章果断用article。
> 4. 如果这个区域不是单独的，而是跟上下文有联系，那么果断用section。
>
> <img src="./images/html基础~1.png" alt="布局" align="left" />

###### 尚待深入理解

#### aside元素

> aside元素用来表示当前页面或者文章的**附属信息**。
>
> aside元素有以下两种用法：
>
> 1. 被包含在article元素中，作为主要内容的附属信息。
> 2. 在article元素之外使用，作为页面或站点全局的附属信息。

###### 尚有问题

为何aside在html文件中使用之后还是从上到下的排序，而不是在右侧栏显示？

代码VUE/html/html-learn/article.html，aside并不是显示在右侧，为何？

有回答说要配合css才行，留下疑问。

#### footer元素

> 作为其上层父级内容区块或者一个根区块的**脚注**。通常包含相关区块的脚注信息，例如作者、相关阅读链接及版权信息等。



### 节点元素

#### nav元素

>nav元素是一个可以**用作页面导航的容器**，其中的导航元素用于链接其他页面或当前页面的其他部分。并不是所有的链接都要放进nav元素中，只需要将主要的、基本的链接放进nav元素中即可。

参考本文档的Section元素中的图，nav显示在左侧。在实现过程中，也可以放在顶栏以横向排列方式展示。需要配合CSS文件对其进行布局。

#### hgroup元素

#### address元素

> address元素用来表示离它最近的article或body元素内容的联系信息，例如文章作者的名字、网站设计和维护者的信息。
>
> 当address的父元素是body时，也可表示该文档的版权信息。
>
> ```html
> <footer>
>   <address>当使用本站时，代表您已经接受了本站的使用条款和隐私条款。版权所有，保留一切权利。</address>
>   <p>赞助商：xx科技有限公司</p>
> </footer>
> ```

这里的address和引用元素cite的效果一样，都是使得字体为斜体。

```html
<address>这是一个斜体字段</address>
<cite>这是一个斜体字段</cite>
```





