# MobX React

Overview:

* [10 minute introduction to MobX and React](https://mobx.js.org/getting-started)
* [React integration](https://mobx.js.org/react-integration.html)
* [Tips](https://mobx.js.org/react-integration.html#tips)
* [React optimizations](https://mobx.js.org/react-optimizations.html)

Libraries:

* [mobx-react-lite](https://github.com/mobxjs/mobx/tree/main/packages/mobx-react-lite)
* [mobx-react vs. mobx-react-lite](https://mobx.js.org/react-integration.html#react-vs-lite)

While MobX works independently from React, they are most commonly used together:

* React renders the application state by providing mechanisms to translate it into a tree of renderable components.
* MobX provides the mechanism to store and update the application state that React then uses.

## Observer HoC

* [React integration](https://mobx.js.org/react-integration.html#react-integration)

You can make your components reactive by wrapping them with the observer function from the bindings package you've
chosen during installation. 

The observer HoC automatically subscribes React components to *any observables* that are used *during rendering*. As a
result, components will automatically re-render when relevant observables change.

```js
import { observer } from "mobx-react-lite" // Or "mobx-react".

const MyComponent = observer((props) => ReactElement)
```

For observer to work, it doesn't matter how the observables arrive in the component, only that they are read (reading
observables deeply is fine).

## Local and external state

* [React integration](https://mobx.js.org/react-integration.html#local-and-external-state)

### External state:

* Observables can be passed into components as props.
* As global variables: we can consume observables from outer scopes directly (including from imports, etc.).
* React Context is a great mechanism to share observables with an entire subtree.

### Local state

* The simplest way to use local observable state is to store a reference to an observable class with useState.
* Instead of using classes, it is possible to directly create observable objects.
* The useLocalObservable hook is exposed from mobx-react-lite
