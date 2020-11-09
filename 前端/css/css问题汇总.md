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

---

