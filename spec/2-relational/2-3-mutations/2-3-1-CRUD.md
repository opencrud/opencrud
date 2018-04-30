# Mutations: CRUD

* Overview
* Create
* Update
* Delete

## Overview

OpenCRUD exposes the following mutations to do simple data manipulation

## Create

Create a single data racord:

```graphql
mutation {
  createUser(data: { name: "Karl" }) {
    id
  }
}
```

## Update

```graphql
mutation {
  updateUser(where: { id: "1" }, data: { name: "Karl" }) {
    id
  }
}
```

## Delete

```graphql
mutation {
  deleteUser(where: { id: "1" }) {
    id
  }
}
```
