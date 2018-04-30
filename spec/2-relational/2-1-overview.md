# Relational

* Areas covered
* Focus on API, not implementation/runtime characteristics
* SDL

## Areas covered

This specification describes all aspects of a flexible GraphQL API suitable for relational databases.

## Focus on API, not implementation/runtime characteristics

OpenCrud is a collection of specifications for GraphQL APIs that are designed to work well with specific database technologies. OpenCRUD is concerned with the API surface, not the implementation. As such two implementations of OpenCRUD could choose to store data in different ways, but applications interacting with the data through the OpenCRUD API wouldn't be able to tell the difference.

## SDL

Examples are used throughout this spec to show the final schema generated for a specific data model. In all examples, the SDL notation is used to define the data model. The benefit of SDL is that it is database independent, so we can use the same notation accross all supported databases.

The following directives have special meaning when used in example SDL in this spec:

- `@unique`: The field has a unique constraint
- `@relation`: specifies a relation between two fields

## Queries

### [Queries: Top level](2-2-queries/2-2-1-toplevel.md)

### [Queries: Relations](2-2-queries/2-2-2-relations.md)

### [Queries: Filters](2-2-queries/2-2-3-filters.md)

### [Queries: Aggregations](2-2-queries/2-2-4-aggregations.md)

## Mutations

### [Mutations: CRUD](2-3-mutations/2-3-1-crud.md)

### [Mutations: Batch](2-3-mutations/2-3-2-batch.md)

### [Mutations: Nested](2-3-mutations/2-3-3-nested.md)
