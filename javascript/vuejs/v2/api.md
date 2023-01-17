# Vue.js v2 API

- [API](https://v2.vuejs.org/v2/api/)

## Global config

- [API](https://v2.vuejs.org/v2/api/#Global-Config)

Every Vue application exposes a config object that contains the configuration settings for that application.

## Global API

- [API](https://v2.vuejs.org/v2/api/#Global-API)

### Vue.set( target, propertyName/index, value )

- [API](https://v2.vuejs.org/v2/api/#Vue-set)

Adds a property to a reactive object, ensuring the new property is also reactive, so triggers view updates. This must be
used to add new properties to reactive objects, as Vue cannot detect normal property additions

### Vue.directive( id, [definition] )

- [API](https://v2.vuejs.org/v2/api/#Vue-directive)
- [Custom directives](https://v2.vuejs.org/v2/guide/custom-directive.html)

Register or retrieve a global directive.

### Vue.filter( id, [definition] )

- [API](https://v2.vuejs.org/v2/api/#Vue-filter)
- [Filters](https://v2.vuejs.org/v2/guide/filters.html)

Register or retrieve a global filter.

### Vue.component( id, [definition] )

- [API](https://v2.vuejs.org/v2/api/#Vue-component)
- [Components](https://v2.vuejs.org/v2/guide/components.html)

Register or retrieve a global component. Registration also automatically sets the component’s name with the given id.

### Vue.observable( object )

- [API](https://v2.vuejs.org/v2/api/#Vue-observable)

Make an object reactive. Internally, Vue uses this on the object returned by the data function.

The returned object can be used directly inside render functions and computed properties, and will trigger appropriate
updates when mutated. It can also be used as a minimal, cross-component state store for simple scenarios.

## Options: DOM

- [el](https://v2.vuejs.org/v2/api/#el)
- [template](https://v2.vuejs.org/v2/api/#template)
- [render](https://v2.vuejs.org/v2/api/#render)
- [renderError](https://v2.vuejs.org/v2/api/#renderError)

## Options: Lifecycle hooks

- [Lifecycle Diagram](https://v2.vuejs.org/v2/guide/instance.html#Lifecycle-Diagram)

- [beforeCreate](https://v2.vuejs.org/v2/api/#beforeCreate)
- [created](https://v2.vuejs.org/v2/api/#created)
- [beforeMount](https://v2.vuejs.org/v2/api/#beforeMount)
- [mounted](https://v2.vuejs.org/v2/api/#mounted)
- [beforeUpdate](https://v2.vuejs.org/v2/api/#beforeUpdate)
- [updated](https://v2.vuejs.org/v2/api/#updated)
- [activated](https://v2.vuejs.org/v2/api/#activated)
- [deactivated](https://v2.vuejs.org/v2/api/#deactivated)
- [beforeDestroy](https://v2.vuejs.org/v2/api/#beforeDestroy)
- [destroyed](https://v2.vuejs.org/v2/api/#destroyed)
- [errorCaptured](https://v2.vuejs.org/v2/api/#errorCaptured)

## Options: Assets

### directives

- [API](https://v2.vuejs.org/v2/api/#directives)
- [Guide](https://v2.vuejs.org/v2/guide/custom-directive.html)

A hash of directives to be made available to the Vue instance.

In addition to the default set of directives shipped in core (v-model and v-show), Vue also allows you to register your
own custom directives.

### filters

- [API](https://v2.vuejs.org/v2/guide/filters.html)
- [Guide](https://v2.vuejs.org/v2/guide/filters.html)

A hash of filters to be made available to the Vue instance.

Vue.js allows you to define filters that can be used to apply common text formatting.

### components

- [API](https://v2.vuejs.org/v2/api/#components)
- [Local registration](https://v2.vuejs.org/v2/guide/components-registration.html#Local-Registration)

A hash of components to be made available to the Vue instance.

You can define your components as plain JavaScript objects, then define the components you’d like to use in a
`components` option for local registration.

## Options: Composition

### parent

- [API](https://v2.vuejs.org/v2/api/#parent)

Use `$parent` and `$children` sparingly - they mostly serve as an escape-hatch.

Prefer using props and events for parent-child communication.

### mixins

- [API](https://v2.vuejs.org/v2/api/#mixins)
- [Guide](https://v2.vuejs.org/v2/guide/mixins.html)

Mixin objects can contain instance options like normal instance objects, and they will be merged against the eventual
options using the same option merging logic in `Vue.extend()`.

### extends

- [API](https://v2.vuejs.org/v2/api/#extends)

Allows declaratively extending another component (could be either a plain options object or a constructor) without
having to use `Vue.extend`. This is primarily intended to make it easier to extend between single file components.

This is similar to `mixins`.

### provide / inject

- [API](https://v2.vuejs.org/v2/api/#provide-inject)

- Type:
  - provide: `Object | () => Object`
  - inject: `Array<string> | { [key: string]: string | Symbol | Object }`

This pair of options are used together to allow an ancestor component to serve as a dependency injector for all its
descendants, regardless of how deep the component hierarchy is, as long as they are in the same parent chain.

You can use ES2015 Symbols as keys in this object.

If you are familiar with React, this is very similar to React’s context feature.

The provide and inject bindings are _NOT reactive_. This is intentional. However, if you pass down an observed object,
properties on that object do remain reactive.

## Options: Misc

### name

- [API](https://v2.vuejs.org/v2/api/#name)

- Type: `string`

Allow the component to recursively invoke itself in its template. Note that when a component is registered globally with
`Vue.component()`, the global ID is automatically set as its name.

### functional

- [API](https://v2.vuejs.org/v2/api/#functional)
- [Guide](https://v2.vuejs.org/v2/guide/render-function.html#Functional-Components)

- Type: `boolean`

Causes a component to be stateless (no `data`) and instanceless (no `this` context).

They are only a `render` function that returns virtual nodes making them much cheaper to render.

### model

- [API](https://v2.vuejs.org/v2/api/#model)
- [Customizing Component v-model](https://v2.vuejs.org/v2/guide/components-custom-events.html#Customizing-Component-v-model)

- Type: `{ prop?: string, event?: string }`

Allows a custom component to customize the prop and event used when it's used with `v-model`.

By default, `v-model` on a component uses `value` as the prop and `input` as the event, but some input types such as
checkboxes and radio buttons may want to use the `value` prop for a different purpose.

Using the `model` option can avoid the conflict in such cases.

### inheritAttrs

- [API](https://v2.vuejs.org/v2/api/#inheritAttrs)
- [Disabling Attribute Inheritance](https://v2.vuejs.org/v2/guide/components-props.html#Disabling-Attribute-Inheritance)

- Type: boolean
- Default: true

By default, parent scope attribute bindings that are not recognized as props will "fallthrough" and be applied to the
root element of the child component as normal HTML attributes.

By setting `inheritAttrs: false`, this default behavior can be disabled. The attributes are available via the `$attrs`
instance property and can be explicitly bound to a non-root element using `v-bind`.

With `inheritAttrs: false` and `$attrs`, you can manually decide which element you want to forward attributes to, which
is often desirable for base components

## Instance

### Instance Properties

- [API](https://v2.vuejs.org/v2/api/#Instance-Properties)

- `vm.$data`: The data object that the Vue instance is observing.
- `vm.$props`: An object representing the current props a component has received.
- `vm.$el`: The root DOM element that the Vue instance is managing.
- `vm.$options`: The instantiation options used for the current Vue instance.
- `vm.$parent`: The parent instance, if the current instance has one.
- `vm.$root`: The root Vue instance of the current component tree.
- `vm.$children`: The direct child components of the current instance.
- `vm.$slots`: Used to programmatically access content distributed by slots.
- `vm.$scopedSlots`: Used to programmatically access scoped slots.
- `vm.$refs`: An object of DOM elements and component instances, registered with `ref` attributes.
- `vm.$isServer`: Whether the current Vue instance is running on the server.
- `vm.$attrs`: Contains parent-scope attribute bindings that are not recognized (and extracted) as props.
- `vm.$listeners`: Contains parent-scope `v-on` event listeners (without `.native` modifiers).

Note there’s no order guarantee for `$children`, and it is not reactive.

### Instance Methods: Data

- [API](https://v2.vuejs.org/v2/api/#Instance-Methods-Data)

- `vm.$watch`: Watch an expression or a computed function on the Vue instance for changes.
- `vm.$set`: This is the alias of the global Vue.set.
- `vm.$delete`: This is the alias of the global Vue.delete.

### Instance Methods: Events

- `vm.$on`: Listen for a custom event on the current vm.
- `vm.$once`: Listen for a custom event, only once. The listener will be removed once it triggers for the first time.
- `vm.$off`: Remove custom event listener(s).
- `vm.$emit`: Trigger an event on the current instance.

### Instance Methods: Lifecycle

- `vm.$mount`: Can be used to manually start the mounting of an unmounted Vue instance.
- `vm.$forceUpdate`: Force the Vue instance to re-render. Note it does not affect all child components, only the
  instance itself and child components with inserted slot content.
- `vm.$nextTick`: Defer the callback to be executed after the next DOM update cycle.
- `vm.$destroy`: Completely destroy a vm. Clean up its connections with other existing vms, unbind all its directives,
  turn off all event listeners.

## Directives

### v-text

- [API](https://v2.vuejs.org/v2/api/#v-text)

Updates the element’s textContent. If you need to update the part of textContent, you should use `{{ }}` interpolations.

```html
<span v-text="msg"></span>
<!-- same as -->
<span>{{msg}}</span>
```

### v-html

- [API](https://v2.vuejs.org/v2/api/#v-html)

Updates the element's innerHTML. Note that the contents are inserted as plain HTML - they will not be compiled as Vue
templates.

Dynamically rendering arbitrary HTML on your website can be very dangerous because it can easily lead to XSS attacks.

### v-show

- [API](https://v2.vuejs.org/v2/api/#v-show)
- [Guide](https://v2.vuejs.org/v2/guide/conditional.html#v-show)
- [v-if vs v-show](https://v2.vuejs.org/v2/guide/conditional.html#v-if-vs-v-show)

Toggles the element's `display` CSS property based on the truthy-ness of the expression value.

### v-if

- [API](https://v2.vuejs.org/v2/api/#v-if)
- [Guide](https://v2.vuejs.org/v2/guide/conditional.html)

Conditionally render the element based on the truthy-ness of the expression value.

Add a [key attribute](https://v2.vuejs.org/v2/guide/conditional.html#Controlling-Reusable-Elements-with-key) with unique
values to stop reusing elements and rendered from scratch on each conditional switch.

### v-else

- [API](https://v2.vuejs.org/v2/api/#v-else)

Denote the else block for `v-if` or a `v-if/v-else-if` chain.

### v-else-if

- [API](https://v2.vuejs.org/v2/api/#v-else-if)

Denote the else if block for `v-if`. Can be chained.

### v-for

- [API](https://v2.vuejs.org/v2/api/#v-for)
- [List rendering](https://v2.vuejs.org/v2/guide/list.html)
- [key](https://v2.vuejs.org/v2/guide/list.html#key)
- [v-for with a Component](https://v2.vuejs.org/v2/guide/list.html#v-for-with-a-Component)

- Expects: `Array | Object | number | string | Iterable`

The directive's value must use the special syntax `alias in expression` to provide an alias for the current element
being iterated on.

Alternatively, you can also specify an alias for the index (or the key if used on an Object):

```html
<div v-for="(item, index) in items"></div>
<div v-for="(val, key) in object"></div>
<div v-for="(val, name, index) in object"></div>
```

To reorder elements, you need to provide an ordering hint with the `key` special attribute:

```html
<div v-for="item in items" :key="item.id">{{ item.text }}</div>
```

When iterating over an _object_, the order is based on the enumeration order of `Object.keys()`, which is not guaranteed
to be consistent across JavaScript engine implementations. Don’t use non-primitive values like objects and arrays as
`v-for` keys. Use string or numeric values instead.

In 2.6+, v-for can also work on values that implement the Iterable Protocol, including native `Map` and `Set`.

However, it should be noted that Vue 2.x currently does not support reactivity on `Map` and `Set` values, so cannot
automatically detect changes.

You can also use `of` as the delimiter instead of `in`, so that it is closer to JavaScript’s syntax for iterators

`v-for` can also take an integer as a range. In this case it will repeat the template that many times.

### v-on

- [API](https://v2.vuejs.org/v2/api/#v-on)
- [Event Handling](https://v2.vuejs.org/v2/guide/events.html)
- [Event modifiers](https://v2.vuejs.org/v2/guide/events.html#Event-Modifiers)
- [Components - Custom Events](https://v2.vuejs.org/v2/guide/components.html#Custom-Events)

- Shorthand: `@`
- Expects: `Function | Inline Statement | Object`
- Argument: `event`
- Modifiers:
  - `.stop` - call event.stopPropagation().
  - `.prevent` - call event.preventDefault().
  - `.capture` - add event listener in capture mode.
  - `.self` - only trigger handler if event was dispatched from this element.
  - `.{keyCode | keyAlias}` - only trigger handler on certain keys.
  - `.native` - listen for a native event on the root element of component.
  - `.once` - trigger handler at most once.
  - `.left` - (2.2.0+) only trigger handler for left button mouse events.
  - `.right` - (2.2.0+) only trigger handler for right button mouse events.
  - `.middle` - (2.2.0+) only trigger handler for middle button mouse events.
  - `.passive` - (2.3.0+) attaches a DOM event with { passive: true }.

Don’t use `.passive` and `.prevent` together, because `.prevent` will be ignored and your browser will probably show you
a warning. Remember, `.passive` communicates to the browser that you don’t want to prevent the event’s default behavior.

Sometimes we also need to access the original DOM event in an inline statement handler. You can pass it into a method
using the special `$event` variable.

### v-bind

- [API](https://v2.vuejs.org/v2/api/#v-bind)
- [Class and Style Bindings](https://v2.vuejs.org/v2/guide/class-and-style.html)
- [Components - Props](https://v2.vuejs.org/v2/guide/components.html#Props)
- [Components - .sync Modifier](https://v2.vuejs.org/v2/guide/components.html#sync-Modifier)

- Shorthand: `:`
- Expects: `any (with argument) | Object (without argument)`
- Argument: `attrOrProp (optional)`
- Modifiers:
  - `.prop` - Bind as a DOM property instead of an attribute. If the tag is a component then .prop will set the property
    on the component’s `$el`.
    [See](https://stackoverflow.com/questions/6003819/properties-and-attributes-in-html#answer-6004028)
  - `.camel` - (2.1.0+) transform the kebab-case attribute name into camelCase.
  - `.sync` - (2.3.0+) a syntax sugar that expands into a v-on handler for updating the bound value.

Dynamically bind one or more attributes, or a component prop to an expression.

### v-model

- [API](https://v2.vuejs.org/v2/api/#v-model)
- [Form Input Bindings](https://v2.vuejs.org/v2/guide/forms.html)
- [Modifier](https://v2.vuejs.org/v2/guide/forms.html#Modifiers)
- [Components - Form Input Components using Custom Events](https://v2.vuejs.org/v2/guide/components.html#Form-Input-Components-using-Custom-Events)

- Limited to:

  - `<input>`
  - `<select>`
  - `<textarea>`
  - components

- Modifiers:
  - `.lazy` - listen to change events instead of input
  - `.number` - cast valid input string to numbers
  - `.trim` - trim input

Create a two-way binding on a form input element or a component:

- text and textarea elements use `value` property and `input` event;
- checkboxes and radiobuttons use `checked` property and `change` event;
- select fields use `value` as a prop and `change` as an event.

`v-model` will ignore the initial `value`, `checked`, or `selected` attributes found on any form elements. It will
always treat the Vue instance data as the source of truth. You should declare the initial value on the JavaScript side,
inside the `data` option of your component.

```html
<input v-model="searchText" />

<!-- does the same thing as -->

<input v-bind:value="searchText" v-on:input="searchText = $event.target.value" />
```

### v-slot

- [API](https://v2.vuejs.org/v2/api/#v-slot)
- [Guide](https://v2.vuejs.org/v2/guide/components-slots.html)

- Shorthand: `#`
- Limited to:
  - `<template>`
  - components (for a lone default slot with props)

Denote named slots or slots that expect to receive props.

### v-pre

- [API](https://v2.vuejs.org/v2/api/#v-pre)

Skip compilation for this element and all its children. You can use this for displaying raw mustache tags.

### v-cloak

- [API](https://v2.vuejs.org/v2/api/#v-cloak)

This directive will remain on the element until the associated Vue instance finishes compilation. Combined with CSS
rules such as `[v-cloak] { display: none }`, this directive can be used to hide un-compiled mustache bindings until the
Vue instance is ready.

### v-once

- [API](https://v2.vuejs.org/v2/api/#v-once)
- [Guide](https://v2.vuejs.org/v2/guide/components.html#Cheap-Static-Components-with-v-once)

Render the element and component once only. On subsequent re-renders, the element/component and all its children will be
treated as static content and skipped. This can be used to optimize update performance.

## Special Attributes

### key

- [API](https://v2.vuejs.org/v2/api/#key)
- [key](https://v2.vuejs.org/v2/guide/list.html#key)

- Expects: `number | string | boolean (since 2.4.2) | symbol (since 2.5.12)`

The `key` special attribute is primarily used as a hint for Vue’s virtual DOM algorithm to identify VNodes when diffing
the new list of nodes against the old list.

Children of the same common parent must have unique keys. Duplicate keys will cause render errors.

### ref

- [API](https://v2.vuejs.org/v2/api/#ref)
- [Guide](https://v2.vuejs.org/v2/guide/components.html#Child-Component-Refs)

`ref` is used to register a reference to an element or a child component. The reference will be registered under the
parent component's `$refs` object.

If used on a plain DOM element, the reference will be that element; if used on a child component, the reference will be
component instance.

### is

- [API](https://v2.vuejs.org/v2/api/#is)
- [Dynamic Components](https://v2.vuejs.org/v2/guide/components.html#Dynamic-Components)
- [DOM Template Parsing Caveats](https://v2.vuejs.org/v2/guide/components.html#DOM-Template-Parsing-Caveats)

Used for dynamic components and to work around limitations of in-DOM templates.

## Built-In Components

### component

- [API](https://v2.vuejs.org/v2/api/#component)
- [Guide](https://v2.vuejs.org/v2/guide/components.html#Dynamic-Components)

Props:

- `is` - string | ComponentDefinition | ComponentConstructor
- `inline-template` - boolean

A _meta component_ for rendering dynamic components. The actual component to render is determined by the `is` prop.

### transition

- [API](https://v2.vuejs.org/v2/api/#transition)
- [Guide](https://v2.vuejs.org/v2/guide/transitions.html)

`<transition>` serve as transition effects for _single_ element/component. The `<transition>` only applies the
transition behavior to the wrapped content inside; it doesn’t render an extra DOM element, or show up in the inspected
component hierarchy.

### transition-group

- [API](https://v2.vuejs.org/v2/api/#transition-group)
- [Guide](https://v2.vuejs.org/v2/guide/transitions.html)

`<transition-group>` serve as transition effects for _multiple_ elements/components. The `<transition-group>` renders a
real DOM element. By default it renders a `<span>`, and you can configure what element it should render via the tag
attribute.

### keep-alive

- [API](https://v2.vuejs.org/v2/api/#keep-alive)
- [Guide](https://v2.vuejs.org/v2/guide/components.html#keep-alive)
- [keep-alive with Dynamic Components](https://v2.vuejs.org/v2/guide/components-dynamic-async.html#keep-alive-with-Dynamic-Components)

Props:

- `include` - string or RegExp or Array. Only components with matching names will be cached.
- `exclude` - string or RegExp or Array. Any component with a matching name will not be cached.
- `max` - number. The maximum number of component instances to cache.

Primarily used to preserve component state or avoid re-rendering.

When switching between these components though, you’ll sometimes want to maintain their state or avoid re-rendering for
performance reasons. Recreating dynamic components is normally useful behavior, but sometimes we’d really like those tab
component instances to be cached once they’re created for the first time.

When wrapped around a dynamic component, `<keep-alive>` caches the inactive component instances without destroying them.
Similar to `<transition>`, `<keep-alive>` is an abstract component: it doesn’t render a DOM element itself, and doesn’t
show up in the component parent chain.

When a component is toggled inside `<keep-alive>`, its `activated` and `deactivated` lifecycle hooks will be invoked
accordingly.

Note that <keep-alive> requires the components being switched between to all have names, either using the name option on
a component, or through local/global registration.

### slot

- [API](https://v2.vuejs.org/v2/api/#slot)
- [Guide](https://v2.vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots)

`<slot>` serve as content distribution outlets in component templates. `<slot>` itself will be replaced.
