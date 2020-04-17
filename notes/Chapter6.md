# Chapter 6
## ChatRoomScreen 을 만들기 위한 변경

(1) typeDefs.graphql 의 내용을 변경
=> Chat type 에 messages field 를 포함시킨다.

(2) resolver 수정
Chat type 에서 messages field 를 받을 수 있도록.
(이렇게 작동하도록)

(3) (1)&(2) 에서 schema 를 변경했으니,
Query 추가.
=> parameter 가 있는 query

Note that unlike the chats query, this time we have a parameter. The parameters are provided to the resolver function as the second parameter as a JSON. Using the provided parameter - the chat ID, we will find and return the relevant chat from the DB.

    // resolver 내의 Query 에 적힌 동작.
    chat(root: any, { chatId }: any) {
      return chats.find(c => c.id === chatId);
    },

## Error handling tip
If you experience any TypeScript related issues with the following error:

    Object literal may only specify known properties, and 'variables' does not exist in type 'Query'.
    Add the following declaration file to your project:

    // under types dir
    // file name : apollo-server-testing.d.ts

    declare module 'apollo-server-testing' {
    import { ApolloServerBase } from 'apollo-server-core';
    import { print, DocumentNode } from 'graphql';
    import { GraphQLResponse } from 'graphql-extensions';
    type StringOrAst = string | DocumentNode;
    // A query must not come with a mutation (and vice versa).
    type Query<TVariables> = {
        query: StringOrAst;
        mutation?: undefined;
        variables?: TVariables;
    };
    type Mutation<TVariables> = {
        mutation: StringOrAst;
        query?: undefined;
        variables?: TVariables;
    };
    export const createTestClient: <TVariables>(
        server: ApolloServerBase
    ) => {
        query: (query: Query<TVariables>) => Promise<GraphQLResponse>;
        mutate: (mutation: Mutation<TVariables>) => Promise<GraphQLResponse>;
    };
    }


