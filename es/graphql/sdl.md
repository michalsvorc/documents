
GraphQL enables declarative data fetching where the client can specify exactly what data it needs from an API. GraphQL minimizes the amount of data that needs to be transferred over the network and thus majorly improves applications operating under these conditions. During execution, GraphQL will wait for Promises, Futures, and Tasks to complete before continuing and will do so with optimal concurrency.

# Documentation \




* [Learn](https://graphql.org/learn/)
* [API](https://graphql.org/graphql-js/graphql/)
* [Best practices](https://graphql.org/learn/best-practices/)

# Read \




* [GraphQL & Caching: The Elephant in the Room](https://www.apollographql.com/blog/graphql-caching-the-elephant-in-the-room-11a3df0c23ad)
* [Query execution - step by step](https://www.apollographql.com/blog/graphql-explained-5844742f195e#987d)
* [Intro to GraphQL | Next.js GraphQL Serverless Tutorial](https://hasura.io/learn/graphql/nextjs-fullstack-serverless/intro-to-graphql/)

# Types

In every GraphQL schema, you can define your own scalar and object types. An often cited example for a custom scalar would be a Date type where the implementation needs to define how that type is validated, serialized, and deserialized.

## Scalar Types \


They represent concrete units of data. The GraphQL spec has five predefined scalars:

- String

- Int

- Float

- Boolean

- ID

## Object Types \


They have fields that express the properties of that type and are composable. 

# SDL

query

mutation

schema {

  // Root types

  query: Query

  mutation: Mutation

  Subscription: Subscription

}

type: [object types and fields](https://graphql.org/learn/schema/#object-types-and-fields)

[fragment](https://graphql.org/learn/queries/#fragments) … on \
[scalar](https://graphql.org/learn/schema/#scalar-types): define custom scalar type 

[enum](https://graphql.org/learn/schema/#enumeration-types) \
[interface](https://graphql.org/learn/schema/#interfaces)

[union](https://graphql.org/learn/schema/#union-types)

[input](https://graphql.org/learn/schema/#input-types) 

__typename: [meta fields](https://graphql.org/learn/queries/#meta-fields)

 \
... on : [inline fragment](https://graphql.org/learn/queries/#inline-fragments)

@include(if: Boolean): [directive](https://graphql.org/learn/queries/#directives)

@skip(if: Boolean): [directive](https://graphql.org/learn/queries/#directives)

@unique

 \
!: non-nullable type modifier

## [Introspection](https://graphql.org/learn/introspection/)

 \
__schema

 \
__Schema \
__Type \
__TypeKind

__Field

__InputValue

__EnumValue

__Directive

## Comments

"Description for argument"

 \
""" \
Multiline description \
"""

These help consumers of your data graph discover fields and learn how to use them.

