# Vue.js

Documentation:

- [v3](https://v3.vuejs.org/)
- [v2](https://vuejs.org/)
- [v2 to v3 Migration](https://v3.vuejs.org/guide/migration/introduction.html#migration-build)

Style guide:

- [v3](https://v3.vuejs.org/style-guide/)
- [v2](https://vuejs.org/v2/style-guide/#Base-component-names-strongly-recommended)

Tools:

- [Vue Devtools](https://github.com/vuejs/devtools#vue-devtools)
- [Vue CLI](https://cli.vuejs.org/)

External:

- [Awesome Vue.js](https://github.com/vuejs/awesome-vue)

## Syntax

Vue uses a `$` prefix when exposing its own built-in APIs via the component instance. It also reserves the prefix `_`
for internal properties. You should avoid using names for top-level data properties that start with either of these
characters.

Vue provides special shorthands for two of the most often used directives:

`v-bind:href` => `:href`, `:[key]`
`v-on:click` => `@click`, `@[event]`

Interpolation on `<textarea>` won't work. Use `v-model` instead.

## Application instance

- [API](https://v3.vuejs.org/guide/instance.html)
- [Application Instance](https://v3.vuejs.org/guide/instance.html)

Every Vue application starts by creating a new application instance with the `createApp` function. The application
instance is used to register 'globals' that can then be used by components within that application.

## Directives

- [Dynamic arguments](https://vuejs.org/v2/guide/syntax.html#Dynamic-Arguments)

Directives are special attributes with the `v-` prefix. A directive's job is to reactively apply side effects to the DOM
when the value of its expression changes.

```
v-<directive>
v-<directive>:argument
v-<directive>:[argument]
v-<directive>:argument.modifier
```

## Data

- [Guide](https://v3.vuejs.org/guide/data-methods.html)

When a Vue instance is created, it adds all the properties found in its `data` object to Vue’s reactivity system.

Data are only reactive if they existed when the instance was created.

It should return an object, which Vue will then wrap in its reactivity system and store on the component instance as
`$data`.

```vue
vm.count === vm.$data.count
```

Where necessary, use `null`, `undefined` or some other placeholder value for properties where the desired value isn't
yet available.

## Methods

- [Guide](https://v3.vuejs.org/guide/data-methods.html#methods)
- [Debouncing and Throttling](https://v3.vuejs.org/guide/data-methods.html#debouncing-and-throttling)

To add methods to a component instance we use the `methods` option. Methods called from a template should not have any
side effects, such as changing data or triggering asynchronous processes.

Vue automatically binds the `this` value for methods so that it always refers to the component instance. This ensures
that a method retains the correct `this` value if it's used as an event listener or callback. You should avoid using
arrow functions when defining methods, as that prevents Vue from binding the appropriate `this` value.

## Computed properties

- [Guide](https://v3.vuejs.org/guide/computed.html)
- [Computed vs Watched Property](https://v3.vuejs.org/guide/computed.html#computed-vs-watched-property)
- [Computed setter](https://v3.vuejs.org/guide/computed.html#computed-setter)

You should use a computed property for complex logic that includes reactive data. Computed properties are cached based
on their reactive dependencies. A computed property will only re-evaluate when some of its reactive dependencies have
changed.

## Watchers

- [Guide](https://v3.vuejs.org/guide/computed.html#watchers)

While computed properties are more appropriate in most cases, there are times when a custom watcher is necessary. That's
why Vue provides a more generic way to react to data changes through the `watch` option. This is most useful when you
want to perform asynchronous or expensive operations in response to changing data.

You can also use the imperative [$watch](https://v3.vuejs.org/api/instance-methods.html#watch) API.

It is often a better idea to use a computed property rather than an imperative watch callback.

## Styling

- [Guide](https://v3.vuejs.org/guide/class-and-style.html)

Vue provides special enhancements when v-bind is used with class and style. In addition to strings, the expressions can
also evaluate to objects or arrays.

### Classes

Object Syntax:

```html
<div :class="{ active: isActive }"></div>

<div :class="classObject"></div>
```

Array Syntax:

```html
<div :class="[activeClass, errorClass]"></div>

<div :class="[isActive ? activeClass : '', errorClass]"></div>

<div :class="[{ active: isActive }, errorClass]"></div>
```

If your component has multiple root elements, you would need to define which component will receive this class. You can
do this using `$attrs` component property:

```html
<p :class="$attrs.class">Hi!</p>
```

### Inline Styles

Object Syntax:

```html
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

<div :style="styleObject"></div>
```

Array Syntax:

```html
<div :style="[baseStyles, overridingStyles]"></div>
```

Prefixing:

When you use a CSS property that requires a vendor prefix (opens new window) in :style, Vue will automatically add the
appropriate prefix.

```html
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

## Conditional Rendering

- [Guide](https://v3.vuejs.org/guide/conditional.html)

- `v-if`
- `v-else`
- `v-else-if`
- `v-show`

If we want to toggle more than one element, we can use `v-if` on a `<template>` element, which serves as an invisible
wrapper. The final rendered result will not include the `<template>` element.

`v-show` will always be rendered and remain in the DOM; `v-show` only toggles the display CSS property of the element.

`v-show` doesn't support the `<template>` element, nor does it work with `v-else`.

Generally speaking, `v-if` has higher toggle costs while `v-show` has higher initial render costs. So prefer `v-show` if
you need to toggle something very often, and prefer `v-if` if the condition is unlikely to change at runtime.

Using `v-if` and `v-for` together is not recommended.

## List Rendering

- [Guide](https://v3.vuejs.org/guide/list.html)
- [Array Change Detection](https://v3.vuejs.org/guide/list.html#array-change-detection)
- [v-for with v-if](https://v3.vuejs.org/guide/list.html#v-for-with-v-if)

- `v-for="item in items"`
- `v-for="item of items"`

When iterating over an object, the order is based on the enumeration order of `Object.keys()`, which isn't guaranteed to
be consistent across JavaScript engine implementations. It is recommended to provide a key attribute with `v-for`
whenever possible:

```html
<div v-for="item in items" :key="item.id"></div>
```

`v-for` can also take an integer as a range. In this case it will repeat the template that many times.

## Events

- [Guide](https://v3.vuejs.org/guide/events.html)
- [Key aliases](https://v3.vuejs.org/guide/events.html#key-aliases)

We can use the `v-on` directive, which we typically shorten to the `@` symbol, to listen to DOM events and run some
JavaScript when they're triggered. You can have multiple methods in an event handler separated by a comma. `this` inside
methods points to the current active instance.

Vue provides event modifiers for `v-on`:

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`
- `.passive`

The `.passive` modifier is especially useful for improving performance on mobile devices. `.passive` communicates to the
browser that you don't want to prevent the event's default behavior. Don't use `.passive` and `.prevent` together.

We recommend you always use kebab-case for event names.

## Form inputs

- [Guide](https://v3.vuejs.org/guide/forms.html)

You can use the v-model directive to create two-way data bindings on form input, textarea, and select elements.

v-model will ignore the initial value, checked or selected attributes found on any form elements. It will always treat
the current active instance data as the source of truth. You should declare the initial value on the JavaScript side,
inside the data option of your component.

[Built-in modifiers](https://v3.vuejs.org/guide/forms.html#modifiers)

- `.lazy`
- `.number`
- `.trim`

## Templates

Template expressions in `{{ }}` are sandboxed and only have access to a [whitelist of
globals](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9).

## Caveats

- [Template syntax](https://v3.vuejs.org/guide/template-syntax.html#caveats)

### v-if with v-for

Using `v-if` and `v-for` together is not recommended. When used together with `v-if`, `v-for` has a higher priority than
`v-if`.
