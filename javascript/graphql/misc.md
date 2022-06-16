# Libraries

- [Documentation](https://graphql.org/code/#javascript)
- [Prisma](https://www.prisma.io/)
- [Hasura](https://hasura.io/)

## Fluent GraphQL Clients

Allow writing GraphQL queries as objects. In addition to freeing you from strings, they offer:

- Strong typing
- Single source of truth for type definitions
- Auto-completion of queries

## JSON GZIP

It's encouraged that any production GraphQL services enable GZIP and encourage their clients to send the header:

## Server Bathing and compiler

The compiler approach lets you map a GraphQL query of any depth to one database query. This is more performant if your
GraphQL query deals with data from the database. However, if data is coming from different sources, the compiler
approach works well for database parts of the query and the DataLoader batching works best for batching external data
sources/HTTP requests.

## Security

### Timeout for large queries

### Maximum query depth

By analyzing the query document’s abstract syntax tree (AST), a GraphQL server is able to reject or accept a request
based on its depth.

### Query Complexity

Certain fields in our schema are known to be more complex to compute than others. Query complexity allows you to define
how complex these fields are, and to restrict queries by implementing a maximum complexity. The idea is to define how
complex each field is by using a simple number.

### Throttling

In most APIs, a simple throttle is used to stop clients from requesting resources too often. GraphQL is a bit special
because throttling on the number of requests does not really help us. Even a few queries might be too much if they are
very large.

### Based on Server Time

A good estimate of how expensive a query is, is the server time it needs to complete. We can use this heuristic to
throttle queries.

### Based on Query Complexity

Just like a time throttle, we can come up with a maximum cost (Bucket Size) per time a client can use.
