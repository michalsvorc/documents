# Symbols

- [Symbol - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [Object.getOwnPropertySymbols()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols)
- [(Video) The Complete Guide to JS Symbols ES6](https://youtu.be/4J5hnOCj69w?t=16)

The data type symbol is a primitive data type. Every symbol value returned from the `Symbol()` constructor is unique.

String parameter in `Symbol('name')` serves as a debugging label.

```javascript
const SYMBOL_ID = Symbol("id");
const SYMBOL_NAME = Symbol("name");

let user = {
  [SYMBOL_ID]: 1,
  [SYMBOL_NAME]: "Alice",
};

user[SYMBOL_ID]; // 1
user[SYMBOL_NAME]; // 'Alice'

console.log(user);
// Object { Symbol("id"): 1, Symbol("name"): "Alice" }

console.log(JSON.stringify(user));
// undefined (!)
```

Symbols are often used to add unique property keys to an object that won’t collide with keys any other code might add to
the object, and which are hidden from any mechanisms other code will typically use to access the object.

That enables a form of weak [encapsulation](https://developer.mozilla.org/en-US/docs/Glossary/Encapsulation), or a weak
form of [information hiding](https://en.wikipedia.org/wiki/Information_hiding).

Symbols are not enumerable with [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) iterations.

In addition, `Object.getOwnPropertyNames()` will not return Symbol object properties, however, you can use
`Object.getOwnPropertySymbols()` to get these.

Symbol-keyed properties will be completely ignored when using `JSON.stringify()` on an object.

## Use cases

- Internal id's for object/class instances.
- Id's for timers.

## Shared Symbols

- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol#shared_symbols_in_the_global_symbol_registry)
- [Symbols in ECMAScript 6](https://2ality.com/2014/12/es6-symbols.html#crossing-realms-with-symbols)

To create Symbols available across files and even across realms (each of which has its own global scope), use the methods:

- [Symbol.for()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/for)

The `Symbol.for(key)` method searches for existing symbols in a runtime-wide symbol registry with the given key and
returns it if found. Otherwise a new symbol gets created in the global symbol registry with this key.

- [Symbol.keyFor()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/keyFor)

The `Symbol.keyFor(symbol)` method retrieves a shared symbol key from the global symbol registry for the given symbol.
