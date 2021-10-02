# Typescript

Documentation:

* [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
* [TypeScript cheat sheet](https://rmolinamir.github.io/typescript-cheatsheet/#table-of-contents)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system)

Releases:

* [Release Notes](https://www.typescriptlang.org/docs/handbook/release-notes/overview.html)

Tutorials:

* [TutorialsTeacher](https://www.tutorialsteacher.com/typescript/type-annotation)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
* [TypeScript Tutorial](https://howtodoinjava.com/typescript/typescript-tutorial/)
* [Unions and Intersection Types](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html)
* [Time to Really Learn TypeScript](https://react-typescript-cheatsheet.netlify.app/docs/basic/troubleshooting/learn_ts)

Style guides:

* [StyleGuide - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/styleguide)
* [TIPs - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/main-1)

Utility types:

* [Utility types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
* [(Playground) Built-in Utility Types](https://www.typescriptlang.org/play?strictNullChecks=true&q=349#example/built-in-utility-types)
* [Advanced TypeScript Types Cheat Sheet (with Examples)](https://www.freecodecamp.org/news/advanced-typescript-types-cheat-sheet-with-examples/)

Topics:

* [Handbook - Advanced Types (+Type Guards)](https://www.typescriptlang.org/docs/handbook/advanced-types.html)
* [Type Compatibility - Documentation](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
* [Type Compatibility - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/type-compatibility)
* [Type Retrospective
  Versioning](https://basarat.gitbook.io/typescript/type-system/discriminated-unions#retrospective-versioning)

Exercises:

* [TypeScript Playground](https://www.typescriptlang.org/play/)
* [TypeScript Exercises](https://typescript-exercises.github.io)

Type assertions don't change the runtime behavior of your code.

## Keywords

* [keyof](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html): Takes an object type and produces a string
  or numeric literal union of its keys.
* [extends keyof](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-constraints): Constrain the type
  of keys of an Type.
* [in keyof](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html): Index signatures in mapped types.
* [keyof typeof](https://basarat.gitbook.io/typescript/type-system/moving-types#capturing-key-names)
    - Capture the key names of a type.
    - Get a Type that represents all Enum keys as strings.
* [typeof](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html): You can use `typeof` in a type context to
  refer to the type of a variable or property.
* [infer](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#type-inference-in-conditional-types):
  Type inference in conditional types.

Narrowing types:

* [in](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing): Acts as a narrowing
  expression for type guards or index signatures.
* [is](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates): Type predicates.
* [as](https://basarat.gitbook.io/typescript/type-system/type-assertion): Type assertion.
* [as const](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions): Const
  assertion.

Extends keyword:

* [extends](https://skovy.dev/typescript-explained-in-javascript-extends/)
* [Extending classes](https://www.typescriptlang.org/docs/handbook/2/classes.html#extends-clauses)
* [Extending interfaces](https://www.typescriptlang.org/docs/handbook/2/objects.html#extending-types)
* [Extending Type parameters (constraint)](https://www.typescriptlang.org/docs/handbook/2/functions.html#constraints)

Declarations:

The `declare` keyword is used for ambient declarations where you want to define a variable that may not have originated
from a TypeScript file.

* [declare](https://basarat.gitbook.io/typescript/type-system/intro): Ambient declarations.
* [declare var](https://basarat.gitbook.io/typescript/type-system/intro/variables): Ambient variable declarations.
* [declare module](https://www.typescriptlang.org/docs/handbook/modules.html#ambient-modules): Ambient module
  declarations.
* [declare namespace](https://www.typescriptlang.org/docs/handbook/namespaces.html#ambient-namespaces): Ambient
  namespace declarations.

Classes:

* [abstract](https://www.typescriptlang.org/docs/handbook/2/classes.html#abstract-classes-and-members): An abstract
  method or abstract field is one that hasn’t had an implementation provided.

## Typing systems

* [Documentation](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)

TypeScript is a *Structural Type System*.

A structural type system means that when comparing types, TypeScript only takes into account the members of the type.
This is in contrast to nominal type systems, where you could create two types but could not assign them to each other.

```typescript
interface Pet {
 name: string;
}

class Dog {
 name: string;
}

let pet: Pet;

pet = new Dog();  // OK, because of structural typing
```

### Nominal typing

* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/main-1/nominaltyping)

There are real-world use cases for a system where you want two variables to be differentiated because they have a
different type name even if they have the same structure.

TypeScript has no native support for nominal types. Many techniques have surfaced for simulating nominal types.

### Variance

* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/type-compatibility#variance)

Variance is an easy to understand and important concept for type compatibility analysis.

For simple types `Base` and `Child`, if `Child` is a child of `Base`, then instances of `Child` can be assigned to a
variable of type `Base`.

The type compatibility of complex types composed of such `Base` and `Child` types depends on where the `Base` and
`Child` in similar scenarios are driven by *variance*.

## Typing

### any

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any)

Use whenever you don’t want a particular value to cause type checking errors. When you don’t specify a type, and
TypeScript can’t infer it from context, the compiler will typically default to `any`.

Use the compiler flag [noImplicitAny](https://www.typescriptlang.org/tsconfig#noImplicitAny) to flag any implicit `any`
as an error.

### never

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-never-type)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/never)

When narrowing, you can reduce the options of a union to a point where you have removed all possibilities and have
nothing left. In those cases, TypeScript will use a `never` type to represent a state which *shouldn’t exist*.

When used in a function return type, `never` means that the function throws an exception or terminates execution of the
program.

Use case: [Exhaustive Checks](https://basarat.gitbook.io/typescript/type-system/discriminated-unions#exhaustive-checks)

Comparison to `void`:

* `void` is a unit
* `never` is a falsum

### unknown

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown)

The `unknown` type is similar to the `any` type, but is safer because it’s not legal to do anything with an `unknown`
value.

### void

* [void](https://www.typescriptlang.org/docs/handbook/2/functions.html#void)
* [Function return type void](https://www.typescriptlang.org/docs/handbook/2/functions.html#return-type-void)

`void` represents the return value of functions which don’t return a value.

It’s the inferred type any time a function doesn’t have any return statements, or doesn’t return any explicit value
from those return statements.

`void` is not the same as undefined.

### Optional Object Properties (?)

Add a `?` after the property name to mark it as optional.

### Non-null Assertion Operator (!)

Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`.

### readonly

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties)

Properties can also be marked as `readonly` for TypeScript. While it won’t change any behavior at runtime, a property
marked as `readonly` can’t be written to during type-checking.

Using the `readonly` modifier doesn’t necessarily imply that a value is totally immutable - or in other words, that its
internal contents can’t be changed (in case of objects). It just means the property itself can’t be re-written to.

### Interfaces and Types

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
* [Differences Between Type Aliases and
  Interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

Almost all features of an interface are available in type; the key distinction is that a type cannot be reopened to add
new properties vs an interface which is always extendable.

A type cannot be changed after being created.

We recommend you use *interfaces over type* aliases. Specifically, because you will get better error  messages.

Use interface until you need to use features from type.

[Play](https://www.typescriptlang.org/play?q=464#example/types-vs-interfaces)

### Union types (|)

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)
* [TypeScript's Type System - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system#union-type)

A union type is a type formed from two or more other types, representing values that may be any one of those types. 

Example: The union `number | string` is composed by taking the union of the values from each type. Notice that given two
sets with corresponding facts about each set, only the *intersection* of those facts applies to the *union* of the sets
themselves.

### Intersection types (&)

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)
* [TypeScript's Type System - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system#intersection-type)

Intersection types are mainly used to combine existing object types. You take two objects and create a new one that has
the features of both these objects. 

### Type Assertions (as Type)

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)
* [Type Assertion - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/type-assertion)
* [Double assertion (`as unknown as Type`) - TypeScript Deep
  Dive](https://basarat.gitbook.io/typescript/type-system/type-assertion#double-assertion)

TypeScript allows you to override its inferred and analyzed view of types in any way you want to.

Like a type annotation, type assertions are removed by the compiler and won’t affect the runtime behavior of your code.
Because type assertions are removed at compile-time, there is no runtime checking associated with a type assertion.
There won’t be an exception or null generated if the type assertion is wrong.

In many cases assertion will allow you to easily migrate legacy code. However, you should be careful with your use of
assertions. The compiler will not protect you from forgetting to actually add the properties you promised.

### Creating Types from types

* [Indexed Access Types](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)

  Using `Type['a']` syntax to access a subset of a type.

* [Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)

  `SomeType extends OtherType ? TrueType : FalseType;`

* [Mapped Types](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)

  Creating types by mapping each property in an existing type.

* [Template Literal Types](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html)

  Mapped types which change properties via template literal strings.

### object

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/functions.html#object)

The special type `object` refers to any value that isn’t a primitive value. This is different from the empty object type
`{}`, and also different from the global type `Object`. 

`typeof null === "object"`

### Function

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/functions.html#function)

This is an untyped function call and is generally best avoided because of the unsafe `any` return type.

If you need to accept an arbitrary function but don’t intend to call it, the type `() => void` is generally safer.

### Iterable interface

* [Documentation - Iterators and Generators](https://www.typescriptlang.org/docs/handbook/iterators-and-generators.html#iterable-interface)

`Iterable` is a type we can use if we want to take in types listed above which are iterable.

```typescript
function toArray<X>(xs: Iterable<X>): X[] {
  return [...xs]
}
```

## Type Narrowing (Type Guards)

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/typeguard)
* [Examples](https://www.typescriptlang.org/play?q=7#example/type-guards)

Type Guards allow you to narrow down the type of an object within a conditional block. 

### typeof

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)

JavaScript supports a `typeof` operator which can give very basic information about the type of values we have at runtime.
TypeScript expects this to return a certain set of strings:

* "string"
* "number"
* "bigint"
* "boolean"
* "symbol"
* "undefined"
* "object"
* "function"

```typescript
if (typeof x === 'string') {}
```

### instanceof

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)

The `instanceof` operator tests to see if the prototype property of a constructor appears anywhere in the prototype chain
of an object. The return value is a boolean value.

```typescript
if (arg instanceof Foo) {}
```

### in 

* [The in operator narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing)

The `in` operator does a safe check for the existence of a property on an object and can be used as a type guard.

```typescript
if ("swim" in animal) {}
```

### Literal Type Guard

You can use `===` / `==` / `!==` / `!=` to distinguish between literal values.

```typescript
type TriState = 'yes' | 'no' | 'unknown';

function logOutState(state:TriState) {
  if (state === 'yes') {}
}
```

### User Defined Type Guard functions: Type Predicates 

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates)

To define a user-defined type guard, we simply need to *define a function* whose *return type* is a *type predicate*.

These are just functions that return `someArgumentName is SomeType`.

```typescript
function isFoo(arg: any): arg is Foo {
  return arg.foo !== undefined;
}
```

### Discriminated unions

When every type in a union contains a common property with literal types, TypeScript considers that to be a
*discriminated union*, and can narrow out the members of the union.

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions)

```typescript
interface Shape {
  kind: "circle" | "square";	// Discriminated union, you can base type checking on it
  radius?: number;
  sideLength?: number;
}
```

## keyof

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)

It conceptually behaves identical to the `Object.keys` method, but it is a type instead of a literal value.

```typescript
type Person = { age: number; name: string; alive: boolean };

type PersonKey = Person[keyof Person]; // type PersonKey = string | number | boolean
```

### extends keyof

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-constraints)

Extends, in this case, is used to constrain the type of keys of a generic parameter.

`<T, K extends keyof T>`

K can therefore only be a public property name of T. It has nothing to do with extending a type or inheritance, contrary
to extending interfaces.

### in keyof

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)

`in` is used when we're defining an index signature that we want to type with a union of string, number or symbol
literals. In combination with `keyof` we can use it to create a so-called mapped type, which re-maps all properties of
the original type.

See mapped types

### keyof typeof

* [Moving Types - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/moving-types#capturing-key-names)

The `keyof` operator lets you capture the key names of a type. E.g. you can use it to capture the key names of a
variable by first grabbing its type using typeof.

```typescript
const colors = {
  red: 'red color',
  blue: 'blue color'
}

type Colors = keyof typeof colors; // type Colors = "red" | "blue"
```

## Mapped Types

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)

Mapped types build on the syntax for index signatures, which are used to declare the types of properties which have not
been declared ahead of time. 

* `[P in K]`
* `[P in keyof T]`

A mapped type is a generic type which uses a union of PropertyKeys (frequently created via a `keyof`) to iterate through
keys to create a type.

```typescript
type OptionsFlags<Type> = {
  [Property in keyof Type]: boolean;
};
```

### Mapping Modifiers

In this example, OptionsFlags will take all the properties from the type Type and change their values to be boolean. 

There are two additional modifiers which can be applied during mapping: `readonly` and `?` which affect mutability and
optionality respectively.

You can remove or add these modifiers by prefixing with `-` or `+`. If you don’t add a prefix, then `+` is assumed.

Remove `optional` attributes from a type's properties:

```typescript
[Property in keyof Type]-?: Type[Property];
```

Remove `readonly` attributes from a type's properties:

```typescript
-readonly [Property in keyof Type]: Type[Property];
```

In TypeScript 4.1 and onwards, you can remap keys in mapped types with an [as
clause](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#key-remapping-via-as) in a mapped type:

```typescript
[Properties in keyof Type as NewKeyType]: Type[Properties]
```

## Literal types

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)
* [Literal Types - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/literal-types)

In addition to the general types string and number, we can refer to specific strings and numbers in type positions.

```typescript
let foo = "hello";            // string 
let bar: "hello" = "hello";   // "hello" literal
```

By combining literals into unions, you can express a much more useful concept - for example, functions that only
accept a certain set of known values.

```typescript
function printText(
  alignment: "left" | "right" | "center" // literals union
) {}
```

### Literal Inference (as const assertion)

* [Documentation - TypeScript 3.4](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions)
* [The Typescript "as const" trick - DEV Community](https://dev.to/adamcoster/the-typescript-as-const-trick-2f4o)
* [const assertions - logrocket.com](https://blog.logrocket.com/const-assertions-are-the-killer-new-typescript-feature-b73451f35802/)

To create literal object properties, use `as const`.

The `as const` suffix acts like `const` but for the type system, ensuring that all properties are assigned the literal
type instead of a more general version like string or number.

Marking an object as const marks all properties as `readonly`, but does not make the object fully immutable.

Array literals become `readonly` tuples.

```typescript
const x = 'hello';          // type "hello" 
let y = 'hello';            // type string
let z = 'hello' as const;   // type "hello"


const action = { type: 'INCREMENT', };            // type { type: string }

const action = { type: 'INCREMENT', } as const;   // type { readonly type: "INCREMENT" }

const myArray = ['hello', 'world', 10];           // type `const myArray: (string | number)[]`

const myArray = ['hello', 'world', 10] as const;    // type `const myArray: readonly ["hello", "world", 10]`
```

### Template Literal Types

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html)

Template literal types build on string literal types, and have the ability to expand into many strings via unions.

They have the same syntax as template literal strings in JavaScript, but are used in type positions. When used with
concrete literal types, a template literal produces a new string literal type by concatenating the contents.

```typescript
type World = "world";
type Person = "person";
 
type Greeting = `hello ${World | Person}`; //  "hello world" | "hello person"
```

## Index signatures

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html#index-signatures)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/index-signatures)

Sometimes you don’t know all the names of a type’s properties ahead of time, but you do know the shape of the values.

In those cases you can use an index signature to describe the types of possible values.

An index signature property type must be either `string` or `number`. JavaScript implicitly calls `toString` on any
object index signature.

This index signature states that when a StringArray is indexed with a number, it will return a string:

```typescript
interface StringArray {
  [index: number]: string;
}
```

### Nested index signature

* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/index-signatures#design-pattern-nested-index-signature)

Try not to mix string indexers with *valid* values this way, `string` might introduce typos in NestedCSS type:

```typescript
[selector: string]: string | NestedCSS | undefined;
```

Instead separate out the nesting into its own property e.g. in a name like nest (or children or subnodes etc.):

```typescript
nest?: {
 [selector: string]: NestedCSS;
}
```

## infer keyword

* [Documentation - TypeScript
  2.8](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#type-inference-in-conditional-types)
* [Documentation](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types)
* [TypeScript Tutorial - DEV Community](https://dev.to/aexol/typescript-tutorial-infer-keyword-2cn)
* [Why is the infer keyword needed in Typescript? - stackoverflow.com](https://stackoverflow.com/questions/60067100/why-is-the-infer-keyword-needed-in-typescript)

Within the `extends` clause of a conditional type, it is now possible to have `infer` declarations that introduce a type
variable to be inferred.

Such inferred type variables may be referenced in the true branch of the conditional type.

Extract the type from the promise:

```typescript
type Unpromisify<T> = T extends Promise<infer R> ? R : T;
```

1. We check if type `extends` Promise
2. If it does we extract (`infer`) the type from the promise
3. If it does not leave it as is

Extract the return type of a function type:

```typescript
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;
```

## Tuple types

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types)

A tuple type is an Array type that knows exactly how many elements it contains, and exactly which types it contains at
specific positions.

```typescript
type StringNumberPair = [string, number];
```

To the type system, `StringNumberPair` describes arrays whose `0` index contains a string and whose `1` index contains a
number. It has no representation at runtime, but is significant to TypeScript.

Optional tuple elements (`?`) can only come at the end, and also affect the type of length.

### Labeled Tuples

* [Documentation](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#labeled-tuple-elements)

Tuples types can now provide labels:

```typescript
type Range = [start: number, end: number];
```

These have no impact on type-checking, they are improving the experience around tuple types and helping us to
communicate our intent.

When labeling a tuple element, all other elements in the tuple must also be labeled.

### Variadic tuple types

* [Documentation](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#variadic-tuple-types)

Concatenate function in JavaScript:

```javascript
function concat(arr1, arr2) {
  return [...arr1, ...arr2];
}
```

We can write a single well-typed signature for concat:

```typescript
type Arr = readonly any[];

function concat<T extends Arr, U extends Arr>(arr1: T, arr2: U): [...T, ...U] {
 return [...arr1, ...arr2];
}
```

While that one signature is still a bit lengthy, it’s just one signature that doesn’t have to be repeated, and it gives
predictable behavior on all arrays and tuples.

### Tuple destructuring

* [Documentation](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#tuple-destructuring)

Tuples may be destructured like arrays; the destructuring variables get the types of the corresponding tuple elements:

```typescript
let tuple: [number, string, boolean] = [7, "hello", true];

let [a, b, c] = tuple;  // a: number, b: string, c: boolean
```

It’s an error to destructure a tuple beyond the range of its elements.

## Enums

* [Documentation](https://www.typescriptlang.org/docs/handbook/enums.html)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/enums)

* Enums are one of the few features TypeScript has which is not a type-level extension of JavaScript. 
* Enums allow a developer to define a set of named constants. 
* Enums are real objects that exist at runtime.
* Each enum member has a value associated with it which can be either *constant* or *computed*.
* Use `keyof typeof` to get a Type that represents all Enum keys as strings.

### Numeric enums

Auto initialized with 0, first member can have custom initialization number.

```typescript
enum Direction {
  Up = 1,
  Down,
}
```

### String enums

Each member has to be constant-initialized with a string literal.


```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
}
```

### Prefer union types over enums

* [fettblog.eu Tidy TypeScript: Prefer union types over enums](https://fettblog.eu/tidy-typescript-avoid-enums/)
* [Put the TypeScript enums and Booleans away](https://blog.logrocket.com/put-the-typescript-enums-and-booleans-away/)

### Reverse mappings for numeric enums

* [Documentation](https://www.typescriptlang.org/docs/handbook/enums.html#enums-at-compile-time)

In addition to creating an object with property names for members, numeric *enum members* also get a reverse mapping
from enum values to enum names. Keep in mind that *string enum* members do not get a reverse mapping generated at all.

```typescript
enum Enum {
 A,
}

let a = Enum.A;

let nameOfA = Enum[a]; // "A" at runtime
```

### const enums

* [Documentation](https://www.typescriptlang.org/docs/handbook/enums.html#const-enums)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/enums#const-enums)

To avoid paying the cost of extra generated code and additional indirection when accessing enum values, it’s possible to
use const enums.

```typescript
const enum Tristate {
   False,
   True,
}

var x = Tristate.False; // JS generates: var x = 0;
```

1. Inline any usage of the enum (`0` instead of `Tristate.False`).
2. Does not generate any JavaScript for the enum definition (there is no `Tristate` variable at runtime) as its usages
   are inline.

## Declaration merging

* [TypeScript Deep Dive](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)

Declaration merging means that the compiler merges two separate declarations declared with the same name into a single
definition. This merged definition has the features of both of the original declarations. Any number of declarations can
be merged; it’s not limited to just two declarations.

