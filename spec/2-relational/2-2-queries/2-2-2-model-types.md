# Queries: Model Types

* Overview
* Scalar Fields
* Relation Field
* Example

## Overview

Model Types directly map to data types in the database. They have one field for each scalar field and each relation. 

## Scalar Fields

Sclar fields map directly. Each scalar field present in the model will generate a scalar field for this model type. 

## Relation Fields

### Multi Relation

Each multi relation in the database will generate a multi field, exactly as described in [the top level specification](./2-2-1-toplevel.md).

TODO: Will there be a connection type as well? 

### Single Relation

Each single relation will generate a field field of the same name, where the type of the field is the model type of the related type. 

## Example

**Data Model**

```graphql
type User {
  id: ID! @unique
  name: String!
  posts: [Post!]!
}

type Post {
  id: ID! @unique
  text: String!
  user: User!
}
```

**Generated Model Types**

```
type User {
  id: ID!
  name: String!
  posts(
  	where: PostWhereInput, 
    orderBy: PostOrderByInput, 
    skip: Int, 
    after: String, 
    before: String, 
    first: Int, 
    last: Int
  ): [Post!]
}

type Post {
  id: ID!
  text: String!
  user: User!
}
```
