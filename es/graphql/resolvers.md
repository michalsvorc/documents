# Resolvers

- [Documentation](https://graphql.org/learn/execution/#root-fields-resolvers)

A function on a GraphQL server that's responsible for fetching the data for a single field

When a field is executed, the corresponding resolver is called to produce the next value. This continues until scalar
values are reached. GraphQL queries always end at scalar values.

On a server, the query is traversed field by field, executing "resolvers" for each field. GraphQL provides default
resolvers for trivial fields.

```javascript
query: Query {
  author(id: "abc"): Author {
posts: [Post] {
title: String
         content: String
       }
  }
}
```

Now, we can easily find the resolvers in our server to run for every field. The execution starts at the query type and
goes **breadth-first**. This means we run the resolver for Query.author first. Then, we take the result of that resolver
and pass it into its child, the resolver for Author.posts. At the next level, the result is a list, so in that case, the
execution algorithm runs on one item at a time.

Every GraphQL query has the shape of a tree — i.e. it is never circular. Execution begins at the root of the query. At
the end, the execution algorithm puts everything together into the correct shape for the result and returns that.

## Batched Resolving and loaders

Let’s imagine we wanted to get the authors of several posts, like so:

```javascript
query {
  posts {
    title
      author {
        name
          avatar
      }
  }
}
```

If these are posts on a blog, it’s likely that many of the posts will have the same authors. So if we need to make an
API call to get each author object, we might accidentally make multiple requests for the same one.

This can be resolved with DataLoader. Batching of resolvers solves the performance problem to a large extent. It reduces
multiple hits to the database. But, even with batching, there would still be multiple hits to the database depending on
the depth of the query.

The compiler approach lets you map a GraphQL query of any depth to one database query. This is more performant if your
GraphQL query deals with data from the database. However, if data is coming from different sources, the compiler
approach works well for database parts of the query and the DataLoader batching works best for batching external data
sources/HTTP requests.
