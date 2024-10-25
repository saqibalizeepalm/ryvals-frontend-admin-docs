# 📜 Actions.js Documentation

Welcome to the **comprehensive** documentation for the `actions.js` file in your project! This file is a crucial part of the Redux architecture used to manage the state of your application. Let's dive deep into what each function does and its significance. 

---

## 📑 Index

1. [Overview](#overview)
2. [Import Statements](#import-statements)
3. [Action Creators](#action-creators)
   - [changeLayout](#changelayout)
   - [changePreloader](#changepreloader)
   - [changeLayoutWidth](#changelayoutwidth)
   - [changeSidebarTheme](#changesidebartheme)
   - [changeSidebarType](#changesidebartype)
   - [changeTopbarTheme](#changetopbartheme)
   - [showRightSidebarAction](#showrightsidebaraction)
   - [showSidebar](#showsidebar)
   - [toggleLeftmenu](#toggleleftmenu)

---

## 🖥️ Overview

The `actions.js` file defines a series of action creators. In Redux, **actions** are payloads of information that send data from your application to your Redux store. They are the **only source of information** for the store.

---

## 📥 Import Statements

```javascript
import { CHANGE_LAYOUT, CHANGE_LAYOUT_WIDTH, CHANGE_SIDEBAR_THEME, CHANGE_SIDEBAR_TYPE, CHANGE_TOPBAR_THEME, SHOW_RIGHT_SIDEBAR, SHOW_SIDEBAR, CHANGE_PRELOADER, TOGGLE_LEFTMENU } from "./actionTypes";
```

- The above import statement brings in **action type constants** from the `actionTypes.js` file. These constants are used to define the type of action being created.

---

## 🛠️ Action Creators

### `changeLayout`

```javascript
export const changeLayout = layout => ({
  type: CHANGE_LAYOUT,
  payload: layout,
});
```

- **Purpose**: This action creator is used to change the layout of the application.
- **Parameters**: 
  - `layout`: The new layout to be applied.
- **Action Type**: `CHANGE_LAYOUT`

### `changePreloader`

```javascript
export const changePreloader = layout => ({
  type: CHANGE_PRELOADER,
  payload: layout,
});
```

- **Purpose**: Controls the appearance of a preloader during layout changes.
- **Parameters**: 
  - `layout`: Boolean or configuration for preloader state.
- **Action Type**: `CHANGE_PRELOADER`

### `changeLayoutWidth`

```javascript
export const changeLayoutWidth = width => ({
  type: CHANGE_LAYOUT_WIDTH,
  payload: width,
});
```

- **Purpose**: To change the width of the layout.
- **Parameters**: 
  - `width`: New width value.
- **Action Type**: `CHANGE_LAYOUT_WIDTH`

### `changeSidebarTheme`

```javascript
export const changeSidebarTheme = theme => ({
  type: CHANGE_SIDEBAR_THEME,
  payload: theme,
});
```

- **Purpose**: To change the theme of the sidebar.
- **Parameters**: 
  - `theme`: The new theme to be applied.
- **Action Type**: `CHANGE_SIDEBAR_THEME`

### `changeSidebarType`

```javascript
export const changeSidebarType = (sidebarType, isMobile) => {
  return {
    type: CHANGE_SIDEBAR_TYPE,
    payload: { sidebarType, isMobile },
  };
};
```

- **Purpose**: Changes the type of sidebar, particularly useful for responsive design.
- **Parameters**: 
  - `sidebarType`: The type of sidebar (e.g., "compact", "expanded").
  - `isMobile`: Boolean indicating if the change is for mobile view.
- **Action Type**: `CHANGE_SIDEBAR_TYPE`

### `changeTopbarTheme`

```javascript
export const changeTopbarTheme = topbarTheme => ({
  type: CHANGE_TOPBAR_THEME,
  payload: topbarTheme,
});
```

- **Purpose**: To change the theme of the topbar.
- **Parameters**: 
  - `topbarTheme`: The new theme for the topbar.
- **Action Type**: `CHANGE_TOPBAR_THEME`

### `showRightSidebarAction`

```javascript
export const showRightSidebarAction = isopen => ({
  type: SHOW_RIGHT_SIDEBAR,
  payload: isopen,
});
```

- **Purpose**: Toggles the visibility of the right sidebar.
- **Parameters**: 
  - `isopen`: Boolean indicating whether the sidebar should be shown.
- **Action Type**: `SHOW_RIGHT_SIDEBAR`

### `showSidebar`

```javascript
export const showSidebar = isopen => ({
  type: SHOW_SIDEBAR,
  payload: isopen,
});
```

- **Purpose**: Toggles the visibility of the main sidebar.
- **Parameters**: 
  - `isopen`: Boolean indicating whether the sidebar should be shown.
- **Action Type**: `SHOW_SIDEBAR`

### `toggleLeftmenu`

```javascript
export const toggleLeftmenu = isopen => ({
  type: TOGGLE_LEFTMENU,
  payload: isopen,
});
```

- **Purpose**: Toggles the opening of the left menu.
- **Parameters**: 
  - `isopen`: Boolean indicating whether the left menu should be open.
- **Action Type**: `TOGGLE_LEFTMENU`

---

## 🎨 Visual Summary

| **Action Creator**        | **Purpose**                                   | **Action Type**          |
|---------------------------|-----------------------------------------------|--------------------------|
| `changeLayout`            | Change the app layout                         | `CHANGE_LAYOUT`          |
| `changePreloader`         | Control preloader state                       | `CHANGE_PRELOADER`       |
| `changeLayoutWidth`       | Adjust the layout width                       | `CHANGE_LAYOUT_WIDTH`    |
| `changeSidebarTheme`      | Set a new sidebar theme                       | `CHANGE_SIDEBAR_THEME`   |
| `changeSidebarType`       | Modify sidebar type for responsiveness        | `CHANGE_SIDEBAR_TYPE`    |
| `changeTopbarTheme`       | Update topbar theme                           | `CHANGE_TOPBAR_THEME`    |
| `showRightSidebarAction`  | Toggle right sidebar visibility               | `SHOW_RIGHT_SIDEBAR`     |
| `showSidebar`             | Toggle main sidebar visibility                | `SHOW_SIDEBAR`           |
| `toggleLeftmenu`          | Toggle left menu state                        | `TOGGLE_LEFTMENU`        |

---

By using these actions, you can effectively manage various layout and design aspects of your application while maintaining a clean and structured codebase. 🛠️✨

# 📜 reducer.js Documentation

Welcome to the documentation for the **`reducer.js`** file! This file is a crucial piece of a Redux-based state management system, responsible for defining how the application's state changes in response to actions. Let's dive in and explore each part of the code! 🌟

## 🎯 Table of Contents

1. [Introduction](#introduction)
2. [Initial State](#initial-state)
3. [Reducer Function](#reducer-function)
4. [Action Handling](#action-handling)
5. [Exports](#exports)

## 🔍 Introduction

The **`reducer.js`** file utilizes Redux to manage the state of various UI components, specifically related to layout settings. It listens for dispatched actions and modifies the state accordingly to ensure consistent UI behavior throughout the application.

## 🛠️ Initial State

The **`INIT_STATE`** is an object that defines the initial state of the layout settings. It serves as the default state when the reducer is first invoked. Here's a breakdown of the properties within this initial state:

```javascript
const INIT_STATE = {
  layoutType: "vertical",
  layoutWidth: "fluid",
  leftSideBarTheme: "light",
  leftSideBarType: "default",
  topbarTheme: "colored",
  isPreloader: false,
  showRightSidebar: false,
  isMobile: false,
  showSidebar: true,
  leftMenu: false,
}
```

| Property            | Default Value | Description                                             |
|---------------------|---------------|---------------------------------------------------------|
| `layoutType`        | "vertical"    | Defines the layout orientation of the application.      |
| `layoutWidth`       | "fluid"       | Determines the width setting of the layout.             |
| `leftSideBarTheme`  | "light"       | Specifies the theme of the left sidebar.                |
| `leftSideBarType`   | "default"     | Sets the type or style of the left sidebar.             |
| `topbarTheme`       | "colored"     | Controls the theme of the top bar.                      |
| `isPreloader`       | false         | Indicates if the preloader is active.                   |
| `showRightSidebar`  | false         | Determines if the right sidebar is visible.             |
| `isMobile`          | false         | Flags if the application is viewed on a mobile device.  |
| `showSidebar`       | true          | Controls the visibility of the sidebar.                 |
| `leftMenu`          | false         | Indicates if the left menu is toggled on.               |

## 🔄 Reducer Function

The reducer function, `Layout`, is at the core of handling the state transitions. It takes two parameters: the current state and an action. Based on the action type, it returns a new state object.

```javascript
const Layout = (state = INIT_STATE, action) => {
  switch (action.type) {
    // Action handling goes here
    default: 
      return state;
  }
}
```

## 🔄 Action Handling

The reducer listens to various action types, defined in **`actionTypes.js`**, and updates the state accordingly. Below is a list of actions it handles:

- **`CHANGE_LAYOUT`**: Updates the `layoutType`.
- **`CHANGE_PRELOADER`**: Toggles the `isPreloader` status.
- **`CHANGE_LAYOUT_WIDTH`**: Modifies the `layoutWidth`.
- **`CHANGE_SIDEBAR_THEME`**: Updates the `leftSideBarTheme`.
- **`CHANGE_SIDEBAR_TYPE`**: Alters the `leftSideBarType`.
- **`CHANGE_TOPBAR_THEME`**: Adjusts the `topbarTheme`.
- **`SHOW_RIGHT_SIDEBAR`**: Toggles the `showRightSidebar`.
- **`SHOW_SIDEBAR`**: Sets the `showSidebar` visibility.
- **`TOGGLE_LEFTMENU`**: Changes the `leftMenu` status.

Each case updates the respective state property with the payload received from the action:

```javascript
case CHANGE_LAYOUT:
  return { ...state, layoutType: action.payload }
```

## 🛳️ Exports

Finally, the reducer is exported as a default export, allowing it to be integrated into the Redux store:

```javascript
export default Layout;
```

This export facilitates the connection between the reducer and the Redux store, ensuring the application's state is managed effectively.

---

With this documentation, you now have a comprehensive understanding of how the **`reducer.js`** file functions within the Redux architecture. 🎉 Feel free to explore and expand upon this knowledge as you develop your application! 🚀

# 📜 `layoutReducer.js` Documentation

Welcome to the detailed documentation for the **`layoutReducer.js`** file. This file is a crucial part of managing the layout state in a Redux store for a JavaScript application. It is designed to handle various actions that dictate the appearance and behavior of the application's layout.

## 🎯 Purpose

The main purpose of **`layoutReducer.js`** is to define a Redux reducer that manages the state related to the layout of the application. This includes properties like layout type, sidebar theme, sidebar type, topbar theme, and others. The reducer listens to actions dispatched from the application and updates the state accordingly.

## 📁 File Contents

### Import Statements

```javascript
import { CHANGE_LAYOUT, CHANGE_LAYOUT_WIDTH, CHANGE_SIDEBAR_THEME, CHANGE_SIDEBAR_TYPE, CHANGE_TOPBAR_THEME, SHOW_RIGHT_SIDEBAR, CHANGE_PRELOADER, TOGGLE_LEFTMENU, SHOW_SIDEBAR, } from "./actionTypes";
```

- This line imports constants from `actionTypes.js`, which represent the different actions that can be dispatched to the reducer.

### Initial State

```javascript
const initialState = {
  layoutType: "vertical",
  layoutWidth: "fluid",
  leftSideBarTheme: "light",
  leftSideBarType: "default",
  topbarTheme: "colored",
  isPreloader: false,
  showRightSidebar: false,
  isMobile: false,
  showSidebar: true,
  leftMenu: false,
};
```

- The `initialState` object defines the default layout settings of the application. This state serves as the starting point and baseline for any future state modifications.

### The Reducer Function

```javascript
const layoutReducer = (state = initialState, { type, payload } = {}) => {
  switch (type) {
    case CHANGE_LAYOUT:
      return { ...state, layoutType: payload };
    case CHANGE_PRELOADER:
      return { ...state, isPreloader: payload };
    case CHANGE_LAYOUT_WIDTH:
      return { ...state, layoutWidth: payload };
    case CHANGE_SIDEBAR_THEME:
      return { ...state, leftSideBarTheme: payload };
    case CHANGE_SIDEBAR_TYPE:
      return { ...state, leftSideBarType: payload.sidebarType };
    case CHANGE_TOPBAR_THEME:
      return { ...state, topbarTheme: payload };
    case SHOW_RIGHT_SIDEBAR:
      return { ...state, showRightSidebar: payload };
    case SHOW_SIDEBAR:
      return { ...state, showSidebar: payload };
    case TOGGLE_LEFTMENU:
      return { ...state, leftMenu: payload };
    default:
      return state;
  }
};
```

- **Parameters**:
  - `state`: Represents the current state of the layout. Defaults to `initialState` if no state is provided.
  - `type`: The action type, which is one of the constants imported from `actionTypes.js`.
  - `payload`: The data associated with the action, used to update the state.

- **Functionality**:
  - This function uses a `switch` statement to determine which action type is being dispatched.
  - For each case, the reducer returns a new state object with updated properties based on the `payload` of the action.
  - If the action type does not match any case, the default behavior is to return the current state unchanged.

### Export Statement

```javascript
export default layoutReducer;
```

- This line exports the `layoutReducer` function as the default export from the file, making it available for import in other parts of the application.

## 📊 State Properties

Here's a quick table of the properties managed by the `layoutReducer`:

| Property          | Description                                                   | Initial Value |
|-------------------|---------------------------------------------------------------|---------------|
| `layoutType`      | Determines the layout orientation (e.g., vertical, horizontal)| `"vertical"`  |
| `layoutWidth`     | Controls the width of the layout (e.g., fluid, boxed)         | `"fluid"`     |
| `leftSideBarTheme`| Theme of the left sidebar                                     | `"light"`     |
| `leftSideBarType` | Type of the left sidebar (e.g., default, compact)             | `"default"`   |
| `topbarTheme`     | Theme of the top bar                                          | `"colored"`   |
| `isPreloader`     | Indicates if a preloader should be displayed                  | `false`       |
| `showRightSidebar`| Determines if the right sidebar is visible                    | `false`       |
| `isMobile`        | Flags if the application is within a mobile view             | `false`       |
| `showSidebar`     | Controls the visibility of the sidebar                        | `true`        |
| `leftMenu`        | Determines if the left menu is toggled                        | `false`       |

## 📚 Conclusion

The **`layoutReducer.js`** file is a critical component for managing the layout state in a Redux application. By handling various layout-related actions and updating the state accordingly, it provides a centralized way to control the appearance and behavior of the application's user interface.

Feel free to explore and modify the reducer to fit your application's specific requirements! 🎨👩‍💻

# 📜 Documentation for `saga.js`

This documentation provides a detailed explanation of the `saga.js` file, which is crucial for handling side effects in a Redux application using Redux-Saga. The file is responsible for managing layout settings and other UI components by listening to actions and executing asynchronous tasks.

---

## 📑 **Index**

1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Utility Functions](#utility-functions)
4. [Saga Functions](#saga-functions)
5. [Watchers](#watchers)
6. [Root Saga](#root-saga)

---

## 🎯 **Overview**

The `saga.js` file uses Redux-Saga to handle side effects in a Redux application. It listens for specific action types related to layout changes and performs tasks such as updating the body attributes and managing CSS classes.

---

## 📦 **Dependencies**

The file imports several functions and constants necessary for its operations:

```javascript
import { all, call, fork, takeEvery, put } from "redux-saga/effects";
import { CHANGE_LAYOUT, CHANGE_LAYOUT_WIDTH, CHANGE_SIDEBAR_THEME, CHANGE_SIDEBAR_TYPE, CHANGE_TOPBAR_THEME, SHOW_RIGHT_SIDEBAR } from "./actionTypes";
import { changeSidebarType as changeSidebarTypeAction, changeTopbarTheme as changeTopbarThemeAction } from "./actions";
```

- **Redux-Saga Effects**:
  - `all`, `call`, `fork`, `takeEvery`, `put`: Used to manage and orchestrate functions.
- **Action Types**:
  - Imported from `actionTypes.js` to trigger specific sagas.
- **Action Creators**:
  - Functions from `actions.js` are used to dispatch new actions.

---

## 🔧 **Utility Functions**

These functions are used internally to manipulate the document body attributes and classes:

### `changeBodyAttribute`

```javascript
function changeBodyAttribute(attribute, value) {
  if (document.body) document.body.setAttribute(attribute, value);
  return true;
}
```

- **Purpose**: Sets a specific attribute on the document body.

### `manageBodyClass`

```javascript
function manageBodyClass(cssClass, action = "toggle") {
  switch (action) {
    case "add":
      if (document.body) document.body.classList.add(cssClass);
      break;
    case "remove":
      if (document.body) document.body.classList.remove(cssClass);
      break;
    default:
      if (document.body) document.body.classList.toggle(cssClass);
      break;
  }
  return true;
}
```

- **Purpose**: Adds, removes, or toggles a CSS class on the document body.

---

## 🚀 **Saga Functions**

### `changeLayout`

```javascript
function* changeLayout({ payload: layout }) {
  try {
    if (layout === "horizontal") {
      yield put(changeTopbarThemeAction("colored"));
      document.body.removeAttribute("data-sidebar");
      yield call(manageBodyClass, "vertical-collpsed", "remove");
      document.body.removeAttribute("data-sidebar-size");
    } else {
      yield put(changeTopbarThemeAction("colored"));
    }
    yield call(changeBodyAttribute, "data-layout", layout);
  } catch (error) {
    // Handle error
  }
}
```

- **Description**: Manages layout changes and updates related body attributes and classes.

### `changeLayoutWidth`

```javascript
function* changeLayoutWidth({ payload: width }) {
  try {
    if (width === "boxed") {
      yield put(changeSidebarTypeAction("icon"));
      yield call(changeBodyAttribute, "data-layout-size", width);
      yield call(changeBodyAttribute, "data-layout-scrollable", false);
    } else if (width === "scrollable") {
      yield put(changeSidebarTypeAction("default"));
      yield call(changeBodyAttribute, "data-layout-scrollable", true);
    } else {
      yield put(changeSidebarTypeAction("default"));
      yield call(changeBodyAttribute, "data-layout-size", width);
      yield call(changeBodyAttribute, "data-layout-scrollable", false);
    }
  } catch (error) {
    // Handle error
  }
}
```

- **Description**: Adjusts the layout width and updates body attributes accordingly.

### Other Saga Functions

- `changeLeftSidebarTheme`
- `changeTopbarTheme`
- `changeLeftSidebarType`
- `showRightSidebar`

These functions handle their respective responsibilities by updating the document's body attributes and classes.

---

## 👀 **Watchers**

Watchers listen for dispatched actions and trigger the corresponding saga function:

- `watchChangeLayoutType`
- `watchChangeLayoutWidth`
- `watchChangeLeftSidebarTheme`
- `watchChangeLeftSidebarType`
- `watchChangeTopbarTheme`
- `watchShowRightSidebar`

Each of these functions uses `takeEvery` to listen for specific action types and run the associated saga.

---

## 🌐 **Root Saga**

The `LayoutSaga` is the root saga that combines all watcher sagas:

```javascript
function* LayoutSaga() {
  yield all([
    fork(watchChangeLayoutType),
    fork(watchChangeLayoutWidth),
    fork(watchChangeLeftSidebarTheme),
    fork(watchChangeLeftSidebarType),
    fork(watchShowRightSidebar),
    fork(watchChangeTopbarTheme),
  ]);
}

export default LayoutSaga;
```

- **Description**: Initializes all the watchers to ensure they listen for actions continuously.

---

This documentation provides a comprehensive look into the `saga.js` file, demonstrating how it efficiently manages layout-related side effects using Redux-Saga. Each function and saga is designed to handle specific UI changes, ensuring a responsive and dynamic user interface.

# Documentation for `actionTypes.js` 📄

Welcome to the documentation for the `actionTypes.js` file! This file plays a crucial role in managing the **action types** in a Redux-based application. It defines a set of constants that represent different actions related to layout management. These constants are used to ensure that action names are consistent throughout the application, reducing the likelihood of errors due to typos and making the codebase easier to maintain and refactor.

---

## Table of Contents 📑

1. [Overview](#overview)
2. [Action Types](#action-types)
3. [Usage](#usage)
4. [Conclusion](#conclusion)

---

## Overview 🌟

The `actionTypes.js` file is part of a **Redux** architecture, which is a predictable state container for JavaScript applications. The primary purpose of this file is to declare string constants used as action types in Redux actions and reducers. By centralizing these constants, it allows the developer to manage changes to the action names efficiently.

---

## Action Types 🎬

Below is the list of action types defined in the `actionTypes.js` file, along with their descriptions:

| **Constant Name**              | **Description**                                                                                                                                  |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `CHANGE_LAYOUT`               | Represents an action to change the overall **layout** of the application.                                                                        |
| `CHANGE_LAYOUT_WIDTH`         | Corresponds to an action that changes the **layout width** (e.g., full width or boxed).                                                          |
| `CHANGE_SIDEBAR_THEME`        | Used for changing the **theme** of the sidebar (e.g., light or dark theme).                                                                      |
| `CHANGE_SIDEBAR_TYPE`         | Pertains to an action that changes the type/style of sidebar (e.g., default or compact).                                                         |
| `CHANGE_TOPBAR_THEME`         | Represents an action to change the **theme** of the topbar.                                                                                      |
| `SHOW_SIDEBAR`                | Used to control the visibility of the **sidebar**.                                                                                               |
| `TOGGLE_LEFTMENU`             | Represents an action to toggle the left menu, potentially opening or closing it based on its current state.                                      |
| `SHOW_RIGHT_SIDEBAR`          | Used for controlling the display of the **right sidebar**.                                                                                       |
| `CHANGE_PRELOADER`            | Corresponds to an action that modifies the state of a **preloader**, likely shown during asynchronous operations.                                 |

---

## Usage 🚀

These action types are typically used in Redux **actions** and **reducers**. Here is an example of how one might use these constants in an action creator and a reducer:

### Example of an Action Creator

```javascript
import { CHANGE_LAYOUT } from './actionTypes';

// Action creator to change layout
export const changeLayout = (layout) => ({
  type: CHANGE_LAYOUT,
  payload: layout,
});
```

### Example of a Reducer

```javascript
import { CHANGE_LAYOUT } from './actionTypes';

const initialState = {
  layout: 'default',
};

const layoutReducer = (state = initialState, action) => {
  switch (action.type) {
    case CHANGE_LAYOUT:
      return {
        ...state,
        layout: action.payload,
      };
    default:
      return state;
  }
};

export default layoutReducer;
```

In these examples, `CHANGE_LAYOUT` is used to trigger changes in the application's layout. The action creator `changeLayout` dispatches an action with a payload specifying the new layout, and the `layoutReducer` updates the state accordingly.

---

## Conclusion 🎉

The `actionTypes.js` file is a fundamental part of the Redux setup in your application. By defining action types as constants, it helps maintain consistency across the codebase, making it easier to manage and scale. Understanding and using these action types effectively can significantly enhance the maintainability and readability of your Redux-based application.

Feel free to dive into the other parts of the codebase and see how these action types interact with other components and reducers to build a cohesive application!