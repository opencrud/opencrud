# Queries: Sorting

## Overview
 
The sort order input type is an enum, with fields generated according to the associated data type. 

## Generated Fields

For each non-list scalar type, two enum fields are generated, one for ordering ascending, one for ordering descending. The name of the enum fields are `[field name]_ASC`, `[field name]_DESC`.

## Example

**Datamodel**

```graphql
type User {
  id: ID! @unique
  name: String!
}
```

**Generated Schema**

TODO: Does this implicitely include createdAt and updatedAt fields? 

```graphql
enum UserOrderByInput {
  id_ASC
  id_DESC
  name_ASC
  name_DESC
  createdAt_ASC
  createdAt_DESC
  updatedAt_ASC
  updatedAt_DESC
}
```