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

- Type: `{ [key: string]: Function | { get: Function, set: Function } }`

Computed properties are cached based on their reactive dependencies, and only re-computed on reactive dependency
changes.

- watch: Watchers.
- methods: Methods.

### methods

- [API](https://v2.vuejs.org/v2/api/#methods)
- [Guide](https://v2.vuejs.org/v2/guide/events.html)

Methods to be mixed into the Vue instance. You can access these methods directly on the VM instance, or use them in directive expressions.

### watch

- [API](https://v2.vuejs.org/v2/api/#watch)
- [Guide](https://v2.vuejs.org/v2/guide/computed.html#Watchers)
- [Computed vs Watched Property](https://v2.vuejs.org/v2/guide/computed.html#Computed-vs-Watched-Property)

Watch an expression or a computed function on the Vue instance for changes. The callback gets called with the new value and the old value.

While computed properties are more appropriate in most cases, there are times when a custom watcher is necessary. That's
why Vue provides a more generic way to react to data changes through the `watch` option. This is most useful when you
want to perform asynchronous or expensive operations in response to changing data.

## Lifecycle hook

- [Guide](https://v2.vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks)
- [Diagram](https://v2.vuejs.org/images/lifecycle.png)

Note that `updated` does not guarantee that all child components have also been re-rendered. If you want to wait until
the entire view has been re-rendered, you can use `vm.$nextTick` inside of updated.

## Filters

- [Guide](https://v2.vuejs.org/v2/guide/filters.html)

```js
{{ message | capitalize }}
```
