# Queries: Filters

* Overview
* Filters
* Unique Filters
* Filter Fields
  * Scalar Fields
  * Relation Fields
  * Boolean Expressions
* Example 

## Overview

OpenCRUD filters are designed to surface as many capabilities of the underlying database as possible while maintaining a simple and intuitive API surface. 

In general, a filter is an input object that has optional fields which describe the filtering operation. We distinguish between regular filters and unique filters. Filters are available on all top level fields and relation fields.

## Filters

A regular, non-unique filter allows filtering by all scalar fields and all relational fields of a type. It will have optional fields for each scalar field and each relational field, according to the field type. 

## Unique filters

A unique filter works the same way as a regular filter, but only allows filtering on unique scalar fields. 

## Filter Fields

The available fields of the filter for each field depend on the type of a field. For example an Integer field supports the filtering on numeric order while a String field supports matching on substrings.

For each filed in the data type, the fields listed below are generated, where `field` is replaced by the field name, and `[T]` is replaced by the type, where applicable.

### Scalar filter fields

#### String filters

```graphql
# String field
field: String # equals
field_not: String # not equals
field_contains: String # contains substring
field_not_contains: String # does not contain substring
field_starts_with: String
field_not_starts_with: String
field_ends_with: String
field_not_ends_with: String
field_lt: String # less than
field_lte: String # less then or equals
field_gt: String # greater than
field_gte: String # greater than or equals
```
#### Integer Filters
```graphql
# Integer field
field: Integer # equals
field_not: Integer # not equals
field_lt: Integer # less than
field_lte: Integer # less then or equals
field_gt: Integer # greater than
field_gte: Integer # greater than or equals
```

#### Float filters
```graphql
# Float field
field: Float # equals
field_not: Float # not equals
field_lt: Float # less than
field_lte: Float # less then or equals
field_gt: Float # greater than
field_gte: Float # greater than or equals
```

#### Boolean filters
```
# Boolean field
field: Boolean # equals
field_not: Boolean # not equals
```

#### DateTime filters
```
# DateTime field
field: DateTime # equals
field_not: DateTime # not equals
field_in: [DateTime] # in list
field_not_in: [DateTime] # not in list
field_lt: DateTime # less than
field_lte: DateTime # less then or equals
field_gt: DateTime # greater than
field_gte: DateTime # greater than or equals
```

#### Enum filters
```
# Enum field
field: Enum # equals
field_not: Enum # not equals
```

#### List filters
```
# List[T] field
field_contains: T # contains single scalar T
field_contains_every: [T] # contains all scalar T
field_contains_some: [T] # contains at least 1 scalar T
```

### Relation filter fields

In relational databases it is common to filter based on columns in a related table. In OpenCRUD this concept is called relation filters.

#### Many relation filter fields
```
# Many Relation field
field_every: Filter # condition must be true for all nodes
field_some: Filter # condition must be true for at least 1 node
field_none: Filter # condition must be false for all nodes
field_is_null: Boolean # is the relation field null
```

In this context, `Filter` is a filter object for the related type.

#### One relation filter field
```
# one Relation field
field: UniqueFilter # condition must be true for related node
```

In this context, `UniqueFilter` is a unique filter object for the related type.

#### Example

The following query retrieves all users that are related to the post with id `1`.

```graphql
{
  users(where:{posts_some:{id: "1"}}){
    name
  }
}
```

The same result could be achieved by inverting the query, however the result format would be different:

```graphql
{
  post(where: {id: "1"}) {
    author {
      name
    }
  }
}
```

### Boolean expressions

Filter conditions can be nested and combined arbitrarily using the boolean expressions `AND` and `OR`. A unique filter can only have nested unique filters, a non-unique filter can only have nested non-unique filters. 

```graphql
{
  users(where: {OR: [
    {name_not_in: ["Karl", "Viggo"]},
  	{AND: [{id: "1"}, {name: "Karl"}]}
  ]}) {
    name
  }
}

```

Two filter conditions on the same level are an explicit `AND`, so the above query can be simplified like this:

```graphql
{
  users(where: {OR: [
    {name_not_in: ["Karl", "Viggo"]},
  	{id: "1", name: "Karl"}
  ]}) {
    name
  }
}
```

## Example

**Data Model**

```graphql
type User {
  id: ID! @unique
  name: String!
  posts: [Post!]!
}
```

**Generated Schema**

```graphql
input UserWhereInput {
  id: ID
  id_not: ID
  id_in: [ID!]
  id_not_in: [ID!]
  id_lt: ID
  id_lte: ID
  id_gt: ID
  id_gte: ID
  id_contains: ID
  id_not_contains: ID
  id_starts_with: ID
  id_not_starts_with: ID
  id_ends_with: ID
  id_not_ends_with: ID
  name: String
  name_not: String
  name_in: [String!]
  name_not_in: [String!]
  name_lt: String
  name_lte: String
  name_gt: String
  name_gte: String
  name_contains: String
  name_not_contains: String
  name_starts_with: String
  name_not_starts_with: String
  name_ends_with: String
  name_not_ends_with: String
  posts_every: PostWhereInput
  posts_some: PostWhereInput
  posts_none: PostWhereInput
  AND: [UserWhereInput!]
  OR: [UserWhereInput!]
  NOT: [UserWhereInput!]
}

input UserWhereUniqueInput {
  id: ID
}
```

The filter for the `Post` type is omitted in this example. 

