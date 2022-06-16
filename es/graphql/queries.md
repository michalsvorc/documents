
# [Queries](https://graphql.org/learn/queries/)



* [Operation Name](https://graphql.org/learn/queries/#operation-name)

## [Arguments](https://graphql.org/learn/queries/#arguments)

```js


```
{
  human(id: "1000") {
    name
    height(unit: FOOT)
  }
}
```


``` \


## [Variables](https://graphql.org/learn/queries/#variables)

```js


```
query HeroNameAndFriends($episode: Episode) {
  hero(episode: $episode) {
    name
    friends {
      name
    }
  }
}

// Variables
{
  "episode": "JEDI"
}
```


```

## [Aliases](https://graphql.org/learn/queries/#aliases)

One of GraphQL’s major strengths is that it lets you send multiple queries in a single request. However, since the response data is shaped after the structure of the fields being requested, you might run into naming issues when you’re sending multiple queries asking for the same fields:

```js


```
{
  User(id: "1") {
    name
  }
  User(id: "2") {
    name
  }
}
```


```

In fact, this will produce an error with a GraphQL server, since it’s the same field but different arguments. . The only way to send a query like that would be to use aliases, i.e. specifying names for the query results:

 \
```js


```
{
  firstUser: User(id: "1") {
    name
  }
  secondUser: User(id: "2") {
    name
  }
}
```


```

## [Directives](https://graphql.org/learn/queries/#directives) \


We might also need a way to dynamically change the structure and shape of our queries using variables. A directive can be attached to a field or fragment inclusion, and can affect execution of the query in any way the server desires.  \




* @include(if: Boolean) Only include this field in the result if the argument is true.
* @skip(if: Boolean) Skip this field if the argument is true.

 \
```js


```
query Hero($episode: Episode, $withFriends: Boolean!) {
  hero(episode: $episode) {
    name
    friends @include(if: $withFriends) {
      name
    }
  }
}
```


```

 \
# [Meta fields](https://graphql.org/learn/queries/#meta-fields)

 \
Given that there are some situations where you don't know what type you'll get back from the GraphQL service, you need some way to determine how to handle that data on the client. 

 \
Search returns a union type that can be one of three options. It would be impossible to tell apart the different types from the client without the __typename field.


```
{
  search(text: "an") {
    __typename
    ... on Human {
      name
    }
    ... on Droid {
      name
    }
    ... on Starship {
      name
    }
  }
}





{
  "data": {
    "search": [
      {
        "__typename": "Human",
        "name": "Han Solo"
      },
      {
        "__typename": "Human",
        "name": "Leia Organa"
      },
      {
        "__typename": "Starship",
        "name": "TIE Advanced x1"
      }
    ]
  }
}
```


# [Fragments](https://graphql.org/learn/queries/#fragments)

A fragment is a collection of fields on a specific type. Fragments let you construct sets of fields, and then include them in queries where you need to. Fragments are great when you need to reuse different fields on a query.

```js


```
type User {
  name: String!
  age: Int!
  email: String!
  street: String!
  zipcode: String!
  city: String!
}

// Here, we could represent all the information that relates to the user's // physical address into a fragment:

fragment addressDetails on User {
  name
  street
  zipcode
  city
}

// And use it in query

{
  allUsers {
    ... addressDetails
  }
}
```


```

If you are querying a field that returns an interface or a union type, you will need to use [inline fragments](https://graphql.org/learn/queries/#inline-fragments) to access data on the underlying concrete type.  \


```js


```
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    ... on Droid {
      primaryFunction
    }
    ... on Human {
      height
    }
  }
}
```


``` \


# [Mutations](https://graphql.org/learn/queries/#mutations)

 \
While query fields are executed in parallel, mutation fields run in series, one after the other. This means that if we send two incrementCredits mutations in one request, the first is guaranteed to finish before the second begins, ensuring that we don't end up with a race condition with ourselves. \


```js


```
mutation {
  createPerson(name: "Bob", age: 36) { # root field of mutation
    name # mutation response fields
    age
  }
}

# Response
"createPerson": {
  "name": "Bob",
  "age": 36,
}
```


```

# Subscriptions

Subscriptions represent a stream of data sent over to the client,  a real-time connection to the server in order to get immediately informed about important events. When a client subscribes to an event, it will initiate and hold a steady connection to the server.  \


```js


```
subscription {
  newPerson {
    name
    age
  }
}
```


```

After a client sends this subscription to a server, a connection is opened between them. Then, whenever a new mutation is performed that creates a new Person, the server sends information about this person over to the client:

```js


```
{
  "newPerson": {
    "name": "Jane",
    "age": 23
  }
}
```


``` \


# Errors

A successful GraphQL query is supposed to return a JSON object with a root field called "data". If the request fails or partially fails (e.g. because the user requesting the data doesn’t have the right access permissions), a second root field called "errors" is added to the response:

```js

{

  "data": { ... },

  "errors": [ ... ]

}

```

 \


