---
title: Vue
---

### 准备工作

#### 介绍

> Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建**用户界面（User Interface）**的渐进式框架。Vue 的核心库只关注**视图层**，与现代化的工具链（Webpack）以及各种支持类库（Babel、TypeScript）结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

<img src="E:/%E7%8E%89/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88/Vue/Vue%E5%9F%BA%E7%A1%80/01day/1-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/web.jpg" alt="web" style="zoom:75%;" />

​	所谓用户界面对于Web开发者来说就是一个网页，也称为视图层。

​	**学习 Vue 其实是以一种全新的方式编写网页。**

#### 安装

> Vue 其实就是一个封装了大量逻辑的 Javascript 文 件。

有多种方式可以获取 vue:

1. [下载](https://cn.vuejs.org/js/vue.js)
2. CDN https://cdn.jsdelivr.net/npm/vue/dist/vue.js
3. npm 仓库

无论何种方式获取 vue ，只需要通过 script 标签将其导入即可。

#### 模型

​		一个**网页的核心是数据**，html 和 css 只是负责将这些数据以较为美观的形式展示，**Vue 可以对页面所承载的数据进行管理，我们称之为 Model，即模型。**

#### 视图

​		通过上述示例，我们知道了通过 vue 提供的属性，如 `v-if` ，可以丰富页面的逻辑控制，**但是它只能在一定的“范围”才可以生效，我们称这部分为View，即视图层 。** 

​		**注：将 el 指定的区域称为视图并不严禁，准确一点儿应该叫模板，不过初学者不必细究。**

```
    new Vue({
      // 指定 Vue 的管辖范围
      // 可以是一个 css 选择器，建议使用 ID 选择器
      // 也可以是一个 DOM 节点
      // el: document.querySelectorAll('div')[1]
      el: '#app'
    })
```

## 

- #### {{msg}}和v-text='msg'意思一样都是引入Vue中的msg文本**

  #### **设置隐藏与显示（v-if）v-show='seen'，不写的话默认false隐藏，**

```html
<div id="p">
    //{{msg}}和v-text='msg'意思一样都是引入Vue中的msg文本
    //设置隐藏与显示v-show='seen'，不写的话默认false隐藏，
    <p v-show='seen'>{{msg}}</p>
    <p>{{msg}}</p>
    <p v-text='msg'></p>
  </div>
  //引入Vue文件
<script src="./libs/vue.min.js"></script>
<script>
  new Vue({
    //如果只写p，则只对第一个p标签生效
    el: '#p',
    data: {
      //   seen: true,
      seen: false,
      msg: '你还好吗'
    }
  })
</script>
```

​             实例化 Vue 时，通过 `data` 可以为 `el` 所对应的 DOM 初始数据，其中数据类型可以为任意合法的 Javascript 数据类型。

​		`{{}}` 是 Vue 中特殊的语法符号，用于将 `data` 中的数据插入到视图层元素的内容区域（innerHTML）。

## 属性绑定

`v-on:事件名="回调函数"` 是为添加事件监听的语法格式

*v-on:事件名='回调函数'    ==== @事件名='回调函数'*

```html
<body>
  <div id="box">
    <!-- 
          v-on:事件名='回调函数'    ==== @事件名='回调函数'
        -->
    <input @blur="blur"></input>
    <a href="javascript:;" v-on:click='clicked'>{{msg}}</a>
    <a href="javascript:;" @click='clicked'>{{msg}}</a>
  </div>
</body>
<script src="./libs/vue.min.js"></script>
<script>
  new Vue({
    el: "#box",
    data: {
      msg: '生活'
    },
    methods: {
      clicked: function() {
        console.log('哈哈');
      },
      blur: function() {
        console.log('很好');
      }
    }
  })
</script>
```

#### 视图

​		通过上述示例，我们知道了通过 vue 提供的属性，如 `v-if` ，可以丰富页面的逻辑控制，**但是它只能在一定的“范围”才可以生效，我们称这部分为View，即视图层 。** 

​		**注：将 el 指定的区域称为视图并不严禁，准确一点儿应该叫模板，不过初学者不必细究。**

```html
    new Vue({
      // 指定 Vue 的管辖范围
      // 可以是一个 css 选择器，建议使用 ID 选择器
      // 也可以是一个 DOM 节点
      // el: document.querySelectorAll('div')[1]
      el: '#app'
    })
```

#### 模型

​		一个**网页的核心是数据**，html 和 css 只是负责将这些数据以较为美观的形式展示，**Vue 可以对页面所承载的数据进行管理，我们称之为 Model，即模型。**

`v-on:事件="回调函数($event)"`  $event 做为参数传递时具有特殊含义，用它获得事件对象

```html
<div id="box">
    <!-- 
          v-on:事件名='回调函数'    ==== @事件名='回调函数'
          $event 传的是一个事件对象
        -->
    <input @blur="blur"></input>
    <a href="javascript:;" v-on:click='clicked(a,$event)'>{{msg}}</a>
  </div>
  <script src="./libs/vue.min.js"></script>
<script>
  new Vue({
    el: "#box",
    data: {
      msg: '生活',
      a: 10
    },
    methods: {
      // arg普通参数,ev接收事件对象
      clicked: function(arg, ev) {
        console.log(arg);
        console.log(ev);
        // 可以执行原生dom属性
        ev.target.style.color = 'red';
      },
      blur: function() {
        console.log('很好');
      }
    }
  })
</script>
```



#### 数据绑定

​		数据绑定是 vue 中非常高级的特性，它是指将**视图层DOM元素与模型层中的数据建立一一对应的联系**，将这种联系称为数据绑定。

​		DOM 元素一般包含**属性节点**和**文本节点**，所以 vue 中实现数据绑定主要体验在两个方面：

- 属性节点绑定
  1. `v-bind:属性名` 是实现属性节点绑定的语法格式。v-bind:属性名` 可以被简写为 `:属性名`
  2. 支持 Javascript 表达式
  3.  在 vue 中对属性进行数据绑定时，使用 v-bind:属性名="值"
  4. class` 和 `style` 是DOM元素中比较重要的两个属性。

```html
<div id="app">
  <!-- 在 vue 中对属性进行数据绑定时，使用 v-bind:属性名="值" -->
  <p v-bind:title="title" v-text="title">一段文本</p>

  <!--v-bind:style 语法相对特殊一些，接受一个对象类型数据 -->
  <!-- 这个对象的内容都是 css 的代码，{color: 'red', width: '100px'} -->
  <p v-bind:style="{color: red}">我是一段带颜色的文本</p>

  <p v-bind:style="styleObject">我是一段带颜色的文本</p>

  <!-- v-bind:class 语法相对特殊一些，接受一个对象类型数据 -->
  <!-- 对象的属性为真实存在的 类名 -->
  <!--
		对象的值为布尔类型，
		如果为 true 则添加属性对应的类名，
		如果为 false 则不添加
	-->
  <p v-bind:class="{demo: true, test: false}">一段文本</p>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      title: 'Vue 的属性绑定',
      styleObject: {
        color: 'red',
        backgroundColor: 'blue'
      }
    }
  })
</script>
```

#### 响应式数据绑定

关于响应式可以理解成一种**自动机制**，即一方发生改变后，另一方也相应做出改变。具体在 vue 中，是指当模型 (data) 中的数据被改变后，所对应的视图区域也会相应改变，而这一切又都是自动完成的。

- 双向数据绑定

  数据绑定有单向和双向之分，具体是指数据的流向。

  1. 单向，模型 ------> 视图
  2. 双向，模型 <------> 视图

  表单元素在 html 中具体特殊意义，它的主要作用并不是展示数据，更多的是收集用户填写的数据，因此表单元素也就成为了数据的提供方了，通过修改表单中的内容，实现模型中 data 数据的变化。

  为表单元素添加 `v-model` 可以实现数据的双向绑定。

```html
<div id="app">
  <!-- v-model 是实现数据双向绑定的关键 -->
  <input type="text" v-model="msg" />
  <!-- 用户在表单中输入内容时，下面 h3 的内容会同步更新 -->
  <h3>{{msg}}</h3>
</div>

<script>
	// 实例化
  new Vue({
    el: '#app',
    data: {
      msg: '初始数据'
    }
  })
</script>
```

#### 结构

​		动态网站的页面结构是根据数据展示的需要动态创建的，**vue 具备动态创建页面结构的能力。**

- 条件控制
  1. `v-if`,`v-else`,`v-else-if`

```html
<div id="box">
    <p v-if="seen" @click="click">显示变为隐藏</p>
    <span>我叫{{name}},今年{{age}}岁了，我是</span>
    <span v-if="age >= 18">成年</span>
    <span v-else="age">未成年</span>人，
    <span>我考了{{score}}分，考试评价：</span>
    <span v-if="score >= 90">优秀</span>
    <span v-else-if="score >=70">良好</span>
    <span v-else-if="score >=60">合格</span>
    <span v-else="score <=60">未合格</span>
  </div>
  <script src="./libs/vue.min.js"></script>
  <script>
    new Vue({
      el: "#box",
      data: {
        seen: true,
        name: "小明",
        age: "19",
        score: "61"
      },
      methods: {
        click: function() {
          this.seen = false;
        }
      }
    })
  </script>
```

#### `v-show`

````html
<div id="app">
  <!-- 根据 seen 取值，显示/隐藏 p 元素 -->
  <p v-if="seen" @click="toggle">你能见我吗？</p>
</div>

<script>
	var vm = new Vue({
    el: '#app',
    data: {
      seen: true
    },
    methods: {
      toggle: function () {
        // 修改seen的值
        this.seen = !this.seen;
      }
    }
  })
</script>
````

`v-if` 和 `v-show` 在视觉效果上是一致的，然而其实现是有差异的，`v-if` 是通过添加/移除 DOM 节点实现，`v-show` 是通过 css 的 display 属性值（block/none）实现。

`v-if` 会导致 DOM 树中，节点数量变化，开销方面会更大一些，`v-show` 并不影响DOM中节点数量变化，开销相对低一些。

对于操作较为频繁的显示/隐藏操作，建议使用 `v-show`，相反建议使用 `v-if`

另外 `v-if` 是惰性的，如果其值为假，则内部所有元素都不会被渲染。

#### 列表控制

1. `v-for` 实现数组/对象类型数据的遍历
2. `v-for="(item, index) in list"`item(值，单元值)，index（下标，索引值）list（键）
3. `v-for="(item, index) in user"`item(为对象的 属性值)，index（为 对象的 属性）list（对象）

```html
<div id="app">
    <ul>
      <li v-for="(item, index) in list">{{index + 1}}-{{item}}</li>
    </ul>

    <p>
      <span v-for="(item, index) in user">{{index}}:{{item}} </span>
    </p>
  </div>

  <script src="./libs/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        list: ['html', 'css', 'vue'],
        user: {
          name: '小明',
          age: 18
        }
      },
    });
  </script>
```

`key` 管理可复用的元素

Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。

当 Vue 正在更新使用 v-for 渲染的元素列表时，它**默认使用“就地更新”的策略**。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。

​		这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

​		**建议尽可能在使用 v-for 时提供 key 属性**，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。