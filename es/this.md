# this

* [this - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
* [Demystifying JavaScript this Keyword with Practical Examples](https://www.javascripttutorial.net/javascript-this/)
* [(PDF) This and Object Prototypes](https://tinyurl.com/9fhspmjr)

`this` is neither a reference to the function itself, nor is it a reference to the function’s lexical scope.

`this` is actually a binding that is made when a function is invoked, and what it references is determined entirely by
the *call-site* where the function is called.

To understand `this` binding, we have to understand the *call-site*: the location in code where a function is *called*, not
where it’s declared. `this` is a runtime binding, not an author-time binding.

`this` references the object that is currently *calling* the function.

## Execution context

When a function is invoked, an activation record, otherwise known as an *execution context*, is created.

This record contains information about where the function was called from (the *call-stack*), how the function was
invoked, what parameters were passed, etc.

One of the properties of this record is the `this` reference, which will be used for the duration of that function’s
execution.

## Default binding

```js
foo(); 
```

Standalone function invocation: the function is called with a plain, undecorated function reference. Think of this rule
as the default catch-all rule when none of the other rules apply.

## Implicit binding

```js
obj.foo(); 
```

Regardless of whether `foo` is initially declared on `obj`, or is added as a reference later, in neither case is the
function really owned or contained by the `obj` object.

When there is a context object for a function reference, the implicit binding rule says that it’s that object that
should be used for the function call `this` binding. 

Beware:

```js
var bar = obj.foo;
bar()     // undefined or global object
```

Even though `bar` appears to be a reference to `obj.foo`, in fact, it’s really just another reference to `foo` *itself*.

Moreover, the *call-site* is what matters, and the call-site is `bar()`, which is a plain, undecorated call, and thus
the *default binding* applies.

## Explicit Binding

### bind

* [Function.prototype.bind() -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)

`bind(thisArg, arg1, ... , argN)`

`thisArg`: The value to be passed as the `this` parameter to the target function when the bound function is called.
`arg1, arg2, ...argN`: Optional, arguments to prepend to arguments provided to the bound function when invoking func.

Returns: A copy of the given function with the specified `this` value, and initial arguments (if provided).

### call and apply

* [Function.prototype.call() -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
* [Function.prototype.apply() -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

```js
apply(thisArg, argsArray)
call(thisArg, arg1, ... , argN)
```

* The `call()` method calls a function with a given `this` value and arguments provided individually.
* The `apply()` method calls a function with a given `this` value, and arguments provided as an array.

Returns: The result of calling the function with the specified `this` value and arguments.

## Global execution context

In the global context, the `this` references the [global object](https://www.javascripttutorial.net/es-next/javascript-globalthis/), which is the `window` object on the Web browser or `global` object on Node.js.

If *strict mode* is in effect, the global object is not eligible for the default binding, so the `this` is instead set
to `undefined`.
 
## Function context

In *strict mode*, however, if the value of `this` is not set when entering an execution context, it remains `undefined`.

In JavaScript, you can invoke a function in the following ways:

* [Function invocation](https://www.javascripttutorial.net/javascript-this/#function_invocation)
* [Method invocation](https://www.javascripttutorial.net/javascript-this/#method_invocation)
* [Constructor invocation](https://www.javascripttutorial.net/javascript-this/#constructor_invocation)
* [Indirect invocation](https://www.javascripttutorial.net/javascript-this/#indirect_invocation)

Each function invocation defines its own context, therefore, the `this` behaves differently than you may expect.

### Constructor invocation

When you use the `new` keyword to create an instance of a function object, you use the function as a constructor.
JavaScript creates a new object and sets `this` to the newly created object.

```js
function Car(brand) {
  this.brand = brand;
}

var car = new Car('A');

console.log(car.brand);   // A
```

Calling a function without the `new` keyword sets this to a global object, because the function was executed in a global
context.


```js
var car = Car('B')

console.log(car.brand); 	// TypeError: car is undefined

console.log(window.brand); // B in nons-strict mode
```

## Lexical this (arrow functions) 

* [Arrow function expressions [ES6] -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

Instead of using the standard `this` rules, arrow-functions adopt the `this` binding from the enclosing (lexical) scope.

While arrow-functions provide an alternative to using `bind()` on a function to ensure its `this`, which can seem
attractive, it’s important to note that they essentially are disabling the traditional `this` mechanism in favor of more
widely understood lexical scoping. 

## this in constructor functions

This points to an object when used in a constructor function with the [new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) keyword.

```js
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}

const car1 = new Car('Eagle', 'Talon TSi', 1993);
```

## self in the browser environment

* [window.self - MDN](https://developer.mozilla.org/en-US/docs/Web/API/window.self), which is different to `this`.

Unless set elsewhere, the value of `self` is `window` because JavaScript lets you access any property `x` of a `window`
as simply `x`, instead of `window.x`. Therefore, self is really `window.self`, which is different to `this`.

## globalThis

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis)

The `globalThis` property provides a standard way of accessing the global `this` value (and hence the global object
itself) across environments.

Global object in different environments:

* web browser: `window`, `self`, `frames`
* web workers: `self`
* Node.js: `global`

## Summary

Determining the `this` binding for an executing function requires finding the direct *call-site* of that function. 

Once examined, four rules can be applied to the call-site, in this order of precedence:

1. Called with `new`? Use the newly constructed object.
2. Called with `call` or `apply, bind`? Use the specified object.
3. Called with a context object owning the call? Use that context object.
4. Default: undefined in strict mode, global object otherwise.
