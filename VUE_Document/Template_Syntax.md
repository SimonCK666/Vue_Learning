#<center>Template Syntax</center>

## Text
The most basic form of data binding is text interpolation using the “Mustache” syntax (double curly braces):
```html
<span>Message: {{ msg }}</span>
```
The mustache tag will be replaced with the value of the `msg` property on the corresponding data object. It will also be updated whenever the data object’s `msg` property changes.

You can also perform one-time interpolations that do not update on data change by using the <font color="green">**`v-once`**</font> directive, but keep in mind this will also affect any other bindings on the same node:
```html
<span v-once>This will never change: {{ msg }}</span>
```

## Raw HTML
The double mustaches interprets the data as plain text, not HTML. In order to output real HTML, you will need to use the `v-html` <font color="green">directive</font>:

<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>

>Using musaches:{{rawHtml}}<br>
>Using v-html directive

The contents of the `span` will be replaced with the value of the `rawHtml` property, interpreted as plain HTML - data bindings are ignored. Note that you cannot use `v-html` to compose template partials, because Vue is not a string-based templating engine. Instead, components are preferred as the fundamental unit for UI reuse and composition.
><font color="red">Dynamically rendering arbitrary HTML on your website can be very dangerous because it can easily lead to <font color="green">XSS vulnerabilities</font>. Only use HTML interpolation on trusted content and never on user-provided content.</font>

## Attributes
Mustaches cannot be used inside HTML attributes. Instead, use a <font color="red">v-bind</font> <font color="green">directive</font>:

```html
<div v-bind:id="dynamicId"></div>
```
In the case of boolean attributes, where their mere existence implies `true`, `v-bind` works a little differently. In this example:

```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```
If `isButtonDisabled` has the value of `null`, `undefined`, or `false`, the disabled attribute will not even be included in the rendered `<button>` element.

## Using JavaScript Expressions
So far we’ve only been binding to simple property keys in our templates. But Vue.js actually supports the full power of JavaScript expressions inside all data bindings:

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```
These expressions will be evaluated as JavaScript in the data scope of the owner Vue instance. One restriction is that each binding can only contain **one single expression**, so the following will **NOT** work:

```html
<!-- this is a statement, not an expression: -->
{{ var a = 1 }}

<!-- flow control won't work either, use ternary expressions -->
{{ if (ok) { return message } }}
```
><font color="red">Template expressions are sandboxed and only have access to a <font color="green">whitelist of globals</font> such as `Math` and `Date`. You should not attempt to access user defined globals in template expressions.</font>

## Shorthands

### <font color="red">`v-bind`</font> Shorthand
```html
<!-- full syntax -->
<a v-bind:href="url"> ... </a>

<!-- shorthand -->
<a :href="url"> ... </a>

<!-- shorthand with dynamic argument (2.6.0+) -->
<a :[key]="url"> ... </a>
```

## <font color="red">`v-on`</font> Shorthand
```html
<!-- full syntax -->
<a v-on:click="doSomething"> ... </a>

<!-- shorthand -->
<a @click="doSomething"> ... </a>

<!-- shorthand with dynamic argument (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```