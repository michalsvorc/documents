# SDL

GraphQL enables declarative data fetching where the client can specify exactly what data it needs from an API. GraphQL
minimizes the amount of data that needs to be transferred over the network and thus majorly improves applications
operating under these conditions. During execution, GraphQL will wait for Promises, Futures, and Tasks to complete
before continuing and will do so with optimal concurrency.

## Documentation \

- [Learn](https://graphql.org/learn/)
- [API](https://graphql.org/graphql-js/graphql/)
- [Best practices](https://graphql.org/learn/best-practices/)

## Read

- [GraphQL & Caching: The Elephant in the Room](https://www.apollographql.com/blog/graphql-caching-the-elephant-in-the-room-11a3df0c23ad)
- [Query execution - step by step](https://www.apollographql.com/blog/graphql-explained-5844742f195e#987d)
- [Intro to GraphQL | Next.js GraphQL Serverless Tutorial](https://hasura.io/learn/graphql/nextjs-fullstack-serverless/intro-to-graphql/)

## Types

In every GraphQL schema, you can define your own scalar and object types. An often cited example for a custom scalar
would be a Date type where the implementation needs to define how that type is validated, serialized, and deserialized.

### Scalar Types

They represent concrete units of data. The GraphQL spec has five predefined scalars:

- String
- Int
- Float
- Boolean
- ID

### Object Types

They have fields that express the properties of that type and are composable.
