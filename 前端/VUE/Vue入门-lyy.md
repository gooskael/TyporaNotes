### Vue入门

[TOC]



#### 引入Vue

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

```html
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

> 使用vue-cli脚手架构建vue项目
>
> https://cli.vuejs.org/zh/



#### 声明式渲染

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地<u>将数据渲染进 DOM</u> 的系统：

```html
<div id="app">
  {{ message }}
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

除了文本插值，我们还可以绑定元素属性：

```html
<div id="app">
  <span v-bind:title="message">
  	将鼠标放放在上面悬停几秒
  </span>
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: '页面加载于' + new Date().toLocaleString()
  }
})
```

`v-bind` attribute 被称为**指令**。指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊 attribute。

在这里，该指令的意思是：“将这个元素节点的 `title` attribute 和 Vue 实例的 `message` property 保持一致”



#### 命令式与声明式

> **命令式**：一步一步告诉程序如何去做，能否达成结果取决于开发者的设计。（用jQuery操作DOM）
> **声明式**：只告诉程序想要什么结果，如何达成由程序保证，开发者不用关心。

> 需求：展示今天的日期，如果是周日就用粉色的字，否则用蓝色。

命令式渲染，使用jQuery：

```html
<div class="box"></div>
```

```js
// JS
let today = new Date();
let color = today.getDay() === 0 ? 'pink' : 'lightBlue';
let box = $('.box');
box.text(today.toLocaleDateString()); 
box.css('color', color);
```

声明式渲染实现的是，DOM 随状态（数据）更新而更新。用 Vue 实现上述功能，代码如下：

```html
<div id="root">
  <div :style="boxStyle">{{today}}</div>
</div>
```

```js
// JS
new Vue({
  el: '#root',
  data: {
    today: '',
    boxStyle: {
      color: ''
    }
  },
  mounted() {
    let now = new Date();
    this.today = now.toLocaleDateString();
    this.boxStyle.color = now.getDay() === 0 ? 'pink' : 'lightBlue';
  }
});
```



我们更新了应用的状态，但没有触碰 DOM——所有的 DOM 操作都由 Vue 来处理，你编写的代码只需要关注逻辑层面即可。

#### 组件化构建应用

```html
<div id="app">
  <ol>
    <todo-item></todo-item>
    <todo-item></todo-item>
  </ol>
</div>
```

```js
Vue.component('todo-item', {
  template: '<li>这是待办项</li>'
});
var app = new Vue({
  el: '#app',
})
```

##### 给组件传值

```js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{todo}}</li>'
})
var app = new Vue({
  el: '#app',
  data: {
    todoList: ['学习js', '学习Vue', '整个项目']
  }
})
```

```html
<div id="app">
  <ol>
    <todo-item v-for="item in todoList" v-bind:todo="item"></todo-item>
  </ol>
</div>
```

##### 验证prop

```js
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```

##### 父子组件通信

```html
<div id="app">
	<child-component v-on:say="handleSend"></child-component>
</div>
```

```js
Vue.component('child-component', {
  template: `
    <div>
    <button v-on:click="send">向父组件通信</button>    
    </div>
  `,
  methods: {
    send() {
      this.$emit('say', 'Hello parent');
    }
  }
})
var vm = new Vue({
  el: '#app',
  methods: {
    handleSend(value) {
      console.log(value);
    }
  }
})
```



#### Vue生命周期

参考资料：

https://juejin.im/entry/6844903602356502542

https://blog.csdn.net/xdnloveme/article/details/78035065

<img src="./images/lifecycle.png" alt="Vue 实例生命周期" style="zoom: 33%;" />

**created**:在模板渲染成html前调用，即通常初始化某些属性值，然后再渲染成视图。

**mounted**:在模板渲染成html后调用，通常是初始化页面完成后，再对html的dom节点进行一些需要的操作。

