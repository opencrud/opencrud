# Mutations: Input Types

* Overview
* Create
* Update
* Delete
* Example

## Overview

OpenCRUD exposes specific types for the `create`, `update` and `delete` fields. These types also enable nested create and update operations. 

## Create

A create input type generally contains a field for each field in the associated data model. If the field is required in the data model, it will be required in the create model input type as well. 

### Scalar Fields

The create input type exposes a scalar field of matching name and type for each scalar field in the datamodel.

### Single Relations

If the relation can not be navigated from both sides, the input object has two fields: 
* `create`, a create input for the associated type. 
* `connect`, a unique filter for the associated type. 

If the relation can be navigated from both sides, the input object has two fields: 
* `create`, a special create input for the associated type, in which the relation is not present. 
* `connect`, a unique filter for the associated type. 

### Multi Relations

Multi relations behave similar as single relations. The only difference is that the `create` and `connect` fields are lists. 

## Update

An update input type generally contains a field for each field in the associated data model. All fields are optional. 

### Scalar Fields

The update input type exposes an optional scalar field matching name and type for each scalar field in the datamodel. 

### Single Relations

If the relation can not be navigated from both sides, the input object has five fields: 
* `create`, a create input for the associated type.
* `update`, an update input for the associated type.
* `delete`, a boolean.
* `disconnect`, a boolean, only present if the related field is not required.
* `connect`, a unique filter for the associated type. 
	
If the relation can be navigated from both sides, the input object has five fields: 
* `create`, a special create input for the associated type, in which the relation is not present. 
* `update`, a special update input for the associated type, in which the relation is not present.
* `delete`, a boolean.
* `disconnect`, a boolean, only present if the related field is not required.
* `connect`, a unique filter for the associated type. 

### Multi Relations

If the relation can not be navigated from both sides, the input object has five fields: 
* `create`, a list of create input for the associated type. 
* `connect`, a list of unique filter for the associated type. 
* `delete`, a list of unique filter for the associated type.
* `disconnect`, a list of unique filter for the associated type. 
* `update`, a list of input object with two fields:	
	* `where`, a unique filter for the associated type.	
	* `data`, an update input for the associated type. 

If the relation can not be navigated from both sides, the input object has five fields: 
* `create`, a list of special create input for the associated type, in which the relation is not present. 
* `connect`, a list of unique filter for the associated type. 
* `delete`, a list of unique filter for the associated type.
* `disconnect`, a list of unique filter for the associated type. 
* `update`, a list of input object with two fields:	
	* `where`, a unique filter for the associated type.	
	* `data`, a special update input for the associated type, in which the relation is not present.  

## Example

**Data Model**

```graphql
type User {
  id: ID! @unique
  name: String!
}
```

**Generated**

Top level create and update types: 

```graphql
input UserCreateInput {
  name: String!
  posts: PostCreateManyWithoutUserInput
}

input UserUpdateInput {
  name: String
  posts: PostUpdateManyWithoutUserInput
}

input PostCreateInput {
  text: String!
  user: UserCreateOneWithoutPostsInput!
}

input PostUpdateInput {
  text: String
  user: UserUpdateOneWithoutPostsInput
}
```

Other types:

```graphql
input PostUpdateManyWithoutUserInput {
  create: [PostCreateWithoutUserInput!]
  delete: [PostWhereUniqueInput!]
  connect: [PostWhereUniqueInput!]
  disconnect: [PostWhereUniqueInput!]
  update: [PostUpdateWithWhereUniqueWithoutUserInput!]
}

input PostUpdateWithoutUserDataInput {
  text: String
}

input PostUpdateWithWhereUniqueWithoutUserInput {
  where: PostWhereUniqueInput!
  data: PostUpdateWithoutUserDataInput!
}

input PostCreateManyWithoutUserInput {
  create: [PostCreateWithoutUserInput!]
  connect: [PostWhereUniqueInput!]
}

input PostCreateWithoutUserInput {
  text: String!
}

input UserCreateOneWithoutPostsInput {
  create: UserCreateWithoutPostsInput
  connect: UserWhereUniqueInput
}

input UserCreateWithoutPostsInput {
  name: String!
}

input UserUpdateOneWithoutPostsInput {
  create: UserCreateWithoutPostsInput
  update: UserUpdateWithoutPostsDataInput
  delete: Boolean
  connect: UserWhereUniqueInput
}

input UserUpdateWithoutPostsDataInput {
  name: String
}
```
