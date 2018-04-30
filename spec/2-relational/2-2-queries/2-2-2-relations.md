# Queries: Relations

* Overview
* Connections
  * Aggregations
  * Cursor
* Example

## Overview

In relational databases a relation is used to connecto two related tables. OpenCRUD defines how relations are exposed in the GraphQL schema.
Relations in OpenCRUD generate two fields:

* `multi fields` are great for most cases where you need to retrieve related data
* `multi connection fields` are compatible with Relay and contain the aggrete and groupBy fields that enable avdanced aggregations.

## Connections

> WIP

## Example

This example illustrates all top level fields

**Data Model**

```graphql
type User {
  id: ID! @unique
  name: String!
  posts: [Post!]!
}

type Post {
  id: ID! @unique
  title: String!
}
```

**Generated Schema**

```graphql
type User implements Node {
  id: ID!
  name: String!
  posts(
    where: PostWhereInput
    orderBy: PostOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): [Post!]
  postsConnection(
    where: PostWhereInput
    orderBy: PostOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): PostConnection!
}

type Post implements Node {
  id: ID!
  title: String!
}
```

**Query**

```graphql
query {
  user(where: {id: "1"}) {
    name
    posts {
      title
    }
    postsConnection {
      edges {
        node {
          title
        }
      }
    }
  }
}
```
