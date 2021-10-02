# Classes

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html)
* [Using Class Types in Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html#using-class-types-in-generics)

## Constructors

* Constructors can have overloads like functions.
* Constructors can’t have type parameters - these belong on the outer class declaration.
* Constructors can’t have return type annotations - the class instance type is always what’s returned.
* Just as in JavaScript, if you use `extended` from base class, you’ll need to call `super()` in your `constructor body`
  before using any base class members with `this` in the constructor.

Constructor overloads example:

```typescript
class Point {
 constructor(x: number, y: string);
 constructor(s: string);
 constructor(xs: any, y?: any) {
    ...
 }
}
```

## Field types

* [public](https://www.typescriptlang.org/docs/handbook/2/classes.html#public): Can be accessed anywhere (default).
* [protected](https://www.typescriptlang.org/docs/handbook/2/classes.html#protected): (TS specific) only visible to
  subclasses of the class they’re declared in.
* [private](https://www.typescriptlang.org/docs/handbook/2/classes.html#private): Like protected, but doesn’t allow
  access to the member even from subclasses.
* [static](https://www.typescriptlang.org/docs/handbook/2/classes.html#static-members): These members aren’t associated
  with a particular instance of the class.

Field types can have `readonly` modifiers. 

Static members can also use the same `public`, `protected`, and `private` visibility modifiers.

### ECMAScript Private Fields

* [Documentation](https://devblogs.microsoft.com/typescript/announcing-typescript-3-8-beta/#ecmascript-private-fields)

`Private` and `protected` fields are only enforced during type checking. If you need to protect values in your class
from malicious actors, you should use mechanisms that offer hard runtime privacy, such as closures, weak maps, or [ES
private fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields).

TypeScript 3.8 added support for ECMAScript private fields (using a hash `#` prefix), not to be confused with the TypeScript `private` modifier. TypeScript currently can’t support this feature unless targeting ECMAScript 2015 (ES6) targets or higher. 

* [Which should I use?](https://devblogs.microsoft.com/typescript/announcing-typescript-3-8-beta/#which-should-i-use)

- TypeScript `private` modifiers are fully erased, better compatibility.
- ECMAScript `#` privates are enforced in runtime code.

## Getters and Setters

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html#getters--setters)

* If getter exists but setter does not, the property is automatically `readonly`.
* If the type of the setter parameter is not specified, it is inferred from the return type of the getter.
* Getters and setters must have the same member visibility.

## Class heritage

* [implements](https://www.typescriptlang.org/docs/handbook/2/classes.html#implements-clauses): Use an implements clause
  to check that a class satisfies a particular interface.
* [extends](https://www.typescriptlang.org/docs/handbook/2/classes.html#extends-clauses): Extend derived class from a
  base class (ECMAScript).

## Generic classes

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html#generic-classes)

Classes, much like interfaces, can be generic. When a generic class is instantiated with `new`, its type parameters are
inferred the same way as in a function call. 

```typescript
class Box<Type> {
  contents: Type;
  constructor(value: Type) {
    this.contents = value;
  }
}
 
const b = new Box("hello!");
     
const b: Box<string>
```

Classes can use generic constraints and defaults the same way as interfaces.

## this in classes

### this function parameter

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-parameters)

In a method or function definition, an initial parameter named `this` has special meaning in TypeScript. These
parameters are erased during compilation:

```typescript
function fn(this: SomeType, x: number) {}
```

TypeScript checks that calling a function with a `this` parameter is done so with a correct context. Instead of using an
arrow function, we can add a `this` parameter to method definitions to statically enforce that the method is called
correctly. These parameters are erased during compilation.

### this Type

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-types)

In classes, a special type called this refers dynamically to the type of the current class. 

```typescript
class Box {
  contents: string = "";
  set(value: string) {
  
(method) Box.set(value: string): this
    this.contents = value;
    return this;
  }
}
```

You can also use this in a parameter type annotation:

```typescript
class Box {
  content: string = "";
  sameAs(other: this) {
    return other.content === this.content;
  }
}
```

### this is: this-based type guards

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-based-type-guards)

You can use the `this is` Type in the return position for methods in classes and interfaces. When mixed with a type
narrowing (e.g. if statements) the type of the target object would be narrowed to the specified Type.

```typescript
class FileSystemObject {
  isFile(): this is FileRep {
    return this instanceof FileRep;
  }
  isDirectory(): this is Directory {
    return this instanceof Directory;
  }
  constructor(public path: string, private networked: boolean) {}
}
```

## abstract Classes and Members

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html#abstract-classes-and-members)

An abstract method or abstract field is one that hasn’t had an implementation provided. These members must exist inside
an abstract class, which cannot be directly instantiated. The role of abstract classes is to serve as a base class for
subclasses which implement all the abstract members.

Use `abstract` keyword to mark class, field or property as abstract.

