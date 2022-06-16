# Queries

- [Documentation](https://graphql.org/learn/queries/)
- [Operation Name](https://graphql.org/learn/queries/#operation-name)
- [Arguments](https://graphql.org/learn/queries/#arguments)
- [Variables](https://graphql.org/learn/queries/#variables)
- [Aliases](https://graphql.org/learn/queries/#aliases)

## Directives

- [Documentation](https://graphql.org/learn/queries/#directives) \

We might also need a way to dynamically change the structure and shape of our queries using variables. A directive can
be attached to a field or fragment inclusion, and can affect execution of the query in any way the server desires.

- `@include(if: Boolean)`: Only include this field in the result if the argument is true.
- `@skip(if: Boolean)`: Skip this field if the argument is true.

## Meta fields

- [Documentation](https://graphql.org/learn/queries/#meta-fields)

Given that there are some situations where you don't know what type you'll get back from the GraphQL service, you need
some way to determine how to handle that data on the client.

Search returns a union type that can be one of three options. It would be impossible to tell apart the different types
from the client without the \_\_typename field.

## Fragments

- [Documentation](https://graphql.org/learn/queries/#fragments)

A fragment is a collection of fields on a specific type. Fragments let you construct sets of fields, and then include
them in queries where you need to. Fragments are great when you need to reuse different fields on a query.

If you are querying a field that returns an interface or a union type, you will need to use [inline
fragments](https://graphql.org/learn/queries/#inline-fragments) to access data on the underlying concrete type.

## Mutations

- [Documentation](https://graphql.org/learn/queries/#mutations)

While query fields are executed in parallel, mutation fields run in series, one after the other. This means that if we
send two incrementCredits mutations in one request, the first is guaranteed to finish before the second begins, ensuring
that we don't end up with a race condition with ourselves.

## Subscriptions

Subscriptions represent a stream of data sent over to the client, a real-time connection to the server in order to get
immediately informed about important events. When a client subscribes to an event, it will initiate and hold a steady
connection to the server.

After a client sends this subscription to a server, a connection is opened between them. Then, whenever a new mutation
is performed that creates a new Person, the server sends information about this person over to the client:

## Errors

A successful GraphQL query is supposed to return a JSON object with a root field called "data". If the request fails or
partially fails (e.g. because the user requesting the data doesn’t have the right access permissions), a second root
field called "errors" is added to the response:
