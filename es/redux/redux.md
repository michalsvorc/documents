# Redux

- [Data flow diagram](https://d33wubrfki0l68.cloudfront.net/01cc198232551a7e180f4e9e327b5ab22d9d14e7/d7584/img/tutorials/essentials/reduxdataflowdiagram.gif)
- [Basic Tutorial: Intro](https://redux.js.org/basics/basic-tutorial)
- [API Reference](https://redux.js.org/api/api-reference)
- [Redux Toolkit](https://redux-toolkit.js.org)
- [Ecosystem](https://redux.js.org/introduction/ecosystem)
- [Reducing Boilerplate](https://redux.js.org/recipes/reducing-boilerplate)

## Further reading

- [Immutable Update Patterns](https://redux.js.org/recipes/structuring-reducers/immutable-update-patterns)
- [Immutability in React and Redux: The Complete Guide](https://daveceddia.com/react-redux-immutability-guide/)
- [Performance and Normalizing Data](https://redux.js.org/tutorials/essentials/part-6-performance-normalization)

## Overview

Redux is a pattern and library for managing and updating application state, using events called **actions**.

Redux manages the state of an app using a single **store**. To modify the state, an action is dispatched to the store
and a **reducer** updates the store based on the type and other values of the action. In order to use the new state, the
store can be subscribed to. Subscribing requires a callback function which is called whenever the store updates.

[Redux Toolkit](https://redux-toolkit.js.org/) is our recommended approach for writing Redux logic. It contains packages
and functions that we think are essential for building a Redux app. Redux Toolkit builds in our suggested best
practices, simplifies most Redux tasks, prevents common mistakes, and makes it easier to write Redux applications.

## Remember

### Redux Toolkit

- configureStore sets up redux-thunk middleware automatically
- createReducer and createSlice allow mutating state directly in reducer (Immer library)
- createSlice is the standard approach for writing Redux logic, it uses
  [createAction](https://redux-toolkit.js.org/api/createAction) and
  [createReducer](https://redux-toolkit.js.org/api/createReducer) internally

## Actions

- [Documentation](https://redux.js.org/basics/actions)

An action is an object that describes how the store should be updated. They are the only source of information for the
store. Actions require a **type** property, which is used by reducers to only update properties for specific actions.

### Action Creators

An action creator is a function that creates and returns an action object. Payload should be passed as creator argument.
This makes them reusable and easy to test.

```javascript
export function addTodo(text) {
  return { type: ADD_TODO, text };
}
```

## Reducers

- [Documentation](https://redux.js.org/basics/reducers)

Reducers specify how the application's state changes in response to [actions](https://redux.js.org/basics/actions) sent
to the store. A reducer takes two arguments, the current state and the action that has been dispatched. The current
state is manipulated and returns a new state based on the action.

```javascript
const reducer = (previousState, action) => newState.
```

See: [Rules of reducers](https://redux.js.org/tutorials/essentials/part-2-app-structure#rules-of-reducers)

### Mutating state inside reducers

You can only write "mutating" logic in Redux Toolkit's **createSlice** and **createReducer** because they use Immer inside.

## Store

- [Documentation](https://redux.js.org/api/store)

A store holds the whole [state tree](https://redux.js.org/understanding/thinking-in-redux/glossary#state) of your application. \

Store methods:

- [getState()](https://redux.js.org/api/store#getstate)
- [dispatch(action)](https://redux.js.org/api/store#dispatchaction)

Store low-level methods:

- [subscribe(listener)](https://redux.js.org/api/store#subscribelistener)
- [replaceReducer(nextReducer)](https://redux.js.org/api/store#replacereducernextreducer)

The Redux store is created using the configureStore function from Redux Toolkit. configureStore requires that we pass in
a reducer argument. When we pass in an object like {counter: counterReducer}, that says that we want to have a
state.counter section of our Redux state object, and that we want the counterReducer function to be in charge of
deciding if and how to update the state.counter section whenever an action is dispatched.

To apply multiple store enhancers, you may use [compose()](https://redux.js.org/api/compose).

### Dispatch

The Redux store has a method called dispatch. The only way to update the state is to call store.dispatch() and pass in
an action object. The store will run its reducer function and save the new state value inside, and we can call
getState() to retrieve the updated value

## Selectors

- [Documentation](https://redux.js.org/tutorials/essentials/part-1-overview-concepts#selectors)

Selectors are functions that know how to extract specific pieces of information from a store state value. A selector is
a function that accepts Redux state as an argument and returns data that is derived from that state.

As an application grows bigger, this can help avoid repeating logic as different parts of the app need to read the same
data. Selectors can provide performance optimizations to your application and can also help you encapsulate your global
state tree. Selector functions are prefixed with _select_ as a convention.

```javascript
const selectCounterValue = state => state.value

const counterValue = selectCounterValue(store.getState())

const selectUserIds = state => state.users.map(user => user.id) \
const userIds = selectUserIds(store.getState())
```

If your application is growing large and unwieldy, you may benefit from creating your own selectors or using a library
such as [Reselect](https://github.com/reduxjs/reselect), which utilizes memoized selectors. See [Reselect
createSelector](https://redux-toolkit.js.org/api/createSelector).

## Slices

- [Documentation](https://redux.js.org/tutorials/essentials/part-2-app-structure#redux-slices)

A "slice" is a collection of Redux **reducer logic** and actions for a single feature in your app,

Slice automatically generates action creators and action types that correspond to the reducers and state.

See:

- [Creating Slice Reducers and
  Actions](https://redux.js.org/tutorials/essentials/part-2-app-structure#creating-slice-reducers-and-actions)
- [createSlice](https://redux-toolkit.js.org/api/createSlice) (Redux-Toolkit).

After creating a slice, we can export action objects from `mySlice.actions` action creator and use them in
dispatch(action).

### combineReducers(reducers)

- [Documentation](https://redux.js.org/api/combinereducers)

A Redux store needs to have a single "root reducer" function passed in when it's created. Redux has a function called
[combineReducers](https://redux.js.org/api/combinereducers) that does this for us automatically. It accepts an object
full of slice reducers as its argument, and returns a function that calls each slice reducer whenever an action is
dispatched.

## Middleware

- [Documentation](https://redux.js.org/advanced/middleware)

### applyMiddleware(...middleware)

- [Documentation](https://redux.js.org/api/applymiddleware)

Middleware enhances the store by enabling you to interact with dispatched actions before they reach the store. Multiple
middleware can be combined together, where each middleware requires no knowledge of what comes before or after it in the
chain.
