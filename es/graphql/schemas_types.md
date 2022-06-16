
# Read 

[Schemas and Types](https://graphql.org/learn/schema/)

Design your schema based on how data is used, not based on how it's stored. In GraphQL, it's recommended for every mutation's response to include the data that the mutation modified. This enables clients to obtain the latest persisted data without needing to send a followup query.

# [object-types-and-fields](https://graphql.org/learn/schema/#object-types-and-fields)

```js \
type Character {

  name: String!

  appearsIn: [Episode!]! \
  length(unit: LengthUnit = METER): Float # Argument

}

``` \
 \
All arguments are named. Unlike languages like JavaScript and Python where functions take a list of ordered arguments, all arguments in GraphQL are passed by name specifically. In this case, the length field has one defined argument, unit.

# [Scalar Types](https://graphql.org/learn/schema/#scalar-types) \




* Int: A signed 32‐bit integer.
* Float: A signed double-precision floating-point value.
* String: A UTF‐8 character sequence.
* Boolean: true or false.
* ID: The ID scalar type represents a unique identifier, often used to refetch an object or as the key for a cache. The ID type is serialized in the same way as a String; however, defining it as an ID signifies that it is not intended to be human‐readable.

 \
## ID (scalar type)

 \


ID is serialized exactly the same as String type; therefore, if you were to replace ID with String, the computer would see no difference in it. However, what is important to you is that YOU as a programmer know for sure that it's a unique identifier.

 \
```js


```
type Person {
  id: ID!
  name: String!
  age: Int!
}
```


```

# [Enumerations](https://graphql.org/learn/schema/#enumeration-types)

 \
```js

enum Episode {

  NEWHOPE

  EMPIRE

  JEDI

} \
```

This means that wherever we use the type Episode in our schema, we expect it to be exactly one of NEWHOPE, EMPIRE, or JEDI.

# [Lists and non-null](https://graphql.org/learn/schema/#lists-and-non-null)

```js


```
myField: [String!]
// This means that the list itself can be null, but it can't have any null members

myField: null // valid
myField: [] // valid
myField: ['a', 'b'] // valid
myField: ['a', null, 'b'] // error

myField: [String]!
// This means that the list itself cannot be null, but it can contain null values

myField: null // error
myField: [] // valid
myField: ['a', 'b'] // valid
myField: ['a', null, 'b'] // valid
```


```

# [Interface](https://graphql.org/learn/schema/#interfaces)

 \
```js

interface Character {

  id: ID!

  name: String!

  friends: [Character]

  appearsIn: [Episode]! \
} \
 \
type Human implements Character {

  id: ID!

  name: String!

  friends: [Character]

  appearsIn: [Episode]!

  starships: [Starship]

  totalCredits: Int

}

``` \
 \
You can see that both of these types have all of the fields from the Character interface, but also bring in extra fields, totalCredits, starships and primaryFunction, that are specific to that particular type of character. \
 \


# [Union](https://graphql.org/learn/schema/#union-types) \
 \
```js \
union SearchResult = Human | Droid | Starship

```

# [Input](https://graphql.org/learn/schema/#input-types)

 \
Passing complex objects as variables. Instead of accepting three arguments, mutation could accept a single input type that includes all three fields. 

The fields on an input object type can themselves refer to input object types, but you can't mix input and output types in your schema. Input object types also can't have arguments on their fields. \
 \
```js

input ReviewInput {

  stars: Int!

  commentary: String \
}

```

Do not use the same input type for both queries and mutations. In many cases, arguments that are required for a mutation are optional for a corresponding query.

# [Naming conventions](https://www.apollographql.com/docs/apollo-server/schema/schema/#naming-conventions)

