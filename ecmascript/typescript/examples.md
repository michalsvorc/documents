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

## Array item type

```typescript
const array = [
  { name: "Alice", id: 1 },
  { name: "Bob", id: 2 },
  { name: "Eve", id: 3 }
];

type ArrayItem = typeof array[number];

const item: ArrayItem = { name: "Alice", id: 1 }
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
