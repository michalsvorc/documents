# RxJS operators

* [Guide](https://rxjs-dev.firebaseapp.com/guide/operators)
* [Categories of operators](https://rxjs-dev.firebaseapp.com/guide/operators#categories-of-operators)
* [API](https://rxjs-dev.firebaseapp.com/api)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators)

## Overview

There are two kinds of operators:

* Pipeable operators: A function that takes an Observable as its input and returns another Observable.
* Creation operators: Can be called as standalone functions to create a new Observable.

The purpose of operators is to subscribe to the original Observable then change the behavior of the Observer.

## Piping

- [Piping](https://rxjs-dev.firebaseapp.com/guide/operators#piping)
- [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/concepts/rxjs-primer#pipe)

Pipeable operator is a function that takes an Observable as its input and returns another Observable.

You can use pipes to link operators together. Pipes let you combine multiple functions into a single function.

It is a pure operation: the previous Observable stays unmodified.

```javascript
observable.pipe(operator1(), operator2(), operator3(), operator4());
```

* An operator has the original observable as the first argument.
* An operator returns an observable.

## Creation

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/creation)

Can be called as standalone functions to create a new Observable.

* [ajax](https://www.learnrxjs.io/learn-rxjs/operators/creation/ajax)
* [from](https://www.learnrxjs.io/learn-rxjs/operators/creation/from)
* [fromEvent](https://www.learnrxjs.io/learn-rxjs/operators/creation/fromevent)
* [of](https://www.learnrxjs.io/learn-rxjs/operators/creation/of)

## Filtering

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/filtering)

These operators provide techniques for accepting values from an observable source.

* [debounceTime](https://www.learnrxjs.io/learn-rxjs/operators/filtering/debouncetime)
* [distinctUntilChanged](https://www.learnrxjs.io/learn-rxjs/operators/filtering/distinctuntilchanged)
* [filter](https://www.learnrxjs.io/learn-rxjs/operators/filtering/filter)
* [find](https://www.learnrxjs.io/learn-rxjs/operators/filtering/find)
* [first](https://www.learnrxjs.io/learn-rxjs/operators/filtering/first)
* [last](https://www.learnrxjs.io/learn-rxjs/operators/filtering/last)
* [take](https://www.learnrxjs.io/learn-rxjs/operators/filtering/take)
* [takeUntil](https://www.learnrxjs.io/learn-rxjs/operators/filtering/takeuntil)

## Transformation

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/transformation)

Transforming values as they pass through the operator chain.

* [concatMap](https://www.learnrxjs.io/learn-rxjs/operators/transformation/concatmap)
* [groupBy](https://www.learnrxjs.io/learn-rxjs/operators/transformation/groupby)
* [map](https://www.learnrxjs.io/learn-rxjs/operators/transformation/map)
* [mapTo](https://www.learnrxjs.io/learn-rxjs/operators/transformation/mapto)
* [mergeMap / flatMap](https://www.learnrxjs.io/learn-rxjs/operators/transformation/mergemap)
* [scan](https://www.learnrxjs.io/learn-rxjs/operators/transformation/scan)
* [switchMap](https://www.learnrxjs.io/learn-rxjs/operators/transformation/switchmap)

## Combination

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/combination)

The combination operators allow the joining of information from multiple observables.  Order, time, and structure of
emitted values is the primary variation among these operators.

* [combineLatest](https://www.learnrxjs.io/learn-rxjs/operators/combination/combinelatest)
* [concat](https://www.learnrxjs.io/learn-rxjs/operators/combination/concat)
* [merge](https://www.learnrxjs.io/learn-rxjs/operators/combination/merge)
* [startWith](https://www.learnrxjs.io/learn-rxjs/operators/combination/startwith)
* [withLatestFrom](https://www.learnrxjs.io/learn-rxjs/operators/combination/withlatestfrom)
* [zip](https://www.learnrxjs.io/learn-rxjs/operators/combination/zip)

## Conditional

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/conditional)

For use-cases that depend on a specific condition to be met, these operators do the trick.

## Multicasting

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/multicasting)

In RxJS observables are cold, or unicast by default. These operators can make an observable hot, or multicast, allowing
side-effects to be shared among multiple subscribers.

* [multicast](https://www.learnrxjs.io/learn-rxjs/operators/multicasting/multicast)
* [share](https://www.learnrxjs.io/learn-rxjs/operators/multicasting/share)

## Utility

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/utility)

From logging, handling notifications, to setting up schedulers, these operators provide helpful utilities in your
observable toolkit.

* [tap / do](https://www.learnrxjs.io/learn-rxjs/operators/utility/do)
* [delay](https://www.learnrxjs.io/learn-rxjs/operators/utility/delay)

## Error Handling

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/error_handling)

* [catch / catchError](https://www.learnrxjs.io/learn-rxjs/operators/error_handling/catch)

## Summary: commonly used operators

* [of](https://rxjs-dev.firebaseapp.com/api/index/function/of)

Converts the arguments to an observable sequence.

* [from](https://rxjs-dev.firebaseapp.com/api/index/function/from)

Creates an Observable from an Array, an array-like object, a Promise, an iterable object, or an Observable-like object.

* [fromEvent](https://rxjs-dev.firebaseapp.com/api/index/function/fromEvent)

Creates an Observable that emits events of a specific type coming from the given event target. 

* [map](https://rxjs-dev.firebaseapp.com/api/operators/map)

Applies a given function to each value emitted by the source Observable, and emits the resulting values as an
Observable.

* [tap](https://rxjs-dev.firebaseapp.com/api/operators/tap)

Perform a side effect for every emission on the source Observable, but return an Observable that is identical to the
source.

* [pluck](https://rxjs-dev.firebaseapp.com/api/operators/pluck)

Like `map`, but meant only for picking one of the nested properties of every emitted object.  Pluck is used when we just
need to pass a single field value to the subscription instead of sending the entire JSON object.

* [share](https://rxjs-dev.firebaseapp.com/api/operators/share)

Alias for multicast(() => new Subject()), refCount(). Returns a new Observable that multicasts (shares) the original
Observable.  As long as there is at least one Subscriber this Observable will be subscribed and emitting data.  When all
subscribers have unsubscribed it will unsubscribe from the source Observable. Because the Observable is multicasting it
makes the stream hot. 


* [switchMap](https://rxjs-dev.firebaseapp.com/api/operators/switchMap)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/transformation/switchmap)
* [(Video) How to Use RxJs SwitchMap with Demos](https://www.youtube.com/watch?v=d12vW8Ch5IE)

Cancels from one observable and switches to another with value from the first one (switch to a new observable).

* [mergeMap / flatMap](https://rxjs-dev.firebaseapp.com/api/operators/mergeMap)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/operators/transformation/mergemap)
* [(Video) RxJs MergeMap | How to use RxJs MergeMap | What is RxJs MergeMap | RxJs MergeMap
  Demo](https://www.youtube.com/watch?v=-Zr2m6j4AV4)

This operator is best used when you wish to flatten an inner observable but want to manually control the number of inner
subscriptions.  For instance, when using `switchMap` each inner subscription is completed when the source emits,
allowing only one active inner subscription.  In contrast, mergeMap allows for multiple inner subscriptions to be active
at a time. `flatMap` is an alias for mergeMap.

* [debounceTime](https://rxjs-dev.firebaseapp.com/api/operators/debounceTime)

Discard emitted values that take less than the specified time between output.  This operator is popular in scenarios
such as type-ahead where the rate of user input must be controlled.

* [debounce](https://rxjs-dev.firebaseapp.com/api/operators/debounce)

Emits a value from the source Observable only after a particular time span determined by another Observable has passed
without another source emission.  It's like `debounceTime`, but the time span of emission silence is determined by a
second Observable.

Also like `debounceTime` this is a rate-limiting operator, and also a delay-like operator since output emissions do not
necessarily occur at the same time as they did on the source Observable.

* [distinctUntilChanged](https://rxjs-dev.firebaseapp.com/api/operators/distinctUntilChanged)

Returns an Observable that emits all items emitted by the source Observable that are distinct by comparison from the
previous item.  If a comparator function is provided, then it will be called for each item to test for whether or not
that value should be emitted.

* [take](https://rxjs-dev.firebaseapp.com/api/operators/take)

Emits only the first count values emitted by the source Observable. Take returns an Observable that emits only the first
count values emitted by the source Observable. If the source emits fewer than count values then all of its values are
emitted.  After that, it completes, regardless if the source completes.

* [concat](https://rxjs-dev.firebaseapp.com/api/index/function/concat)

Concatenates multiple Observables together by sequentially emitting their values, one Observable after another.

* [forkJoin](https://rxjs-dev.firebaseapp.com/api/index/function/forkJoin)

Similar to Promise.all(). Wait for Observables to complete and then combine last values they emitted.  Accepts an Array
of [ObservableInput](https://rxjs-dev.firebaseapp.com/api/index/type-alias/ObservableInput) or a dictionary Object of
`ObservableInput` and returns an Observable that emits either an array of values in the exact same order as the passed
array, or a dictionary of values in the same shape as the passed dictionary. 

* [catchError](https://rxjs-dev.firebaseapp.com/api/operators/catchError)

Catches errors on the observable to be handled by returning a new observable or throwing an error. Usage:

- Continues with a different Observable when there's an error 
- Retries the caught source Observable again in case of error, similar to retry() operator
- Throws a new error when the source Observable throws an error

* [zip](https://rxjs-dev.firebaseapp.com/api/operators/zip)

Zip operator will wait for all observables to emit and then it zips those values into an array as an output.  Combines
multiple Observables to create an Observable whose values are calculated from the values, in order, of each of its input
Observables.  If the last parameter is a function, this function is used to compute the created value from the input
values. Otherwise, an array of the input values is returned.

