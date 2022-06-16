# TypeScript examples

## Get values of an object

```typescript
type ValueOf<T> = T[keyof T];
```

## Get property of an object

```typescript
function getProperty<Type, Key extends keyof Type>(obj: Type, key: Key) {
  return obj[key];
}
```

## Array item types

```typescript
const users = [
  { name: "Alice", id: 1 },
  { name: "Bob", id: 2 },
];

type User = typeof users[number]; // {name: string; id: number;}
type UserName = User["name"]; // string
type UserId = User["id"]; // number

const Charlie: User = { name: "Charlie", id: 3 };
```

## Object key/value literal types

```typescript
type ValueOf<T> = T[keyof T];

const currencies = {
  GBP: "£",
  USD: "$",
  EUR: "€",
} as const;

type CurrencyId = keyof typeof currencies; // type "GBP" | "USD" | "EUR"
type CurrencySymbolV1 = ValueOf<typeof currencies>; // type "£" | "$" | "€"
type CurrencySymbolV2 = typeof currencies[keyof typeof currencies]; // type "£" | "$" | "€"
```

## Object structure with literal keys

```typescript
type Index = "a" | "b" | "c";
type FromIndex<K extends string> = { [key in K]: number };

const obj: FromIndex<Index> = { a: 1, b: 2, c: 3 };
```

## Freshness

- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/freshness)

TypeScript provides a concept of _Freshness_ (also called strict object literal checking) to make it easier to type check
object literals that would otherwise be structurally type compatible.

Structural typing has a weakness in that it allows you to misleadingly think that something accepts more data than it
actually does. This is demonstrated in the following code which TypeScript will error on as shown:

```typescript
function logName(something: { name: string }) {
  console.log(something.name);
}

logName({ name: "matt" }); // okay
logName({ name: "matt", job: "being awesome" }); // Error
// object literals must only specify known properties.
// `job` is excessive here.
```

Note that this error only happens on object literals.

Solution: Allowing extra properties

A type can include an index signature to explicitly indicate that excess properties are permitted:

```typescript
function logName(something: { name: string; [key: string]: string }) {
  console.log(something.name);
}
```

## Index signatures

### Using a limited set of string literals

- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/index-signatures#using-a-limited-set-of-string-literals)

An index signature can require that index strings be members of a union of literal strings by using Mapped Types:

```typescript
type Index = "a" | "b" | "c";
type FromIndex = { [k in Index]: number };
type FromSomeIndex<K extends string> = { [key in K]: number };

const obj1: FromIndex = { a: 1, b: 2, c: 3 };
const obj2: FromSomeIndex<Index> = { a: 1, b: 2, c: 3 };
```

### Nested index signature

- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/index-signatures#design-pattern-nested-index-signature)

Try not to mix string indexers with _valid_ values this way, it might introduce typos in NestedCSS type:

```typescript
interface NestedCSS {
  color?: string;
  [selector: string]: string | NestedCSS | undefined;
}

const failsSilently: NestedCSS = {
  colour: "red", // No error as `colour` is a valid string selector
};
```

Instead separate out the nesting into its own property e.g. in a name like nest (or children or subnodes etc.):

```typescript
interface NestedCSS {
  color?: string;
  nest?: {
    [selector: string]: NestedCSS;
  };
}
```

## Mapped types

Remove `optional` attributes from a type's properties:

```typescript
[Property in keyof Type]-?: Type[Property];
```

Remove `readonly` attributes from a type's properties:

```typescript
-readonly [Property in keyof Type]: Type[Property];
```

### Key Remapping via as

- [Release notes - TypeScript 4.1](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#key-remapping-via-as)

You can leverage features like template literal types to create new property names from prior ones:

```typescript
type Getters<Type> = {
  [Property in keyof Type as `get${Capitalize<string & Property>}`]: () => Type[Property];
};
```

You can filter out keys by producing never via a conditional type:

```typescript
type RemoveKindField<Type> = {
  [Property in keyof Type as Exclude<Property, "kind">]: Type[Property];
};
```

You can map over arbitrary unions, not just unions of `string | number | symbol`, but unions of any type:

```typescript
type EventConfig<Events extends { kind: string }> = {
  [E in Events as E["kind"]]: (event: E) => void;
};
```

A mapped type using a conditional type which returns either a `true` or `false` depending on whether an object has the
property `pii` set to the literal `true`:

```typescript
type ExtractPII<Type> = {
  [Property in keyof Type]: Type[Property] extends { pii: true } ? true : false;
};
```

## Variadic tuple types

- [Release notes - TypeScript 4.0](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#variadic-tuple-types)

Example of concatenate function in JavaScript:

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

## Type Retrospective Versioning

- [basarat.gitbook.io](https://basarat.gitbook.io/typescript/type-system/discriminated-unions#retrospective-versioning)

You can add versioning retrospectively by creating a new union with literal number (or string if you want).
