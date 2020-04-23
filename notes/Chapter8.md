# Chapter 8
Sending messages with GraphQL mutations

GraphQL mutations - a method for sending and applying mutations in our back-end.

Mutation is a remote procedure call (RPC), meaning it is used to trigger a function on the server, but unlike other protocols which have RPCs, GraphQL Mutation also includes a query, which means the client can ask for data once the operation is complete.
=> 데이터 변경이 끝난 이후 데이터 요청도 한 번에 할 수 있다.

## Optimistic Response
 a common pattern that will update the state of the component twice so we can have a better UX: First it updates the component's state with the predicted result, and then it will update the state with the actual result.

Apollo-Client stores the data in a hash, where the key represents the query and the value represents the retrieved result. This means that the cache will need to be updated for

- chats query : which we already did, without really diving into the reason behind it.
- chat(chatId : $chatId) where chatId is the chat that was just mutated.

## GraphQL fragment
A GraphQL fragment is a shared piece of query logic.

    fragment NameParts on Person {
    firstName
    lastName
    }

    query GetPerson {
    people(id: "7") {
        ...NameParts
        avatar(size: LARGE)
    }
    }
=> It's important to note that the component after the onclause is designated for the type we are selecting from. In this case, peopleis of type Personand we want to select the firstNameand lastNamefields from people(id: "7").
=> 특정 데이터 타입의 일부분(fragment)를 이미 정의해놓은거임.

## fragment id
When working with a fragment we need to compose its ID, just like explained earlier. The default mapping function called 
### defaultDataIdFromObject
can be imported from apollo-cache-inmemory
and be used to specify the fragment that we would like to read/write


