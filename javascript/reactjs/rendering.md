# Rendering

- [A (Mostly) Complete Guide to React Rendering Behavior -
  isquaredsoftware.com](https://blog.isquaredsoftware.com/2020/05/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior/#what-is-rendering)
- [Reconciliation - React](https://reactjs.org/docs/reconciliation.html)

## Overview

React term _rendering_ does not refer to updating the DOM, but to _rendering phases_.

Component may be _rendered_ without any visible changes happening as a result.

Rendering by itself is fine - it's how React knows what DOM changes are needed.

But, rendering takes time, and _wasted renders_ where the UI output didn't change can add up.

## Props

- [How New Props References Affect Render Optimizations - isquaredsoftware.com](https://blog.isquaredsoftware.com/2020/05/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior/#how-new-props-references-affect-render-optimizations)

Rendering a component will, by default, cause all components inside of it (children) to be rendered too. By default,
React does not care whether _props changed_ - it will render child components unconditionally just because the parent
rendered.

React will still have to do the work of asking components to render themselves and diffing the render output.

Passing new references as props to a child component doesn't matter, because it will render even when you pass the same
props.

It does matter when you're using _optimization techniques_.

## State

- [State updates may be
  asynchronous - React](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-may-be-asynchronous)

Every update to the state triggers re-rendering.

React update might be asynchronous due to render batching. Render batching is when multiple calls to setState() result
in a single render pass being queued and executed, usually on a slight delay.

Calling `setState()` in the class component always queues a render of that component.

In order to trigger re-rendering in function components, React requires that any hook state updates (`useState` and
`useReducer`) must pass in or return a new reference as the new state value, whether it be a new object reference, or a
new primitive.

## Strict mode

React will double-render components inside of a `<StrictMode>` tag in development.

Never measure absolute render times using a React development build - only measure absolute times using production
builds.

That means the number of times your rendering logic runs is not the same as the number of committed render passes, and
you cannot rely on `console.log()` statements.

Use the [React Profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) to capture a trace and
count the number of committed renders overall, or add logging inside of a `useEffect` hook or `componentDidMount/Update`
lifecycle.

## Virtual DOM (Reconciliation)

- [Reconciliation - React](https://reactjs.org/docs/reconciliation.html)

React has internal optimizations which create the appearance of whole app re-rendering while maintaining great
performance. The bulk of these optimizations are part of a process called _reconciliation_.

React implements a heuristic O(n) algorithm based on two assumptions:

- Different _component types_ are assumed to generate substantially different trees. React will not attempt to diff
  them, but rather replace the old tree completely.
- Diffing of lists is performed using keys. Keys should therefore be stable, predictable, and unique.

Reconciliation is the algorithm behind what is popularly understood as the _virtual DOM_.

## Rendering process

The React team divides rendering process work into two phases:

- The _Render phase_ contains all the work of rendering components and calculating changes.
- The _Commit phase_ is the process of applying those changes to the DOM.

### Render phase

React will start at the root of the component tree and loop downwards to find all components that have been flagged as
needing updates. For each flagged component, React will call the _render method_, and save the _render output_.

React will then _diff_ the new tree of objects (a.k.a. the "virtual DOM"), and collects a list of all the changes that
need to be applied to make the real DOM look like the current desired output.

The diffing and calculation process is known as [reconciliation](https://reactjs.org/docs/reconciliation.html).

### Commit phase

React then applies all the calculated changes to the DOM in one synchronous sequence.

Then it synchronously runs:

- `componentDidMount`
- `componentDidUpdate`
- `useLayoutEffect` hooks

React then sets a short timeout, and when it expires, runs all the `useEffect` hooks.

## React Fiber

- [Reconciliation - React](https://reactjs.org/docs/reconciliation.html)
- [acdlite/react-fiber-architecture - github.com](https://github.com/acdlite/react-fiber-architecture)
- [(Video) What Is React Fiber? React.js Deep Dive #2 - youtube.com](https://www.youtube.com/watch?v=0ympFIwQFJw)

Introduced in React v16.

React Fiber is an ongoing reimplementation of React's core algorithm for the reconciler. The goal of React Fiber is to
increase its suitability for areas like animation, layout, and gestures.

Its headline feature is _incremental rendering_: the ability to split rendering work into chunks and spread it out over
multiple frames.

Although Fiber is a ground-up rewrite of the reconciler, the high-level algorithm described in the React docs will be
largely the same.

If something is offscreen, we can delay any logic related to it. If data is arriving faster than the frame rate, we can
coalesce and batch updates. We can prioritize work coming from user interactions (such as an animation caused by a
button click) over less important background work (such as rendering new content just loaded from the network) to avoid
dropping frames.

The key points are:

- In a UI, it's not necessary for every update to be applied immediately; in fact, doing so can be wasteful, causing
  frames to drop and degrading the user experience.
- Different types of updates have different priorities — an animation update needs to complete more quickly than, say,
  an update from a data store.
- A push-based approach requires the app (you, the programmer) to decide how to schedule work. A pull-based approach
  allows the framework (React) to be smart and make those decisions for you.

Some popular libraries implement the "push" approach where computations are performed when the new data is available.
React, however, sticks to the "pull" approach where computations can be delayed until necessary.

The primary goal of Fiber is to enable React to take advantage of scheduling.

- Scheduling: the process of determining when work should be performed.
- Work: any computations that must be performed. Work is usually the result of an update (e.g. setState).

Specifically, we need to be able to:

- pause work and come back to it later.
- assign priority to different types of work.
- reuse previously completed work.
- abort work if it's no longer needed.

We need to use Browser API:

- `requestIdleCallback`: schedules a low priority function to be called during an idle period
- `requestAnimationFrame`: schedules a high priority function to be called on the next animation frame.

In order to use those APIs, you need a way to break rendering work into incremental units. In one sense, that's what a
fiber is. A fiber represents a unit of work.

During a rendering pass, React will iterate over a tree of fiber objects, and construct an updated tree as it
calculates the new rendering results.

Note that these fiber objects store the real component props and state values. When a parent component renders a given
child component for the first time, React creates a fiber object to track that instance of a component.
