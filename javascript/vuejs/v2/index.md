# Vue.js v2

- [Guide](https://v2.vuejs.org/v2/guide/)
- [API](https://v2.vuejs.org/v2/api/)
- [Style guide](https://v2.vuejs.org/v2/style-guide/)

Resources:

- [(Video) Full Course for Beginners](https://www.youtube.com/watch?v=4deVCNJq3qc)
- [Vue.js cheatsheet](https://devhints.io/vue)

## Custom elements

Vue’s component syntax is loosely modeled after the Custom Elements, which are part of the [Web Components Spec](https://www.w3.org/wiki/WebComponents/).
Although Vue doesn’t use custom elements internally, it has great interoperability when it comes to consuming or distributing as custom elements.

## Vue application

A Vue application consists of a root Vue instance created with `new Vue`, optionally organized into a tree of nested, reusable components.
All Vue components are also Vue instances, and so accept the same options object (except for a few root-specific options).

## Component options

- [API](https://v2.vuejs.org/v2/api/#Options-Data)

### data

- [API](https://v2.vuejs.org/v2/api/#data)
- [Guide](https://v2.vuejs.org/v2/guide/reactivity.html)

When a Vue instance is created, it adds all the properties found in its `data` object to Vue’s reactivity system.

### props

- [API](https://v2.vuejs.org/v2/api/#props)
- [Guide](https://v2.vuejs.org/v2/guide/components-props.html)
- [Type checks](https://v2.vuejs.org/v2/guide/components-props.html#Type-Checks)

A list/hash of attributes that are exposed to accept data from the parent component.

### computed

- [API](https://v2.vuejs.org/v2/api/#computed)
- [Guide](https://v2.vuejs.org/v2/guide/computed.html)
- [Computed setter](https://v2.vuejs.org/v2/guide/computed.html#Computed-Setter)

Computed properties are cached based on their reactive dependencies, and only re-computed on reactive dependency
changes.

Computed properties are by default getter-only, but you can also provide a setter when you need it.

### methods

- [API](https://v2.vuejs.org/v2/api/#methods)
- [Guide](https://v2.vuejs.org/v2/guide/events.html)

Methods to be mixed into the Vue instance. You can access these methods directly on the VM instance, or use them in directive expressions.

### watch

- [API](https://v2.vuejs.org/v2/api/#watch)
- [Guide](https://v2.vuejs.org/v2/guide/computed.html#Watchers)
- [Computed vs Watched Property](https://v2.vuejs.org/v2/guide/computed.html#Computed-vs-Watched-Property)

Watch an expression or a computed function on the Vue instance for changes. The callback gets called with the new value and the old value.

This is most useful when you want to perform asynchronous or expensive operations in response to changing data.

## Lifecycle hook

- [Guide](https://v2.vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks)
- [Diagram](https://v2.vuejs.org/images/lifecycle.png)

Note that `updated` does not guarantee that all child components have also been re-rendered. If you want to wait until
the entire view has been re-rendered, you can use `vm.$nextTick` inside of updated.

## Directives

- [Guide](https://v2.vuejs.org/v2/guide/syntax.html#Directives)

Directives are special attributes with the `v-` prefix. Directive attribute values are expected to be a single JavaScript expression.
A directive’s job is to reactively apply side effects to the DOM when the value of its expression changes.

Template expressions are sandboxed and only have access to a [whitelist](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9) of globals.

### Dynamic Arguments

- [Guide](https://v2.vuejs.org/v2/guide/syntax.html#Dynamic-Arguments)

```html
<a v-bind:[attributeName]="url"> ... </a>
```

Here `attributeName` will be dynamically evaluated as a JavaScript expression, and its evaluated value will be used as the final value for the argument.

Dynamic arguments are expected to evaluate to a string, with the exception of `null`. The special value `null` can be used to explicitly remove the binding.

## Conditional rendering

- [Guide](https://v2.vuejs.org/v2/guide/conditional.html)
- [Controlling Reusable Elements with key](https://v2.vuejs.org/v2/guide/conditional.html#Controlling-Reusable-Elements-with-key)
- [v-if vs v-show](https://v2.vuejs.org/v2/guide/conditional.html#v-if-vs-v-show)

- `v-if`
- `v-else`
- `v-else-if`
- `v-show`

## List rendering

- [Guide](https://v2.vuejs.org/v2/guide/list.html)
- [Mutation methods](https://v2.vuejs.org/v2/guide/list.html#Mutation-Methods)
- [API: key](https://v2.vuejs.org/v2/api/#key)
- [v-for with v-if](https://v2.vuejs.org/v2/guide/list.html#v-for-with-v-if)
- [DOM Template Parsing Caveats](https://v2.vuejs.org/v2/guide/components.html#DOM-Template-Parsing-Caveats)

You can also use `of` as the delimiter instead of in, so that it is closer to JavaScript’s syntax for iterators.
When iterating over an object, the order is based on the enumeration order of `Object.keys()`, which is not guaranteed to be consistent across JavaScript engine implementations.
Don’t use non-primitive values like objects and arrays as `v-for` keys.

### Additional arguments

Arrays:

```html
<li v-for="(item, index) in items">
```

Object:

```html
<li v-for="(item, index) in items">
```

### v-for with a Range

```html
<span v-for="n in 10">{{ n }}</span>
```

## Filters

- [Guide](https://v2.vuejs.org/v2/guide/filters.html)

`{{ message | capitalize }}`
