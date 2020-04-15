# Chapter4
REST API 말고, GraphQL을 이용하여 만들어보자!

## GraphQL
It allows clients to define the structure of the data required, and the exact same structure of data will be returned from the server, therefore preventing excessively large amounts of data from being returned.

Unlike REST, GraphQL APIs are organized in terms of types and fields, not endpoints.

In GraphQL, the API is based on a schema built from many entities that we call object types. Think of GraphQL as something similar to TypeScript but for API. Object types are like interfaces, they describe the shape of an entity.
=> 오호, TS 를 아는 사람에게는 좋은 설명!

### In TypeScript you would describe a Chat as:

    interface Chat {
    id: string;
    name: string;
    picture: string;
    lastMessage: Message;
    }

    interface Message {
    id: string;
    content: string;
    createdAt: number;
    }

### GraphQL:

    type Chat {
    id: String
    name: String
    picture: String
    lastMessage: Message
    }

    type Message {
    id: String
    content: String
    createdAt: Float
    }

## scalar & type
To define a concrete data without any inner schema definition, scalars are used in GraphQL. For example; Int, Float, Date, URLand EmailAddress.
### Custom Scalars,types
Any custom scalar can be declared with the scalar keyword, and custom types can be declared with the type keyword. Scalars have their own internal validation, parsing and serialization logics.

### apollo-server-express
 Apollo's implementation for the GraphQL Express REST endpoint.

### @types/graphql
TypeScript definitions. Notice that we didn't need to install Apollo's types library. That is because Apollo themselves writes their source code in Typescript so we get a ready Typescript code directly from their library.

### .graphql file extension
a more convenient way to work with a GraphQL schema. The exported result should be a simple string that we can use to compose our GraphQL schema. The clear advantage of working with a dedicated file is that we get to have syntax highlight.

### resolvers
Now we will implement the resolvers. Resolvers functions, presented in a JSON object, that correspond to each field in the GraphQL schema. <b>Each resolver name should match the field name it represents.</b> It will accept as a parameter the parent resolver value (we'll explain that process in a second), can run any logic, like calling a server, and returns a value that correspond to the type it has in the schema

### graphql-scalars
Note that we've implemented a custom scalar named Date and URL but we will need an implementation for it. We will use graphql-scalars that has many custom scalars ready-to-use.

### graphql-tools
 a library with a set of utilities that will help us create a schema that will be compatible with Apollo's API