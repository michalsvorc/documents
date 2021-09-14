# RxJS examples

## Creating Observables

Observable constructor:

```javascript
const observable = new Observable(function subscribe(subscriber) {
    try {
    subscriber.next(1);
    subscriber.next(2);
    subscriber.next(3);
    subscriber.complete();
  } catch (err) {
    subscriber.error(err); // delivers an error if it caught one
  }

  // Provide a way of canceling and disposing the interval resource
  return function unsubscribe() {
    console.log('clearing')
  };
});
```

Creation function:

```javascript
const observable = fromEvent(button, 'click');
```

See more [creation functions](https://www.learnrxjs.io/learn-rxjs/operators/creation).

## Disposing Observable Executions

```javascript
const subscription = observable.subscribe(x => console.log(x));
subscription.unsubscribe();
```

## Subscribing to an Observable

### With an Observer object

```javascript
const observer = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};

const subscription = observable.subscribe(observer);
```

### With a callback

```javascript
observable.subscribe(x => console.log('Observer got a next value: ' + x));
```

Internally in observable.subscribe, it will create an Observer object using the callback argument as the next handler.

## Creating a Subject

```javascript
const subject = new Subject();
```
