# Event loop

Overview:

* [The Node.js Event Loop - nodejs.dev](https://nodejs.dev/learn/the-nodejs-event-loop)
* [Timers API](https://nodejs.org/api/timers.html)
* [(Video) Morning Keynote - Bert Belder, IBM](https://www.youtube.com/watch?v=PNa9OMajw9w)
* [The Node.js Event Loop - nodejs.org](https://nodejs.org/uk/docs/guides/event-loop-timers-and-nexttick/)

Topics:

* [What exactly is a Node.js event loop tick? - stackoverflow.com](https://stackoverflow.com/questions/19822668/what-exactly-is-a-node-js-event-loop-tick)
* [Don't Block the Event Loop (or the Worker Pool) - nodejs.org](https://nodejs.org/en/docs/guides/dont-block-the-event-loop/)

## Overview

The event loop is what allows Node.js to perform non-blocking I/O operations - despite the fact that JavaScript is
single-threaded - by offloading operations to the system kernel whenever possible.

Almost all the I/O primitives in JavaScript are non-blocking. This means network requests, filesystem operations, and so
on. Being blocking is the exception, and this is why JavaScript is based so much on callbacks, and more recently on
promises and async/await.

Concurrency refers to the event loop's capacity to execute JavaScript callback functions after completing other work.
Any code that is expected to run in a concurrent manner must allow the event loop to continue running as non-JavaScript
operations, like I/O, are occurring.

Web Workers run in their own loop.

## Phases

* [Documentation](https://nodejs.org/uk/docs/guides/event-loop-timers-and-nexttick/#phases-overview)

Each phase has a FIFO queue of callbacks to execute. When the event loop enters a given phase, it will perform any
operations specific to that phase, then execute callbacks in that phase's queue until the queue has been exhausted or
the maximum number of callbacks has been executed. 

* timers: This phase executes callbacks scheduled by `setTimeout()` and `setInterval()`. A timer specifies the threshold
  after which a provided callback may be executed rather than the exact time a person wants it to be executed. 
* pending callbacks: Executes I/O callbacks deferred to the next loop iteration.
* (idle, prepare): Only used internally.
* poll: Retrieve new I/O events; execute I/O related callbacks (almost all with the exception of close callbacks, the
  ones scheduled by timers, and `setImmediate()`); Node will block here when appropriate.
* check: `setImmediate()` callbacks are invoked here.
* close callbacks: some close callbacks, e.g. `socket.on('close', ...)`.

### The poll phase

* [Documentation](https://nodejs.org/uk/docs/guides/event-loop-timers-and-nexttick/#poll)

The poll phase has two main functions:

1. Calculating how long it should block and poll for I/O.
2. Processing events in the poll queue.

When the event loop enters the poll phase and there are no timers scheduled, one of two things will happen:

* If the poll queue is not empty, the event loop will iterate through its queue of callbacks executing them
  synchronously until either the queue has been exhausted, or the system-dependent hard limit is reached.
* If the poll queue is empty, one of two more things will happen:
  - If scripts have been scheduled by `setImmediate()`, the event loop will end the poll phase and continue to the
    *check phase* to execute those scheduled scripts.
  - If scripts have not been scheduled by `setImmediate()`, the event loop will wait for callbacks to be added to the
    queue, then execute them immediately.

Once the poll queue is empty the event loop will check for timers whose time thresholds have been reached. If one or
more timers are ready, the event loop will wrap back to the timers phase to execute those timers' callbacks.

## setTimeout

* [API](https://nodejs.org/api/timers.html#timers_settimeout_callback_delay_args)

`setTimeout(callback[, delay[, ...args]])`

Schedules execution of a one-time callback after delay milliseconds.

## setImmediate

* [API](https://nodejs.org/api/timers.html#timers_setimmediate_callback_args)
* [Documentation](https://nodejs.dev/learn/understanding-setimmediate)
* [setImmediate() vs setTimeout()](https://nodejs.org/uk/docs/guides/event-loop-timers-and-nexttick/#setimmediate-vs-settimeout)

`setImmediate(callback[, ...args])`

When you want to execute some piece of code asynchronously, but as soon as possible, one option is to use the
`setImmediate()` function.

`setImmediate()` schedules the "immediate" execution of the callback after I/O events' callbacks.

A `setTimeout()` callback with a 0ms delay is very similar to `setImmediate()`. The execution order will depend on
various factors, but they will be both run in the next iteration of the event loop.

The main advantage to using `setImmediate()` over setTimeout() with 0 is that `setImmediate()` will always be executed
before any timers if scheduled within an I/O cycle, independently of how many timers are present.

`setImmediate()` is also easier to reason about than `setTimeout()` with 0.

## process.nextTick

* [API](https://nodejs.org/api/process.html#process_process_nexttick_callback_args)
* [Documentation](https://nodejs.dev/learn/understanding-process-nexttick)

`process.nextTick(callback[, ...args])`

Every time the event loop takes a full trip, we call it a tick.

When we pass a function to `process.nextTick()`, we instruct the engine to invoke this function at the end of the current
operation, before the next event loop tick starts.

Use `nextTick()` when you want to make sure that in the next event loop iteration that code is already executed.

`process.nextTick()` is not technically part of the event loop. Instead, the nextTickQueue will be processed after the
current operation is completed, *regardless* of the current phase of the event loop.

A function passed to `process.nextTick()` is going to be executed on the current iteration of the event loop, after the
current operation ends. This means it will always execute before `setTimeout` and `setImmediate`.

There are two main reasons to use `nextTick()`:

1. Allow users to handle errors, cleanup any then unneeded resources, or perhaps try the request again before the event
   loop continues.
2. At times it's necessary to allow a callback to run after the call stack has unwound but before the event loop
   continues.

