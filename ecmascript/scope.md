# Scope

* [Scope - MDN](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
* [Scope & Closures - You Don't Know JS Yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/README.md)
* [Shadowing - You Don't Know JS Yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch3.md#shadowing)

The four scopes are:

1. Global: visible by everything
2. Function: visible within a function (and its sub-functions and blocks)
3. Block: visible within a block (and its sub-blocks)
4. Module: visible within a module

## Keywords

```js
var x;                      // Declaration
x = 1;                      // Initialization
var num = 1;                // variable statement with assignment

function main() { ... }     // Function declaration
var main = function() {...} // Function expression
```

* Scope: The current context of execution. Defines the area, where functions, variables and such are available. 
* Scope chain: The connections between scopes that are nested within other scopes is called the scope chain, which
  determines the path along which variables can be accessed. The chain is directed, meaning the lookup moves
  upward/outward only.
* Lexical scope: JS scopes are lexical scopes, meaning they are defined during lexing step.
* Hoisting: Registering a variable at the beginning of a scope. A variable being visible from the beginning of its
  enclosing scope, even though its declaration may appear further down in the scope.

## Lexical scope

* [You Don't Know JS Yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md#lexical-scope)

JavaScript has *lexical* (also called static) scoping and closures. This means you can tell the scope of an identifier
by looking at the source code.

Processing of JS programs occurs in (at least) two phases: 

1. compilation/lexing/parsing
2. execution

JS's scope is determined at compile time; the term for this kind of scope is "lexical scope". The term "lexical" refers
to the first stage of compilation (lexing/parsing). 

Compilation defines all the scopes (aka, "lexical environments") and registers all the identifiers (variables) for each
scope. 

While scopes are identified during compilation, they're not actually created until runtime.

One of the key aspects of lexical scope is that any time an identifier reference cannot be found in the current scope,
the next outer scope in the nesting is consulted; that process is repeated until an answer is found or there are no more
scopes to consult.

When Engine exhausts all lexically available scopes (moving outward) in the scope chain and still cannot resolve the
lookup of an identifier, an error condition then exists. 

### Lexical scope and functions

A lexical scope in JavaScript means that a variable defined outside a function can be accessible inside another function
defined after the variable declaration. But the opposite is not true; the variables defined inside a function scope will
not be accessible outside that function.

Lexical Scoping defines how variable names are resolved in nested functions: inner functions contain the scope of parent
functions even if the parent function has returned. The last part: "even if the parent function has returned" is called
*Closure*. 

### Loops

* [MDN](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch5.md#loops)

All the rules of scope are applied per scope instance. In other words, each time a scope is entered during execution,
everything resets. Each loop iteration is its own new scope instance, and within each scope instance.

## Variables

Outside of the special cases of global and module scope, variables are declared using:

* `var`: Function scope
* `let/const`: Block scope

Most other forms of identifier declaration have block scope in strict mode.

### var

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)

Properties:

* function scoped, ignore block scope
* hoisted
* attached to the global object (e.g.: window.x)
* can be redeclared

`var` declarations are accessible anywhere within their containing function, module, namespace, or global scope
regardless of the containing block.

### let, const

* [let - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
* [const - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

Properties:

* block-scoped
* not hoisted (technically hoisted but never initialized resulting to reference error, see TDZ)
* doesn’t affect the global object
* const value assignment can’t be changed, except for the content of objects and arrays

When a variable is declared using `let/const`, it uses what some call lexical-scoping or block-scoping. Unlike variables
declared with `var` whose scopes leak out to their containing function, block-scoped variables are not visible outside
of their nearest containing block or for-loop.

`const` is an augmentation of let in that it prevents re-assignment to a variable.

## Hoisting

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
* [You Don't Know JS
  Yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch5.md#hoisting-yet-another-metaphor)

The term most commonly used for a variable being visible from the beginning of its enclosing scope, even though its
declaration may appear further down in the scope, is called hoisting. It means that a variable can be used before it is
declared without throwing an error.

The typical assertion of what hoisting means: *lifting* any identifiers all the way to the top of a scope.

The explanation often asserted is that the JS engine will actually (rewrite) that program before execution. The JS
engine doesn't actually rearrange the code. It can't magically look ahead and find declarations; the only way to
accurately find them, as well as all the scope boundaries in the program, would be to fully parse the code.

Instead, the variable and function declarations are put into memory during the compile phase, but stay exactly where you
typed them in your code. 

### Declarations vs initializations

JavaScript only hoists declarations, not initializations. 

All identifiers are registered to their respective scopes during compile time. 

Moreover, every identifier is created at the beginning of the scope it belongs to, every time that scope is entered.

Example:

```js
var greeting;               // 1.

console.log(greeting)       //undefined

function greeting() {
    console.log("Hello!");
}

var greeting;               // 2., a no-op. This will not reset to undefined.

typeof greeting;            // "function"

var greeting = "Hello!";

typeof greeting;            // "string"
````

The 1. greeting declaration registers the identifier to the scope, and because it's a `var` the auto-initialization will
be undefined. The function declaration doesn't need to re-register the identifier, but because of function hoisting it
overrides the auto-initialization to use the function reference.

The 2. greeting by itself doesn't do anything since greeting is already an identifier and function hoisting
already took precedence for the auto-initialization. It's worth mentioning that `var x;` declaration does not mean `var
x = undefined` during program execution. The `undefined` auto-initialization happens during hoisting.

Remember that *compiler* ends up removing any `var/let/const` declarators, replacing them with the instructions at the
top of each scope to register the appropriate identifiers.

Both function hoisting and variable hoisting attach their name identifiers to the nearest enclosing function scope (or,
if none, the global scope), not a block scope.

### Var hoisting

```js
console.log(x);  // undefined, declaration was hoisted and then auto-initialized to undefined

var x;           // variable declaration
x = 1;           // variable initialization
```

### Function hoisting

A `function` declaration is hoisted and initialized to its function value.

Function hoisting only applies to formal function declarations, not to function expression assignments. 

Function declarations are built in memory as soon as the script is loaded, function expressions are built as soon as the
interpreter reaches expression code.

```js
console.log(greeting1);     // function value
console.log(greeting1());   // undefined
console.log(greeting2());   // TypeError

function greeting1() {      // function declaration
  console.log("Hello declaration!");
}

var greeting2 = function() {  // function expression
  console.log("Hello expression!");
};

function outer() { \
  function test() {return 0;} // function declaration

  return test();

  function test() {return 1;} // function declaration
}

console.log(outer())  // returns 1

function outer() {
  var test = function() {return 0;} // function expression

  return test();

  var test = function() {return 1;} // function expression
}

console.log(outer())  // returns 0
```

### let/const hoisting

With `var` declarations, the variable is hoisted to the top of its scope. But it's also automatically initialized to the
undefined value, so that the variable can be used throughout the entire scope.

Declarations with `let` and `const` still hoist (see the TDZ section). The actual difference is that `let/const`
declarations do not automatically initialize at the beginning of the scope, the way `var` does.

These two declaration forms also attach to their enclosing block rather than just an enclosing function as with `var`
and function declarations.

## Function scope

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#function_scope)

A function serves as a closure in JavaScript, and thus creates a scope, so that (for example) a variable defined
exclusively within the function cannot be accessed from outside the function or within other functions. However, a
function can access all variables and functions defined inside the scope in which it is defined.

When a function (declaration or expression) is defined, a new scope is created. The positioning of scopes nested inside
one another creates a natural scope hierarchy throughout the program, called the scope chain. The scope chain controls
variable access, directionally oriented upward and outward.

Each new scope offers a clean slate, a space to hold its own set of variables. When a variable name is repeated at
different levels of the scope chain, shadowing occurs, which prevents access to the outer variable from that point
inward.

## Block scope

* [MDN](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch6.md#scoping-with-blocks)

In general, any `{}` curly-brace pair which is a statement will act as a block, but *not necessarily* as a scope.

A block only becomes a scope if necessary, to contain its block-scoped declarations (i.e., `let/const`). Explicit
standalone `{}` blocks have always been valid JS syntax, but since they couldn't be a scope prior to ES6's `let/const`.

Not all `{}` curly-brace pairs create blocks (and thus are eligible to become scopes):

* Object literals use curly-brace pairs to delimit their key-value lists, but such object values are not scopes.
* class uses curly-braces around its body definition, but this is not a block or scope.
* A function uses around its body, but this is not technically a block—it's a single statement for the function
  body. It is, however, a function scope.
* The curly-brace pair on a switch statement (around the set of case clauses) does not define a block/scope.

## Global scope

A program may or may not:

* Declare a global variable in the top-level scope with `var` or function declarations—or `let`, `const`, and `class`.
* Also add global variables declarations as properties of the global scope object if `var` or function are used for the
  declaration.
* Refer to the global scope object (for adding or retrieving global variables, as properties) with `window`, `self`, or
  `global`.

### Globals Shadowing Globals

* [You Don't Know JS Yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch4.md#globals-shadowing-globals)

The `let` declaration adds a global variable but not a global object property.

The effect is that the lexical identifier shadows the global object property.

Example:

```js
window.something = 42;

let something = "Kyle";

console.log(something); // Kyle

console.log(window.something); // 42, var declaration would return Kyle
```

A simple way to avoid this gotcha with global declarations: always use `var` for globals.

Reserve `let` and `const` for block scopes.

## Temporal Dead Zone (TDZ)

* [You Don't Know JS Yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch5.md#uninitialized-variables-aka-tdz)
* [Temporal Dead Zone (TDZ) demystified](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)
* [What is the temporal dead zone?](https://stackoverflow.com/questions/33198849/what-is-the-temporal-dead-zone)

* Uninitialized variables
* Not enabled in Babel.js by default

With `var` declarations, the variable is hoisted to the top of its scope. But it's also automatically initialized to the
`undefined` value, so that the variable can be used throughout the entire scope.

There's a common misconception that *TDZ* means `let` and `const` do not hoist. This is an inaccurate, or at least
slightly misleading, claim. They definitely hoist. The actual difference is that `let/const` declarations do not
automatically initialize at the beginning of the scope, the way `var` does.

`Let/const` declarations do hoist, but they throw *Reference errors* when accessed before being initialized (instead of
returning an `undefined` as `var` would). 

The debate then is if the auto-initialization is part of hoisting, or not? I think auto-registration of a variable at
the top of the scope (i.e., what I call "hoisting") and auto-initialization of var at the top of the scope (to
undefined) are distinct operations and shouldn't be lumped together under the single term "hoisting."

```js
console.log(studentName);   // ReferenceError, no auto initialization

let studentName = "Suzy";   // declaration and assignment
```

Consider:

```
let studentName;          // auto initialization

console.log(studentName); // undefined

studentName = "Suzy";

console.log(studentName); // Suzy
```

Compiler is also adding an instruction in the middle of the program, at the point where the variable studentName was
declared, to handle that declaration's auto-initialization. We cannot use the variable at any point prior to that
initialization occuring. The same goes for `const` as it does for `let`.

The term coined by TC39 to refer to this period of time from the entering of a scope to where the auto-initialization of
the variable occurs is: Temporal Dead Zone (TDZ).

"Temporal" in TDZ does indeed refer to *time* not *position* in code (Tempus is a Latin word meaning time).

The TDZ is the time window where a variable exists but is still uninitialized, and therefore cannot be accessed in any
way. Only the execution of the instructions left by Compiler at the point of the original declaration can do that
initialization. After that moment, the TDZ is done, and the variable is free to be used for the rest of the scope.

We've already seen that `let` and `const` don't auto-initialize at the top of the scope. But let's prove that `let` and
`const` do hoist:

```js
var studentName = "Kyle";

{
  // ReferenceError: can't access lexical declaration before initialization
  // ignoring var "Kyle"
  console.log(studentName);	

  let studentName = "Suzy";

  console.log(studentName); // Never executes due to Error
}
```

The inner scope's `studentName` was hoisted (auto-registered at the top of the scope - block scope). What didn't happen
(yet!) was the auto-initialization of that inner studentName; it's still uninitialized at that moment, hence the TDZ
violation and a ReferenceError.

Default parameters also have TDZ semantics, default parameters are evaluated from left to right, so `b` is in the TDZ
when `a` 's initializer tries to read it.

Example:

```js

(function(a = b, b) {}(undefined, 1)); 		// ReferenceError: TDZ

(function(a, b = a) {}(undefined, 1)); 		// OK

```

The TDZ error is strange and frustrating when encountered. Fortunately, TDZ is relatively
straightforward to avoid if you're always careful to place `let/const` declarations at the top of any scope.
