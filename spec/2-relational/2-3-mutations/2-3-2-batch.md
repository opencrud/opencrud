# Mutationa: Batch Operations

* Overview
* Update
* Delete
* Examples

## Overview

OpenCRUD exposes the followig mutations to update or delete a set of data records.

### Naming

As with the top-level query type, OpenCRUD does enforce naming of the fields. The reference implementation uses `updateMany[pluralized type name]` and `deleteMany[pluralized type name]`. 

## Update

Updates a set of data records. Nested updates of multiple records is possible. 

The type of this field exposes a single field with the name `count` of type `Long`.

### Arguments
* `data`, a model update input. 
* `where`, a filter for the associated data type, specifying the record to update. 

## Delete

Deletes a set of data records. 

The type of this field exposes a single field with the name `count` of type `Long`. 

### Arguments
* `where`, a filter for the associated data type, specifying the record to delete. 

## Examples

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
  deleteManyUsers(where: {name_not: "Karl"}) {
    count
  }
}
```

```graphql
mutation {
  updateManyUsers(where: {name_not: "Karl"}, data:{name: "Karl"}) {
    count
  }
}
```