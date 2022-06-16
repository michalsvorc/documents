# Optimization

Overview:

* [Optimizing Performance - React](https://reactjs.org/docs/optimizing-performance.html)
* [Profiling - React](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab)

Topics:

* [Improving Rendering Performance -
  isquaredsoftware.com](https://blog.isquaredsoftware.com/2020/05/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior/#improving-rendering-performance)
* [Use React.memo() wisely - dmitripavlutin.com](https://dmitripavlutin.com/use-react-memo-wisely/)
* [When to useMemo and useCallback - kentcdodds.com](https://kentcdodds.com/blog/usememo-and-usecallback/)
* [The Effect of Shallow Equality in React - JavaScript in Plain
  English](https://javascript.plainenglish.io/the-effect-of-shallow-equality-in-react-85ae0287960c)

Libraries:

* [Introducing the React Profiler – React Blog](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html)

## Overview

Rendering a component will, by default, cause all components inside of it (children) to be rendered too. By default,
React does not care whether *props changed* - it will render child components unconditionally just because the parent
rendered. 

That also means there's no point in trying to optimize renders for *host components* withouth children, like a `<div>`
or a `<button>`, by wrapping them up in a `React.memo()`.

There's no child component underneath those basic components, so the rendering process would stop there anyway.

Skipping rendering a component means React will also skip rendering that entire subtree, because it's effectively
putting a stop sign up to halt the default "render children recursively" behavior.

These methods exist only as a performance optimization, do not rely on them to prevent a render, as this can lead to
potential bugs.

Passing new *references* as props will cause the child to render despite optimization techniques.

Optimization comes with a cost. Always use profiling to decide optimization efficiency. Performance-related changes
applied incorrectly can even harm the performance.

## Shallow equality

* [How to Compare Objects in JavaScript -
  dmitripavlutin.com](https://dmitripavlutin.com/how-to-compare-objects-in-javascript/#3-shallow-equality)
* [Object equality diagram - medium.com](https://miro.medium.com/max/1825/1*Yzdvx-DBdojQFiEzCx3dVw.jpeg)

All of these optimization approaches use a comparison technique called *shallow equality*.

During shallow equality check of objects you get the list of properties (using `Object.keys()`) of both objects, then
check the properties' values for equality.

If these properties contain complex data structures, it may produce false-negatives for deeper differences. 

## Class component APIs

Class component is re-rendered whenever:

* state changes
* context changes
* parent re-renders
* props change

### shouldComponentUpdate()

* [Documentation](https://reactjs.org/docs/react-component.html#shouldcomponentupdate)

`React.Component.shouldComponentUpdate(nextProps, nextState)`

An optional class component lifecycle method that will be called early in the render process.

`shouldComponentUpdate()` is invoked before rendering when new props or state are being received. Defaults to true.

If it returns false, React will skip rendering the component.

Consider using the built-in `PureComponent` instead of 

We do not recommend doing deep equality checks or using `JSON.stringify()` in `shouldComponentUpdate()`. It is very
inefficient and will harm performance.

### React.PureComponent

* [Documentation](https://reactjs.org/docs/react-api.html#reactpurecomponent)

To prevent a component from re-rendering because of its parent's re-render, you can declare it as a sub class of
`PureComponent`. 

PureComponent implements shouldComponentUpdate out of the box and should be used instead of writing
`shouldComponentUpdate()` by hand.

It does a shallow comparison of `props` and `state`. If the state and props haven't changed, react doesn't re-render
the component even if the parent re-renders. 

Since the comparison of props and state is the most common way to implement `shouldComponentUpdate()`, the
`PureComponent` base class implements that behavior by default, and should be used instead.

If your React component's `render()` function renders the same result given the same props and state, you can use
`React.PureComponent` for a performance boost in some cases.

## Function components APIs

Unlike `componentDidMount` or `componentDidUpdate`, effects scheduled with `useEffect` don't block the browser from
updating the screen. This makes your app feel more responsive.

`useReducer` lets you optimize performance for components that trigger deep updates because you can pass dispatch
down instead of callbacks.

### React.memo()

* [Documentation](https://reactjs.org/docs/react-api.html#reactmemo)

`React.memo(functionComponent(props))`

`React.memo()` is the functional component equivalent of `React.PureComponent`. It is a higher-order component.

Both function components and class components can be wrapped in `React.memo()`.

The more often the component renders with the same props than with changed props, the heavier and the more
computationally expensive the output is, the more chances are that component needs to be wrapped in `React.memo()`.

When a component is wrapped in `React.memo()`, React renders the component and memoizes the result. Before the next
render, if the new props are the same as the previous one, React reuses the memoized result.

By reusing the memoized result, React skips rendering the component and doesn't perform a virtual DOM difference check.

React.memo() only checks for prop changes. If your function component wrapped in `React.memo()` has a `useState()` or
`useContext` Hook in its implementation, it will still rerender when state or context change. 

`React.memo` is equivalent to PureComponent, but it only compares props. `React.memo` doesn't compare state because
there is no single state object to compare. But you can make children pure too, or even optimize individual children
with [useMemo](https://reactjs.org/docs/hooks-faq.html#how-to-memoize-calculations).

If you always pass *new references* down as props, `React.memo()` will never skip a render, so you may need to memoize
those values.

By default it will only shallowly compare complex objects in the props object. If you want control over the comparison,
you can also provide a custom comparison function as the second argument.

`React.memo()` only checks for prop changes. If your function component wrapped in `React.memo()` has a `useState`,
`useReducer` or `useContext` Hook in its implementation, it will still rerender when state or context change.

When to use `React.memo()` when your component:

* Is pure functional component and given the same props, it always renders the same output.
* Re-renders often with the same props.
* Contains a decent amount of UI elements.

### References as props

Class components don't have to worry about accidentally creating new callback function references as much, because they
can have instance methods that are always the same reference.

React provides two hooks to help you reuse the same references inside function components:

* [useMemo](https://reactjs.org/docs/hooks-reference.html#usememo): For any kind of general data like creating objects
  or doing complex calculations.
* [useCallback](https://reactjs.org/docs/hooks-reference.html#usecallback): For creating callback functions.

### Immutability and state

* [Blog - isquaredsoftware.com](https://blog.isquaredsoftware.com/2020/05/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior/#immutability-and-rerendering)

Optimization techniques rely on shallow equality checks of the current props vs the previous props.

React applies all state updates during the render phase. When React tries to apply a state update from a hook, it checks
to see if the new value is the same reference.

React requires that any hook state updates must pass in or return a new reference as the new state value, whether it
be a new object reference, or a new primitive value.

Note that there is a distinct difference in behavior between the class component `setState()` and the function component
`useState` and `useReducer` hooks with regards to mutations and re-rendering:

`setState()` doesn't care if you mutate the state object or provide the same values. Calling `setState()` will always
lead to a re-render unless `shouldComponentUpdate()` returns false.

React, and the rest of the React ecosystem, assume immutable updates. Any time you mutate, you run the risk of bugs.

## Performance

* [React FAQ](https://reactjs.org/docs/hooks-faq.html#are-hooks-slow-because-of-creating-functions-in-render)

Are Hooks slow because of creating functions in render?

No. In modern browsers, the raw performance of closures compared to classes doesn't differ significantly except in
extreme scenarios.

Traditionally, performance concerns around inline functions in React have been related to how passing new callbacks on
each render breaks shouldComponentUpdate optimizations in child components. Hooks approach this problem from three
sides.

* The `useCallback` Hook lets you keep the same callback reference between re-renders so that `shouldComponentUpdate`
  continues to work.
* The `useMemo` Hook makes it easier to control when individual children update, reducing the need for pure components.
* The `useReducer` Hook reduces the need to pass callbacks deeply, it can pass down a `dispatch` function via context.

## Callbacks and re-rendering

```jsx
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
   <button onClick={() => this.handleClick()}>
     Click me
   </button>
  }
}
```

The problem with this syntax is that a different callback is created each time the `LoggingButton` renders. In most cases, this is fine.

However, if this callback is passed as a prop to lower components, those components might do an extra re-rendering.

You should write the callback as follows:

```jsx
class LoggingButton extends React.Component {
  handleClick = () => {
    console.log('this is:', this);
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
