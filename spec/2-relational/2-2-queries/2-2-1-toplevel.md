# Queries: Top level

* Overview
* Single fields multi fields
* Multi connection fields
* Node field
* Example

## Overview

GraphQL defines the top level `Query` type. OpenCRUD defines multiple top level fields that are generated for each database type (table in a relational database)

## Single fields

Retrieve a single data record.

## Multi fields

Retrieve multiple data records

## Multi connection fields

Retrieve multiple data records. This field is [Relay compliant](https://facebook.github.io/relay/docs/en/graphql-server-specification.html) and contains the `aggregate` and `groupBy` sub fields.

## Node field

The node field is specified by the [Relay spec](https://facebook.github.io/relay/docs/en/graphql-server-specification.html) and allow a client to retrieve any data record by its id.

## Naming

OpenCRUD does not specify how fields generated for each data type must be named. It is up to each OpenCRUD implementation define a naming system. The reference implementation uses the followig naming convention:

- single field: `[data type name]`
- multi field: `[pluralized data type name]` (using the [evo-inflector library](https://github.com/atteo/evo-inflector))
- multi connecton field: `[pluralized data type name]Connection`

OpenCRUD implementations can choose to make field names configurable instead of convention based.

## Example

This example illustrates all top level fields

**Data Model**

```graphql
type User {
  id: ID! @unique
  name: String!
}
```

**Generated Schema**

```graphql
type Query {
  users(
    where: UserWhereInput
    orderBy: UserOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): [User]!
  user(where: UserWhereUniqueInput!): User
  usersConnection(
    where: UserWhereInput
    orderBy: UserOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): UserConnection!
  node(id: ID!): Node
}
```

**Query**

```graphql
query {
  user(where: { id: "1" }) {
    name
  }
  users(where: { name_contains: "Karl" }) {
    name
  }
  usersConnection(where: { name_contains: "Karl" }) {
    edges {
      node {
        name
      }
    }
  }
  node(id: "1") {
    name
  }
}
```
