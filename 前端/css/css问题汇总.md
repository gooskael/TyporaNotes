[TOC]

### 1. CSS字体 px rpx em rem vw vh vmin vmax

[一文搞懂CSS中的字体单位大小(px,em,rem...)](https://juejin.im/post/6844903897421578253)

---

### 2. ```a:link```不起作用？

```css
a:link {color:#FF0000;}		/* 未被访问的链接 */
a:visited {color:#00FF00;}	/* 已被访问的链接 */
a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}	/* 正在被点击的链接 */
```

​		css中对链接的属性定义主要有上面四个属性。```a:link```表示的是未被访问的链接，注意的是：历史中如果访问了但是没有清楚缓存历史记录的话，这个链接就算是已经被访问过的链接了；而不是每一次重新打开这个页面的时候都会重新刷新状态，这就是```a:link```不起作用的原因。

****

### 3. `:focus` & `:hover`

```css
input:focus {
	outline: none; //点击了之后的边框没有了
  border: 1px dotted black; //自定义
}
```

****

### 4. 修改`input`中的`button`样式

[修改input file的样式（或用按钮button替代file）](https://blog.csdn.net/u014800380/article/details/53105767)：设置`opacity: 0;`拿自定义button覆盖

> ```
> file的透明度设为0的话，按钮和框好像是一起没了，再添一个框？这种方式我知道的。请问你是否知道EXT，我直接在JS里面能否用EXT
> ```

=> 在input外层套一个`a`标签，设置`input`的`position: absolute;`, `opacity: 0`：但没有文件显示列表。

****

