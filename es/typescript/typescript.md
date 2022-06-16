# Typescript

Documentation:

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript cheat sheet](https://rmolinamir.github.io/typescript-cheatsheet/#table-of-contents)
- [Release Notes](https://www.typescriptlang.org/docs/handbook/release-notes/overview.html)

Guides:

- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/)

Style guides:

- [StyleGuide - basarat.gitbook.io](https://basarat.gitbook.io/typescript/styleguide)
- [TIPs - basarat.gitbook.io](https://basarat.gitbook.io/typescript/main-1)
- [Google TypeScript Style Guide - google.github.io](https://google.github.io/styleguide/tsguide.html)

Utility types:

- [Handbook](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- [Playground](https://www.typescriptlang.org/play?strictNullChecks=true&q=349#example/built-in-utility-types)
- [freecodecamp.org](https://www.freecodecamp.org/news/advanced-typescript-types-cheat-sheet-with-examples/)

Exercises:

- [TypeScript Playground](https://www.typescriptlang.org/play/)
- [TypeScript Exercises](https://typescript-exercises.github.io)

## Types

### Type compatibility

- [Handbook](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/type-compatibility)
- [Variance - basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/type-compatibility#variance)
- [Nominal typing in TypeScript - basarat.gitbook.io](https://basarat.gitbook.io/typescript/main-1/nominaltyping)

Type compatibility in TypeScript is based on *structural subtyping*. Structural typing is a way of relating types based
solely on their members.

The basic rule for TypeScript's structural type system is that `x` is compatible with `y` if `y` has at least the same
members as `x`.

TypeScript's type system allows certain operations that can't be known at compile-time to be safe. When a type system
has this property, it is said to not be *sound*.

### Interfaces and Types

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
- [Differences Between Type Aliases and Interfaces - Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

Almost all features of an interface are available in type; the key distinction is that a type cannot be reopened to add
new properties vs an interface which is always extendable.

See the [Playground](https://www.typescriptlang.org/play?q=464#example/types-vs-interfaces) comments:

"We recommend you use interfaces over type aliases. Specifically, because you will get better error messages.

One major difference between type aliases vs interfaces are that interfaces are open and type aliases are closed. This
means you can extend an interface by declaring it a second time."

### Union types (|)

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system#union-type)

A union type is a type formed from two or more other types, representing values that may be any one of those types.

### Intersection types (&)

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system#intersection-type)


Interfaces allowed us to build up new types from other types by extending them with the `extends` keyword.

TypeScript provides another construct called intersection types that is mainly used to combine existing object types.
You take two objects and create a new one that has the features of both these objects.

## Type Narrowing (Type Guards)

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/typeguard)
- [Playground](https://www.typescriptlang.org/play?q=7#example/type-guards)

Type Guards allow you to narrow down the type of an object within a conditional block.

### typeof

- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)

JavaScript supports a `typeof` operator which can give very basic information about the type of values we have at runtime.

Example:

```typescript
if (typeof x === 'string') {}
```

TypeScript expects this to return a certain set of strings:

- `string`
- `number`
- `bigint`
- `boolean`
- `symbol`
- `undefined`
- `object`
- `function`

### instanceof

- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)

The `instanceof` operator tests to see if the prototype property of a constructor appears anywhere in the prototype chain
of an object. The return value is a boolean value.

Example:

```typescript
if (foo instanceof Foo) {}
```

### in

- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in)
- [Handbook](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing)

The `in` operator does a safe check for the existence of a property on an object and can be used as a type guard.

```typescript
if ("swim" in animal) {}
```

### Literal Type Guard

You can use `===` / `==` / `!==` / `!=` to distinguish between literal values.

```typescript
type TriState = 'yes' | 'no' | 'unknown';

function logOutState(state: TriState) {
  if (state === 'yes') {}
}
```

### is (Type Predicates) 

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates)

To define a *user-defined type guard*, we simply need to define a function whose return type is a *type predicate*.

```typescript
function isFoo(arg: any): arg is Foo {
  return arg.foo !== undefined;
}
```

### Discriminated unions

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions)

When every type in a union contains a common property with literal types, TypeScript considers that to be a
*discriminated union*, and can narrow out the members of the union.

## Literal types

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/literal-types)

Literal types (literals) are exact values that are JavaScript primitives.

```typescript
let foo = "hello";            // string
let bar: "hello" = "hello";   // "hello"
```

By combining literals into unions, you can express a certain set of known values.

```typescript
type Position = "left" | "right" | "center"
```

The type `boolean` itself is actually just an alias for the union `true | false`.

### Literal Inference

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-inference)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/literal-types#inference)

When you initialize a variable with an object, TypeScript assumes that the properties of that object might change values
later. This might raise errors such as `Argument of type 'string' is not assignable to parameter of type ...`

1. You can change the inference by adding a type assertion in either location:

```typescript
// Change 1:
const req = { url: "https://example.com", method: "GET" as "GET" };

// Change 2
handleRequest(req.url, req.method as "GET");
```
2. You can use `as const` to convert the entire object to be type literals:

```typescript
// Change:
const req = { url: "https://example.com", method: "GET" } as const;
```

3. Use a type annotation that helps TypeScript infer the correct thing at the point of declaration:

```typescript
// Add:
interface Req {
    url: string,
    method: "GET" | "POST"
}

// Change:
const req: Req = { url: "https://example.com", method: "GET" };
```

### as const assertion

- [Release notes - TypeScript 3.4](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions)

The `as const` suffix acts like `const` but for the type system, ensuring that all properties are assigned the literal
type instead of a more general version like `string` or `number`.

```typescript
const x = 'hello';          // type "hello" 
let y = 'hello';            // type string
let z = 'hello' as const;   // type "hello"
```

Marking an object `as const` marks all properties as `readonly`, but does not make the object fully immutable.

```typescript
const action = { type: 'INCREMENT', };            // type { type: string }
const action = { type: 'INCREMENT', } as const;   // type { readonly type: "INCREMENT" }
```

Array literals become `readonly` tuples.

```typescript
const myArray = ['hello', 'world', 10];             // type `const myArray: (string | number)[]`
const myArray = ['hello', 'world', 10] as const;    // type `const myArray: readonly ["hello", "world", 10]`
```

### Template Literal Types

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html)

Template literal types build on string literal types, and have the ability to expand into many strings via unions.

They have the same syntax as template literal strings in JavaScript, but are used in type positions. When used with
concrete literal types, a template literal produces a new string literal type by concatenating the contents.

```typescript
type World = "world";
type Person = "person";
 
type Greeting = `hello ${World | Person}`; //  "hello world" | "hello person"
```

## Index signatures

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/objects.html#index-signatures)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/index-signatures)

You can use an index signature to declare the types of properties which have not been declared ahead of time.

An index signature property type must be either `string` or `number`. JavaScript implicitly calls `toString` on any
object index signature.

Example:

```typescript
interface StringArray {
  [index: number]: string;
}
```

## Mapped Types

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html)

When you don't want to repeat yourself, sometimes a type needs to be based on another type.

Mapped types build on the syntax for index signatures. A mapped type is a *generic type* which uses a union of
PropertyKeys (frequently created via a `keyof`) to iterate through keys to create a type.

Example:

```typescript
type OptionsFlags<Type> = {
  [Property in keyof Type]: boolean;
};
```

In this example, `OptionsFlags` will take all the properties from the type `Type` and change their values to be a
boolean.

There are two additional modifiers which can be applied during mapping: `readonly` and `?` which affect mutability and
optionality respectively.

You can remove or add these modifiers by prefixing with `-` or `+`. If you don't add a prefix, then `+` is assumed.

## Conditional Types

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)

Conditional types take a form that looks a little like conditional expressions `(condition ? trueExpression :
falseExpression)` in JavaScript:

```typescript
SomeType extends OtherType ? TrueType : FalseType;
```

When the type on the left of the extends is assignable to the one on the right, then you'll get the type in the first
branch (the "true" branch); otherwise you'll get the type in the latter branch (the "false" branch).

The power of conditional types comes from using them with generics.

```typescript
type NameOrId<T extends number | string> = T extends number
  ? IdLabel
  : NameLabel;
```

## Tuple types

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types)

A tuple type is an Array type that knows exactly how many elements it contains, and exactly which types it contains at
specific positions. It has no representation at runtime, but is significant to TypeScript.

```typescript
type StringNumberPair = [string, number];
```

Optional tuple elements (`?`) can only come at the end. Tuples can also have rest elements, which have to be an
array/tuple type.

Tuples may be destructured like arrays; the destructuring variables get the types of the corresponding tuple elements.

### Labeled Tuples

- [Release notes - TypeScript 4.0](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#labeled-tuple-elements)

When labeling a tuple element, all other elements in the tuple must also be labeled.

```typescript
type Range = [start: number, end: number];
```

These have no impact on type-checking, they are improving the experience around tuple types and helping us to
communicate our intent.

## Enums

- [Handbook](https://www.typescriptlang.org/docs/handbook/enums.html)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/enums)

An enum is a way to organize a collection of related values.

Overview:

- Enums are one of the few features TypeScript has which is not a type-level extension of JavaScript.
- Enums allow a developer to define a set of named constants.
- Enums are real objects that exist at runtime.
- Each enum member has a value associated with it which can be either *constant* or *computed*.
- Use `keyof typeof` to get a Type that represents all Enum keys as strings.

NOTE: Prefer union types over enums.

- [fettblog.eu Tidy TypeScript: Prefer union types over enums](https://fettblog.eu/tidy-typescript-avoid-enums/)
- [Put the TypeScript enums and Booleans away](https://blog.logrocket.com/put-the-typescript-enums-and-booleans-away/)

### const enums

- [Handbook](https://www.typescriptlang.org/docs/handbook/enums.html#const-enums)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/enums#const-enums)

To avoid paying the cost of extra generated code and additional indirection when accessing enum values, it's possible to
use const enums.

Const enums can only use constant enum expressions and unlike regular enums they are completely removed during
compilation. Const enums cannot have computed members.

Example:

```typescript
const enum Tristate {
   False,
   True,
}

var x = Tristate.False; // JS generates: var x = 0; there is no `Tristate` variable at runtime
```

## Declaration merging

* [basarat.gitbook.io](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)

Declaration merging means that the compiler merges two separate declarations declared with the same name into a single
definition. This merged definition has the features of both of the original declarations. Any number of declarations can
be merged; it's not limited to just two declarations.

