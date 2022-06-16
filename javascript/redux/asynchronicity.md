# Asynchronicity

- [Async Actions](https://redux.js.org/advanced/async-actions)
- [Redux Essentials, Part 5: Async Logic and Data Fetching](https://redux.js.org/tutorials/essentials/part-5-async-logic)

## Async Logic

By itself, a Redux store doesn't know anything about async logic. It only knows how to synchronously dispatch actions,
update the state by calling the root reducer function, and notify the UI that something has changed. Any asynchronicity
has to happen outside the store.

### Using Middleware to Enable Async Logic

- [Documentation](https://redux.js.org/tutorials/essentials/part-5-async-logic#using-middleware-to-enable-async-logic)

The most common async middleware is [redux-thunk](https://github.com/reduxjs/redux-thunk), which lets you write plain
functions that may contain async logic directly. Fortunately, Redux Toolkit's `configureStore` function already sets
that up for us automatically.

### Thunk functions

- [Documentation](https://redux.js.org/tutorials/essentials/part-5-async-logic#thunk-functions)

A thunk is a specific kind of Redux function that can contain asynchronous logic.

Once the thunk middleware has been added to the Redux store, it allows you to pass thunk functions directly to
store.dispatch(). A thunk function will always be called with (dispatch, getState) as its arguments, and you can use
them inside the thunk as needed. This gives us a way to write whatever sync or async code we want, while still having
access to dispatch and getState.

Thunks are written using two functions:

- An inside thunk function, which gets `dispatch` and `getState` as arguments
- The outside thunk creator function, which creates and returns the thunk function

```javascript
// Outside thunk creator function
const logAndAdd = (amount) => {
  // Inside thunk function
  return (dispatch, getState) => {
    const stateBefore = getState();
    console.log(`Counter before: ${stateBefore.counter}`);
    dispatch(incrementByAmount(amount));
    const stateAfter = getState();
    console.log(`Counter after: ${stateAfter.counter}`);
  };
};

store.dispatch(logAndAdd(5)); // pass function to dispatch
```

### Fetching Data with createAsyncThunk

- [Documentation](https://redux.js.org/tutorials/essentials/part-5-async-logic#fetching-data-with-createasyncthunk)

Redux Toolkit's createAsyncThunk API generates thunks that automatically dispatch "start/success/failure" actions for
you.

- createAsyncThunk accepts a "payload creator" callback that should return a Promise, and generates
  pending/fulfilled/rejected action types automatically
- Generated action creators like fetchPosts dispatch those actions based on the Promise you return
- You can listen for these action types in createSlice using the extraReducers field, and update the state in reducers
  based on those actions.
- Action creators can be used to automatically fill in the keys of the extraReducers object so the slice knows what
  actions to listen for.

```javascript
export const fetchPosts = createAsyncThunk("posts/fetchPosts", async () => {
  const response = await client.get("/fakeApi/posts");
  return response.posts;
});
```

## Other available async middleware

- [redux-promise](https://github.com/acdlite/redux-promise) or
  [redux-promise-middleware](https://github.com/pburtchaell/redux-promise-middleware) to dispatch Promises instead of
  functions.
- [redux-observable](https://github.com/redux-observable/redux-observable) to dispatch Observables.
- [redux-saga](https://github.com/yelouafi/redux-saga/) middleware to build more complex asynchronous actions.
- [redux-pack](https://github.com/lelandrichardson/redux-pack) middleware to dispatch promise-based asynchronous
  actions.
- Write a custom middleware to describe calls to your API, like the [real world
  example](https://redux.js.org/introduction/examples#real-world) does.
