# Refs

- [Refs and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)
- [Forwarding Refs](https://reactjs.org/docs/forwarding-refs.html)
- [Callback refs](https://reactjs.org/docs/refs-and-the-dom.html#callback-refs)
- [A guide to React refs - blog.logrocket.com](https://blog.logrocket.com/a-guide-to-react-refs/)
- [(Video) ReactJS Tutorial -
  youtube.com](https://www.youtube.com/watch?v=FXa9mMTKOu8&list=PLC3y8-rFHvwgg3vaYJgHGnModB54rxOk3)

Refs provide a way to access DOM nodes or React elements created in the render method.

Refs are escape hatches for React developers, and we should try to avoid using them if possible.

Use cases:

- Focus control: You can achieve focus in an element programmatically by calling `focus()` on the node instance.
- Detects if an element is contained: Modal component could get closed if you click outside of it.
- Integrating with DOM-based non-React libraries.

## Creating refs

- [Documentation](https://reactjs.org/docs/refs-and-the-dom.html#creating-refs)

Refs are created using `React.createRef()` and attached to React elements via the `ref` attribute.

Refs are commonly assigned to an instance property when a component is constructed so they can be referenced throughout
the component.

```jsx
class MyComponent extends React.Component {
  constructor() {
    this.myRef = React.createRef();
  }

  render() {
    return <div ref={this.myRef} />;
  }
}
```

## Accessing refs

- [Documentation](https://reactjs.org/docs/refs-and-the-dom.html#accessing-refs)
- [Adding a Ref to a DOM Element](https://reactjs.org/docs/refs-and-the-dom.html#adding-a-ref-to-a-dom-element)
- [Adding a Ref to a Class Component](https://reactjs.org/docs/refs-and-the-dom.html#adding-a-ref-to-a-class-component)
- [Refs and Function Components](https://reactjs.org/docs/refs-and-the-dom.html#refs-and-function-components)

When a ref is passed to an element in render, a reference to the node becomes accessible at the `current` attribute of
the ref.

```javascript
const node = this.myRef.current;
```

The value of the ref differs depending on the type of the node:

- When the ref attribute is used on an HTML element, the ref created in the constructor with `React.createRef()`
  receives the underlying DOM element as its current property.
- When the ref attribute is used on a custom class component, the ref object receives the mounted instance of the
  component as its current.

You may not use the ref attribute on function components because they don't have instances.

See [Refs and Function Components](https://reactjs.org/docs/refs-and-the-dom.html#refs-and-function-components).

## Forwarding refs

- [Forwarding Refs – React](https://reactjs.org/docs/forwarding-refs.html)
- [(Video) ReactJS Tutorial - youtube.com](https://www.youtube.com/watch?v=RLWniwmfdq4)

Ref forwarding is a technique for automatically passing a ref ("forwarding") through a component to one of its children.
Ref forwarding lets components opt into exposing any child component's ref as their own.

React components hide their implementation details, including their rendered output.

Although such encapsulation is desirable for application-level components like FeedStory or Comment, it can be
inconvenient for highly reusable "leaf" components like FancyButton or MyTextInput.

These components tend to be used throughout the application in a similar manner as a regular DOM button and input, and
accessing their DOM nodes may be unavoidable for managing focus, selection, or animations.

In the example below, FancyButton uses `React.forwardRef` to obtain the ref passed to it, and then forward it to the DOM
button that it renders:

```jsx
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();

<FancyButton ref={ref}>Click me</FancyButton>;
```

This way, components using FancyButton can get a ref to the underlying button DOM node and access it if necessary - just
like if they used a DOM button directly.

## Hooks

### useRef(initialValue)

- [Documentation](https://reactjs.org/docs/hooks-reference.html#useref)

`useRef` returns a mutable ref object whose `current` property is initialized to the passed argument (`initialValue`).

The returned object will persist for the full lifetime of the component.

### useImperativeHandle(ref, createHandle, [deps])

- [Documentation](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)

`useImperativeHandle` customizes the instance value that is exposed to parent components when using ref.

As always, imperative code using refs should be avoided in most cases.
