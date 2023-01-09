# Vue.js v2 Components

- [Components Basics](https://v2.vuejs.org/v2/guide/components.html)
- [Components Registration](https://v2.vuejs.org/v2/guide/components-registration.html)
- [DOM Template Parsing Caveats](https://v2.vuejs.org/v2/guide/components.html#DOM-Template-Parsing-Caveats)
- [Handling Edge Cases](https://v2.vuejs.org/v2/guide/components-edge-cases.html)

Components are reusable Vue instances with a name. Each time you use a component, a new instance of it is created.

## Props

- [Guide](https://v2.vuejs.org/v2/guide/components-props.html)
- [Prop Validation](https://v2.vuejs.org/v2/guide/components-props.html#Prop-Validation)
- [Type Checks](https://v2.vuejs.org/v2/guide/components-props.html#Type-Checks)
- [Non Prop Attributes](https://v2.vuejs.org/v2/guide/components-props.html#Non-Prop-Attributes)

Props are custom attributes you can register on a component. When a value is passed to a prop attribute, it becomes a property on that component instance.

All props form a one-way-down binding between the child property and the parent one. Note that objects and arrays in JavaScript are passed by reference,
so if the prop is an array or object, mutating the object or array itself inside the child component will affect parent state.

We need `v-bind` to tell Vue that prop is a JavaScript expression rather than a string, for example when we're passing
numbers, booleans, or non-primitive types.

## Child to Parent communication

- [Guide](https://v2.vuejs.org/v2/guide/components.html#Listening-to-Child-Components-Events)
- [Custom events](https://v2.vuejs.org/v2/guide/components-custom-events.html)

- The parent can choose to listen to any event on the child component instance with `v-on`, just as we would with a native DOM event.
- The child component can emit an event on itself by calling the built-in `$emit` method.
- Then when we listen to the event in the parent, we can access the emitted event’s value with `$event`. If the event handler is a method,
  then the value will be passed as the first parameter of that method.
- Custom events can also be used to create custom inputs that work with `v-model`.

## Dynamic components

- [Guide](https://v2.vuejs.org/v2/guide/components.html#Dynamic-Components)
- [Dynamic & Async Components](https://v2.vuejs.org/v2/guide/components-dynamic-async.html)

To dynamically switch between components use Vue’s `<component>` element with the `is` special attribute.

To avoid re-rendering and losing component state, we can wrap our dynamic component with a `<keep-alive>` element.

## Async Components

- [Dynamic & Async Components](https://v2.vuejs.org/v2/guide/components-dynamic-async.html#Async-Components)

Vue allows you to define your component as a factory function that asynchronously resolves your component definition.
Vue will only trigger the factory function when the component needs to be rendered and will cache the result for future
re-renders.

## Slots

- [Content Distribution with Slots](https://v2.vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots)
- [Compilation Scope](https://v2.vuejs.org/v2/guide/components-slots.html#Compilation-Scope)

Vue implements a content distribution API inspired by the Web Components spec draft, using the `<slot>` element to serve
as distribution outlets for content.

In 2.6.0, we introduced a new unified syntax (the `v-slot` directive) for named and scoped slots. It replaces the `slot`
and `slot-scope` attributes, which are now deprecated, but have not been removed.
