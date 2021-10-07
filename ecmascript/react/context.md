# Context

* [Documentation](https://reactjs.org/docs/context.html)
* [Caveats](https://reactjs.org/docs/context.html#caveats)
* [Examples](https://reactjs.org/docs/context.html#examples)
* [Context and Rendering Behavior - React
  Blog](https://blog.isquaredsoftware.com/2020/05/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior/#context-and-rendering-behavior)

React's Context API is a mechanism for making a single user-provided value available to a subtree of components. 

Context is not a "state management" tool. You have to manage the values that are passed into context yourself. This is
typically done by keeping data in React component state, and constructing context values based on that data.

Use context when:

* You just need to pass some simple values that don't change often.
* You have some state or functions that need to be accessed through part of the app, and you don't want to pass them as
  props all the way down.
* You want to stick with what's built in to React and not add additional libraries.

## React.createContext

* [Documentation](https://reactjs.org/docs/context.html#reactcreatecontext)
* [displayName](https://reactjs.org/docs/context.html#contextdisplayname)

```jsx
const MyContext = React.createContext(defaultValue);

MyContext.displayName = 'MyDisplayName';
```

Creates a Context object. When React renders a component that subscribes to this Context object it will read the current
context value from the closest matching `Context.Provider` above it in the tree.

The `defaultValue` argument is only used when a component does not have a matching `Context.Provider` above it in the
tree. This default value can be helpful for testing components in isolation without wrapping them.

Context object accepts a `displayName` string property. React DevTools uses this string to determine what to display for
the context.

## Context.Provider

* [Documentation](https://reactjs.org/docs/context.html#contextprovider)

```jsx
const MyContext = React.createContext(defaultValue);

<MyContext.Provider value={value}>
   <App/>
</MyContext.Provider>
```

The Provider component accepts a value prop to be passed to consuming components that are descendants of this Provider.
One Provider can be connected to many consumers. Providers can be nested to override values deeper within the tree.

## Consumers

Consumers accept a context object.

Consumers can be created as:

* Class component: [Class.contextType](https://reactjs.org/docs/context.html#classcontexttype)
* React component: [Context.Consumer](https://reactjs.org/docs/context.html#contextconsumer)
* Function component (hook): [useContext](https://reactjs.org/docs/hooks-reference.html#usecontext)

###  Class.contextType (Class component)

* [Documentation](https://reactjs.org/docs/context.html#classcontexttype)

```jsx
class MyClass extends React.Component {
  static contextType = MyContext;

  render() {
    let value = this.context;

    /* render something based on the value of MyContext */
  }
}
```

You can only subscribe to a single context using this API. If you need to read more than one see [Consuming Multiple
Contexts](https://reactjs.org/docs/context.html#consuming-multiple-contexts).

### Context.Consumer (React component)

* [Documentation](https://reactjs.org/docs/context.html#contextconsumer)

A React component that subscribes to context changes. Using this component lets you subscribe to a context within a
function component.

Requires a [function as a child](https://reactjs.org/docs/render-props.html#using-props-other-than-render). 

```jsx
<MyContext.Consumer>
  { value => /* render something based on the context value */ }
</MyContext.Consumer>
```

### useContext hook (Function component)

* [Documentation](https://reactjs.org/docs/hooks-reference.html#usecontext)

```jsx
const {value} = useContext(MyContext);
```

## Rendering

Context uses reference identity to determine when to re-render. When a context provider has a new value, every nested
component that consumes that context will be forced to re-render.

Changes to the context object are determined by comparing the new and old values using the same algorithm as [Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#Description).

Note that from React's perspective, each context provider only has a single value - doesn't matter whether that's an
object, array, or a primitive, it's just one context value. Currently, there is no way for a component that consumes a
context to skip updates caused by new context values, even if it only cares about part of a new value in the context
object.

Remember:

* Calling `setState()` in the class component queues a render of that component.
* React recursively renders nested components by default.
* Context providers are given a value by the component that renders them.
* That value normally comes from that parent *component's state*.

This means that by default, any state update to a parent component that renders a context provider will cause all of
its descendants to re-render anyway, regardless of whether they read the context value or not!.

React component right under your context provider should probably use `React.memo`. That way, state updates in the
parent component will not force every component to re-render, just the sections where the context is read. 

The propagation from `Context.Provider` to its descendant consumers is not subject to the `shouldComponentUpdate()`
method, so the consumer is updated even when an ancestor component skips an update. 

### Using objects

* [Caveats](https://reactjs.org/docs/context.html#caveats)

Because context uses reference identity to determine when to re-render, there are some gotchas that could trigger
unintentional renders in consumers when a provider's parent re-renders.

This code below will re-render all consumers every time the Provider re-renders because a new object is always created
for value due to the reference identity:

```jsx
<MyContext.Provider value={{something: 'something'}}>
```

To get around this, lift the value into the parent's state:

```jsx
<MyContext.Provider value={this.state.something}>
```

## Updating Context from a Nested Component

* [Documentation](https://reactjs.org/docs/context.html#updating-context-from-a-nested-component)

Pass a function down through the context object to allow consumers to update the context:

```jsx
export const ThemeContext = React.createContext({
  theme: themes.dark,
  toggleTheme: () => {},
});
```

Make sure the shape of the default value passed to `createContext` matches the shape that the consumers expect.

