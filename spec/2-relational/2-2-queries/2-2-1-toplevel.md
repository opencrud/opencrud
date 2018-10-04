# Queries: Top level

* Overview
* Single fields
* Multi fields
* Multi connection fields
* Node field
* Example

## Overview

GraphQL defines the top level `Query` type. OpenCRUD defines multiple top level fields that are generated for each existing type in the data model: **single fields**, **multi fields** and **connection fields**. Each query field might take several input arguments of types that depent on the types in the data model.

## Single fields

Retrieve a single data record, allows filtering.

The type of this field is always a model type. 

#### Arguments 
* `where`, a unique filter. 

## Multi fields

Retrieve multiple data records, allows filtering, sorting and pagination.

The type of this field is always a list of type model type. 

#### Arguments
* `where`, a filter.
* `orderBy`, a sort order (TODO, find a better name). 
* `skip`, an integer, specifying how many matching nodes to skip before returing a node as result. 
* `after`, an ID, specifying up to which node nodes are skipped before returning a node as the result. 
* `before`, an ID, specifying for up to which node nodes should be returned as result. 
* `first`, an integer, specifying how many matching nodes to return. 
* `last`, an integer, specifying how many matching nodes to return, counting form the end of the result set.

## Multi connection fields

Retrieve multiple data records. This field is [Relay compliant](https://facebook.github.io/relay/docs/en/graphql-server-specification.html) and allows filtering, sorting, aggregation and pagination. 

The type of this field is a connection type, which has the following `pageInfo`, `aggregate` and `edges` subfields. The `edges` subfield is of type list of edge, where each edge contains the actual node. The `pageInfo` subfield is of type `PageInfo` subfield contains pagination information for the current result set.  

### Arguments
The arguments are equal to the connection field. 

## Node field

The node field is specified by the [Relay spec](https://facebook.github.io/relay/docs/en/graphql-server-specification.html) and allow a client to retrieve any data record by its id.

The type of this field is the special type `Node`.

### Arguments
* `id`, the ID of the node to return. 

## Remarks

### Naming

OpenCRUD does not specify how fields, connection types and input types generated for each data type must be named. It is up to each OpenCRUD implementation define a naming system. The reference implementation uses the followig naming convention:

- single field: `[data type name]`
- multi field: `[pluralized data type name]` (using the [evo-inflector library](https://github.com/atteo/evo-inflector))
- multi connecton field: `[pluralized data type name]Connection`
- unique filters: `[data type name]WhereUniqueInput`
- filters: `[data type name]WhereInput`
- sort order: `[data type name]OrderByInput`
- connection type: `[data type name]Connection`
- edge type: `[data type name]Edge`

OpenCRUD implementations can choose to make field names configurable instead of convention based.

## Example

This example illustrates all top level fields for simple object without any relation. 

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

  user(
  	where: UserWhereUniqueInput!
  ): User
  
  users(
  	where: UserWhereInput, 
    orderBy: UserOrderByInput, 
    skip: Int, 
    after: String, 
    before: String, 
    first: Int, 
    last: Int
  ): [User]!
  
  usersConnection(
  	where: UserWhereInput, 
    orderBy: UserOrderByInput, 
    skip: Int, 
    after: String, 
    before: String, 
    first: Int, 
    last: Int
  ): UserConnection!
  
  node(id: ID!): Node
}
```

Input types for filters, aggregation, pagination and sorting as well as model types are omitted in this example.

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
