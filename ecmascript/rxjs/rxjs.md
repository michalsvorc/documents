# RxJS

Overview:

* [RxJS](https://rxjs-dev.firebaseapp.com/guide/overview)
* [Learn RxJS](https://www.learnrxjs.io)
* [API](https://rxjs-dev.firebaseapp.com/api)
* [Glossary](https://rxjs-dev.firebaseapp.com/guide/glossary-and-semantics)

Operators:

* [Guide](https://rxjs-dev.firebaseapp.com/guide/operators)
* [Operator Decision Tree](https://rxjs-dev.firebaseapp.com/operator-decision-tree)
* [Categories of operators](https://rxjs-dev.firebaseapp.com/guide/operators#categories-of-operators)
* [API](https://rxjs-dev.firebaseapp.com/api)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/complete)
* [RxJS Marbles](https://rxmarbles.com/)

Playground:

* [RxFiddle](https://rxfiddle.net)
* [Rx Visualizer](https://rxviz.com/examples/custom)
* [Codesandbox.io](https://codesandbox.io/s/rxjs-playground-onlev?file=/src/index.js)

Topics:

* [RxJS Primer](https://www.learnrxjs.io/learn-rxjs/concepts/rxjs-primer)
* [Pull vs. Push](https://rxjs-dev.firebaseapp.com/guide/observable#pull-versus-push)

## Overview

RxJS (Reactive Extensions for JavaScript) is a library for reactive programming using observables that makes it easier
to compose asynchronous or callback-based code.

RxJS offers powerful, *functional* approach for dealing with events.

_      | Single   | Multiple
------ | ------   |---------
Pull   |Function  |Iterator
Push   |Promise   |Observable

A Promise is simply an Observable with one single emitted value. Rx streams go beyond promises by allowing many returned
values.

RxJS introduces Observables, a new Push system for JavaScript. An Observable is a Producer of multiple values, "pushing"
them to Observers (Consumers).

## Reactive programming

* [Introduction](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)
* [Observer pattern](https://en.wikipedia.org/wiki/Observer_pattern)
* [Iterator pattern](https://en.wikipedia.org/wiki/Iterator_pattern)

Reactive programming is an asynchronous programming paradigm concerned with data streams and the propagation of change.

A stream is a sequence of ongoing events ordered in time. It can emit three different things: a value (of some type), an
error, or a "completed" signal. 

We capture these emitted events only asynchronously, by defining a function that will execute when a value is emitted,
another function when an error is emitted, and another function when 'completed' is emitted. 

* The listening to the stream is called *subscribing*.
* The functions we are defining are *observers*.
* The stream is the *subject* (or "observable") being observed.

## Observables

* [Guide](https://rxjs-dev.firebaseapp.com/guide/observable)
* [Creation functions](https://www.learnrxjs.io/learn-rxjs/operators/creation)

An Observable represents a stream, or source of data that can arrive over time.

An Observable is basically a *function* that can return a stream of values to an Observer over time.

The Observable does not maintain a list of attached Observers.

Observables are able to deliver values either synchronously or asynchronously.

Core Observable concerns:

* Creating Observables
* Subscribing to Observables
* Executing the Observable
* Disposing Observables

Observables are created using `new Observable` or a creation operator, are subscribed to with an Observer, execute to
deliver `next` / `error` / `complete` notifications to the Observer, and their execution may be disposed.

### Creating Observables

* [Creation Operators](https://rxjs-dev.firebaseapp.com/guide/operators#creation-operators-list) 

Observables can be created with `new Observable`. Most commonly, observables are created using creation functions, like
`of`, `from`, `interval`, etc.

### Subscribing to Observables

* [Guide](https://rxjs-dev.firebaseapp.com/guide/observable#subscribing-to-observables)
* [Subscription](https://rxjs-dev.firebaseapp.com/guide/subscription)

Subscribing to an Observable is like calling a function, providing callbacks where the data will be delivered to.  

A subscribe call is simply a way to start an "Observable execution" and deliver values or events to an Observer of that
execution.

Subscribe calls are not shared among multiple Observers of the same Observable. Each subscription will create a new
execution context.  Each execution is exclusive to one Observer only.

With `observable.subscribe`, the given Observer is not registered as a listener in the Observable. The Observable does
not maintain a list of attached Observers.

```javascript
const subscription = observable.subscribe(x => console.log(x));
```

When you subscribe, you get back a Subscription object, which represents the ongoing execution.

### Executing Observables

- [Guide](https://rxjs-dev.firebaseapp.com/guide/observable#executing-observables)

There are three types of values an Observable execution can deliver:

* `Next`: Required. A handler for each delivered value. Called zero or more times after execution starts.
* `Error`: Optional. A handler for an error notification. An error halts execution of the observable instance.
* `Complete`: Optional. A handler for the execution-complete notification. Delayed values can continue to be delivered
  to the next handler after execution is complete.

`Error` and `Complete` notifications may happen only once during the Observable Execution, and there can only be either
one of them.

If either an `Error` or `Complete` notification is delivered, then nothing else can be delivered afterwards.

### Disposing Observable Executions

- [Guide](https://rxjs-dev.firebaseapp.com/guide/observable#disposing-observable-executions)

Because Observable Executions may be infinite, and it's common for an Observer to want to abort execution in finite
time, we need an API for canceling an execution.

When you subscribe, you get back a Subscription, which represents the ongoing execution. Call `unsubscribe()` method on
that subscription to cancel the execution.

Each Observable must define how to dispose resources of that execution when we create the Observable. You can do that by
returning a custom unsubscribe function from within `subscribe()` function.

### Cold and Hot Observables

* *Cold* observables: The data is produced by the Observable itself.

*Cold* observables start running upon subscription, i.e., the observable sequence only starts pushing values to the
observers when Subscribe is called.

* *Hot* observables: The data is produced outside of the Observable.

*Hot* observables such as mouse move events or stock tickers are already producing values even before a subscription is
active. 

## Observers

* [Guide](https://rxjs-dev.firebaseapp.com/guide/observer)

Observers are just objects with three callbacks, one for each type of notification that an Observable may deliver: next,
error, and complete.

To use the Observer, provide it to the subscribe of an Observable:

```javascript
observable.subscribe(observer);
```

When subscribing to an Observable, you may also just provide the next callback as an argument, without being attached to
an Observer object.

## Scheduler

* [Guide](https://rxjs-dev.firebaseapp.com/guide/scheduler)

A Scheduler lets you define in what execution context will an Observable deliver notifications to its Observer.
A Scheduler has a (virtual) clock. It provides a notion of "time" by a getter method now() on the scheduler.
Tasks being scheduled on a particular scheduler will adhere only to the time denoted by that clock.

