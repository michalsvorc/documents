# Vue.js v2 Components

- [Components Basics](https://v2.vuejs.org/v2/guide/components.html)
- [Components Registration](https://v2.vuejs.org/v2/guide/components-registration.html)
- [v-for with a Component](https://v2.vuejs.org/v2/guide/list.html#v-for-with-a-Component)
- [Handling Edge Cases](https://v2.vuejs.org/v2/guide/components-edge-cases.html)

Components are reusable Vue instances with a name. Each time you use a component, a new instance of it is created.

Components have isolated scopes of their own.

## Component registration

- [Guide](https://v2.vuejs.org/v2/guide/components-registration.html)
- [Global registration](https://v2.vuejs.org/v2/guide/components-registration.html#Global-Registration)
- [Local registration](https://v2.vuejs.org/v2/guide/components-registration.html#Local-Registration)
- [Module systems](https://v2.vuejs.org/v2/guide/components-registration.html#Module-Systems)


## Child to Parent communication

- [Guide](https://v2.vuejs.org/v2/guide/components.html#Listening-to-Child-Components-Events)
  - [Emitting a Value With an Event](https://v2.vuejs.org/v2/guide/components.html#Emitting-a-Value-With-an-Event)
  - [Using v-model on Components](https://v2.vuejs.org/v2/guide/components.html#Using-v-model-on-Components)
- [Custom events](https://v2.vuejs.org/v2/guide/components-custom-events.html)

Use custom events for Child to Parent communication. The child component can emit an event on itself by calling the
built-in `$emit` method, passing the name of the event and a second parameter to emit a custom value.

Then when we listen to the event in the parent, we can access the emitted event’s value with `$event`.

Custom events can also be used to create custom inputs that work with `v-model`.

## Dynamic components

- [Dynamic & Async Components](https://v2.vuejs.org/v2/guide/components-dynamic-async.html)
- [Components Guide](https://v2.vuejs.org/v2/guide/components.html#Dynamic-Components)

To dynamically switch between components use Vue’s `<component>` element with the `is` special attribute.

```html
<!-- Component changes when currentTabComponent changes -->
<component v-bind:is="currentTabComponent"></component>
```

In the example above, currentTabComponent can contain either:

- the name of a registered component, or
- a component’s options object

To avoid re-rendering and losing component state, we can wrap our dynamic component with a `<keep-alive>` element.

## Async Components

- [Dynamic & Async Components](https://v2.vuejs.org/v2/guide/components-dynamic-async.html#Async-Components)

Vue allows you to define your component as a factory function that asynchronously resolves your component definition.
Vue will only trigger the factory function when the component needs to be rendered and will cache the result for future
re-renders.

You can also return a Promise in the factory function, so with Webpack 2 and ES2015 syntax you can make use of dynamic
imports.

## Customizing Component v-model

- [Guide](https://v2.vuejs.org/v2/guide/components-custom-events.html#Customizing-Component-v-model)
- [Guide latest](https://vuejs.org/guide/components/v-model.html)

By default, `v-model` on a component uses `value` as the prop and `input` as the event, but some input types such as
checkboxes and radio buttons may want to use the `value` attribute for a different purpose. Using the `model` option can
avoid a conflict in such cases.

## Slots

- [Content Distribution with Slots](https://v2.vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots)

In 2.6.0, we introduced a new unified syntax (the `v-slot` directive) for named and scoped slots. It replaces the `slot`
and `slot-scope` attributes, which are now deprecated, but have not been removed

Vue implements a content distribution API inspired by the Web Components spec draft, using the `<slot>` element to serve
as distribution outlets for content.

## .sync modifier

- [Guide](https://v2.vuejs.org/v2/guide/components-custom-events.html#sync-Modifier)
- [Codepen](https://codepen.io/mahendranKannan/pen/VxXzJB?editors=1010)

In some cases, we may need “two-way binding” for a prop. We recommend emitting events in the pattern of `update:myPropName`.

For convenience, we offer a shorthand for this pattern with the `.sync` modifier.

The `.sync` modifier can also be used with v-bind when using an object to set multiple props at once.
