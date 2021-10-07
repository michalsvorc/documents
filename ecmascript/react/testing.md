# React testing

* [Testing Overview - React](https://reactjs.org/docs/testing.html)

We recommend using React Testing Library which is designed to enable and encourage writing tests that use your
components as the end users do.

For React versions <= 16, the Enzyme library makes it easy to assert, manipulate, and traverse your React Components'
output.

## React testing library

* [API](https://testing-library.com/docs/react-testing-library/api)
* [Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet)
* [Queries](https://testing-library.com/docs/queries/about)
* [Events](https://testing-library.com/docs/dom-testing-library/api-events)
* [Examples](https://testing-library.com/docs/recipes)

The core library, DOM Testing Library, is a light-weight solution for testing web pages by querying and interacting with
DOM nodes (whether simulated with JSDOM/Jest or in the browser). 

The main utilities it provides involve querying for nodes similarly to how users would find them.

Guiding Principle is the more your tests resemble the way your software is used, the more confidence they can give you.

React Testing Library builds on top of DOM Testing Library by adding APIs for working with React components.

Rather than dealing with instances of rendered React components, your tests will work with actual DOM nodes.

### render()

* [API](https://testing-library.com/docs/react-testing-library/api/#render)

```tsx
function render(
  ui: React.ReactElement<any>,
  options?: TestingLibrary.Options,
): RenderResult
```

By default, React Testing Library will create a `div` and append that `div` to the `document.body`.

The most important feature of render is that the *queries* from DOM Testing Library are automatically returned with
their first argument bound to the baseElement, which defaults to `document.body`.

You can pass a React Component as the `wrapper` option property to have it rendered around the inner element. This is
most useful for creating reusable custom render functions for common data providers.

### cleanup

* [API](https://testing-library.com/docs/react-testing-library/api/#cleanup)

Unmounts React trees that were mounted with render.

Please note that this is done automatically if the testing framework you're using supports the `afterEach` global and it
is injected to your testing environment (like mocha, Jest, and Jasmine).

### act()

* [API](https://testing-library.com/docs/react-testing-library/api/#act)

The fireEvent method allows you to fire events to simulate user actions.

This is a light wrapper around the `react-dom/test-utils` `act` function. All it does is forward all arguments to the
`act` function if your version of react supports act.

## React Test Renderer

* [Documentation](https://reactjs.org/docs/test-renderer.html)
* [API](https://reactjs.org/docs/test-renderer.html#testrenderer)
* [TDD with React Test Renderer](https://blog.logrocket.com/tdd-with-react-test-renderer/)

This package provides a React renderer that can be used to render React components to pure JavaScript objects, without
depending on the DOM or a native mobile environment.

Essentially, this package makes it easy to grab a snapshot of the platform view hierarchy (similar to a DOM tree)
rendered by a React DOM or React Native component without using a browser or jsdom.

You can use Jest's snapshot testing feature to automatically save a copy of the JSON tree to a file and check in your
tests that it hasn't changed.

See [Jest Snapshot Testing](https://jestjs.io/docs/snapshot-testing).

You can also traverse the output to find specific nodes and make assertions about them.

### create()

* [API](https://reactjs.org/docs/test-renderer.html#testrenderercreate)

Create a TestRenderer instance with the passed React element. It doesn't use the real DOM, but it still fully renders
the component tree into memory so you can make assertions about it. Returns a TestRenderer instance.

`TestRenderer.create(element, options);`

### act()

* [API](https://reactjs.org/docs/test-renderer.html#testrendereract)

Similar to the `act()` helper from `react-dom/test-utils`, TestRenderer.act prepares a component for assertions. 

`TestRenderer.act(callback);`

## Test Utilities

* [Documentation](https://reactjs.org/docs/test-utils.html)

ReactTestUtils makes it easy to test React components in the testing framework of your choice. 

### act()

* [API](https://reactjs.org/docs/test-utils.html#act)

To prepare a component for assertions, wrap the code rendering it and performing updates inside an `act()` call. This
makes your test run closer to how React works in the browser.

If you use React Test Renderer, it also provides an act export that behaves the same way.

## Enzyme

* [Documentation](https://github.com/enzymejs/enzyme)
* [Shallow Rendering API](https://enzymejs.github.io/enzyme/docs/api/shallow.html)

Enzyme is a JavaScript Testing utility for React that makes it easier to test your React Components' output. You can
also manipulate, traverse, and in some ways simulate runtime given the output.

Enzyme has three rendering methods:

* `mount()` renders the whole DOM tree and gives you jQuery-like API to access DOM elements inside this tree, simulate
  events and read text content. I prefer this method most of the time.
* `render()` returns a string with rendered HTML code, similar to the renderToString() method from react-dom. It's useful
  when you need to test HTML output. For example, a component that renders Markdown.
* `shallow()` renders only the component itself without its children. 

There are two similar ways to fire an event in Enzyme:

* Calling an event handler prop directly, like wrapper.props().onClick().
* Using `simulate()` method, like `wrapper.simulate('click');`.

Note: Simulate is deprecated; if there's ever a v4 of enzyme it will be removed with prejudice.

