# Classes

Overview:

* [Classes - MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)
* [Prototype chains and classes - JavaScript for impatient programmers](https://exploringjs.com/impatient-js/ch_proto-chains-classes.html)

Topics:

* [Class fields - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Class_fields)

Classes are in fact "special functions", the class syntax has two components:

* [class expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/class)
* [class declarations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/class)

An important difference between function declarations and class declarations is that function declarations are hoisted
and *class declarations are not*. 

The body of a class is executed in strict mode.

## constructor

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor)

The `constructor` method is a special method of a class for creating and initializing an object of that class. A
`constructor` enables you to provide any custom initialization that must be done before any other methods can be called
on an instantiated object.

A `constructor` can use the `super` keyword to call the constructor of the super class.

## super

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)

When used in a `constructor`, the super keyword appears alone and must be used before the `this` keyword is used.

The `super` keyword can also be used to call corresponding methods of super class. This is one advantage over
prototype-based inheritance.

## extends

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends)

The `extends` keyword can be used to subclass custom classes as well as built-in objects.

## Fields

* [Field declarations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#field_declarations)

### Static methods

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static)
* [Static methods and properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#static_methods_and_properties)

The static keyword defines a static method or property for a class. Neither static methods nor static properties can be
called on instances of the class. Instead, they're called on the class itself.

### Public class fields

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields)
* [Public static fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields#public_static_fields)
* [Public instance fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields#public_instance_fields)

Both static and instance public fields are writable, enumerable, and configurable properties. As such, unlike their
private counterparts, they participate in prototype inheritance.

You don't use a `public` keyword, properties are public by default.

### Private class fields

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)

Class fields are public by default, and can be examined or modified outside the class.

Private class members can be created by using a hash `#` prefix. 

Private fields are accessible on the class constructor from inside the class declaration itself. They are used for
declaration of field names as well as for accessing a field’s value.

Use the [`get`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get) and
[`set`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set) syntax to declare a public
instance getter or setter.

```javascript
class ClassWithGetSet {
  #msg = 'hello world'

  get msg() {
    return this.#msg
  }

  set msg(x) {
    this.#msg = `hello ${x}`
  }

}
```
