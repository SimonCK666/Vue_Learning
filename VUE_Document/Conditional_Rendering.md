# <center>Conditional Rendering</center>

[TOC]

## Introduction
It’s easy to toggle the presence of an element, too:
```html
<div id="app-3">
  <span v-if="seen">Now you see me</span>
</div>
```
```js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```
>Now you see me

Go ahead and enter `app3.seen = false` in the console. You should see the message disappear.

This example demonstrates that we can bind data to not only text and attributes, but also the **structure** of the DOM. Moreover, Vue also provides a powerful transition effect system that can automatically apply *transition effects* when elements are inserted/updated/removed by Vue.

## `v-if`
The directive `v-if` is used to conditionally render a block. The block will only be rendered if the directive’s expression returns a truthy value.
```html
<h1 v-if="awesome">Vue is awesome!</h1>
```
It is also possible to add an “else block” with `v-else`:
```html
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```
## `v-else`
You can use the `v-else` directive to indicate an “else block” for `v-if`:
```html
<div v-if="Math.random() > 0.5">
  Now you see me
</div>
<div v-else>
  Now you don't
</div>
```
**A `v-else` element must immediately follow a v-if or a v-else-if element, otherwise it will not be recognized.**

## `v-else-if`
>New in 2.1.0+

The `v-else-if`, as the name suggests, serves as an “else if block” for `v-if`. It can also be chained multiple times:
```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
>**<font color="red">Similar to `v-else`, a `v-else-if` element must immediately follow a `v-if` or a `v-else-if` element.**</font>

## `v-show`
Another option for conditionally displaying an element is the v-show directive. The usage is largely the same:
```html
<h1 v-show="ok">Hello!</h1>
```
The difference is that an element with `v-show` will always be rendered and remain in the DOM; `v-show` only toggles the display CSS property of the element.
><font color="red">**Note that `v-show` doesn’t support the `<template>` element, nor does it work with `v-else`.**</font>

## `v-if` vs `v-show`

`v-if` is “real” conditional rendering because it ensures that event listeners and child components inside the conditional block are properly destroyed and re-created during toggles.

`v-if` is also **lazy**: if the condition is false on initial render, it will not do anything - the conditional block won’t be rendered until the condition becomes true for the first time.

In comparison, `v-show` is much simpler - the element is always rendered regardless of initial condition, with CSS-based toggling.

Generally speaking, `v-if` has higher toggle costs while `v-show` has higher initial render costs. So prefer `v-show` if you need to toggle something very often, and prefer `v-if` if the condition is unlikely to change at runtime.