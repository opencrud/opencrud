# Mutations: CRUD

* Overview
* Create
* Update
* Delete
* Usage Examples

## Overview

OpenCRUD exposes `create`, `update` and `delete` fields on the top-level `Mutation` type.

### Naming

As with the top-level query type, OpenCRUD does enforce naming of the fields. The reference implementation uses `create[type name]`, `update[type name]` and `delete[type name]`. 

### Nesting of mutations

Nesting of mutations is enabled by providing relation fields in the respective [input types](2-3-3-input-types.md) of the mutatoin. 

## Create

Create a single data record. Nested creation of multiple records is possible. 

The type of this field is the associated model object type. 

### Arguments
* `data`, a model create input. 

## Update

Update a single data record. Nested update of multiple records is possible. 

The type of this field is the associated model object type. 

### Arguments
* `data`, a model update input. 
* `where`, a unique filter for the associated data type, specifying the record to update. 

## Delete

Deletes a single data record. 

The type of this field is the associated model object type. 

### Arguments
* `where`, a unique filter for the associated data type, specifying the record to delete. 

## Example

**Data Model**

```graphql
type User {
  id: ID! @unique
  name: String!
}
```

**Usage**

```graphql
mutation {
  createUser(data: { name: "Karl" }) {
    id
  }
}
```

```graphql
mutation {
  updateUser(where: { id: "1" }, data: { name: "Karl" }) {
    id
  }
}
```

```graphql
mutation {
  deleteUser(where: { id: "1" }) {
    id
  }
}
```