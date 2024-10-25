# Documentation: `actions.js` 📜

This file defines a set of **Redux actions** used within the application. These actions are essential for managing state transitions in response to various events or operations. Below is a comprehensive explanation of each action and its purpose.

## Index 📚

1. **Overview**
2. **Actions and Their Usage**
   - Event Actions
   - Category Actions
3. **Import Statements**
4. **Conclusion**

---

## 1. Overview 🌟

In Redux, **actions** are payloads of information that send data from the application to the Redux store. These actions are triggered by user interactions or other events, which in turn can dispatch changes to the application state. The `actions.js` file is responsible for defining these actions related to:

- **Events**: Creating, updating, deleting, and fetching events.
- **Categories**: Fetching categories.

These actions are used alongside **action creators** to facilitate the dispatch of actions and to handle asynchronous operations, such as API calls.

## 2. Actions and Their Usage 🚀

### Event Actions

| Action Creator Function            | Action Type               | Description                                                                                                 |
|------------------------------------|---------------------------|-------------------------------------------------------------------------------------------------------------|
| `getEvents()`                      | `GET_EVENTS`              | Initiates the process to fetch events from the server.                                                      |
| `getEventsSuccess(events)`         | `GET_EVENTS_SUCCESS`      | Dispatched when events are successfully fetched, where `events` is the payload containing event details.    |
| `getEventsFail(error)`             | `GET_EVENTS_FAIL`         | Dispatched when there is an error fetching events, with `error` detailing the issue encountered.            |
| `addNewEvent(event)`               | `ADD_NEW_EVENT`           | Initiates the addition of a new event, with `event` being the details of the event to add.                  |
| `addEventSuccess(event)`           | `ADD_EVENT_SUCCESS`       | Dispatched upon successful addition of an event, where `event` is the newly added event's details.          |
| `addEventFail(error)`              | `ADD_EVENT_FAIL`          | Dispatched when there is a failure in adding a new event, with `error` providing the failure details.       |
| `updateEvent(event)`               | `UPDATE_EVENT`            | Initiates the update process for an existing event, with `event` being the updated event's details.         |
| `updateEventSuccess(event)`        | `UPDATE_EVENT_SUCCESS`    | Dispatched upon successful update of an event, where `event` is the updated event's information.            |
| `updateEventFail(error)`           | `UPDATE_EVENT_FAIL`       | Dispatched when there is an error updating an event, with `error` detailing the problem encountered.        |
| `deleteEvent(event)`               | `DELETE_EVENT`            | Initiates the process to delete an event, where `event` specifies which event is to be removed.             |
| `deleteEventSuccess(event)`        | `DELETE_EVENT_SUCCESS`    | Dispatched upon successful deletion of an event, with `event` confirming the event that was deleted.        |
| `deleteEventFail(error)`           | `DELETE_EVENT_FAIL`       | Dispatched when there is a failure in deleting an event, with `error` providing information on the problem. |

### Category Actions

| Action Creator Function          | Action Type                  | Description                                                                                            |
|----------------------------------|------------------------------|--------------------------------------------------------------------------------------------------------|
| `getCategories()`                | `GET_CATEGORIES`             | Initiates the process to fetch categories from the server.                                             |
| `getCategoriesSuccess(categories)`| `GET_CATEGORIES_SUCCESS`     | Dispatched when categories are successfully fetched, with `categories` containing the category details.|
| `getCategoriesFail(error)`        | `GET_CATEGORIES_FAIL`        | Dispatched when there is an error fetching categories, with `error` detailing the issue encountered.   |

## 3. Import Statements 📦

At the top of the file, several action type constants are imported from `actionTypes.js`. These constants represent the types of actions that are dispatched within the application.

```javascript
import { 
  GET_EVENTS, GET_EVENTS_FAIL, GET_EVENTS_SUCCESS, 
  ADD_NEW_EVENT, ADD_EVENT_SUCCESS, ADD_EVENT_FAIL, 
  UPDATE_EVENT, UPDATE_EVENT_SUCCESS, UPDATE_EVENT_FAIL, 
  DELETE_EVENT, DELETE_EVENT_SUCCESS, DELETE_EVENT_FAIL, 
  GET_CATEGORIES, GET_CATEGORIES_SUCCESS, GET_CATEGORIES_FAIL 
} from "./actionTypes";
```

## 4. Conclusion 🎯

The `actions.js` file is a crucial component of the Redux architecture as it defines all the necessary actions related to events and categories. These actions are the first step in the flow of data through a Redux application, ensuring that state changes are dispatched and handled correctly. By understanding the role of each action creator, developers can effectively manage state and enhance the application's ability to respond to different operations.

This documentation aims to provide clarity on the purpose and implementation of each action within the `actions.js` file. For further exploration, consider diving into the corresponding reducers and sagas that handle these actions to understand the complete state management flow.

# Documentation for `actionTypes.js` 📜

## Introduction 📚

The `actionTypes.js` file is an essential component of a Redux-based application. It defines a set of constants representing the types of actions that can be dispatched in the application. By centralizing these action types, we reduce the risk of typos and inconsistencies across the codebase, promoting a more manageable, maintainable, and scalable application.

## Table of Contents 📑

1. [Overview](#overview)
2. [Action Types](#action-types)
    - [Event Actions](#event-actions)
    - [Category Actions](#category-actions)
3. [Conclusion](#conclusion)

## Overview 🔍

The file consists of string constants that are used to specify the type of actions dispatched in the Redux flow. These constants help in maintaining a uniform and consistent naming convention across different parts of the application, such as actions and reducers.

## Action Types 🏷️

### Event Actions 🎉

These action types are related to event operations such as fetching, adding, updating, and deleting events:

| Constant Name             | Description                                  |
|---------------------------|----------------------------------------------|
| **GET_EVENTS**            | Action type for initiating event fetch.      |
| **GET_EVENTS_SUCCESS**    | Action type for successful event fetch.      |
| **GET_EVENTS_FAIL**       | Action type for failed event fetch.          |
| **ADD_NEW_EVENT**         | Action type for initiating adding a new event.|
| **ADD_EVENT_SUCCESS**     | Action type for successful event addition.   |
| **ADD_EVENT_FAIL**        | Action type for failed event addition.       |
| **UPDATE_EVENT**          | Action type for initiating event update.     |
| **UPDATE_EVENT_SUCCESS**  | Action type for successful event update.     |
| **UPDATE_EVENT_FAIL**     | Action type for failed event update.         |
| **DELETE_EVENT**          | Action type for initiating event deletion.   |
| **DELETE_EVENT_SUCCESS**  | Action type for successful event deletion.   |
| **DELETE_EVENT_FAIL**     | Action type for failed event deletion.       |

### Category Actions 📂

These action types are associated with category operations:

| Constant Name                | Description                                    |
|------------------------------|------------------------------------------------|
| **GET_CATEGORIES**           | Action type for initiating category fetch.     |
| **GET_CATEGORIES_SUCCESS**   | Action type for successful category fetch.     |
| **GET_CATEGORIES_FAIL**      | Action type for failed category fetch.         |

## Conclusion 📝

By using the constants defined in `actionTypes.js`, developers can ensure that the action types used across the Redux actions and reducers are consistent and error-free. This file is crucial for maintaining clarity and reducing potential bugs due to typographical errors in action type strings.

This setup is integral to a well-structured Redux application, making it easy to trace actions throughout the lifecycle of the state management process. 🎯

# 📜 Saga.js Documentation

Welcome to the **Saga.js** documentation, where we'll explore the functionality and purpose of the code in this file. This file plays a crucial role in handling side effects in the application using Redux Saga middleware.

## 🗂️ Index

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Functions](#functions)
    - [fetchEvents](#fetchevents)
    - [onAddNewEvent](#onaddnewevent)
    - [onUpdateEvent](#onupdateevent)
    - [onDeleteEvent](#ondeleteevent)
    - [onGetCategories](#ongetcategories)
4. [Main Saga](#main-saga)
    - [calendarSaga](#calendarsaga)
5. [Summary](#summary)

## 🎯 Introduction

The **Saga.js** file is part of the Redux Saga setup, responsible for handling asynchronous operations (side effects) such as API calls related to calendar events and categories. It listens for dispatched actions and runs corresponding generator functions to manage these side effects efficiently.

## 📦 Imports

Here's a breakdown of the imports used in this file:

```javascript
import { takeEvery, put, call } from "redux-saga/effects";
```

- **takeEvery**: A helper function that listens for dispatched actions and triggers the corresponding saga function.
- **put**: Used to dispatch actions back to the Redux store.
- **call**: Invokes functions and deals with asynchronous operations.

```javascript
import { ADD_NEW_EVENT, DELETE_EVENT, GET_CATEGORIES, GET_EVENTS, UPDATE_EVENT } from "./actionTypes";
```

- Action type constants for identifying different actions related to events and categories.

```javascript
import { getEventsSuccess, getEventsFail, addEventFail, addEventSuccess, updateEventSuccess, updateEventFail, deleteEventSuccess, deleteEventFail, getCategoriesSuccess, getCategoriesFail } from "./actions";
```

- Action creators for dispatching success or failure actions.

```javascript
import { getEvents, addNewEvent, updateEvent, deleteEvent, getCategories } from "../../helpers/fakebackend_helper";
```

- Fake backend helper functions simulating API calls.

## 🔧 Functions

### fetchEvents

This generator function handles fetching events.

```javascript
function* fetchEvents() {
    try {
        const response = yield call(getEvents);
        yield put(getEventsSuccess(response));
    } catch (error) {
        yield put(getEventsFail(error));
    }
}
```

- **call(getEvents)**: Invokes the `getEvents` function, simulating an API call.
- **put(getEventsSuccess(response))**: Dispatches a success action with the response data.
- **put(getEventsFail(error))**: Dispatches a failure action with the error.

### onAddNewEvent

This generator function handles adding a new event.

```javascript
function* onAddNewEvent({ payload: event }) {
    try {
        const response = yield call(addNewEvent, event);
        yield put(addEventSuccess(response));
    } catch (error) {
        yield put(addEventFail(error));
    }
}
```

- **call(addNewEvent, event)**: Calls the `addNewEvent` function with the event data.
- **put(addEventSuccess(response))**: Dispatches a success action with the response.
- **put(addEventFail(error))**: Dispatches a failure action with the error.

### onUpdateEvent

This generator function handles updating an event.

```javascript
function* onUpdateEvent({ payload: event }) {
    try {
        const response = yield call(updateEvent, event);
        yield put(updateEventSuccess(response));
    } catch (error) {
        yield put(updateEventFail(error));
    }
}
```

- **call(updateEvent, event)**: Calls the `updateEvent` function with the event data.
- **put(updateEventSuccess(response))**: Dispatches a success action with the response.
- **put(updateEventFail(error))**: Dispatches a failure action with the error.

### onDeleteEvent

This generator function handles deleting an event.

```javascript
function* onDeleteEvent({ payload: event }) {
    try {
        const response = yield call(deleteEvent, event);
        yield put(deleteEventSuccess(response));
    } catch (error) {
        yield put(deleteEventFail(error));
    }
}
```

- **call(deleteEvent, event)**: Calls the `deleteEvent` function with the event data.
- **put(deleteEventSuccess(response))**: Dispatches a success action with the response.
- **put(deleteEventFail(error))**: Dispatches a failure action with the error.

### onGetCategories

This generator function handles fetching categories.

```javascript
function* onGetCategories() {
    try {
        const response = yield call(getCategories);
        yield put(getCategoriesSuccess(response));
    } catch (error) {
        yield put(getCategoriesFail(error));
    }
}
```

- **call(getCategories)**: Invokes the `getCategories` function, simulating an API call.
- **put(getCategoriesSuccess(response))**: Dispatches a success action with the response data.
- **put(getCategoriesFail(error))**: Dispatches a failure action with the error.

## 🚀 Main Saga

### calendarSaga

The main saga function that combines all the individual saga functions and listens for specific actions.

```javascript
function* calendarSaga() {
    yield takeEvery(GET_EVENTS, fetchEvents);
    yield takeEvery(ADD_NEW_EVENT, onAddNewEvent);
    yield takeEvery(UPDATE_EVENT, onUpdateEvent);
    yield takeEvery(DELETE_EVENT, onDeleteEvent);
    yield takeEvery(GET_CATEGORIES, onGetCategories);
}
```

- **takeEvery**: Listens for specific actions and triggers corresponding saga functions.

## 📝 Summary

The **Saga.js** file is a powerhouse for managing side effects in the application. It listens for dispatched actions related to events and categories, performs the necessary asynchronous operations using Redux Saga, and communicates the results back to the Redux store through success or failure actions.

By handling side effects with Redux Saga, this file ensures that the application remains responsive and efficient, even when dealing with complex asynchronous workflows. 🎉

Feel free to explore more about Redux Saga's capabilities to enhance your application's performance and reliability!

# Documentation for `reducer.js` 📜

## Introduction
The `reducer.js` file is an integral part of the Redux architecture used in managing the state of events and categories in a calendar application. It defines how the state changes in response to actions dispatched in the application. The reducer is a pure function that takes the current state and an action as arguments and returns a new state. Let's delve into the specifics of what this file does. 

## Index
1. [Initial State](#initial-state)
2. [Reducer Function](#reducer-function)
3. [Action Type Handling](#action-type-handling)
4. [State Updates](#state-updates)
5. [Default Case](#default-case)

## Initial State

```javascript
const INIT_STATE = {
  events: [],
  categories: [],
  error: {},
}
```

The initial state, `INIT_STATE`, is an object with three properties:
- `events`: An array to hold event objects.
- `categories`: An array to hold category objects.
- `error`: An object to capture any errors that occur during state operations.

## Reducer Function

The core of this file is the `Calendar` reducer function:

```javascript
const Calendar = (state = INIT_STATE, action) => { /* ... */ }
```

### Purpose
The `Calendar` reducer manages changes to the `events` and `categories` state based on specific action types. It ensures that the state is updated immutably, meaning a new state object is returned rather than modifying the current state directly.

## Action Type Handling

The reducer responds to a variety of action types imported from `actionTypes.js`. Each case in the switch statement corresponds to a specific action type.

### Action Types and Their Purpose

| **Action Type**            | **Description**                                                 |
|----------------------------|-----------------------------------------------------------------|
| `GET_EVENTS_SUCCESS`       | Successfully fetched events, updating the `events` array.       |
| `GET_EVENTS_FAIL`          | Failed to fetch events, updating the `error` object.            |
| `ADD_EVENT_SUCCESS`        | Successfully added an event to the `events` array.              |
| `ADD_EVENT_FAIL`           | Failed to add an event, updating the `error` object.            |
| `UPDATE_EVENT_SUCCESS`     | Successfully updated an event in the `events` array.            |
| `UPDATE_EVENT_FAIL`        | Failed to update an event, updating the `error` object.         |
| `DELETE_EVENT_SUCCESS`     | Successfully deleted an event from the `events` array.          |
| `DELETE_EVENT_FAIL`        | Failed to delete an event, updating the `error` object.         |
| `GET_CATEGORIES_SUCCESS`   | Successfully fetched categories, updating the `categories` array.|
| `GET_CATEGORIES_FAIL`      | Failed to fetch categories, updating the `error` object.        |

## State Updates

The reducer updates the state based on the action type:

- **GET_EVENTS_SUCCESS**
  ```javascript
  return { ...state, events: action.payload }
  ```
  - Updates the `events` state with the payload from the action.

- **GET_EVENTS_FAIL**
  ```javascript
  return { ...state, error: action.payload }
  ```
  - Updates the `error` state with the error payload.

- **ADD_EVENT_SUCCESS**
  ```javascript
  return { ...state, events: [...state.events, action.payload] }
  ```
  - Appends the new event to the `events` array.

- **ADD_EVENT_FAIL**
  ```javascript
  return { ...state, error: action.payload }
  ```
  - Updates the `error` state with the error payload.

- **UPDATE_EVENT_SUCCESS**
  ```javascript
  return {
    ...state,
    events: state.events.map(event =>
      event.id.toString() === action.payload.id.toString()
        ? { event, ...action.payload }
        : event
    ),
  }
  ```
  - Maps through the `events` array to update the specific event that matches the ID from the action payload.

- **UPDATE_EVENT_FAIL**
  ```javascript
  return { ...state, error: action.payload }
  ```
  - Updates the `error` state with the error payload.

- **DELETE_EVENT_SUCCESS**
  ```javascript
  return {
    ...state,
    events: state.events.filter(
      event => event.id.toString() !== action.payload.id.toString()
    ),
  }
  ```
  - Filters the `events` array to remove the event with the ID specified in the action payload.

- **DELETE_EVENT_FAIL**
  ```javascript
  return { ...state, error: action.payload }
  ```
  - Updates the `error` state with the error payload.

- **GET_CATEGORIES_SUCCESS**
  ```javascript
  return { ...state, categories: action.payload }
  ```
  - Updates the `categories` state with the payload from the action.

- **GET_CATEGORIES_FAIL**
  ```javascript
  return { ...state, error: action.payload }
  ```
  - Updates the `error` state with the error payload.

## Default Case

```javascript
default: return state
```

- If the action type does not match any case, the reducer returns the current state unchanged.

## Conclusion

The `reducer.js` file is a well-structured component of the Redux setup, ensuring that the application's state transitions are handled predictably and immutably. By managing the state of events and categories, it plays a crucial role in the functionality of the calendar application. 🗓️

With this detailed look at `reducer.js`, you can better understand its role in the Redux flow and how it contributes to maintaining a consistent application state.