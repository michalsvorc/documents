# Vue.js

- [Guide](https://vuejs.org/guide/introduction.html)
- [API](https://vuejs.org/api/)
- [Tooling](https://vuejs.org/guide/scaling-up/tooling.html)
- [Style guide](https://vuejs.org/style-guide/)

Resources:

- [Awesome Vue.js: A curated list of awesome things related to Vue.js](https://github.com/vuejs/awesome-vue)

## Features

- Declarative Rendering: Vue extends standard HTML with a template syntax that allows us to declaratively describe HTML output based on JavaScript state.
- Reactivity: Vue automatically tracks JavaScript state changes and efficiently updates the DOM when changes happen.
- Single-File Component: `*.vue` file, encapsulates the component's logic (JavaScript), template (HTML), and styles (CSS) in a single file.

## API Styles

Vue components can be authored in two different API styles:

- [Options API](https://vuejs.org/api/options-state.html): we define a component's logic using an object of options such as data, methods, and mounted.
- [Composition API](https://vuejs.org/api/composition-api-setup.html): we define a component's logic using imported API functions.

The underlying system for both is the same, as the Options API is implemented on top of the Composition API.

## Templates

- [Guide](https://vuejs.org/guide/essentials/template-syntax.htm)
- [Restricted Globals Access](https://vuejs.org/guide/essentials/template-syntax.html#restricted-globals-access)

## Directives

- [Built in directives](https://vuejs.org/api/built-in-directives.html)
- [Custom directives](https://vuejs.org/guide/reusability/custom-directives.html#introduction)

## Computed properties

- [Guide](https://vuejs.org/guide/essentials/computed.html)

For complex logic that includes reactive data, it is recommended to use a computed property. Computed properties are cached based
on their reactive dependencies. A computed property will only re-evaluate when some of its reactive dependencies have
changed.

## Class and Style Bindings

- [Guide](https://vuejs.org/guide/essentials/class-and-style.html)

Vue provides special enhancements when `v-bind` is used with `class` and `style`.

When you use a CSS property that requires a vendor prefix in `:style`, Vue will automatically add the appropriate prefix.

### Binding HTML Classes

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

### Binding Inline Styles

Object Syntax:

```html
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
<div :style="styleObject"></div>
```

Array Syntax:

```html
<div :style="[baseStyles, overridingStyles]"></div>
```

## Conditional Rendering

- [Guide](https://vuejs.org/guide/essentials/conditional.html)

Using `v-if` and `v-for` together is [not recommended](https://vuejs.org/style-guide/rules-essential.html#avoid-v-if-with-v-for).

If we want to toggle more than one element, we can use `v-if` on a `<template>`:

```html
<template v-if="ok">
  <!-- multiple components -->
</template>
```

### v-show

`v-show` will always be rendered and remain in the DOM; `v-show` only toggles the display CSS property of the element.

`v-show` doesn't support the `<template>` element, nor does it work with `v-else`.

Generally speaking, `v-if` has higher toggle costs while `v-show` has higher initial render costs.

## List Rendering

- [Guide](https://vuejs.org/guide/essentials/list.html)

- `v-for="item in items"`
- `v-for="item of items"`

When iterating over an object, the order is based on the enumeration order of `Object.keys()`, which isn't guaranteed to
be consistent across JavaScript engine implementations. It is recommended to provide a key attribute with `v-for`
whenever possible:

```html
<div v-for="item in items" :key="item.id"></div>
```

`v-for` can also take an integer as a range. In this case it will repeat the template that many times.

## Event Handling

- [Guide](https://vuejs.org/guide/essentials/event-handling.html)
- [Key aliases](https://vuejs.org/guide/essentials/event-handling.html#key-modifiers)

We can use the `v-on` directive, which we typically shorten to the `@` symbol, to listen to DOM events.
You can directly use any valid key names exposed via `KeyboardEvent.key` as modifiers by converting them to kebab-case.

## Form Input Bindings

- [Guide](https://vuejs.org/guide/essentials/forms.html)
- [Modifiers](https://vuejs.org/guide/essentials/forms.html#modifiers)

You can use the `v-model` directive to create two-way data bindings on form input, textarea, and select elements.
