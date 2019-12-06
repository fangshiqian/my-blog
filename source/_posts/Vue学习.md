---
title: 1.Vue基础
date: 2019-12-04 13:47:57
top: 
categories:
   - 学习
   - Vue
tags: Vue
---
## 基础

### 1. 安装

#### (1) 兼容性 : (注意!!)

Vue 不支持IE8 及以下版本,因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有[兼容 ECMAScript 5 的浏览器](https://caniuse.com/#feat=es5)。

#### (2) Vue Devtools : (浏览器插件)

审查和调试Vue 的一个插件  安装插件需要进入Chrome商店进行下载 点击此处[谷歌插件(可以访问谷歌商店)]([https://fangshiqian.github.io/my-blog/2018/11/30/%E8%B0%B7%E6%AD%8C%E6%8F%92%E4%BB%B6/](https://fangshiqian.github.io/my-blog/2018/11/30/谷歌插件/))进行下载该插件

### 2. 介绍

#### (1) Vue.js 是什么?

> ​	Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。(这段话引自于官网[Vue.js 是什么](https://cn.vuejs.org/v2/guide/index.html#Vue-js-是什么))

简单理解:

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E7%AE%80%E5%8D%95%E7%90%86%E8%A7%A3Vue)

#### (2) 安装

* 直接下载
  * 开发版本：https://cn.vuejs.org/js/vue.js
  * 生产版本：https://cn.vuejs.org/js/vue.min.js
* CDN
  * `<script src="https://cdn.jsdelivr.net/npm/vue"></script>` 最新稳定版
  * `<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>` 指定版本
* 使用 `npm` 下载
  * `npm install vue` 最新稳定版
  * `npm install vue@版本号` 指定版本

#### (3) 使用举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <h1>{{masges}}</h1>
        <p>姓名：{{user.name}}</p>
        <p>年龄：{{user.age}}</p>
        <p>性别：{{user.gender === 0 ? '男':'女'}}</p>
        <ul>
            <li v-for='itme in biaoqian'>{{itme}}</li>
        </ul>
    </div>
    <!-- 1. 安装vue.js
        2. 创建vue 
        3. 根据视图抽象 data 里面的数据
        4. 使用 vue 语法把数据绑定到视图中 -->
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    <script>
        const app = new Vue({
            // 告诉 vue管理视图的入口
            el:'#app',
            // 可以理解为data中的数据渲染到视图里面
            data: {
                masges:'hello vue.js',
                user:{
                    name: '里斯',
                    age: 19,
                    gender: 0
                },
                biaoqian:['吃饭','睡觉','打豆豆S']
            },
            methods: {
            }
        })
    </script>
</body>
</html>
```

### 3. Vue 实例 (多看)

> ​	每个Vue应用都是通过用Vue函数创建一个新的Vue 实例开始的

```js
var app = new Vue({
	// 选项
})
```

当创建一个Vue实例时,你可以传入一个**选项对象**下面的就是使用这个选项创建想要的**行为**

例如:

* el
* data(这里的数据会放到视图里面)
* methods(方法)
* watch()
* computed()
* . . . 

#### (1) 实例选项 - el

* 不能是html、body节点
* el只能作用到单一节点上

#### (2) 实例选项 - data

官方一点说: data不是普通数据,这种数据我们称之为**响应式**数据,用来驱动视图更新的数据

自己理解: data里面的数据就是渲染到视图(html)上的数据

注意:

* 模板中访问的数据,必须初始化到data中
* 模板无法访问Vue实例之外的数据

```js
const a = 1
    const app = new Vue({
      /**
       * 告诉 Vue 管理视图的入口
       */
      el: '#app',
      /**
       * 这个 data 就好比之前使用 art-template 模板引擎的数据一样的
       * 我们可以直接在被 Vue 管理的视图中使用 data 中的数据绑定
       */
      data: {
        message: 'Hello Vue.js!',
        user: {
          name: '张三',
          age: 18,
          gender: 0 // 0 男，1 女
        },
        todos: ['吃饭', '睡觉', '打豆豆'],
        count: '',
        num: 0, // 数字
        str: '', // 字符串
        isSeen: false, // 布尔值
        arr: [], // 空数组
        /**
         * 对于对象的修改
         * 1. 没有初始化的对象成员如果修改不会更新视图
         * 2. 也有方式可以动态添加未初始化的数据成员并且能更新视图（后面说）
         * 3. 直接对对象进行重新赋值可以实现视图更新
         *   xxx = 新的数据对象，例如 app.obj = { a: 123 }
         * 建议：最好把所有需要的数据都初始化到 data 中来
         */
        obj: {
          // a: 0
        } // 对象，没有初始化的对象成员如果修改不会更新视图
      }
    })
```



### 4. 模板语法(多看)

> ​	官方: Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析。

#### (1) 插值

a: 文本

 数据绑定最常见的形式就是使用"Mustache"语法(双大括号)的文本插值

 ```html
  <p>{{ message }}</p>
  <span>{{ message }}</span>
  <strong>{{ message }}</strong>
 ```

b: JavaScript表达式

 `双大括号` 中可以有一些简单的JavaScript逻辑运算:

 ```html
  <p>{{ number + 1 }}</p>
  <p>{{ number + 1 > 10 ? 'number大于10' : 'number小于10' }}</p>
  <p>{{ arr }}</p>
  <p>{{ message.split('').reverse().join('') }}</p>
 ```

c:  属性

 ```html
  <p v-bind:title="message">花括号不能使用在属性中</p>
  <a v-bind:href="url">去百度</a>
 ```

 可以简写

 ```html
  <p :title="message">花括号不能使用在属性中</p>
  <a :href="url">去百度</a>
 ```

 后面可以作为动态属性使用

 属性只中的写法和文本插值中的写法一致，也可以写简单的 JavaScript 运算表达式：

 ```html
  <p :title="message.split('').reverse().join('')">Hello World</p>
  <p :title="1 + 1">属性中的表达式</p>
  <p :title="number + 1 > 10 ? 'number大于10' : 'number小于10'">属性中的表达式</p>
 ```

`双大括号`怎么写，那么 `v-bind` 属性绑定也怎么写

d:  原始 HTML 字符串

```html
<div>{{ htmlStr }}</div>
<!-- 使用 v-html 指令渲染 html 标签内容字符串 -->
<div v-html="htmlStr"></div>
```

v-html 中绑定的 html 内容数据不能使用数据绑定

### 5. 计算属性和侦听器

### 6. Class 与 Style 绑定

### 7. 条件渲染

### 8. 列表渲染

#### (1) 遍历数组

html:

```html
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

js:

```html
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
})
```

结果：

![](https://raw.githubusercontent.com/fangshiqian/mtup/master/mtup/%E5%81%9A%E5%AE%A3%E4%BC%A05w7e)

### 9. 事件处理

### 10. 表单输入绑定

### 11. 组件基础

## 深入了解组件

### 1. 组件注册

### 2. Prop

### 3. 自定义事件

### 4. 插槽

### 5. 动态组件 & 异步组件

### 6. 处理边界情况

## 过渡 & 动画

### 1. 进入/离开 & 列表过渡

### 2. 状态过渡

## 可复用性 & 组合

### 1. 混入

### 2. 自定义指令

### 3. 渲染函数 & JSX

### 4. 插件

### 5. 过滤器

## 工具

### 1. 单文件组件

### 2. 单元测试

### 3. TypeScript 支持

### 4. 生产环境部署

## 规模化

### 1. 路由

### 2. 状态管理

### 3. 服务端渲染

## 内在

### 1. 深入响应式原理