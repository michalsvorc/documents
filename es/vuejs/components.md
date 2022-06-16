# Components

- [Guide](https://v3.vuejs.org/guide/component-basics.html)

In Vue, a component is essentially an instance with pre-defined options. Registering a component in Vue is
straightforward: we create a component object as we did with App objects and we define it in parent's components option.

```vue
app.mount
```

Since components are reusable instances, they accept the same options as a root instance.

See the [API](https://v3.vuejs.org/api/application-api.html).

## Web Components

- [Guide](https://v3.vuejs.org/guide/introduction.html#composing-with-components)
- [MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)

Vue components look similar to Custom Elements, which are part of the Web Components Spec (opens new window). Indeed,
parts of Vue's component design (for example the slot API) were influenced by the spec before it was natively
implemented in browsers.

## Registration

- [Guide](https://v3.vuejs.org/guide/component-registration.html)

To use these components in templates, they must be registered so that Vue knows about them. There are two types of
component registration: global and local.

### Global registration

```vue
Vue.createApp({...}).component('my-component-name', ...)
```

These components are globally registered for the application. That means they can be used in the template of any
component instance within this application.

Global registration often isn't ideal for code bundlers.

### Local registration

Locally registered components are not also available in subcomponents.

You can define your components as plain JavaScript objects, then define the components you'd like to use in a
`components` option:

```vue
const app = Vue.createApp({ components: { 'component-a': ComponentA, // plain object 'component-b': ComponentB // plain
object } })
```

## Props

- [Introduction](https://v3.vuejs.org/guide/component-basics.html#passing-data-to-child-components-with-props)
- [Guide](https://v3.vuejs.org/guide/component-props.html#props)

Props are custom attributes you can register on a component. All props form a one-way-down binding between the child
property and the parent one.

Static props:

```html
<blog-post title="My journey with Vue"></blog-post>
<!-- evaluates to string -->
```

Props are assigned dynamically with `v-bind` or its shortcut, the `:` character:

```html
<blog-post :title="post.title"></blog-post>
<!-- evaluates to title property of post object -->
<blog-post :likes="42"></blog-post>
<!-- evaluates to number -->
<blog-post :is-published="false"></blog-post>
<!-- evaluates to boolean -->
```

If you want to pass all the properties of an object as props, you can use `v-bind` without an argument:

```html
<blog-post v-bind="post"></blog-post>

<!-- Will be equivalent to: -->
<blog-post v-bind:id="post.id" v-bind:title="post.title"></blog-post>
```

## Non-Prop Attributes

- [Guide](https://v3.vuejs.org/guide/component-attrs.html)

A component non-prop attribute is an attribute or event listener that is passed to a component, but does not have a
corresponding property defined in props or emits.

Common examples of this include: class, style, and id attributes.

You can access those attributes via `$attrs` property.

When a component returns a single root node, non-prop attributes will automatically be added to the root node's
attributes. If you do not want a component to automatically inherit attributes, you can set `inheritAttrs: false` in the
component's options.

### Immutability

You should not attempt to mutate a prop inside a child component. Note that objects and arrays in JavaScript are passed
by reference, so if the prop is an array or object, mutating the object or array itself inside the child component will
affect parent state.

### Casing

- [Guide](https://v3.vuejs.org/guide/component-props.html#prop-casing-camelcase-vs-kebab-case)

HTML attribute names are case-insensitive, so browsers will interpret any uppercase characters as lowercase. That means
when you're using in-DOM templates, camelCased prop names need to use their kebab-cased (hyphen-delimited) equivalents.

## Provide / inject pair

- [Guide](https://v3.vuejs.org/guide/component-provide-inject.html#provide-inject)

Parent components can serve as dependency provider for all its children, regardless how deep the component hierarchy is.

This feature works on two parts: parent component has a `provide` option to provide data and child component has an
`inject` option to start using this data.

In fact, you can think of dependency injection as sort of "long-range props", except:

- parent components don’t need to know which descendants use the properties it provides
- child components don’t need to know where injected properties are coming from

`provide/inject` bindings are not reactive by default. We can change this behavior by passing a `ref` property or
reactive object to provide.

## Child to parent communication

The child component can emit an event on itself by calling the built-in $emit method, passing the name of the event. We
can list emitted events in the component's `emits` option. This will allow you to check all the events that a component
emits and optionally validate them.

## Custom events

- [Guide](https://v3.vuejs.org/guide/component-custom-events.html)

Emitted events can be defined on the component via the `emits` option.

When a native event (e.g., click) is defined in the emits option, the component event will be used instead of a native
event listener.

Similar to prop type validation, an emitted event can be validated if it is defined with the Object syntax instead of
the array syntax.

### v-model arguments

Custom events can also be used to create custom inputs that work with `v-model`. By default, v-model on a component uses
`modelValue` as the prop and `update:modelValue` as the event.

Custom modifiers added to a component `v-model` will be provided to the component via the `modelModifiers` prop.

## Lifecycle Hooks

- [Lifecycle Hooks](https://v3.vuejs.org/api/options-lifecycle-hooks.html#lifecycle-hooks)
- [Lifecycle diagram](https://v3.vuejs.org/images/lifecycle.svg)

All lifecycle hooks are called with their `this` context pointing to the current active instance invoking it.

## Slots

- [Introduction](https://v3.vuejs.org/guide/component-basics.html#content-distribution-with-slots)
- [Guide](https://v3.vuejs.org/guide/component-slots.html)

Vue implements a content distribution API inspired by the Web Components spec draft, using the `<slot>`
element to serve as distribution outlets for content.

When you want to use data inside a slot, that slot has access to the same instance properties (i.e. the same "scope") as
the rest of the template.

The `<slot>` element has a special attribute, name, which can be used to assign a unique ID to different slots so you
can determine where content should be rendered. A `<slot>` outlet without name implicitly has the name "default".

## :is attribute

Dynamically switch between components:

```html
<component :is="currentTabComponent"></component>
```

You can also use the is attribute to create regular HTML elements.
