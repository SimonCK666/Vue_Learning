# <center>List Rendering</center>
## Mapping an Array to Elements with `v-for`
We can use the `v-for` directive to render a list of items based on an array. The `v-for` directive requires a special syntax in the form of `item in items`, where `items` is the source data array and `item` is an **alias** for the array element being iterated on:
```html
<ul id="example-1">
  <li v-for="item in items" :key="item.message">
    {{ item.message }}
  </li>
</ul>
```
```js
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
Result:<br>
>**·** Foo<br>
>**·** Bar

Inside `v-for` blocks we have full access to parent scope properties. `v-for` also supports an optional <font color="red">second argument</font> for the index of the current item.
```html
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```
```js
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
Result:
> **·** Parent - 0 - Foo<br>
> **·** Parent - 1 - Bar

You can also use <font color="red">`of`</font> as the delimiter instead of in, so that it is closer to JavaScript’s syntax for iterators:
```html
<div v-for="item of items"></div>
```

## <font color="red">`v-for`</font> with an Object
You can also use v-for to iterate through the properties of an object.
```html
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```
```js
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
Result:
>**·** How to do lists in Vue
>**·** Jane Doe
>**·** 2016-04-10

