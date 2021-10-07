# Hooks

Overview:

* [Introducing Hooks - React](https://reactjs.org/docs/hooks-intro.html)
* [Hooks FAQ - React](https://reactjs.org/docs/hooks-faq.html)
* [(Video) 10 React Hooks Explained - youtube.com](https://www.youtube.com/watch?v=TNhaISOUy6Q)
* [(Video) React Today and Tomorrow - youtube.com](https://youtu.be/dpw9EHDh2bM)

APIs:

* [Hooks API Reference - React](https://reactjs.org/docs/hooks-reference.html)

Topics:

* [How do lifecycle methods correspond to Hooks?
  ](https://reactjs.org/docs/hooks-faq.html#how-do-lifecycle-methods-correspond-to-hooks)

Libraries:

* [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)
* [useHooks](https://usehooks.com/)
* [useHooks TypeScript](https://usehooks-typescript.com/)

Examples:

* [Data fetching with Hooks](https://codesandbox.io/s/jvvkoo8pq3)

## Overview

* [Introducing Hooks - React](https://reactjs.org/docs/hooks-intro.html#motivation)

Introduced in React 16.8.0.

Hooks let you use state and other React features from function components without need of class components.

Disadvantages of classes:

* constructor (not really true with public fields)
* complicated this bindings
* duplicate side-effect logic in life cycles
* forced OOP patern

Hooks avoid a lot of the overhead that classes require, like the cost of creating class instances and binding event
handlers in the constructor.

Hooks allow you to reuse stateful logic without changing your component hierarchy. Hooks let you split one component
into smaller functions based on what pieces are related (such as setting up a subscription or fetching data).

Hooks are functions that let you "hook into" React state and lifecycle features from function components. Hooks don't
work inside classes - they let you use React without classes

Hooks let you organize side effects in a component by what pieces are related (such as adding and removing a
subscription), rather than forcing a split based on lifecycle methods.

### Rules

* [Hooks at a Glance - React](https://reactjs.org/docs/hooks-overview.html#rules-of-hooks)
* [Rules of Hooks - React](https://reactjs.org/docs/hooks-rules.html)

* Hook names are always prefixed with `use`.
* Only call Hooks at the top level of your component. Don't call Hooks inside loops, conditions, or nested functions.
* Only call Hooks from React function components. Don't call Hooks from regular JavaScript functions.

### Built-in hooks

Basic Hooks:

* [useState](https://reactjs.org/docs/hooks-reference.html#usestate)
* [useEffect](https://reactjs.org/docs/hooks-reference.html#useeffect)
* [useContext](https://reactjs.org/docs/hooks-reference.html#usecontext)

Additional Hooks:

* [useReducer](https://reactjs.org/docs/hooks-reference.html#usereducer)
* [useCallback](https://reactjs.org/docs/hooks-reference.html#usecallback)
* [useMemo](https://reactjs.org/docs/hooks-reference.html#usememo)
* [useRef](https://reactjs.org/docs/hooks-reference.html#useref)
* [useImperativeHandle](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)
* [useLayoutEffect](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)
* [useDebugValue](https://reactjs.org/docs/hooks-reference.html#usedebugvalue)

### Do Hooks cover all use cases for classes?

* [React FAQ](https://reactjs.org/docs/hooks-faq.html#do-hooks-cover-all-use-cases-for-classes)

There are no Hook equivalents to:

* `getSnapshotBeforeUpdate`
* `getDerivedStateFromError`
* `componentDidCatch`

To implement `shouldComponentUpdate`, you can wrap a function component with `React.memo` to shallowly compare its props.

## useState

* [API](https://reactjs.org/docs/hooks-reference.html#usestate)
* [Documentation](https://reactjs.org/docs/hooks-state.html)

`useState` is a hook that lets you add state to function components.

```js
const [state, setState] = useState(initialState);
```

Returns a stateful value, and a function to update it.

Unlike with classes, the state value doesn't have to be an object. We recommend to split state into multiple state
variables based on which values tend to change together.

Note: If you're doing expensive calculations while rendering, you can optimize them with `useMemo`.

### setState update function

```js
setState(newState);
setState(prevState => {...});
```

The `setState` function is used to update the state.

React guarantees that the `setState` function identity is stable and won't change on re-renders.

If the new state is computed using the previous state, you can pass a function to `setState` to access the previous
state value.

Updating a state variable with new object always replaces it instead of merging it.

You can replicate the class component state merging behavior by combining the function updater form with object spread
or `Object.assign` syntax. This will still trigger re-render because of new object reference.

If your update function returns the exact same value as the current state, the subsequent rerender will be skipped
completely. React uses the `Object.is` comparison algorithm.

Note: `useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or
when the next state depends on the previous one.

### Initial state

* [API](https://reactjs.org/docs/hooks-reference.html#lazy-initial-state)

The `initialState` argument is the state used during the initial render. In subsequent renders, it is disregarded.

If you don't provide initial state the value is `undefined`.

If the initial state is the result of an expensive computation, you may provide a function instead, which will be
executed only on the initial render.

```js
// ! expensiveCalculation() is called on every render
const [rows, setRows] = useState(expensiveCalculation());

//  expensiveCalculation() is called only once
const [rows, setRows] = useState(() => expensiveCalculation());
```

## useEffect

* [API](https://reactjs.org/docs/hooks-reference.html#useeffect)
* [Documentation](https://reactjs.org/docs/hooks-effect.html)

Adds the ability to perform side effects from a function component after every completed render.

```js
useEffect(() => {
  // perform side effects

  // optionally return a cleanup function
  return () => {};
}, [...dependencies]);
```

You can think of useEffect Hook as `componentDidMount`,` componentDidUpdate`, and `componentWillUnmount` combined.

Instead of thinking in terms of mounting and updating, you might find it easier to think that effects happen "after
render". React guarantees the DOM has been updated by the time it runs the effects.

The anonymous function passed as an argument to `useEffect` is going to be different on every render. This is
intentional, as it lets us read the count value from inside the effect without worrying about it getting stale.

You can use several effects, this lets us separate unrelated logic into different effects. React will apply every effect
used by the component, in the order they were specified.

### Timing

Although the `useEffect` is deferred until after the browser has been painted, it's guaranteed to fire before any new
renders. React will always flush previous render effects before starting a new update.

Unlike `componentDidMount` or `componentDidUpdate`, effects scheduled with `useEffect` don't block the browser from
updating the screen. This makes your app feel more responsive.

The majority of effects don't need to happen synchronously. In the uncommon cases where they do (such as measuring the
layout), there is a separate `useLayoutEffect` hook.

### Cleanup function

Every effect may return a function that cleans up after it.

The optional returned clean-up function runs before the component is removed from the UI to prevent memory leaks.

For example, we might want to unsubscribe from some external data source or stop timers.

React performs the cleanup when the component unmounts. However, effects run for every render and not just once. This is
why React also cleans up effects from the previous render before running the effects next time. This is the default
behaviour.

In some cases, cleaning up or applying the effect after every render might create a performance problem.

You can tell React to skip applying an effect if certain values haven't changed between re-renders. To do so, pass
dependencies array as an optional second argument.

### Dependencies array

* [Conditionally firing an effect - React](https://reactjs.org/docs/hooks-reference.html#conditionally-firing-an-effect)
* [Optimizing Performance by Skipping Effects - React](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects)

The default behavior for effects is to fire the effect after the first render and after every completed render. That way
an effect is always recreated if one of its dependencies changes.

Pass a second argument to `useEffect` that is the array of values that the effect depends on. 

If you use this optimization, make sure the array includes all values from the component scope (such as `props` and
`state`) that change over time and that are used by the effect. Otherwise, your code will reference stale values from
previous renders.

If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array (`[]`) as a
second argument. This tells React that your effect doesn't depend on any values from props or state, so it never needs
to re-run.

### FAQ

* Is it safe to omit functions from the list of dependencies? [React
  FAQ](https://reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies)

  Generally speaking, no. Usually you'll want to declare functions needed by an effect inside of it.

* What can I do if my effect dependencies change too often? [React FAQ](https://reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often)

Sometimes, your effect may be using state that changes too often. To fix this, we can use the functional update form of
setState. It lets us specify how the state needs to change without referencing the current state.

In more complex cases (such as if one state depends on another state), try moving the state update logic outside the
effect with the useReducer Hook.

* Can I run an effect only on updates? [React FAQ](https://reactjs.org/docs/hooks-faq.html#can-i-run-an-effect-only-on-updates)

This is a rare use case. If you need it, you can use a mutable ref to manually store a boolean value corresponding to
whether you are on the first or a subsequent render, then check that flag in your effect. (If you find yourself doing
this often, you could create a custom Hook for it.)

* How to get the previous props or state? [React FAQ](https://reactjs.org/docs/hooks-faq.html#how-to-get-the-previous-props-or-state)

Currently, you can do it manually with a ref. This might be a bit convoluted but you can extract it into a custom Hook.

```js
function usePrevious(value) {
  const ref = useRef();

  useEffect(() => {
    ref.current = value;
  });

  return ref.current;
}
```
Note how this would work for props, state, or any other calculated value.

## useReducer

* [API](https://reactjs.org/docs/hooks-reference.html#usereducer)

An alternative to `useState`, similar to Redux dispatch actions.

```js
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

Accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a dispatch method. 

`useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or
when the next state depends on the previous one.

If you return the same value from a Reducer Hook as the current state, React will bail out without rendering the
children or firing effects. This is the same behavior as `useState` hook.

Note: If you're doing expensive calculations while rendering, you can optimize them with `useMemo`.

### Specifying the initial state

There are two different ways to initialize useReducer state: through `initialArg` or lazy initialization.

The simplest way is to pass the initial state as a second argument:

```js
const [state, dispatch] = useReducer(
    reducer,
    {count: initialCount}
);
```

You can also create the initial state [lazily](https://reactjs.org/docs/hooks-reference.html#lazy-initialization). To do
this, you can pass an `init` function as the third argument. The initial state will be set to `init(initialArg)`.

It lets you extract the logic for calculating the initial state outside the reducer. This is also handy for resetting
the state later in response to an action.

```js
const initialCount = 0

// outside the reducer
function init(initialCount) { return {count: initialCount} }

// inside of a function component
const [state, dispatch] = useReducer(reducer, initialCount, init);
```

### Pass dispatch down instead of callbacks

* [React FAQ](https://reactjs.org/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down)

`useReducer` lets you optimize performance for components that trigger deep updates because you can pass `dispatch` down
instead of callbacks.

In large component trees, it's possible to pass down a `dispatch` function from useReducer via context. Note that you
can still choose whether to pass the application state down as props (more explicit) or as context (more convenient for
very deep updates).

React guarantees that the `dispatch` function identity is stable and won't change on re-renders, so components that read
it don't need to re-render.

This is why it's also safe to omit from the `useEffect` or `useCallback` dependency list.

## useCallback

* [Hooks API Reference – React](https://reactjs.org/docs/hooks-reference.html#usecallback)
* [(Video) useCallback Hook - youtube.com ](https://www.youtube.com/watch?v=IL82CzlaCys)

Returns a memoized version of the passed callback that only changes if one of the dependencies has changed. 

```js
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

It is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary
re-renders.

When to use `useCallback`:

1. A functional component wrapped inside `React.memo()` accepts a function as a prop.
2. When the function object is a dependency to other hooks, e.g. in `useEffect`.
3. When the function has some internal state.

Note: `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.

## useMemo

* [API](https://reactjs.org/docs/hooks-reference.html#usememo)
* [React FAQ](https://reactjs.org/docs/hooks-faq.html#how-to-memoize-calculations)
* [(Video) useMemo Hook - youtube.com](https://www.youtube.com/watch?v=qySZIzZvZOY)

The `useMemo` Hook lets you cache calculations between multiple renders by remembering the previous computation.

This optimization helps to avoid expensive calculations on every render if the dependencies are the same.

```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

This code calls `computeExpensiveValue(a, b)`. But if the dependencies `[a, b]` haven't changed since the last value,
`useMemo` skips calling it a second time and simply reuses the last value it returned.

Remember that the function passed to `useMemo` runs during rendering. Don't do anything there that you wouldn't normally
do while rendering. For example, side effects belong in `useEffect`, not `useMemo`.

`useMemo` serves only as a hint, and doesn't guarantee the computation won't re-run.

You may rely on `useMemo` as a performance optimization, not as a semantic guarantee. Write your code so that it still
works without `useMemo` - and then add it to optimize performance.

Note: `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.

## useContext

* [API](https://reactjs.org/docs/hooks-reference.html#usecontext)

```js
const value = useContext(MyContext);
```

Accepts a context object (the value returned from `React.createContext`) and returns the current context value.

The current context value is determined by the value prop of the nearest context provider above the calling component in
the tree.

A component calling `useContext` will always re-render when the context value changes.

## useRef

* [API](https://reactjs.org/docs/hooks-reference.html#useref)
* [(Video) useRef Hook Part 1 (DOM) - youtube.com](https://www.youtube.com/watch?v=yCS2m01bQ6w)
* [(Video) useRef Hook Part 2 (Values) - youtube.com](https://www.youtube.com/watch?v=LWg0OyZQffc)

The `ref` object is a generic container whose current property is mutable and can hold any value, similar to an instance
property on a class.

```js
const refContainer = useRef(initialValue);
```

`useRef` returns a mutable JavaScript object whose `current` property is initialized to the passed argument
(`initialValue`). The returned object will persist for the full lifetime of the component and will give you the same ref
object on every render.

Mutating the `current` property doesn't cause a re-render.

You might be familiar with refs primarily as a way to access the DOM. However, `useRef()` is useful for more than the
ref attribute.

It's handy for keeping any mutable value around similar to how you'd use instance fields in classes.

Avoid setting refs during rendering - this can lead to surprising behavior. Instead, typically you want to modify refs
in event handlers and effects.

### Avoid re-creating the useRef() initial value

For example, maybe you want to ensure some imperative class instance only gets created once:

```js
// ! imperativeClass is created on every render
const ref = useRef(new imperativeClass());

---

const ref = useRef(null);

// imperativeClass is created lazily once
function getImperativeInstance() {
  if (ref.current === null) {
    ref.current = new imperativeClass(onIntersect);
  }
  return ref.current;
}
```

## useImperativeHandle

* [API](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)
* [(Video) useImperativeHandle Hook - youtube.com](https://youtu.be/N8PwptJ6Qlk)

```js
useImperativeHandle(ref, createHandle, [deps])
```

`useImperativeHandle` customizes the instance value that is exposed to parent components when using ref. This way, it
allows us to access methods from within a function component.

You can use to use this hook to create an API for your component.

As always, imperative code using refs should be avoided in most cases. `useImperativeHandle` should be used with
`forwardRef`.

## useLayoutEffect

* [API](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)

The signature is identical to `useEffect`, but it fires synchronously after all DOM mutations. Use this to read layout
from the DOM and synchronously re-render. 

Your callback will run after rendering the component, but before the actual updates have been painted to the screen.
This means it will *block visual updates* until your callback has finished running.

Prefer the standard `useEffect` when possible to *avoid* blocking visual updates.

## useDebugValue

* [API](https://reactjs.org/docs/hooks-reference.html#usedebugvalue)

```js
useDebugValue(value)
```

`useDebugValue` can be used to display a label for custom hooks in React DevTools.

## Custom Hooks

* [Building Your Own Hooks - React](https://reactjs.org/docs/hooks-custom.html)

Examples:

* [(Video) useDocumentTitle Custom Hook - youtube.com](https://www.youtube.com/watch?v=4yp6T-hF5ZY)
* [(Video) useCounter Custom Hook - youtube.com](https://www.youtube.com/watch?v=W3_GIiN-nuc)
* [(Video) useInput Custom Hook - youtube.com](https://www.youtube.com/watch?v=6am-yn3ZLEw)

Unlike a React component, a custom Hook doesn't need to have a specific signature. Custom Hooks are a convention that
naturally follows from the design and rules of Hooks, rather than a React feature.

A custom Hook is a JavaScript function whose name starts with "use" and that may call other Hooks.

We can decide what it takes as arguments, and what, if anything, it should return.

Custom Hooks are a mechanism to reuse stateful logic (such as setting up a subscription and remembering the current
value), but every time you use a custom Hook, all state and effects inside of it are fully isolated.

