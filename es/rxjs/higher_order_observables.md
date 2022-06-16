# RxJS Higher-order Observables

* [Guide](https://rxjs-dev.firebaseapp.com/guide/operators#higher-order-observables)

Observables most commonly emit ordinary values like strings and numbers, but surprisingly often, it is necessary to
handle Observables of Observables, so-called higher-order Observables.

```javascript
const fileObservable = urlObservable.pipe(
   map(url => http.get(url)),
);
```

http.get() returns an Observable (of string or string arrays probably) for each individual URL.
Now you have an Observables of Observables, a higher-order Observable.

## Flattening

But how do you work with a higher-order Observable? Typically, by flattening: by (somehow) converting a higher-order
Observable into an ordinary Observable.

For example:

```javascript
const fileObservable = urlObservable.pipe(
   map(url => http.get(url)),
   concatAll(),
);
```

The [concatAll()](https://rxjs-dev.firebaseapp.com/api/operators/concatAll) operator subscribes to each "inner"
Observable that comes out of the "outer" Observable, and copies all the emitted values until that Observable completes,
and goes on to the next one.  All of the values are in that way concatenated.

Other useful flattening operators (called join operators) are:

* [mergeAll()](https://rxjs-dev.firebaseapp.com/api/operators/mergeAll): Subscribes to each inner Observable as it
  arrives, then emits each value as it arrives.
* [switchAll()](https://rxjs-dev.firebaseapp.com/api/operators/switchAll): Subscribes to the first inner Observable when
  it arrives, and emits each value as it arrives, but when the next inner Observable arrives, unsubscribes to the
  previous one, and subscribes to the new one.
* [exhaust()](https://rxjs-dev.firebaseapp.com/api/operators/exhaust): Subscribes to the first inner Observable when it
  arrives, and emits each value as it arrives, discarding all newly arriving inner Observables until that first one
  completes, then waits for the next inner Observable.

## Summary

* merge: observables
* mergeAll: flattening
* mergeMap: flattening + mapping
* concat: observables
* concatAll: flattening
* concatMap: flattening + mapping
* switchMap: flattening + mapping

