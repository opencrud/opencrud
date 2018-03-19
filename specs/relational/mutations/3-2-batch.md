# Mutationa: Batch Operations

* Overview
* Update
* Delete

## Overview

OpenCRUD exposes the followig mutations to manipulate a batch of data records. The count field returns a count of the number of records affected

## Update

```graphql
mutation {
  updateManyUsers(where: {name_not: "Karl"}, data:{name: "Karl"}) {
    count
  }
}
```

## Delete

```graphql
mutation {
  deleteManyUsers(where: {name_not: "Karl"}) {
    count
  }
}
```