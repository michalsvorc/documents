# Asynchronicity

* [Asynchronous JavaScript - MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)
* [Asynchronous programming in JavaScript - exploringjs.com](https://exploringjs.com/impatient-js/ch_async-js.html)
* [(Video) Javascript async/await, promises & callbacks](https://www.youtube.com/watch?v=RXLS5qqkEfQ)
* [Asynchronous iteration - exploringjs.com](https://exploringjs.com/impatient-js/ch_async-iteration.html)

JavaScript is a single-threaded, synchronous and blocking language.

Non-blocking and asynchronous execution is possible with the Javascript engine, which has Web APIs (or C wrappers in
case of Node.js) that handle these tasks in the background.

Asynchronous code:

* Async callbacks (e.g.
  [addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) argument)
* Promises
* async/await

## Threads

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Thread)

A thread is basically a single process that a program can use to complete tasks. Each thread can only do a single task
at once.

JavaScript is traditionally single-threaded. Even with multiple cores, you could only get it to run tasks on a single
thread, called the [main thread](https://developer.mozilla.org/en-US/docs/Glossary/Main_thread).

Only one thing can happen at a time, on a single main thread, and everything else is blocked until an operation
completes.

*Web workers* allow you to send some of the JavaScript processing off to a separate thread called a worker.

## Concurrency model 

* [Concurrency model and the event loop - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#event_loop)
* [Event loop - exploringjs.com](https://exploringjs.com/impatient-js/ch_async-js.html#the-event-loop)
* [(Video) Javascript event loop, stack & queue](https://www.youtube.com/watch?v=4xsvn6VUTwQ)

### Call stack

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Call_stack)

FILO datastructure.

A call stack is a mechanism for an interpreter (like the JavaScript interpreter in a web browser) to keep track of its
place in a script that calls multiple functions - what function is currently being run and what functions are called
from within that function, etc.

When a JavaScript runtime encounters an asynchronous function in the call stack, it returns immediately and the
asynchronous process continues in the JavaScript engine APIs. 

A callback is then added to the message queue, when the operation from an API is completed.

Once the call stack is empty, then the event loop will grab that callback out of the message queue and add it to the
call stack to run it.

### Message Queue / Event Queue / Callback Queue

Each message is associated with a function as a callback or an event.

### Event loop

The event loop's job is to continually watch the call stack and the message queue. When the call stack becomes empty,
it checks the message queue to see if there's any messages waiting to be processed. 

If they are, it puts them into the call stack one at a time and executes them.

### ES6 Job queue

ECMAScript 2015 introduced the concept of the Job Queue, which is used by Promises (also introduced in ES6/ES2015).
It's a way to execute the result of an async function as soon as possible, rather than being put at the end of the call
stack. Promises that resolve before the current function ends will be executed right after the current function.

## Timeouts and intervals

* [MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Timeouts_and_intervals)

The specified amount of time (or the delay) is not the guaranteed time to execution, but rather the minimum time to the
execution. As a consequence, code like `setTimeout(fn, 0)` will execute as soon as the stack is empty, not immediately.

* [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout): Execute a
specified block of code once after a specified time has elapsed.

* [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval): Execute a
specified block of code repeatedly with a fixed time delay between each call.

* [requestAnimationFrame()](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame): The modern
  version of `setInterval()`. Executes a specified block of code before the browser next repaints the display, allowing
  an animation to be run at a suitable frame rate regardless of the environment it is being run in.

## Promises

* [Promise - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
* [Promises for asynchronous programming [ES6] -
  exploringjs.com](https://exploringjs.com/impatient-js/ch_promises.html)
* [States and Fates: Terminology](https://github.com/domenic/promises-unwrapping/blob/master/docs/states-and-fates.md)
* [Tips for chaining Promises -
  exploringjs.com](https://exploringjs.com/impatient-js/ch_promises.html#tips-for-chaining-promises)

A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers
with an asynchronous action's eventual success value or failure reason. 

The Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting
value.

### States and Fates

* [Promises unwrapping](https://github.com/domenic/promises-unwrapping/blob/master/docs/states-and-fates.md)

* States: pending; fulfilled, rejected
* Fates: unresolved; resolved

We say that a promise is *settled* if it is not pending (if it is either fulfilled or rejected). Being settled is
not a state, just a linguistic convenience.

A promise can be *resolved to* either a promise or thenable, in which case it will store the promise or thenable for
later unwrapping; or it can be resolved to a non-promise value, in which case it is fulfilled with that value.

### Promise() constructor - JavaScript | MDN

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise)

```js
new Promise(executor)
```

Executor function:

```js
function(resolutionFunc, rejectionFunc){
  // typically, some asynchronous operation.
}
```

When called via `new`, the Promise constructor returns a promise object. The promise object will become *resolved* when
either of the functions `resolutionFunc` or `rejectionFunc` are invoked.

`resolutionFunc` and `rejectionFunc` are also functions, and you can give them whatever actual names you want. Their signatures are simple: they accept a single parameter of any type.

```js
resolutionFunc(value) // call on resolved
rejectionFunc("reason") // call on rejected
```

About the executor, it’s important to understand the following:

* The executor return value is ignored.
* If an error is thrown in the executor, the promise is *rejected*.

```js
const myFirstPromise = new Promise((resolve, reject) => {
  // do something asynchronous which eventually calls either:
  //
  //   resolve(someValue)        // fulfilled
  // or
  //   reject("failure reason")  // rejected
});
```

### promise.then(), promise.catch(), and promise.finally()

* [Promise.prototype.then()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
* [Promise.prototype.catch()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)
* [Promise.prototype.finally()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally)

These methods are used to associate further action with a promise that becomes *settled*.

The `.then()` callback is only executed if somePromise is *fulfilled*.

The `.catch()` callback is only executed if:

* either the initial Promise is *rejected*,
* or the `.then()` callback returns a rejected Promise,
* or the `.then()` callback throws an exception.

We can chain the Promise methods `.then()` and `.catch()` because they both return Promises. Catch is actually a shortcut for `.then(undefined, onRejected)`.

The `.finally()` callback is always executed - independently of somePromise and the values returned by `.then()` and/or
`.catch()`.

`.finally()` ignores what its callback returns and simply passes on the settlement that existed before it was called.
If, however, the `.finally()` callback throws an exception, the Promise returned by `.finally()` is rejected.

### Promise combinator functions: working with Arrays of Promises

* [Quick reference: Promise combinator functions](https://exploringjs.com/impatient-js/ch_promises.html#quick-reference-promise-combinator-functions)

#### Promise.all()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

The `Promise.all()` method takes an iterable of promises as an input, and returns a single Promise that resolves to an
array of the results of the input promises.

This returned promise will resolve when all of the input's promises have resolved, or if the input iterable contains no
promises.

`Promise.all()` will reject immediately upon any of the input promises rejecting. It rejects immediately upon any of the
input promises rejecting or non-promises throwing an error, and will reject with this first rejection message / error.

*Use case*: It is typically used when there are multiple related asynchronous tasks that the overall code relies on to
work successfully - all of whom we want to fulfill before the code execution continues.

In comparison, the promise returned by `Promise.allSettled()` will wait for all input promises to complete, regardless
of whether or not one rejects.

#### Promise.allSettled() [ES2020]

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)

The `Promise.allSettled()` method returns a promise that resolves after all of the given promises have either
*fulfilled* or *rejected*, with an array of objects that each describes the outcome of each promise.

*Use case*: It is typically used when you have multiple asynchronous tasks that are not dependent on one another to
complete successfully, or you'd always like to know the result of each promise.

In comparison, the Promise returned by `Promise.all()` may be more appropriate if the tasks are dependent on each other
/ if you'd like to immediately reject upon any of them rejecting.

`[{status: "fulfilled", value: 1}, {status: "rejected",  reason: Error: an error}, ...]`

For each outcome object, a `status` string is present. If the status is fulfilled, then a `value` is present. If the
status is rejected, then a `reason` is present.

#### Promise.race()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

The `Promise.race()` method returns a promise that fulfills or rejects as soon as one of the promises in an iterable
fulfills or rejects, with the value or reason from that promise.

The race function returns a Promise that is settled the same way (and takes the same value) as the first promise that
settles amongst the promises of the iterable passed as an argument.

*Use case*: Reacting to the first settlement among multiple Promises.

#### Promise.any() [ES2021]

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any)

`Promise.any()` takes an iterable of Promise objects and, as soon as one of the promises in the iterable fulfills,
returns a single promise that resolves with the value from that promise. If no promises in the iterable fulfill (if all
of the given promises are rejected), then the returned promise is rejected with an AggregateError, a new subclass of
Error that groups together individual errors.

This method is useful for returning the first promise that fulfills. It short-circuits after a promise fulfills, so it
does not wait for the other promises to complete once it finds one. 

*Use case*: Among several asynchronous computations, we are only interested in the first successful one. That is, we are
trying several approaches and the fastest one should win.

Unlike `Promise.all()`, which returns an *array of fulfillment* values, we only get *one fulfillment* value (assuming at
least one promise fulfills).

Also, unlike `Promise.race()`, which returns the first *settled* value (either fulfillment or rejection), this method
returns the *first fulfilled* value. 

## async/await functions

* [async function - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
* [Async functions - exploringjs.com](https://exploringjs.com/impatient-js/ch_async-functions.html)
* [Concurrency and await -
  exploringjs.com](https://exploringjs.com/impatient-js/ch_async-functions.html#concurrency-and-await)

The `async` and `await` keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding
the need to explicitly configure promise chains. Use of async and await enables the use of ordinary `try/catch` blocks
around asynchronous code.

Async functions always return a promise. If the return value of an async function is not explicitly a promise, it will
be implicitly wrapped in a promise.

* Any value that is returned (explicitly or implicitly) is used to fulfill the Promise.
* Any exception that is thrown is used to reject the Promise.

### Await

Top-level code, up to and including the first `await` expression (if there is one), is run synchronously. In this way,
an async function without an await expression will run synchronously.

If there is an `await` expression inside the function body, however, the async function will always complete
asynchronously.

Inside the body of an async function, we write Promise-based code as if it were synchronous. We only need to apply the
await operator whenever a value is a Promise. That operator pauses the async function and resumes it once the Promise is
settled:

* If the Promise is fulfilled, await returns the fulfillment value.
* If the Promise is rejected, await throws the rejection value.

