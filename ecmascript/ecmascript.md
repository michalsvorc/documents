# ECMAScript

Overview:

* [A re-introduction to JavaScript -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)
* [JavaScript Recap - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/recap)
* [JavaScript Deep Dive - github.com/romainl](https://gist.github.com/romainl/db0142bf4f38109b04104f205abcbde7)

Reference:

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
* [JavaScript for impatient programmers - exploringjs.com](https://exploringjs.com/impatient-js/toc.html)

Topics:

* [Standard built-in objects - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
* [Expressions and operators - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators)
* [Scope & Closures - You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS)
* [(Video) Stack & Event loop - youtube.com](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

New features:

* [New JavaScript features - exploringjs.com](https://exploringjs.com/impatient-js/ch_new-javascript-features.html)

Resources:

* [Reference Books](https://github.com/codesONLY/JavaScriptONLY/tree/master/ReferenceBooks)

## Data types and data structures

* [Data structures - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
* [Typeof operator - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)

### Primitives

Data Types that are primitives, checked by `typeof` operator:

* [undefined](https://developer.mozilla.org/en-US/docs/Glossary/undefined): `typeof instance === "undefined"`
* [Boolean](https://developer.mozilla.org/en-US/docs/Glossary/Boolean): `typeof instance === "boolean"`
* [Number](https://developer.mozilla.org/en-US/docs/Glossary/Number): `typeof instance === "number"`
* [String](https://developer.mozilla.org/en-US/docs/Glossary/String): `typeof instance === "string"`
* [BigInt](https://developer.mozilla.org/en-US/docs/Glossary/BigInt): `typeof instance === "bigint"`
* [Symbol](https://developer.mozilla.org/en-US/docs/Glossary/Symbol): `typeof instance === "symbol"`

### Structural types

* [Object - MDN](https://developer.mozilla.org/en-US/docs/Glossary/Object)
* [The constructor - MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects#the_constructor)
* [New keyword - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new).

Special non-data but Structural type for any constructed object instance, and almost everything made with `new` keyword:

* new [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
* new [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
* new [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
* new [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
* new [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
* new [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)
* new [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)

`typeof <structural_type> === "object"`

### Functions

* [Function - MDN](https://developer.mozilla.org/en-US/docs/Glossary/Function) 

A non-data structure, though it also answers for the typeof operator: `typeof instance === "function"`. This is merely a
special shorthand for Functions, though every Function constructor is derived from an Object constructor.

### Structural root primitive

* [null - MDN](https://developer.mozilla.org/en-US/docs/Glossary/Null) 

(!) `typeof instance === "object"`

Special primitive type having additional usage for its value: if object is not inherited, then null is shown;

## Falsy values

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)

There are 6 falsy values:

* false
* 0
* "" (empty string)
* undefined
* null
* NaN

## Strict mode 

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

* Eliminates some JavaScript silent errors by changing them to throw errors.
* Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes
  be made to run faster than identical code that's not strict mode.
* Prohibits some syntax likely to be defined in future versions of ECMAScript.
* Prevents `this` to reference a global object in the global execution context. The global object is not eligible for
  the default binding, so the `this` is instead set to `undefined`. 
* The body of a class is executed in strict mode by default.

## Regular expressions

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#creating_a_regular_expression)

You construct a regular expression in one of two ways:

* regular expression literal: `/ab+c/`
* constructor function of the RegExp object: `new RegExp('ab+c')`

Regular expression literals provide compilation of the regular expression when the script is loaded. If the regular
expression remains constant, using this can improve performance.

Using the constructor function provides runtime compilation of the regular expression. Use the constructor function when
you know the regular expression pattern will be changing, or you don't know the pattern and are getting it from another
source, such as user input.

## Decimal calculations

Binary floating point numbers do not map correctly to Decimal numbers:

`console.log(.1 + .2); // 0.30000000000000004`

Whenever you use math for financial calculations (e.g. GST calculation, money with cents, addition etc) use a library like[ big.js](https://github.com/MikeMcl/big.js/) which is designed for perfect decimal math and safe out of bound integer values.

## The !! pattern

Quite commonly it helps to be explicit that the intent is to treat the value as a boolean and convert it into a true
boolean (one of `true|false`). You can easily convert values to a true boolean by prefixing it with `!!`.

## Set

* [Set - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
* [Examples - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set#examples):

Set objects are collections of unique ordered values. You can iterate through the elements of a set in insertion order.
A value in the Set may only occur once; it is unique in the Set's collection. The Set object lets you store unique
values of any type, whether primitive values or object references.

* [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)

WeakSets are collections of objects only. They cannot contain arbitrary values of any type, as Sets can. If no other
references to an object stored in the WeakSet exist, those objects can be garbage collected. This also means that there
is no list of current objects stored in the collection. WeakSets are not enumerable.

## Map

* [Map - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
* [Objects vs. Maps -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps)

The Map object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and
primitive values) may be used as either a key or a value. A Map object iterates its elements in insertion order.

* [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)

Keys of WeakMaps are of the type Object only. Primitive data types as keys are not allowed (e.g. a Symbol can't be a
WeakMap key). Because the references are weak, WeakMap keys are not enumerable. 

## Arrow function expressions

* [Arrow function expressions - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
* [Arrow functions used as methods - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arrow_functions#arrow_functions_used_as_methods)

Differences & Limitations:

* Does not have its own bindings to `this` or `super`, and should not be used as a method.
* Does not have function [arguments object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments), or [new.target](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target) keywords.
* Not suitable for call, apply and bind methods, which generally rely on establishing a [scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope).
* Can not be used as [constructors](https://developer.mozilla.org/en-US/docs/Glossary/Constructor).
* Can not use [yield](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield), within its body.

Arrow functions do not bind their own `this`, they inherit the one from the parent scope instead, which is called
*lexical scoping*: they will lexically go up a scope, and use the value of `this` in the scope in which it was defined.

## Loops

Overview:

* [Loops and iteration - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)

Types:

* [for](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)
* [do...while](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while)
* [while](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)
* [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
* [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

Operators:

* [break](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/break)
* [continue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/continue)
* [label](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label)

### Difference between for...of and for...in

* [Difference - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of#difference_between_for...of_and_for...in)
* [Iteration protocols - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)
* [Enumerability and ownership of properties - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)
* [Why Use for...in? - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in#why_use_for...in)

* The `for...of` statement creates a loop iterating over *iterable objects*: built-in String, Array, array-like objects (e.g., arguments or NodeList), TypedArray, Map, Set, and user-defined iterables. It invokes a custom iteration hook with statements to be executed for the *value* of each distinct property of the object.
* The `for...in` statement iterates in an arbitrary order over all enumerable *properties* of an object that is keyed by strings (ignoring ones keyed by Symbols), including inherited enumerable properties. It may be most practically used for debugging purposes, being an easy way to check the properties of an object (by outputting to the console or otherwise).

### Iteration over Arrays

`for...in` should not be used to iterate over an Array where the index order is important.

When iterating over arrays where the order of access is important, it is better to use one of: 

* `for` loop
* `Array.prototype.forEach()` method
* `for...of` loop

### Iteration protocols

* [Iteration protocols - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)
* [Iterators and generators - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)
* [Built-in iterables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#built-in_iterables)

An *iterable* is an object whose contents can be traversed sequentially. Built-in iterables:

* String
* Array
* TypedArray
* Map
* Set

*Object* is not a built-in iterable. To iterate over the properties of objects, you need helpers such as `Object.keys()` and `Object.entries()`.

* The *iterable protocol* allows JavaScript objects to define or customize their iteration behavior. The protocol is not
  meant to be used directly - it is meant to be used via higher-level language constructs built on top of it.
* An *iterator* is the pointer used for the traversal.
* The *iterator protocol* defines a standard way to produce a sequence of values (either finite or infinite), and
  potentially a return value when all values have been generated. An object is an iterator when it implements a `next()`
  method and returns `{ value: <any>, done: <boolean> }` object.

## Generator

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)

Generators are functions that can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances.

The *Generator object* is returned by a *generator function* and it conforms to both the iterable protocol and the iterator protocol.

This object cannot be instantiated directly. Instead, a Generator instance can be returned from a generator function.


* `Generator.prototype.next()`: Returns a value yielded by the `yield` expression.
* `Generator.prototype.return()`: Returns the given value and finishes the generator.
* `Generator.prototype.throw()`: Throws an error to a generator (also finishes the generator, unless caught from within
  that generator).

### Generator function

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)

The `function*` declaration defines a *generator function*, which returns a *Generator object*. 

### yield keyword

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield)
* [`yield*` - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield*)

The `yield` keyword pauses generator function execution and the value of the expression following the `yield` keyword is
returned to the generator's caller. It can be thought of as a generator-based version of the `return` keyword.

Once paused on a `yield` expression, the generator's code execution remains paused until the generator's `next()` method is
called. Each time the generator's `next()` method is called, the generator resumes execution, and runs until it reaches
one of the following:

* `yield`
* `throw`
* a `return` statement is reached
* the end of the generator function is reached

The `yeld*` expression is used to delegate to another generator or iterable object.

## Error types

* [Error - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
* [Exception Handling - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/exceptions#error-sub-types)

* [SyntaxError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SyntaxError)

Creates an instance representing a syntax error. Syntax errors represent faults in the program that stop it from even
starting execution. 

* [TypeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError)

Creates an instance representing an error that occurs when a variable or parameter is not of a valid type. Type errors
represent faults that arise during program execution.

* [ReferenceError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError)

Creates an instance representing an error that occurs when dereferencing an invalid reference.

* [RangeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RangeError)

Creates an instance representing an error that occurs when a numeric variable or parameter is outside of its valid range.

* [URIError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/URIError)

Creates an instance representing an error that occurs when `encodeURI()` or `decodeURI()` are passed invalid parameters.

* [AggregateError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/AggregateError)

Creates an instance representing several errors wrapped in a single error when multiple errors need to be reported by an
operation, for example by `Promise.any()`.

* [EvalError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/EvalError)

Creates an instance representing an error that occurs regarding the global function `eval()`.

## Modules

* [Modules - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
* [The Module Pattern - You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch8.md)
* [Modules - TypeScript](https://www.typescriptlang.org/docs/handbook/modules.html)

ES Modules (ESM) are file-based, and module instances are singletons, with everything private by default. One notable
difference is that ESM files are assumed to be strict-mode, without needing a "use strict" pragma at the top. There's no
way to define an ESM as non-strict-mode.

### Visibility

Any file containing a top-level `import` or `export` is considered a module. Conversely, a file without any top-level
import or export declarations is treated as a script whose contents are available in the global scope (and therefore to
modules as well).

Modules are executed within their own scope, not in the global scope. This means that variables, functions, classes,
etc. declared in a module are not visible outside the module unless they are explicitly exported using one of the export
forms. Conversely, to consume a variable, function, class, interface, etc. exported from a different module, it has to
be imported using one of the import forms.


* Import a module for side-effects only: `import "./my-module.js";`
* Loading modules dynamically via import() (ES2020): [Exploring JS](https://exploringjs.com/impatient-js/ch_modules.html#dynamic-imports)
