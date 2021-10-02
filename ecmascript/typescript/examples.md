# TypeScript examples

## Get the values of an object

```typescript
type ValueOf<T> = T[keyof T];
```

## Get property of a type

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
type UserName = User["name"];     // string
type UserId = User["id"];         // number

const Charlie: User = { name: "Charlie", id: 3 }
```

## Object key/value literal types

```typescript
type ValueOf<T> = T[keyof T];

const currencies = {
  GBP: '£',
  USD: '$',
  EUR: '€',
} as const 

type CurrencyId = keyof typeof currencies;                          // type "GBP" | "USD" | "EUR"
type CurrencySymbolV1 = ValueOf<typeof  currencies>                 // type "£" | "$" | "€"
type CurrencySymbolV2 = typeof currencies[keyof typeof currencies]  // type "£" | "$" | "€"
```

## Object structure with literal keys

```typescript
type Index = 'a' | 'b' | 'c'
type FromIndex<K extends string> = { [key in K]: number }

const obj: FromIndex<Index> = {a: 1, b: 2, c: 3}
```

## Freshness

* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/freshness)

TypeScript provides a concept of *Freshness* (also called strict object literal checking) to make it easier to type check
object literals that would otherwise be structurally type compatible.

Structural typing has a weakness in that it allows you to misleadingly think that something accepts more data than it
actually does. This is demonstrated in the following code which TypeScript will error on as shown:

```typescript
function logName(something: { name: string }) {
  console.log(something.name);
}

logName({ name: 'matt' }); // okay
logName({ name: 'matt', job: 'being awesome' });  // Error
                                                  // object literals must only specify known properties.
                                                  // `job` is excessive here.
```

Note that this error only happens on object literals.

Solution: Allowing extra properties

A type can include an index signature to explicitly indicate that excess properties are permitted:


```typescript
function logName(something: { name: string, [key: string]: string }) {
  console.log(something.name);
}
```
