# Queries: Pagination

* Overview
* PageInfo

## Overview

Pagination is possible on multi fields, as well as multi connection fields by using the `skip`, `first`, `last`, `before` and `after` arguments. Multi connection fields provide a `pageInfo` field for the current result set, which exposes pagination information. 

## PageInfo

The `PageInfo` type is as type of the `pageInfo` field of a connection type. It contains pagination information for the current result set. The `PageInfo` type is not associated with any specific data type and only exists once. 

**Definition**

```graphql
type PageInfo {
  hasNextPage: Boolean!
  hasPreviousPage: Boolean!
  startCursor: String # Id of the first node in the result set
  endCursor: String # Id of the lsat node in the result set
}
```
