# Documentation for `actionTypes.js` 📄

Welcome to the documentation for the `actionTypes.js` file. This file plays a critical role in defining the action types used in a Redux application. By understanding the contents and purpose of this file, developers can better manage and maintain their application's state management system. Let's dive into the details!

## Overview

The `actionTypes.js` file is a part of the Redux architecture, which is commonly used in React applications for state management. This file defines constants that represent the types of actions that can be dispatched in the application. By using constants, we reduce the likelihood of typos and ensure consistency across the application.

### Purpose

- **Consistency**: Action types are used across multiple files. Defining them in one location ensures that they are consistent and reduces the risk of errors.
- **Maintainability**: Having a single source of truth for action types makes it easier to update and maintain the application.
- **Scalability**: As the application grows, new action types can be easily added to this file.

## Key Components

The file defines the following action types related to the "Forget Password" functionality of the application. Let's explore each of these:

### Action Types 📋

| Action Type                   | Description                                                                                  |
|-------------------------------|----------------------------------------------------------------------------------------------|
| `FORGET_PASSWORD`             | This action type is dispatched when the user initiates the password recovery process.        |
| `FORGET_PASSWORD_SUCCESS`     | This action type is dispatched when the password recovery process completes successfully.    |
| `FORGET_PASSWORD_ERROR`       | This action type is dispatched when there is an error during the password recovery process.  |

### Code Explanation

Let's take a closer look at the code:

```javascript
export const FORGET_PASSWORD = "FORGET_PASSWORD";
export const FORGET_PASSWORD_SUCCESS = "FORGET_PASSWORD_SUCCESS";
export const FORGET_PASSWORD_ERROR = "FORGET_PASSWORD_ERROR";
```

- **Exported Constants**: Each of the above lines exports a constant representing an action type. These constants are strings, which serve as identifiers for the specific actions in the application.

- **Naming Convention**: The action types follow a clear and descriptive naming convention. The names are all uppercase, which is a common practice to differentiate them from other variables and make them easily recognizable.

## Usage

These action types are typically used in the following parts of a Redux application:

- **Actions**: Functions that create and return action objects. These objects include a `type` property set to one of the action types defined in this file.

  ```javascript
  // Example usage in an action
  export const forgetPassword = (email) => ({
    type: FORGET_PASSWORD,
    payload: { email },
  });
  ```

- **Reducers**: Functions that determine how the application's state changes in response to actions. They use the action types to identify which logic to execute.

  ```javascript
  // Example usage in a reducer
  case FORGET_PASSWORD_SUCCESS:
    return {
      ...state,
      isLoading: false,
      successMessage: action.payload.message,
    };
  ```

- **Sagas**: Middleware functions that handle side effects. They listen for specific action types and execute asynchronous code.

  ```javascript
  // Example usage in a saga
  function* watchForgetPassword() {
    yield takeEvery(FORGET_PASSWORD, handleForgetPassword);
  }
  ```

## Conclusion

The `actionTypes.js` file is a simple yet powerful component of a Redux application. By defining action types in a centralized location, developers can ensure consistency and reduce errors. This file sets the foundation for the application's state management, making it more maintainable and scalable.

Feel free to reach out if you have any questions or need further clarification on the contents of this documentation! 📚✨

# 📄 Actions.js Documentation

This document provides a detailed explanation of the `actions.js` file. This file is a crucial part of Redux and its purpose is to define action creators that facilitate the flow of data between the application and the Redux store. Specifically, it concerns actions related to the process of forgetting a password.

## 📜 Overview

The `actions.js` file utilizes **Redux** action types defined in `actionTypes.js`. The action creators are functions that return action objects, which are then dispatched to the Redux store to update the state based on the user's interaction with the application.

### 🚀 Action Creators

The file defines three main action creators related to the forget password process:

1. **userForgetPassword**
2. **userForgetPasswordSuccess**
3. **userForgetPasswordError**

### ⚙️ Import Statements

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";
```

The above import statement brings in the action types from `actionTypes.js`. These constants are used to define the type of each action creator.

### 🛠️ Action Creators

Below is a detailed explanation of each action creator:

1. **userForgetPassword**

    ```javascript
    export const userForgetPassword = (user, history) => {
      return {
        type: FORGET_PASSWORD,
        payload: { user, history },
      }
    }
    ```

    - **Purpose**: Initiates the forget password process.
    - **Parameters**:
      - `user`: The user object containing information (e.g., email) needed to reset the password.
      - `history`: The history object from React Router, used to navigate programmatically.
    - **Returns**: An action object with type `FORGET_PASSWORD` and a payload containing the user and history.

2. **userForgetPasswordSuccess**

    ```javascript
    export const userForgetPasswordSuccess = message => {
      return {
        type: FORGET_PASSWORD_SUCCESS,
        payload: message,
      }
    }
    ```

    - **Purpose**: Handles successful password reset processes.
    - **Parameters**:
      - `message`: A success message to be displayed to the user.
    - **Returns**: An action object with type `FORGET_PASSWORD_SUCCESS` and a payload containing the success message.

3. **userForgetPasswordError**

    ```javascript
    export const userForgetPasswordError = message => {
      return {
        type: FORGET_PASSWORD_ERROR,
        payload: message,
      }
    }
    ```

    - **Purpose**: Handles errors that occur during the password reset process.
    - **Parameters**:
      - `message`: An error message to be displayed to the user.
    - **Returns**: An action object with type `FORGET_PASSWORD_ERROR` and a payload containing the error message.

## 📚 Conclusion

The `actions.js` file plays a pivotal role in managing the state related to the password reset process. By defining action creators, it allows for the decoupling of logic and state management, leading to a more modular and maintainable codebase. Through these action creators, the application can effectively communicate what changes need to occur in the Redux store based on user interactions.

---

Feel free to delve deeper into each action to understand its implementation details further! If you have any questions, don't hesitate to reach out. Happy coding! 🌟

# Documentation for `actionTypes.js`, `actions.js`, and `reducer.js`

This documentation provides insights into the code structure and functionality for the three provided files related to handling user password resetting in a Redux-based application. They work together to manage the state changes and actions for a "Forget Password" feature.

---

## Index

1. [actionTypes.js](#actiontypesjs)
    - Description
    - Action Types
2. [actions.js](#actionsjs)
    - Description
    - Action Creators
3. [reducer.js](#reducerjs)
    - Description
    - State Management
    - Reducer Function

---

## `actionTypes.js`

### Description

The `actionTypes.js` file defines constants for action types. These action types are used in both actions and reducers to ensure consistency and avoid typos across the codebase.

### Action Types

| **Action Type**              | **Description**                                |
|------------------------------|------------------------------------------------|
| `FORGET_PASSWORD`            | 🚀 Initiates the password reset process.       |
| `FORGET_PASSWORD_SUCCESS`    | ✅ Indicates the password reset was successful. |
| `FORGET_PASSWORD_ERROR`      | ❌ Indicates there was an error during password reset. |

---

## `actions.js`

### Description

The `actions.js` file contains action creators which are functions that return action objects. These actions are dispatched to the Redux store to update the application's state.

### Action Creators

- **`userForgetPassword`**
  - **Purpose**: Dispatches the `FORGET_PASSWORD` action to initiate the password reset process.
  - **Parameters**:
    - `user`: The user object containing information to reset the password.
    - `history`: React Router’s history object for navigation purposes.
  - **Usage**:
    ```javascript
    userForgetPassword(user, history)
    ```
  - **Returns**: An action object with type `FORGET_PASSWORD` and payload containing user and history.

- **`userForgetPasswordSuccess`**
  - **Purpose**: Dispatches the `FORGET_PASSWORD_SUCCESS` action when the password reset is successful.
  - **Parameters**:
    - `message`: Success message string.
  - **Usage**:
    ```javascript
    userForgetPasswordSuccess(message)
    ```
  - **Returns**: An action object with type `FORGET_PASSWORD_SUCCESS` and payload containing the success message.

- **`userForgetPasswordError`**
  - **Purpose**: Dispatches the `FORGET_PASSWORD_ERROR` action when there is an error during the password reset process.
  - **Parameters**:
    - `message`: Error message string.
  - **Usage**:
    ```javascript
    userForgetPasswordError(message)
    ```
  - **Returns**: An action object with type `FORGET_PASSWORD_ERROR` and payload containing the error message.

---

## `reducer.js`

### Description

The `reducer.js` file exports a reducer function that manages the state related to the password reset process. It handles the actions dispatched by the action creators and updates the state accordingly.

### State Management

- **Initial State**:
  - `forgetSuccessMsg`: Initially set to `null`. It stores the success message after a successful password reset.
  - `forgetError`: Initially set to `null`. It stores the error message if the password reset encounters any issues.

### Reducer Function

- **`forgetPassword`**
  - **Parameters**:
    - `state`: The current state of the reducer, initialized with `initialState`.
    - `action`: The action dispatched to the reducer.
  - **Switch Cases**:
    - **`FORGET_PASSWORD`**: Resets both `forgetSuccessMsg` and `forgetError` to `null` as the process begins.
    - **`FORGET_PASSWORD_SUCCESS`**: Updates the `forgetSuccessMsg` with the message from the action's payload.
    - **`FORGET_PASSWORD_ERROR`**: Updates `forgetError` with the error message from the action's payload.
    - **`default`**: Returns the current state if no relevant action type is matched.
  - **Returns**: The updated state based on the action type.

### Usage Example

```javascript
import forgetPassword from './reducer';

// Initial state
let state = forgetPassword(undefined, {});
console.log(state); // { forgetSuccessMsg: null, forgetError: null }

// Dispatch a success action
state = forgetPassword(state, userForgetPasswordSuccess('Password reset successful!'));
console.log(state); // { forgetSuccessMsg: 'Password reset successful!', forgetError: null }

// Dispatch an error action
state = forgetPassword(state, userForgetPasswordError('Error resetting password.'));
console.log(state); // { forgetSuccessMsg: 'Password reset successful!', forgetError: 'Error resetting password.' }
```

---

This documentation provides a comprehensive overview of how these files work together to handle the "Forget Password" feature using Redux. By defining action types, creating actions, and managing state with the reducer, this implementation ensures a consistent and efficient user password reset process.

# Documentation for Forget Password Module

This documentation provides a detailed overview of the Forget Password functionality implemented across four key files: `actionTypes.js`, `actions.js`, `reducer.js`, and `saga.js`. Each file plays a specific role in handling the forget password process within a React-Redux application.

## **1. actionTypes.js**

### **Purpose**

This file defines constants that represent the action types for handling the forget password process. These constants are used to identify the specific actions dispatched to the Redux store.

### **Code Explanation**

```javascript
export const FORGET_PASSWORD = "FORGET_PASSWORD";
export const FORGET_PASSWORD_SUCCESS = "FORGET_PASSWORD_SUCCESS";
export const FORGET_PASSWORD_ERROR = "FORGET_PASSWORD_ERROR";
```

- **FORGET_PASSWORD**: This action type is dispatched when a user initiates the forget password process.
- **FORGET_PASSWORD_SUCCESS**: This action type is dispatched when the forget password request is successful, and the user receives a reset link.
- **FORGET_PASSWORD_ERROR**: This action type is dispatched when there is an error during the forget password request.

## **2. actions.js**

### **Purpose**

This file defines action creators for the forget password process. These functions create actions that are dispatched to the Redux store.

### **Code Explanation**

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";

export const userForgetPassword = (user, history) => {
  return {
    type: FORGET_PASSWORD,
    payload: { user, history },
  };
};

export const userForgetPasswordSuccess = message => {
  return {
    type: FORGET_PASSWORD_SUCCESS,
    payload: message,
  };
};

export const userForgetPasswordError = message => {
  return {
    type: FORGET_PASSWORD_ERROR,
    payload: message,
  };
};
```

- **userForgetPassword**: Creates an action to initiate the forget password process, carrying the user data and navigation history as payload.
- **userForgetPasswordSuccess**: Creates an action indicating the forget password request was successful, carrying a success message.
- **userForgetPasswordError**: Creates an action indicating there was an error in the forget password request, carrying an error message.

## **3. reducer.js**

### **Purpose**

This file implements the reducer function that updates the Redux store based on the actions dispatched during the forget password process.

### **Code Explanation**

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";

const initialState = {
  forgetSuccessMsg: null,
  forgetError: null,
};

const forgetPassword = (state = initialState, action) => {
  switch (action.type) {
    case FORGET_PASSWORD:
      state = {
        ...state,
        forgetSuccessMsg: null,
        forgetError: null,
      };
      break;
    case FORGET_PASSWORD_SUCCESS:
      state = {
        ...state,
        forgetSuccessMsg: action.payload,
      };
      break;
    case FORGET_PASSWORD_ERROR:
      state = {
        ...state,
        forgetError: action.payload
      };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default forgetPassword;
```

- **Initial State**: The initial state includes `forgetSuccessMsg` and `forgetError`, both initialized to `null`.
- **FORGET_PASSWORD**: Resets the success message and error to `null`.
- **FORGET_PASSWORD_SUCCESS**: Updates the state with a success message from the action payload.
- **FORGET_PASSWORD_ERROR**: Updates the state with an error message from the action payload.

## **4. saga.js**

### **Purpose**

This file implements Redux-Saga middleware to handle side effects for the forget password process, such as making asynchronous API calls.

### **Code Explanation**

```javascript
import { takeEvery, fork, put, all, call } from "redux-saga/effects";
import { FORGET_PASSWORD } from "./actionTypes";
import { userForgetPasswordSuccess, userForgetPasswordError } from "./actions";
import { getFirebaseBackend } from "../../../helpers/firebase_helper";
import { postFakeForgetPwd, postJwtForgetPwd } from "../../../helpers/fakebackend_helper";

const fireBaseBackend = getFirebaseBackend();

function* forgetUser({ payload: { user, history } }) {
  try {
    if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
      const response = yield call(fireBaseBackend.forgetPassword, user.email);
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sent to your mailbox, check there first"));
      }
    } else if (process.env.REACT_APP_DEFAULTAUTH === "jwt") {
      const response = yield call(postJwtForgetPwd, "/jwt-forget-pwd", { email: user.email });
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sent to your mailbox, check there first"));
      }
    } else {
      const response = yield call(postFakeForgetPwd, "/fake-forget-pwd", { email: user.email });
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sent to your mailbox, check there first"));
      }
    }
  } catch (error) {
    yield put(userForgetPasswordError(error));
  }
}

export function* watchUserPasswordForget() {
  yield takeEvery(FORGET_PASSWORD, forgetUser);
}

function* forgetPasswordSaga() {
  yield all([fork(watchUserPasswordForget)]);
}

export default forgetPasswordSaga;
```

- **forgetUser**: A generator function handling the forget password logic. It supports different authentication methods (Firebase, JWT, Fake backend) and dispatches success or error actions based on the API response.
- **watchUserPasswordForget**: Watches for `FORGET_PASSWORD` actions and triggers `forgetUser`.
- **forgetPasswordSaga**: Combines all the sagas using `all` and `fork` to run them concurrently.

---

This documentation provides a comprehensive overview of the forget password functionality within the application, outlining the roles and responsibilities of each file involved in the process. 🎉

# Documentation for `actions.js` 📄

Welcome to the comprehensive documentation for the `actions.js` file! This file plays a crucial role in managing actions in a Redux-based application. Actions are payloads of information that send data from your application to your Redux store. They are the only source of information for the store.

## File Overview 📚

The `actions.js` file is responsible for defining action creators. These functions return action objects, which are then dispatched to the Redux store. This file imports various action types from the `actionTypes.js` file and provides action creators for different use cases, such as user login, logout, error handling, and managing game, prize, and schedule data.

## Table of Contents 📑

1. [Imports](#imports)
2. [Action Creators](#action-creators)
   - [Login Actions](#login-actions)
   - [Logout Actions](#logout-actions)
   - [Error Handling](#error-handling)
   - [Social Login](#social-login)
   - [Game Management](#game-management)
   - [Prize Management](#prize-management)
   - [Schedule Management](#schedule-management)
3. [Conclusion](#conclusion)

## Imports 📥

```javascript
import { gamesToCategories } from "../../../helpers/util";
import {
  LOGIN_USER,
  LOGIN_SUCCESS,
  LOGOUT_USER,
  LOGOUT_USER_SUCCESS,
  API_ERROR,
  SOCIAL_LOGIN,
  SET_GAMES,
  SET_PRIZE_LIST,
  SET_SCHEDULE_LIST,
  SET_SCHEDULE_COUNT,
  SET_CLEAR_PRIZE_LIST,
  UPDATE_PRIZE_COUNT,
  UPDATE_PRIZE_LIST,
  UPDATE_SCHEDULE_LIST,
  SET_CLEAR_SCHEDULE_LIST,
} from "./actionTypes";
```

- **`gamesToCategories`**: A utility function for categorizing games.
- Various **action types**: Constants representing different types of actions.

## Action Creators 🚀

### Login Actions 🔐

- **`loginUser`**: Initiates the login process for a user.

  ```javascript
  export const loginUser = (user, history) => {
    return {
      type: LOGIN_USER,
      payload: { user, history },
    };
  };
  ```

- **`loginSuccess`**: Called when a user successfully logs in.

  ```javascript
  export const loginSuccess = (user) => {
    return {
      type: LOGIN_SUCCESS,
      payload: user,
    };
  };
  ```

### Logout Actions 🚪

- **`logoutUser`**: Initiates the logout process for a user.

  ```javascript
  export const logoutUser = (history) => {
    return {
      type: LOGOUT_USER,
      payload: { history },
    };
  };
  ```

- **`logoutUserSuccess`**: Confirms a successful logout.

  ```javascript
  export const logoutUserSuccess = () => {
    return {
      type: LOGOUT_USER_SUCCESS,
      payload: {},
    };
  };
  ```

### Error Handling ❗

- **`apiError`**: Handles API errors during various processes.

  ```javascript
  export const apiError = (error) => {
    return {
      type: API_ERROR,
      payload: error,
    };
  };
  ```

### Social Login 🌐

- **`socialLogin`**: Initiates social login for a user.

  ```javascript
  export const socialLogin = (data, history, type) => {
    return {
      type: SOCIAL_LOGIN,
      payload: { data, history, type },
    };
  };
  ```

### Game Management 🎮

- **`setGames`**: Sets the games list with categorized data.

  ```javascript
  export const setGames = (data) => {
    return {
      type: SET_GAMES,
      payload: gamesToCategories(data),
    };
  };
  ```

### Prize Management 🏆

- **`setPrizeList`**: Sets the prize list.

  ```javascript
  export const setPrizeList = (prizeList) => {
    return {
      type: SET_PRIZE_LIST,
      payload: prizeList,
    };
  };
  ```

- **`setClearPrizeList`**: Clears the prize list.

  ```javascript
  export const setClearPrizeList = () => {
    return {
      type: SET_CLEAR_PRIZE_LIST,
      payload: {},
    };
  };
  ```

- **`updatePrizeCount`**: Updates the prize count.

  ```javascript
  export const updatePrizeCount = (prizeCount) => {
    return {
      type: UPDATE_PRIZE_COUNT,
      payload: prizeCount,
    };
  };
  ```

- **`updatePrizeList`**: Updates the prize list.

  ```javascript
  export const updatePrizeList = () => {
    return {
      type: UPDATE_PRIZE_LIST,
    };
  };
  ```

### Schedule Management 📅

- **`setScheduleList`**: Sets the schedule list.

  ```javascript
  export const setScheduleList = (scheduleList) => {
    return {
      type: SET_SCHEDULE_LIST,
      payload: scheduleList,
    };
  };
  ```

- **`setScheduleCount`**: Sets the schedule count.

  ```javascript
  export const setScheduleCount = (scheduleCount) => {
    return {
      type: SET_SCHEDULE_COUNT,
      payload: scheduleCount,
    };
  };
  ```

- **`updateScheduleList`**: Updates the schedule list.

  ```javascript
  export const updateScheduleList = () => {
    return {
      type: UPDATE_SCHEDULE_LIST,
    };
  };
  ```

- **`setClearScheduleList`**: Clears the schedule list.

  ```javascript
  export const setClearScheduleList = () => {
    return {
      type: SET_CLEAR_SCHEDULE_LIST,
      payload: {},
    };
  };
  ```

## Conclusion 🎉

In summary, the `actions.js` file is an essential component of the Redux architecture in this application. It defines a plethora of actions that manage user authentication, error handling, and the manipulation of games, prizes, and schedules.

Feel free to explore each action creator and understand how they are used within the application to manage state effectively. Happy coding! 🚀

# Documentation for `actionTypes.js`

## Overview 📑

The `actionTypes.js` file is a crucial part of the Redux architecture, especially in managing actions that are dispatched in response to user interactions or events in a web application. This file defines a set of constant strings that represent the types of actions that can be dispatched, ensuring consistency and reducing the likelihood of errors due to typos.

## Action Types Defined 🚀

The following table outlines the action types defined in this file, along with their descriptions:

| Action Type                  | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| `LOGIN_USER`                 | Initiates the process of logging in a user.                                 |
| `LOGIN_SUCCESS`              | Indicates that a user has successfully logged in.                           |
| `LOGOUT_USER`                | Initiates the process of logging out a user.                                |
| `LOGOUT_USER_SUCCESS`        | Indicates that a user has successfully logged out.                          |
| `API_ERROR`                  | Represents an error that occurred during an API call related to login.      |
| `SOCIAL_LOGIN`               | Initiates the process of logging in using a social login method.            |
| `SET_GAMES`                  | Sets the list of games available.                                           |
| `SET_PRIZE_LIST`             | Sets the list of available prizes.                                          |
| `SET_CLEAR_PRIZE_LIST`       | Clears the list of prizes, typically used for resetting state.              |
| `UPDATE_PRIZE_COUNT`         | Updates the count of prizes available.                                      |
| `UPDATE_PRIZE_LIST`          | Updates the list of prizes, often used when new prizes are added.           |
| `SET_SCHEDULE_LIST`          | Sets the list of schedules available.                                       |
| `SET_SCHEDULE_COUNT`         | Sets the count of schedules available.                                      |
| `UPDATE_SCHEDULE_LIST`       | Updates the list of schedules, often used when new schedules are added.     |
| `SET_CLEAR_SCHEDULE_LIST`    | Clears the list of schedules, typically used for resetting state.           |

## Usage 📘

In a Redux application, action types serve as identifiers for actions. By using constants for action types, developers can avoid potential bugs that arise from using hard-coded strings throughout their application. Here's an example of how these action types might be used in an action creator:

```javascript
import { LOGIN_USER } from './actionTypes';

export const loginUser = (user, history) => {
    return {
        type: LOGIN_USER,
        payload: { user, history }
    };
};
```

## Conclusion 🎉

The `actionTypes.js` file plays a pivotal role in maintaining a clean and maintainable Redux architecture. By centralizing the action type definitions, developers can ensure that their applications remain robust, less error-prone, and easier to debug. This file acts as a dictionary of the possible actions that can occur within the application, serving as a reference for developers as they create and manage different application states.

# Documentation for `gameReducer.js` 🎮

## Overview

The **`gameReducer.js`** file contains a Redux reducer that manages the state related to game data within an application. This reducer is responsible for handling actions that update the list of games and their associated categories. It listens for specific action types to update the state accordingly.

## Contents

- **Initial State**: Defines the structure of the initial state for games.
- **Reducer Function**: Handles state changes based on dispatched actions.
  
## Initial State

The initial state is defined as follows:

```javascript
const initialState = {
  game: {
    ppkGames: [],        // List of Pay per Kill games
    killRaceGames: [],   // List of Kill Race games
    traditionalGames: [],// List of Traditional games
    allGames: [],        // List of all games
    modeObj: {},         // Additional game mode data
  },
};
```
  
This initial state sets up empty arrays for different categories of games, as well as an empty object for additional mode data.

## Reducer Function

### Function Signature

```javascript
const gameReducer = (state = initialState, { type, payload } = {}) => {
  ...
};
```

### Functionality

The **`gameReducer`** function takes two parameters:
- `state`: The current state of the game data, initialized to `initialState`.
- An action object containing `type` and `payload`.

### Action Handling

The `gameReducer` listens for the following action type:

- **`SET_GAMES`**: When this action is dispatched, the reducer updates the state with the new game data provided in the `payload`.

### Code Logic

```javascript
if (type === SET_GAMES) {
  return { ...state, game: payload };
} else {
  return (state = { ...state });
}
```

- **SET_GAMES**: If the action type is `SET_GAMES`, the reducer updates the `game` part of the state with the `payload`.
- **Default**: If no recognized action type is dispatched, the state remains unchanged.

## Export

The reducer is exported as the default export of the module:

```javascript
export default gameReducer;
```

This allows it to be easily imported and used in the application's Redux store setup.

## Conclusion

The **`gameReducer.js`** plays a crucial role in managing the state related to games within the application. By responding to the `SET_GAMES` action, it ensures that the game's data is kept up-to-date, reflecting any changes made elsewhere in the application. This helps maintain a consistent and responsive gaming experience for users.

# Documentation for Redux and Redux-Saga Files

This documentation provides an in-depth look into the JavaScript files used for handling Redux actions, action types, reducers, and sagas related to user authentication, game settings, and more. Each section will describe the purpose of the file, the code within, and how it integrates into the larger application.

## Table of Contents
1. [actionTypes.js (Forget Password)](#actiontypesjs-forget-password)
2. [actions.js (Forget Password)](#actionsjs-forget-password)
3. [reducer.js (Forget Password)](#reducerjs-forget-password)
4. [saga.js (Forget Password)](#sagajs-forget-password)
5. [actions.js (General Actions)](#actionsjs-general-actions)
6. [actionTypes.js (General Action Types)](#actiontypesjs-general-action-types)
7. [gameReducer.js](#gamereducerjs)
8. [authSaga.js](#authsagajs)

---

## actionTypes.js (Forget Password)

This file defines the action types related to the forget password functionality.

```javascript
export const FORGET_PASSWORD = "FORGET_PASSWORD";
export const FORGET_PASSWORD_SUCCESS = "FORGET_PASSWORD_SUCCESS";
export const FORGET_PASSWORD_ERROR = "FORGET_PASSWORD_ERROR";
```

### Purpose
- **Action Types**: This file exports constants that represent specific actions in the Redux flow, particularly for handling password reset requests.

### Key Points
- **FORGET_PASSWORD**: Initiates the forget password process.
- **FORGET_PASSWORD_SUCCESS**: Indicates success in the forget password process.
- **FORGET_PASSWORD_ERROR**: Represents an error during the forget password process.

---

## actions.js (Forget Password)

This file exports actions to handle the forget password process.

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";

export const userForgetPassword = (user, history) => {
  return {
    type: FORGET_PASSWORD,
    payload: { user, history },
  };
};

export const userForgetPasswordSuccess = message => {
  return {
    type: FORGET_PASSWORD_SUCCESS,
    payload: message,
  };
};

export const userForgetPasswordError = message => {
  return {
    type: FORGET_PASSWORD_ERROR,
    payload: message,
  };
};
```

### Purpose
- **Actions**: Functions that return Redux action objects. They are dispatched to trigger state changes in the Redux store.

### Key Actions
- **userForgetPassword**: Dispatches an action to initiate the forget password process.
- **userForgetPasswordSuccess**: Dispatches an action when the password reset link is successfully sent.
- **userForgetPasswordError**: Dispatches an action when there is an error in sending the reset link.

---

## reducer.js (Forget Password)

This file contains the reducer for managing the forget password state.

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";

const initialState = {
  forgetSuccessMsg: null,
  forgetError: null,
};

const forgetPassword = (state = initialState, action) => {
  switch (action.type) {
    case FORGET_PASSWORD:
      state = { ...state, forgetSuccessMsg: null, forgetError: null };
      break;
    case FORGET_PASSWORD_SUCCESS:
      state = { ...state, forgetSuccessMsg: action.payload };
      break;
    case FORGET_PASSWORD_ERROR:
      state = { ...state, forgetError: action.payload };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default forgetPassword;
```

### Purpose
- **Reducer**: Manages the state related to forget password actions by responding to dispatched actions and returning the new state.

### Key Points
- **Initial State**: Contains `forgetSuccessMsg` and `forgetError` to store success and error messages.
- **Action Handling**: Depending on the action type, it updates the state accordingly.

---

## saga.js (Forget Password)

This file implements a saga to handle side effects for the forget password functionality.

```javascript
import { takeEvery, fork, put, all, call } from "redux-saga/effects";
// Login Redux States
import { FORGET_PASSWORD } from "./actionTypes";
import { userForgetPasswordSuccess, userForgetPasswordError } from "./actions";
//Include Both Helper File with needed methods
import { getFirebaseBackend } from "../../../helpers/firebase_helper";
import { postFakeForgetPwd, postJwtForgetPwd } from "../../../helpers/fakebackend_helper";

const fireBaseBackend = getFirebaseBackend();

//If user is send successfully send mail link then dispatch redux action's are directly from here.
function* forgetUser({ payload: { user, history } }) {
  try {
    if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
      const response = yield call(fireBaseBackend.forgetPassword, user.email);
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sended to your mailbox, check there first"));
      }
    }
    // Additional logic for JWT and Fake backends...
  } catch (error) {
    yield put(userForgetPasswordError(error));
  }
}

export function* watchUserPasswordForget() {
  yield takeEvery(FORGET_PASSWORD, forgetUser);
}

function* forgetPasswordSaga() {
  yield all([fork(watchUserPasswordForget)]);
}

export default forgetPasswordSaga;
```

### Purpose
- **Saga**: Manages side effects like asynchronous requests and complex synchronous actions.

### Key Points
- **forgetUser**: Manages the logic for sending password reset emails using different backends (Firebase, JWT, Fake).
- **watchUserPasswordForget**: Watches for `FORGET_PASSWORD` actions and triggers `forgetUser`.

---

## actions.js (General Actions)

This file exports a variety of actions related to user management, games, prizes, and schedules.

```javascript
import { gamesToCategories } from "../../../helpers/util";
import {
  LOGIN_USER, LOGIN_SUCCESS, LOGOUT_USER, LOGOUT_USER_SUCCESS, API_ERROR, SOCIAL_LOGIN,
  SET_GAMES, SET_PRIZE_LIST, SET_SCHEDULE_LIST, SET_SCHEDULE_COUNT, SET_CLEAR_PRIZE_LIST,
  UPDATE_PRIZE_COUNT, UPDATE_PRIZE_LIST, UPDATE_SCHEDULE_LIST, SET_CLEAR_SCHEDULE_LIST,
} from "./actionTypes";

// User Authentication Actions
export const loginUser = (user, history) => ({
  type: LOGIN_USER,
  payload: { user, history },
});

// Additional actions for loginSuccess, logoutUser, apiError, etc...
```

### Purpose
- **Actions**: Define a set of actions for managing user authentication, games, prizes, and schedules.

### Key Actions
- **loginUser**: Initiates a login action.
- **setGames**: Sets the list of games.
- **setPrizeList**: Updates the prize list.
- **setScheduleList**: Updates the schedule list.

---

## actionTypes.js (General Action Types)

This file defines action types for various functionalities such as user authentication, game settings, and more.

```javascript
export const LOGIN_USER = "LOGIN_USER";
export const LOGIN_SUCCESS = "LOGIN_SUCCESS";
// Additional action types...
export const SET_GAMES = "SET_GAMES";
export const SET_PRIZE_LIST = "SET_PRIZE_LIST";
// More action types...
```

### Purpose
- **Action Types**: Provide a set of constants for different actions, ensuring consistent use across actions, reducers, and sagas.

### Key Points
- **LOGIN_USER**: Triggered when a user attempts to log in.
- **SET_GAMES**: Used to set the game data in the state.

---

## gameReducer.js

This file defines the reducer for managing game-related state.

```javascript
import { SET_GAMES } from "./actionTypes";

const initialState = {
  game: {
    ppkGames: [],
    killRaceGames: [],
    traditionalGames: [],
    allGames: [],
    modeObj: {},
  },
};

const gameReducer = (state = initialState, { type, payload } = {}) => {
  if (type === SET_GAMES) {
    return { ...state, game: payload };
  } else {
    return (state = { ...state });
  }
};

export default gameReducer;
```

### Purpose
- **Reducer**: Handles the state management for game data.

### Key Points
- **Initial State**: Contains categorized game arrays and a mode object.
- **Handling SET_GAMES**: Updates the game state with new data.

---

## authSaga.js

This file implements a saga handling side effects for user authentication.

```javascript
import { put, takeEvery } from "redux-saga/effects";
import { LOGIN_USER } from "./actionTypes";
import { apiError } from "./actions";
import axios from "axios";

function* loginUser({ payload: { user, history } }) {
  try {
    const body = { email: user.email, password: user.password };
    const url = process.env.REACT_APP_APIURL + "login/";
    const isProduction = process.env.REACT_APP_PRODUCTION;
    let headers;
    if (!isProduction) {
      headers = { Authorization: `Bearer ${process.env.REACT_APP_CLIENTTOKEN}`, "Content-Type": "application/json" };
    }
    axios
      .post(url, body, { headers })
      .then((res) => {
        localStorage.setItem("authUser", JSON.stringify(res.data));
        history.push("/users");
      })
      .catch((err) => {
        put(apiError(err));
      });
  } catch (error) {
    yield put(apiError(error));
  }
}

function* authSaga() {
  yield takeEvery(LOGIN_USER, loginUser);
}

export default authSaga;
```

### Purpose
- **Saga**: Manages side effects for user authentication, such as logging in through an API call.

### Key Points
- **loginUser**: Sends a login request to the server and manages the response.
- **authSaga**: Watches for `LOGIN_USER` actions and triggers `loginUser`.

---

This concludes the documentation for these JavaScript files. The integration of Redux and Redux-Saga simplifies the handling of state and side effects, making the application more scalable and maintainable.

# Documentation for `loginReducer.js` 📄

Welcome to the documentation for the **`loginReducer.js`** file, which is a part of the Redux implementation for managing the authentication state in a React application. This reducer handles actions related to user login, logout, and API errors.

## Index 📑
- [Purpose](#purpose-)
- [Initial State](#initial-state-)
- [Reducer Function](#reducer-function-)
- [Action Types](#action-types-)
- [Usage](#usage-)

## Purpose 🎯
The `loginReducer.js` file is designed to manage the state of the application's login functionality. It handles changes to the state based on different actions dispatched during the login process, such as starting a login, successful login, logging out, and handling errors.

## Initial State 🌱
The reducer initializes with the following state:

```javascript
const initialState = {
  error: "",
  loading: false,
};
```

- **`error`**: A string that holds any error message encountered during login operations.
- **`loading`**: A boolean that indicates whether a login operation is in progress.

## Reducer Function ⚙️
The reducer function is responsible for updating the state based on the action types it receives. Here's a breakdown of its functionality:

```javascript
const loginReducer = (state = initialState, { type, payload }={}) => {
  switch (type) {
    case LOGIN_USER:
      state = { ...state, loading: true };
      break;

    case LOGIN_SUCCESS:
      state = { ...state, loading: false };
      break;

    case LOGOUT_USER:
      state = { ...state };
      break;

    case LOGOUT_USER_SUCCESS:
      state = { ...state };
      break;

    case API_ERROR:
      state = { ...state, error: payload, loading: false };
      break;

    default:
      state = { ...state };
      break;
  }
  return state;
};
```

### Key Points:
- **`LOGIN_USER`**: Sets `loading` to `true` to indicate a login attempt is in progress.
- **`LOGIN_SUCCESS`**: Sets `loading` to `false` to indicate the login attempt is completed successfully.
- **`LOGOUT_USER`** and **`LOGOUT_USER_SUCCESS`**: Maintains the current state without changes. These cases could be expanded in the future to handle specific logout-related state changes.
- **`API_ERROR`**: Updates the `error` state with the error message received in the payload and sets `loading` to `false`.
- **`default`**: Returns the current state for any unhandled action types.

## Action Types 🎬
The reducer utilizes the following action types, which are imported from `actionTypes.js`:

- **`LOGIN_USER`**: Initiates the login process.
- **`LOGIN_SUCCESS`**: Indicates a successful login.
- **`LOGOUT_USER`**: Initiates the logout process.
- **`LOGOUT_USER_SUCCESS`**: Indicates a successful logout.
- **`API_ERROR`**: Handles any API errors that occur during authentication processes.

## Usage 📘
This reducer should be combined with other reducers in the application using `combineReducers` from Redux. It is connected to the Redux store to manage the login-related state.

```javascript
import { combineReducers } from 'redux';
import loginReducer from './loginReducer';

const rootReducer = combineReducers({
  login: loginReducer,
  // other reducers...
});

export default rootReducer;
```

By understanding the structure and functionality of the `loginReducer.js` file, developers can effectively manage the authentication state of their application and handle user login processes efficiently.

# Prize Reducer Documentation 📜

The `prizeReducer.js` file is part of a Redux setup in a React application and is responsible for managing the application's state related to prizes. This is crucial for maintaining and updating the prize data efficiently.

## Table of Contents
- [Overview](#overview)
- [Initial State](#initial-state)
- [Action Types](#action-types)
- [Reducer Logic](#reducer-logic)
- [Exports](#exports)

## Overview
The prize reducer handles the state of prizes for a particular feature in the application. It manages a list of prizes, updates the count of prizes, and has the ability to clear the prize list. This reducer responds to specific action types to update the state accordingly.

## Initial State

```javascript
const initialState = {
  prize: [],
  count: 0,
};
```
- **`prize`**: An empty array that will eventually hold the list of prizes.
- **`count`**: An integer that keeps track of the number of prizes.

## Action Types

The reducer listens for the following action types imported from `actionTypes.js`:

| Action Type            | Description                                   |
|------------------------|-----------------------------------------------|
| `SET_PRIZE_LIST`       | Sets the list of prizes.                      |
| `UPDATE_PRIZE_COUNT`   | Updates the count of prizes.                  |
| `UPDATE_PRIZE_LIST`    | Updates the prize list based on the count.    |
| `SET_CLEAR_PRIZE_LIST` | Clears the prize list and resets the count.   |

## Reducer Logic

The reducer function, `prizeReducer`, handles the state changes based on different actions dispatched:

```javascript
const prizeReducer = (state = initialState, action) => {
  switch (action.type) {
    case SET_PRIZE_LIST:
      return {
        ...state,
        prize: action === undefined ? [] : action.payload.map(({ positionLabel, ...rest }) => ({ ...rest })),
      };
      
    case UPDATE_PRIZE_COUNT:
      return {
        ...state,
        count: action.payload,
      };
      
    case UPDATE_PRIZE_LIST:
      return {
        ...state,
        prize: [...state.prize.slice(0, state.count)],
      };
      
    case SET_CLEAR_PRIZE_LIST:
      return {
        count: 0,
        prize: [],
      };
      
    default:
      state = { ...state };
      break;
  }
  return state;
};
```

### Action Handling
- **`SET_PRIZE_LIST`**: Maps the payload to remove `positionLabel` and sets the prize state.
- **`UPDATE_PRIZE_COUNT`**: Sets the `count` state with the payload.
- **`UPDATE_PRIZE_LIST`**: Slices the prize list up to the number specified in the count.
- **`SET_CLEAR_PRIZE_LIST`**: Resets the prize list and count to their initial states.

## Exports

```javascript
export default prizeReducer;
```

The `prizeReducer` function is exported as the default export. This function will be combined with other reducers in the Redux store configuration.

## Conclusion

The `prizeReducer.js` file is a crucial part of the Redux architecture, enabling the application to manage prize data effectively. By handling specific actions, it ensures the correct state transitions necessary for application functionality. 🎉

# Documentation for Redux-Saga Authentication Flow

This documentation provides a detailed explanation of the Redux-Saga workflow for authentication, including the login process. It encompasses four main JavaScript files: `actionTypes.js`, `actions.js`, `loginReducer.js`, and `saga.js`. These files are responsible for defining action types, handling actions, updating the state, and managing side effects respectively.

## Index

1. [File: actionTypes.js](#file-actiontypesjs)
2. [File: actions.js](#file-actionsjs)
3. [File: loginReducer.js](#file-loginreducerjs)
4. [File: saga.js](#file-sagajs)

---

## File: actionTypes.js

This file defines the action types as constants, which are used throughout the authentication process to ensure consistency and avoid typos.

### Action Types

| Constant Name         | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `LOGIN_USER`          | Action type for initiating a user login.                                    |
| `LOGIN_SUCCESS`       | Action type for successful login.                                           |
| `LOGOUT_USER`         | Action type for logging out a user.                                         |
| `LOGOUT_USER_SUCCESS` | Action type for a successful logout.                                        |
| `API_ERROR`           | Action type for handling API errors.                                        |
| `SOCIAL_LOGIN`        | Action type for logging in via social media.                                |
| `SET_GAMES`           | Action type for setting games data.                                         |
| `SET_PRIZE_LIST`      | Action type for setting prize list data.                                    |
| `SET_CLEAR_PRIZE_LIST`| Action type for clearing the prize list data.                               |
| `UPDATE_PRIZE_COUNT`  | Action type for updating the count of prizes.                               |
| `UPDATE_PRIZE_LIST`   | Action type for updating the prize list.                                    |
| `SET_SCHEDULE_LIST`   | Action type for setting schedule list data.                                 |
| `SET_SCHEDULE_COUNT`  | Action type for setting the count of schedules.                             |
| `UPDATE_SCHEDULE_LIST`| Action type for updating the schedule list.                                 |
| `SET_CLEAR_SCHEDULE_LIST` | Action type for clearing the schedule list data.                       |

These constants are primarily used in the other JavaScript files to trigger specific actions related to the Redux state.

---

## File: actions.js

This file defines action creator functions, which return action objects. These actions are dispatched to the Redux store to alter the state.

### Action Creators

```javascript
import { LOGIN_USER, LOGIN_SUCCESS, LOGOUT_USER, LOGOUT_USER_SUCCESS, API_ERROR, SOCIAL_LOGIN, SET_GAMES, SET_PRIZE_LIST, SET_SCHEDULE_LIST, SET_SCHEDULE_COUNT, SET_CLEAR_PRIZE_LIST, UPDATE_PRIZE_COUNT, UPDATE_PRIZE_LIST, UPDATE_SCHEDULE_LIST, SET_CLEAR_SCHEDULE_LIST, } from "./actionTypes";

export const loginUser = (user, history) => ({
    type: LOGIN_USER,
    payload: { user, history },
});

export const loginSuccess = (user) => ({
    type: LOGIN_SUCCESS,
    payload: user,
});

export const logoutUser = (history) => ({
    type: LOGOUT_USER,
    payload: { history },
});

export const logoutUserSuccess = () => ({
    type: LOGOUT_USER_SUCCESS,
    payload: {},
});

export const apiError = (error) => ({
    type: API_ERROR,
    payload: error,
});

export const socialLogin = (data, history, type) => ({
    type: SOCIAL_LOGIN,
    payload: { data, history, type },
});

export const setGames = (data) => ({
    type: SET_GAMES,
    payload: gamesToCategories(data),
});

export const setPrizeList = (prizeList) => ({
    type: SET_PRIZE_LIST,
    payload: prizeList,
});

export const setClearPrizeList = () => ({
    type: SET_CLEAR_PRIZE_LIST,
    payload: {},
});

export const updatePrizeCount = (prizeCount) => ({
    type: UPDATE_PRIZE_COUNT,
    payload: prizeCount,
});

export const updatePrizeList = () => ({
    type: UPDATE_PRIZE_LIST,
});

export const setScheduleList = (scheduleList) => ({
    type: SET_SCHEDULE_LIST,
    payload: scheduleList,
});

export const setScheduleCount = (scheduleCount) => ({
    type: SET_SCHEDULE_COUNT,
    payload: scheduleCount,
});

export const updateScheduleList = () => ({
    type: UPDATE_SCHEDULE_LIST,
});

export const setClearScheduleList = () => ({
    type: SET_CLEAR_SCHEDULE_LIST,
    payload: {},
});
```

These action creators provide a standardized way to trigger state changes in response to user interactions in the application.

---

## File: loginReducer.js

This file contains the reducer function responsible for updating the state related to user authentication.

### Reducer

```javascript
import { LOGIN_USER, LOGIN_SUCCESS, LOGOUT_USER, LOGOUT_USER_SUCCESS, API_ERROR } from "./actionTypes";

const initialState = {
    error: "",
    loading: false,
};

const loginReducer = (state = initialState, { type, payload } = {}) => {
    switch (type) {
        case LOGIN_USER:
            state = { ...state, loading: true };
            break;
        case LOGIN_SUCCESS:
            state = { ...state, loading: false };
            break;
        case LOGOUT_USER:
            state = { ...state };
            break;
        case LOGOUT_USER_SUCCESS:
            state = { ...state };
            break;
        case API_ERROR:
            state = { ...state, error: payload, loading: false };
            break;
        default:
            state = { ...state };
            break;
    }
    return state;
};

export default loginReducer;
```

#### Initial State

- **error**: Holds any error message related to authentication.
- **loading**: Boolean indicating if the login request is in progress.

This reducer listens to dispatched actions and updates the state accordingly, particularly during login/logout operations.

---

## File: saga.js

This file contains the saga function that handles side effects related to user authentication using Redux-Saga.

### Saga Functionality

```javascript
import { put, takeEvery } from "redux-saga/effects";
import { LOGIN_USER } from "./actionTypes";
import { apiError } from "./actions";
import axios from "axios";

function* loginUser({ payload: { user, history } }) {
    try {
        const body = {
            email: user.email,
            password: user.password,
        };
        const url = process.env.REACT_APP_APIURL + "login/";
        const isProduction = process.env.REACT_APP_PRODUCTION === "true" ? true : false;
        let headers;
        if (!isProduction) {
            headers = {
                Authorization: `Bearer ${process.env.REACT_APP_CLIENTTOKEN}`,
                "Content-Type": "application/json",
            };
        }
        axios
            .post(url, body, { headers })
            .then((res) => {
                localStorage.setItem("authUser", JSON.stringify(res.data));
                history.push("/users");
            })
            .catch((err) => {
                put(apiError(err));
            });
    } catch (error) {
        yield put(apiError(error));
    }
}

function* authSaga() {
    yield takeEvery(LOGIN_USER, loginUser);
}

export default authSaga;
```

#### Key Points

- **`loginUser` Generator Function**: Handles the login process by making an API call. It uses Axios to send a POST request with user credentials. On success, it stores the `authUser` data in local storage and redirects the user. On failure, it dispatches an API error action.

- **`authSaga` Generator Function**: Watches for `LOGIN_USER` actions and triggers the `loginUser` function.

This saga ensures that side effects like API calls are managed efficiently and that asynchronous workflows are properly handled within the Redux environment.

---

This documentation provides a comprehensive overview of the files involved in managing authentication in a Redux-Saga setup, detailing each file's purpose and functionality in the authentication flow.

# Documentation for `reducer.js`

This document provides a comprehensive guide to the `reducer.js` file, which is a part of a Redux setup for managing authentication state in a React application.

## Overview 📄

In Redux, a **reducer** is a pure function that determines changes to an application's state. In this particular file, the reducer is responsible for handling state changes related to user authentication actions such as login, logout, and handling API errors. 

## Initial State 🌱

The reducer starts with the following initial state:

```javascript
const initialState = {
  error: "",
  loading: false,
}
```

- **error**: Stores any error messages that occur during the authentication process.
- **loading**: A boolean indicating whether an authentication request is in progress.

## Actions 🚀

The reducer responds to several action types defined in `actionTypes.js`:

- **LOGIN_USER**: Indicates a user login attempt. Sets `loading` to `true`.
- **LOGIN_SUCCESS**: Indicates a successful login. Sets `loading` to `false`.
- **LOGOUT_USER**: Indicates a user logout attempt.
- **LOGOUT_USER_SUCCESS**: Indicates a successful logout.
- **API_ERROR**: Captures any errors returned by the API. Sets `error` with the payload and `loading` to `false`.

## Reducer Function ⚙️

The main reducer function processes the incoming actions and updates the state accordingly:

```javascript
const login = (state = initialState, action) => {
  switch (action.type) {
    case LOGIN_USER:
      state = { ...state, loading: true }
      break

    case LOGIN_SUCCESS:
      state = { ...state, loading: false }
      break

    case LOGOUT_USER:
      state = { ...state }
      break

    case LOGOUT_USER_SUCCESS:
      state = { ...state }
      break

    case API_ERROR:
      state = { ...state, error: action.payload, loading: false }
      break

    default:
      state = { ...state }
      break
  }
  return state
}
```

### Breakdown

- **LOGIN_USER**: When this action is dispatched, the reducer sets `loading` to `true` indicating the start of a login process.
  
- **LOGIN_SUCCESS**: On successful login, this action resets `loading` to `false`.

- **LOGOUT_USER & LOGOUT_USER_SUCCESS**: These actions don't alter the state in this implementation but are placeholders for any potential state changes needed during logout.

- **API_ERROR**: This action captures error messages and stops the loading process by setting `loading` to `false`.

## Export 📤

The reducer is exported as the default export of the module:

```javascript
export default login
```

This allows it to be imported and used in the Redux store setup.

## Conclusion 🎯

The `reducer.js` file provides a simple yet crucial function in managing the authentication state within a Redux architecture. It ensures that the UI reflects the current authentication status and handles errors gracefully, providing a seamless user experience.

# 📄 Documentation for `scheduleReducer.js`

## Overview
The `scheduleReducer.js` file contains a reducer function specifically designed to manage the state associated with schedules. In Redux, reducers are pure functions that take the previous state and an action, and return the next state. This reducer handles actions related to scheduling lists, counts, and clearing the schedule data.

## Initial State
The reducer's initial state is defined with the following properties:
- **`schedule`**: An array to hold the list of schedule items.
- **`count`**: An integer that keeps track of the number of schedule items.

```javascript
const initialState = {
  schedule: [],
  count: 0,
};
```

## Action Types
This reducer responds to several action types. These types are defined in `actionTypes.js` and imported into this file:

| Action Type              | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `SET_SCHEDULE_LIST`      | Sets the list of schedules, sorted by ID.                                   |
| `SET_SCHEDULE_COUNT`     | Sets the count of schedules.                                                |
| `UPDATE_SCHEDULE_LIST`   | Updates the list of schedules based on the current count.                   |
| `SET_CLEAR_SCHEDULE_LIST`| Clears the schedule list and resets count to zero.                          |

## Reducer Function
The main function in this file is the `scheduleReducer` which updates the state based on the dispatched action:

```javascript
const scheduleReducer = (state = initialState, action) => {
  switch (action.type) {
    case SET_SCHEDULE_LIST:
      return {
        ...state,
        schedule: action === undefined ? [] : action.payload
          .sort((a, b) => a.id - b.id)
          .map(({ id, ...rest }) => ({ ...rest })),
      };

    case SET_SCHEDULE_COUNT:
      return {
        ...state,
        count: action.payload,
      };

    case UPDATE_SCHEDULE_LIST:
      return {
        ...state,
        schedule: [...state.schedule.slice(0, state.count)],
      };

    case SET_CLEAR_SCHEDULE_LIST:
      return {
        count: 0,
        schedule: [],
      };

    default:
      state = { ...state };
      break;
  }
  return state;
};
```

### Explanation of Cases:
- **`SET_SCHEDULE_LIST`**: This case sets the `schedule` state with a sorted list of schedules by `id`. It ensures that if `action` is undefined, the schedule list is an empty array.
  
- **`SET_SCHEDULE_COUNT`**: Updates the `count` state with the payload provided in the action.
  
- **`UPDATE_SCHEDULE_LIST`**: Limits the `schedule` array to the number of items specified by `count`, effectively "trimming" the list.
  
- **`SET_CLEAR_SCHEDULE_LIST`**: Resets both the `schedule` array and `count` to their initial empty or zero states.

## Export
The `scheduleReducer` function is exported as the default export from this module, allowing it to be easily integrated into the Redux store.

```javascript
export default scheduleReducer;
```

## Summary
The `scheduleReducer.js` file plays a crucial role in managing the state of schedules in an application, enabling features such as setting, updating, and clearing schedules based on dispatched actions. Its design ensures that the state transitions are predictable and maintainable.

# Documentation for `actions.js` 🚀

This file, `actions.js`, is a central part of a Redux setup that manages user profile actions. It defines several action creators related to editing user profiles. Each action has a specific type and payload that indicates the nature of the action being dispatched. Here's a detailed breakdown:

## Index
1. [Import Statements](#import-statements)
2. [Action Types](#action-types)
3. [Action Creators](#action-creators)
   - [editProfile](#editprofile)
   - [profileSuccess](#profilesuccess)
   - [profileError](#profileerror)
   - [resetProfileFlag](#resetprofileflag)

---

## Import Statements
```javascript
import { PROFILE_ERROR, PROFILE_SUCCESS, EDIT_PROFILE, RESET_PROFILE_FLAG } from "./actionTypes";
```
- **Purpose**: Import constants representing action types from `actionTypes.js`. These constants are used to define the type of actions that can be dispatched.

---

## Action Types
Action types are string constants that represent different actions that can occur in the application. They help in identifying the type of action being performed.

- **PROFILE_ERROR**: Represents an error in profile actions.
- **PROFILE_SUCCESS**: Indicates a successful profile-related operation.
- **EDIT_PROFILE**: Action to edit a user's profile.
- **RESET_PROFILE_FLAG**: Used to reset the profile flag in the state.

---

## Action Creators

Action creators are functions that create actions. They return an action, which is an object that typically contains a `type` and a `payload`.

### `editProfile` 🎨

```javascript
export const editProfile = user => {
  return {
    type: EDIT_PROFILE,
    payload: { user },
  };
};
```
- **Purpose**: To dispatch an action indicating that a user's profile is being edited.
- **Parameters**: 
  - `user`: The user object containing updated profile information.
- **Returns**: An action with `type` as `EDIT_PROFILE` and `payload` containing the `user` data.

### `profileSuccess` ✅

```javascript
export const profileSuccess = msg => {
  return {
    type: PROFILE_SUCCESS,
    payload: msg,
  };
};
```
- **Purpose**: To signal that a profile operation was successful.
- **Parameters**: 
  - `msg`: A success message.
- **Returns**: An action with `type` as `PROFILE_SUCCESS` and `payload` as the success message.

### `profileError` ❌

```javascript
export const profileError = error => {
  return {
    type: PROFILE_ERROR,
    payload: error,
  };
};
```
- **Purpose**: To handle errors occurring during profile operations.
- **Parameters**: 
  - `error`: The error message or object.
- **Returns**: An action with `type` as `PROFILE_ERROR` and `payload` containing the error.

### `resetProfileFlag` 🔄

```javascript
export const resetProfileFlag = () => {
  return {
    type: RESET_PROFILE_FLAG,
  };
};
```
- **Purpose**: To reset any flags related to profile actions, typically used after a success or error message has been displayed to the user.
- **Returns**: An action with `type` as `RESET_PROFILE_FLAG` and no payload.

---

These action creators are essential in managing state transitions related to user profiles in the application. They allow the application to respond to user interactions by dispatching specific actions that reducers will handle to update the state accordingly.

# Documentation for `actionTypes.js` 📜

This file defines **action types** for profile management in a Redux-based application. Action types are constants that represent the type of action to be performed. They are used to avoid typos and make the code more maintainable.

## 🗂️ Index

- [Overview](#overview)
- [Action Types](#action-types)
- [Usage](#usage)

## Overview

The `actionTypes.js` file is part of a Redux setup, focusing on **profile management** actions. This file exports string constants that are used as action types in Redux actions and reducers.

## Action Types

Here is a list of action types defined in this file:

| Action Type         | Description                                           |
|---------------------|-------------------------------------------------------|
| **`EDIT_PROFILE`**  | Represents the action of editing a user's profile.    |
| **`PROFILE_SUCCESS`** | Dispatched when a profile action succeeds.         |
| **`PROFILE_ERROR`**   | Dispatched when there is an error in profile action.|
| **`RESET_PROFILE_FLAG`** | Resets any profile-related status flags.        |

## Usage

```javascript
// Import action types
import { EDIT_PROFILE, PROFILE_SUCCESS, PROFILE_ERROR, RESET_PROFILE_FLAG } from "./actionTypes"

// Example usage in an action
export const editProfile = (user) => {
  return {
    type: EDIT_PROFILE,
    payload: { user },
  }
}
```

### Explanation

- **`EDIT_PROFILE`**: Used to trigger the process of editing a user profile.
- **`PROFILE_SUCCESS`**: Dispatched when a profile operation completes successfully.
- **`PROFILE_ERROR`**: Used when there is an error during profile operations.
- **`RESET_PROFILE_FLAG`**: This action type is used to reset flags that might indicate the state of profile operations, typically to clear success/error messages.

### 🚀 Benefits

- **Maintainability**: Centralizing action types allows for easy updates and management.
- **Error Reduction**: Reduces the risk of typos and errors in action names throughout the codebase.
- **Consistency**: Ensures that the same action names are used across different parts of the application, maintaining consistency.

By keeping action types in a dedicated file, developers can manage and reference action types easily, making the application more scalable and easier to debug.

# Documentation for `reducer.js`

Welcome to the documentation for the `reducer.js` file, which is an integral part of managing the state related to user profile updates in a Redux store. This documentation will guide you through the code, explaining its purpose and functionality in detail. 📝

## Table of Contents
1. [Overview](#overview)
2. [Initial State](#initial-state)
3. [Reducer Function](#reducer-function)
4. [Action Types](#action-types)
5. [State Management](#state-management)
6. [Export](#export)

---

## Overview

The `reducer.js` file is responsible for handling state transitions related to user profile actions in a Redux application. It listens to specific action types and updates the state accordingly.

## Initial State

The initial state is defined at the top of the file. It sets the default values for the state attributes related to user profile actions:

```javascript
const initialState = {
  error: "",
  success: "",
}
```

- **error**: Stores any error messages resulting from profile-related actions.
- **success**: Stores success messages confirming profile updates.

## Reducer Function

The core of this file is the `profile` reducer function. This function takes the current state and an action as arguments and returns a new state based on the action type:

```javascript
const profile = (state = initialState, action) => {
  switch (action.type) {
    case EDIT_PROFILE:
      state = { ...state }
      break
    case PROFILE_SUCCESS:
      state = { ...state, success: action.payload }
      break
    case PROFILE_ERROR:
      state = { ...state, error: action.payload }
      break
    case RESET_PROFILE_FLAG:
      state = { ...state, success: null }
      break
    default:
      state = { ...state }
      break
  }
  return state
}
```

## Action Types

The reducer function listens for several action types:

- **EDIT_PROFILE**: Triggered when a profile edit action is initiated.
- **PROFILE_SUCCESS**: Triggered when a profile edit action is successful. It updates the `success` state with a success message.
- **PROFILE_ERROR**: Triggered when a profile edit action fails. It updates the `error` state with an error message.
- **RESET_PROFILE_FLAG**: Resets the `success` state to `null`, effectively clearing the success message.

## State Management

The reducer handles the state transitions as follows:

- **EDIT_PROFILE**: Currently does not update the state, but it sets the stage for potential future enhancements.
- **PROFILE_SUCCESS**: Updates the `success` message in the state.
- **PROFILE_ERROR**: Updates the `error` message in the state.
- **RESET_PROFILE_FLAG**: Clears the `success` message by setting it to `null`.

## Export

Finally, the reducer function is exported as the default export of the module:

```javascript
export default profile
```

This allows the reducer to be integrated into the Redux store where it can handle profile-related state transitions.

---

This completes the documentation for the `reducer.js` file. This file plays a crucial role in managing user profile actions and ensuring that the application state is updated correctly in response to these actions. 🎉

# Documentation for Redux File Structures

This documentation provides a comprehensive explanation of the JavaScript files used in a Redux-based application. Each file plays a specific role in managing the state, actions, and side effects within the application. This documentation will cover various aspects including action types, action creators, reducers, and sagas, focusing on their functionality and usage.

## Index

1. **actionTypes.js**
2. **actions.js**
3. **reducer.js**
4. **saga.js**
5. **gameReducer.js**
6. **authSaga.js**
7. **loginReducer.js**
8. **prizeReducer.js**
9. **scheduleReducer.js**
10. **profile actions.js**
11. **profile actionTypes.js**
12. **profile reducer.js**
13. **profile saga.js**

---

## 1. actionTypes.js

This file declares constants for action types related to profile management. These constants are used to avoid errors due to typos in action type strings.

### Code Breakdown

```javascript
export const EDIT_PROFILE = "EDIT_PROFILE";
export const PROFILE_SUCCESS = "PROFILE_SUCCESS";
export const PROFILE_ERROR = "PROFILE_ERROR";
export const RESET_PROFILE_FLAG = "RESET_PROFILE_FLAG";
```

### Purpose

- **EDIT_PROFILE**: Initiates the profile editing process.
- **PROFILE_SUCCESS**: Indicates successful profile editing.
- **PROFILE_ERROR**: Represents a failed profile editing attempt.
- **RESET_PROFILE_FLAG**: Resets the profile success flag.

⚙️ Usage: These constants are imported wherever these actions need to be dispatched or handled, ensuring consistency across the application.

---

## 2. actions.js

This file defines action creator functions that dispatch actions related to profile management.

### Code Breakdown

```javascript
import {
  PROFILE_ERROR,
  PROFILE_SUCCESS,
  EDIT_PROFILE,
  RESET_PROFILE_FLAG,
} from "./actionTypes";

export const editProfile = user => {
  return {
    type: EDIT_PROFILE,
    payload: { user },
  };
};

export const profileSuccess = msg => {
  return {
    type: PROFILE_SUCCESS,
    payload: msg,
  };
};

export const profileError = error => {
  return {
    type: PROFILE_ERROR,
    payload: error,
  };
};

export const resetProfileFlag = () => {
  return {
    type: RESET_PROFILE_FLAG,
  };
};
```

### Purpose

- **editProfile**: Dispatches an action to edit a user's profile.
- **profileSuccess**: Dispatches an action when profile editing is successful.
- **profileError**: Dispatches an action when profile editing fails.
- **resetProfileFlag**: Dispatches an action to reset the profile success state.

🔗 These actions are typically used in conjunction with redux-saga to handle asynchronous operations.

---

## 3. reducer.js

This file defines a reducer function to manage the state related to profile operations.

### Code Breakdown

```javascript
import {
  PROFILE_ERROR,
  PROFILE_SUCCESS,
  EDIT_PROFILE,
  RESET_PROFILE_FLAG,
} from "./actionTypes";

const initialState = {
  error: "",
  success: "",
};

const profile = (state = initialState, action) => {
  switch (action.type) {
    case EDIT_PROFILE:
      state = { ...state };
      break;
    case PROFILE_SUCCESS:
      state = { ...state, success: action.payload };
      break;
    case PROFILE_ERROR:
      state = { ...state, error: action.payload };
      break;
    case RESET_PROFILE_FLAG:
      state = { ...state, success: null };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default profile;
```

### Purpose

- **Initial State**: Defines default values for `error` and `success`.
- **EDIT_PROFILE**: Maintains current state.
- **PROFILE_SUCCESS**: Updates the `success` message.
- **PROFILE_ERROR**: Updates the `error` message.
- **RESET_PROFILE_FLAG**: Resets the `success` message to `null`.

🔄 This reducer updates the state based on actions dispatched from the actions.js file.

---

## 4. saga.js

This file manages asynchronous operations related to profile editing using redux-saga.

### Code Breakdown

```javascript
import { takeEvery, fork, put, all, call } from "redux-saga/effects";
import { EDIT_PROFILE } from "./actionTypes";
import { profileSuccess, profileError } from "./actions";
import { getFirebaseBackend } from "../../../helpers/firebase_helper";
import { postFakeProfile, postJwtProfile } from "../../../helpers/fakebackend_helper";

const fireBaseBackend = getFirebaseBackend();

function* editProfile({ payload: { user } }) {
  try {
    if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
      const response = yield call(fireBaseBackend.editProfileAPI, user.username, user.idx);
      yield put(profileSuccess(response));
    } else if (process.env.REACT_APP_DEFAULTAUTH === "jwt") {
      const response = yield call(postJwtProfile, "/post-jwt-profile", { username: user.username, idx: user.idx });
      yield put(profileSuccess(response));
    } else if (process.env.REACT_APP_DEFAULTAUTH === "fake") {
      const response = yield call(postFakeProfile, { username: user.username, idx: user.idx });
      yield put(profileSuccess(response));
    }
  } catch (error) {
    yield put(profileError(error));
  }
}

export function* watchProfile() {
  yield takeEvery(EDIT_PROFILE, editProfile);
}

function* ProfileSaga() {
  yield all([fork(watchProfile)]);
}

export default ProfileSaga;
```

### Purpose

- **editProfile**: Handles asynchronous profile editing logic based on the authentication method (Firebase, JWT, or Fake).
- **watchProfile**: Watches for EDIT_PROFILE actions and triggers the editProfile saga.
- **ProfileSaga**: Combines all profile-related sagas for easier management.

🚀 This saga facilitates complex asynchronous operations and state updates in response to dispatched actions.

---

This documentation aims to provide clarity on how each component interacts within a Redux architecture in a React application. Each file has a unique role, contributing to efficient state management and enhancing the scalability of the application.

# Documentation for `actionTypes.js`

This **documentation** provides a detailed explanation of the `actionTypes.js` file, which is an essential part of managing action types in a Redux-based application. This file defines constants representing various action types used throughout the application to maintain consistent and error-free action dispatching. Below, we'll delve into the specifics of each action type defined in this file, focusing particularly on user registration.

## 🎯 Purpose

The `actionTypes.js` file acts as a central repository for all action type constants. By using constants, we avoid potential errors that can arise from typos in action type strings in action creators and reducers.

## 📜 Action Types Defined

Here's a list of action types included in this `actionTypes.js` file:

| Action Type Constant             | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| `REGISTER_USER`                  | 🚀 Dispatched when a user registration process is initiated.                 |
| `REGISTER_USER_SUCCESSFUL`       | ✅ Dispatched when a user registration completes successfully.               |
| `REGISTER_USER_FAILED`           | ❌ Dispatched when a user registration process fails.                        |

### Detailed Explanation

- **`REGISTER_USER`**: This action type is used to indicate the start of a user registration process. It is typically dispatched by an action creator when a user submits their registration details.

- **`REGISTER_USER_SUCCESSFUL`**: This action type is dispatched upon the successful completion of the user registration process. It may carry additional payload data such as user information or confirmation messages.

- **`REGISTER_USER_FAILED`**: This action type is dispatched if the user registration process fails for any reason. It usually carries payload data containing error messages or codes.

## 📚 Example Usage

These constants are used in action creators and reducers. Here's a simple example of how these might be used in an action creator:

```javascript
import { REGISTER_USER, REGISTER_USER_SUCCESSFUL, REGISTER_USER_FAILED } from './actionTypes';

// Action creator for registering a user
export const registerUser = (userData) => ({
    type: REGISTER_USER,
    payload: userData,
});

// Action creator for successful registration
export const registerUserSuccessful = (user) => ({
    type: REGISTER_USER_SUCCESSFUL,
    payload: user,
});

// Action creator for failed registration
export const registerUserFailed = (error) => ({
    type: REGISTER_USER_FAILED,
    payload: error,
});
```

## 🎉 Conclusion

The `actionTypes.js` file is a crucial component in a Redux application, ensuring that action types are consistent and reducing the risk of errors. By defining action types such as `REGISTER_USER`, `REGISTER_USER_SUCCESSFUL`, and `REGISTER_USER_FAILED`, this file supports a robust user registration process, providing clear paths for success and error handling. This approach enhances the maintainability and scalability of the application.

# Documentation for `actions.js`

Welcome to the documentation for the `actions.js` file. This file is a crucial part of the Redux architecture in your application. It defines a set of actions that manage the process of user registration. Actions in Redux are payloads of information that send data from your application to your Redux store. They are the only source of information for the store. Let's dive into the details of this file. 🚀

## Table of Contents

1. [Overview](#overview)
2. [Imports](#imports)
3. [Action Creators](#action-creators)
   - [registerUser](#registeruser)
   - [registerUserSuccessful](#registerusersuccessful)
   - [registerUserFailed](#registeruserfailed)

---

## Overview

The `actions.js` file is designed to handle the registration process of users. It exports three action creators:

- **registerUser**: Initiates the registration process.
- **registerUserSuccessful**: Dispatched when a user is successfully registered.
- **registerUserFailed**: Dispatched when the registration process fails.

## Imports

```javascript
import { REGISTER_USER, REGISTER_USER_SUCCESSFUL, REGISTER_USER_FAILED } from "./actionTypes";
```

This section imports the action types from the `actionTypes.js` file. These constants are used to define the types of actions that can be dispatched in the application.

## Action Creators

### registerUser

**Definition**: 

```javascript
export const registerUser = user => {
    return {
        type: REGISTER_USER,
        payload: { user },
    };
};
```

- **Purpose**: This action creator is used to initiate the registration process for a new user. It takes a `user` object as an argument.
- **Parameters**: 
  - `user`: An object containing user details required for registration.
- **Returns**: An action object with:
  - `type`: A constant `REGISTER_USER` that identifies the action.
  - `payload`: An object containing the `user` data.

### registerUserSuccessful

**Definition**:

```javascript
export const registerUserSuccessful = user => {
    return {
        type: REGISTER_USER_SUCCESSFUL,
        payload: user,
    };
};
```

- **Purpose**: This action is dispatched when a user is successfully registered.
- **Parameters**: 
  - `user`: An object containing the registered user details.
- **Returns**: An action object with:
  - `type`: A constant `REGISTER_USER_SUCCESSFUL`.
  - `payload`: The `user` data.

### registerUserFailed

**Definition**:

```javascript
export const registerUserFailed = user => {
    return {
        type: REGISTER_USER_FAILED,
        payload: user,
    };
};
```

- **Purpose**: This action is dispatched when there is an error in the registration process.
- **Parameters**: 
  - `user`: An object or message detailing the error.
- **Returns**: An action object with:
  - `type`: A constant `REGISTER_USER_FAILED`.
  - `payload`: The error information.

---

**Conclusion**: The `actions.js` file plays a pivotal role in the registration workflow of your application by defining clear and concise action creators. These actions facilitate communication between the user interface and the Redux store, ensuring that the state of the application is updated efficiently based on user interactions. 🎉

# Documentation for Account Module

## Table of Contents

1. [Overview](#overview)
2. [Code Structure](#code-structure)
3. [State Management](#state-management)
4. [Reducers](#reducers)
5. [Conclusion](#conclusion)

---

## Overview

The file `reducer.js` in this module is responsible for managing the state related to user registration within a Redux store. It handles different actions to update the Redux state during the user registration process.

---

## Code Structure

The `reducer.js` file is structured to manage the registration state of a user. It imports necessary action types from the `actionTypes.js` file and defines an initial state for registration.

```javascript
import { REGISTER_USER, REGISTER_USER_SUCCESSFUL, REGISTER_USER_FAILED } from "./actionTypes";

const initialState = {
  registrationError: null,
  message: null,
  loading: false,
  user: null,
};

const account = (state = initialState, action) => {
  switch (action.type) {
    case REGISTER_USER:
      state = {
        ...state,
        loading: true,
        registrationError: null,
      };
      break;
    case REGISTER_USER_SUCCESSFUL:
      state = {
        ...state,
        loading: false,
        user: action.payload,
        registrationError: null,
      };
      break;
    case REGISTER_USER_FAILED:
      state = {
        ...state,
        user: null,
        loading: false,
        registrationError: action.payload,
      };
      break;
    default:
      state = {
        ...state,
      };
      break;
  }
  return state;
};

export default account;
```

---

## State Management

The initial state is defined as:

- **`registrationError`**: Holds any error message that occurs during registration.
- **`message`**: Reserved for any messages that may be used (currently unused).
- **`loading`**: Boolean indicating if a registration operation is in progress.
- **`user`**: Holds user data upon successful registration.

---

## Reducers

### Action Handling

1. **`REGISTER_USER`**:
   - **Purpose**: Initiates user registration.
   - **State Changes**:
     - Sets `loading` to `true`.
     - Resets `registrationError` to `null`.

2. **`REGISTER_USER_SUCCESSFUL`**:
   - **Purpose**: Updates the state when user registration is successful.
   - **State Changes**:
     - Sets `loading` to `false`.
     - Updates `user` with the payload (user data).
     - Resets `registrationError` to `null`.

3. **`REGISTER_USER_FAILED`**:
   - **Purpose**: Updates the state when user registration fails.
   - **State Changes**:
     - Sets `user` to `null`.
     - Sets `loading` to `false`.
     - Updates `registrationError` with the payload (error message).

### Default Case

- Returns the current state when no action is matched.

---

## Conclusion

The `reducer.js` in this module is crucial for managing user registration states, providing a robust structure to handle user registration actions effectively. By updating the state based on dispatched actions, it ensures the UI reflects the current registration process, whether it is loading, successful, or failed. This reducer is a foundational piece in the user account management flow.

# Detailed Documentation for Redux Files

## 🎯 Introduction
This documentation provides an in-depth explanation of several Redux files concerning user authentication, profile editing, and game management. Each section covers a specific file, detailing its purpose, functionality, and how it interacts with other parts of the Redux architecture.

## 📑 Index
1. **actionTypes.js** - [Forget Password](#forget-password-actiontypes), [Authentication & Game](#auth-game-actiontypes), [Profile Editing](#profile-actiontypes), [User Registration](#register-actiontypes)
2. **actions.js** - [Forget Password](#forget-password-actions), [Authentication & Game](#auth-game-actions), [Profile Editing](#profile-actions), [User Registration](#register-actions)
3. **reducer.js** - [Forget Password](#forget-password-reducer), [Authentication & Game](#auth-game-reducer), [Profile Editing](#profile-reducer), [User Registration](#register-reducer)
4. **saga.js** - [Forget Password](#forget-password-saga), [Profile Editing](#profile-saga), [User Registration](#register-saga)
5. **gameReducer.js** - [Game Management](#game-reducer)
6. **prizeReducer.js** - [Prize Management](#prize-reducer)
7. **scheduleReducer.js** - [Schedule Management](#schedule-reducer)

## Forget Password actionTypes.js <a name="forget-password-actiontypes"></a>
This file defines action types for orchestrating the forget password functionality.

```javascript
export const FORGET_PASSWORD = "FORGET_PASSWORD";
export const FORGET_PASSWORD_SUCCESS = "FORGET_PASSWORD_SUCCESS";
export const FORGET_PASSWORD_ERROR = "FORGET_PASSWORD_ERROR";
```

| Action Type              | Description                                           |
|--------------------------|-------------------------------------------------------|
| `FORGET_PASSWORD`        | Initiates the forget password process.                |
| `FORGET_PASSWORD_SUCCESS`| Dispatched when the password reset link is sent.      |
| `FORGET_PASSWORD_ERROR`  | Dispatched when there's an error in the reset process.|

---

## Authentication & Game actionTypes.js <a name="auth-game-actiontypes"></a>
This file contains action types used for user login/logout and game state management.

```javascript
export const LOGIN_USER = "LOGIN_USER";
export const LOGIN_SUCCESS = "LOGIN_SUCCESS";
export const LOGOUT_USER = "LOGOUT_USER";
export const LOGOUT_USER_SUCCESS = "LOGOUT_USER_SUCCESS";
export const API_ERROR = "LOGIN_API_ERROR";
export const SOCIAL_LOGIN = "SOCIAL_LOGIN";
export const SET_GAMES = "SET_GAMES";
export const SET_PRIZE_LIST = "SET_PRIZE_LIST";
export const SET_CLEAR_PRIZE_LIST = "SET_CLEAR_PRIZE_LIST";
export const UPDATE_PRIZE_COUNT = "UPDATE_PRIZE_COUNT";
export const UPDATE_PRIZE_LIST = "UPDATE_PRIZE_LIST";
export const SET_SCHEDULE_LIST = "SET_SCHEDULE_LIST";
export const SET_SCHEDULE_COUNT = "SET_SCHEDULE_COUNT";
export const UPDATE_SCHEDULE_LIST = "UPDATE_SCHEDULE_LIST";
export const SET_CLEAR_SCHEDULE_LIST = "SET_CLEAR_SCHEDULE_LIST";
```

| Action Type                  | Description                                              |
|------------------------------|----------------------------------------------------------|
| `LOGIN_USER`                 | Starts the login process.                                |
| `LOGIN_SUCCESS`              | Dispatched when user login is successful.                |
| `LOGOUT_USER`                | Initiates the logout process.                            |
| `LOGOUT_USER_SUCCESS`        | Dispatched upon successful logout.                       |
| `API_ERROR`                  | Handles API errors.                                      |
| `SOCIAL_LOGIN`               | Manages social login actions.                            |
| `SET_GAMES`                  | Sets the list of games.                                  |
| `SET_PRIZE_LIST`             | Sets the prize list data.                                |
| `SET_CLEAR_PRIZE_LIST`       | Clears the prize list.                                   |
| `UPDATE_PRIZE_COUNT`         | Updates prize count.                                     |
| `UPDATE_PRIZE_LIST`          | Updates the list of prizes.                              |
| `SET_SCHEDULE_LIST`          | Sets the schedule list.                                  |
| `SET_SCHEDULE_COUNT`         | Updates the schedule count.                              |
| `UPDATE_SCHEDULE_LIST`       | Updates the schedule list.                               |
| `SET_CLEAR_SCHEDULE_LIST`    | Clears the schedule list.                                |

---

## Profile Editing actionTypes.js <a name="profile-actiontypes"></a>
Defines action types used for handling profile editing actions.

```javascript
export const EDIT_PROFILE = "EDIT_PROFILE";
export const PROFILE_SUCCESS = "PROFILE_SUCCESS";
export const PROFILE_ERROR = "PROFILE_ERROR";
export const RESET_PROFILE_FLAG = "RESET_PROFILE_FLAG";
```

| Action Type             | Description                                  |
|-------------------------|----------------------------------------------|
| `EDIT_PROFILE`          | Initiates the profile editing process.       |
| `PROFILE_SUCCESS`       | Dispatched when profile editing is successful.|
| `PROFILE_ERROR`         | Dispatched when there's an error in editing. |
| `RESET_PROFILE_FLAG`    | Resets the profile success/error flag.       |

---

## User Registration actionTypes.js <a name="register-actiontypes"></a>
Defines action types related to user registration.

```javascript
export const REGISTER_USER = "register_user";
export const REGISTER_USER_SUCCESSFUL = "register_user_successfull";
export const REGISTER_USER_FAILED = "register_user_failed";
```

| Action Type                      | Description                                      |
|----------------------------------|--------------------------------------------------|
| `REGISTER_USER`                  | Begins the user registration process.            |
| `REGISTER_USER_SUCCESSFUL`       | Dispatched when registration is successful.      |
| `REGISTER_USER_FAILED`           | Dispatched when registration fails.              |

---

## Forget Password actions.js <a name="forget-password-actions"></a>
Contains actions for initiating and handling the forget password process.

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";

export const userForgetPassword = (user, history) => {
  return {
    type: FORGET_PASSWORD,
    payload: { user, history },
  };
};

export const userForgetPasswordSuccess = (message) => {
  return {
    type: FORGET_PASSWORD_SUCCESS,
    payload: message,
  };
};

export const userForgetPasswordError = (message) => {
  return {
    type: FORGET_PASSWORD_ERROR,
    payload: message,
  };
};
```

| Action Creator                   | Description                                                                     |
|----------------------------------|---------------------------------------------------------------------------------|
| `userForgetPassword`             | Dispatches the forget password action with user details and history.            |
| `userForgetPasswordSuccess`      | Dispatches a success message when password reset link is sent.                  |
| `userForgetPasswordError`        | Dispatches an error message if the reset process fails.                         |

---

## Authentication & Game actions.js <a name="auth-game-actions"></a>
Defines actions for user authentication and game-related state.

```javascript
import { gamesToCategories } from "../../../helpers/util";
import { LOGIN_USER, LOGIN_SUCCESS, LOGOUT_USER, LOGOUT_USER_SUCCESS, API_ERROR, SOCIAL_LOGIN, SET_GAMES, SET_PRIZE_LIST, SET_SCHEDULE_LIST, SET_SCHEDULE_COUNT, SET_CLEAR_PRIZE_LIST, UPDATE_PRIZE_COUNT, UPDATE_PRIZE_LIST, UPDATE_SCHEDULE_LIST, SET_CLEAR_SCHEDULE_LIST } from "./actionTypes";

export const loginUser = (user, history) => {
  return { type: LOGIN_USER, payload: { user, history } };
};

export const loginSuccess = (user) => {
  return { type: LOGIN_SUCCESS, payload: user };
};

export const logoutUser = (history) => {
  return { type: LOGOUT_USER, payload: { history } };
};

export const logoutUserSuccess = () => {
  return { type: LOGOUT_USER_SUCCESS, payload: {} };
};

export const apiError = (error) => {
  return { type: API_ERROR, payload: error };
};

export const socialLogin = (data, history, type) => {
  return { type: SOCIAL_LOGIN, payload: { data, history, type } };
};

export const setGames = (data) => {
  return { type: SET_GAMES, payload: gamesToCategories(data) };
};

export const setPrizeList = (prizeList) => {
  return { type: SET_PRIZE_LIST, payload: prizeList };
};

export const setClearPrizeList = () => {
  return { type: SET_CLEAR_PRIZE_LIST, payload: {} };
};

export const updatePrizeCount = (prizeCount) => {
  return { type: UPDATE_PRIZE_COUNT, payload: prizeCount };
};

export const updatePrizeList = () => {
  return { type: UPDATE_PRIZE_LIST };
};

export const setScheduleList = (scheduleList) => {
  return { type: SET_SCHEDULE_LIST, payload: scheduleList };
};

export const setScheduleCount = (scheduleCount) => {
  return { type: SET_SCHEDULE_COUNT, payload: scheduleCount };
};

export const updateScheduleList = () => {
  return { type: UPDATE_SCHEDULE_LIST };
};

export const setClearScheduleList = () => {
  return { type: SET_CLEAR_SCHEDULE_LIST, payload: {} };
};
```

| Action Creator                   | Description                                                                     |
|----------------------------------|---------------------------------------------------------------------------------|
| `loginUser`                      | Initiates the login process for a user.                                         |
| `loginSuccess`                   | Handles successful login.                                                       |
| `logoutUser`                     | Initiates the logout process.                                                   |
| `logoutUserSuccess`              | Handles successful logout.                                                      |
| `apiError`                       | Handles API errors.                                                             |
| `socialLogin`                    | Initiates social login process.                                                 |
| `setGames`                       | Sets the list of available games.                                               |
| `setPrizeList`                   | Sets the prize list data.                                                       |
| `setClearPrizeList`              | Clears the prize list.                                                          |
| `updatePrizeCount`               | Updates the prize count in the state.                                           |
| `updatePrizeList`                | Updates the prize list based on count.                                          |
| `setScheduleList`                | Sets the schedule list data.                                                    |
| `setScheduleCount`               | Updates the count of scheduled items.                                           |
| `updateScheduleList`             | Updates the schedule list based on count.                                       |
| `setClearScheduleList`           | Clears the schedule list data.                                                  |

---

## Profile Editing actions.js <a name="profile-actions"></a>
Actions related to editing user profiles and handling errors.

```javascript
import { PROFILE_ERROR, PROFILE_SUCCESS, EDIT_PROFILE, RESET_PROFILE_FLAG } from "./actionTypes";

export const editProfile = (user) => {
  return { type: EDIT_PROFILE, payload: { user } };
};

export const profileSuccess = (msg) => {
  return { type: PROFILE_SUCCESS, payload: msg };
};

export const profileError = (error) => {
  return { type: PROFILE_ERROR, payload: error };
};

export const resetProfileFlag = () => {
  return { type: RESET_PROFILE_FLAG };
};
```

| Action Creator                   | Description                                |
|----------------------------------|--------------------------------------------|
| `editProfile`                    | Initiates the profile editing process.     |
| `profileSuccess`                 | Handles successful profile update.         |
| `profileError`                   | Handles profile update errors.             |
| `resetProfileFlag`               | Resets success/error flags for profile.    |

---

## User Registration actions.js <a name="register-actions"></a>
Actions for handling user registration and related errors.

```javascript
import { REGISTER_USER, REGISTER_USER_SUCCESSFUL, REGISTER_USER_FAILED } from "./actionTypes";

export const registerUser = (user) => {
  return { type: REGISTER_USER, payload: { user } };
};

export const registerUserSuccessful = (user) => {
  return { type: REGISTER_USER_SUCCESSFUL, payload: user };
};

export const registerUserFailed = (user) => {
  return { type: REGISTER_USER_FAILED, payload: user };
};
```

| Action Creator                   | Description                                  |
|----------------------------------|----------------------------------------------|
| `registerUser`                   | Initiates the user registration process.     |
| `registerUserSuccessful`         | Handles successful user registration.        |
| `registerUserFailed`             | Handles registration failures.               |

---

## Forget Password reducer.js <a name="forget-password-reducer"></a>
Reducer to manage the state of the forget password process.

```javascript
import { FORGET_PASSWORD, FORGET_PASSWORD_SUCCESS, FORGET_PASSWORD_ERROR } from "./actionTypes";

const initialState = {
  forgetSuccessMsg: null,
  forgetError: null,
};

const forgetPassword = (state = initialState, action) => {
  switch (action.type) {
    case FORGET_PASSWORD:
      state = { ...state, forgetSuccessMsg: null, forgetError: null };
      break;
    case FORGET_PASSWORD_SUCCESS:
      state = { ...state, forgetSuccessMsg: action.payload };
      break;
    case FORGET_PASSWORD_ERROR:
      state = { ...state, forgetError: action.payload };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default forgetPassword;
```

| State Property          | Description                                         |
|-------------------------|-----------------------------------------------------|
| `forgetSuccessMsg`      | Holds the success message for password reset.       |
| `forgetError`           | Holds error messages related to the reset process.  |

---

## Authentication & Game reducer.js <a name="auth-game-reducer"></a>
Reducer handling authentication state and game-related actions.

```javascript
import { LOGIN_USER, LOGIN_SUCCESS, LOGOUT_USER, LOGOUT_USER_SUCCESS, API_ERROR } from "./actionTypes";

const initialState = {
  error: "",
  loading: false,
};

const login = (state = initialState, action) => {
  switch (action.type) {
    case LOGIN_USER:
      state = { ...state, loading: true };
      break;
    case LOGIN_SUCCESS:
      state = { ...state, loading: false };
      break;
    case LOGOUT_USER:
      state = { ...state };
      break;
    case LOGOUT_USER_SUCCESS:
      state = { ...state };
      break;
    case API_ERROR:
      state = { ...state, error: action.payload, loading: false };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default login;
```

| State Property          | Description                              |
|-------------------------|------------------------------------------|
| `error`                 | Holds error messages for login actions.  |
| `loading`               | Indicates if a login/logout action is in progress. |

---

## Profile Editing reducer.js <a name="profile-reducer"></a>
Reducer to manage state for profile editing and associated errors.

```javascript
import { PROFILE_ERROR, PROFILE_SUCCESS, EDIT_PROFILE, RESET_PROFILE_FLAG } from "./actionTypes";

const initialState = {
  error: "",
  success: "",
};

const profile = (state = initialState, action) => {
  switch (action.type) {
    case EDIT_PROFILE:
      state = { ...state };
      break;
    case PROFILE_SUCCESS:
      state = { ...state, success: action.payload };
      break;
    case PROFILE_ERROR:
      state = { ...state, error: action.payload };
      break;
    case RESET_PROFILE_FLAG:
      state = { ...state, success: null };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default profile;
```

| State Property          | Description                              |
|-------------------------|------------------------------------------|
| `error`                 | Holds error messages for profile actions.|
| `success`               | Holds success messages for profile updates. |

---

## User Registration reducer.js <a name="register-reducer"></a>
Reducer to manage the state of user registration.

```javascript
import { REGISTER_USER, REGISTER_USER_SUCCESSFUL, REGISTER_USER_FAILED } from "./actionTypes";

const initialState = {
  registrationError: null,
  message: null,
  loading: false,
  user: null,
};

const account = (state = initialState, action) => {
  switch (action.type) {
    case REGISTER_USER:
      state = { ...state, loading: true, registrationError: null };
      break;
    case REGISTER_USER_SUCCESSFUL:
      state = { ...state, loading: false, user: action.payload, registrationError: null };
      break;
    case REGISTER_USER_FAILED:
      state = { ...state, user: null, loading: false, registrationError: action.payload };
      break;
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default account;
```

| State Property          | Description                                      |
|-------------------------|--------------------------------------------------|
| `registrationError`     | Holds error messages for registration attempts.  |
| `message`               | Holds success messages related to registration.  |
| `loading`               | Indicates if a registration action is in progress.|
| `user`                  | Stores the user data upon successful registration.|

---

## Forget Password saga.js <a name="forget-password-saga"></a>
Saga to handle asynchronous operations of the forget password process.

```javascript
import { takeEvery, fork, put, all, call } from "redux-saga/effects";
import { FORGET_PASSWORD } from "./actionTypes";
import { userForgetPasswordSuccess, userForgetPasswordError } from "./actions";
import { getFirebaseBackend } from "../../../helpers/firebase_helper";
import { postFakeForgetPwd, postJwtForgetPwd } from "../../../helpers/fakebackend_helper";

const fireBaseBackend = getFirebaseBackend();

function* forgetUser({ payload: { user, history } }) {
  try {
    if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
      const response = yield call(fireBaseBackend.forgetPassword, user.email);
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sent to your mailbox, check there first"));
      }
    } else if (process.env.REACT_APP_DEFAULTAUTH === "jwt") {
      const response = yield call(postJwtForgetPwd, "/jwt-forget-pwd", { email: user.email });
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sent to your mailbox, check there first"));
      }
    } else {
      const response = yield call(postFakeForgetPwd, "/fake-forget-pwd", { email: user.email });
      if (response) {
        yield put(userForgetPasswordSuccess("Reset link are sent to your mailbox, check there first"));
      }
    }
  } catch (error) {
    yield put(userForgetPasswordError(error));
  }
}

export function* watchUserPasswordForget() {
  yield takeEvery(FORGET_PASSWORD, forgetUser);
}

function* forgetPasswordSaga() {
  yield all([fork(watchUserPasswordForget)]);
}

export default forgetPasswordSaga;
```

| Function                 | Description                                                            |
|--------------------------|------------------------------------------------------------------------|
| `forgetUser`             | Handles forgetting password with different auth methods and dispatches success/error.|
| `watchUserPasswordForget`| Watches for `FORGET_PASSWORD` actions to invoke `forgetUser`.          |
| `forgetPasswordSaga`     | Combines all forget password related sagas.                            |

---

## Profile Editing saga.js <a name="profile-saga"></a>
Saga to manage asynchronous profile editing operations.

```javascript
import { takeEvery, fork, put, all, call } from "redux-saga/effects";
import { EDIT_PROFILE } from "./actionTypes";
import { profileSuccess, profileError } from "./actions";
import { getFirebaseBackend } from "../../../helpers/firebase_helper";
import { postFakeProfile, postJwtProfile } from "../../../helpers/fakebackend_helper";

const fireBaseBackend = getFirebaseBackend();

function* editProfile({ payload: { user } }) {
  try {
    if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
      const response = yield call(fireBaseBackend.editProfileAPI, user.username, user.idx);
      yield put(profileSuccess(response));
    } else if (process.env.REACT_APP_DEFAULTAUTH === "jwt") {
      const response = yield call(postJwtProfile, "/post-jwt-profile", { username: user.username, idx: user.idx });
      yield put(profileSuccess(response));
    } else if (process.env.REACT_APP_DEFAULTAUTH === "fake") {
      const response = yield call(postFakeProfile, { username: user.username, idx: user.idx });
      yield put(profileSuccess(response));
    }
  } catch (error) {
    yield put(profileError(error));
  }
}

export function* watchProfile() {
  yield takeEvery(EDIT_PROFILE, editProfile);
}

function* ProfileSaga() {
  yield all([fork(watchProfile)]);
}

export default ProfileSaga;
```

| Function                 | Description                                                            |
|--------------------------|------------------------------------------------------------------------|
| `editProfile`            | Manages profile editing via different auth methods and dispatches success/error.|
| `watchProfile`           | Watches for `EDIT_PROFILE` actions to invoke `editProfile`.            |
| `ProfileSaga`            | Combines all profile editing related sagas.                            |

---

## User Registration saga.js <a name="register-saga"></a>
Saga for handling asynchronous registration operations.

```javascript
import { takeEvery, fork, put, all, call } from "redux-saga/effects";
import { REGISTER_USER } from "./actionTypes";
import { registerUserSuccessful, registerUserFailed } from "./actions";
import { getFirebaseBackend } from "../../../helpers/firebase_helper";
import { postFakeRegister, postJwtRegister } from "../../../helpers/fakebackend_helper";

const fireBaseBackend = getFirebaseBackend();

function* registerUser({ payload: { user } }) {
  try {
    if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
      const response = yield call(fireBaseBackend.registerUser, user.email, user.password);
      yield put(registerUserSuccessful(response));
    } else if (process.env.REACT_APP_DEFAULTAUTH === "jwt") {
      const response = yield call(postJwtRegister, "/post-jwt-register", user);
      yield put(registerUserSuccessful(response));
    } else if (process.env.REACT_APP_DEFAULTAUTH === "fake") {
      const response = yield call(postFakeRegister, user);
      yield put(registerUserSuccessful(response));
    }
  } catch (error) {
    yield put(registerUserFailed(error));
  }
}

export function* watchUserRegister() {
  yield takeEvery(REGISTER_USER, registerUser);
}

function* accountSaga() {
  yield all([fork(watchUserRegister)]);
}

export default accountSaga;
```

| Function                 | Description                                                            |
|--------------------------|------------------------------------------------------------------------|
| `registerUser`           | Handles user registration with different auth methods and dispatches success/error.|
| `watchUserRegister`      | Watches for `REGISTER_USER` actions to invoke `registerUser`.          |
| `accountSaga`            | Combines all user registration related sagas.                          |

---

## Game Management gameReducer.js <a name="game-reducer"></a>
Reducer to manage the state of games.

```javascript
import { SET_GAMES } from "./actionTypes";

const initialState = {
  game: {
    ppkGames: [],
    killRaceGames: [],
    traditionalGames: [],
    allGames: [],
    modeObj: {},
  },
};

const gameReducer = (state = initialState, { type, payload } = {}) => {
  if (type === SET_GAMES) {
    return { ...state, game: payload };
  } else {
    return (state = { ...state });
  }
};

export default gameReducer;
```

| State Property          | Description                                 |
|-------------------------|---------------------------------------------|
| `game`                  | Stores different types of games and their configurations.|

---

## Prize Management prizeReducer.js <a name="prize-reducer"></a>
Reducer to handle the state of prize lists and counts.

```javascript
import { SET_PRIZE_LIST, SET_CLEAR_PRIZE_LIST, UPDATE_PRIZE_COUNT, UPDATE_PRIZE_LIST } from "./actionTypes";

const initialState = {
  prize: [],
  count: 0,
};

const prizeReducer = (state = initialState, action) => {
  switch (action.type) {
    case SET_PRIZE_LIST:
      return { ...state, prize: action === undefined ? [] : action.payload.map(({ positionLabel, ...rest }) => ({ ...rest })) };
    case UPDATE_PRIZE_COUNT:
      return { ...state, count: action.payload };
    case UPDATE_PRIZE_LIST:
      return { ...state, prize: [...state.prize.slice(0, state.count)] };
    case SET_CLEAR_PRIZE_LIST:
      return { count: 0, prize: [] };
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default prizeReducer;
```

| State Property          | Description                               |
|-------------------------|-------------------------------------------|
| `prize`                 | Stores the list of prizes.                |
| `count`                 | Holds the count of prizes.                |

---

## Schedule Management scheduleReducer.js <a name="schedule-reducer"></a>
Reducer for managing the state of schedules and their counts.

```javascript
import { SET_SCHEDULE_LIST, SET_SCHEDULE_COUNT, UPDATE_SCHEDULE_LIST, SET_CLEAR_SCHEDULE_LIST } from "./actionTypes";

const initialState = {
  schedule: [],
  count: 0,
};

const scheduleReducer = (state = initialState, action) => {
  switch (action.type) {
    case SET_SCHEDULE_LIST: {
      return {
        ...state,
        schedule: action === undefined ? [] : action.payload.sort((a, b) => a.id - b.id).map(({ id, ...rest }) => ({ ...rest })),
      };
    }
    case SET_SCHEDULE_COUNT: {
      return { ...state, count: action.payload };
    }
    case UPDATE_SCHEDULE_LIST:
      return { ...state, schedule: [...state.schedule.slice(0, state.count)] };
    case SET_CLEAR_SCHEDULE_LIST:
      return { count: 0, schedule: [] };
    default:
      state = { ...state };
      break;
  }
  return state;
};

export default scheduleReducer;
```

| State Property          | Description                               |
|-------------------------|-------------------------------------------|
| `schedule`              | Stores the list of scheduled items.       |
| `count`                 | Holds the count of scheduled items.       |

---

This documentation aims to provide clarity on the individual components of your Redux setup and how they integrate to create a cohesive application state management strategy. Each section is crafted to give you a better understanding of the purpose and functionality of the Redux files you are working with.