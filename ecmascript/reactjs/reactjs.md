# React.js

Overview:

* [Documentation](https://reactjs.org/docs/hello-world.html)
* [JSX In Depth](https://reactjs.org/docs/jsx-in-depth.html)
* [Advanced Guides](https://reactjs.org/docs/getting-started.html#advanced-concepts)
* [Glossary of React Terms](https://reactjs.org/docs/glossary.html)

APIs:

* [React Top-Level API](https://reactjs.org/docs/react-api.html)
* [SyntheticEvent](https://reactjs.org/docs/events.html)
* [Changelog](https://github.com/facebook/react/blob/main/CHANGELOG.md)

Blogs:

* [React Blog](https://reactjs.org/blog/)

Topics:

* [React Internals Series' Articles](https://dev.to/burhanuday/series/8556)
* [Browser support](https://reactjs.org/docs/javascript-environment-requirements.html)
* [Code-Splitting](https://reactjs.org/docs/code-splitting.html)
* [Why copying props into state causes bugs - React Blog](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html)

TypeScript:

* [TypeScript – React](https://reactjs.org/docs/static-type-checking.html#typescript)
* [React TS cheatsheet](https://react-typescript-cheatsheet.netlify.app)
* [DefinitelyTyped index.d.ts - github.com](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/react/index.d.ts)

## Components

* [Components and Props - React](https://reactjs.org/docs/components-and-props.html)

The simplest way to define a component is to write a JavaScript function that accepts a single props (which stands for
properties) object argument with data and returns a React element. 

You can also use an ES6 class to define a component that extends `React.Component`.

## Props

* [JSX In Depth - React](https://reactjs.org/docs/jsx-in-depth.html#props-in-jsx)

Props are read only. All React components must act like pure functions with respect to their props.

If you pass no value for a prop, it defaults to `true`. In general, we don't recommend not passing a value for a prop.

### props vs. state

Props (short for "properties") and state are both plain JavaScript objects.

Props get passed to the component (similar to function parameters) whereas state is managed within the component
(similar to variables declared within a function).

In React, both `this.props` and `this.state` represent the rendered values, i.e. what's currently on the screen.

### props.children

* [JSX In Depth - React](https://reactjs.org/docs/jsx-in-depth.html#children-in-jsx)
* [Composition vs Inheritance - React](https://reactjs.org/docs/composition-vs-inheritance.html)

In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a
special prop: `props.children`.

Some components don't know their children ahead of time. We recommend that such components use the special `children`
prop to pass children elements directly into their output.

### Render props

* [Render Props - React](https://reactjs.org/docs/render-props.html)
* [Use a Render Prop - medium.com](https://medium.com/@mjackson/use-a-render-prop-50de598f11ce)

A component with a render prop takes a function that returns a React element and executes it instead of implementing its
own render logic. The prop doesn't have to be called `render`,we could just as easily use the `children` prop. 

A render prop is a function prop that a component uses to know what to render.

```jsx
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```

Use render props for cross-cutting concerns, like reusing and encapsulating behavior in another component.

One interesting thing to note about render props is that you can implement most higher-order components (HOC) using a
regular component with a render prop.

## Events

* [Handling Events - React](https://reactjs.org/docs/handling-events.html)
* [SyntheticEvent - React](https://reactjs.org/docs/events.html)

* React events are named using camelCase, rather than lowercase.
* With JSX you pass a function as the event handler, rather than a string.
* You must call `preventDefault` explicitly to prevent the default behaviour.

## Falsy values and rendering

* [JSX In Depth - React](https://reactjs.org/docs/jsx-in-depth.html#booleans-null-and-undefined-are-ignored)

* `false`, `null`, `undefined`, and `true` are valid children. They simply don't render. 
* One caveat is that some falsy values, such as the `0`, are still rendered by React. 

## Lists and keys

* [Lists and Keys - React](https://reactjs.org/docs/lists-and-keys.html#extracting-components-with-keys)

Keys only make sense in the context of the surrounding array. A good rule of thumb is that elements inside the `map()`
call need keys.

Keys used within arrays should be unique among their siblings. However, they don't need to be globally unique. We can
use the same keys when we produce two different arrays.

Keys serve as a hint to React but they don't get passed to your components. If you need the same value in your
component, pass it explicitly as a prop with a different name, e.g. id.

### Keyed fragments

* [Fragments - React](https://reactjs.org/docs/fragments.html#keyed-fragments)

Fragments declared with the explicit `<React.Fragment key={item.id}>` syntax may have keys. A use case for this is mapping a
collection to an array of fragments - for example, to create a description list:

## Forms

* [Forms - React](https://reactjs.org/docs/forms.html)

In HTML, form elements such as `<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it
based on user input. An input form element whose value is controlled by React in this way is called a *controlled
component*.

In most cases, we recommend using controlled components to implement forms. In a controlled component, form data is
handled by a React component. The alternative is [uncontrolled
components](https://reactjs.org/docs/uncontrolled-components.html), where form data is handled by the DOM itself.

## Accessibility

* [Accessibility - React](https://reactjs.org/docs/accessibility.html)
* [MDN HTML elements reference - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

Semantic HTML is the foundation of accessibility in a web application. Developers should prefer using the correct
semantic HTML element over using ARIA. All `aria-*` HTML attributes are still fully supported in JSX.

The `for` attribute in `<label>` is written as `htmlFor` in JSX: 

```jsx
<label htmlFor="namedInput">Name:</label>
<input id="namedInput" type="text" name="name"/>
```

### Focus

* [Programmatically managing focus –
  React.js](https://reactjs.org/docs/accessibility.html#programmatically-managing-focus)

To set focus in React, we can use [Refs to DOM elements](https://reactjs.org/docs/refs-and-the-dom.html).

## React element manipulation APIs:

* [cloneElement()](https://reactjs.org/docs/react-api.html#cloneelement)
* [isValidElement()](https://reactjs.org/docs/react-api.html#isvalidelement)
* [React.Children](https://reactjs.org/docs/react-api.html#reactchildren)
  - [React.Children.map](https://reactjs.org/docs/react-api.html#reactchildrenmap)
  - [React.Children.forEach](https://reactjs.org/docs/react-api.html#reactchildrenforeach)
  - [React.Children.count](https://reactjs.org/docs/react-api.html#reactchildrencount)
  - [React.Children.only](https://reactjs.org/docs/react-api.html#reactchildrenonly)
  - [React.Children.toArray](https://reactjs.org/docs/react-api.html#reactchildrentoarray)

## Higher-order components (HOC)

* [Higher-Order Components - React](https://reactjs.org/docs/higher-order-components.html)
* [(Video) ReactJS Tutorial - 34 - Higher Order Components (Part 2)](https://www.youtube.com/watch?v=rsBQj6X7UK8)

Higher-order component is a function that takes a component and returns a new component. Resist the temptation to modify
a component's prototype (or otherwise mutate it) inside a HOC, use Composition instead.

NOTE: See "Render props" as a possible alternative to HOC.

## Error Boundaries

* [Error Boundaries - React](https://reactjs.org/docs/error-boundaries.html)
* [React.Component - React](https://reactjs.org/docs/react-component.html#error-boundaries)
* [Error Handling in React 16 - React Blog](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html)

`try/catch` is great but it only works for imperative code. However, React components are declarative and specify what should be rendered. Error boundaries work like a JavaScript `catch {}` block, but for components.

A class component becomes an error boundary if it defines either (or both) of the Error boundaries lifecycle methods:

* [static getDerivedStateFromError(error)](https://reactjs.org/docs/react-component.html#static-getderivedstatefromerror)

Render a fallback UI after an error has been thrown, no side-effects.

* [componentDidCatch(error, info)](https://reactjs.org/docs/react-component.html#componentdidcatch)

Log error information, side-effects.

As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component
tree.

Note that error boundaries only catch errors in the components below them in the tree. If an error boundary fails trying
to render the error message, the error will propagate to the closest error boundary above it. 

```jsx
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

Error boundaries do not catch errors for:
* Event handlers ([learn more](https://reactjs.org/docs/error-boundaries.html#how-about-event-handlers)).
* Asynchronous code (e.g. `setTimeout` or `requestAnimationFrame` callbacks).
* Server side rendering.
* Errors thrown in the error boundary itself (rather than its children).

If you need to catch an error inside an event handler, use the regular JavaScript `try/catch` statement.

### Component Stack Traces

Component names displayed in the stack traces depend on the
[Function.name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name)
property.

Alternatively, you may explicitly set the [displayName](https://reactjs.org/docs/react-component.html#displayname)
property on all your components.

## Portals

* [Portals - React](https://reactjs.org/docs/portals.html)
* [Example: Portal event bubbling - codepen.io](https://codepen.io/gaearon/pen/jGBWpE)

Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent
component.

```jsx
ReactDOM.createPortal(child, container)
```

The first argument (`child`) is any renderable React child, such as an element, string, or fragment.

The second argument (`container`) is a DOM element. Container can be any valid DOM node, regardless of its location in the
DOM.

A typical use case for portals is when a parent component has an overflow: hidden or z-index style, but you need the
child to visually *break out* of its container. For example, dialogs, hovercards, and tooltips.

## Profiler API

* [Profiler API - React](https://reactjs.org/docs/profiler.html)

The Profiler measures how often a React application renders and what the *cost of rendering* is. Its purpose is to help
identify parts of an application that are slow and may benefit from optimizations such as memoization.

```jsx
<Profiler id="Navigation" onRender={callback}>
  <Navigation {...props} />
</Profiler>
```

## Strict mode

* [Strict Mode - React](https://reactjs.org/docs/strict-mode.html)

Strict mode is a tool for highlighting potential problems in an application. StrictMode does not render any visible UI.
It activates additional checks and warnings for its descendants. Strict mode checks are run in development mode only;
they do not impact the production build.

```jsx
<React.StrictMode>
  ...
</React.StrictMode>
```

StrictMode currently helps with:

* Identifying components with unsafe lifecycles
* Warning about legacy string ref API usage
* Warning about deprecated findDOMNode usage
* Detecting unexpected side effects
* Detecting legacy context API

## Code Splitting

* [Code-Splitting - React](https://reactjs.org/docs/code-splitting.html#code-splitting)

### Dynamic import

* [Code-Splitting - React](https://reactjs.org/docs/code-splitting.html#import)

The best way to introduce code-splitting into your app is through the *dynamic import*: 

`import("./lib").then(Lib => { ... })`

### React.lazy and Suspense

* [Code-Splitting - React](https://reactjs.org/docs/code-splitting.html#reactlazy)

The `React.lazy` function lets you render a dynamic import as a regular component. The lazy component should then be
rendered inside a `Suspense` component, which allows us to show some fallback content (such as a loading indicator) while
we're waiting for the lazy component to load.

```jsx
const OtherComponent = React.lazy(() => import('./OtherComponent'));

<Suspense fallback={<div>Loading</div>}>
  <OtherComponent />
</Suspense>
```

### Loadable Components library

* [Loadable Components](https://github.com/gregberge/loadable-components)
* [guide for bundle splitting with server-side
rendering](https://loadable-components.com/docs/server-side-rendering/)

`React.lazy` and `Suspense` are not yet available for server-side rendering. If you want to do code-splitting in a
server rendered app, we recommend Loadable Components library.

## Server components

* [Introducing Zero-Bundle-Size React Server Components - React
  Blog](https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html)

WIP

