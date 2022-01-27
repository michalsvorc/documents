# Keywords

## keyof

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html): Takes an object type and produces a string
  or numeric literal union of its keys.

Usage:

- [extends
  keyof](https://www.typescriptlang.org/docs/handbook/2/generics.html#using-type-parameters-in-generic-constraints):
  Using Type Parameters in Generic Constraints.
- [in keyof](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html): Index signatures in mapped types.
- [keyof typeof](https://basarat.gitbook.io/typescript/type-system/moving-types#capturing-key-names): Capture the key
  names of a variable by first grabbing its type using `typeof`.

## Narrowing types

- [in](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing): Acts as a narrowing
  expression for type guards or index signatures.
- [is](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates): Type predicates.
- [as](https://basarat.gitbook.io/typescript/type-system/type-assertion): Type assertion.
- [as const](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions): Const
  assertion.

## extends

- [skovy.dev](https://skovy.dev/typescript-explained-in-javascript-extends/)

Usage:

- [Extending classes](https://www.typescriptlang.org/docs/handbook/2/classes.html#extends-clauses)
- [Extending interfaces](https://www.typescriptlang.org/docs/handbook/2/objects.html#extending-types)
- [Imposing constraints](https://www.typescriptlang.org/docs/handbook/2/functions.html#constraints)

## any

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any)

Use whenever you don't want a particular value to cause type checking errors. When you don't specify a type, and
TypeScript can't infer it from context, the compiler will typically default to `any`.

Use the compiler flag [noImplicitAny](https://www.typescriptlang.org/tsconfig#noImplicitAny) to flag any implicit `any`
as an error.

## never

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-never-type)
- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/never)

When narrowing, you can reduce the options of a union to a point where you have removed all possibilities and have
nothing left. In those cases, TypeScript will use a `never` type to represent a state which *shouldn't exist*.

When used in a function return type, `never` means that the function throws an exception or terminates execution of the
program.

Usage: [Exhaustive Checks](https://basarat.gitbook.io/typescript/type-system/discriminated-unions#exhaustive-checks)

Comparison to `void`:

- `void` is a unit
- `never` is a falsum

## unknown

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown)

The `unknown` type is similar to the `any` type, but is safer because it's not legal to do anything with an `unknown`
value.

## void

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#void)
- [Function return type void - Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#return-type-void)

`void` represents the return value of functions which don't return a value.

It's the inferred type any time a function doesn't have any return statements, or doesn't return any explicit value
from those return statements.

`void` is not the same as undefined.

## ? (Optional Object Properties)

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/objects.html#optional-properties)

We can mark properties as optional by adding a question mark `?` to the end of their names.

## ! (Non-null Assertion Operator)

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#non-null-assertion-operator-postfix-)

Writing `!` after any expression is effectively a type assertion that the value isn't `null` or `undefined`. Just like
other type assertions, this doesn't change the runtime behavior of your code, so it's important to only use ! when you
know that the value can't be null or undefined.

## readonly

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties)

Properties can also be marked as `readonly` for TypeScript. While it won't change any behavior at runtime, a property
marked as `readonly` can't be written to during type-checking.

Using the `readonly` modifier doesn't necessarily imply that a value is totally immutable - or in other words, that its
internal contents can't be changed (in case of objects). It just means the property itself can't be re-written to.

## object

* [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#object)

The special type `object` refers to any value that isn't a primitive value. This is different from the empty object type
`{}`, and also different from the global type `Object`. 

`typeof null === "object"`

## Function

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#function)

The global type `Function` describes properties like `bind`, `call`, `apply`, and others present on all function values
in JavaScript.

This is an untyped function call and is generally best avoided because of the unsafe `any` return type.

If you need to accept an arbitrary function but don't intend to call it, the type `() => void` is generally safer.

## Iterable

- [Handbook](https://www.typescriptlang.org/docs/handbook/iterators-and-generators.html#iterable-interface)

`Iterable` is a type we can use if we want to take in types listed above which are iterable.

## declare

The `declare` keyword is used for ambient declarations where you want to define a variable that may not have originated
from a TypeScript file.

- [declare](https://basarat.gitbook.io/typescript/type-system/intro): Ambient declarations.

Usage:

- [declare var](https://basarat.gitbook.io/typescript/type-system/intro/variables): Ambient variable declarations.
- [declare module](https://www.typescriptlang.org/docs/handbook/modules.html#ambient-modules): Ambient module
  declarations.
- [declare namespace](https://www.typescriptlang.org/docs/handbook/namespaces.html#ambient-namespaces): Ambient
  namespace declarations.

## infer

* [Release notes - TypeScript
  2.8](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#type-inference-in-conditional-types)
* [Handbook](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types)
* [TypeScript Tutorial - dev.to](https://dev.to/aexol/typescript-tutorial-infer-keyword-2cn)
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
