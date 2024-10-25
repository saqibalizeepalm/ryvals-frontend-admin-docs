# 📄 **Actions Documentation**

This documentation provides an in-depth look into the `actions.js` file of our project. The actions defined here are integral to our application's state management, particularly in handling invoices. Let's dive into the details!

## 📚 **Index**

- [Introduction](#introduction)
- [Action Types](#action-types)
- [Defined Actions](#defined-actions)
  - [getInvoices](#getinvoices)
  - [getInvoicesSuccess](#getinvoicessuccess)
  - [getInvoicesFail](#getinvoicesfail)
  - [getInvoiceDetail](#getinvoicedetail)
  - [getInvoiceDetailSuccess](#getinvoicedetailsuccess)
  - [getInvoiceDetailFail](#getinvoicedetailfail)

## 📘 **Introduction**

In Redux architecture, **actions** are payloads of information that send data from your application to your Redux store. They are the sole source of information for the store and are processed by reducers to update the state. Our `actions.js` file is responsible for defining actions related to invoice operations.

## 📌 **Action Types**

The action types are constants imported from the `actionTypes.js` file to avoid typos and provide a single source of truth for action type strings. The action types used in this file are:

- `GET_INVOICES`
- `GET_INVOICES_SUCCESS`
- `GET_INVOICES_FAIL`
- `GET_INVOICE_DETAIL`
- `GET_INVOICE_DETAIL_SUCCESS`
- `GET_INVOICE_DETAIL_FAIL`

These constants are employed in action creators to define the type of action being performed.

## 🚀 **Defined Actions**

Here we will explain each action defined in the file, detailing their purpose and structure.

### 🔄 `getInvoices`

```javascript
export const getInvoices = () => ({
  type: GET_INVOICES,
})
```

- **Purpose**: Initiates the process of fetching all invoices.
- **Usage**: This action is dispatched when the application starts a request to retrieve invoice data from the server.

### ✅ `getInvoicesSuccess`

```javascript
export const getInvoicesSuccess = invoices => ({
  type: GET_INVOICES_SUCCESS,
  payload: invoices,
})
```

- **Purpose**: Handles the successful retrieval of invoices.
- **Parameters**:
  - **invoices**: The array of invoice objects retrieved from the server.
- **Usage**: Dispatched when invoices are successfully fetched, carrying the data as its payload.

### ❌ `getInvoicesFail`

```javascript
export const getInvoicesFail = error => ({
  type: GET_INVOICES_FAIL,
  payload: error,
})
```

- **Purpose**: Handles errors that occur during the fetching of invoices.
- **Parameters**:
  - **error**: The error object or message received from the failed request.
- **Usage**: Dispatched when there is a failure in fetching invoice data.

### 🔄 `getInvoiceDetail`

```javascript
export const getInvoiceDetail = invoiceId => ({
  type: GET_INVOICE_DETAIL,
  invoiceId,
})
```

- **Purpose**: Initiates the process of fetching detailed information for a specific invoice.
- **Parameters**:
  - **invoiceId**: The unique identifier of the invoice whose details are being requested.
- **Usage**: Dispatched when the application requests detailed information about a specific invoice.

### ✅ `getInvoiceDetailSuccess`

```javascript
export const getInvoiceDetailSuccess = invoices => ({
  type: GET_INVOICE_DETAIL_SUCCESS,
  payload: invoices,
})
```

- **Purpose**: Handles the successful retrieval of detailed invoice information.
- **Parameters**:
  - **invoices**: The detailed invoice data retrieved from the server.
- **Usage**: Dispatched when detailed information for a specific invoice is successfully fetched.

### ❌ `getInvoiceDetailFail`

```javascript
export const getInvoiceDetailFail = error => ({
  type: GET_INVOICE_DETAIL_FAIL,
  payload: error,
})
```

- **Purpose**: Handles errors that occur during the fetching of detailed invoice information.
- **Parameters**:
  - **error**: The error object or message received from the failed request.
- **Usage**: Dispatched when there is a failure in fetching detailed invoice information.

## 🎨 **Conclusion**

The `actions.js` file plays a crucial role in managing the state related to invoices within the application. By defining clear and concise action creators, the file aids in dispatching actions that trigger state changes in response to asynchronous operations such as API calls. Understanding these actions is key to maintaining and extending the application's invoice management functionality.

# Documentation for `actionTypes.js` 📜

Welcome to the detailed documentation for the `actionTypes.js` file. This file is crucial as it defines the types of actions that can be dispatched in a Redux application, specifically in the context of handling invoices. These action types help in maintaining consistency and avoiding typos across the application.

## Table of Contents 📖
1. [Introduction](#introduction)
2. [Action Types](#action-types)
3. [Usage](#usage)
4. [Conclusion](#conclusion)

## Introduction 🚀

In Redux, **action types** are string constants that represent the type of action being performed. These constants are used in action creators and reducers to handle specific actions. Defining action types in a separate file helps in maintaining the codebase by providing a single source of truth for all action types.

## Action Types 🎨

Below is a list of all the action types defined in the `actionTypes.js` file:

| Action Type Constant           | Description                                                                 |
|--------------------------------|-----------------------------------------------------------------------------|
| `GET_INVOICES`                 | Triggered to initiate the process of fetching all invoices.                  |
| `GET_INVOICES_SUCCESS`         | Dispatched when invoices are successfully fetched.                           |
| `GET_INVOICES_FAIL`            | Dispatched when there is an error in fetching invoices.                      |
| `GET_INVOICE_DETAIL`           | Triggered to initiate the process of fetching the details of a specific invoice. |
| `GET_INVOICE_DETAIL_SUCCESS`   | Dispatched when the invoice details are successfully retrieved.              |
| `GET_INVOICE_DETAIL_FAIL`      | Dispatched when there is an error in fetching the invoice details.           |

### Detailed Explanation 📝

- **GET_INVOICES**: This action type is dispatched to start the process of retrieving all invoices. It usually triggers a saga or a thunk to perform an asynchronous operation such as an API call.

- **GET_INVOICES_SUCCESS**: This action type is used when the operation to fetch invoices is completed successfully, and the fetched data is sent to the reducer to update the state.

- **GET_INVOICES_FAIL**: If there is an error during the fetch operation, this action type is dispatched to signal the failure and often carries an error message.

- **GET_INVOICE_DETAIL**: Similar to `GET_INVOICES`, but specific to fetching the details of one invoice.

- **GET_INVOICE_DETAIL_SUCCESS**: Indicates successful retrieval of a specific invoice's details.

- **GET_INVOICE_DETAIL_FAIL**: Dispatched when there is an error in retrieving the invoice details.

## Usage 💡

These action types are typically used in two main parts of a Redux application:

1. **Action Creators**: Functions that create actions, these functions often return an object containing an action type and a payload.

   ```javascript
   // Example usage in action creators
   export const getInvoices = () => ({
     type: GET_INVOICES,
   });
   ```

2. **Reducers**: Functions that update the state based on the action type received.

   ```javascript
   // Example usage in a reducer
   const invoiceReducer = (state = initialState, action) => {
     switch(action.type) {
       case GET_INVOICES_SUCCESS:
         return {
           ...state,
           invoices: action.payload,
         };
       // other cases...
     }
   }
   ```

## Conclusion 🎯

The `actionTypes.js` file might seem simple, but it plays a pivotal role in maintaining a scalable and maintainable Redux application. By consolidating all action types in one place, developers can easily manage and track the actions being used throughout the application, leading to cleaner and more reliable code.

Feel free to explore other parts of the codebase to see how these action types integrate with actions, reducers, and possibly middleware like Redux Saga or Thunk!

# **Reducer.js Documentation 📄**

Welcome to the comprehensive documentation for the `reducer.js` file! This file plays a crucial role in the state management of our application using Redux. It is responsible for handling how the application's state changes in response to actions dispatched from the action creators.

## **Index 📚**
1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Initial State](#initial-state)
4. [Invoices Reducer](#invoices-reducer)
5. [Switch Cases](#switch-cases)
6. [Export](#export)

---

## **Introduction 🌟**
In Redux, a reducer is a pure function that takes the current state and an action as arguments, and returns a new state. The `reducer.js` file contains a reducer function that manages the state related to invoices in our application.

## **Imports 📥**
The file begins by importing the necessary action types:

```javascript
import { GET_INVOICES_FAIL, GET_INVOICES_SUCCESS, GET_INVOICE_DETAIL_SUCCESS, GET_INVOICE_DETAIL_FAIL, } from "./actionTypes";
```

These action types are constants that represent the types of actions that can be dispatched. They are used within the reducer to determine how the state should be updated.

## **Initial State 🏁**
The reducer initializes a default state, `INIT_STATE`, which serves as the starting point for the state managed by this reducer:

```javascript
const INIT_STATE = {
  invoices: [],
  invoiceDetail: {},
  error: {},
};
```

- `invoices`: An array that will hold the list of invoices.
- `invoiceDetail`: An object that will store the details of a specific invoice.
- `error`: An object that will contain error information if an error occurs.

## **Invoices Reducer 🔄**
The main function in this file is the `Invoices` reducer function:

```javascript
const Invoices = (state = INIT_STATE, action) => {
  switch (action.type) {
    // Cases to handle different action types
    default:
      return state;
  }
};
```

- **Parameters**:
  - `state`: Represents the current state. It defaults to `INIT_STATE`.
  - `action`: An object containing a `type` and optionally a `payload`.

## **Switch Cases 🔀**
The reducer uses a `switch` statement to determine how to update the state based on the action type:

1. **GET_INVOICES_SUCCESS**:
   - **Updates**: `invoices` with the payload from the action.
   - **Code**:
     ```javascript
     case GET_INVOICES_SUCCESS:
       return {
         ...state,
         invoices: action.payload,
       };
     ```

2. **GET_INVOICES_FAIL**:
   - **Updates**: `error` with the payload from the action.
   - **Code**:
     ```javascript
     case GET_INVOICES_FAIL:
       return {
         ...state,
         error: action.payload,
       };
     ```

3. **GET_INVOICE_DETAIL_SUCCESS**:
   - **Updates**: `invoiceDetail` with the payload from the action.
   - **Code**:
     ```javascript
     case GET_INVOICE_DETAIL_SUCCESS:
       return {
         ...state,
         invoiceDetail: action.payload,
       };
     ```

4. **GET_INVOICE_DETAIL_FAIL**:
   - **Updates**: `error` with the payload from the action.
   - **Code**:
     ```javascript
     case GET_INVOICE_DETAIL_FAIL:
       return {
         ...state,
         error: action.payload,
       };
     ```

5. **Default**:
   - **Returns**: The current state if no action types match.
   - **Code**:
     ```javascript
     default:
       return state;
     ```

## **Export 🚀**
Finally, the reducer is exported as the default export of the module:

```javascript
export default Invoices;
```

This export allows the reducer to be used in the Redux store setup, enabling the management of the application's state related to invoices.

---

**In summary**, the `reducer.js` file defines how the state of invoices is updated in response to various actions, ensuring a predictable state management pattern using Redux.

# Documentation for `saga.js` 📜

Welcome to the documentation for `saga.js`! This file is a part of a Redux-Saga implementation, designed to handle side effects in a Redux application. It orchestrates the asynchronous calls to fetch invoice data and manages the action dispatching based on the outcome of these calls. Let's dive into the details! 🚀

## Table of Contents 📑

1. [Introduction](#introduction)
2. [Key Imports](#key-imports)
3. [Generator Functions](#generator-functions)
   - [fetchInvoices](#fetchinvoices)
   - [fetchInvoiceDetail](#fetchinvoicedetail)
4. [Root Saga Function](#root-saga-function)
   - [invoiceSaga](#invoicesaga)
5. [Conclusion](#conclusion)

## Introduction 🌟

In Redux applications, managing side effects like data fetching can become complicated. Redux-Saga is a library that makes handling such side effects easier by using generator functions. In `saga.js`, we define the flows for asynchronous actions related to invoices.

## Key Imports 📥

Let's take a look at the essential imports in this file:

```javascript
import { call, put, takeEvery } from "redux-saga/effects"
import { GET_INVOICES, GET_INVOICE_DETAIL } from "./actionTypes"
import { getInvoicesSuccess, getInvoicesFail, getInvoiceDetailSuccess, getInvoiceDetailFail } from "./actions"
import { getInvoices, getInvoiceDetail } from "../../helpers/fakebackend_helper"
```

- **`redux-saga/effects`**: Provides functions like `call`, `put`, and `takeEvery` to manage side effects.
- **Action Types**: `GET_INVOICES` and `GET_INVOICE_DETAIL` are the actions that trigger the saga.
- **Actions**: Import functions to dispatch actions for success and failure scenarios.
- **Helpers**: Functions `getInvoices` and `getInvoiceDetail` are called to fetch data.

## Generator Functions ⚙️

### `fetchInvoices`

This generator function handles the fetching of invoices.

```javascript
function* fetchInvoices() {
  try {
    const response = yield call(getInvoices)
    yield put(getInvoicesSuccess(response))
  } catch (error) {
    yield put(getInvoicesFail(error))
  }
}
```

- **`call`**: Invokes the `getInvoices` function asynchronously.
- **`put`**: Dispatches `getInvoicesSuccess` or `getInvoicesFail` based on the result.

### `fetchInvoiceDetail`

This function fetches details for a specific invoice using its ID.

```javascript
function* fetchInvoiceDetail({ invoiceId }) {
  try {
    const response = yield call(getInvoiceDetail, invoiceId)
    yield put(getInvoiceDetailSuccess(response))
  } catch (error) {
    yield put(getInvoiceDetailFail(error))
  }
}
```

- Fetches details by calling `getInvoiceDetail` with `invoiceId`.
- Dispatches success or failure actions accordingly.

## Root Saga Function 🌐

### `invoiceSaga`

The root saga function listens for dispatched actions and triggers the corresponding generator functions.

```javascript
function* invoiceSaga() {
  yield takeEvery(GET_INVOICES, fetchInvoices)
  yield takeEvery(GET_INVOICE_DETAIL, fetchInvoiceDetail)
}
```

- **`takeEvery`**: Listens for every dispatched action type and triggers the specified generator function.

## Conclusion 📝

The `saga.js` file is a critical part of managing asynchronous operations in a Redux application. By leveraging Redux-Saga, we can keep our side effects organized and our state management logic clean. This file ensures that fetching invoices and their details is handled efficiently, with proper success and error management. 🎉

Feel free to explore other parts of the codebase to see how these sagas integrate with the rest of the application!