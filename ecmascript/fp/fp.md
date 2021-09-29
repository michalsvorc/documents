# Functional programming

Resources:

* [Functional-Light JavaScript](https://github.com/getify/Functional-Light-JS)
* [Beginner's guide to functional programming in JavaScript](https://opensource.com/article/17/6/functional-javascript)

Libraries:

* [Ramda](https://ramdajs.com)
* [Lodash FP](https://github.com/lodash/lodash/wiki/FP-Guide)

Immutable complex data structures:

* JS: `Object.freeze`
* TS: `Readonly<T>`, `ReadonlyArray<T>`, `ReadonlyMap<K, V>`, `ReadonlySet<T>`
* [Immutable.js](https://facebook.github.io/immutable-js/):
  * [List](https://facebook.github.io/immutable-js/docs/#/List),
  * [Stack](https://facebook.github.io/immutable-js/docs/#/Stack),
  * [Map](https://facebook.github.io/immutable-js/docs/#/Map),
  * [Set](https://facebook.github.io/immutable-js/docs/#/Set)

## Overview

* The arity of a function is the number of arguments that it accepts.
* Point-free is a style of writing code that eliminates unnecessary verbosity of mapping parameters ("points") to
  arguments, with the goal of making code easier to read/understand.

## Pure function

* Output calculated only from direct input.
* Returns same output based on the same input each time.
* Causes no side effects.

## Partial application

Partial application is a technique for reducing the arity (that is, the expected number of arguments to a function) by
creating a new function where some of the arguments are preset.

Currying is often used to do partial application, but it's not the only way.

The JavaScript language has a built-in mechanism for doing partial application without currying. This is done using the
[function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
method. See also [Functional Light
JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#bind).

## Currying

* [Functional Light JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#one-at-a-time)

Currying unwinds a single higher-arity function into a series of chained unary functions.

Currying is a special form of partial application, where a function that expects multiple arguments is broken down into
successive chained functions that each take a single argument (arity: 1) and return another function to accept the next
argument.

Once all arguments have been specified by these function calls, the original function is executed with all the collected
arguments.

The advantage of currying is that each call to pass in an argument produces another function that's more specialized,
and we can capture and use that new function later in the program. Partial application specifies all the partially
applied arguments up front, producing a function that's waiting for all the rest of the arguments on the next call.

Think about the order of arguments from least specific arguments to most specific arguments. The least specific argument
might be the data.

Both currying and partial application use closure to remember the arguments over time until all have been received, and
then the original function can be invoked.

## Point-free programming

* [Functional Light JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#no-points)

Point-free is a style of writing code that eliminates unnecessary verbosity of mapping parameters ("points") to
arguments, with the goal of making code easier to read/understand.

The term "point" here is referring to a function's parameter input.

```javascript
function double(x) {
    return x * 2;
}

[1,2,3,4,5].map( double ); // point-free style
```

## Loops

Use recursion and HOC instead of loops.

## Recursion

Use instead of loops, test for call stack exceeding.

## Higher order function (HOF)

* Excepts function as an argument
* Might return a new (enhanced) function

Examples:  filter, map, and reduce

## Function Composition

Function composition is the process of combining two or more functions to produce a new function. A composition of
functions `f` and `g` can be defined as `f(g(x))`, which evaluates from the inside out - right to left. 
