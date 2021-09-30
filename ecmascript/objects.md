# Objects

Overview:

* [Object - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
* [Single objects - JavaScript for impatient programmers](https://exploringjs.com/impatient-js/ch_single-objects.html)

An object is a set of *properties* (key-value entries). A property *key* can only be a `string` or a `symbol`.

Nearly all objects in JavaScript are instances of Object which sits on the top of a *prototype chain*.

ECMAScript 2015 introduces [class syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) to
JavaScript as a way to write reusable classes using easier, cleaner syntax, which is more similar to classes in C++ or
Java. 

## Prototype chain

* [Object prototypes - MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
* [Inheritance - MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)
* [Inheritance and the prototype chain -
  MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
* [Prototype chains and classes - JavaScript for impatient
  programmers](https://exploringjs.com/impatient-js/ch_proto-chains-classes.html#prototype-chains)
* [Different ways to create objects and the resulting prototype chain - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#different_ways_to_create_objects_and_the_resulting_prototype_chain)

Prototypes are JavaScript’s only inheritance mechanism: each object has a prototype that is either null or an object. In
the latter case, the object inherits all of the prototype’s properties.

Prototypes are the mechanism by which JavaScript objects inherit features from one another.

The methods and properties are not copied from one object to another in the prototype chain. They are accessed by
walking up the prototype chain.

It's important to understand that there is a distinction between an *object's prototype* and the *prototype property on constructor functions*.

If we were to create a new instance, e.g. `let fooInstance = new Foobar()`, `fooInstance` would take its prototype from its constructor function's prototype property.

Thus `Object.getPrototypeOf(fooInstance) === Foobar.prototype`.

## Accessing Prototype

Since ECMAScript 2015, the `[[Prototype]]` is accessed using the accessors:

* [Object.getPrototypeOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)
* [Object.setPrototypeOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf)

This is equivalent to the JavaScript property `__proto__` which is *non-standard* but de-facto implemented by many browsers.

## Object.prototype.constructor

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)

The constructor property returns a reference to the Object constructor function that created the instance object. Note that the value of this property is a reference to the function itself, not a string containing the function's name.

```js
let o = {}
o.constructor === Object // true

let a = []
a.constructor === Array // true
```

All objects (with the exception of objects created with `Object.create(null))` will have a constructor property.

## Enumerability and ownership of properties

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)

*Enumerable* properties are those properties whose internal enumerable flag is set to true, which is the default for
properties created via simple assignment or via a property initializer. 

*Ownership* of properties is determined by whether the property belongs to the object directly and not to its prototype
chain.

## Property related methods

* [Detecting, retrieving, and enumerating object
  properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties#detecting_retrieving_and_enumerating_object_properties)

* [Object.defineProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
  allows a precise addition to or modification of a property on an object. You can set property to be configurable,
  enumerable and writable.
* [Object.defineProperties()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)
  method defines new or modifies existing properties directly on an object, returning the object.

### Defining getters and setters

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#defining_getters_and_setters)

* [getter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get) is a method that gets the
  value of a specific property.
* [setter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set) is a method that sets the
  value of a specific property.

You can define getters and setters on any predefined core object or user-defined object that supports the addition of
new properties.

## Spread ...

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)

Use case for spreading: 

* copying objects
* default values for missing properties
* non-destructively changing properties: we make a copy of obj where property has a different value

## in operator

* [in operator - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)
* [Object.prototype.hasOwnProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)

The `in` operator returns `true` for properties in the prototype chain. If you want to check for only non-inherited
properties, use `Object.prototype.hasOwnProperty()` instead.

```js
const car = { make: 'Honda', model: 'Accord', year: 1998 };
console.log('make' in car); // true

// Beware:
const dict = {};
console.log('toString' in dict); // true
```

## delete operator 

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)

The delete operator removes a given property from an object. On successful deletion, it will return true, else false
will be returned.

Unlike what common belief suggests, the delete operator has nothing to do with directly freeing memory. Memory
management is done indirectly via breaking references.

## The pitfalls of using an object as a dictionary

* [MDN](https://exploringjs.com/impatient-js/ch_single-objects.html#the-pitfalls-of-using-an-object-as-a-dictionary)
* [Objects vs.
  Maps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps).

The first pitfall is that the `in` operator also finds inherited properties. The second pitfall is that we can’t use the
property key `__proto__` because it has special powers (it sets the prototype of the object). Although the keys of an
ordinary Object are ordered now, this was not always the case, and the order is complex. As a result, it's best not to
rely on property order. 

Whenever you can, use `Maps` for dictionaries.

## Immutability

### Object.freeze()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

* Nothing can be added to or removed from the properties set of a frozen object.
* Existing properties (shallow) in objects are made immutable, meaning it prevents changing the enumerability,
  configurability, or writability of existing properties, and prevents the values of existing properties from being
  changed. 
* Prevents its prototype from being changed.

`Object.freeze()` returns the same object that was passed into the function. *It does not create a frozen copy.*

Accessor properties (getters and setters) work the same (and still give the illusion that you are changing the value).

Note that values that are objects can still be modified, unless they are also frozen (shallow freeze). 

### Object.seal()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)

Existing properties in objects frozen with `Object.freeze()` are made immutable. Objects sealed with `Object.seal()` can
have their existing properties changed.

`Object.freeze()` creates a frozen object, which means it takes an existing object and essentially calls `Object.seal()`
on it, but it also marks all *data accessor* properties as `writable:false`, so that their values cannot be changed.

### Object.preventExtensions()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)

Object.preventExtensions() marks an object as no longer extensible, so that it will never have properties beyond the ones it had at the time it was marked as non-extensible. Note that the properties of a non-extensible object, in general, may still be deleted

## Object representation

* [Object.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

Every object has a `toString()` method that is automatically called when the object is to be represented as a text value
or when an object is referred to in a manner in which a string is expected. If this method is not overridden in a custom
object, `toString()` returns `[object <type>]`, where type is the object type. 

* [Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

JavaScript calls the `valueOf()` method to convert an object to a primitive value. You rarely need to invoke the
`valueOf()` method yourself; JavaScript automatically invokes it when encountering an object where a primitive value is
expected. You can use `valueOf()` within your own code to convert a built-in object into a primitive value.

