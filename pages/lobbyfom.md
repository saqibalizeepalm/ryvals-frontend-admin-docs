# 📄 Documentation for `data.js`

Welcome to the documentation for the `data.js` file! This file is a module that exports various constants and utility functions tailored for managing lobby modes, game types, and additional operations in a gaming context. Let's dive into the details!

## 📋 Index

1. [Constants](#constants)
   - [Lobby Modes](#lobby-modes)
   - [Call of Duty Warzone Lobby Modes](#cod-warzone-lobby-modes)
   - [Lobby Mode Map](#lobby-mode-map)
   - [Lobby Result Map](#lobby-result-map)
   - [Game Types](#game-types)
   - [Game Type Map](#game-type-map)
2. [Utility Functions](#utility-functions)
   - [Convert Time 12 to 24 Hours](#convert-time-12-to-24)
   - [Remove Not Valid Keys for Comparison](#remove-not-valid-keys-for-comparison)
   - [Parse Integer Keys for Comparison](#parse-integer-keys-for-comparison)
   - [Trim Object Keys for Comparison](#trim-object-keys-for-comparison)

---

## 1. Constants

### 🎮 Lobby Modes

This constant is an array of objects representing different modes available in a lobby, each with a label and a corresponding value.

```javascript
export const LobbyMode = [
  { label: "Solo", value: 1 },
  { label: "Duo", value: 2 },
  { label: "Trio", value: 3 },
  { label: "Quad", value: 4 },
  { label: "Penta", value: 5 },
];
```

### 🎮 Call of Duty Warzone Lobby Modes

A specialized array for Call of Duty Warzone, supporting only limited modes.

```javascript
export const LobbyModeForCODWarzone = [
  { label: "Solo", value: 1 },
  { label: "Duo", value: 2 },
];
```

### 🗺️ Lobby Mode Map

A mapping of lobby mode values to detailed information about each mode.

```javascript
export const LobbyModeMap = {
  1: { label: "Solo", value: 1 },
  2: { label: "Duo", value: 2 },
  3: { label: "Trio", value: 3 },
  4: { label: "Quad", value: 4 },
  5: { label: "Penta", value: 5 },
};
```

### 🗺️ Lobby Result Map

Defines various states a lobby can be in, from "New" to "Cancelled".

```javascript
export const LobbyResultMap = {
  1: { label: "New", value: 1 },
  2: { label: "Uploaded", value: 2 },
  3: { label: "Ready", value: 3 },
  4: { label: "Published", value: 4 },
  5: { label: "Cancelled", value: 5 },
};
```

### 🎲 Game Types

An array representing different game types available.

```javascript
export const GameType = [
  { label: "PPK", value: 1 },
  { label: "Kill Race", value: 2 },
  { label: "Traditional", value: 3 },
];
```

### 🗺️ Game Type Map

A map providing detailed information on each game type.

```javascript
export const GameTypeMap = {
  1: { label: "PPK", value: 1 },
  2: { label: "Kill Race", value: 2 },
  3: { label: "Traditional", value: 3 },
};
```

---

## 2. Utility Functions

### 🕒 Convert Time 12 to 24 Hours

Converts a time string from 12-hour format (AM/PM) to 24-hour format.

```javascript
export const convertTime12To24 = (timeInAmPm) => {
  if (!timeInAmPm) return;
  const time = timeInAmPm.split(" ")[0] + " " + timeInAmPm.split(" ")[1];
  var hours = Number(time.match(/^(\d+)/)[1]);
  var minutes = Number(time.match(/:(\d+)/)[1]);
  var AMPM = time.match(/\s(.*)$/)[1];
  if (AMPM === "PM" && hours < 12) hours = hours + 12;
  if (AMPM === "AM" && hours === 12) hours = hours - 12;
  var sHours = hours.toString();
  var sMinutes = minutes.toString();
  if (hours < 10) sHours = "0" + sHours;
  if (minutes < 10) sMinutes = "0" + sMinutes;
  return sHours + ":" + sMinutes;
};
```

### 🗑️ Remove Not Valid Keys for Comparison

Removes specific keys from objects to prepare them for comparison.

```javascript
export const removeNotValidKeysForComparison = (obj1, obj2) => {
  let tempObj = { obj1 };
  let refTempObj = { obj2 };
  delete tempObj?.obj1?.gameNew;
  delete tempObj?.obj1?.game?.rules;
  delete tempObj?.obj1?.game?.min_players;
  delete tempObj?.obj1?.game?.max_players;
  delete tempObj?.obj1?.optionGroup;
  delete tempObj?.obj1?.editSubmitDisable;
  delete tempObj?.obj1?.admins;
  delete refTempObj?.obj2?.optionGroup;
  delete refTempObj?.obj2?.gameNew;
  delete refTempObj?.obj2?.editSubmitDisable;
  delete refTempObj?.obj2?.admins;
};
```

### 🔢 Parse Integer Keys for Comparison

Converts certain keys in an object to integers to facilitate accurate comparisons.

```javascript
export const parseIntKeysForCompare = (obj) => {
  obj["maxPlayer"] = parseInt(obj["maxPlayer"]);
  obj["minPlayer"] = parseInt(obj["minPlayer"]);
  obj["entryFee"] = parseInt(obj["entryFee"]);
};
```

### ✂️ Trim Object Keys for Comparison

Trims whitespace from specific string keys in an object.

```javascript
export const trimObjectKeysForCompare = (obj) => {
  obj.stats_code = obj?.stats_code?.trim();
  obj.participant_code = obj?.participant_code?.trim();
  obj.admin_code = obj?.admin_code?.trim();
  obj.name = obj?.name?.trim();
};
```

---

## 🎉 Summary

The `data.js` file is an essential component for defining game lobby modes, game types, and providing utility functions that help manage and compare game-related data effectively. The rich set of constants and utility functions make it a versatile tool for game management systems.

# 📄 LobbyForm.js Documentation

This document provides comprehensive details on the **LobbyForm.js** file, which is a React component for managing the creation and editing of game lobbies. This component is part of a larger application that deals with gaming lobbies, offering functionalities such as form validation, data handling, and interaction with APIs.

## 📚 Index

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Overview](#component-overview)
4. [State Management](#state-management)
5. [Lifecycle Methods](#lifecycle-methods)
6. [Event Handlers](#event-handlers)
7. [Render Method](#render-method)
8. [Connected Redux State](#connected-redux-state)
9. [Utility Functions](#utility-functions)
10. [Conclusion](#conclusion)

## 📜 Introduction

**LobbyForm.js** is a React component managing the user interface for adding and editing game lobbies. It provides various form fields for lobby settings, integrates with several APIs for data retrieval, and manages state transitions effectively. It uses libraries such as `reactstrap`, `react-select`, and `react-flatpickr` for UI components and date handling.

## 📦 Dependencies

The component leverages several external libraries and internal modules:

| Dependency | Description |
|------------|-------------|
| `React` | Core library for building UI components. |
| `reactstrap` | Provides Bootstrap 4 components as React components. |
| `react-select` | Flexible select input control for React. |
| `react-flatpickr` | A lightweight datepicker component. |
| `react-toastify` | For displaying toast notifications. |
| `lodash` | A utility library providing functions for common programming tasks. |
| `react-router-dom` | For navigation and routing in React components. |
| `react-redux` | Official React bindings for Redux to connect component with the Redux store. |

## 📖 Component Overview

### Import Statements

```javascript
import React from "react";
import { Row, Col, Card, CardBody, FormGroup, Button, Label, InputGroup } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import Select from "react-select";
import Flatpickr from "react-flatpickr";
import { Link, withRouter } from "react-router-dom";
import { connect } from "react-redux";
import { toast } from "react-toastify";
import { cloneDeep, isEmpty, isEqual } from "lodash";
import { addLobby, getLobbyDetail, editLobby } from "../../services/lobby_api_helper";
import { getAdminUserListLobby } from "../../services/admin_user_api_helper";
import { convertTime12To24, parseIntKeysForCompare, removeNotValidKeysForComparison, trimObjectKeysForCompare } from "./data";
import Loader from "../../components/Common/Loader";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getGlobalSettings } from "../../services/globalSettings_api_helper";
import { canEditLobbyField, gameTypeFilters, getModeLabelsSelect, randomPasswordGenerator, passwordCharacterData } from "../../helpers/util";
import EditorToolbar from "../CMS/EditorToolbar";
import ReactQuill from "react-quill";
import Switch from "react-switch";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css";
import "flatpickr/dist/themes/material_blue.css";
import "react-quill/dist/quill.snow.css";
```

### Class Component

The `LobbyForm` component is a class-based React component extending `React.Component`.

## 🧠 State Management

### State Variables

The component's state holds various properties essential for form data, UI state, and logic flow:

- **isLoading**: A boolean to show or hide the loader.
- **editMode**: Determines if the form is in edit mode.
- **lobbyId**: Stores the ID of the lobby being edited.
- **optionGroup**: List of options for games or modes.
- **errorMsg**: Stores error messages for display.
- **gameNew**: Tracks the newly selected game.
- **gameTypeMode**: Holds the selected game type.
- **minPlayer, maxPlayer**: For managing player limits.
- **startDate, startTime, endTime**: Handles date and time for the lobby.
- **rules**: Stores the game rules entered by the user.
- **admin_id**: Tracks the selected admin.
- **isPasswordProtected**: Boolean to toggle password protection.
- **displayRules**: Raw HTML content for rules.
  
...and many more, ensuring comprehensive control of form inputs and logic.

## ⏳ Lifecycle Methods

- **constructor**: Initializes state and binds event handlers.
- **componentDidMount**: Fetches initial data like admin list and global settings.
- **componentDidUpdate**: Responds to changes in props or state to trigger methods like `subtractMinutesModeChange`.

## 🔧 Event Handlers

The component includes numerous event handlers to manage form interactions:

- **handleChange**: Handles changes to form fields.
- **handleValidSubmit**: Logic for submitting valid form data.
- **handleInvalidSubmit**: Handles form submission errors.
- **handleSelectGroup**: Updates state on game selection changes.
- **handleAdminSelectGroup**: Updates state when an admin is selected.
  
...and more to provide a seamless form input experience.

## 🖼 Render Method

The `render` method builds the UI structure using JSX:

- Utilizes `AvForm` and `AvField` for form validation.
- Includes interactive elements like `Select` for dropdowns, `Flatpickr` for date/time input, and `Switch` for toggle inputs.
- Provides buttons for actions like "Submit" and "Generate Password".
- Integrates `Loader` for asynchronous operations and `Breadcrumbs` for navigation.

## 🔗 Connected Redux State

The component connects to the Redux store to access the global `game` state:

```javascript
const mapStateToProps = (state) => {
    const newGameObj = { ...state.Games?.game, modeObj: { ...state.Games?.game.modeObj } };
    return { game: newGameObj };
};

export default withRouter(connect(mapStateToProps)(LobbyForm));
```

## 🛠 Utility Functions

The component imports and utilizes several utility functions from `data.js` and other helper files:

- **convertTime12To24**: Converts 12-hour time format to 24-hour format.
- **parseIntKeysForCompare**: Parses numeric values for comparison.
- **removeNotValidKeysForComparison**: Cleans objects by removing unnecessary keys.
- **trimObjectKeysForCompare**: Trims whitespace from object keys.
- **randomPasswordGenerator**: Generates a random password.

## 🤔 Conclusion

The **LobbyForm.js** component is a robust and interactive form for managing gaming lobbies. It effectively uses React's class component structure, manages state, integrates with APIs, and ensures user-friendly form interactions. The component's architecture supports extensibility and maintenance, making it a crucial part of the application.