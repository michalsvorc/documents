# Components

- [Components basics](https://vuejs.org/v2/guide/components.html)
- [v-for with a Component](https://vuejs.org/v2/guide/list.html#v-for-with-a-Component)
- [Handling Edge Cases](https://vuejs.org/v2/guide/components-edge-cases.html)

Components are reusable Vue instances with a name. Each time you use a component, a new instance of it is created.

## Component registration

- [Guide](https://vuejs.org/v2/guide/components-registration.html)

There are two types of component registration: global and local. 

### Global registration

- [Guide](https://vuejs.org/v2/guide/components-registration.html#Global-Registration)

```js
Vue.component('my-component-name', {
  // ... options ...
})
```

These components are globally registered. That means they can be used in the template of any root Vue instance (new Vue)
created after registration. This even applies to all subcomponents, meaning all three of these components will also be
available inside each other.

### Local registration

- [Guide](https://vuejs.org/v2/guide/components-registration.html#Local-Registration)

Global registration often isn’t ideal. For example, if you’re using a build system like Webpack, globally registering
all components means that even if you stop using a component, it could still be included in your final build.

Note that locally registered components are not also available in subcomponents.

You can define your components as plain JavaScript objects, then define the components you’d like to use in a
`components` option.

```js
new Vue({
  el: '#app',
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```

### Module Systems

- [Guide](https://vuejs.org/v2/guide/components-registration.html#Module-Systems)

For local registration, you’ll need to import each component you’d like to use, before you locally register it. 

## Child to Parent communication

- [Guide](https://vuejs.org/v2/guide/components.html#Listening-to-Child-Components-Events)
  - [Emitting a Value With an Event](https://vuejs.org/v2/guide/components.html#Emitting-a-Value-With-an-Event)
  - [Using v-model on Components](https://vuejs.org/v2/guide/components.html#Using-v-model-on-Components)
- [Custom events](https://vuejs.org/v2/guide/components-custom-events.html)

Use custom events for Child to Parent communication. The child component can emit an event on itself by calling the
built-in `$emit` method, passing the name of the event and a second parameter to emit a custom value.

Then when we listen to the event in the parent, we can access the emitted event’s value with `$event`.

Custom events can also be used to create custom inputs that work with `v-model`.

## Dynamic components

- [Dynamic & Async Components](https://vuejs.org/v2/guide/components-dynamic-async.html)
- [Components Guide](https://vuejs.org/v2/guide/components.html#Dynamic-Components)

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

- [Dynamic & Async Components](https://vuejs.org/v2/guide/components-dynamic-async.html#Async-Components)

Vue allows you to define your component as a factory function that asynchronously resolves your component definition.
Vue will only trigger the factory function when the component needs to be rendered and will cache the result for future
re-renders.

You can also return a Promise in the factory function, so with Webpack 2 and ES2015 syntax you can make use of dynamic
imports.

## Customizing Component v-model

- [Guide](https://vuejs.org/v2/guide/components-custom-events.html#Customizing-Component-v-model)

By default, `v-model` on a component uses `value` as the prop and `input` as the event, but some input types such as
checkboxes and radio buttons may want to use the `value` attribute for a different purpose. Using the `model` option can
avoid a conflict in such cases.

## Slots

- [Content Distribution with Slots](https://vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots)

In 2.6.0, we introduced a new unified syntax (the `v-slot` directive) for named and scoped slots. It replaces the `slot`
and `slot-scope` attributes, which are now deprecated, but have not been removed

Vue implements a content distribution API inspired by the Web Components spec draft, using the `<slot>` element to serve
as distribution outlets for content.
