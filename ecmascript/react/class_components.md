# Class based components

Overview:

* [React.Component](https://reactjs.org/docs/react-component.html)
* [React.Component lifecycle](https://reactjs.org/docs/react-component.html#the-component-lifecycle)

React components can be defined by subclassing `React.Component` or `React.PureComponent`.

APis:

* [React.Component](https://reactjs.org/docs/react-api.html#reactcomponent)
* [React.PureComponent](https://reactjs.org/docs/react-api.html#reactpurecomponent)

Topics:

* [Bind a function to a component instance - React FAQ](https://reactjs.org/docs/faq-functions.html)

Minimal example:

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## render()

* [Documentation](https://reactjs.org/docs/react-component.html#render)

* The only method you must define in a `React.Component` subclass. 
* The `render()` function should be pure.
* By default, when your component's state or props change, your component will re-render.
* `render()` will not be invoked if `shouldComponentUpdate()` returns false.

## constructor(props)

* [Documentation](https://reactjs.org/docs/react-component.html#constructor)
* [Public class fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields)

Constructors in class components are mainly used for two purposes:

* Initializing [local state](https://reactjs.org/docs/state-and-lifecycle.html) by assigning an object to `this.state`.
* Binding [event handler](https://reactjs.org/docs/handling-events.html) methods to an instance.

With introduction of public class fields, you can now omit the constructor completely:

```jsx
class classComponent extends React.Component {
  state = { a: 1 }; // initialize local state

  handleClick = () => { 
    console.log("a", this.state.a) // bind event handler
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

### Props inside the constructor

You can use `this.props` withouth the contructor because React sets `props` on the instance from the outside.

If you do want to use `this.props` inside the constructor, you need to pass `props` to `super`.

```jsx
class classComponent extends React.Component {
  constructor(props) {
    super(props)
    // Do something with this.props inise the constructor
  }
}
```

## setState(updater, [callback])

* [State and Lifecycle - React](https://reactjs.org/docs/state-and-lifecycle.html#using-state-correctly)
* [Component state - React FAQ](https://reactjs.org/docs/faq-state.html)
* [setState - React](https://reactjs.org/docs/react-component.html#setstate)

`setState()` schedules an update to a component's state object.

Calling `setState()` will always lead to a re-render unless `shouldComponentUpdate()` returns false. 
`setState()` doesn't care if you mutate the state object or provide the same values.

State updates are merged: When you call `setState()`, React merges the object you provide into the current state. The
merging is shallow.

* Object argument:

```jsx
this.setState({...});
```

* Function argument:

```jsx
this.setState((state, props) => ({
  ...
}));
```

### Asynchronicity

`setState()` does not always immediately update the component, state updates may be asynchronous.

React may batch multiple `setState()` calls into a single update for performance.

Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating
the next state.

To perform a task after state update, use `componentDidUpdate()` or a `setState()` function callback argument, either of
which are guaranteed to fire *after* the update has been applied.

Correct implementation of calculating next state from current state:

```js
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

Incorrect implementation:

```js
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

## Component lifecycle

* [Documentation](https://reactjs.org/docs/react-component.html)

Methods marked `*` are not recommended to use.

### Mounting

These methods are called in the following order when an instance of a component is being created and inserted into the
DOM:

* `constructor()`
* `static getDerivedStateFromProps()`
* `render()`
* `componentDidMount()`

### Updating

An update can be caused by changes to props or state. These methods are called in the following order when a component
is being re-rendered:

* `static getDerivedStateFromProps()`
* `shouldComponentUpdate()`
* `render()`
* `getSnapshotBeforeUpdate()`
* `componentDidUpdate()`

### Unmounting

This method is called when a component is being removed from the DOM:

* `componentWillUnmount()`

### Error Handling

These methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any
child component.

* static getDerivedStateFromError()
* componentDidCatch()

## Lifecycle methods

* [Documentation](https://reactjs.org/docs/glossary.html#lifecycle-methods)

Lifecycle methods are custom functionality that gets executed during the different phases of a component.

### componentDidMount()

* [Documentation](https://reactjs.org/docs/react-component.html#componentdidmount)

`componentDidMount()` is invoked immediately after a component is mounted (inserted into the tree). This method is a good
place to set up any subscriptions. If you do that, don't forget to unsubscribe in `componentWillUnmount()`.

### componentDidUpdate(prevProps, prevState, snapshot)

* [Documentation](https://reactjs.org/docs/react-component.html#componentdidupdate)

`componentDidUpdate()` is invoked immediately after updating occurs. This method is not called for the initial render.

You may call `setState()` immediately in `componentDidUpdate()` but note that it must be wrapped in a condition, or
you'll cause an infinite loop. 

`componentDidUpdate()` will not be invoked if `shouldComponentUpdate()` returns false.

### componentWillUnmount()

* [Documentation](https://reactjs.org/docs/react-component.html#componentwillunmount)

`componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed. Perform any necessary
cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that
were created in `componentDidMount()`.

You should not call `setState()` in `componentWillUnmount()` because the component will never be re-rendered.

## Other methods

### static getDerivedStateFromProps(props, state)

* [Documentation](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)

`getDerivedStateFromProps` is invoked right before calling the render method, both on the initial mount and on subsequent
updates.

This method exists for rare use cases where the state depends on changes in props over time.

Deriving state leads to verbose code and makes your components difficult to think about.

### shouldComponentUpdate(nextProps, nextState)

* [Documentation](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)

`shouldComponentUpdate()` is invoked before rendering when new props or state are being received.

Defaults to true.

This method only exists as a performance optimization. Do not rely on it to "prevent" a rendering, as this can lead to
bugs.

Consider using the built-in `PureComponent` class instead.

### getSnapshotBeforeUpdate(prevProps, prevState)

* [Documentation](https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)

`getSnapshotBeforeUpdate()` is invoked right before the most recently rendered output is committed to e.g. the DOM. It
enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed.

This use case is not common, but it may occur in UIs like a chat thread that need to handle scroll position in a special
way.

### component.forceUpdate(callback)

* [Documentation](https://reactjs.org/docs/react-component.html#forceupdate)

Calling `forceUpdate()` will cause `render()` to be called on the component, skipping `shouldComponentUpdate()`.

Normally you should try to avoid all uses of this method.

## Class properties

* [defaultProps](https://reactjs.org/docs/react-component.html#defaultprops)

`defaultProps` can be defined as a property on the component class itself, to set the default props for the class. This
is used for undefined props, but not for null props. 

* [displayName](https://reactjs.org/docs/react-component.html#displayname)

The `displayName` string is used in debugging messages. 

