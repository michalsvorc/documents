# New features

Full overview:
* [New features - exploringjs.com](https://exploringjs.com/impatient-js/ch_new-javascript-features.html)
* []

* [Exploring ES2018 and ES2019 - exploringjs.com](https://exploringjs.com/es2018-es2019/toc.html)
* [Exploring ES2016 and ES2017 - exploringjs.com](https://exploringjs.com/es2016-es2017/)
* [ES6 - exploringjs.com](https://exploringjs.com/es6/)
* [ES6 features - github.com/lukehoban](https://github.com/lukehoban/es6features)

This is not an extensive list of new features, please visit the links above.

## Asynchronous iteration [ECMAScript 2018]

* [exploringjs.com](https://exploringjs.com/es2018-es2019/ch_asynchronous-iteration.html)

With ECMAScript 6, JavaScript got built-in support for synchronously iterating over data. But what about data that is
delivered asynchronously? For example, lines of text, read asynchronously from a file or an HTTP connection.

The asynchronous iteration protocol can be used directly or via `for-await-of` loop.

Normal (synchronous) generators help with implementing synchronous iterables. Asynchronous generators do the same for
asynchronous iterables.

An async generator returns a generator object. Each invocation of `next()` returns a Promise for an object `{value,
done}` that wraps a yielded value.

Alternatives to async iteration:

* Communicating Sequential Processes (CSP)
* Reactive programming (RxJS)

## Object.fromEntries() [ECMAScript 2019]

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries)

The `Object.fromEntries()` method takes a list of key-value pairs and returns a new object whose properties are given by those entries.

`Object.fromEntries()` performs the reverse of `Object.entries()`.

Usage:

* Converting a Map to an Object
* Converting an Array to an Object
* Object transformations: passing `Object.entries(object).map()` to `fromEntries()`

## Optional chaining (?.) [ECMAScript 2020]

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

The optional chaining operator provides a way to simplify accessing values through connected objects when it's possible
that a reference or function may be `undefined` or `null`.

## Nullish coalescing operator (??) [ECMAScript 2020]

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

The nullish coalescing operator (`??`) is a logical operator that returns its right-hand side operand when its left-hand
side operand is `null` or `undefined`, and otherwise returns its left-hand side operand. 

## Logical assignment operators [ECMAScript 2021]

* [exploringjs.com](https://exploringjs.com/impatient-js/ch_operators.html#logical-assignment-operators)
* [Logical OR assignment - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR_assignment)
* [Logical AND assignment - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND_assignment)
* [Logical nullish assignment - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_nullish_assignment)


| Operator    | Equivalent to   | Only assigns if a is  |

|-------------|-----------------|-----------------------|

| `a ||= b`   | `a || (a = b)`  | Falsy                 |

| `a &&= b`   | `a && (a = b)`  | Truthy                |

| `a ??= b`   | `a ?? (a = b)`  | Nullish               |

|-------------|-----------------|-----------------------|

