### 0.前言

#### 浏览器兼容

​	以下几个网站提供了浏览器兼容的现状查询：

1. [Can I Use...?](http://caniuse.com)
2. [WebPlatform.org](http://webplatform.org)
3. [Mozilla Developer Network](http://developer.mozilla.org)
4. [维基百科上的“浏览器排版引擎对比(CSS 兼容性)”词条](http:// en.wikipedia.org/wiki/Comparison_of_layout_engines_(Cascading_ Style_Sheets))

#### 支持早期浏览器

​	早期一些浏览器可能除了标准语法之外，还需要一些其余代码提供支持；比如要得到一条**从黄色到红色的垂直渐变色**，本书只会列出标准语法:

```css
/* 标准语法 */
.c {
  background: liner-gradient(90deg, yellow, red);
}

.c_compatible {
  background: -moz-linear-gradient(0deg, yellow, red); 
  background: -o-linear-gradient(0deg, yellow, red); 
  background: -webkit-linear-gradient(0deg, yellow, red); 
  background: linear-gradient(90deg, yellow, red);
}
```

