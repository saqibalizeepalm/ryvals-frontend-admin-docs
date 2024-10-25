# 📄 Documentation for `actions.js`

Welcome to the documentation for the `actions.js` file! This file is a crucial component of a Redux-based application architecture, responsible for defining action creators that help manage state changes in your app. These actions are dispatched to the Redux store, triggering reducers or sagas to update the state or perform side effects like API calls.

## 📚 Index

1. [Introduction](#introduction)
2. [Action Types](#action-types)
3. [Action Creators](#action-creators)
    - [Product Actions](#product-actions)
    - [Order Actions](#order-actions)
    - [Cart Data Actions](#cart-data-actions)
    - [Customer Actions](#customer-actions)
    - [Shop Actions](#shop-actions)
4. [Summary](#summary)

## 🌟 Introduction <a name="introduction"></a>

In a Redux application, **actions** are payloads of information that send data from your application to your Redux store. They are the only source of information for the store. You send them to the store using `store.dispatch()`.

The `actions.js` file defines several action creators related to products, orders, cart data, customers, and shops, which are essential for managing the application's state effectively.

## 📋 Action Types <a name="action-types"></a>

The file imports several action types from `actionTypes.js`, which are used to differentiate between the various actions. These constants help avoid typos and provide a single source of truth for action naming.

### Example of Action Types

```javascript
import { 
  GET_CART_DATA, 
  GET_CART_DATA_FAIL, 
  GET_CART_DATA_SUCCESS, 
  GET_ORDERS, 
  GET_ORDERS_FAIL, 
  GET_ORDERS_SUCCESS, 
  GET_PRODUCTS, 
  GET_PRODUCTS_FAIL, 
  GET_PRODUCTS_SUCCESS, 
  GET_CUSTOMERS, 
  GET_CUSTOMERS_FAIL, 
  GET_CUSTOMERS_SUCCESS, 
  GET_SHOPS, 
  GET_SHOPS_FAIL, 
  GET_SHOPS_SUCCESS, 
  GET_PRODUCT_DETAIL, 
  GET_PRODUCT_DETAIL_FAIL, 
  GET_PRODUCT_DETAIL_SUCCESS 
} from "./actionTypes"
```

## 🚀 Action Creators <a name="action-creators"></a>

Action creators are functions that create and return an action object. These functions make it easier to manage actions in a scalable way.

### 🛍️ Product Actions <a name="product-actions"></a>

- **getProducts**: Triggers the process to fetch product data.
  ```javascript
  export const getProducts = () => ({
    type: GET_PRODUCTS,
  })
  ```

- **getProductsSuccess**: Called when product data is fetched successfully.
  ```javascript
  export const getProductsSuccess = products => ({
    type: GET_PRODUCTS_SUCCESS,
    payload: products,
  })
  ```

- **getProductsFail**: Called when there is an error fetching product data.
  ```javascript
  export const getProductsFail = error => ({
    type: GET_PRODUCTS_FAIL,
    payload: error,
  })
  ```

- **getProductDetail**: Initiates the fetching of detailed information about a specific product.
  ```javascript
  export const getProductDetail = productId => ({
    type: GET_PRODUCT_DETAIL,
    productId,
  })
  ```

- **getProductDetailSuccess**: Called when product detail data is retrieved successfully.
  ```javascript
  export const getProductDetailSuccess = products => ({
    type: GET_PRODUCT_DETAIL_SUCCESS,
    payload: products,
  })
  ```

- **getProductDetailFail**: Called when there is an error fetching product detail data.
  ```javascript
  export const getProductDetailFail = error => ({
    type: GET_PRODUCT_DETAIL_FAIL,
    payload: error,
  })
  ```

### 📦 Order Actions <a name="order-actions"></a>

- **getOrders**: Initiates the fetching of orders data.
  ```javascript
  export const getOrders = () => ({
    type: GET_ORDERS,
  })
  ```

- **getOrdersSuccess**: Called when orders data is fetched successfully.
  ```javascript
  export const getOrdersSuccess = orders => ({
    type: GET_ORDERS_SUCCESS,
    payload: orders,
  })
  ```

- **getOrdersFail**: Called when there is an error fetching orders data.
  ```javascript
  export const getOrdersFail = error => ({
    type: GET_ORDERS_FAIL,
    payload: error,
  })
  ```

### 🛒 Cart Data Actions <a name="cart-data-actions"></a>

- **getCartData**: Initiates the fetching of cart data.
  ```javascript
  export const getCartData = () => ({
    type: GET_CART_DATA,
  })
  ```

- **getCartDataSuccess**: Called when cart data is fetched successfully.
  ```javascript
  export const getCartDataSuccess = cartData => ({
    type: GET_CART_DATA_SUCCESS,
    payload: cartData,
  })
  ```

- **getCartDataFail**: Called when there is an error fetching cart data.
  ```javascript
  export const getCartDataFail = error => ({
    type: GET_CART_DATA_FAIL,
    payload: error,
  })
  ```

### 👥 Customer Actions <a name="customer-actions"></a>

- **getCustomers**: Initiates the fetching of customer data.
  ```javascript
  export const getCustomers = () => ({
    type: GET_CUSTOMERS,
  })
  ```

- **getCustomersSuccess**: Called when customer data is fetched successfully.
  ```javascript
  export const getCustomersSuccess = customers => ({
    type: GET_CUSTOMERS_SUCCESS,
    payload: customers,
  })
  ```

- **getCustomersFail**: Called when there is an error fetching customer data.
  ```javascript
  export const getCustomersFail = error => ({
    type: GET_CUSTOMERS_FAIL,
    payload: error,
  })
  ```

### 🏬 Shop Actions <a name="shop-actions"></a>

- **getShops**: Initiates the fetching of shop data.
  ```javascript
  export const getShops = () => ({
    type: GET_SHOPS,
  })
  ```

- **getShopsSuccess**: Called when shop data is fetched successfully.
  ```javascript
  export const getShopsSuccess = shops => ({
    type: GET_SHOPS_SUCCESS,
    payload: shops,
  })
  ```

- **getShopsFail**: Called when there is an error fetching shop data.
  ```javascript
  export const getShopsFail = error => ({
    type: GET_SHOPS_FAIL,
    payload: error,
  })
  ```

## 🎯 Summary <a name="summary"></a>

The `actions.js` file plays a pivotal role in managing the flow of data in a Redux application. By defining comprehensive action creators for products, orders, cart data, customers, and shops, it ensures that the state management is organized, scalable, and maintainable.

These action creators are integral in dispatching actions that either initiate data fetching or handle the success and failure of these asynchronous operations, thus maintaining the integrity and consistency of application state.

# Documentation for `actionTypes.js` 📜

## Introduction

The `actionTypes.js` file plays a crucial role in managing action types for Redux actions in your application. It exports constants that represent different action types used across various parts of the application. This practice helps in reducing errors caused by typos in action type strings and facilitates easier management of action types in large applications.

## Action Types Overview

The file is organized into sections, each dedicated to a specific feature or domain of the application. Below is a detailed breakdown of each section and the corresponding action types.

### Products 🛍️

These action types are used for managing product-related operations, such as fetching a list of products or handling errors that occur while fetching them.

| Action Type                  | Description                                      |
|------------------------------|--------------------------------------------------|
| `GET_PRODUCTS`               | Initiates the process of fetching products.      |
| `GET_PRODUCTS_SUCCESS`       | Indicates successful retrieval of products.      |
| `GET_PRODUCTS_FAIL`          | Indicates failure in retrieving products.        |

### Product Details 🔍

These action types are specifically for operations related to detailed information about a specific product.

| Action Type                      | Description                                            |
|----------------------------------|--------------------------------------------------------|
| `GET_PRODUCT_DETAIL`             | Initiates fetching detailed information for a product. |
| `GET_PRODUCT_DETAIL_SUCCESS`     | Indicates success in retrieving product details.       |
| `GET_PRODUCT_DETAIL_FAIL`        | Indicates failure in retrieving product details.       |

### Orders 📦

Handles action types related to order management, including fetching order data and handling associated errors.

| Action Type        | Description                                       |
|--------------------|---------------------------------------------------|
| `GET_ORDERS`       | Initiates the process of fetching orders.         |
| `GET_ORDERS_SUCCESS` | Indicates successful retrieval of orders.       |
| `GET_ORDERS_FAIL`  | Indicates failure in retrieving orders.           |

### Cart Data 🛒

These action types are used for operations related to the shopping cart, such as fetching cart data or handling errors.

| Action Type            | Description                                    |
|------------------------|------------------------------------------------|
| `GET_CART_DATA`        | Initiates the process of fetching cart data.   |
| `GET_CART_DATA_SUCCESS`| Indicates successful retrieval of cart data.   |
| `GET_CART_DATA_FAIL`   | Indicates failure in retrieving cart data.     |

### Customers 👥

Handles action types for managing customer-related data and operations.

| Action Type            | Description                                       |
|------------------------|---------------------------------------------------|
| `GET_CUSTOMERS`        | Initiates the process of fetching customers.      |
| `GET_CUSTOMERS_SUCCESS`| Indicates successful retrieval of customer data.  |
| `GET_CUSTOMERS_FAIL`   | Indicates failure in retrieving customer data.    |

### Shops 🏬

These action types are used for operations related to shop data management.

| Action Type         | Description                                    |
|---------------------|------------------------------------------------|
| `GET_SHOPS`         | Initiates the process of fetching shops.       |
| `GET_SHOPS_SUCCESS` | Indicates successful retrieval of shop data.   |
| `GET_SHOPS_FAIL`    | Indicates failure in retrieving shop data.     |

## Conclusion

The `actionTypes.js` file provides a centralized and organized way to manage action types in your application. By defining all action types as constants, it reduces the potential for errors and improves the maintainability of your codebase. This file acts as a backbone for handling different operations related to products, product details, orders, cart data, customers, and shops in the Redux store.

# 📚 Documentation for `saga.js`

## Table of Contents
1. [Introduction](#introduction)
2. [Import Statements](#import-statements)
3. [Saga Functions](#saga-functions)
   - [fetchProducts](#fetchproducts)
   - [fetchProductDetail](#fetchproductdetail)
   - [fetchOrders](#fetchorders)
   - [fetchCartData](#fetchcartdata)
   - [fetchCustomers](#fetchcustomers)
   - [fetchShops](#fetchshops)
4. [Root Saga](#root-saga)
5. [Conclusion](#conclusion)

## Introduction
The `saga.js` file is responsible for handling side effects in a Redux application using Redux-Saga. It orchestrates asynchronous operations such as data fetching from an API, and dispatches actions depending on whether the operation was successful or failed. This file is crucial for managing complex asynchronous logic in a clear and maintainable way.

## Import Statements
The file begins by importing necessary functions and actions:

```javascript
import { call, put, takeEvery } from "redux-saga/effects"
import {
  GET_CART_DATA, GET_CUSTOMERS, GET_ORDERS, GET_PRODUCT_DETAIL, GET_PRODUCTS, GET_SHOPS,
} from "./actionTypes"
import {
  getCartDataFail, getCartDataSuccess, getCustomersFail, getCustomersSuccess,
  getOrdersFail, getOrdersSuccess, getProductDetailFail, getProductDetailSuccess,
  getProductsFail, getProductsSuccess, getShopsFail, getShopsSuccess,
} from "./actions"
import {
  getCartData, getCustomers, getOrders, getProducts, getShops, getProductDetail,
} from "../../helpers/fakebackend_helper"
```

- **`redux-saga/effects`**: Provides core Saga functionality.
- **Action Types**: Import constants to identify which actions should trigger the Sagas.
- **Action Creators**: Import functions to dispatch success or failure actions.
- **Helpers**: Import functions simulating API calls.

## Saga Functions

### fetchProducts
Handles fetching product data:

```javascript
function* fetchProducts() {
  try {
    const response = yield call(getProducts)
    yield put(getProductsSuccess(response))
  } catch (error) {
    yield put(getProductsFail(error))
  }
}
```

- **`call(getProducts)`**: Calls the `getProducts` function.
- **`put(getProductsSuccess(response))`**: Dispatches success action.
- **`catch` block**: Dispatches failure action if an error occurs.

### fetchProductDetail
Handles fetching product details:

```javascript
function* fetchProductDetail({ productId }) {
  try {
    const response = yield call(getProductDetail, productId)
    yield put(getProductDetailSuccess(response))
  } catch (error) {
    yield put(getProductDetailFail(error))
  }
}
```

- Takes a `productId` to fetch specific product details.

### fetchOrders
Handles fetching orders:

```javascript
function* fetchOrders() {
  try {
    const response = yield call(getOrders)
    yield put(getOrdersSuccess(response))
  } catch (error) {
    yield put(getOrdersFail(error))
  }
}
```

- **Similar structure** to `fetchProducts`.

### fetchCartData
Handles fetching cart data:

```javascript
function* fetchCartData() {
  try {
    const response = yield call(getCartData)
    yield put(getCartDataSuccess(response))
  } catch (error) {
    yield put(getCartDataFail(error))
  }
}
```

- **Similar structure** to `fetchProducts`.

### fetchCustomers
Handles fetching customer data:

```javascript
function* fetchCustomers() {
  try {
    const response = yield call(getCustomers)
    yield put(getCustomersSuccess(response))
  } catch (error) {
    yield put(getCustomersFail(error))
  }
}
```

- **Similar structure** to `fetchProducts`.

### fetchShops
Handles fetching shop data:

```javascript
function* fetchShops() {
  try {
    const response = yield call(getShops)
    yield put(getShopsSuccess(response))
  } catch (error) {
    yield put(getShopsFail(error))
  }
}
```

- **Similar structure** to `fetchProducts`.

## Root Saga
The `ecommerceSaga` is the root saga that listens for dispatched actions and triggers the appropriate worker saga:

```javascript
function* ecommerceSaga() {
  yield takeEvery(GET_PRODUCTS, fetchProducts)
  yield takeEvery(GET_PRODUCT_DETAIL, fetchProductDetail)
  yield takeEvery(GET_ORDERS, fetchOrders)
  yield takeEvery(GET_CART_DATA, fetchCartData)
  yield takeEvery(GET_CUSTOMERS, fetchCustomers)
  yield takeEvery(GET_SHOPS, fetchShops)
}
```

- **`takeEvery`**: Listens for every dispatched action of the specified type and runs the associated saga function.

## Conclusion
The `saga.js` is an integral part of managing asynchronous flows in a Redux application. It efficiently handles side effects and keeps the logic separated from the UI components, promoting maintainability and scalability. By leveraging Redux-Saga, developers can write complex logic in a clear and testable manner. 🛠️

This file, together with the actions and action types, delivers a robust structure for state management in a React application, ensuring that data fetching and error handling are well-organized and predictable. 🌟

# 📚 Reducer.js Documentation

Welcome to the comprehensive documentation for `reducer.js`. This file is pivotal in the state management of an e-commerce application using Redux. It outlines the structure of the state and defines how the state changes in response to actions dispatched in the application. Let's dive into the details! 🌟

## 🎯 Purpose

The `reducer.js` file is responsible for:
- Defining the initial state of the application.
- Handling state transitions based on different action types.
- Updating the state immutably in response to successes and failures in fetching e-commerce data.

## 🔍 Index

- [Initial State](#initial-state)
- [Reducer Function: `Ecommerce`](#reducer-function-ecommerce)
- [Action Handlers](#action-handlers)
  - [Products](#products)
  - [Product Details](#product-details)
  - [Orders](#orders)
  - [Cart Data](#cart-data)
  - [Customers](#customers)
  - [Shops](#shops)
- [Default Case](#default-case)

## 📋 Initial State

The initial state (`INIT_STATE`) is defined as a JavaScript object containing the default values for different pieces of data used in the e-commerce application.

```javascript
const INIT_STATE = {
  products: [],
  product: {},
  orders: [],
  cartData: {},
  customers: [],
  shops: [],
  error: {},
}
```

### Explanation:
- **products**: An array holding the list of products.
- **product**: An object storing details of a single product.
- **orders**: An array of customer orders.
- **cartData**: An object representing the user's cart.
- **customers**: An array of customer information.
- **shops**: An array of shop details.
- **error**: An object to capture errors from failed actions.

## ⚙️ Reducer Function: `Ecommerce`

The `Ecommerce` reducer function is the core component that manages state updates. It takes the current state and an action as arguments and returns a new state based on the action type.

```javascript
const Ecommerce = (state = INIT_STATE, action) => {
  switch (action.type) {
    // Action handlers
    default:
      return state
  }
}
```

## 🔄 Action Handlers

The reducer contains multiple action handlers that listen for specific action types and update the state accordingly.

### 🛒 Products

- **`GET_PRODUCTS_SUCCESS`**: Updates the state with the list of products.
- **`GET_PRODUCTS_FAIL`**: Captures any errors encountered when fetching products.

```javascript
case GET_PRODUCTS_SUCCESS:
  return { ...state, products: action.payload }

case GET_PRODUCTS_FAIL:
  return { ...state, error: action.payload }
```

### 📝 Product Details

- **`GET_PRODUCT_DETAIL_SUCCESS`**: Stores the details of a specific product.
- **`GET_PRODUCT_DETAIL_FAIL`**: Captures errors when fetching product details.

```javascript
case GET_PRODUCT_DETAIL_SUCCESS:
  return { ...state, product: action.payload }

case GET_PRODUCT_DETAIL_FAIL:
  return { ...state, error: action.payload }
```

### 📦 Orders

- **`GET_ORDERS_SUCCESS`**: Updates the state with customer orders.
- **`GET_ORDERS_FAIL`**: Captures errors when fetching orders.

```javascript
case GET_ORDERS_SUCCESS:
  return { ...state, orders: action.payload }

case GET_ORDERS_FAIL:
  return { ...state, error: action.payload }
```

### 🛒 Cart Data

- **`GET_CART_DATA_SUCCESS`**: Updates the cart data.
- **`GET_CART_DATA_FAIL`**: Captures errors when fetching cart data.

```javascript
case GET_CART_DATA_SUCCESS:
  return { ...state, cartData: action.payload }

case GET_CART_DATA_FAIL:
  return { ...state, error: action.payload }
```

### 👥 Customers

- **`GET_CUSTOMERS_SUCCESS`**: Stores information about customers.
- **`GET_CUSTOMERS_FAIL`**: Captures errors when fetching customer information.

```javascript
case GET_CUSTOMERS_SUCCESS:
  return { ...state, customers: action.payload }

case GET_CUSTOMERS_FAIL:
  return { ...state, error: action.payload }
```

### 🏬 Shops

- **`GET_SHOPS_SUCCESS`**: Updates the state with shop details.
- **`GET_SHOPS_FAIL`**: Captures errors when fetching shops.

```javascript
case GET_SHOPS_SUCCESS:
  return { ...state, shops: action.payload }

case GET_SHOPS_FAIL:
  return { ...state, error: action.payload }
```

## ⚖️ Default Case

The default case in the switch statement ensures that the state remains unchanged if an action type does not match any of the defined cases.

```javascript
default:
  return state
```

This concludes the documentation for `reducer.js`. By understanding each part, you can effectively manage the state of your e-commerce application. Happy coding! 🚀