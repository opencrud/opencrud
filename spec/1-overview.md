# Overview

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
