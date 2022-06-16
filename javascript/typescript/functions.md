# Functions

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html)

## Specifying Type Arguments

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#specifying-type-arguments)

TypeScript can usually infer the intended type arguments in a generic call, but not always.

You could manually specify Type on the function call:

```typescript
function combine<Type>(arr1: Type[], arr2: Type[]): Type[] {
  return arr1.concat(arr2);
}

const arr = combine<number | string>([1, 2, 3], ["a"]);
```

## Function Overloading

- [Functions - basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/functions#overloading)
- [More on Functions - Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads)
- [Type Compatibility - basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/type-compatibility#functions)
- [Guidelines for Writing Good Generic Functions - Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#guidelines-for-writing-good-generic-functions)

Some JavaScript functions can be called in a variety of argument counts and types.

In TypeScript, we can specify a function that can be called in different ways by writing overload signatures. To do
this, write some number of function signatures (usually two or more), followed by the body of the function.

- The implementation signature must be type-compatible with the overload signatures.
- Always prefer parameters with union types instead of overloads when possible.

We can avoid overloads entirely by instead using generic functions.

## Declaring `this` in a Function

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#declaring-this-in-a-function)

There are a lot of cases where you need more control over what object `this` represents. The JavaScript specification
states that you cannot have a parameter called `this`, and so TypeScript uses that syntax space to let you declare the
type for `this` in the function body.

This pattern is common with callback-style APIs, where another object typically controls when your function is called.

```typescript
interface DB {
  filterUsers(filter: (this: User) => boolean): User[];
}
```

## Call signatures

- [Handbook](https://www.typescriptlang.org/docs/handbook/2/functions.html#call-signatures)
- [Generic call signatures - Handbook](https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-types)
- [Newable - basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/callable#newable)

In JavaScript, functions can have properties in addition to being callable.

If we want to describe something callable with properties, we can write a call signature in an object type:

```typescript
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
```

JavaScript functions can also be invoked with the new operator. TypeScript refers to these as _constructors_ because
they usually create a new object. You can write a construct signature by adding the new keyword in front of a call
signature:

```typescript
type SomeConstructor = {
  new (s: string): any;
};
```
