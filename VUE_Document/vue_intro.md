# <center>VUE Introduction</center>

[TOC]

## Official
--------------------

### What is VUE
---------------
>
Vue (pronounced /vjuː/, like view) is a progressive framework for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable.The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects.On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with modern tooling and supporting libraries.
If you’d like to learn more about Vue before diving in, we created a video walking through the core principles and a sample project.
If you are an experienced frontend developer and want to know how Vue compares to other libraries/frameworks, check out the Comparison with Other Frameworks.

### Getting Started
-----------------
1. The easiest way to try out Vue.js is using the Hello World example. Feel free to open it in another tab and follow along as we go through some basic examples. Or, you can create an index.html file and include Vue with:
```html
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
or:
```html
<!-- production version, optimized for size and speed -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```
2.[Installation Page](https://vuejs.org/v2/guide/installation.html)

### Declarative Rendering
-------------------------
At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax:
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
> Hello Vue!

Note that we no longer have to interact with the HTML directly. A Vue app attaches itself to a single DOM element (#app in our case) then fully controls it. The HTML is our entry point, but everything else happens within the newly created Vue instance.

In addition to text interpolation, we can also bind element attributes like this:
```html
<div id="app-2">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
  </span>
</div>
```
```js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'You loaded this page on ' + new Date().toLocaleString()
  }
})
```
>Hover your mouse over me for a few seconds to see my dynamically bound title!

Here we are encountering something new. The `v-bind` attribute you are seeing is called a **directive**. Directives are prefixed with `v-` to indicate that they are special attributes provided by Vue, and as you may have guessed, they apply special reactive behavior to the rendered DOM. Here, it is basically saying “keep this element’s `title` attribute up-to-date with the `message` property on the Vue instance.”

If you open up your JavaScript console again and enter `app2.message = 'some new message'`, you’ll once again see that the bound HTML - in this case the `title` attribute - has been updated.

## MVVM Model
------------------
- M -> model -> 负责数据存储
- V -> 负责页面展示
- VM -> View Model -> 负责业务逻辑：如：Ajax请求，对数据进行加工后交给视图展示

### MVC Model (设计模式，前后端都有)
--------------------
- M -> model -> data(放置数据) 【js变量】
- V -> view -> 视图 -> 用户所见界面 【HTML & CSS】
- C -> control -> 控制器 -> 事件交互 -> 如何根据试图与用户交互后改变数据 （如何通过DOM对象绑定事件，将变量及进行修改）
## 虚拟 DOM
-------------------------
我们可以在JS的内存里构建类似于DOM的对象，去拼装数据，拼装完整后，把数据整体解析，一次性插入到HTML里去
