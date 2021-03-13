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