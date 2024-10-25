# API Helper Documentation 🛠️📄

## Overview

The `api_helper.js` file is a utility module designed to simplify and standardize HTTP requests within a JavaScript application. It leverages the Axios library to handle HTTP requests and provides a centralized way to configure the request headers, base URL, and error handling. This module is particularly useful in applications that interact with RESTful APIs.

## Table of Contents

1. [Introduction](#introduction)
2. [Installation and Setup](#installation-and-setup)
3. [Key Components](#key-components)
4. [Functions](#functions)
5. [Usage Examples](#usage-examples)
6. [Conclusion](#conclusion)

## Introduction

The `api_helper.js` module is an abstraction layer over Axios, offering a simplified API for making `GET`, `POST`, `PUT`, and `DELETE` HTTP requests. It includes:

- **Base URL Configuration**: Ensures all requests are sent to the correct API endpoint.
- **Authorization Handling**: Automatically includes an access token in the request headers.
- **Error Handling**: Centralized error management for failed requests.

## Installation and Setup

To utilize this helper, ensure you have Axios installed in your project. You can install it using npm or yarn:

```bash
npm install axios
```

```bash
yarn add axios
```

Make sure you have a valid access token module in place (`accessToken.js`) that exports the token used for authentication.

## Key Components

Here's a breakdown of the key components in `api_helper.js`:

- **Imports**:
  - `axios`: The library used to make HTTP requests.
  - `accessToken`: A module that exports the current access token for authentication.

- **Axios Instance**:
  - `axiosApi`: Configured with a base URL and default headers including the Authorization header.

- **Interceptors**:
  - Handles responses and errors, designed to propagate errors back to the caller for handling.

## Functions

The module exports four main functions:

1. **`get(url, config = {})`**: Performs a `GET` request.
   - **Parameters**:
     - `url`: The endpoint to fetch data from.
     - `config`: Optional Axios configuration object.
   - **Returns**: A promise resolving to the response data.

2. **`post(url, data, config = {})`**: Performs a `POST` request.
   - **Parameters**:
     - `url`: The endpoint to send data to.
     - `data`: The payload to send in the request body.
     - `config`: Optional Axios configuration object.
   - **Returns**: A promise resolving to the response data.

3. **`put(url, data, config = {})`**: Performs a `PUT` request.
   - **Parameters**:
     - `url`: The endpoint to update data.
     - `data`: The payload to update in the request body.
     - `config`: Optional Axios configuration object.
   - **Returns**: A promise resolving to the response data.

4. **`del(url, config = {})`**: Performs a `DELETE` request.
   - **Parameters**:
     - `url`: The endpoint to delete data from.
     - `config`: Optional Axios configuration object.
   - **Returns**: A promise resolving to the response data.

## Usage Examples

### Example 1: GET Request

```javascript
import { get } from './api_helper';

async function fetchData() {
  try {
    const data = await get('/api/v1/resource');
    console.log(data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}
```

### Example 2: POST Request

```javascript
import { post } from './api_helper';

async function createResource(payload) {
  try {
    const response = await post('/api/v1/resource', payload);
    console.log('Resource created:', response);
  } catch (error) {
    console.error('Error creating resource:', error);
  }
}
```

## Conclusion

The `api_helper.js` module is a powerful tool for managing HTTP requests and handling API interactions within your project. By centralizing configurations and leveraging Axios interceptors, it provides a cleaner and more manageable way to work with APIs, ensuring consistency and reducing boilerplate code.

# 📄 AddPrizes.jsx Documentation

The `AddPrizes.jsx` file is a React component used in a web application that handles the addition and management of prizes based on ranking positions. This component allows users to input prize amounts for specific positions in a tournament or competition.

---

## Table of Contents
- [🛠️ Functionality Overview](#functionality-overview)
- [📚 Dependencies](#dependencies)
- [📦 Component Structure](#component-structure)
- [📋 Key Functions and Logic](#key-functions-and-logic)
- [🧩 Usage](#usage)
- [🔗 Other Components and Utilities](#other-components-and-utilities)
- [🎨 Styling](#styling)

---

## 🛠️ Functionality Overview

The `AddPrizes` component provides a user interface for inputting prize amounts for different ranking positions. It integrates with a Redux store to manage and update the prize list, ensuring that the entered data is consistent across the application. This component enforces validation rules on the input fields to ensure data integrity.

---

## 📚 Dependencies

- **React & React Hooks**: `useState, useEffect`
- **Redux**: `useSelector, useDispatch`
- **Availity Reactstrap Validation**: `AvField` for form validation

---

## 📦 Component Structure

```jsx
const AddPrizes = (count) => {
  // Initialization
  const prizeList = useSelector((state) => state?.PrizeList);
  const [prizeBasedOnRanking, setPrizeBasedOnRanking] = useState(prizeList.prize);
  const dispatch = useDispatch();

  // Functions
  const handlePrize = (event, prizeListArr) => { /* ... */ };
  const handleKeyDown = (e) => { /* ... */ };

  // Render
  return (
    <table className="table table-striped table-bordered lobbies-table responsiveTable addPrize-tournament">
      <thead>
        <tr>
          <th>Position</th>
          <th>Amount</th>
        </tr>
      </thead>
      <tbody>
        {/* Dynamic Rows */}
      </tbody>
    </table>
  );
};
```

---

## 📋 Key Functions and Logic

### **1. State Management with Redux**
- **`useSelector`**: Retrieves the current prize list from the Redux store.
- **`useDispatch`**: Allows dispatching actions to update the Redux store.

### **2. Handling Prize Input**
- **`handlePrize`**: Updates the prize list based on user input. Ensures that positions and amounts are correctly updated and avoids duplicate entries.
- **`handleKeyDown`**: Prevents invalid characters (e.g., `.` or `-`) from being entered into the input fields.

### **3. Validation**
- Uses `AvField` from Availity Reactstrap Validation to enforce input validation rules such as:
  - Amount is required and must be greater than 0.
  - Amount must not exceed 1000.
  - No decimal values allowed.

### **4. Dynamic Table Generation**
- Uses `createPrizeTable` utility function to generate table rows based on the `count` prop.

---

## 🧩 Usage

To utilize the `AddPrizes` component, it must be included in a parent component that provides the necessary props and is connected to a Redux store containing a `PrizeList` state.

```jsx
import AddPrizes from './AddPrizes';

const TournamentPage = () => {
  const prizeCount = { count: 10, PrizeData: [...] };

  return (
    <div>
      <h1>Manage Prizes</h1>
      <AddPrizes count={prizeCount} />
    </div>
  );
};
```

---

## 🔗 Other Components and Utilities

- **`createPrizeTable`**: A utility function imported from `util.js` that likely constructs the structure of prize data based on given count and data.
- **`setPrizeList`**: An action from `redux/actions` used to update the prize list in the Redux store.

---

## 🎨 Styling

The component applies the following classes for styling:
- `table`
- `table-striped`
- `table-bordered`
- `lobbies-table`
- `responsiveTable`
- `addPrize-tournament`

These classes are likely defined in a corresponding CSS file to ensure consistent styling across the application.

---

This documentation provides a detailed overview of the `AddPrizes.jsx` component, explaining its purpose, structure, and integration within a React-Redux application. This component is crucial for managing prize data, ensuring that users can input and update prize amounts accurately and efficiently.

# Documentation for `consts.js` 📜

Welcome to the documentation for the `consts.js` file. This file is a simple yet essential part of the application as it defines constants that are used throughout the codebase. Constants are immutable values that provide meaningful names to data, making the code easier to read and maintain. In this file, the constants relate to tournament entry timings.

## Table of Contents 📚
- [Overview](#overview)
- [Constants Defined](#constants-defined)
- [Usage](#usage)

## Overview 🌟

The `consts.js` file exports constants that are likely used in settings or configurations related to tournaments. By centralizing these constants in one file, we can easily manage and update them without having to search through the entire codebase.

## Constants Defined 📏

Here are the constants defined in this file:

| Constant Name                          | Value | Description                                                                                           |
|----------------------------------------|-------|-------------------------------------------------------------------------------------------------------|
| `tournamentLastEntryBufferMinutes`     | 10    | Represents the buffer time in minutes before the tournament entry closes. This ensures no last-minute entries. |
| `tournamentLastEntryBufferFromNow`     | 5     | Similar to the above, it defines a buffer time, possibly indicating a different context or situation. |

### Explanation

- **`tournamentLastEntryBufferMinutes`**: This constant is set to 10, which could mean that users must enter the tournament at least 10 minutes before it starts. This buffer ensures that there is adequate processing time before the tournament begins.

- **`tournamentLastEntryBufferFromNow`**: Set to 5, it might be used in different scenarios, possibly when calculating time from a different reference point. It serves to provide a flexible buffer for operations related to tournament entries.

## Usage 📈

These constants are likely imported wherever tournament timing logic is implemented, ensuring consistent values are used throughout the application. Here's a hypothetical example of how these constants might be used:

```javascript
import { tournamentLastEntryBufferMinutes, tournamentLastEntryBufferFromNow } from './consts';

function canEnterTournament(currentTime, tournamentStartTime) {
  const bufferEndTime = tournamentStartTime - tournamentLastEntryBufferMinutes * 60 * 1000;
  return currentTime < bufferEndTime;
}

function calculateBuffer() {
  // Logic using tournamentLastEntryBufferFromNow
}
```

In the above code, `canEnterTournament` function checks if the current time is within the allowed entry period based on the buffer defined.

## Conclusion 🎯

The `consts.js` file might be simple, but it plays a significant role in ensuring the code is clean, maintainable, and easy to update. By using constants, developers can avoid magic numbers in the code, making it more readable and understandable.

Feel free to reach out if you have any questions or need further clarification on how these constants are used within the application! 😊

# CreatePrizes.jsx Documentation 📜

Welcome to the documentation for the `CreatePrizes.jsx` file! This React component is part of a larger application that manages the creation and configuration of prizes for tournaments or competitions. Below, you'll find a detailed breakdown of what this component does and how it works.

## Table of Contents 📑

- [Overview](#overview)
- [Imports](#imports)
- [Component Props](#component-props)
- [State Variables](#state-variables)
- [Functions](#functions)
- [Return Structure](#return-structure)
- [Usage](#usage)

## Overview

The `CreatePrizes` component is responsible for managing the input and validation of prize and match numbers for a tournament. It uses various React and Redux functionalities to handle state and dispatch actions accordingly.

## Imports

```javascript
import React, { useState } from "react";
import { Col, FormGroup, Label, Input, FormFeedback } from "reactstrap";
import "react-quill/dist/quill.snow.css";
import { AvField } from "availity-reactstrap-validation";
import AddPrizes from "./AddPrizes";
import { useDispatch } from "react-redux";
import {
  setClearPrizeList,
  setScheduleCount,
  updatePrizeCount,
} from "../store/actions";
```

### Description of Imports:

- **React & Reactstrap**: Used for building React components and form controls.
- **AddPrizes**: A child component that handles the detailed prize list.
- **Redux**: Utilized for managing state and dispatching actions.
- **Styles**: CSS for styling the component.

## Component Props

The `CreatePrizes` component receives several props:

- **BestOfMatches**: Determines if the component should handle matches input.
- **matchId, count, resetError, EditPrizeCount, EditPrizeData, Edit**: Various props for managing matches and prizes.
- **SetMaxPrizeCount**: Maximum number of prizes allowed.
- **gameTypeMode**: Game mode that affects form behavior.

## State Variables

### `numberOfPrizes`
- **Type**: `Number`
- **Purpose**: Tracks the number of prizes to be created.

### `numberOfMatches`
- **Type**: `Number`
- **Purpose**: Tracks the number of matches (if applicable).

### `numberOfMatchesError`
- **Type**: `String`
- **Purpose**: Stores error messages related to the number of matches.

## Functions

### `handleKeyDown(e)`
Prevents the input of invalid characters such as dots and hyphens in number fields.

### `handleInputChange(e)`
- **Purpose**: Handles the change events for match input fields, validates the input, and updates state and Redux store accordingly.
- **Validation**: Ensures the number of matches is between 1 and 5.

## Return Structure

The component conditionally renders input fields based on the `BestOfMatches` prop:

- **If `BestOfMatches` is true**: Renders an input for the number of matches with validation.
- **If false**: Renders an input for the number of prizes and includes the `AddPrizes` component to handle prize details.

### JSX Structure

```jsx
<FormGroup className="mb-3 w-100">
  <Label>No. of matches*</Label>
  <Input
    name="noOfMatches"
    placeholder="No. of matches"
    type="number"
    onChange={handleInputChange}
    min={1}
    max={5}
  />
  <FormFeedback className="errorMsgGames invalid-feedback">
    {numberOfMatchesError}
  </FormFeedback>
</FormGroup>
```

## Usage

To use this component, import it and include it in your JSX with the necessary props. Make sure to provide the required Redux setup and context for it to function properly.

```jsx
<CreatePrizes
  BestOfMatches={true}
  matchId={1}
  count={(value) => console.log(value)}
  resetError={() => console.log("reset")}
  EditPrizeCount={5}
  EditPrizeData={[/* data */]}
  Edit={false}
  SetMaxPrizeCount={10}
  gameTypeMode={{ value: 1 }}
/>
```

## Conclusion

The `CreatePrizes` component is a robust tool for managing prize and match configurations in a tournament setting. With its built-in validation and state management, it streamlines the setup process, ensuring a smooth user experience. 🎯

Feel free to tweak and extend this component as needed to fit the requirements of your specific application! 🚀

# DateToUtc.js 📅✨

## Overview
The `DateToUtc.js` file contains a simple yet powerful utility function, `DateToUtc`, that converts a given local date and time to UTC format. This is particularly useful for applications that need to handle time zone differences and ensure consistent time representation.

## Function Description

### `DateToUtc(date, time)`
This function takes a local date and time as input and returns an object with the date and time converted to UTC.

#### Parameters:
- **`date`** (string): The local date in the format `YYYY-MM-DD`.
- **`time`** (string): The local time in the format `HH:MM:SS`.

#### Returns:
- An object containing:
  - **`date`**: A string representation of the UTC date in the format `YYYY-MM-DD`.
  - **`time`**: A string representation of the UTC time in the format `HH:MM:SS`.

#### Example Usage:
```javascript
import DateToUtc from './DateToUtc';

const localDate = "2023-10-05";
const localTime = "14:30:00";

const utcDateTime = DateToUtc(localDate, localTime);
console.log(utcDateTime); 
// Output: { date: '2023-10-05', time: '18:30:00' } (assuming local is UTC-4)
```

## Implementation Details
- The function creates a `Date` object by concatenating the provided date and time, appending the UTC offset `-04:00` to adjust for the timezone.
- It then extracts and formats the UTC year, month, day, hours, minutes, and seconds using the `getUTCFullYear`, `getUTCMonth`, `getUTCDate`, `getUTCHours`, `getUTCMinutes`, and `getUTCSeconds` methods.
- The result is returned as an object with properly formatted UTC date and time.

## Key Points
- **Time Zone Handling**: This utility is crucial for applications dealing with multiple time zones, ensuring that all date-time data is standardized to UTC.
- **Simplicity**: The function is straightforward to use, requiring only a date and time string.
- **Flexibility**: Can be easily integrated into various parts of a project where date-time conversion is necessary.

## Conclusion
The `DateToUtc.js` file provides an essential utility for converting local time to UTC, aiding in maintaining time consistency across applications, especially those operating in multiple geographical locations. Its straightforward approach makes it a handy tool for developers dealing with time data.

# 📄 CsvView.jsx Documentation

---

## 📋 Table of Contents

1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Code Breakdown](#code-breakdown)
4. [Props](#props)
5. [Rendering Logic](#rendering-logic)
6. [Conclusion](#conclusion)

---

## 🌟 Introduction

The `CsvView.jsx` component is a React functional component designed to render CSV content. It evaluates whether the CSV content is JSON-based or table-formatted and displays it accordingly. This flexibility allows it to handle different data formats seamlessly.

---

## ⚙️ Component Overview

- **Language**: JavaScript (React)
- **Functionality**: Renders CSV data as a list or table.
- **Dependencies**: React library.

---

## 🔍 Code Breakdown

```jsx
import React from "react";

const CsvView = ({ csvContents }) => {
  const isjson = csvContents[0]?.tournamentName === "[";

  return (
    <>
      {isjson ? (
        csvContents?.map((csvItem, csvIndex) => {
          return (
            <>
              {csvItem.tournamentName} {csvItem.tournamentRank}
            </>
          );
        })
      ) : (
        <table className="table table-striped table-bordered responsiveTable">
          <tbody>
            {csvContents?.map((csvItem, csvIndex) => {
              return (
                <tr key={csvIndex}>
                  <>
                    {csvIndex === 0 ? (
                      <>
                        <th>{csvItem.tournamentName}</th>
                        <th>{csvItem.tournamentRank}</th>
                      </>
                    ) : (
                      <>
                        <td>{csvItem.tournamentName || "N/A"}</td>
                        <td>{csvItem.tournamentRank || "0"}</td>
                      </>
                    )}
                  </>
                </tr>
              );
            })}
          </tbody>
        </table>
      )}
    </>
  );
};

export default CsvView;
```

---

## 📥 Props

- **`csvContents`**: An array of objects that represent the CSV data. Each object should have at least two properties:
  - `tournamentName`: Name of the tournament.
  - `tournamentRank`: Rank of the tournament.

---

## 🔗 Rendering Logic

1. **Determine Format**: 
   - The component first checks if the data is in JSON format by inspecting the first item's `tournamentName` property. If it equals `"["`, it assumes JSON format.

2. **Render JSON**:
   - If the data is JSON, it maps through the `csvContents` array, rendering each item as a simple text line showing `tournamentName` followed by `tournamentRank`.

3. **Render Table**:
   - If the data is not JSON, it renders a table.
   - The first row contains table headers.
   - Subsequent rows display data cells for `tournamentName` and `tournamentRank`.

4. **Data Handling**:
   - For headers (first row), it uses `<th>` tags.
   - For data rows, it uses `<td>` tags.
   - Provides default values: `"N/A"` for `tournamentName` and `"0"` for `tournamentRank` if they are missing.

---

## 📌 Conclusion

The `CsvView.jsx` component is a robust solution for rendering CSV data in a React application. It intelligently determines the format of the incoming data and chooses the appropriate rendering method. This flexibility ensures that it can handle a variety of CSV data formats effectively. 

By following the outlined structure, developers can easily integrate this component into their applications to display CSV data without additional formatting concerns.

---

# 📄 EditFreeLobby.js Documentation

**EditFreeLobby.js** is a React component designed to allow users to update the free lobby limit for a specific user. This component utilizes several libraries and components to achieve its functionality, including `react-toastify` for notifications, `availity-reactstrap-validation` for form validation, and several custom utilities and assets.

## 📑 Table of Contents
1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Component Props](#component-props)
4. [State Management](#state-management)
5. [Functions](#functions)
   - [handleChange](#handlechange)
   - [handleSubmit](#handlesubmit)
6. [Rendering](#rendering)
7. [PropTypes](#proptypes)

## 📘 Overview

The `EditFreeLobby` component provides a form interface for updating the free lobby limit of a user. The component takes in default values and functions as props and handles updates and validations internally before submitting the data.

## 📦 Dependencies

```javascript
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import { updateFreeLobbyLimit } from "../services/user_api_helper";
import PropTypes from "prop-types";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { FormGroup, Button } from "reactstrap";
import { toast } from "react-toastify";
import toastrOptions from "../helpers/toastr-options/toastr-options";
import tickIcon from "../assets/images/user-tick-icon.svg";
import crossIcon from "../assets/images/user-cross-icon.svg";
import IconsToolTip from "../components/IconsToolTip";
```

### 📋 Description of Dependencies:

- **React & useState**: To manage component state.
- **react-super-responsive-table**: For responsive table design.
- **user_api_helper**: Custom service for API interactions.
- **PropTypes**: For runtime type checking of the props.
- **availity-reactstrap-validation**: For form validation.
- **reactstrap**: For Bootstrap components.
- **react-toastify**: For displaying notifications.
- **IconsToolTip**: A custom component for displaying icons with tooltips.

## 🧩 Component Props

- **`onClose`**: A function to close the form/modal.
- **`callApi`**: A function to refresh or fetch data after the limit is updated.
- **`defaultFreeLobbyLimit`**: The default value for the free lobby limit.
- **`userId`**: The ID of the user whose free lobby limit is being updated.

## 🔄 State Management

- **`value`**: Represents the current value of the free lobby limit input. It is initially set to `props.defaultFreeLobbyLimit`.

```javascript
const [value, setValue] = useState(props.defaultFreeLobbyLimit);
```

## 🔧 Functions

### handleChange

```javascript
const handleChange = (val) => {
    setValue(val);
};
```

- **Purpose**: Updates the state `value` whenever the input value changes.

### handleSubmit

```javascript
const handleSubmit = async (event, values) => {
    let data = { limit: values.freeLobbyLimit };
    if (value)
        await updateFreeLobbyLimit(props.userId, data)
            .then((res) => {
                props.onClose();
                props.callApi();
                toast.success("Free lobby limit successfully updated", toastrOptions);
            })
            .catch((err) => {
                console.log(err);
            });
};
```

- **Purpose**: Submits the updated free lobby limit to the backend. It calls `updateFreeLobbyLimit` from the `user_api_helper` and handles success and error cases.

## 🖼 Rendering

The component returns a form using `AvForm` with a single input field to update the free lobby limit. The form includes validation rules such as ensuring the input is a number, is required, and that it doesn't allow decimal values.

```jsx
<AvForm className="d-flex editEarning-timeline" onValidSubmit={(e, v) => { handleSubmit(e, v); }}>
    <AvField className="min-width-261" name="freeLobbyLimit" label="Free Lobby Limit" placeholder="Free Lobby Limit" type="text" validate={{
        required: { value: true, errorMessage: "Free lobby limit is required" },
        number: { value: true, errorMessage: "Please enter number only" },
        min: { value: 0, errorMessage: "Free lobby limit can't be less than 0" },
        pattern: { value: /^(0|[1-9]\d*)(e-?(0|[1-9]\d*))?$/, errorMessage: "Free lobby limit can't be in decimals" },
    }} onChange={(e) => handleChange(e.target.value)} defaultValue={value} />
    <FormGroup>
        <div className="mt-4 d-flex">
            <Button type="submit" color="primary" className="edit-icon info-icon">
                <IconsToolTip image={tickIcon} altImageText="user-tick-icon" text="Save" />
            </Button>
            <Button className="edit-icon mt-2 ms-0 px-0 info-icon" onClick={() => { props.onClose(); }}>
                <IconsToolTip image={crossIcon} altImageText="user-cross-icon" text="Cancel" />
            </Button>
        </div>
    </FormGroup>
</AvForm>
```

## 📏 PropTypes

The component uses `PropTypes` to enforce type checking for the props to ensure they are correctly passed to the component.

```javascript
EditFreeLobby.propTypes = {
    onClose: PropTypes.func,
    callApi: PropTypes.func,
};
```

## ✅ Conclusion

The **EditFreeLobby** component provides a user-friendly way to update the free lobby limit with validations and feedback, ensuring data integrity and smooth user experience. It is structured to handle input changes, validate them, and submit data asynchronously, providing visual feedback through toast notifications.

# EarningTimeline.js Documentation 📄

## Overview
The **EarningTimeline.js** file is a React component designed for updating the earning timeline of a user's profile within a web application. It provides a user interface for editing and validating the number of days in the earning timeline, while ensuring that user input adheres to specific validation rules. This component uses Redux for state management and integrates with services for updating user data.

## Components and Libraries Used

- **React**: A JavaScript library for building user interfaces.
- **AvField** and **AvForm**: Components from `availity-reactstrap-validation` for form validation.
- **PropTypes**: Used to document the intended types of properties passed to components.
- **reactstrap**: Provides Bootstrap components as React components.
- **react-toastify**: Used for displaying notifications.
- **IconsToolTip**: Custom component for displaying tooltips with icons.

## Key Features 🛠️

- **Form Validation**: Ensures that the input adheres to rules such as being a number, not in decimals, and within the allowed range (1 to 365 days).
- **State Management**: Uses React's state to manage the earning timeline input.
- **Asynchronous Operations**: Handles the submission of data and updates the backend asynchronously.
- **User Feedback**: Utilizes `react-toastify` to provide feedback upon successful update or error.
- **Responsive UI**: The component supports responsive design using `react-super-responsive-table`.

## Component Breakdown

### Imports

```javascript
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import { updateEarning } from "../services/user_api_helper";
import PropTypes from "prop-types";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { FormGroup, Button } from "reactstrap";
import { toast } from "react-toastify";
import toastrOptions from "../helpers/toastr-options/toastr-options";
import tickIcon from "../assets/images/user-tick-icon.svg";
import crossIcon from "../assets/images/user-cross-icon.svg";
import IconsToolTip from "../components/IconsToolTip";
```

### State Management

- **value**: This state holds the current value of the earning timeline input, initialized with `props.days`.

### Event Handlers

- **handleChange**: Updates the `value` state when the input changes.
- **handleSubmit**: Manages form submission, calls the API to update the earning timeline, and handles responses.

### Validation Rules ✔️

- **Required**: The field is mandatory.
- **Number**: Only numerical inputs are allowed.
- **Max Value**: The maximum allowed value is 365.
- **Pattern**: Ensures the value is a positive integer.

### Form Structure

```jsx
<AvForm className="d-flex editEarning-timeline"
    onValidSubmit={(e, v) => { handleSubmit(e, v); }}>
    <AvField name="earningTimeline" label="Earning Timeline" placeholder="Earning Timeline"
        type="text" validate={{ required, number, max, pattern }}
        onChange={(e) => handleChange(e.target.value)} defaultValue={value} />
    <div className="daysBox editDaysBox">
        <span class="input-group-addon">Days</span>
    </div>
    <FormGroup>
        <div className="mt-4 d-flex">
            <Button type="submit" color="primary" className="edit-icon info-icon">
                <IconsToolTip image={tickIcon} altImageText="user-tick-icon" text="Save" />
            </Button>
            <Button className="edit-icon mt-2 ms-0 px-0 info-icon"
                onClick={() => { props.onClose(); }}>
                <IconsToolTip image={crossIcon} altImageText="user-cross-icon" text="Cancel" />
            </Button>
        </div>
    </FormGroup>
</AvForm>
```

### PropTypes

```javascript
EarningTimeline.propTypes = {
    onClose: PropTypes.func,
    callApi: PropTypes.func,
};
```

## Usage and Integration

- **onClose**: A function prop to handle the closing of the edit form.
- **callApi**: A function prop to trigger additional API calls if needed.

## Conclusion

The **EarningTimeline.js** component is a comprehensive solution for managing the earning timeline in a user-centric application, with robust validation and user feedback mechanisms. It leverages React's ecosystem to provide a seamless editing experience.

# EditReferral.js Documentation

**Filename**: `EditReferral.js`

## Overview

The `EditReferral.js` file defines a React component that allows users to update referral codes in a user interface. It utilizes form validation and provides feedback upon successful or unsuccessful operations. The component displays a form with input fields and provides options to submit the form or cancel the operation.

### Table of Contents
1. [Component Structure](#component-structure)
2. [Key Features](#key-features)
3. [Code Breakdown](#code-breakdown)
4. [Prop Types](#prop-types)
5. [Usage](#usage)

## Component Structure

The `EditReferral` component consists of the following elements:

- Importing necessary libraries and utilities.
- Defining the `EditReferral` component with state and handlers.
- Form rendering and validation using `AvForm` and `AvField`.
- Submit and cancel buttons with associated actions.

## Key Features

- 📋 **Form Validation**: Uses `availity-reactstrap-validation` to ensure input fields meet specific criteria.
- 🔄 **State Management**: Maintains input values using React state hooks.
- ☑️ **Icons and Tooltips**: Utilizes tooltips alongside buttons for enhanced user understanding.
- 🛠️ **API Integration**: Sends requests to update referral codes using an API helper function.
- 📢 **Toaster Notifications**: Displays success messages using `react-toastify`.

## Code Breakdown

### Imports

```javascript
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import { updateReferral } from "../services/user_api_helper";
import PropTypes from "prop-types";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { FormGroup, Button } from "reactstrap";
import { toast } from "react-toastify";
import toastrOptions from "../helpers/toastr-options/toastr-options";
import tickIcon from "../assets/images/user-tick-icon.svg";
import crossIcon from "../assets/images/user-cross-icon.svg";
import IconsToolTip from "../components/IconsToolTip";
```

### Component Function

The component is a functional React component using hooks for state management.

```javascript
const EditReferral = (props) => {
  const [value, setValue] = useState(props.defaultReferral);

  const handleChange = (val) => {
    setValue(val);
  };

  const handleSubmit = async (event, values) => {
    let data = { referral_code: values.referralCode };
    if (value)
      await updateReferral(props.userId, data)
        .then((res) => {
          props.onClose();
          props.callApi();
          toast.success("Referral code successfully updated", toastrOptions);
        })
        .catch((err) => {
          console.log(err);
        });
  };

  return (
    <>
      <AvForm
        className="d-flex editEarning-timeline"
        onValidSubmit={(e, v) => {
          handleSubmit(e, v);
        }}
      >
        <AvField
          className="min-width-261"
          name="referralCode"
          label="Referral Code"
          placeholder="Referral Code"
          type="text"
          validate={{
            required: { value: true, errorMessage: "Referral Code is required" },
            pattern: {
              value: /^.{4,23}$/,
              errorMessage: "Referral Code must be between 4 to 23 characters",
            },
          }}
          onChange={(e) => handleChange(e.target.value)}
          defaultValue={value}
        />
        <FormGroup>
          <div className="mt-4 d-flex">
            <Button
              type="submit"
              color="primary"
              className="edit-icon info-icon"
            >
              <IconsToolTip image={tickIcon} altImageText="user-tick-icon" text="Save" />
            </Button>
            <Button
              className="edit-icon mt-2 ms-0 px-0 info-icon"
              onClick={() => {
                props.onClose();
              }}
            >
              <IconsToolTip image={crossIcon} altImageText="user-cross-icon" text="Cancel" />
            </Button>
          </div>
        </FormGroup>
      </AvForm>
    </>
  );
};
```

### Prop Types

```javascript
EditReferral.propTypes = {
  onClose: PropTypes.func,
  callApi: PropTypes.func,
};
```

- **onClose**: Function to close the form modal.
- **callApi**: Function to refresh or fetch updated data from the API.

## Usage

To use the `EditReferral` component, it should be integrated within a parent component where user referral codes need to be edited. You need to pass relevant props such as `onClose` and `callApi` functions.

```jsx
<EditReferral
  defaultReferral="defaultCode"
  userId={someUserId}
  onClose={someCloseFunction}
  callApi={someApiFunction}
/>
```

This component will handle displaying the form, validating user input, and updating the referral code through the given API when submitted.

# 📄 `fakebackend_helper.js` Documentation

Welcome to the documentation for `fakebackend_helper.js`. This file serves as a collection of helper functions for interacting with a fake backend service. It uses the Axios library to perform HTTP requests and provides utility functions for authentication, user management, and various API operations.

---

## 📚 **Table of Contents**

1. [Overview](#overview)
2. [Imports](#imports)
3. [Authentication Helpers](#authentication-helpers)
4. [User Management](#user-management)
5. [Event Management](#event-management)
6. [Product Management](#product-management)
7. [Social Login](#social-login)
8. [Chat and Messaging](#chat-and-messaging)
9. [Project Management](#project-management)
10. [Task Management](#task-management)
11. [User Profile](#user-profile)
12. [Exports](#exports)

---

## Overview

The `fakebackend_helper.js` file provides a suite of functions that facilitate communication with a backend API. These functions wrap HTTP requests for various operations, such as user authentication, event management, product management, and more. The file leverages helper functions from `api_helper.js` and predefined URL paths from `url_helper.js`.

---

## 📥 Imports

```javascript
import axios from "axios";
import { post, del, get, put } from "./api_helper";
import * as url from "./url_helper";
```

- **Axios**: Used for making HTTP requests.
- **API Helper Functions**: `post`, `del`, `get`, `put` functions abstract HTTP methods.
- **URL Helper**: Contains predefined endpoints used within this file.

---

## 🔐 Authentication Helpers

### Get Logged In User
```javascript
const getLoggedInUser = () => {
    const user = localStorage.getItem("user");
    if (user) return JSON.parse(user);
    return null;
}
```
- Retrieves the currently logged-in user from `localStorage`.

### Is User Authenticated
```javascript
const isUserAuthenticated = () => {
    return getLoggedInUser() !== null;
}
```
- Determines if a user is authenticated by checking the presence of user data in `localStorage`.

---

## 🧑‍💻 User Management

### Register Methods
```javascript
const postFakeRegister = (data) => post(url.POST_FAKE_REGISTER, data);
const postJwtRegister = (url, data) => {
    return axios.post(url, data)
        .then(response => { /* ... */ })
        .catch(err => { /* ... */ });
}
```
- **postFakeRegister**: Registers a new user using fake API.
- **postJwtRegister**: Registers a new user using JWT (JSON Web Token) authentication.

### Login Methods
```javascript
const postFakeLogin = data => post(url.POST_FAKE_LOGIN, data);
const postJwtLogin = data => post(url.POST_FAKE_JWT_LOGIN, data);
```
- **postFakeLogin**: Logs in a user through fake API.
- **postJwtLogin**: Logs in a user with JWT.

### Password Forget
```javascript
const postFakeForgetPwd = data => post(url.POST_FAKE_PASSWORD_FORGET, data);
const postJwtForgetPwd = data => post(url.POST_FAKE_JWT_PASSWORD_FORGET, data);
```
- Sends a request to reset the password.

### Profile Update
```javascript
const postJwtProfile = data => post(url.POST_EDIT_JWT_PROFILE, data);
const postFakeProfile = data => post(url.POST_EDIT_PROFILE, data);
```
- Updates user profile information.

---

## 🌟 Event Management

### Event Operations
```javascript
export const getEvents = () => get(url.GET_EVENTS);
export const addNewEvent = event => post(url.ADD_NEW_EVENT, event);
export const updateEvent = event => put(url.UPDATE_EVENT, event);
export const deleteEvent = event => del(url.DELETE_EVENT, { headers: { event } });
```
- **getEvents**: Retrieves all events.
- **addNewEvent**: Adds a new event.
- **updateEvent**: Updates an existing event.
- **deleteEvent**: Deletes an event.

---

## 🛍️ Product Management

### Product Operations
```javascript
export const getProducts = () => get(url.GET_PRODUCTS);
export const getProductDetail = id => get(`${url.GET_PRODUCTS_DETAIL}/${id}`, { params: { id } });
```
- **getProducts**: Fetches a list of products.
- **getProductDetail**: Retrieves detailed information about a specific product.

---

## 🌐 Social Login

```javascript
export const postSocialLogin = data => post(url.SOCIAL_LOGIN, data);
```
- Allows for social media authentication by posting social login data.

---

## 💬 Chat and Messaging

### Chat Operations
```javascript
export const getChats = () => get(url.GET_CHATS);
export const getGroups = () => get(url.GET_GROUPS);
export const getContacts = () => get(url.GET_CONTACTS);
```
- **getChats**: Retrieves chat sessions.
- **getGroups**: Fetches groups.
- **getContacts**: Obtains contact lists.

### Messaging
```javascript
export const getMessages = (roomId = "") => get(`${url.GET_MESSAGES}/${roomId}`, { params: { roomId } });
export const addMessage = message => post(url.ADD_MESSAGE, message);
```
- **getMessages**: Obtains messages in a specific room.
- **addMessage**: Adds a new message to a chat.

---

## 📊 Project Management

### Project Operations
```javascript
export const getProjects = () => get(url.GET_PROJECTS);
export const getProjectsDetails = id => get(`${url.GET_PROJECT_DETAIL}/${id}`, { params: { id } });
```
- **getProjects**: Fetches a list of projects.
- **getProjectsDetails**: Retrieves details for a specific project.

---

## 📋 Task Management

```javascript
export const getTasks = () => get(url.GET_TASKS);
```
- Retrieves a list of tasks.

---

## 👤 User Profile

### Profile Operations
```javascript
export const getUsers = () => get(url.GET_USERS);
export const getUserProfile = () => get(url.GET_USER_PROFILE);
```
- **getUsers**: Fetches users.
- **getUserProfile**: Retrieves the profile of the logged-in user.

---

## 📤 Exports

The following functions are exported for use in other modules:
- `getLoggedInUser`
- `isUserAuthenticated`
- `postFakeRegister`
- `postFakeLogin`
- `postFakeProfile`
- `postFakeForgetPwd`
- `postJwtRegister`
- `postJwtLogin`
- `postJwtForgetPwd`
- `postJwtProfile`

These utility functions are essential for handling various backend operations, authentication, and data management in your application.

--- 

This concludes the documentation for `fakebackend_helper.js`. If you have any questions or need further assistance, please refer to the code comments and function definitions for more insight. Happy coding! 🚀

# 📚 fakeBackend.js Documentation

Welcome to the documentation for the **`fakeBackend.js`** file! This module is designed to simulate a backend server using Axios and Mock Adapter. It provides a series of mock API endpoints for testing purposes without having to set up a real backend server. Below, you will find a comprehensive guide to understanding how this module works and the functionalities it provides.

## 📑 Table of Contents

1. [Overview](#overview)
2. [Modules and Libraries](#modules-and-libraries)
3. [Mocked Endpoints](#mocked-endpoints)
    - [User Authentication](#user-authentication)
    - [Profile Management](#profile-management)
    - [Password Management](#password-management)
    - [Event Management](#event-management)
    - [Task Management](#task-management)
    - [Category Management](#category-management)
4. [Usage](#usage)
5. [Conclusion](#conclusion)

## 🔍 Overview

The **`fakeBackend.js`** file uses Axios Mock Adapter to mock HTTP requests and responses. It is particularly useful for frontend development and testing, allowing developers to simulate API interactions without needing a live server. This is ideal for creating a development environment that is stable and predictable.

## 📦 Modules and Libraries

The module imports several libraries and modules:

- **axios**: A promise-based HTTP client for making requests.
- **axios-mock-adapter**: A module to mock requests made using Axios.
- **url_helper**: Contains various constants used as URL endpoints.
- **accessToken**: A utility for handling JWT access tokens.
- **common/data**: Contains mock data for calendar events and tasks.

## 🔧 Mocked Endpoints

### 👤 User Authentication

The module provides mock endpoints for user registration and login:

- **Register**: Adds a new user to the mock user list.
- **Login**: Validates user credentials and returns a mock user object with a JWT token.

#### Example
```javascript
mock.onPost("/post-fake-login").reply(config => {
    const user = JSON.parse(config["data"]);
    // Validate user credentials
});
```

### 📝 Profile Management

Endpoints for editing user profiles:

- **Edit Profile**: Updates user information and stores it in local storage.
- **Profile Validation**: Validates JWT tokens and user data.

#### Example
```javascript
mock.onPost("/post-jwt-profile").reply(config => {
    const user = JSON.parse(config["data"]);
    // Check for JWT token validity and update profile
});
```

### 🔑 Password Management

Endpoints for password management:

- **Forget Password**: Simulates a password reset process by sending an email notification.

#### Example
```javascript
mock.onPost("/fake-forget-pwd").reply(config => {
    // Simulate email for password reset
});
```

### 📅 Event Management

Endpoints for managing events:

- **Get Events**: Returns a list of mock events.
- **Add Event**: Simulates adding a new event.
- **Update Event**: Simulates updating an existing event.
- **Delete Event**: Simulates deleting an event.

#### Example
```javascript
mock.onGet(url.GET_EVENTS).reply(() => {
    // Return mock events
});
```

### ✅ Task Management

Provides an endpoint to retrieve tasks:

- **Get Tasks**: Returns a list of mock tasks.

#### Example
```javascript
mock.onGet(url.GET_TASKS).reply(() => {
    // Return mock tasks
});
```

### 📚 Category Management

Provides an endpoint to retrieve categories:

- **Get Categories**: Returns a list of mock categories.

#### Example
```javascript
mock.onGet(url.GET_CATEGORIES).reply(() => {
    // Return mock categories
});
```

## 🚀 Usage

To use the `fakeBackend.js` file, simply import it into your project and call the `fakeBackend()` function. This will set up the mock adapters and endpoints for your Axios instance.

```javascript
import fakeBackend from './path/to/fakeBackend';
fakeBackend(); // Initialize the fake backend
```

## 🏁 Conclusion

The **`fakeBackend.js`** module is a valuable tool for developers who want to simulate backend interactions while developing a frontend application. By using this mock backend, you can ensure that your application behaves correctly in a controlled environment without the need for a real server.

This documentation covers the primary functionalities of the module. For a detailed understanding, you may explore the code further and adapt it to your specific needs. Happy coding! 🎉

# 📄 FileUploadS3.js Documentation

## Overview

The `FileUploadS3.js` file provides a React component that facilitates the uploading of files (.csv and .json) using a drag-and-drop interface. It also previews the uploaded file content and any previously uploaded data from a given S3 URL.

## Table of Contents

- [Overview](#overview)
- [Component: FileUploadS3](#component-fileuploads3)
  - [Props](#props)
  - [State Variables](#state-variables)
  - [Functions](#functions)
    - [callUrl](#callurl)
    - [isValidType](#isvalidtype)
    - [handleAcceptedFiles](#handleacceptedfiles)
  - [JSX Structure](#jsx-structure)

## Component: FileUploadS3

This component is primarily responsible for handling file uploads and displaying file previews. It integrates with S3 to fetch and display content from a provided URL.

### Props

- `S3URL`: The URL pointing to the file stored in S3 to be fetched and previewed.
- `dataFromUploadedFile`: A callback function that is used to pass the uploaded file information back to the parent component.
- `isError`: A boolean indicating if there is an error in file upload that affects the styling of the component.

### State Variables

- `previewOldcsvData`: Stores the data fetched from the S3 URL to be previewed.
- `csvData`: Stores data from the newly uploaded file for preview.
- `invalidFile`: An object containing:
  - `invalidFileBoolean`: A boolean flag that indicates if the uploaded file is of invalid type.
  - `invalidFileMsg`: A string message that provides error information about the file upload.

### Functions

#### `callUrl`

- **Purpose**: Fetches the content from the S3 URL and updates the preview data.
- **Implementation**:
  ```javascript
  const callUrl = async () => {
    fetch(props.S3URL)
      .then((response) => response.text())
      .then((data) => {
        const csvpreview = csvConverterToPreviewFile(data);
        setPreviewOldCsvData(csvpreview);
      });
  };
  ```

#### `isValidType`

- **Purpose**: Checks if the file extension is within the acceptable formats (.csv, .json).
- **Implementation**:
  ```javascript
  const isValidType = (dataValid) => {
    const ext = fileFormat.map((dataFileFormat, i) => {
      return dataFileFormat;
    });
    return ext.some((el) => dataValid.endsWith(el));
  };
  ```

#### `handleAcceptedFiles`

- **Purpose**: Handles the file drop event, validates file type, reads the file content, and updates the state accordingly.
- **Implementation**:
  ```javascript
  const handleAcceptedFiles = (files) => {
    if (files.length === 0) {
      props.dataFromUploadedFile({ invalidFileBoolean: true });
      setInvalidFile({
        invalidFileBoolean: true,
        invalidFileMsg: `Please upload ${fileFormat.map((data) => {
          return data;
        })} file only`,
      });
    } else {
      // Additional implementation for handling valid files
    }
  };
  ```

### JSX Structure

The component utilizes a combination of Reactstrap components and the `react-dropzone` library to create a user-friendly file upload interface.

```jsx
return (
  <Row>
    <Col className="col-12">
      <div className="mb-3 chooseImage">
        <Dropzone
          onDrop={(acceptedFiles) => {
            handleAcceptedFiles(acceptedFiles);
          }}
          accept={[
            ".csv",
            ".json",
            // Other accept types
          ]}
        >
          {({ getRootProps, getInputProps }) => (
            <div className={`dropzone dz-clickable ${...}`}>
              <div className="dz-message needsclick" {...getRootProps()}>
                <input {...getInputProps()} />
                <div className="mb-3">
                  <i className="display-4 text-muted mdi mdi-upload-network-outline"></i>
                </div>
                <h4>
                  {invalidFile.invalidFileBoolean ? (
                    <p className="error-msg">{invalidFile.invalidFileMsg}</p>
                  ) : (
                    "Upload file"
                  )}
                  <p>
                    Accepted file {fileFormat.map((data, i) => (
                      <span> {data}</span>
                    ))}
                  </p>
                </h4>
              </div>
            </div>
          )}
        </Dropzone>
        <Col className="col-12 mt-3 ml-3">
          {csvData?.length === 0 ? null : <CsvView csvContents={csvData} />}
          {previewOldcsvData?.length === 0 ? null : (
            <>
              <h6>Preview file</h6>
              <CsvView csvContents={previewOldcsvData} />
            </>
          )}
        </Col>
      </div>
    </Col>
  </Row>
);
```

This component is designed to provide immediate visual feedback on the files being uploaded and handle errors gracefully with appropriate messaging.

# 📜 Documentation for `Find_Permission.js`

## 🎯 Overview

The `Find_Permission.js` file contains a single utility function, `FindPermission`, which is designed to extract a list of permission IDs from a given dataset. This function is particularly useful in scenarios where you need to determine all the permissions associated with certain entities, for example, users or roles, in an application.

## 📂 File Summary

- **Filename**: `Find_Permission.js`
- **Exported Function**: `FindPermission`
- **Dependencies**: None

## 🔍 Function Details

### `FindPermission(trueValue)`

#### 📝 Description

The `FindPermission` function takes an array of objects (`trueValue`) as input and returns a flattened array of permission IDs. Each object in the input array is expected to have a `permissions` property that is an array of permission objects. The function filters these permissions based on a `type_` property and extracts the `id` of each filtered permission.

#### 🖋️ Function Signature

```javascript
function FindPermission(trueValue)
```

#### 📥 Parameters

- `trueValue`: An array of objects. Each object should have a `permissions` property, which is an array of permission objects.

#### 📤 Returns

- `flattenArr`: An array of permission IDs that meet the specified conditions.

#### 🔨 Implementation

```javascript
function FindPermission(trueValue) {
  let flattenArr = [];

  const filterAllowedPermission = trueValue.map((item, id) =>
    item.permissions.filter((value) => value.type_).map((data) => data.id)
  );

  filterAllowedPermission.forEach(function (flatItem) {
    flattenArr.push(...flatItem);
  });

  return flattenArr;
}
```

#### 📚 Usage Example

Suppose you have an array of user roles, and each role has a list of permissions. You want to compile a list of all unique permission IDs that are marked as allowed (`type_` is true):

```javascript
const roles = [
  {
    role: "Admin",
    permissions: [
      { id: 1, type_: true },
      { id: 2, type_: false },
    ],
  },
  {
    role: "User",
    permissions: [
      { id: 1, type_: true },
      { id: 3, type_: true },
    ],
  },
];

const allowedPermissions = FindPermission(roles);
console.log(allowedPermissions); // Output: [1, 1, 3]
```

#### 🛠️ Notes

- **Flattening**: The function uses array flattening to compile a single list of IDs from nested arrays.
- **Filtering**: Only permissions with `type_` set to true are considered.
- **No External Dependencies**: The function operates purely on its input and does not rely on any external libraries or APIs.

## 🎨 Conclusion

The `FindPermission` function is a straightforward utility to extract and compile permissions from a structured dataset. It is essential for managing permissions dynamically in applications where roles and permissions are a key component of the security model. By delivering an array of allowed permission IDs, it simplifies the task of determining access rights in a system.

# 📄 Documentation for `FindAllowedPermission.js`

## 🎯 Overview
The `FindAllowedPermission.js` file contains a utility function designed to filter and return a modified list of objects based on a specific condition related to permissions. This function is particularly useful in applications where user roles and permissions need to be managed dynamically.

## 📘 Function: `FindAllowedPermission`

### Description
The `FindAllowedPermission` function processes an array of objects, where each object contains a list of permissions. It filters out only those objects that have at least one permission with a specific property (`type_`) set to `true`, and then returns a new array containing these filtered objects.

### Usage
This function is beneficial in scenarios where you need to extract and work with a subset of permission data from a larger list based on specific criteria.

### Function Definition
```javascript
function FindAllowedPermission(trueValue) {
    const defaultAssignedPermissions = trueValue
        .filter(({ permissions }) => permissions.some(({ type_ }) => type_))
        .map((o) => ({
            ...o,
            permissions: o.permissions.filter(({ type_ }) => o.permissions),
        }));
    return defaultAssignedPermissions;
}
export default FindAllowedPermission;
```

### Parameters
- **`trueValue`**: An array of objects. Each object is expected to have a `permissions` property, which is itself an array of permission objects. Each permission object should have a `type_` property.

### Return Value
- Returns a new array of objects. Each object contains only those permissions whose `type_` property evaluates to `true`.

### Detailed Explanation
1. **Filtering Objects**:
   - The function uses the `filter` method to iterate over each object in the `trueValue` array.
   - It checks if any permission within the `permissions` array has the `type_` property set to `true`.

2. **Mapping and Transforming Objects**:
   - For each object that passes the filter, the function uses the `map` method to create a new object structure.
   - Each resulting object retains all original properties but filters its `permissions` array to only include permissions where the `type_` property is `true`.

3. **Return Statement**:
   - The function returns the newly created array of objects containing only the filtered permissions.

### Example Usage
```javascript
const roles = [
    {
        role: "admin",
        permissions: [
            { id: 1, type_: true },
            { id: 2, type_: false },
        ],
    },
    {
        role: "user",
        permissions: [
            { id: 3, type_: true },
            { id: 4, type_: true },
        ],
    },
];

const allowedPermissions = FindAllowedPermission(roles);
console.log(allowedPermissions);
/*
Output:
[
    {
        role: "admin",
        permissions: [{ id: 1, type_: true }]
    },
    {
        role: "user",
        permissions: [
            { id: 3, type_: true },
            { id: 4, type_: true }
        ]
    }
]
*/
```

## 🚀 Summary
The `FindAllowedPermission` function is a convenient utility for filtering permission data in an application, ensuring that only the relevant permissions are processed further. This is particularly useful in role-based access control systems and applications with complex permission management requirements.

# Firebase Helper Documentation

This documentation provides an overview and explanation of the `firebase_helper.js` file, which is a JavaScript module for handling Firebase authentication and Firestore operations in a web application.

## Overview

The `firebase_helper.js` module is designed to facilitate user authentication and data management using Firebase. It incorporates Firebase's Auth and Firestore services, allowing for user registration, login, password reset, and data storage.

## Table of Contents

- [Firebase Initialization](#firebase-initialization)
- [Class: FirebaseAuthBackend](#class-firebaseauthbackend)
  - [Constructor](#constructor)
  - [Methods](#methods)
    - [registerUser](#registeruser)
    - [editProfileAPI](#editprofileapi)
    - [loginUser](#loginuser)
    - [forgetPassword](#forgetpassword)
    - [logout](#logout)
    - [addNewUserToFirestore](#addnewusertofirestore)
    - [setLoggeedInUser](#setloggeedinuser)
    - [getAuthenticatedUser](#getauthenticateduser)
    - [_handleError](#_handleerror)
- [Firebase Backend Initialization Functions](#firebase-backend-initialization-functions)
  - [initFirebaseBackend](#initfirebasebackend)
  - [getFirebaseBackend](#getfirebasebackend)

---

## Firebase Initialization

Before utilizing Firebase services, the Firebase application must be initialized with a configuration object. This is typically done within the `FirebaseAuthBackend` class, ensuring that all Firebase functionalities are set up correctly.

```javascript
firebase.initializeApp(firebaseConfig);
```

## Class: FirebaseAuthBackend

### Constructor

The constructor initializes Firebase using the provided configuration. It also sets up an authentication state observer to manage user sessions.

```javascript
constructor(firebaseConfig) {
  if (firebaseConfig) {
    firebase.initializeApp(firebaseConfig);
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        localStorage.setItem("authUser", JSON.stringify(user));
      } else {
        localStorage.removeItem("authUser");
      }
    });
  }
}
```

### Methods

#### `registerUser`

Registers a new user with an email and password.

```javascript
registerUser = (email, password) => {
  return new Promise((resolve, reject) => {
    firebase.auth().createUserWithEmailAndPassword(email, password)
      .then(user => {
        resolve(firebase.auth().currentUser);
      })
      .catch(error => {
        reject(this._handleError(error));
      });
  });
}
```

#### `editProfileAPI`

This method has the same structure as `registerUser`, but it's intended for editing user profiles. (Note: Implementation may overlap with `registerUser`.)

#### `loginUser`

Allows a user to log in with an email and password.

```javascript
loginUser = (email, password) => {
  return new Promise((resolve, reject) => {
    firebase.auth().signInWithEmailAndPassword(email, password)
      .then(user => {
        resolve(firebase.auth().currentUser);
      })
      .catch(error => {
        reject(this._handleError(error));
      });
  });
}
```

#### `forgetPassword`

Sends a password reset email to the specified address.

```javascript
forgetPassword = (email) => {
  return new Promise((resolve, reject) => {
    firebase.auth().sendPasswordResetEmail(email, {
      url: window.location.protocol + "//" + window.location.host + "/login",
    })
      .then(() => {
        resolve(true);
      })
      .catch(error => {
        reject(this._handleError(error));
      });
  });
}
```

#### `logout`

Logs the current user out of the application.

```javascript
logout = () => {
  return new Promise((resolve, reject) => {
    firebase.auth().signOut()
      .then(() => {
        resolve(true);
      })
      .catch(error => {
        reject(this._handleError(error));
      });
  });
}
```

#### `addNewUserToFirestore`

Stores additional user information in Firestore after a new user is created.

```javascript
addNewUserToFirestore = (user) => {
  const collection = firebase.firestore().collection("users");
  const { profile } = user.additionalUserInfo;
  const details = {
    firstName: profile.given_name ? profile.given_name : profile.first_name,
    lastName: profile.family_name ? profile.family_name : profile.last_name,
    fullName: profile.name,
    email: profile.email,
    picture: profile.picture,
    createdDtm: firebase.firestore.FieldValue.serverTimestamp(),
    lastLoginTime: firebase.firestore.FieldValue.serverTimestamp(),
  };
  collection.doc(firebase.auth().currentUser.uid).set(details);
  return { user, details };
}
```

#### `setLoggeedInUser`

Saves the logged-in user details to local storage.

```javascript
setLoggeedInUser = (user) => {
  localStorage.setItem("authUser", JSON.stringify(user));
}
```

#### `getAuthenticatedUser`

Retrieves the authenticated user from local storage.

```javascript
getAuthenticatedUser = () => {
  if (!localStorage.getItem("authUser")) return null;
  return JSON.parse(localStorage.getItem("authUser"));
}
```

#### `_handleError`

Handles and returns error messages from Firebase operations.

```javascript
_handleError(error) {
  var errorMessage = error.message;
  return errorMessage;
}
```

## Firebase Backend Initialization Functions

### `initFirebaseBackend`

Initializes the Firebase backend with the given configuration.

```javascript
const initFirebaseBackend = (config) => {
  if (!_fireBaseBackend) {
    _fireBaseBackend = new FirebaseAuthBackend(config);
  }
  return _fireBaseBackend;
}
```

### `getFirebaseBackend`

Returns the initialized Firebase backend instance.

```javascript
const getFirebaseBackend = () => {
  return _fireBaseBackend;
}
```

---

This document serves as a comprehensive guide to understanding and utilizing the functionalities provided by the `firebase_helper.js` module for Firebase authentication and Firestore integration. If you have any questions or require further assistance, please refer to the Firebase documentation or consult the module's author.

# Documentation for `getSignedUrls.jsx`

The `getSignedUrls.jsx` file is a utility for generating signed URLs for accessing objects in an AWS S3 bucket. This allows for secure access to S3 objects without exposing the S3 bucket to the public. Below, you will find a detailed explanation of the components and functionality provided by this file.

---

## 📜 Overview

The `getSignedUrls` function uses the AWS SDK for JavaScript to generate pre-signed URLs, which are used to securely access objects stored in Amazon S3. Pre-signed URLs grant temporary access to objects in private S3 buckets by embedding an access token in the URL.

---

## 🛠️ Components and Functions

### Imports

```javascript
import { GetObjectCommand } from "@aws-sdk/client-s3";
import { getSignedUrl } from "@aws-sdk/s3-request-presigner";
import { S3Client } from "@aws-sdk/client-s3";
```

- **`GetObjectCommand`**: Command used to retrieve an object from an S3 bucket.
- **`getSignedUrl`**: Function to generate a signed URL for an S3 request.
- **`S3Client`**: AWS SDK client for interacting with S3.

### Function: `getSignedUrls`

```javascript
async function getSignedUrls(bucketName, objectKeys) {
    const CREDENTIAL = {
        accessKeyId: process.env.REACT_APP_S3_ACCESS_KEY,
        secretAccessKey: process.env.REACT_APP_S3_SECRET_KEY,
    };
    const s3Client = new S3Client({
        region: process.env.REACT_APP_S3_REGION_NAME,
        credentials: CREDENTIAL,
    });
    const signedUrls = [];
    for (const objectKey of objectKeys) {
        const bucketData = {
            Bucket: bucketName,
            Key: objectKey,
        };
        const signedUrl = await getSignedUrl(
            s3Client,
            new GetObjectCommand(bucketData)
        );
        const urlWithoutParams = signedUrl.split("?")[0];
        signedUrls.push(urlWithoutParams);
    }
    return signedUrls;
}
```

- **Parameters**: 
  - `bucketName`: The name of the S3 bucket.
  - `objectKeys`: An array of object keys (file identifiers) in the S3 bucket.

- **CREDENTIAL**: 
  - Uses environment variables `REACT_APP_S3_ACCESS_KEY` and `REACT_APP_S3_SECRET_KEY` for AWS credentials.

- **S3Client**: 
  - Configured with the specified region and credentials.

- **Loop through `objectKeys`**: 
  - For each object key, a signed URL is generated using `getSignedUrl` and `GetObjectCommand`.

- **Return**: 
  - Returns an array of signed URLs without query parameters.

### Export

```javascript
export default getSignedUrls;
```

- **Export**: Exports the `getSignedUrls` function as the default module export.

---

## ⚙️ Environment Variables

- **`REACT_APP_S3_ACCESS_KEY`**: AWS access key ID.
- **`REACT_APP_S3_SECRET_KEY`**: AWS secret access key.
- **`REACT_APP_S3_REGION_NAME`**: AWS region name where the S3 bucket is located.

---

## 👥 Usage

To use this utility, ensure that your environment variables are set correctly and import `getSignedUrls` into your component:

```javascript
import getSignedUrls from './getSignedUrls.jsx';

const bucketName = 'your-bucket-name';
const objectKeys = ['file1.txt', 'file2.jpg'];

getSignedUrls(bucketName, objectKeys).then(urls => {
    console.log(urls); // Output the signed URLs
}).catch(err => {
    console.error('Error generating signed URLs', err);
});
```

---

## 🚀 Features

- **Secure Access**: Provides a secure method to access S3 objects without making the bucket public.
- **Configurable**: Easily configurable via environment variables for access keys and region.
- **Asynchronous**: Efficiently handles multiple requests using asynchronous operations.

---

## 🛡️ Security

Ensure that your AWS credentials are kept safe and not hardcoded into your application code. Use environment variables to manage sensitive information securely.

---

This file is a crucial part of applications that require secure, temporary access to S3 objects, providing an efficient and flexible method to manage file access in a scalable way.

# Documentation for `PermissionPath.js`

## Overview

The `PermissionPath.js` module is designed to generate and manage user permission paths within an application. It utilizes user permissions to create a navigational path that dictates what parts of the application a user can access based on their assigned permissions. This module interacts with several constants and helper functions to determine the paths and sort them accordingly.

## Table of Contents

- [Imports](#imports)
- [Functions](#functions)
  - [PermissionPath](#permissionpath)
- [Usage](#usage)
- [Exports](#exports)

## Imports

```javascript
import { sortBy } from "lodash";
import { 
    challengePermissionsGames, 
    checkIfGamePermissionIsAvailable, 
    permissionConstant, 
    permissionConstantSecond, 
    permissionGameConstantForLobbies, 
    retirevePath 
} from "../constants/permissionConstant";
import challenges from "../../src/assets/images/challenges.svg";
import leaderboard from "../../src/assets/images/leaderboard.svg";
```

### Description

- **`sortBy`**: A utility function from lodash used for sorting arrays.
- **`challengePermissionsGames`, `checkIfGamePermissionIsAvailable`, etc.**: Functions and constants imported from `permissionConstant` which are used to verify and retrieve user permissions.
- **`challenges`, `leaderboard`**: SVG image imports for icons associated with specific permissions.

## Functions

### PermissionPath

```javascript
function PermissionPath() {
    const obj = JSON.parse(localStorage.getItem("authUser"));
    const notFound = obj === null ? true : obj.extras?.permissions.some((dataCheck) => {
        return dataCheck.label === "Static Page";
    });
    const gamePermissions = checkIfGamePermissionIsAvailable(obj);
    const path = retirevePath(
        obj, 
        notFound, 
        permissionConstant, 
        permissionConstantSecond 
    );

    let newPath = gamePermissions.length != 0 ? [...path, [permissionGameConstantForLobbies[0]]] : path;
    const challengePath = challengePermissionsGames(gamePermissions);

    const chal = [
        {
            permissionName: "Challenges",
            pathname: "/challenges",
            label: "Challenges",
            icon: challenges,
            order: 15,
        },
        {
            permissionName: "Leaderboard",
            pathname: "/leaderboard",
            label: "Leaderboard",
            icon: leaderboard,
            order: 17,
        },
    ];

    newPath = challengePath.length ? [...newPath, chal] : newPath;

    if (newPath === null || newPath === "/login") {
        return null;
    } else if (newPath !== null || newPath !== "/login") {
        const extractArrayOfArrayPath = [];
        newPath.forEach((data) =>
            data.forEach((destructure) =>
                extractArrayOfArrayPath.push(destructure)
            )
        );
        const sortResult = sortBy(extractArrayOfArrayPath, ["order"], ["asc"]);
        return sortResult;
    } else {
        const extractArrayOfArrayPath = [];
        newPath.forEach((data) =>
            data.forEach((destructure) =>
                extractArrayOfArrayPath.push(destructure)
            )
        );
        return extractArrayOfArrayPath;
    }
}
```

### Description

- **`PermissionPath`**: This function performs the main logic of determining the navigation path based on user permissions.
  - It checks the current user's permissions from `localStorage`.
  - Utilizes helper functions to determine available game permissions and retrieve paths.
  - Constructs a new path array with additional permissions for `Challenges` and `Leaderboard`.
  - Sorts the final path array based on the `order` attribute for organized navigation.

## Usage

The `PermissionPath` function is essential for dynamically constructing a user's accessible routes within an application based on their permissions. It helps in generating a structured and sorted path for navigation purposes, allowing a tailored user experience.

## Exports

```javascript
export default PermissionPath;
```

### Description

- **`PermissionPath`**: The default export is the `PermissionPath` function, which can be imported and used in other parts of the application to determine user navigation paths.

This documentation provides a comprehensive understanding of the `PermissionPath.js` file, detailing its purpose, functionality, and how it integrates with other parts of the application.

# Documentation for `local_to_utc.js` 📅🌐

## Overview
The `local_to_utc.js` file contains a single utility function, `DateToUtc`, designed to convert a local date and time to Coordinated Universal Time (UTC). This function is useful for applications that need to handle and store date-time information consistently, no matter the user's local timezone.

## Function Details

### `DateToUtc(date, time)`
Transforms a local date and time into UTC date and time.

#### Parameters
- **`date`**: A string representing the local date in the format `YYYY-MM-DD`.
- **`time`**: A string representing the local time in the format `HH:MM:SS`.

#### Returns
- An object containing:
  - **`date`**: A string representing the UTC date in the format `YYYY-MM-DD`.
  - **`time`**: A string representing the UTC time in the format `HH:MM:SS`.

#### How it Works
1. The function concatenates the `date` and `time` strings with a timezone offset (`-04:00`), creating a full date-time string.
2. A `Date` object is created using this string.
3. The function extracts the UTC year, month, day, hours, minutes, and seconds from the `Date` object.
4. It returns an object with the UTC date and time.

#### Example Usage

```javascript
import DateToUtc from './local_to_utc';

const localDate = "2023-10-12";
const localTime = "14:30:00";
const utcDateTime = DateToUtc(localDate, localTime);

console.log(utcDateTime);
// Output might be: { date: "2023-10-12", time: "18:30:00" }
```

## Notes 🗒️
- The function assumes the local time is in the `-04:00` timezone. This is a hardcoded value and should be adjusted if the application needs to support different local timezones.
- The handling of daylight saving time changes is not considered in this simple conversion.
- When using this in a real-world application, ensure that input dates and times are validated to avoid runtime errors.

## Conclusion
The `DateToUtc` function provides a straightforward way to convert local times to UTC, which is essential for timestamp consistency in global applications. Adjustments may be necessary depending on the specific requirements of your application, especially regarding timezone handling.

# `SearchPath.js` Documentation 📜💻

## Overview
The `SearchPath.js` module is a utility designed to filter and retrieve the allowable paths for a user based on their permissions. It utilizes a helper function `PermissionPath` to gather all possible paths and filters them against a provided list of user routes. This ensures that users only access paths they have permissions for.

## Code Explanation

### Imports

```javascript
import PermissionPath from "./PermissionPath";
```

- The module imports the `PermissionPath` function from `PermissionPath.js` which is responsible for retrieving paths based on user permissions.

### Main Function

```javascript
function SearchPath(userRoutes) {
```

- **Purpose**: The primary function of this module. It determines and returns the paths a user is allowed to access.

### Function Logic

1. **Retrieve All Paths**:

   ```javascript
   const allPath = PermissionPath();
   ```

   - Calls the `PermissionPath` function to get all paths related to the user's permissions.

2. **Handle Special Cases**:

   ```javascript
   if (allPath == "/login") {
       return;
   } else if (allPath === null) {
       return;
   }
   ```

   - If `allPath` is `"/login"` or `null`, the function exits early. This could imply that the user is not authenticated or lacks permissions to view any path.

3. **Filter User-Allowed Paths**:

   ```javascript
   else {
       const filterPath = [];
       allPath?.filter( (elem) => !userRoutes.find((data) => {
           if (elem?.pathname == data.commonName) {
               filterPath.push(data);
           }
       }));
   ```

   - For each path in `allPath`, check if it exists in `userRoutes`. If it does, add it to `filterPath`.
   - `filterPath` is built by checking the presence of `elem.pathname` in `data.commonName` from `userRoutes`.

4. **Return Allowed Paths**:

   ```javascript
   const allowedPathForUser = [filterPath];
   return allowedPathForUser;
   ```

   - `allowedPathForUser` is an array containing `filterPath`.
   - The function returns `allowedPathForUser`, representing the paths a user can access.

### Export

```javascript
export default SearchPath;
```

- The `SearchPath` function is exported as the default export of this module, making it available for use in other parts of the application.

## Usage

To use the `SearchPath` function, you pass it a list of routes (`userRoutes`) and it will return the paths the user is permitted to navigate.

```javascript
import SearchPath from './SearchPath';

const userRoutes = [
  { commonName: '/home' },
  { commonName: '/dashboard' },
  // ... other routes
];

const accessiblePaths = SearchPath(userRoutes);
console.log(accessiblePaths);
```

## Conclusion

`SearchPath.js` is a concise utility that leverages user permissions to filter through available paths, ensuring that users only access what they are authorized to. It is a critical part of managing user navigation and maintaining security within an application. 🚀🔒

# Documentation for `PermissionUtils.js`

The `PermissionUtils.js` file is a utility module designed to manage and handle permissions within a React application. It helps in filtering, determining, and setting paths based on user permissions. This file is essential for ensuring that users only have access to the routes and components they are authorized to view or interact with.

## Table of Contents

1. [Overview](#overview)
2. [Functions](#functions)
3. [Usage](#usage)
4. [Code Breakdown](#code-breakdown)
5. [Exported Functions](#exported-functions)

---

## Overview

This module imports several constants and components, and utilizes them to manage user permissions. It ensures that only the allowed paths and components are rendered based on the user's permissions stored in local storage.

## Functions

### Main Functions:

1. **filterOutPermissionToShowHide**: Checks if a given permission type should be shown or hidden.
2. **findPathsBetweenTwo**: Finds and returns the allowed paths between two sets of routes based on user permissions.
3. **newData**: Generates new permission paths based on game permissions.
4. **filterDefaultViewPermissions**: Filters out default view permissions from the given permissions.
5. **givenAndUploadpermission**: Adds or removes a permission based on presence and type.
6. **defaultViewPermission**: Adjusts the default view permissions based on the type.
7. **assignDefaultViewPermission**: Assigns default view permissions if not already assigned.
8. **deleteGivenPermission**: Deletes a given permission if it matches certain criteria.
9. **findViewPermissionId**: Finds and filters out a specific view permission ID.
10. **givenAndUploadpermissionRadio**: Manages permissions for radio button interfaces, ensuring only appropriate permissions are assigned.
11. **checkForAllowedPermission**: Verifies and adjusts permissions based on allowed permissions.
12. **defaultCheckedPermissions**: Determines if a permission should be marked as checked based on its type and presence.

## Usage

This utility module is used in scenarios where permission-based rendering and routing are required. It is particularly useful in applications with role-based access control, ensuring that users only access features they are permitted to use.

## Code Breakdown

### Imports

- **React Router**: Utilizes `Redirect` from `react-router-dom` for redirecting unauthorized users.
- **Permissions & Constants**: Imports various helper functions and constants related to permissions from `permissionConstant`.
- **Components**: Imports several React components for routing and rendering based on permissions.

### Core Logic

- **Permission Handling**: The module checks user permissions stored in local storage, determining which routes and components are accessible.
- **Dynamic Routing**: Based on the permissions, it dynamically generates routes and components that should be accessible to the user.
- **Permission Filtering**: Implements numerous helper functions to filter and adjust permissions, ensuring accurate and secure access control.

### Example

Here's a brief example of how some functions work:

```javascript
export const findPathsBetweenTwo = (userRoutes1) => {
  const allPath = PermissionPath(); // Retrieves all paths based on permissions
  const obj = JSON.parse(localStorage.getItem("authUser"));
  const filterPath = []; // Array to hold filtered paths

  // Check if user is logged in
  if (data == "/login" || data == null) {
    return null;
  } else {
    // Iterate through user routes and filter based on permissions
    finalRoutes.forEach((route) => {
      data.forEach((permission) => {
        if (route.codename === permission.codename) {
          filterPath.push(route);
        }
      });
    });

    // Additional logic for handling game and challenge routes
    const gamePermissions = checkIfGamePermissionIsAvailable(obj);
    const challengePath = challengePermissionsGames(gamePermissions);
    let challengePaths = challengePath.length ? [{ /* ... */ }] : [];

    // Return allowed paths for the user
    const allowedPathForUser = [...filterPath, ...b];
    return allowedPathForUser;
  }
};
```

## Exported Functions

- **filterOutPermissionToShowHide**
- **findPathsBetweenTwo**
- **newData**
- **filterDefaultViewPermissions**
- **givenAndUploadpermission**
- **defaultViewPermission**
- **assignDefaultViewPermission**
- **deleteGivenPermission**
- **findViewPermissionId**
- **givenAndUploadpermissionRadio**
- **checkForAllowedPermission**
- **defaultCheckedPermissions**

These utility functions are crucial for handling permission logic within the application, allowing for flexible and secure access control.

---

This comprehensive overview of `PermissionUtils.js` should provide a clear understanding of its role and functionality within the application. If you're implementing or modifying permission logic, this module is central to ensuring that users only access what they are permitted to.

# Documentation for `PermissionUtils.js`

The `PermissionUtils.js` file is a utility module designed to manage and handle permissions within a React application. It helps in filtering, determining, and setting paths based on user permissions. This file is essential for ensuring that users only have access to the routes and components they are authorized to view or interact with.

## Table of Contents

1. [Overview](#overview)
2. [Functions](#functions)
3. [Usage](#usage)
4. [Code Breakdown](#code-breakdown)
5. [Exported Functions](#exported-functions)

---

## Overview

This module imports several constants and components, and utilizes them to manage user permissions. It ensures that only the allowed paths and components are rendered based on the user's permissions stored in local storage.

## Functions

### Main Functions:

1. **filterOutPermissionToShowHide**: Checks if a given permission type should be shown or hidden.
2. **findPathsBetweenTwo**: Finds and returns the allowed paths between two sets of routes based on user permissions.
3. **newData**: Generates new permission paths based on game permissions.
4. **filterDefaultViewPermissions**: Filters out default view permissions from the given permissions.
5. **givenAndUploadpermission**: Adds or removes a permission based on presence and type.
6. **defaultViewPermission**: Adjusts the default view permissions based on the type.
7. **assignDefaultViewPermission**: Assigns default view permissions if not already assigned.
8. **deleteGivenPermission**: Deletes a given permission if it matches certain criteria.
9. **findViewPermissionId**: Finds and filters out a specific view permission ID.
10. **givenAndUploadpermissionRadio**: Manages permissions for radio button interfaces, ensuring only appropriate permissions are assigned.
11. **checkForAllowedPermission**: Verifies and adjusts permissions based on allowed permissions.
12. **defaultCheckedPermissions**: Determines if a permission should be marked as checked based on its type and presence.

## Usage

This utility module is used in scenarios where permission-based rendering and routing are required. It is particularly useful in applications with role-based access control, ensuring that users only access features they are permitted to use.

## Code Breakdown

### Imports

- **React Router**: Utilizes `Redirect` from `react-router-dom` for redirecting unauthorized users.
- **Permissions & Constants**: Imports various helper functions and constants related to permissions from `permissionConstant`.
- **Components**: Imports several React components for routing and rendering based on permissions.

### Core Logic

- **Permission Handling**: The module checks user permissions stored in local storage, determining which routes and components are accessible.
- **Dynamic Routing**: Based on the permissions, it dynamically generates routes and components that should be accessible to the user.
- **Permission Filtering**: Implements numerous helper functions to filter and adjust permissions, ensuring accurate and secure access control.

### Example

Here's a brief example of how some functions work:

```javascript
export const findPathsBetweenTwo = (userRoutes1) => {
  const allPath = PermissionPath(); // Retrieves all paths based on permissions
  const obj = JSON.parse(localStorage.getItem("authUser"));
  const filterPath = []; // Array to hold filtered paths

  // Check if user is logged in
  if (data == "/login" || data == null) {
    return null;
  } else {
    // Iterate through user routes and filter based on permissions
    finalRoutes.forEach((route) => {
      data.forEach((permission) => {
        if (route.codename === permission.codename) {
          filterPath.push(route);
        }
      });
    });

    // Additional logic for handling game and challenge routes
    const gamePermissions = checkIfGamePermissionIsAvailable(obj);
    const challengePath = challengePermissionsGames(gamePermissions);
    let challengePaths = challengePath.length ? [{ /* ... */ }] : [];

    // Return allowed paths for the user
    const allowedPathForUser = [...filterPath, ...b];
    return allowedPathForUser;
  }
};
```

## Exported Functions

- **filterOutPermissionToShowHide**
- **findPathsBetweenTwo**
- **newData**
- **filterDefaultViewPermissions**
- **givenAndUploadpermission**
- **defaultViewPermission**
- **assignDefaultViewPermission**
- **deleteGivenPermission**
- **findViewPermissionId**
- **givenAndUploadpermissionRadio**
- **checkForAllowedPermission**
- **defaultCheckedPermissions**

These utility functions are crucial for handling permission logic within the application, allowing for flexible and secure access control.

---

This comprehensive overview of `PermissionUtils.js` should provide a clear understanding of its role and functionality within the application. If you're implementing or modifying permission logic, this module is central to ensuring that users only access what they are permitted to.

# Documentation for `url_helper.js` 📜

## Overview
The `url_helper.js` file serves as a centralized location for defining and exporting API endpoint constants used across the application. These constants are utilized to standardize and manage the URLs for various backend services, ensuring that any changes to the endpoints are easily manageable within a single file. This approach enhances maintainability and reduces the risk of errors that might occur from hardcoding URLs in different parts of the application.

## Table of Contents
- [Register Endpoints](#register-endpoints)
- [Login Endpoints](#login-endpoints)
- [Profile Endpoints](#profile-endpoints)
- [Products Endpoints](#products-endpoints)
- [Calendar Endpoints](#calendar-endpoints)
- [Chats Endpoints](#chats-endpoints)
- [Orders Endpoints](#orders-endpoints)
- [Cart Data Endpoints](#cart-data-endpoints)
- [Customers Endpoints](#customers-endpoints)
- [Shops Endpoints](#shops-endpoints)
- [Crypto Endpoints](#crypto-endpoints)
- [Invoices Endpoints](#invoices-endpoints)
- [Projects Endpoints](#projects-endpoints)
- [Tasks Endpoints](#tasks-endpoints)
- [Contacts Endpoints](#contacts-endpoints)

---

### Register Endpoints 🔑
- **POST_FAKE_REGISTER**: `/post-fake-register`
  - Used for fake user registration.

### Login Endpoints 🔓
- **POST_FAKE_LOGIN**: `/post-fake-login`
  - Fake login endpoint.
- **POST_FAKE_JWT_LOGIN**: `/post-jwt-login`
  - JWT login endpoint.
- **POST_FAKE_PASSWORD_FORGET**: `/fake-forget-pwd`
  - Endpoint for fake password recovery.
- **POST_FAKE_JWT_PASSWORD_FORGET**: `/jwt-forget-pwd`
  - JWT password recovery endpoint.
- **SOCIAL_LOGIN**: `/social-login`
  - Endpoint for social media login.

### Profile Endpoints 👤
- **POST_EDIT_JWT_PROFILE**: `/post-jwt-profile`
  - Endpoint to edit profile with JWT authentication.
- **POST_EDIT_PROFILE**: `/post-fake-profile`
  - Endpoint to edit fake profile.

### Products Endpoints 🛒
- **GET_PRODUCTS**: `/products`
  - Fetch all products.
- **GET_PRODUCTS_DETAIL**: `/product`
  - Fetch details of a specific product.

### Calendar Endpoints 📅
- **GET_EVENTS**: `/events`
  - Fetch all calendar events.
- **ADD_NEW_EVENT**: `/add/event`
  - Add a new calendar event.
- **UPDATE_EVENT**: `/update/event`
  - Update an existing calendar event.
- **DELETE_EVENT**: `/delete/event`
  - Delete a calendar event.
- **GET_CATEGORIES**: `/categories`
  - Fetch event categories.

### Chats Endpoints 💬
- **GET_CHATS**: `/chats`
  - Fetch all chat conversations.
- **GET_GROUPS**: `/groups`
  - Fetch all chat groups.
- **GET_CONTACTS**: `/contacts`
  - Fetch all chat contacts.
- **GET_MESSAGES**: `/messages`
  - Fetch all messages in a conversation.
- **ADD_MESSAGE**: `/add/messages`
  - Add a new message to a conversation.

### Orders Endpoints 🧾
- **GET_ORDERS**: `/orders`
  - Fetch all orders.

### Cart Data Endpoints 🛍️
- **GET_CART_DATA**: `/cart`
  - Fetch all items in the shopping cart.

### Customers Endpoints 🧑‍🤝‍🧑
- **GET_CUSTOMERS**: `/customers`
  - Fetch all customer profiles.

### Shops Endpoints 🏪
- **GET_SHOPS**: `/shops`
  - Fetch all shop details.

### Crypto Endpoints 💰
- **GET_WALLET**: `/wallet`
  - Fetch wallet details.
- **GET_CRYPTO_ORDERS**: `/crypto/orders`
  - Fetch all cryptocurrency orders.

### Invoices Endpoints 📄
- **GET_INVOICES**: `/invoices`
  - Fetch all invoices.
- **GET_INVOICE_DETAIL**: `/invoice`
  - Fetch details of a specific invoice.

### Projects Endpoints 📊
- **GET_PROJECTS**: `/projects`
  - Fetch all projects.
- **GET_PROJECT_DETAIL**: `/project`
  - Fetch details of a specific project.

### Tasks Endpoints 📋
- **GET_TASKS**: `/tasks`
  - Fetch all tasks.

### Contacts Endpoints 📇
- **GET_USERS**: `/users`
  - Fetch all user contacts.
- **GET_USER_PROFILE**: `/user`
  - Fetch details of a specific user profile.

---

## Conclusion
This file is a crucial part of the application where all the RESTful API endpoints are managed. Having these constants in one place makes it easier to maintain and update the URLs without having to search through the entire codebase. It's a good practice to use such helper files for better code management and scalability.

# StringConstant.js Documentation

Welcome to the **StringConstant.js** module documentation. This file serves as a centralized location for various string constants used across the application. These constants are primarily used for permissions, game types, success messages, error messages, and other common strings. By using constants, we ensure consistency and ease of maintenance throughout the codebase.

---

## Table of Contents

1. [Permissions Strings](#permissions-strings)
2. [Game Type](#game-type)
3. [Success Messages](#success-messages)
4. [Error Messages](#error-messages)
5. [General Messages](#general-messages)
6. [Constant Strings](#constant-strings)

---

## Permissions Strings

These constants are used to manage user permissions for various sections of the application.

| Constant Name           | Value                        | Description                                 |
|-------------------------|------------------------------|---------------------------------------------|
| `userList`              | `"Users"`                    | Represents the user list section.           |
| `typeUserListView`      | `"view_user"`                | Permission to view the user list.           |
| `staticPage`            | `"Static Page"`              | Represents static page management.          |
| `PPKFAQ`                | `"PPK & FAQ"`                | Represents policy and FAQ management.       |
| `typeStaticPageChange`  | `"change_staticpage"`        | Permission to change static pages.          |
| `typeStaticPageView`    | `"view_staticpage"`          | Permission to view static pages.            |
| `typePPKFAQChange`      | `"change_question"`          | Permission to change FAQ questions.         |
| `typePPKFAQView`        | `"view_question"`            | Permission to view FAQ questions.           |
| `typePPKFAQAdd`         | `"add_question"`             | Permission to add new FAQ questions.        |
| `typePPKFAQDelete`      | `"delete_question"`          | Permission to delete FAQ questions.         |
| ...                     | ...                          | ...                                         |

## Game Type

Defines the types of games available in the application.

| Constant Name | Value            | Description                                |
|---------------|------------------|--------------------------------------------|
| `gameTypePPW` | `"Pay Per Win"`  | Represents a Pay Per Win type of game.     |

## Success Messages

These constants are used to display success messages to the user after performing specific actions.

| Constant Name              | Value                                                            | Description                                   |
|----------------------------|------------------------------------------------------------------|-----------------------------------------------|
| `gameDemoSuccess`          | `"Game demo updated successfully"`                               | Message shown when a game demo is updated.    |
| `gameDemoDeleteSuccess`    | `"Game demo deleted successfully"`                               | Message shown when a game demo is deleted.    |
| `imageSuccess`             | `"Image uploaded successfully"`                                  | Message shown when an image is uploaded.      |
| `gameDemoAddSuccess`       | `"Game demo has been added successfully"`                        | Message shown when a game demo is added.      |
| `updateSuccess`            | `"Updated successfully"`                                         | Generic success update message.               |
| `communitySuccess`         | `"Community video has been deleted successfully"`                | Community video deletion success message.     |
| `addedSuccess`             | `"Added successfully"`                                           | Generic success addition message.             |
| `deletedSuccess`           | `"Deleted successfully"`                                         | Generic success deletion message.             |
| `tAndcAddSuccess`          | `"Terms and Conditions added successfully"`                      | Message shown when T&C are added.             |
| `tAndcUpdatedSuccess`      | `"Terms and Conditions updated successfully"`                    | Message shown when T&C are updated.           |
| `ppAddSuccess`             | `"Privacy policy added successfully"`                            | Message shown when a privacy policy is added. |
| `ppUpdatedSuccess`         | `"Privacy policy updated successfully"`                          | Message shown when a privacy policy is updated.|
| `cpAddSuccess`             | `"California privacy added successfully"`                        | Message shown when California privacy is added.|
| `cpUpdatedSuccess`         | `"California privacy updated successfully"`                      | Message shown when California privacy is updated.|

## Error Messages

Constants for error messages to be displayed to the user.

| Constant Name        | Value                                      | Description                                       |
|----------------------|--------------------------------------------|---------------------------------------------------|
| `validFile`          | `"Please select a valid Image file."`     | Error message for invalid image file selection.   |
| `validGame`          | `"Please select game."`                   | Error message when no game is selected.           |
| `addContent`         | `"Please add some content"`               | Error message when content is missing.            |
| `lobbyRequired`      | `"Lobby name is required"`                | Error message when a lobby name is missing.       |
| `usernameRequired`   | `"Username is required"`                  | Error message when a username is missing.         |

## General Messages

These are miscellaneous messages used throughout the application.

| Constant Name          | Value                                                       | Description                                   |
|------------------------|-------------------------------------------------------------|-----------------------------------------------|
| `InactivityReminder`   | `"Inactivity Reminder value can't be more than Inactivity Timeline value"` | Message for inactivity settings.              |
| `communityM`           | `"Community"`                                               | General community message.                    |
| `communityU`           | `"Updated"`                                                 | General updated message.                      |
| `communityA`           | `"Added"`                                                   | General added message.                        |
| `communityS`           | `"Successfully"`                                            | General success message.                      |

## Constant Strings

These constants represent commonly used strings in the application.

| Constant Name   | Value                     | Description                                      |
|-----------------|---------------------------|--------------------------------------------------|
| `tANDc`         | `"Terms and Conditions"`  | Represents the Terms and Conditions section.     |
| `PP`            | `"Privacy policy"`        | Represents the Privacy Policy section.           |
| `CP`            | `"California privacy"`    | Represents the California Privacy section.       |

---

By using these constants, developers can ensure that the application remains consistent and easier to maintain, especially when dealing with multiple occurrences of the same strings across different files. 🎉

# 📄 `FilterPermission.js` Documentation

## Overview
The `FilterPermission.js` file contains a simple utility function designed to filter out permissions based on a specified type. This function is useful when you need to segregate or identify specific permissions from a set of permissions data, likely in a user authentication or authorization context.

## Function: `FilterPermission`
This file exports a single function `FilterPermission` which takes two arguments:

- **Parameters**:
  - `permission`: An array of permission objects. Each object is expected to have at least a `label` property.
  - `type`: A string against which each permission's label is compared.

- **Returns**: 
  - An array of permission objects whose `label` matches the specified `type`.

### Code Explanation
```javascript
function FilterPermission(permission, type) {
  return permission.filter((data) => data.label == type);
}

export default FilterPermission;
```

### How It Works
- **Filtering Logic**: The function iterates over the `permission` array and applies the `filter` method. For each element (object) in the array, it checks if the `label` property matches the `type` provided.
- **Equality Check**: It uses a strict equality comparison (`==`) to ensure that only permissions with a matching label are included in the returned array.

### Usage Example
Suppose you have a list of permissions, and you want to filter out only those that are of type "admin":

```javascript
const permissions = [
  { label: "user", access: "read" },
  { label: "admin", access: "write" },
  { label: "guest", access: "read" }
];

const adminPermissions = FilterPermission(permissions, "admin");
console.log(adminPermissions); 
// Output: [{ label: "admin", access: "write" }]
```

### Notes
- **Case Sensitivity**: The function uses a strict equality check, meaning that the comparison is case-sensitive. Ensure that the `type` argument matches the case of the `label` in the permissions array.

- **Potential Enhancements**: 
  - **Type Checking**: Additional type checking could be added to ensure that inputs are as expected.
  - **Error Handling**: Consider adding error handling for cases where `permission` might not be an array.

### Conclusion
The `FilterPermission` function is a straightforward and efficient way to filter a list of permissions by a specific type. Its simplicity makes it easy to integrate into larger authentication and authorization logic where permissions need to be categorized or accessed selectively.

# Documentation for `util.js`

Welcome to the documentation for the `util.js` file! This file contains a variety of utility functions and constants that are used throughout the application. These utilities help with tasks such as password generation, date formatting, and tournament management. Below you'll find a detailed description of each function and constant available in this file.

## Table of Contents
- [Constants](#constants)
  - [Password and Characters](#password-and-characters)
  - [Game Statistics Table Headings](#game-statistics-table-headings)
  - [Game Type Enums](#game-type-enums)
  - [Competition Status](#competition-status)
  - [Dropdown Options](#dropdown-options)
  - [Game and Challenges Mapping](#game-and-challenges-mapping)
  - [Bracket Styles and Seeding Options](#bracket-styles-and-seeding-options)
- [Functions](#functions)
  - [randomPasswordGenerator](#randompasswordgenerator)
  - [convertDateToHyphenFormat](#convertdatetohyphenformat)
  - [createPrizeTable](#createprizetable)
  - [createMatchesTable](#creatematchestable)
  - [getEstDateObj](#getestdateobj)
  - [compareDatesDDMMYYYY](#comparedatesddmmyyyy)
  - [checkTimeDifference](#checktimedifference)
  - [getCurrentTimeESTWithTournamentLastEntryBufferMinutesAhead](#getcurrenttimeestwithtournamentlastentrybufferminutesahead)
  - [Date and Time Helpers](#date-and-time-helpers)
  - [Miscellaneous Helpers](#miscellaneous-helpers)

---

## Constants

### Password and Characters
- **`passwordCharacterData`**: An array of characters used for generating passwords, including uppercase, lowercase, numbers, and symbols.
- **`charactersForRandomText`**: An array of characters used for generating random text, comprising uppercase, lowercase, and numbers.

### Game Statistics Table Headings
- **`gameStatsTableHeadForApex`**: Defines the column headers for Apex game statistics.
- **`gameStatsTableHeadForValorant`**: Defines the column headers for Valorant game statistics.

### Game Type Enums
- **`gameTypeEnumForChallenges`**: Enum mapping game type IDs to their respective names (e.g., PPK, Kill Race, Traditional).

### Competition Status
- **`competitionStatus`**: Maps competition status IDs to their status names (e.g., Upcoming, Active, Ended).

### Dropdown Options
- **`dropdownOptions`**: Options for sorting users by username, email, and creation date.
- **`DropDownOptionsChallenges`**: Options for sorting challenges by match date and type.
- **`dropdownOptionsForChallengeMode`**: Options indicating the challenge mode, such as Open or Team.
- **`challengesStatusOption`**: Options for challenge status, such as Active or Cancelled.

### Game and Challenges Mapping
- **`GAME_MAP_CHALLENGES`**: Maps game slugs to their respective labels and permission types.

### Bracket Styles and Seeding Options
- **`bracketStyleOptionsTraditonal`**: Options for traditional tournament bracket styles.
- **`seedingOptions`**: Options for seeding in tournaments, such as Qualifiers and Manual Placement.

---

## Functions

### `randomPasswordGenerator`
Generates a random password of specified length using the provided character set.

```javascript
export const randomPasswordGenerator = ({ passWordLength, data }) => { ... }
```

### `convertDateToHyphenFormat`
Converts a date into the format `YYYY-MM-DD`.

```javascript
export const convertDateToHyphenFormat = (fieldDate) => { ... }
```

### `createPrizeTable`
Creates a prize table based on a given count and data. Each entry includes position and price.

```javascript
export const createPrizeTable = (count, data) => { ... }
```

### `createMatchesTable`
Generates a list of match objects with default settings, including ID and match name.

```javascript
export const createMatchesTable = (count) => { ... }
```

### `getEstDateObj`
Returns a Date object adjusted to the specified time zone.

```javascript
export const getEstDateObj = (date, timeZone) => { ... }
```

### `compareDatesDDMMYYYY`
Compares two dates formatted as `DD-MM-YYYY` and returns an integer indicating which is greater.

```javascript
export const compareDatesDDMMYYYY = (date1, date2) => { ... }
```

### `checkTimeDifference`
Checks the difference between a start time and the user's selected time to determine if it's more than two hours apart.

```javascript
export const checkTimeDifference = (start, userDate) => { ... }
```

### `getCurrentTimeESTWithTournamentLastEntryBufferMinutesAhead`
Returns the current time in EST adjusted by a buffer.

```javascript
export const getCurrentTimeESTWithTournamentLastEntryBufferMinutesAhead = () => { ... }
```

### Date and Time Helpers
- **`getEstDate`**: Fetches the current date in EST.
- **`getEstDateToConvert`**: Converts a given date to EST format.
- **`compareDateTournament`**: Compares a tournament date with the current date adjusted by a buffer.

### Miscellaneous Helpers
- **`filterLabel`**: Filters objects by a given label.
- **`csvConverterToPreviewFile`**: Converts CSV files into a preview format.
- **`dateFormat`**: Formats a date into a readable string.
- **`getFromLocalStorage`**: Safely retrieves an item from local storage.

---

This concludes the documentation for the `util.js` file. With these utilities, you can streamline various operations in your application! 🛠️

# accessToken.js Documentation

## Overview

The `accessToken.js` file is a simple JavaScript module that exports a constant string representing a Bearer token used for authentication purposes. This token is typically used to authenticate requests made to an API, where the token is included in the HTTP header to verify the user's identity and permissions.

## Contents

- [Code Explanation](#code-explanation)
- [Usage](#usage)
- [Security Note](#security-note)

## Code Explanation

```javascript
const accessToken = "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6ImFkbWluIiwiYWRtaW4iOnRydWUsImp0aSI6ImQ2MTEwYzAxLWMwYjUtNDUzNy1iNDZhLTI0NTk5Mjc2YjY1NiIsImlhdCI6MTU5MjU2MDk2MCwiZXhwIjoxNTkyNTY0NjE5fQ.QgFSQtFaK_Ktauadttq1Is7f9w0SUtKcL8xCmkAvGLw";

export default accessToken;
```

### Breakdown

- **`const accessToken`:** This variable holds a JWT (JSON Web Token) as a string, prefixed by "Bearer ". This is a standard format for including tokens in HTTP Authorization headers.
- **Token Structure:**
  - **Header:** `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9` indicates the type of token and the signing algorithm used.
  - **Payload:** `eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6ImFkbWluIiwiYWRtaW4iOnRydWUsImp0aSI6ImQ2MTEwYzAxLWMwYjUtNDUzNy1iNDZhLTI0NTk5Mjc2YjY1NiIsImlhdCI6MTU5MjU2MDk2MCwiZXhwIjoxNTkyNTY0NjE5fQ` contains the claims, such as user ID, name, and roles.
  - **Signature:** `QgFSQtFaK_Ktauadttq1Is7f9w0SUtKcL8xCmkAvGLw` is used to verify that the token has not been altered.

- **`export default accessToken;`:** Exports the `accessToken` as the default export of this module, making it easy to import in other files.

## Usage

This token is typically used to authorize API requests. When making requests to a server, you include this token in the `Authorization` header to prove that the request is coming from an authenticated user:

```javascript
import accessToken from './accessToken';

// Example usage with fetch API
fetch('https://api.example.com/protected-endpoint', {
  method: 'GET',
  headers: {
    'Authorization': accessToken,
    'Content-Type': 'application/json'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

## Security Note

⚠️ **Important:** Hardcoding tokens in your source code, as shown here, is **not a recommended practice** for production applications. This is because it poses a security risk if the source code is ever exposed. Instead, consider using environment variables or secure storage solutions to manage sensitive data like tokens.

# Documentation for `auth-token-header.js`

## Overview
The `auth-token-header.js` file exports a function responsible for generating an authentication header containing a Bearer token. This header is typically used for making authenticated HTTP requests to APIs that require a token for user verification.

### Purpose
The primary function of this file is to retrieve an access token from the browser's local storage and format it into a Bearer token string that can be used in HTTP headers for authorized API requests.

## Function: `authHeader`

### Description
The `authHeader` function checks the local storage for authentication details and constructs a Bearer token string if an access token is found.

### Implementation

```javascript
export default function authHeader() {
    const obj = JSON.parse(localStorage.getItem("authUser"));
    if (obj && obj.extras.access_token) {
        return `Bearer ${obj.extras.access_token}`;
    } else {
        return null;
    }
}
```

### How It Works
- **Retrieving User Information**: The function attempts to retrieve the `authUser` object from the local storage. It assumes that this object contains user authentication details.
  
- **Token Verification**: It checks if the retrieved object exists and contains an `access_token` within its `extras` property.
  
- **Bearer Token Formatting**: If the token is present, it formats the token as a Bearer token string, which is a common format for API authentication headers.

- **Return Value**: The function returns the formatted Bearer token string if the token is available. Otherwise, it returns `null`.

### Use Case
This function is typically used in API helper functions or HTTP request configurations where authentication is required. It ensures that the correct authorization header is added when making requests to a secured API.

## Key Takeaways
- **Bearer Token**: A standard way of sending a security token in HTTP headers, prefixed with "Bearer".
- **Local Storage**: A common method for persisting user authentication information in a web application.
- **Error Handling**: The function gracefully handles the absence of an access token by returning `null`, allowing the calling code to handle authentication errors appropriately.

## Summary
The `auth-token-header.js` file is a straightforward utility for generating authorization headers. It simplifies the process of accessing protected resources by extracting and formatting tokens from local storage, ensuring that applications can seamlessly integrate secure API communication with minimal boilerplate code.

# Documentation for `authHeader.js`

## Overview

The `authHeader.js` file is a utility module that helps in generating authorization headers for HTTP requests. This is commonly used in web applications to handle authentication by passing a token in the request headers to authenticate API calls.

## Code Explanation

```javascript
export default function authHeader() {
    const obj = JSON.parse(localStorage.getItem("authUser"));
    if (obj && obj.extras.access_token) {
        return `Bearer ${obj.extras.access_token}`;
    } else {
        return null;
    }
}
```

### Functionality

- **Purpose**: The primary purpose of this function is to retrieve an authentication token from the browser's local storage and format it as an HTTP Authorization header.

- **Steps**:
    1. **Retrieve User Data**: The function attempts to fetch the `authUser` object from the local storage.
    2. **Parse the Object**: It parses this object using `JSON.parse()` to access its properties.
    3. **Check for Access Token**: It checks if the `extras` property of the object contains an `access_token`.
    4. **Return Header**: If the access token is available, it returns a formatted string `Bearer <token>`. If not, it returns `null`.

### Usage

- **Integration**: This function is designed to be used wherever you need to make authenticated HTTP requests. By providing the authorization header, you ensure that the server recognizes the user making the request.
  
- **Example**:
  ```javascript
  import authHeader from './authHeader';

  // Usage in an axios configuration
  axios.get('/some-endpoint', {
      headers: {
          'Authorization': authHeader()
      }
  });
  ```

### Key Considerations

- **Security**: Always ensure that access tokens are securely stored and handled. Tokens should not be exposed to unauthorized access.
  
- **Error Handling**: This function returns `null` if no token is available. The calling code should handle this case appropriately, such as redirecting to a login page or displaying an error message.

- **Local Storage**: The reliance on local storage means this utility is specific to browser environments and may not be suitable for server-side applications.

### Conclusion

The `authHeader.js` file provides a simple yet effective way to manage authentication headers for API requests in a web application. By encapsulating the logic in a single function, it helps maintain clean and consistent code across the application.

# Documentation for `paginator.js`

Welcome to the documentation for the `paginator.js` file! 📃✨ This file is a React component that handles pagination functionality using the `react-paginate` library. Pagination is crucial for breaking down large datasets into manageable chunks, allowing users to navigate through pages efficiently.

## Table of Contents
- [Overview](#overview)
- [Component: Paginator](#component-paginator)
- [Props](#props)
- [Usage](#usage)
- [Dependencies](#dependencies)
- [Code Explanation](#code-explanation)

## Overview
The `Paginator` component is designed to facilitate pagination in a React application. It leverages the `react-paginate` library to provide a user-friendly interface for navigating through paginated content. This component is particularly useful in scenarios where data is too extensive to be displayed on a single page.

## Component: Paginator
The `Paginator` is a functional component that renders a pagination interface. It provides navigational controls to the user, such as previous, next, and page numbers. The component dynamically determines the number of pages based on total data count and the number of items per page.

### Props
The `Paginator` component accepts the following props:

| Prop Name   | Type   | Description                                                  |
|-------------|--------|--------------------------------------------------------------|
| `totalCount`| Number | The total number of items to paginate through.               |
| `pageSize`  | Number | The number of items to display per page.                     |
| `forcePage` | Number | The current page to be highlighted as active.                |
| `pageClick` | Function | Callback function triggered when a page number is clicked. |

## Usage
To use the `Paginator` component, simply import it into your React component and provide the necessary props. Here's an example of how you might integrate it:

```jsx
import React, { useState } from 'react';
import Paginator from './paginator';

function ExampleComponent() {
  const [currentPage, setCurrentPage] = useState(1);

  const handlePageClick = (pageNumber) => {
    setCurrentPage(pageNumber);
    // Fetch data for the selected page
  };

  return (
    <div>
      <h1>Paginated Data</h1>
      {/* Your data rendering logic here */}
      <Paginator
        totalCount={100}
        pageSize={10}
        forcePage={currentPage}
        pageClick={handlePageClick}
      />
    </div>
  );
}
```

## Dependencies
The `Paginator` component depends on the following library:
- **react-paginate**: A ReactJS component that creates a pagination UI.

## Code Explanation
Let's break down the key parts of the code:

```jsx
import React from "react";
import ReactPaginate from "react-paginate";

const Paginator = (props) => {
  const handlePageChange = ({ selected }) => {
    props.pageClick(selected + 1);
  };

  return (
    <>
      <div className="mt-3">
        {props.totalCount > props.pageSize ? (
          <ReactPaginate
            forcePage={props.forcePage - 1}
            pageCount={props.totalCount / props.pageSize}
            pageRangeDisplayed={3}
            marginPagesDisplayed={1}
            previousLabel={"<"}
            nextLabel={">"}
            breakLabel={"..."}
            onPageChange={handlePageChange}
            containerClassName={"pagination"}
            pageClassName={"page-item"}
            pageLinkClassName={"page-link"}
            previousClassName={"page-item"}
            previousLinkClassName={"page-link"}
            nextClassName={"page-item"}
            nextLinkClassName={"page-link"}
            breakClassName={"page-link"}
            breakLinkClassName={"page-item"}
            activeClassName={"active"}
            activeLinkClassName={"active"}
            disabledClassName={"disabled"}
          />
        ) : null}
      </div>
    </>
  );
};

export default Paginator;
```

- **`handlePageChange`**: This function is triggered when a user clicks on a page number. It calls the `pageClick` prop with the selected page number.
- **`ReactPaginate` Component**: This component renders the pagination UI. It takes various props to customize the pagination controls, including `pageCount`, `onPageChange`, and CSS class names for styling.

## Conclusion
The `Paginator` component is a versatile tool for managing paginated data in React applications. By leveraging `react-paginate`, it provides a seamless user experience for navigating between pages. Customize it with your data and integrate it into your components for efficient pagination!

Happy coding! 🎉

# `PaginatorReport.js` Documentation 📄

## Overview
`PaginatorReport.js` is a React component that provides pagination functionality to navigate through a list of items. It utilizes the `react-paginate` library to implement a paginated interface. This component is specifically designed to handle pagination for reports, allowing users to easily navigate through pages of data.

## Key Features ✨
- **Pagination Control**: Allows users to navigate between pages of data.
- **Customizable**: Offers various props to customize pagination behavior and appearance.
- **Responsive Design**: Adapts to different screen sizes and maintains usability.

## Component Breakdown

### Imports
```javascript
import React from "react"; // Import React library
import ReactPaginate from "react-paginate"; // Import the react-paginate library
```

### Component Definition
```javascript
const PaginatorReport = (props) => {
```
This is a functional component that receives `props` to configure its behavior.

### Page Change Handler
```javascript
const handlePageChange = ({ selected }) => {
  props.pageClick(selected + 1);
};
```
- This function is called when the user selects a different page. It triggers the `pageClick` function passed through `props`, with the new page number.

### JSX Structure
```jsx
return (
  <>
    <div className="mt-3">
      {props.totalCount > props.pageSize ? (
        <ReactPaginate
          pageCount={props.totalCount / props.pageSize}
          pageRangeDisplayed={3}
          marginPagesDisplayed={1}
          previousLabel={"<"}
          nextLabel={">"}
          breakLabel={"..."}
          onPageChange={handlePageChange}
          forcePage={props.forcePage - 1}
          disableInitialCallback={true}
          containerClassName={"pagination"}
          pageClassName={"page-item"}
          pageLinkClassName={"page-link"}
          previousClassName={"page-item"}
          previousLinkClassName={"page-link"}
          nextClassName={"page-item"}
          nextLinkClassName={"page-link"}
          breakClassName={"page-link"}
          breakLinkClassName={"page-item"}
          activeClassName={"active"}
          activeLinkClassName={"active"}
          disabledClassName={"disabled"}
        />
      ) : null}
    </div>
  </>
);
```

#### Key Props for `ReactPaginate`
- **`pageCount`**: Total number of pages calculated by dividing `totalCount` by `pageSize`.
- **`pageRangeDisplayed`**: Number of page links to display.
- **`marginPagesDisplayed`**: Number of page links to display at the beginning and end of pagination.
- **`previousLabel` & `nextLabel`**: Labels for the previous and next buttons.
- **`onPageChange`**: Function to call when a page is changed.
- **`forcePage`**: Force a specific active page, adjusted by subtracting 1 from `props.forcePage`.
- **`disableInitialCallback`**: Disables the callback for the initial page load.
- **`containerClassName`**: CSS class for the pagination container.
- **`activeClassName`**: CSS class for the active page link.
- **`disabledClassName`**: CSS class for the disabled state.

### Export
```javascript
export default PaginatorReport;
```
The component is exported as the default export, making it available for import in other modules.

## Usage Example
To use the `PaginatorReport` component, you need to provide it with the necessary props, such as `totalCount`, `pageSize`, `forcePage`, and a `pageClick` handler function. Here's an example:

```jsx
import PaginatorReport from './PaginatorReport';

const MyComponent = () => {
  const handlePageClick = (pageNumber) => {
    console.log("Navigated to page:", pageNumber);
    // Fetch data for the selected page
  };

  return (
    <PaginatorReport
      totalCount={100}
      pageSize={10}
      forcePage={1}
      pageClick={handlePageClick}
    />
  );
};
```

## Conclusion
The `PaginatorReport` component provides a robust solution for implementing pagination in React applications, particularly for report-type data views. By leveraging the `react-paginate` library, it offers a flexible and user-friendly pagination interface.

# `paginatorReports.js` Documentation

## Overview
The `paginatorReports.js` file defines a React component `PaginatorReport` which renders a pagination control using the `react-paginate` library. This component is used to navigate through paginated data, especially in scenarios where reports or large lists need to be displayed in chunks.

## Component: `PaginatorReport`

### Props

The `PaginatorReport` component accepts the following props:

- **`pageClick`**: A function that is invoked when a page is selected. This function receives the page number as an argument.
- **`totalCount`**: The total number of items across all pages.
- **`pageSize`**: The number of items displayed per page.
- **`forcePage`**: (Optional) Sets the currently active page programmatically. It is zero-based.

### Functionality

- **`handlePageChange`**: A function that is called whenever a user selects a new page. It takes an object with a `selected` property, which represents the new page index (zero-based). This function then calls the `pageClick` prop function with the selected page number (one-based).

### Render

The component conditionally renders a `ReactPaginate` component if the `totalCount` is greater than the `pageSize`. This ensures pagination is only displayed when needed.

#### `ReactPaginate` Attributes

- **`pageCount`**: Calculated as `totalCount / pageSize`, determining the number of pages.
- **`pageRangeDisplayed`**: Number of page links to display.
- **`marginPagesDisplayed`**: Number of page links to display at the beginning and end of the pagination.
- **`previousLabel`**: Label for the previous page button, set to "<".
- **`nextLabel`**: Label for the next page button, set to ">".
- **`breakLabel`**: Label for the ellipsis between page numbers.
- **`onPageChange`**: The function to call when the page is changed.
- **`forcePage`**: Zero-based index of the page that should be selected.
- **`disableInitialCallback`**: Boolean to control if the initial callback should be disabled.
- **`containerClassName`, `pageClassName`, `pageLinkClassName`, etc.**: CSS class names for styling different parts of the pagination control.

### Example Usage

Here's an example of how you might use the `PaginatorReport` component in a React application:

```jsx
import React, { useState } from 'react';
import PaginatorReport from './paginatorReports';

const ReportPage = () => {
  const [currentPage, setCurrentPage] = useState(1);
  const totalItems = 100; // Example total items
  const itemsPerPage = 10;

  const handlePageClick = (pageNumber) => {
    setCurrentPage(pageNumber);
    // Fetch new data based on the page number
  };

  return (
    <div>
      <h1>Report</h1>
      {/* Report data display here */}
      <PaginatorReport
        pageClick={handlePageClick}
        totalCount={totalItems}
        pageSize={itemsPerPage}
        forcePage={currentPage}
      />
    </div>
  );
};

export default ReportPage;
```

### Styling

The component uses Bootstrap-like class names for styling pagination (`page-item`, `page-link`, `active`, `disabled`). Ensure your project includes appropriate CSS to style these classes.

## Conclusion

`PaginatorReport` is a flexible and easy-to-use component that simplifies paginating large datasets in a React application. It leverages the `react-paginate` library to provide a robust pagination UI, handling user interactions efficiently and allowing for customization through props.

# 📄 `toastr-options.js` Documentation

The `toastr-options.js` file is a configuration file that defines the default options for displaying toast notifications using the [react-toastify](https://github.com/fkhadra/react-toastify) library. This file exports a single object that specifies various properties to control the appearance and behavior of toast notifications. These settings are particularly useful for maintaining consistency across different toast notifications in a React application.

## 🌟 Features

- **Positioning**: Determines where on the screen the toast will appear.
- **Auto-Close**: Sets the duration after which the toast will automatically disappear.
- **Visual Elements**: Options for showing/hiding the progress bar and setting the theme.
- **Interactivity**: Allows interaction with the toast through clicks and hover actions.

## 📜 Configuration Options

Below is a table outlining the different configuration options available in `toastrOptions`:

| Option             | Type    | Default Value | Description                                                                 |
|--------------------|---------|---------------|-----------------------------------------------------------------------------|
| `position`         | String  | `top-right`   | Sets the position of the toast notification on the screen.                  |
| `autoClose`        | Number  | `3000`        | Time in milliseconds before the toast automatically closes.                 |
| `hideProgressBar`  | Boolean | `true`        | Hides the progress bar when set to `true`.                                  |
| `newestOnTop`      | Boolean | `false`       | Displays the newest toast on top when set to `true`.                        |
| `closeOnClick`     | Boolean | `true`        | Allows the toast to be dismissed by clicking on it.                         |
| `pauseOnHover`     | Boolean | `true`        | Pauses the auto-close timer when the toast is hovered upon.                 |
| `draggable`        | Boolean | `true`        | Makes the toast draggable across the screen.                                |
| `progress`         | `undefined` | | Not explicitly defined, allows customizing the progress bar animation.   |
| `pauseOnFocusLoss` | Boolean | `false`       | Continues the auto-close timer even when the window loses focus.            |
| `theme`            | String  | `colored`     | Sets the theme of the toast notification. Options include `light`, `dark`, `colored`, etc. |

## 🚀 Usage Example

To use the `toastrOptions` in your React application, you can import the configuration and pass it to the `toast` function provided by `react-toastify`:

```javascript
import { toast } from "react-toastify";
import toastrOptions from "./toastr-options";

// Display a success toast
toast.success("Operation Successful!", toastrOptions);

// Display an error toast
toast.error("An error occurred.", toastrOptions);
```

## 🛠️ Customization

You can customize the `toastrOptions` to fit the needs of your application. Simply modify the values in the object to change the behavior and appearance of the toast notifications.

Example of modifying the auto-close duration and enabling the progress bar:

```javascript
const customToastrOptions = {
  ...toastrOptions,
  autoClose: 5000,
  hideProgressBar: false,
};

toast.info("This is an info message!", customToastrOptions);
```

By using this configuration file, you ensure a consistent user experience across different notifications in your application. It allows for flexibility and ease of maintenance as your notification requirements evolve.