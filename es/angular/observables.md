
# Documentation



* [The RxJS library](https://angular.io/guide/rx-library)
* [Top 10 RxJs Operators in Angular [Angular Series]](https://www.youtube.com/watch?v=5TnWFaI49aw)

# [Observables in Angular](https://angular.io/guide/observables-in-angular)



* You can define [custom events](https://angular.io/guide/event-binding#custom-events-with-eventemitter) that send observable output data from a child to a parent component.
* The HTTP module uses observables to handle AJAX requests and responses.
* The Router and Forms modules use observables to listen for and respond to user-input events.

# [Naming conventions for observables (value$)](https://angular.io/guide/rx-library#naming-conventions-for-observables)

Although the Angular framework does not enforce a naming convention for observables, you will often see observables named with a trailing “$” sign: `observable$`

```js


```
 stopwatchValue: number;
 stopwatchValue$: Observable<number>;
```


```

# [Using observables to pass values](https://angular.io/guide/observables)

```js


<table>
  <tr>
   <td><code>const subscriberFn(observer => { \
  observer.next('Hello') \
  observer.complete(); \
 \
  return {unsubscribe() {}}; \
})</code>
<p>
<code> \
const observable = new Observable(subscriberFn); \
 \
const observer = observable.subscribe({ \
  next(message) { console.log(message); }, \
  complete() { console.log('Finished'); } \
});</code>
   </td>
  </tr>
  <tr>
   <td>
   </td>
  </tr>
</table>


```

## [Multicasting](https://angular.io/guide/observables#multicasting)

Multicasting is the practice of broadcasting to a list of multiple subscribers in a single execution. With a multicasting observable, you don't register multiple listeners on the document, but instead re-use the first listener and send values out to each subscriber.

