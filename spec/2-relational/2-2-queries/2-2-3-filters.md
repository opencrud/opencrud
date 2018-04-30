# Queries: Filters

* Overview
* Data types
* Single field
* Multi field
* Boolean expressions
* Cross-relation filters

## Overview

OpenCRUD filters are designed to surface as many capabilities of the underlying database as possible while maintaining a simple and intuitive API surface. Filters are available on all top level fields and relation fields.

## Data types

The available filters depend on the type of a field. For example an Integer field supports the greater than filter while a String field supports the contains filter that match on substrings.

```graphql
type UserWhereInput {
  AND: [UserWhereInput]
  OR: [UserWhereInput]

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
  field_in: [String] # in list
  field_not_in: [String] # not in list

  # Integer field
  field: Integer # equals
  field_not: Integer # not equals
  field_lt: Integer # less than
  field_lte: Integer # less then or equals
  field_gt: Integer # greater than
  field_gte: Integer # greater than or equals
  field_in: [Integer] # in list
  field_not_in: [Integer] # not in list
  
  # Float field
  field: Float # equals
  field_not: Float # not equals
  field_lt: Float # less than
  field_lte: Float # less then or equals
  field_gt: Float # greater than
  field_gte: Float # greater than or equals
  field_in: [Float] # in list
  field_not_in: [Float] # not in list
  
  # Boolean field
  field: Boolean # equals
  field_not: Boolean # not equals
  
  # DateTime field
  field: DateTime # equals
  field_not: DateTime # not equals
  field_in: [DateTime] # in list
  field_not_in: [DateTime] # not in list
  field_lt: DateTime # less than
  field_lte: DateTime # less then or equals
  field_gt: DateTime # greater than
  field_gte: DateTime # greater than or equals
  
  # Enum field
  field: Enum # equals
  field_not: Enum # not equals
  field_in: [Enum] # in list
  field_not_in: [Enum] # not in list
  
  # List[T] field
  field_contains: T # contains single scalar T
  field_contains_every: [T] # contains all scalar T
  field_contains_some: [T] # contains at least 1 scalar T
 
  # many Relation field
   field_every: FilterCondition # condition must be true for all nodes
  field_some: FilterCondition # condition must be true for at least 1 node
  field_none: FilterCondition # condition must be false for all nodes
  field_is_null: Boolean # is the relation field null
 
  # one Relation field
  field: UserWhereInput # condition must be true for related node
}
```

## Single field

Fields for relations to a single data record allow you to filter by exact matches on unique fields:

```graphql
{
  user(where: {id: "1"}){
    name
  }
}
```

## Multi field

Fields for relations to many data records allow you to filter by all filters specified above:

```graphql
{
  users(where: {name_not_in:["Karl", "Viggo"]}){
    name
  }
}
```

## Boolean expressions

Filter conditions can be nested and combined arbitrarily using the boolean expressions `AND` and `OR`: 

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

## Cross-relation filters

In relational databases it is common to filter based on columns in a related table. In OpenCRUD this concept is called relation filters. The following query retrieves all users that are related to the post with id `1`.

```graphql
{
  users(where:{posts_some:{id: "1"}}){
    name
  }
}
```

The same result could be achieved by inverting the query:

```graphql
{
  post(where: {id: "1"}) {
    author {
      name
    }
  }
}
```

Relation filters have the same power as normal filters and can use one of tree modifiers:

* every
* none
* some

```graphql
{
  every: users(where:{posts_every:{id: "1"}}){name}
  none: users(where:{posts_none:{id: "1"}}){name}
  some: users(where:{posts_some:{id: "1"}}){name}
}
```
