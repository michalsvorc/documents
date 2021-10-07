# Remember

React uses the `Object.is` comparison algorithm.

## Props

If you pass no value for a prop, it defaults to `true`. In general, we don't recommend not passing a value for a prop.

[defaultProps](https://reactjs.org/docs/typechecking-with-proptypes.html#default-prop-values) will eventually be [deprecated](https://twitter.com/hswolff/status/1133759319571345408).

## Rendering

React will double-render components in strict mode in development.

Render lists inside a standalone component.

Try to use [render props](https://reactjs.org/docs/render-props.html) technique instead of HOC.

## State in class components

State value in class components must be a single object. Function component might have multiple state values, which
could be objects or primitives.

You may optionally pass an update state object as the first argument to `setState()` instead of an update function. This
performs a shallow object merge of changes into the state. Don't calculate new state from previous one with this method,
use the update function argument instead.

## State updates in class vs function componenets

Rendering:

* Calling `setState()` triggers re-render even when you pass the same state object. 
* When you update `useState` and `useReducer` hooks to the same value as the current state, React will bail out without
  rendering the children or firing effects. 

Merging update objects:

* `setState` automatically merges update object.
* `useState` and `useReducer` does not automatically merge update object.
