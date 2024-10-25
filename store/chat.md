# Documentation for `actionTypes.js`

Welcome to the comprehensive documentation for the `actionTypes.js` file in our project. This file plays a crucial role in defining action types for handling different states in our application, particularly related to chats, groups, contacts, and messages.

## 📜 Index
1. [Introduction](#introduction)
2. [Purpose of Action Types](#purpose-of-action-types)
3. [Action Types Overview](#action-types-overview)
    - [Chats](#chats)
    - [Groups](#groups)
    - [Contacts](#contacts)
    - [Messages](#messages)
4. [Conclusion](#conclusion)

---

## Introduction

The **`actionTypes.js`** file is responsible for declaring constants that represent the various action types used throughout our application. These action types are utilized in Redux to describe a specific change or event occurring within the app.

## Purpose of Action Types

**Action types** serve as a bridge between components and reducers in a Redux architecture. They ensure consistency and prevent errors that might arise from string literals used in multiple places. 📑 By using constants, we can easily manage and update our application states.

## Action Types Overview

Below is a detailed breakdown of the action types defined in the `actionTypes.js` file. Each section is dedicated to a specific feature of the application.

### 🗨️ Chats

- **GET_CHATS**: Initiates the process of retrieving chat data.
- **GET_CHATS_SUCCESS**: Indicates the successful retrieval of chat data.
- **GET_CHATS_FAIL**: Denotes a failure in retrieving chat data.

### 👥 Groups

- **GET_GROUPS**: Starts the process of fetching group information.
- **GET_GROUPS_SUCCESS**: Confirms successful acquisition of group data.
- **GET_GROUPS_FAIL**: Signifies an error in fetching group information.

### 📇 Contacts

- **GET_CONTACTS**: Begins the retrieval of contact details.
- **GET_CONTACTS_SUCCESS**: Marks the successful retrieval of contact data.
- **GET_CONTACTS_FAIL**: Highlights a failure in obtaining contact information.

### 💬 Messages

- **GET_MESSAGES**: Initiates the fetching of message data.
- **GET_MESSAGES_SUCCESS**: Indicates successful retrieval of messages.
- **GET_MESSAGES_FAIL**: Points to a failure in retrieving message data.
- **POST_ADD_MESSAGE**: Starts the process of adding a new message.
- **POST_ADD_MESSAGE_SUCCESS**: Confirms the successful addition of a new message.
- **POST_ADD_MESSAGE_FAIL**: Indicates a failure in adding a new message.

## Conclusion

The `actionTypes.js` file is an essential component of the Redux setup in our application. By defining action types, it helps maintain a clear and consistent flow of data and state changes. 🛠️ Using constants prevents errors and simplifies the process of managing actions across various parts of the application.

With this structured documentation, developers can quickly understand the purpose and implementation of each action type, contributing to a more efficient and error-free development process. 🌟

Feel free to explore each action type and its usage in the respective reducers and components to gain a deeper understanding of the Redux flow in our application.

# 📄 Documentation for `actions.js`

This document provides a comprehensive overview of the `actions.js` file in a Redux-based architecture. This file is responsible for defining action creators that dispatch actions to the Redux store. Actions are plain JavaScript objects that represent an intention to change the state.

## 📋 Index

1. [Introduction](#introduction)
2. [Action Creators](#action-creators)
   * [Chats](#chats)
   * [Groups](#groups)
   * [Messages](#messages)
3. [Understanding Action Creators](#understanding-action-creators)
4. [Summary](#summary)

## 📝 Introduction

In Redux, **actions** are payloads of information that tell the store how to change its state. These actions are dispatched to the store using **action creators**. In `actions.js`, we define action creators for managing chats, groups, and messages.

### 🎨 Action Types

The file imports action types from `actionTypes.js`, which define the constant values representing different action types. Here’s a brief look at the imports:

```javascript
import { 
  GET_CHATS, 
  GET_CHATS_FAIL, 
  GET_CHATS_SUCCESS, 
  GET_GROUPS, 
  GET_GROUPS_FAIL, 
  GET_GROUPS_SUCCESS, 
  GET_MESSAGES, 
  GET_MESSAGES_FAIL, 
  GET_MESSAGES_SUCCESS, 
  POST_ADD_MESSAGE, 
  POST_ADD_MESSAGE_FAIL, 
  POST_ADD_MESSAGE_SUCCESS 
} from "./actionTypes";
```

## ⚙️ Action Creators

Below are the action creators defined in the `actions.js` file:

### 💬 Chats

- **`getChats`**: Initiates the fetching of chat data.
  ```javascript
  export const getChats = () => ({
    type: GET_CHATS,
  });
  ```

- **`getChatsSuccess`**: Dispatched when chat data is successfully fetched.
  ```javascript
  export const getChatsSuccess = chats => ({
    type: GET_CHATS_SUCCESS,
    payload: chats,
  });
  ```

- **`getChatsFail`**: Dispatched when there is an error fetching chat data.
  ```javascript
  export const getChatsFail = error => ({
    type: GET_CHATS_FAIL,
    payload: error,
  });
  ```

### 👥 Groups

- **`getGroups`**: Initiates the fetching of group data.
  ```javascript
  export const getGroups = () => ({
    type: GET_GROUPS,
  });
  ```

- **`getGroupsSuccess`**: Dispatched when group data is successfully fetched.
  ```javascript
  export const getGroupsSuccess = groups => ({
    type: GET_GROUPS_SUCCESS,
    payload: groups,
  });
  ```

- **`getGroupsFail`**: Dispatched when there is an error fetching group data.
  ```javascript
  export const getGroupsFail = error => ({
    type: GET_GROUPS_FAIL,
    payload: error,
  });
  ```

### 📩 Messages

- **`getMessages`**: Initiates the fetching of messages for a particular room.
  ```javascript
  export const getMessages = roomId => ({
    type: GET_MESSAGES,
    roomId,
  });
  ```

- **`getMessagesSuccess`**: Dispatched when messages are successfully fetched.
  ```javascript
  export const getMessagesSuccess = messages => ({
    type: GET_MESSAGES_SUCCESS,
    payload: messages,
  });
  ```

- **`getMessagesFail`**: Dispatched when there is an error fetching messages.
  ```javascript
  export const getMessagesFail = error => ({
    type: GET_MESSAGES_FAIL,
    payload: error,
  });
  ```

- **`addMessage`**: Initiates the process of adding a new message.
  ```javascript
  export const addMessage = message => ({
    type: POST_ADD_MESSAGE,
    message,
  });
  ```

- **`addMessageSuccess`**: Dispatched when a message is successfully added.
  ```javascript
  export const addMessageSuccess = message => ({
    type: POST_ADD_MESSAGE_SUCCESS,
    payload: message,
  });
  ```

- **`addMessageFail`**: Dispatched when there is an error adding a message.
  ```javascript
  export const addMessageFail = error => ({
    type: POST_ADD_MESSAGE_FAIL,
    payload: error,
  });
  ```

## 🧠 Understanding Action Creators

### What are Action Creators?

**Action creators** are functions that create actions. They are the primary way to interact with the Redux store to update the application state.

### Why Use Action Creators?

- **Consistency**: They ensure that the actions follow a consistent shape.
- **Maintainability**: Easier to manage and scale as the application grows.
- **Decoupling**: They abstract away the action creation logic from the components.

## 🏁 Summary

The `actions.js` file defines the necessary action creators for handling chats, groups, and messages in a Redux-based application. By dispatching these actions, the application can update the state accordingly, ensuring that the UI reflects the current application state.

This documentation provides a detailed overview of the action creators and their purposes, offering a clear understanding of their roles in the Redux flow. By using these action creators, developers can manage state changes in a predictable and scalable manner.

# Saga.js Documentation 📜

Welcome to the documentation for the `saga.js` file! This file uses Redux-Saga to manage side effects in your application. Let's dive deep into understanding its purpose and functionality.

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Saga Functions](#saga-functions)
    - [onGetChats](#ongetchats)
    - [onGetGroups](#ongetgroups)
    - [onGetMessages](#ongetmessages)
    - [onAddMessage](#onaddmessage)
4. [Main Saga](#main-saga)
5. [Conclusion](#conclusion)

## Introduction 🌟

`redux-saga` is a library that aims to make side effects (e.g., asynchronous tasks like data fetching) in a Redux application easier to manage, more efficient to execute, and better at handling failures. This file, `saga.js`, is designed to handle chat-related actions like fetching chats, groups, messages, and adding messages.

## Imports 📦

The file begins with importing necessary functions and actions:

```javascript
import { takeEvery, put, call } from "redux-saga/effects"
import { GET_CHATS, GET_GROUPS, GET_MESSAGES, POST_ADD_MESSAGE } from "./actionTypes"
import { getChatsSuccess, getChatsFail, getGroupsSuccess, getGroupsFail, getMessagesSuccess, getMessagesFail, addMessageSuccess, addMessageFail } from "./actions"
import { getChats, getGroups, getMessages, addMessage } from "../../helpers/fakebackend_helper"
```

- **Redux-Saga Effects**: 
  - `takeEvery`: Watches for dispatched actions and runs the saga.
  - `put`: Dispatches an action.
  - `call`: Invokes a function, useful for calling API endpoints.

- **Action Types and Actions**: Imports action types and corresponding action creators from other files.

- **Helper Methods**: Imports functions that simulate backend requests.

## Saga Functions 🛠️

### onGetChats

Handles the fetching of chat data.

```javascript
function* onGetChats() {
    try {
        const response = yield call(getChats)
        yield put(getChatsSuccess(response))
    } catch (error) {
        yield put(getChatsFail(error))
    }
}
```

- **call(getChats)**: Calls the `getChats` function.
- **put(getChatsSuccess(response))**: Dispatches success action with the data.
- **put(getChatsFail(error))**: Dispatches fail action if an error occurs.

### onGetGroups

Handles the fetching of group data.

```javascript
function* onGetGroups() {
    try {
        const response = yield call(getGroups)
        yield put(getGroupsSuccess(response))
    } catch (error) {
        yield put(getGroupsFail(error))
    }
}
```

- Similar to `onGetChats`, but for groups.

### onGetMessages

Handles the retrieval of messages for a specific room.

```javascript
function* onGetMessages({ roomId }) {
    try {
        const response = yield call(getMessages, roomId)
        yield put(getMessagesSuccess(response))
    } catch (error) {
        yield put(getMessagesFail(error))
    }
}
```

- **call(getMessages, roomId)**: Calls the `getMessages` function with `roomId`.
- Fetches messages based on a specific chat room.

### onAddMessage

Handles adding a new message.

```javascript
function* onAddMessage({ message }) {
    try {
        const response = yield call(addMessage, message)
        yield put(addMessageSuccess(response))
    } catch (error) {
        yield put(addMessageFail(error))
    }
}
```

- **call(addMessage, message)**: Calls the `addMessage` function with the message data.
- Used for adding messages to the chat.

## Main Saga 🚀

```javascript
function* chatSaga() {
    yield takeEvery(GET_CHATS, onGetChats)
    yield takeEvery(GET_GROUPS, onGetGroups)
    yield takeEvery(GET_MESSAGES, onGetMessages)
    yield takeEvery(POST_ADD_MESSAGE, onAddMessage)
}
```

- **chatSaga**: A generator function that watches for dispatched actions (`GET_CHATS`, `GET_GROUPS`, `GET_MESSAGES`, `POST_ADD_MESSAGE`) and runs the corresponding saga function for each action.

## Conclusion 🎉

The `saga.js` file is a crucial part of handling asynchronous tasks in the Redux framework using `redux-saga`. It ensures that fetching and posting operations are managed efficiently and can handle success or failure scenarios gracefully. 

Understanding this file helps in managing side effects and ensures a smooth flow of data in your application's chat functionalities.

# 📄 Reducer.js Documentation

Welcome to the **Reducer.js** documentation! This file is a crucial part of managing the application's state in a Redux architecture. Here, we define how different actions modify the state and ensure the application behaves consistently.

## 🎯 Purpose

The **Reducer.js** file is responsible for managing and updating the application's state based on dispatched actions. It listens for specific action types and updates the state accordingly, ensuring that the UI reflects the latest data.

## 📂 Initial State

The reducer starts with an initial state, defined as follows:

```javascript
const INIT_STATE = {
  chats: [],
  groups: [],
  contacts: [],
  messages: [],
  error: {},
};
```

### Initial State Breakdown

- **chats**: An empty array to store chat data.
- **groups**: An empty array to store group data.
- **contacts**: An empty array to store contact data.
- **messages**: An empty array to store message data.
- **error**: An object to store any errors encountered.

## 🔄 Reducer Function: `Calendar`

The main function in this file is the `Calendar` reducer, which takes the current state and an action as parameters, and returns a new state based on the action type.

### 🎨 Function Structure

```javascript
const Calendar = (state = INIT_STATE, action) => {
  switch (action.type) {
    // Handle success actions
    case GET_CHATS_SUCCESS:
      return { ...state, chats: action.payload };
    case GET_GROUPS_SUCCESS:
      return { ...state, groups: action.payload };
    case GET_CONTACTS_SUCCESS:
      return { ...state, contacts: action.payload };
    case GET_MESSAGES_SUCCESS:
      return { ...state, messages: action.payload };
    case POST_ADD_MESSAGE_SUCCESS:
      return { ...state, messages: [...state.messages, action.payload] };

    // Handle fail actions
    case GET_CHATS_FAIL:
    case GET_GROUPS_FAIL:
    case GET_CONTACTS_FAIL:
    case GET_MESSAGES_FAIL:
    case POST_ADD_MESSAGE_FAIL:
      return { ...state, error: action.payload };

    // Default state
    default:
      return state;
  }
};
```

### 🌟 Action Types and Effects

Below is a table of action types handled by the reducer and their effects on the state:

| **Action Type**                 | **Effect**                                                                 |
|---------------------------------|----------------------------------------------------------------------------|
| `GET_CHATS_SUCCESS`             | Updates `chats` with the payload.                                          |
| `GET_CHATS_FAIL`                | Updates `error` with the payload.                                          |
| `GET_GROUPS_SUCCESS`            | Updates `groups` with the payload.                                         |
| `GET_GROUPS_FAIL`               | Updates `error` with the payload.                                          |
| `GET_CONTACTS_SUCCESS`          | Updates `contacts` with the payload.                                       |
| `GET_CONTACTS_FAIL`             | Updates `error` with the payload.                                          |
| `GET_MESSAGES_SUCCESS`          | Updates `messages` with the payload.                                       |
| `GET_MESSAGES_FAIL`             | Updates `error` with the payload.                                          |
| `POST_ADD_MESSAGE_SUCCESS`      | Appends new message to `messages`.                                         |
| `POST_ADD_MESSAGE_FAIL`         | Updates `error` with the payload.                                          |

## 📤 Export

Finally, the reducer is exported for use in the Redux store:

```javascript
export default Calendar;
```

## 🎨 Summary

The **Reducer.js** file is an essential part of a Redux-based application, handling the modification of state based on dispatched actions. It listens for both success and failure actions and updates the state accordingly, ensuring the application's data layer is in sync with the operations performed by the user and the backend responses.

This documentation should provide a comprehensive understanding of how the reducer operates and how it interacts with the rest of the Redux setup. Happy coding! 🚀