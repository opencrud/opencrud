<p align="center"><img src="https://i.imgur.com/t8WPeTM.png" width="150" /></p>

# OpenCRUD

OpenCRUD is a GraphQL CRUD API specification for databases

## Overview

OpenCRUD is a fully [GraphQL compliant](http://facebook.github.io/graphql/) query language to access and modify data. OpenCRUD provides API flavours for many popular databases including MySQL and MongoDB.

For example, this OpenCRUD query retrieves a single user:

```graphql
{
  user(where: { id: 4 }) {
    name
  }
}
```

returns:

```json
{
  "user": {
    "name": "Mark Zuckerberg"
  }
}
```

## Rationale

GraphQL is a flexible query language supporting many different data access patterns. In practice, simple CRUD operations turn out to be a very common pattern. Standardising this very common pattern enables the community to build tooling specific to the common CRUD style API.

## Reference Implementation

[Prisma](https://github.com/graphcool/prisma) serves as a reference implementation of OpenCRUD

## Projects compatible with OpenCRUD

- [Prisma](https://github.com/graphcool/prisma)
- [GraphCMS](https://graphcms.com)
- [PostGraphile](https://github.com/graphile/postgraphile) (planned)
- [VulcanJS](https://github.com/VulcanJS/Vulcan) (planned)
- [Strapi](https://github.com/strapi/strapi) [(planned)](https://github.com/strapi/strapi/issues/1057)

> Feel free to create a PR to add your project to the list

## Index

- Specs
    - SDL for data modelling: non normative
    - relational
        - [Intro](https://github.com/opencrud/opencrud/blob/master/specs/relational/1-intro.md)
            - Areas covered
            - Focus on API, not implementation/runtime characteristics
        - Queries
            - [Top level](https://github.com/opencrud/opencrud/blob/master/specs/relational/queries/2-1-toplevel.md)
                - Single fields multi fields
                - Multi field conenctions
                - Node field
            - [Relations](https://github.com/opencrud/opencrud/blob/master/specs/relational/queries/2-2-relations.md)
                - Both simple and connection
                - Connections
                    - Aggregations
                    - Cursor
            - [Filters](https://github.com/opencrud/opencrud/blob/master/specs/relational/queries/2-3-filters.md)
                - Data type specific filters
                - Single node
                - Multi node
                - Cross-relation filters
            - [Aggregations](https://github.com/opencrud/opencrud/blob/master/specs/relational/queries/2-4-aggregations.md)
        - Mutations
            - [CRUD](https://github.com/opencrud/opencrud/blob/master/specs/relational/mutations/3-1-CRUD.md)
                - Overview
                - Create
                - Update
                - Delete
            - [Batch mutations](https://github.com/opencrud/opencrud/blob/master/specs/relational/mutations/3-2-batch.md)
                - Overview
                - Update
                - Delete
            - [Nested mutations](https://github.com/opencrud/opencrud/blob/master/specs/relational/mutations/3-3-nested.md)
            - Return type
        - Subscriptions
        - Generated type names
