[TOC]

## Antdv.com

[ant design](antdv.com)

- [x] 学会官方组件库，组件实现的具体方式的查看

> [ant design/Customize Theme](https://antdv.com/docs/vue/customize-theme/)
>
> [default variables](https://github.com/vueComponent/ant-design-vue/blob/master/components/style/themes/default.less)
>
> [ant design/components](https://github.com/vueComponent/ant-design-vue/tree/master/components)

### 如何引入ant design组件？

[vue中使用ant design](https://www.cnblogs.com/psxiao/p/11417697.html)

​	1.打开项目terminal，下载ant design

```shell
$ npm i --save ant-design-vue
```

> 在执行了这个命令之后，package.json中会添加相关的依赖"dependencies"
>
> 这样如果上传到git之后，git pull完，通过```npm install```就可以下载相关的依赖，包括刚引入的ant-design-vue。
>
> 下面无论**全局引入**还是**局部引入**，都需要先下载。

​	2.1选择全局引入

```js
// 在src/main.js添加
import Antd from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css'

Vue.use(Antd)
```

> 全局引入完成后，其他的页面使用的时候就不用进行其他别的操作，直接使用即可。
>
> 全局引入的问题是引入了很多你可能不会用上的一些组件，使得整个项目很臃肿。

​	2.2选择部分引入

```js
// 在src/main.js添加
import Table from 'ant-design-vue'
//import {Table, Button} from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css'

Vue.use(Table);
//Vue.use(Button);
```

​	2.3按需引入

> 按需引入是在每个页面各自import，而不是在main.js里面管理import。有点麻烦，没必要。

---

### a-tooltip

###### ```title```

​		弹出的提示信息。在```a-tooltip```内部嵌入不同的元素，当鼠标移到该元素的时候会出现提示信息。

```vue
<template>
  <a-tooltip title="tips text">
    <p>Tooltip will show when mouse enter.</p>
  </a-tooltip>
</template>
```

###### ```placement```

​		可以设定气泡框的位置，同时也可以设定气泡的箭头相对于气泡的位置。

​		气泡框相对于元素出现的位置：```top```/```bottom```/```left```/```right```

​		气泡框的小箭头相对于气泡的位置：```topLeft/topRight``` / ```bottomLeft/bottomRight``` / ```leftTop/leftBottom``` / ```rightTop/rightBottom```

```vue
<template>
  <a-tooltip title="tips text" placement="topLeft">
    <p>Tooltip will show when mouse enter.</p>
  </a-tooltip>
</template>
```

###### ```arrowPointAtCenter```

​		气泡框出现的位置置中。

```vue
<template>
  <a-tooltip title="tips text" placement="topLeft" arrow-point-at-center>
    <p>Tooltip will show when mouse enter.</p>
  </a-tooltip>
</template>
```

###### ```autoAdjustOverflow```

​		气泡被遮挡时自动调整位置。```:auto-adjust-overflow="true"```是默认的。

```vue
<template>
  <a-tooltip title="tips text" placement="topLeft" :get-popup-container="getPopupContainer">
    <p>Tooltip will show when mouse enter.</p>
  </a-tooltip>
</template>
<script>
export default {
  data() {
    return {
    };
  },
  methods: {
    getPopupContainer(trigger) {
      return trigger.parentElement;
    },
  },
};
</script>
```

----------------

### a-icon

​		图标。

###### ```type```

​		图标类型。遵循图标的命名规范。

```vue
<a-icon type="search" />
```

###### ```theme```

​		图标主题风格。可以选择实心、描线、双色。适用于官方图标。

​		```filled```：实心

​		```outlined```：描线，默认属性

​		```twoTone```：双色。仅适用于官方的双色图标。

```vue
<a-icon type="smile" theme="twoTone">
```

​		对于```twoTone```，可以通过使用```Icon.getTwoToneColor()```和```Icon.setTwoToneColor()```来全局设置图标的主色。

```js
import { Icon } from 'ant-design-vue'

Icon.setTwoToneColor('#eb2f96');
Icon.getTwoToneColor(); // #eb2f96
```

###### ```spin```

​		图标旋转

```vue
<a-icon type="smile" theme="twoTone" spin>
```

-------------------

### a-input

###### ```placeholder```

​		不输入任何字符的时候，文本框默认显示的内容。

```vue
<template>
  <a-input placeholder="Basic usage" />
</template>
```

###### ```prefix``` & ```suffix```

​		在文本框内的头尾加入一些元素。

```vue
<!-- 加入一些简单的字符元素 -->
<a-input prefix="￥" suffix="RMB" />

<!-- 
	加入图片、图标；可以选用a-icon和a-tooltip，
	在子元素中定义 slot=""来设定位置
-->
<a-input ref="userNameInput" v-model="userName" placeholder="Basic usage">
	<a-icon slot="prefix" type="user" />
	<a-tooltip slot="suffix" title="Extra information">
		<a-icon type="info-circle" style="color: rgba(0,0,0,.45)" />
	</a-tooltip>
</a-input>
```

###### ```allow-clear```

​		允许快捷删除框内的内容。

```vue
<a-input placeholder="search" v-model="data" allow-clear></a-input>
```

#### a-input-search

​		?

----------------

### a-pagination

###### ```size```

​		分页栏提供两种样式，一种是带边框的（default），一种是不带边框的```size="small"```。

```vue
<a-pagination
	size="small"
	v-model="current"
	:total="total"
  >
</a-pagination>
```

###### ```total``` & ```show-total```

​		```total```绑定总共要展示的条目，页面大小默认值是10条目/页。```show-total```可以展示出总共有多少页（实际上可以根据分页的情况也可以看到总共多少页）。```:show-total="total => `共 ${pages} 页`" ```。这里的```pages```可以是后台直接返回一个相应的页码数，也可以根据回调函数返回的参数pageSize & 和总条目书total进行计算得到。

```vue
<a-pagination
	size="small"
	v-model="current"
	:total="total"
	:show-toal="total => `共 ${pages} 页"
	>
</a-pagination>
```

###### ```showSizeChanger```

​		决定页面大小是否可以进行改变，会有相应改变框。改变框中的选项也可以自定义。

```vue
<a-pagination
	size="small"
	v-model="current"
	:total="total"
	:show-toal="total => `共 ${pages} 页"
	show-size-changer
	>
</a-pagination>
```

###### ```showQuickJumper```

​		决定是否能够输入页码快速跳转过去，会有相应改变框。

```vue
<a-pagination
	size="small"
	v-model="current"
	:total="total"
	:show-toal="total => `共 ${pages} 页"
	show-size-changer
	show-quick-jumper
	>
</a-pagination>
```

###### ```simple```

​		一种十分简洁的跳转页码。

```vue
<a-pagination
	simple
	v-model="current"
	:total="total"
	>
</a-pagination>
```

###### 回调函数

​		```change```页码改变响应函数。

​		```showSizeChange```页面大小改变响应函数。

```vue
<a-pagination 
	size="small"
	:total="total" 
	:show-total="total => `共 ${pages} 页`" 
	:default-current=1
	@change="handleChange"
	@showSizeChange="handleChange"
	show-size-changer 
	show-quick-jumper >
</a-pagination>
```





### a-table

###### ```columns``` & ```dataSource```

​		定义表格的标题内容，以及该标题下（这一列）的各个表格元素的数据绑定。

```vue
<template>
	<a-table :columns="columns" :data-source="data">
    <a slot="name" slot-scope="text">{{ text }}</a>
  </a-table>
</template>
```



### a-layout



