[TOC]

[Property(CSS)](https://developer.mozilla.org/en-US/docs/Glossary/property/CSS)

[CSS简单的继承](https://juejin.im/post/6844903997459922958)

[VSCode的一些小操作(二)——快速生成HTML,CSS代码](https://blog.csdn.net/ycx60rzvvbj/article/details/105775469)

[一文搞懂CSS中的字体单位大小(px,em,rem...)](https://juejin.im/post/6844903897421578253)

[常用css样式属性大全](https://www.cnblogs.com/zhaoyingblog/p/8342739.html)

### CSS盒模型

![CSS box-model](/Users/samstephen/Documents/Typora/前端/css/images/box-model.png)

​		不同部分的说明：

> - **Margin(外边距)** - 清除边框外的区域，外边距是透明的。
> - **Border(边框)** - 围绕在内边距和内容外的边框。
> - **Padding(内边距)** - 清除内容周围的区域，内边距是透明的。
> - **Content(内容)** - 盒子的内容，显示文本和图像。

###### W3C标准盒模型

> width=内容的宽度
>
> height=内容的高度
>
> ```js
> box-sizing: content-box;
> ```

###### IE盒模型

> width = border + padding + 内容的宽度
>
> height = border + padding + 内容的高度
>
> ```js
> box-sizing: border-box;
> ```

###### 从父元素继承box-sizing的值

> ```js
> box-sizing: inherit;
> ```

[CSS简单的继承](https://juejin.im/post/6844903997459922958)

---

### 选择器

###### 类选择器 ```.``` & id选择器```#```

> 与vue的挂载el表示的完全不同，```el: #app```表示挂载到```id="app"```，```el: .app```表示挂载到```class="app"```。

```vue
<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

```vue
<style scoped>
li {
	
}
</style>
```



###### 一次使用多个选择器

```css
p, li {
  color: red;
}
```



### css常用属性

[常用css样式属性大全](https://www.cnblogs.com/zhaoyingblog/p/8342739.html)