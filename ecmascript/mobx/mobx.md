# MobX

Overview:

* [Mobx.js.org](https://mobx.js.org/)
* [Videos](https://mobx.js.org/README.html#videos)

API:
* [API reference](https://mobx.js.org/api.html)

Topics:

* [Defining data stores](https://mobx.js.org/defining-data-stores.html)
* [Understanding reactivity](https://mobx.js.org/understanding-reactivity.html)

Libraries:

* [Linting](https://mobx.js.org/configuration.html#linting-options)
* [mobx-state-tree](https://github.com/mobxjs/mobx-state-tree)
* [mobx-keystone](https://mobx-keystone.js.org/) 

## Overview

MobX is unopinionated and allows you to manage your application state outside of any UI framework. See [MobX on other
frameworks / platforms](https://mobx.js.org/installation.html#mobx-on-other-frameworks--platforms).

MobX works in any ES5 environment, which includes browsers and NodeJS. In MobX 6, we have chosen to move away from
decorators by default, for maximum compatibility with standard JavaScript. They can still be used if you enable them
though.

MobX reacts to any existing observable property that is read during the execution of a tracked function. MobX tracks
property access, not values. Reading is dereferencing an object's property, which can be done through "dotting into" it
(eg. `user.name`) or using the bracket notation (eg. `user['name']`).

## Concepts

* [Documentation](https://mobx.js.org/the-gist-of-mobx.html)

*Anything that can be derived from the application state, should be. Automatically.* This includes the UI, data
serialization, server communication, etc.

MobX distinguishes between the following three concepts in your application:

1. [State](https://mobx.js.org/observable-state.html): State is the data that drives your application (store).
2. [Actions](https://mobx.js.org/actions.html): Update state using actions.
3. *Derivations*: Create derivations that automatically respond to state changes.

MobX is inspired by reactive programming principles as found in the spreadsheets.

Using observable is like turning a property of an object into a spreadsheet cell. 

An action is any piece of code that changes the state. An action is like a user that enters a new value into a
spreadsheet cell.

MobX uses a uni-directional data flow where actions change the state, which in turn updates all affected views.

`Actions` -> `Observable state` -> `Derived values` -> `Reactions`

1. All derivations are updated automatically and atomically when the state changes. As a result, it is never possible to
observe intermediate values.
2. All derivations are updated synchronously by default. This means that, for example, actions can safely inspect a
computed value directly after altering the state.
3. Computed values are updated lazily. Any computed value that is not actively in use will not be updated until it is
needed for a side effect (I/O). If a view is no longer in use it will be garbage collected automatically.
4. All computed values should be pure. They are not supposed to change state.

## State

* [Documentation](https://mobx.js.org/observable-state.html)
* [Limitations](https://mobx.js.org/observable-state.html#limitations)
* [Annotations](https://mobx.js.org/observable-state.html#available-annotations)
* [Options](https://mobx.js.org/observable-state.html#options-)
* [Observable array](https://mobx.js.org/observable-state.html#observable-array)
* [Classes](https://mobx.js.org/observable-state.html#a-short-note-on-classes)

State is like spreadsheet cells that hold a value.

All properties you want to change over time should be marked as observable so MobX can track them.

The most important annotations are:

* `observable` defines a trackable field that stores the state.
* `action` marks a method as action that will modify the state.
* `computed` marks a getter that will derive new facts from the state and cache its output.

Collections such as arrays, Maps and Sets are made observable automatically.

### makeObservable

* [Documentation](https://mobx.js.org/observable-state.html#makeobservable)

`makeObservable(target, annotations?, options?)`

It can be used to trap *existing* object properties and make them observable.

### makeAutoObservable

* [Documentation](https://mobx.js.org/observable-state.html#makeautoobservable)

`makeAutoObservable(target, overrides?, options?)`

Like makeObservable, it infers all the properties by default. You can still use overrides to override the default
behavior with specific annotations.

The makeAutoObservable function can be more compact and easier to maintain than using makeObservable, since new members
don't have to be mentioned explicitly.

### observable

* [Documentation](https://mobx.js.org/observable-state.html#observable)

`observable(source, overrides?, options?)`

The observable annotation can also be called as a function to make an entire object observable at once.

The source object will be cloned and all members will be made observable, similar to how it would be done by
makeAutoObservable.

## Actions 

* [Documentation](https://mobx.js.org/actions.html)
* [Asynchronous actions](https://mobx.js.org/actions.html#asynchronous-actions)
* [Mobx - runInAction() usage](https://stackoverflow.com/questions/57271153/mobx-runinaction-usage-why-do-we-need-it)

An action is any piece of code that modifies the state.

Actions help you structure your code better and offer the following performance benefits:

* They are run inside transactions. No reactions will be run until the outer-most action has finished, guaranteeing that
  intermediate or incomplete values produced during an action are not visible to the rest of the application until the
  action has completed.
* By default, it is not allowed to change the state outside of actions. This helps to clearly identify in your code base
  where the state updates happen.

Usage:

* `action` (*annotation*)
* `action(fn)`
* `action(name, fn)`

### Using flow instead of async / await

* [Documentation](https://mobx.js.org/actions.html#using-flow-instead-of-async--await-)

Usage:

* `flow (annotation)`
* `flow(function* (args) { })`


Flow is an alternative to async / await that doesn't need any further action wrapping. Flow takes a [generator
function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator) as its only input.
Another neat benefit of flows is that they are cancellable. 

## Computeds

* [Documentation](https://mobx.js.org/computeds.html)
* [Tips](https://mobx.js.org/computeds.html#tips)
* [Options](https://mobx.js.org/computeds.html#options-).
* [Built-in comparer methods](https://mobx.js.org/computeds.html#built-in-comparers)

Usage:

* `computed` (*annotation*)
* `computed(options)` (*annotation*)
* `computed(fn, options?)`

Computed values can be created by annotating JavaScript *getters* with computed.

Computed values can be used to derive information from other observables. They evaluate lazily, caching their output and
only recomputing if one of the underlying observables has changed. If they are not observed by anything, they suspend
entirely.

Conceptually, they are very similar to formulas in spreadsheets, and can't be underestimated. They help in reducing the
amount of state you have to store and are highly optimized. Use them wherever possible.

## Reactions

* [Documentation](https://mobx.js.org/reactions.html)

Reactions APIs should rarely be used directly, They are often abstracted away in other libraries or abstractions
specific to your application.

Reactions are similar to computed values, but instead of producing information, they produce side effects like printing
to the console, making network requests, incrementally updating React component tree to patch the DOM, etc.

### autorun

* [Documentation](https://mobx.js.org/reactions.html#autorun)

`autorun(effect: (reaction) => void)`

Accepts one function that should run every time anything it observes changes. It also runs once when you create the
autorun itself.

### reaction 

* [Documentation](https://mobx.js.org/reactions.html#reaction)

`reaction(() => value, (value, previousValue, reaction) => { sideEffect }, options?)`

Reaction is like autorun, but gives more fine grained control on which observables will be tracked. It takes two
functions: the first, data function, is tracked and returns the data that is used as input for the second, effect
function.

### when

* [Documentation](https://mobx.js.org/reactions.html#when)

`when(predicate: () => boolean, effect?: () => void, options?)`
`when(predicate: () => boolean, options?): Promise`

When observes and runs the given predicate function until it returns true. Once that happens, the given effect function
is executed and the autorunner is disposed of.

