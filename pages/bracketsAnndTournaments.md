# TournamentDetails.jsx Documentation

## Overview

The `TournamentDetails.jsx` component is a React component designed to display and manage the details of a tournament. This component is structured to provide a comprehensive view of tournament information, including details, schedule, match info, standings, and enrolled teams. It leverages various tabs to organize this information in a user-friendly interface.

---

## Table of Contents

1. [Imports](#imports)
2. [Component Definition](#component-definition)
3. [State Variables](#state-variables)
4. [Lifecycle Methods](#lifecycle-methods)
5. [Helper Functions](#helper-functions)
6. [Render Method](#render-method)
7. [Export](#export)
8. [Dependencies](#dependencies)

---

## Imports

The component imports several libraries and components to function:

- **React & react-router-dom**: For component creation and routing functionalities.
- **reactstrap**: For UI components like Cards, Rows, and Columns.
- **classnames**: For conditional class names.
- **Custom Components**: Such as `Breadcrumbs`, `GoBack`, and various tab components.
- **Helpers**: For permission filtering and data fetching.

```jsx
import React, { useEffect, useState } from "react";
import { withRouter } from "react-router-dom";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Card, CardBody, Col, Row, NavLink, NavItem, Nav, TabContent, TabPane } from "reactstrap";
import classnames from "classnames";
import FilterPermission from "../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils";
import { getTournamentsById } from "../../services/bracket_tournaments_api_helper";
import { GoBack } from "../../components/GoBack";
import TournamentDetailsTab from "./Tabs/TournamentDetailsTab";
import ScheduleTab from "./Tabs/ScheduleTab";
import StandingsTab from "./Tabs/StandingsTab";
import TeamsTab from "./Tabs/TeamsTab";
import MatchInfoTab from "./Tabs/MatchInfoTab";
```

---

## Component Definition

The `TournamentDetails` function is a React functional component that utilizes hooks for state management and effects.

```jsx
const TournamentDetails = (props) => { ... }
```

---

## State Variables

The component uses several state variables managed by React's `useState` hook:

- **tournamentDetails**: Stores the tournament details fetched from the API.
- **isLoading**: Manages the loading state of the component.
- **changePermission**: Stores permission status related to tournament changes.
- **activeTab**: Tracks the currently active tab in the UI.
- **roundData**: Stores round data from the schedule.

```jsx
const [tournamentDetails, setTournamentDetails] = useState(null);
const [isLoading, setisLoading] = useState(false);
const [changePermission, setChangePermission] = useState(false);
const [activeTab, setActiveTab] = useState(props.location.data?.active ? props.location.data?.active : "1");
const [roundData, setRoundData] = useState([]);
```

---

## Lifecycle Methods

### `useEffect`

The `useEffect` hook is used to perform actions on component mount:

- Fetches tournament details if a valid `tournamentId` is detected.
- Calls permission settings function.

```jsx
useEffect(() => {
  if (tournamentId > 0) {
    getDetail();
  } else {
    goToBack();
  }
  callSetPermission();
}, [tournamentId]);
```

---

## Helper Functions

### getDetail

Fetches tournament details using an API call and handles navigation if the game slug does not match.

```jsx
const getDetail = async () => {
  setisLoading(true);
  await getTournamentsById(tournamentId)
    .then((res) => { /* logic */ })
    .catch(() => { /* error handling */ });
};
```

### goToBack

Navigates back to the tournaments list view.

```jsx
const goToBack = () => {
  props.history.push(returnUrl);
};
```

### toggle

Handles the tab switching functionality.

```jsx
const toggle = (tab) => {
  if (activeTab !== tab) {
    setActiveTab(tab);
  }
};
```

### callSetPermission

Sets the permission state based on the user's permissions.

```jsx
const callSetPermission = () => { /* logic */ };
```

---

## Render Method

The render method of the component lays out the structure using Reactstrap components. It includes:

- **Breadcrumbs**: For navigation context.
- **GoBack**: To navigate back to the tournaments list.
- **Tabs**: For displaying different sections of tournament information.
- **Spinner**: Displays a loading indicator when data is being fetched.

```jsx
return (
  <>
    <div className="page-content">
      <Breadcrumbs breadcrumbItem="Tournament Detail" />
      <GoBack backUrl="/tournament" />
      <Row>
        <Col>
          <Nav tabs>
            <NavItem> {/* Tournament Details Tab */} </NavItem>
            <NavItem> {/* Schedule Tab */} </NavItem>
            <NavItem> {/* Match Info Tab */} </NavItem>
            <NavItem> {/* Standings Tab */} </NavItem>
            <NavItem> {/* Enrolled Teams Tab */} </NavItem>
          </Nav>
          {isLoading ? ( /* Spinner */ ) : ( /* TabContent */ )}
        </Col>
      </Row>
    </div>
  </>
);
```

---

## Export

The component is wrapped in `withRouter`, which provides routing capabilities, and is exported as default.

```jsx
export default withRouter(TournamentDetails);
```

---

## Dependencies

The following dependencies are required for this component:

- **React and react-router-dom**: Core and routing functionalities.
- **reactstrap**: UI components.
- **classnames**: Conditional class name utility.
- **Custom Helpers and Components**: For permission filtering and UI components.

---

**🎨 Note:** This component is designed to provide a seamless user experience by organizing tournament data into easily navigable tabs, enhancing the user's ability to manage and view tournament details efficiently. 🏆

# TournamentsList.jsx Documentation 📄

Welcome to the documentation for the **TournamentsList.jsx** file. This component is designed for managing and displaying a list of tournaments within a web application. It integrates several functionalities such as filtering, pagination, and CRUD operations (Create, Read, Update, Delete) for managing tournament data.

## Index 📚

1. [Component Overview](#1-component-overview-)
2. [Imports and Dependencies](#2-imports-and-dependencies-)
3. [State Variables](#3-state-variables-)
4. [Functions and Methods](#4-functions-and-methods-)
5. [UI Elements and JSX Structure](#5-ui-elements-and-jsx-structure-)
6. [Permissions and Interactivity](#6-permissions-and-interactivity-)

---

### 1. Component Overview 📋

The **TournamentsList** component provides a comprehensive interface for users to interact with a list of tournaments. It includes features such as date filtering, game type filtering, pagination, and actions like viewing, editing, adding, and deleting tournaments.

---

### 2. Imports and Dependencies 📦

```javascript
import React, { useCallback, useState } from "react";
import { Row, Col, Card, CardBody, Button, Dropdown, DropdownToggle, DropdownMenu, DropdownItem } from "reactstrap";
import { Link } from "react-router-dom";
import { useEffect } from "react";
import { useSelector } from "react-redux";
import { format } from "date-fns";

// Custom Components and Helpers
import Breadcrumbs from "../../components/Common/Breadcrumb";
import FilterPermission from "../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils";
import { getTournamentList } from "../../services/bracket_tournaments_api_helper";
import { dateTimeFormatter, getFilterText, getFilterGame } from "../../helpers/util";
import Paginator from "../../helpers/paginator/paginator";
import ReactDatePicker from "react-datepicker";
import ClearButton from "../../components/ClearButton";
import DeleteAlertModal from "../../components/Common/DeleteAlertModal";
import PrizeList from "./Common/PrizeList";
import { uniqBy } from "lodash";

// Assets
import calenderIcon from "../../assets/images/calendar.svg";
import edit from "../../assets/images/editTournament.svg";
import disableEditIcon from "../../assets/images/disableEditIcon.svg";
import addSchedule from "../../assets/images/add-schedule.svg";
import disableSchedule from "../../assets/images/addscheduledisable.svg";
import view from "../../assets/images/view.svg";
import deleteIcon from "../../assets/images/delete.svg";
import deleteDisable from "../../assets/images/deleteDisable.svg";
```

#### Key Dependencies:
- **React & Reactstrap**: For developing UI components.
- **React Router DOM**: For navigation and routing.
- **Lodash**: For utility functions.
- **React Redux**: For accessing state from the Redux store.
- **Date-fns**: For formatting dates.

---

### 3. State Variables 🗄️

| State Variable | Type   | Description |
|----------------|--------|-------------|
| `dateRange`        | Array  | Stores the start and end date for filtering tournaments. |
| `tournamentLists`  | Array  | Holds the list of tournaments fetched from the API. |
| `addPermission`    | Boolean| Determines if the user has permission to add tournaments. |
| `changePermission` | Boolean| Determines if the user has permission to change tournament details. |
| `deletePermission` | Boolean| Determines if the user has permission to delete tournaments. |
| `pageNumber`       | Number | Tracks the current page number for pagination. |
| `showLoadder`      | Boolean| Indicates if the loader should be displayed. |

And many more for handling dropdown selections and filters.

---

### 4. Functions and Methods 🔧

- **tournamentList()**: Fetches the list of tournaments based on the current filters and updates the state.
- **handlePageClick(pageNum)**: Updates the page number when the pagination controls are used.
- **handleChange(dates)**: Updates the date range for filtering tournaments.
- **handleClear()**: Clears all filters and resets the state to its default values.
- **callSetPermission()**: Sets the permissions for adding, changing, and deleting tournaments based on the user's role.
- **handleDelete(tournamentId, index, currentStat)**: Prepares to delete a tournament and prompts for confirmation.

---

### 5. UI Elements and JSX Structure 🖼️

The component is structured with several UI elements:

- **Breadcrumbs** for navigation context.
- **Dropdowns** for filtering tournaments by game type, game name, bracket style, seeding, etc.
- **Date Picker** for selecting a date range to filter tournaments.
- **Table** to display the list of tournaments with columns such as Tournament Name, Game, Entry Fee, Schedule, etc.
- **Buttons** for actions such as adding, viewing, editing, and deleting tournaments.
- **Paginator** for navigating through pages of tournaments.

Example of a table row in the JSX:

```jsx
<tr key={index}>
  <td>
    <Link to={{ pathname: `/tournament/view/${item?.slug}/${item?.id}`, data: { nameOfGame: item.game } }}>
      {item?.name}
    </Link>
  </td>
  <td>{item.game}</td>
  ...
</tr>
```

---

### 6. Permissions and Interactivity 🔐

The component uses permissions to control the availability of certain actions:

- **Add Tournament**: Conditional rendering based on `addPermission`.
- **Edit Tournament**: Conditionally rendered links/buttons depending on `changePermission`.
- **Delete Tournament**: Conditionally rendered buttons depending on `deletePermission`.

Each of these permissions is determined by the `FilterPermission` utility, which checks the user's permissions passed down as props.

---

This comprehensive documentation aims to provide a detailed understanding of the **TournamentsList.jsx** component, its functionalities, and its place within the application. For further improvement, consider adding more comments within the code to clarify complex logic and enhance maintainability.

# Documentation for `useStateWithCallback.jsx` 📄

## Overview

The `useStateWithCallback.jsx` file introduces a custom React Hook that enhances the built-in `useState` hook by adding the ability to perform a callback after the state has been updated. This functionality is particularly useful when you need to execute a side-effect or perform an operation immediately after the state change.

## Table of Contents

1. [Introduction](#introduction)
2. [Usage](#usage)
3. [API](#api)
4. [Example](#example)
5. [Conclusion](#conclusion)

## Introduction

The `useStateWithCallback` hook is designed to work similarly to React's `useState`, but with an added feature: it allows you to pass a callback function that runs after the state value has been updated. This can be beneficial in scenarios where you need to ensure that certain actions are performed after a state change.

## Usage

To use this custom hook, you need to import it into your component and use it just like the traditional `useState`. However, when updating the state, you have the option to pass a callback function that will be executed after the state has been updated.

## API

### `useStateWithCallback(initialValue)`

- **Parameters:**
  - `initialValue`: The initial state value.

- **Returns:**
  - An array containing:
    1. The current state value.
    2. A function to update the state and optionally execute a callback.

### `setValueAndCallback(newValue, callback)`

- **Parameters:**
  - `newValue`: The new state value to be set.
  - `callback`: An optional function that receives the previous and new value as arguments, executed after the state is updated.

## Example

Here's an example of how to use the `useStateWithCallback` hook in a React component:

```jsx
import React from 'react';
import { useStateWithCallback } from './useStateWithCallback';

const ExampleComponent = () => {
  const [counter, setCounter] = useStateWithCallback(0);

  const handleClick = () => {
    setCounter(counter + 1, (prevValue, newValue) => {
      console.log(`Counter changed from ${prevValue} to ${newValue}`);
    });
  };

  return (
    <div>
      <p>Counter: {counter}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
};

export default ExampleComponent;
```

### Explanation:

- **Initial State:** The counter is initialized to `0`.
- **State Update with Callback:** When the "Increment" button is clicked, the `counter` state is incremented by 1. After updating, a callback logs the transition of the counter value from its previous state to the new state.

## Conclusion

The `useStateWithCallback` hook is a powerful tool for managing state changes with side effects in React components. By providing a callback mechanism, it allows developers to ensure certain operations are executed immediately after a state update, improving the control and predictability of component behavior.

Feel free to integrate this custom hook into your projects to enhance state management capabilities where needed! 🚀

# AddWinningPercentage.jsx Documentation 📄

## Overview
`AddWinningPercentage.jsx` is a React component that provides a form interface for updating the winning percentage for a specific round in a tournament. It leverages the `availity-reactstrap-validation` library for form validations and `react-toastify` for displaying success or error notifications.

---

## Table of Contents
- [Imports](#imports)
- [Component Structure](#component-structure)
- [State Management](#state-management)
- [Form Handling](#form-handling)
- [Event Handlers](#event-handlers)
- [Rendering](#rendering)
- [Usage](#usage)
- [Conclusion](#conclusion)

---

## Imports
The component imports several libraries and modules required for its functionality:

```javascript
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { FormGroup, Button } from "reactstrap";
import { toast } from "react-toastify";
import toastrOptions from "../../../helpers/toastr-options/toastr-options";
import tickIcon from "../../../assets/images/user-tick-icon.svg";
import crossIcon from "../../../assets/images/user-cross-icon.svg";
import IconsToolTip from "../../../components/IconsToolTip";
import { updateWinningPercentageOfRound } from "../../../services/bracket_tournaments_api_helper";
```

### Key Libraries Used:
- **React & useState**: For creating the component and managing state.
- **AvForm & AvField**: For form handling with validation.
- **reactstrap**: For UI components like `FormGroup` and `Button`.
- **react-toastify**: For displaying notifications.
- **Custom Assets**: Icons used within the component.

---

## Component Structure
The component is structured as a functional component with the use of React hooks. It receives several props and maintains internal state for handling input changes.

### Props:
- **roundDetails**: Contains details about the current round, such as `round_percent` and identifiers.
- **SaveWinningPercentageOfRound**: Callback function to handle saving actions.
- **CloseWinningPercentageOfRound**: Callback function to handle closing or cancel actions.

---

## State Management
The component manages a single piece of state:

```javascript
const [value, setValue] = useState(roundDetails.round_percent);
```
- **value**: Represents the current input value for the winning percentage. Initialized with `roundDetails.round_percent`.

---

## Form Handling
The component uses `AvForm` and `AvField` to handle input validation:

```javascript
<AvForm className="d-flex editEarning-timeline" onValidSubmit={(e, v) => { handleSubmit(e, v); }}>
  <AvField 
    className="winningPercentage" 
    name="winningPercentage" 
    label="Winning Percentage*" 
    placeholder="Winning Percentage" 
    type="text" 
    validate={{
      required: { value: true, errorMessage: "Winning Percentage is required" },
      number: { value: true, errorMessage: "Please enter number only" },
      min: { value: 1, errorMessage: "Winning Percentage should be greater than 0" },
      max: { value: 1000, errorMessage: "Winning Percentage should be less than or equal to 1000" },
    }}
    onKeyDown={(e) => handleKeyDown(e)}
    onChange={(e) => handleChange(e.target.value)}
    defaultValue={value}
  />
</AvForm>
```

### Validation Rules:
- **Required**: Field must be filled.
- **Number**: Input must be a number.
- **Min**: Greater than 0.
- **Max**: Less than or equal to 1000.

---

## Event Handlers
### handleChange
Updates the `value` state when input changes:
```javascript
const handleChange = (val) => {
  setValue(val);
};
```

### handleSubmit
Handles form submission, calling the API to update the winning percentage:
```javascript
const handleSubmit = async (event, values) => {
  event.preventDefault();
  let data = { round_percentage: Number(values.winningPercentage) };
  await updateWinningPercentageOfRound(roundDetails.tournament_id, roundDetails.id, data)
    .then(() => {
      SaveWinningPercentageOfRound();
      CloseWinningPercentageOfRound();
      toast.success("Winning percentage updated successfully", toastrOptions);
    })
    .catch(() => {
      toast.error("Error", toastrOptions);
    });
};
```

### handleKeyDown
Prevents entering invalid characters:
```javascript
const handleKeyDown = (e) => {
  if (e.key === "." || e.key === "-") {
    e.preventDefault();
  }
};
```

---

## Rendering
The component renders a form with inputs and buttons, providing a user interface for updating the winning percentage:

- **Input Field**: For entering the winning percentage.
- **Save Button**: Submits the form.
- **Cancel Button**: Closes the form without saving.

```javascript
return (
  <>
    <AvForm className="d-flex editEarning-timeline" onValidSubmit={(e, v) => { handleSubmit(e, v); }}>
      <AvField ... />
      <FormGroup>
        <div className="mt-4 d-flex">
          <Button type="submit" color="primary" className="edit-icon info-icon">
            <IconsToolTip image={tickIcon} altImageText="user-tick-icon" text="Save" />
          </Button>
          <Button className="edit-icon mt-2 ms-0 px-0 info-icon" onClick={() => { CloseWinningPercentageOfRound(); }}>
            <IconsToolTip image={crossIcon} altImageText="user-cross-icon" text="Cancel" />
          </Button>
        </div>
      </FormGroup>
    </AvForm>
  </>
);
```

---

## Usage
To use this component, it needs to be integrated into a parent component where `roundDetails`, `SaveWinningPercentageOfRound`, and `CloseWinningPercentageOfRound` are defined and passed as props.

---

## Conclusion
The `AddWinningPercentage.jsx` component is a straightforward form-based interface for updating the winning percentage of a tournament round. It ensures data validation and provides feedback to the user through notifications, enhancing the user experience.

# AddTournamentSchedule.jsx Documentation

## Overview

The **AddTournamentSchedule** component is part of a web application that deals with managing tournaments. It provides functionalities to view and manage the schedule of rounds for a specific tournament. This component handles fetching details about the tournament and its rounds, displaying the schedule in an accordion-style UI, and managing manual placements and ranks for teams.

## Table of Contents

- [Component Imports](#component-imports)
- [State Management](#state-management)
- [API Integration](#api-integration)
- [UI Components](#ui-components)
- [Event Handlers](#event-handlers)
- [Redux Integration](#redux-integration)
- [Routing and Navigation](#routing-and-navigation)
- [Component Rendering](#component-rendering)
- [Conclusion](#conclusion)

## Component Imports

The component imports several modules and components which are essential for its functionality:

```jsx
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody } from "reactstrap";
import Breadcrumbs from "../../../components/Common/Breadcrumb";
import { withRouter } from "react-router-dom";
import Loader from "../../../components/Common/Loader";
import { connect } from "react-redux";
import { getTournamentRoundList, getTournamentsById } from "../../../services/bracket_tournaments_api_helper";
import { Accordion, AccordionItem, AccordionItemHeading, AccordionItemButton, AccordionItemPanel } from "react-accessible-accordion";

import "react-accessible-accordion/dist/fancy-example.css"; // Styles for accordion
import TournamentsRoundHeading from "./TournamentsRoundHeading";
import TournamentScheduleTable from "./TournamentScheduleTable";
import "../BracketsAndTournaments.scss";
import { GoBack } from "../../../components/GoBack";
import ManualPlacementAddRankForTeam from "../Form/ManualPlacementAddRankForTeam";
import ViewBracket from "./ViewBracket";
import ViewManualCreatedBracket from "./ViewManualCreatedBracket";
```

## State Management

The component uses React's `useState` hook to manage local state variables:

- `showLoadder`: Boolean to control the display of the loader.
- `tournamentScheduleLists`: Holds the list of tournament schedules.
- `bracketId`: Stores the bracket embed ID.
- `tournamentDetails`: Stores details of the tournament.
- `rank`: Holds rank-related data for teams.

## API Integration

The component makes use of API helper functions to fetch data:

- **getTournamentsById**: Fetches tournament details by ID.
- **getTournamentRoundList**: Retrieves the list of rounds for a given tournament.

The data fetching is initiated inside `useEffect` when component mounts or when the `tournamentId` changes.

## UI Components

- **Loader**: Displays a loading spinner while fetching data.
- **Breadcrumbs**: Displays the navigation path.
- **Accordion**: Displays tournament rounds in a collapsible format.
- **ManualPlacementAddRankForTeam**: Allows manual ranking of teams.
- **ViewBracket** and **ViewManualCreatedBracket**: Provides a preview of the tournament bracket.

## Event Handlers

The component defines several key event handlers:

- **getDetail**: Fetches tournament details and updates state.
- **getRoundData**: Fetches round data and updates state.
- **goToBack**: Redirects back to the tournament list view.
- **reCallApi**: Re-fetches round and tournament details.

## Redux Integration

The component is connected to the Redux store to access the current game's state:

```jsx
const mapStateToProps = (state) => {
  return {
    game: state.Games?.game,
  };
};

export default withRouter(connect(mapStateToProps)(AddTournamentSchedule));
```

## Routing and Navigation

The component utilizes `withRouter` from `react-router-dom` to access route parameters and history for navigation purposes. It uses this to navigate back to the tournament list or to a specific tournament based on the slug and ID.

## Component Rendering

The component conditionally renders various elements based on the state:

- **Loader**: Shown when data is being fetched.
- **Breadcrumbs**: Displayed if not in viewMode.
- **Accordion**: Renders each tournament round with its schedule.
- **Bracket Preview**: Displays the tournament bracket based on the type of game (PPK or traditional).

## Conclusion

The **AddTournamentSchedule** component is a crucial part of the tournament management system, providing a detailed view and management interface for tournament schedules. Its integration with APIs and Redux, along with a responsive UI using accordions, makes it a robust tool for handling complex tournament scheduling needs.

# ChangeAssignedAdmin.jsx Documentation

## Overview
The `ChangeAssignedAdmin.jsx` component is a React component that allows users to change the assigned admin for a specific tournament match. It leverages several libraries and services to provide a user-friendly interface for selecting an admin from a dropdown and updating the admin assignment.

## Importing Necessary Libraries and Components

```jsx
import React, { useState, useEffect } from "react";
import { AvForm } from "availity-reactstrap-validation";
import Select from "react-select";
import { FormGroup, Label, Button } from "reactstrap";
import { toast } from "react-toastify";
import toastrOptions from "../../../helpers/toastr-options/toastr-options";
import tickIcon from "../../../assets/images/user-tick-icon.svg";
import crossIcon from "../../../assets/images/user-cross-icon.svg";
import { getAdminUserListTournamentForDropdown, updateAssignedAdminForTournament } from "../../../services/bracket_tournaments_api_helper";
```

### Key Imported Items
- **React and Hooks**: Used to create the component and manage state.
- **Availity Reactstrap Validation**: Provides form validation.
- **React Select**: Used for creating the admin select dropdown.
- **Reactstrap**: Provides UI components like `Button` and `FormGroup`.
- **React Toastify**: For displaying toast notifications.
- **Custom Services**: Functions to interact with the backend API for fetching and updating admin data.

## Component Structure

### State Variables
- **admins**: Array of admin options for the dropdown.
- **adminId**: Currently selected admin ID.
- **adminRequiredMsg**: Error message if no admin is selected.

### Side Effects
- **useEffect**: Calls `adminList` to fetch and set the list of admins when the component is mounted.

### Functions

#### `adminList`
Fetches admin users for the tournament from the backend and sets the `admins` state.

#### `handleSubmit`
Handles form submission. Validates the admin selection and updates the assigned admin for the tournament match.

#### `handleAdminSelectGroup`
Updates the selected admin state and clears any error message.

#### `handleInvalidSubmit`
Sets an error message if the form is submitted without selecting an admin.

## Component Rendering

```jsx
return (
  <>
    <AvForm className="editEarning-timeline" onValidSubmit={(e) => { handleSubmit(e); }} onInvalidSubmit={handleInvalidSubmit}>
      <Label>Select Admin*</Label>
      <Select value={adminId} onChange={(event) => { handleAdminSelectGroup(event); }} options={admins} name="admin_id" classNamePrefix="select2-selection" />
      {adminRequiredMsg.length === 0 ? null : (<label className={adminRequiredMsg.length === 0 ? "" : "errorMsgGames invalid-feedback"}>{adminRequiredMsg}</label>)}
      <FormGroup>
        <div className="mt-4 d-flex">
          <Button type="submit" color="primary" className="edit-icon">
            <img alt="user-tick-icon" src={tickIcon} />
          </Button>
          <Button className="edit-icon mt-2" onClick={() => { CloseAssignedAdmin(); }}>
            <img alt="user-cross-icon" src={crossIcon} />
          </Button>
        </div>
      </FormGroup>
    </AvForm>
  </>
);
```

### Key Components
- **AvForm**: Handles form validation and submission.
- **Select**: Provides a dropdown to select an admin from the list.
- **Buttons**: Save and Cancel buttons to submit the form or close the modal.

## Features
- **Admin Selection**: Users can select an admin from a dropdown list.
- **Form Validation**: Ensures that an admin is selected before form submission.
- **API Integration**: Fetches admin data and updates tournament match assignments.
- **User Feedback**: Provides success and error notifications using toast.

## Usage
To use this component, include it in the parent component, passing the necessary props: `TournamentId`, `MatchId`, `SaveAssignedAdmin`, and `CloseAssignedAdmin`.

## Conclusion
The `ChangeAssignedAdmin` component is designed to streamline the process of reassigning admins in a tournament setting. It is built using modern React practices, ensuring easy integration and a smooth user experience.

# PrizeList.jsx Documentation

## Overview
The `PrizeList.jsx` component is a React functional component designed to display a list of prizes for a tournament. It showcases the top three prizes by default and provides an option to view more if there are additional prizes. To achieve this, it utilizes a modal dialog to show the complete list of prizes when requested.

## Key Features
- **Display Top Prizes**: Shows the top three prizes of a tournament by default.
- **View More Prizes**: Allows users to see more prizes if there are more than three.
- **Modal Integration**: Uses a modal to display the full list of prizes.
- **Suffix Helper**: Applies a suffix to the prize position (e.g., 1st, 2nd) for better readability.

## Component Structure

### Imports
- **React**: The primary library for building the user interface.
- **useState**: A React Hook to manage component state.
- **Button**: A component from Reactstrap for UI button elements.
- **appendSuffixToTournamentPosition**: A utility function to append suffixes to numeric positions.
- **PrizeListModal**: A modal component specifically designed to display an extended list of prizes.

### State Management
```javascript
const [showMore, setShowMore] = useState(false);
const [showMorePrice, setShowMorePriceData] = useState([]);
```
- `showMore`: A boolean state to control the visibility of the modal.
- `showMorePrice`: An array state to hold the complete prize data when the modal is displayed.

### Functions

#### `handleShowMore`
```javascript
const handleShowMore = (showMorePriceData) => {
    setShowMore(true);
    setShowMorePriceData(showMorePriceData);
};
```
- **Purpose**: Activates the modal to display additional prizes and updates the `showMorePrice` state with the full list of prizes.

#### `handleClose`
```javascript
const handleClose = () => {
    setShowMore(false);
    setShowMorePriceData([]);
};
```
- **Purpose**: Closes the modal and resets the `showMorePrice` state.

### Rendering Logic
- **Top Prizes**: Displays the top three prizes by sorting and slicing the prize data.
- **View More Button**: Conditionally renders a button to view more prizes if the total number of prizes exceeds three.
- **Modal**: Integrates the `PrizeListModal` to display the full list of prizes when `showMore` is true.

### JSX Structure
```jsx
<>
    {prize
        .sort((first, second) => {
            return first.position > second.position ? 1 : -1;
        })
        .slice(0, 3)
        .map((priceList, id) => {
            return (
                <p key={id} className="mb-0">
                    {priceList.position} {appendSuffixToTournamentPosition(priceList.position)} prize - $ {priceList.price}
                </p>
            );
        })}
    {prize.length > 3 ? (
        <Button onClick={() => handleShowMore(prize)} variant="link" className="btn btn-primary btn-sm view-button theme-color mt-2">
            View more
        </Button>
    ) : null}
    <PrizeListModal show={showMore} prizelist={showMorePrice} closeModal={handleClose} />
</>
```

## Usage
To use the `PrizeList` component, simply pass the `prize` prop with an array of prize objects where each object contains `position` and `price` attributes.

## Conclusion
The `PrizeList.jsx` component provides a user-friendly interface to display tournament prizes. Featuring a conditional modal and a structured prize list, it enhances the overall experience of viewing tournament details by presenting information in a concise and expandable format.

# Documentation for TournamentScheduleTable.js

## Overview
The `TournamentScheduleTable.js` component is designed to manage and display the scheduling details of a tournament round. It includes functionalities to view, edit, assign admins to matches, add winners manually, and view more details about the matches.

---

## Table of Contents
1. [Component Imports](#component-imports)
2. [State Management](#state-management)
3. [Main Functionalities](#main-functionalities)
4. [Component Structure](#component-structure)
5. [Modals](#modals)
6. [Helper Functions](#helper-functions)

---

## Component Imports

The component imports several libraries and components which include:

- **React and Hooks**: For creating the component and managing state.
- **reactstrap**: For UI components like `Button`, `Modal`, etc.
- **redux**: To connect with the application's state management.
- **lodash**: For utility functions, particularly `isEmpty`.
- **Custom Components**: Such as `AddBestOfMatches`, `ViewMatches`, `ChangeAssignedAdmin`, etc.

---

## State Management

The component uses React's state management to handle various states:

- **Modals**: Tracks the visibility of different modals like `addBestOfMatchesModal`, `viewMatchesModal`, etc.
- **Data Handling**: Includes states like `showLoadder`, `showerror`, `disableSubmit`, which manage loading status, errors, and submission capabilities respectively.
- **Redux State**: Uses `useSelector` to access `scheduleList` from the Redux store.

---

## Main Functionalities

1. **Schedule Management**: 
   - Adding and viewing "Best of Matches" for a particular match.
   - Submitting the schedule to update the tournament details.

2. **Admin Assignment**: 
   - Changing the admin assigned to a match.

3. **Winner Assignment**: 
   - Manually assigning a winner to a match.

4. **Match Viewing**: 
   - Viewing the list of matches and their details.

5. **Error Handling**: 
   - Provides feedback and error messages for user actions.

---

## Component Structure

The component structure is organized into a table to display match details with columns such as Match, Start and End Date Time, Admin, Best of Matches, and Winner. Each row represents a match, and users can interact with buttons to edit details or view more information.

### Table Headers

- **Match**: Displays the match identifier.
- **Start/End Date Time**: Shows the scheduled timing for each match.
- **Admin**: Displays the admin assigned to oversee the match.
- **Best of Matches**: Indicates the number of matches scheduled under "Best of" format.
- **Winner**: Displays the winner of the match, or a button to add one manually.

---

## Modals

The component includes several modals for detailed operations:

1. **Add Best of Matches Modal**: Allows users to add multiple matches under a single "Best of" match.
2. **View Matches Modal**: Provides a detailed view of the sub-matches within a match.
3. **Add Manual Winner Modal**: Facilitates the manual assignment of winners to a match.
4. **View More Teams Modal**: Displays additional team information when needed.

---

## Helper Functions

- **openModal**: Opens the modal for adding "Best of Matches".
- **closeModal**: Closes the modal and clears errors.
- **submitSchedule**: Handles the submission of the schedule to the backend.
- **handleShowMore**: Manages the display of additional teams or matches.
- **handleSaveAssignedAdmin**: Callback function to refresh data after changing assigned admin.

---

## Conclusion
The `TournamentScheduleTable.js` component is a comprehensive tool for managing tournament schedules. Its integration with modals and Redux allows for seamless user interactions and efficient data handling. This component is essential for organizing and updating tournament rounds effectively.

# TournamentsRoundHeading.js Documentation

The `TournamentsRoundHeading.js` file is a React component that renders the heading section for each round in a tournament schedule. It displays basic information about a tournament round, such as the round name, number of matches, and, if applicable (for PPK-style tournaments), the winning percentage. The component also provides functionality for editing the winning percentage.

## Index
- [Component Overview](#component-overview)
- [Props](#props)
- [State](#state)
- [Key Functions](#key-functions)
- [UI Elements](#ui-elements)

## Component Overview

The `TournamentsRoundHeading` component is responsible for presenting a concise summary of a tournament round. It includes the round's name, total number of matches, and, in the case of PPK tournaments, the ability to adjust the winning percentage. The component is interactive, allowing users to edit fields where permitted.

## Props

| Prop     | Type     | Description                                                   |
|----------|----------|---------------------------------------------------------------|
| `data`   | Object   | Contains details about the tournament round, such as round name, type, total matches, and winning percentage. |
| `callApi`| Function | Callback function to refresh data after changes are made.     |
| `isPPK`  | Boolean  | Flag that indicates if the tournament is of type PPK, affecting the display of winning percentage controls. |

## State

| State         | Type    | Initial Value | Description                                         |
|---------------|---------|---------------|-----------------------------------------------------|
| `winnerIndex` | Number  | `null`        | Holds the ID of the round currently being edited for the winning percentage. |

## Key Functions

### `handleSave()`
- **Purpose**: Executes the `callApi` function to refresh data and resets `winnerIndex` to null, closing any open edit forms.
- **When Used**: Invoked after successfully saving changes to the winning percentage.

### `handleClose()`
- **Purpose**: Closes the winning percentage edit form by setting `winnerIndex` to null.
- **When Used**: Triggered when the user decides to cancel editing the winning percentage.

## UI Elements

- **Round Name and Details**: Displays the round name, along with additional type information if applicable.
- **Total Matches**: Shows the total number of matches scheduled for the round.
- **Winning Percentage**: (PPK Only) Displays and allows editing of the winning percentage using the `AddWinningPercentage` component.
- **Edit Button**: Allows users to open the edit form for the winning percentage. The button's availability is controlled by the `is_field_editable` property of the `data` object.

## Example Usage

```jsx
<TournamentsRoundHeading 
  data={roundData} 
  callApi={refreshFunction} 
  isPPK={true} 
/>
```

This example demonstrates how to use the `TournamentsRoundHeading` component by passing it necessary data and callback functions. The `isPPK` boolean is set to `true` to enable the winning percentage feature.

---

This documentation covers the functionalities and usage of the `TournamentsRoundHeading.js` component. The component is designed to be a part of a larger system for managing and interacting with tournament schedules, particularly useful in the context of tournaments that require percentage-based winnings.

# Documentation for `UpdateAdminCode.jsx`

## Overview
The `UpdateAdminCode.jsx` file defines a React component responsible for updating either an admin or participant code within a lobby. This component utilizes the `availity-reactstrap-validation` for form handling and validation, and integrates with the `lobby_api_helper` service to update the lobby details.

## Table of Contents
1. [Component Structure](#component-structure)
2. [Props](#props)
3. [Functionality](#functionality)
4. [Usage](#usage)
5. [Dependencies](#dependencies)

## Component Structure

```jsx
import React from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { FormGroup, Button } from "reactstrap";
import { toast } from "react-toastify";
import toastrOptions from "../../../helpers/toastr-options/toastr-options";
import tickIcon from "../../../assets/images/user-tick-icon.svg";
import crossIcon from "../../../assets/images/user-cross-icon.svg";
import IconsToolTip from "../../../components/IconsToolTip";
import { editLobby } from "../../../services/lobby_api_helper";
import { convertTo24HourFormat } from "./utils";

const UpdateAdminCode = ({ isAdminCode, lobbyData, SaveAdminCode, CloseAdminCode }) => {
    const handleSubmit = async (event, values) => {
        event.preventDefault();
        try {
            let data = { ...lobbyData };
            let successMessage = "";
            data.end_time = lobbyData.end_time === null ? null : convertTo24HourFormat(lobbyData.end_time);
            data.last_entry_time = convertTo24HourFormat(lobbyData.last_entry_time);
            data.start_time = convertTo24HourFormat(lobbyData.start_time);

            if (isAdminCode) {
                data.admin_code = values.admin_code;
                successMessage = "Admin code";
            } else {
                data.participant_code = values.participant_code;
                successMessage = "Participant code";
            }

            await editLobby(lobbyData.lobby_id, data);
            toast.success(`${successMessage} updated successfully`, toastrOptions);
            SaveAdminCode(successMessage === "Admin code" ? data.admin_code : data.participant_code);
        } catch (error) {
            CloseAdminCode();
        }
    };

    return (
        <>
            <AvForm className="d-flex editEarning-timeline" onValidSubmit={(e, v) => { handleSubmit(e, v); }}>
                <AvField
                    name={isAdminCode ? "admin_code" : "participant_code"}
                    label={isAdminCode ? "Admin Code*" : "Participant Code*"}
                    placeholder={isAdminCode ? "Enter admin code here" : "Enter participant code here"}
                    type="text"
                    validate={{
                        required: { value: true, errorMessage: isAdminCode ? "Admin code is required" : "Participant code is required" },
                    }}
                />
                <FormGroup>
                    <div className="mt-4 d-flex">
                        <Button type="submit" color="primary" className="edit-icon info-icon update-admin-button">
                            <IconsToolTip image={tickIcon} altImageText="user-tick-icon" text="Save" />
                        </Button>
                        <Button className="edit-icon mt-2 ms-0 px-0 info-icon update-admin-button" onClick={() => { CloseAdminCode(); }}>
                            <IconsToolTip image={crossIcon} altImageText="user-cross-icon" text="Cancel" />
                        </Button>
                    </div>
                </FormGroup>
            </AvForm>
        </>
    );
};

export default UpdateAdminCode;
```

## Props

| Prop Name     | Type     | Description                                                  |
|---------------|----------|--------------------------------------------------------------|
| `isAdminCode` | Boolean  | Determines if the code being updated is an admin code.       |
| `lobbyData`   | Object   | Contains current lobby details including timings and IDs.    |
| `SaveAdminCode` | Function | Callback function triggered after a successful code update. |
| `CloseAdminCode` | Function | Callback function to close the update code dialog.         |

## Functionality

- **Form Handling**: Uses `AvForm` and `AvField` from `availity-reactstrap-validation` to manage form submission and validation.
- **Code Update**: Depending on the `isAdminCode` prop, either the admin code or participant code is updated in the lobby details.
- **API Integration**: Utilizes `editLobby` from `lobby_api_helper` to save the updated lobby information.
- **Feedback**: Upon successful update, a toast notification is displayed to the user.

## Usage

This component is used within a larger admin panel or management interface where admins can update participation details of a lobby. It is particularly useful for managing access or participation credentials.

## Dependencies

- **React**: For building the UI component.
- **Availity Reactstrap Validation**: For handling form validation.
- **Reactstrap**: For UI components such as `FormGroup` and `Button`.
- **React Toastify**: For displaying notifications.
- **Custom Utilities**: 
  - `editLobby` from `lobby_api_helper` for API operations.
  - `convertTo24HourFormat` from `utils` for time conversion.

This component efficiently manages code updates and provides a seamless user experience for administrators.

# Documentation for `utils.jsx` 📚

This document provides a detailed explanation of the `utils.jsx` file, which includes utility functions to handle date and time manipulations, validate tournament rounds, and more. These utilities are particularly useful for managing tournaments and ensuring the integrity of scheduling.

## Table of Contents
- [Overview](#overview)
- [Function Descriptions](#function-descriptions)
  - [validateRounds](#validaterounds)
  - [convertRoundDateTimeToTimestamp](#convertrounddatetimetotimestamp)
  - [getESTDateTimeTimestamp](#getestdatetimetimestamp)
  - [convertDateFormat](#convertdateformat)
  - [checkIfLinkIsNeeded](#checkiflinkisneeded)
  - [checkMatchDateTime](#checkmatchdatetime)
  - [findMaxSubMatchLength](#findmaxsubmatchlength)
  - [getESTDateTimeTimestampWithMinus10Minutes](#getestdatetimetimestampwithminus10minutes)
  - [checkLastEntryTime](#checklastentrytime)
  - [checkLastEntryTimeForSubmatchesEdit](#checklastentrytimeforsubmatchesedit)
  - [convertTo24HourFormat](#convertto24hourformat)
- [Constants](#constants)

## Overview

The `utils.jsx` file is designed to provide helper functions that facilitate the handling of tournament scheduling. It focuses on date and time calculations, ensuring that tournament rounds are scheduled correctly and comply with specified constraints.

## Function Descriptions

### `validateRounds`

```javascript
export function validateRounds(rounds, formValues, roundId)
```

**Purpose**: Validates the start dates and times of tournament rounds to ensure they adhere to scheduling rules.

- **Parameters**:
  - `rounds`: Array of round objects.
  - `formValues`: Form data containing start date and time for validation.
  - `roundId`: The ID of the current round being validated.

- **Validation Logic**:
  - Ensures subsequent round starts after the current round.
  - Ensures a minimum of 1.5 hours gap between successive rounds.
  - Throws errors if conditions are not met.

### `convertRoundDateTimeToTimestamp`

```javascript
export function convertRoundDateTimeToTimestamp(date, time)
```

**Purpose**: Converts a provided date and time into a timestamp.

- **Parameters**:
  - `date`: Date string in `YYYY-MM-DD` format.
  - `time`: Time string in `HH:MM AM/PM` format.

- **Returns**: Timestamp of the provided date and time.

### `getESTDateTimeTimestamp`

```javascript
export function getESTDateTimeTimestamp(date, time)
```

**Purpose**: Converts a date and time to an EST timezone timestamp.

- **Parameters**:
  - `date`: Date string.
  - `time`: Time string, supports both 12-hour and 24-hour formats.

- **Returns**: Timestamp adjusted to EST timezone.

### `convertDateFormat`

```javascript
export const convertDateFormat = (format) => { ... }
```

**Purpose**: Converts a date from `YYYY-MM-DD` format to `MM-DD-YYYY`.

- **Parameters**:
  - `format`: Date string in `YYYY-MM-DD`.

- **Returns**: Date string in `MM-DD-YYYY`.

### `checkIfLinkIsNeeded`

```javascript
export const checkIfLinkIsNeeded = (gameslug) => { ... }
```

**Purpose**: Checks if a link is needed for a specific game based on its slug.

- **Parameters**:
  - `gameslug`: The slug identifier for a game.

- **Returns**: Boolean indicating if a link is needed.

### `checkMatchDateTime`

```javascript
export const checkMatchDateTime = ( tournamentStartDate, tournamentStartTime, matchStartDate, matchStartTime )
```

**Purpose**: Validates that the match start time is greater than the tournament start time.

- **Parameters**:
  - `tournamentStartDate`: Start date of the tournament.
  - `tournamentStartTime`: Start time of the tournament.
  - `matchStartDate`: Start date of the match.
  - `matchStartTime`: Start time of the match.

- **Throws**: Error if the match start time is not valid.

### `findMaxSubMatchLength`

```javascript
export const findMaxSubMatchLength = (roundData, roundId) => { ... }
```

**Purpose**: Finds the maximum number of sub-matches within a specific round.

- **Parameters**:
  - `roundData`: Array of round data.
  - `roundId`: The ID of the round for which to find the max sub-match length.

- **Returns**: Maximum length of sub-matches found in the specified round.

### `getESTDateTimeTimestampWithMinus10Minutes`

```javascript
export const getESTDateTimeTimestampWithMinus10Minutes = (date, time) => { ... }
```

**Purpose**: Provides the timestamp 10 minutes before the given date and time in EST.

- **Parameters**:
  - `date`: Date string.
  - `time`: Time string.

- **Returns**: Timestamp 10 minutes prior to the provided date and time.

### `checkLastEntryTime`

```javascript
export const checkLastEntryTime = (matchStartDate, matchStartTime) => { ... }
```

**Purpose**: Ensures the last entry time is later than the current EST time.

- **Parameters**:
  - `matchStartDate`: Start date of the match.
  - `matchStartTime`: Start time of the match.

- **Throws**: Error if the last entry time is not valid.

### `checkLastEntryTimeForSubmatchesEdit`

```javascript
export const checkLastEntryTimeForSubmatchesEdit = ( startDate, lastEntryTime )
```

**Purpose**: Checks if the last entry time for editing sub-matches is valid.

- **Parameters**:
  - `startDate`: Start date of the sub-match.
  - `lastEntryTime`: Last entry time for the sub-match.

- **Returns**: Boolean indicating if editing is allowed.

### `convertTo24HourFormat`

```javascript
export const convertTo24HourFormat = (time) => { ... }
```

**Purpose**: Converts a 12-hour time format to a 24-hour format.

- **Parameters**:
  - `time`: Time string in `HH:MM AM/PM`.

- **Returns**: Time string in 24-hour format `HH:MM`.

## Constants

### `uploadFileslug`

A constant array containing game IDs and their slugs, used to check if a link is needed for specific games.

```javascript
const uploadFileslug = [
  { id: 1, slug: "fortnite" },
  { id: 2, slug: "pubg-mobile" },
  { id: 3, slug: "cod-mobile" },
];
```

## Conclusion

The `utils.jsx` file provides essential utility functions for handling tournament scheduling and validation, ensuring that date and time constraints are respected. These utilities support the broader functionality of managing tournament logistics efficiently.

# Documentation for ViewBracket.jsx 📄

## Overview

The **ViewBracket.jsx** component is responsible for fetching and displaying a tournament bracket based on the provided `bracketId`. It retrieves the bracket's HTML content from an API and embeds it within an iframe after removing any unwanted elements, such as an embed logo.

---

## Components and Functions

### React Imports

- **React, useState, useEffect**: Core React library and hooks used for managing state and side effects.

### Third-Party Libraries

- **Spinner** (from `react-bootstrap`): A spinner component used to indicate loading state.

### Services

- **getBracketsTempalate**: A function imported from the API helper services to fetch the bracket template HTML using a `bracketId`.

---

## Component Logic

### State Variables

- **`htmlSource`**: A state variable to store the fetched HTML content of the bracket.
- **`isLoading`**: A boolean state variable to manage the loading state of the component.

### Effects

- **useEffect Hook**: Triggers the **fetchData** function whenever the `bracketId` changes. This effect fetches the bracket HTML and updates the state with the modified content.

### Functions

#### fetchData
- **Purpose**: Fetches the bracket HTML template, processes it to remove any specific elements (like embed logos), and updates the component state.
- **Process**:
  1. Sets `isLoading` to `true` to initiate a loading state.
  2. Fetches bracket HTML using `getBracketsTempalate`.
  3. Calls `removeEmbedLogo` to clean up the HTML.
  4. Updates `htmlSource` with the cleaned HTML.
  5. Handles any errors by logging them to the console.

#### removeEmbedLogo
- **Purpose**: Removes the embed logo element from the fetched HTML content.
- **Process**:
  1. Parses the HTML string into a DOM object.
  2. Locates and removes the element with the ID `embed-logo`.
  3. Returns the cleaned HTML as a string.

---

## Render Logic

- **Loading Spinner**: While `isLoading` is `true`, display a spinner to indicate that the content is being loaded.
- **Iframe**: Once loading is complete, an iframe is rendered to display the bracket using the `htmlSource` state.

```jsx
return (
  <div>
    {isLoading ? (
      <Spinner animation="border" role="status">
        <span className="visually-hidden">Loading...</span>
      </Spinner>
    ) : (
      <iframe
        id="my-iframe"
        title="Bracket Preview Tournament"
        srcdoc={htmlSource}
        width="100%"
        height="500"
      ></iframe>
    )}
  </div>
);
```

---

## Error Handling

- The component logs any errors that occur during the fetch operation to the console, ensuring that failure to load the bracket does not cause a crash.

---

## Conclusion

The **ViewBracket.jsx** component provides a seamless way to display tournament brackets by embedding HTML content within an iframe. This allows for dynamic content loading and easy integration within a larger application using React.

# Documentation for ViewManualCreatedBracket.jsx

## Overview
The `ViewManualCreatedBracket.jsx` component is a React functional component responsible for displaying a manually created tournament bracket. It allows users to view different rounds of matches and interact with individual matches to see the teams involved. This component is particularly useful in scenarios where brackets are not automatically generated and need manual adjustments or reviews.

## Key Features
- **Displays Tournament Rounds**: Shows the different rounds in a tournament and the matches within each round.
- **Interactive Matches**: Allows users to click on a match to see more details about the teams involved in a modal.
- **Responsive Design**: Designed to fit within a responsive layout.

## Imports
- **React**: Core library for building the user interface.
- **useState**: A React hook for managing local component state.
- **PPKTeamsModal**: A modal component to display teams in a match.

## Component Details

### State Management
- **show**: A boolean state to control the visibility of the `PPKTeamsModal`.
- **teamsInRound**: An array that stores the teams involved in a selected match.
- **matchNumber**: A string to store the current match number being viewed.

### Methods

#### handleMatches
```jsx
const handleMatches = (teams, matchNo) => {
    setShow(teams.length !== 0);
    setTeamsInRound(teams);
    setMatchNumber(matchNo);
};
```
This method is invoked when a match is clicked. It sets the teams and match number for the selected match and displays the modal if there are teams present.

#### handleClose
```jsx
const handleClose = () => {
    setShow(false);
    setTeamsInRound([]);
    setMatchNumber("");
};
```
This method is responsible for closing the modal and resetting the state related to the teams and match number.

### Rendered Elements

#### Div Structure
- **round-brackets-preview**: Main container for the bracket.
- **bracket-ctn**: Contains two primary sections: `round-comments` and `matches`.

#### Rounds and Matches
- **Round Titles**: Each round is displayed with a title like "Round 1", "Round 2", etc.
- **Match Containers**: Each match is clickable and displays the number of teams involved. Clicking a match triggers the `handleMatches` function.

### PPKTeamsModal
A modal component that displays detailed information about the teams in a selected match. It is shown when a match is clicked and closed using the `handleClose` method.

## Usage
To use this component, you should pass the `details` prop, which includes the tournament data structured in rounds and matches. Each match can be interacted with to reveal more details in a modal.

### Example
```jsx
<ViewManualCreatedBracket details={tournamentDetails.match_info} />
```

## Conclusion
The `ViewManualCreatedBracket` component provides a clean and interactive way to visualize and manage tournament brackets manually. It ensures that users can access detailed match information through a simple and intuitive interface, making it an essential part of a tournament management system.

# Documentation for `ViewMatches.js`

This document provides a detailed explanation of the `ViewMatches.js` file, including the purpose of the component, its functionalities, and how it interacts with other components and services.

## Overview

The `ViewMatches` component is a React functional component that displays a table of match data with details like start and end times, admin codes, participant codes, and map information. It also provides functionality to edit admin and participant codes for matches and view detailed information about each match when required.

## Key Features

- Display match details in a structured table format.
- Ability to edit admin and participant codes for specific matches.
- Conditional rendering based on game slugs to determine if additional functionalities are needed.
- Handles navigation to detailed match views when clicked.

## Dependencies

- **React Components**: Utilizes standard React hooks like `useState`.
- **React Router**: For navigation through `useHistory`.
- **Reactstrap**: Provides UI components such as `Button`.
- **Utilities**: Imports utility functions like `checkIfLinkIsNeeded`, `checkLastEntryTimeForSubmatchesEdit`, and `convertDateFormat` from `utils`.

## Component Breakdown

### Props

- **matchData**: Object containing all the match details including sub-matches.
- **gameslug**: String indicating the game type (e.g., "cod-mobile").
- **nameOfGame**: String representing the name of the game.
- **isPPK**: Boolean indicating if the game is of type PPK.
- **successCallBack**: Function callback to handle successful updates.

### State

- **editAdminCodeIndex**: Index of the sub-match currently being edited for the admin code.
- **editParticipantCodeIndex**: Index of the sub-match currently being edited for the participant code.

### Main Functionalities

1. **Rendering Table**: 
    - Renders a table displaying matches with columns for match number, start and end times, admin/participant codes, statistical code, map, and optional view details button.

2. **Edit Functionality**:
    - Allows editing of admin and participant codes for matches if conditions are met (e.g., correct game slug and last entry time checks).
    - Uses `UpdateAdminCode` component to manage the edit forms for admin and participant codes.

3. **Conditional Links**:
    - Checks if a link is needed for specific game types using `checkIfLinkIsNeeded`.
    - Provides a button to navigate to the detailed match view when required.

### Functions

- **handleClick**: Navigates to the detailed view of a lobby based on its ID.
- **handleSaveEditAdminCode**: Saves the updated admin code and triggers a success callback.
- **handleCloseEditAdminCode**: Closes the admin code edit form without saving.
- **handleSaveEditParticipantCode**: Saves the updated participant code and triggers a success callback.
- **handleCloseEditParticipantCode**: Closes the participant code edit form without saving.

### UI Elements

- **Buttons**: Used for triggering edit actions and viewing details.
- **Table**: Displays match data with rows for each sub-match.

## Code Snippet

```jsx
return (
  <div className="table-rep-plugin">
    <div className="table-responsive mb-0" data-pattern="priority-columns">
      <div className="table-responsive seize-wallet-table">
        <table className="table table-striped table-bordered manage-complaints-table lobbies-table">
          <thead>
            <tr>
              <th scope="col" rowspan="2"> Match </th>
              <th scope="col" rowspan="2"> Start Date Time </th>
              <th scope="col" rowspan="2"> End Date Time </th>
              <th scope="col" rowspan="2"> Admin code </th>
              <th scope="col" rowspan="2"> Statistical Code </th>
              <th scope="col" rowspan="2"> Participant Code </th>
              <th scope="col" rowspan="2"> Map </th>
              {isLinkRequired ? (
                <th scope="col" rowspan="2"> View Details </th>
              ) : null}
            </tr>
          </thead>
          <tbody>
            {matchData.sub_match.map((item, index) => {
              const isLastEntryTimeGreater = checkLastEntryTimeForSubmatchesEdit(item.lobby.start_date, item.lobby.last_entry_time);
              return (
                <tr key={index} id={index}>
                  <td className="text-capitalize">{item.sub_match} <span className="text-lowercase"> of</span> {matchData.match}</td>
                  <td>{convertDateFormat(item.lobby.start_date)} {item.lobby.start_time}</td>
                  <td>{item.lobby.end_date === null ? "NA" : `${convertDateFormat(item.lobby.start_date)} ${item.lobby.end_time}`}</td>
                  <td>
                    {/* Edit Admin Code Logic */}
                  </td>
                  <td>{item.lobby.stats_code || "NA"}</td>
                  <td>
                    {/* Edit Participant Code Logic */}
                  </td>
                  <td>{item.lobby.map || "NA"}</td>
                  {isLinkRequired ? (
                    <td>
                      <Button className="px-0 pt-0 pb-0 text-start" color="link" onClick={() => handleClick(item?.lobby?.lobby_id)}>
                        {item?.lobby?.name}
                      </Button>
                    </td>
                  ) : null}
                </tr>
              );
            })}
          </tbody>
        </table>
      </div>
    </div>
  </div>
);
```

## Conclusion

The `ViewMatches` component is designed to provide a detailed view of match data with options to edit specific fields and navigate to more detailed views. It leverages several utility functions and conditional rendering to enhance user interaction and maintain code clarity.

# AddManualWinner.jsx Documentation 📄

The `AddManualWinner.jsx` component is a React functional component designed to handle the manual addition of winners for a specific match within a tournament. It provides a form interface for selecting one or more winning teams, depending on the type of tournament (Traditional or not). This component uses `availity-reactstrap-validation` for form validation and management.

## Component Overview

### Imports

- **React and Hooks**: Utilizes `useState` from React for managing component state.
- **AvForm Components**: Imports components like `AvForm`, `AvCheckboxGroup`, `AvCheckbox`, `AvRadioGroup`, and `AvRadio` from `availity-reactstrap-validation` for form handling.
- **Reactstrap Components**: Imports `Row`, `FormGroup`, and `Button` from `reactstrap`.
- **API Helper**: `addManualWinner` function from `bracket_tournaments_api_helper` to submit the selected winners.
- **Toastr**: Uses `toast` from `react-toastify` to display success or error messages.
- **Toastr Options**: Custom options for toastr notifications.

### Props

- `teams`: Array of team objects available for selection as winners.
- `matchId`: The ID of the match for which winners are being added.
- `isTraditional`: Boolean indicating if the tournament type is Traditional.
- `successCallBack`: Function to call on successful submission.
- `closeAddWinnerModal`: Function to close the modal after adding winners.
- `threshold`: Maximum number of winners that can be selected.

### State Variables

- **`disabled`**: Boolean state to manage the submit button's disabled state during form submission.
- **`error`**: String state to store any validation error messages related to threshold.

### Key Functions and Logic

- **`handleValidSubmit`**: Handles form submission, constructing the data object based on whether the tournament is Traditional. It makes an API call to add the selected winners and invokes callback functions on success.
  
- **`thresholdValidation`**: Validates the number of selected teams against the provided threshold, updating the `error` state if the selection exceeds the threshold.

### Rendered Output

- **Form Structure**: 
  - Utilizes `AvForm` for validation.
  - Depending on `isTraditional`, renders either `AvRadioGroup` (for selecting a single team) or `AvCheckboxGroup` (for selecting multiple teams).
  - Maps over the `teams` array to generate radio buttons or checkboxes for each team.
  
- **Submit Button**: 
  - Displays a spinner when `disabled` is true, indicating a loading state during submission.

- **Validation**: 
  - Enforces selection constraints and provides error messages when criteria are not met.

### Example Usage

```jsx
<AddManualWinner
  teams={teamList}
  matchId={123}
  isTraditional={false}
  successCallBack={updateMatchDetails}
  closeAddWinnerModal={closeModal}
  threshold={2}
/>
```

### Visuals

The component presents a form allowing users to select winners from a list of teams. Depending on the tournament type, users can either select a single winner or multiple winners, adhering to the threshold set. A submit button is available to finalize the selection, with loading and error states managed intuitively.

### Conclusion

The `AddManualWinner` component is a robust tool for tournament administrators to manage match outcomes manually. By leveraging form validation and state management, it ensures a smooth user experience and accurate data entry.

# Documentation for Tournament Management System

## Table of Contents

1. **Introduction**
2. **Components Overview**
   - TournamentDetails.jsx
   - TournamentsList.jsx
   - useStateWithCallback.jsx
   - AddWinningPercentage.jsx
   - AddTournamentSchedule.jsx
   - ChangeAssignedAdmin.jsx
   - PrizeList.jsx
   - TournamentScheduleTable.js
   - TournamentsRoundHeading.js
   - UpdateAdminCode.jsx
   - utils.jsx
   - ViewBracket.jsx
   - ViewManualCreatedBracket.jsx
   - ViewMatches.js
   - AddManualWinner.jsx
   - AddBestOfMatches.js

---

## Introduction

This documentation provides an overview of a series of React components and utility functions designed to manage and display information about tournaments. They cover various functionalities such as viewing and editing tournament details, scheduling matches, assigning admins, and handling tournament rounds.

---

### AddBestOfMatches.js

The `AddBestOfMatches.js` file is a React component focusing on adding "Best of" matches to a tournament round. This involves setting up a series of matches with details like start and end times, participant codes, and more.

#### Key Features

- Utilizes `AvForm` and `AvField` for form validations to capture match-related data.
- Employs utility functions to manage and validate time-related data.
- Uses Redux for state management, particularly for handling match schedules.
- Provides real-time feedback with Toast notifications for successful operations.
- Dynamic generation of form fields based on the number of matches (`maxSubMatchLength`).

#### Code Breakdown

##### Imports

- **React Libraries:** Handles state and effect management with hooks like `useState` and `useEffect`.
- **Utility Functions:** Uses helper functions for date-time manipulation and validation.
- **Styling and UI Libraries:** Includes components from `reactstrap` for UI elements.

##### State Management

- **State Variables:** Manages multiple states like `countForForm`, `startTimeByID`, `multipleFormValues`, etc., to handle form data and validations.
- **Redux:** Dispatches actions to update the global state with match schedules.

##### Event Handlers

- **handleValidSubmit:** Validates and submits the form data for each match, ensuring that the start dates and times are consistent with tournament requirements.
- **addMinutes:** Adjusts the time for match entries, ensuring constraints are met.

##### Validation

- **Date and Time Checks:** Uses custom validations to ensure schedules do not conflict and that entries are future-dated and adhere to tournament start times.
- **Error Handling:** Provides descriptive error messages if validations fail.

#### UI Components

- **Accordion:** Utilizes an accordion component to manage the display of multiple match forms, enhancing the user interface for handling match details.
- **Flatpickr:** Used for date and time picking, ensuring a consistent user experience across time zones.
- **Buttons and Labels:** Provides simple feedback and clear instructions through buttons and labels within the form.

##### Example of Use

```jsx
<AvForm onValidSubmit={(e, v) => { handleValidSubmit(e, v, item.id); }}>
  <AccordionItem key={item.id} uuid={item.id}>
    <AccordionItemHeading>
      <AccordionItemButton>
        {item.match}
      </AccordionItemButton>
    </AccordionItemHeading>
    <AccordionItemPanel accordionId={item.id}>
      {/* Form Elements */}
    </AccordionItemPanel>
  </AccordionItem>
</AvForm>
```

This component is critical for ensuring that tournament matches are scheduled accurately and efficiently, adhering to all predefined rules and constraints.

---

### Conclusion

Each component plays a specific role in the tournament management system, allowing for a comprehensive and cohesive application that handles complex scheduling, management, and display tasks. The use of modern React features and libraries ensures that the system is both robust and user-friendly.

# Documentation for `ManualPlacementAddRankForTeam.jsx`

## Overview
The `ManualPlacementAddRankForTeam` component provides a user interface for manually assigning ranks to teams within a tournament. This component allows administrators to input and submit team rankings, ensuring that each team has a unique rank.

## Components and Libraries Used

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library for Bootstrap components in React.
- **React-Toastify**: A library for displaying notifications.
- **React Accessible Accordion**: A library for creating accessible accordion components.
- **Custom Components**:
  - `PlayersRankInfoTable`: Displays information about players in a team.

## Features

- **Accordion Display**: Teams are displayed in an accordion format, allowing users to expand and view details about each team.
- **Rank Input**: Provides an input field for setting the rank of each team.
- **Validation**: Ensures that no two teams have the same rank and ranks are greater than zero.
- **Submit Button**: Allows submission of the ranking data after validation.

## Code Explanation

### State Variables

- `rankData`: Stores the rank information for each team.
- `errorForDuplicateTeamRank`: Holds error messages when duplicate ranks are detected.
- `isRankInputFocused`: Manages the focus state of rank input fields.

### Functions

- **handleSubmit**: Gathers rank data and submits it. Handles validation to ensure no duplicate ranks are present before calling the API.
  
  ```jsx
  const handleSubmit = () => {
      // Validate and prepare rank data for submission
  };
  ```

- **callSubmitApi**: Sends the rank data to the server through an API call. Displays success or error messages using `toast`.

  ```jsx
  const callSubmitApi = async (payload) => {
      // API call to submit the rank data
  };
  ```

- **handleTeamRank**: Updates the `rankData` state when a rank is input by the user.

  ```jsx
  const handleTeamRank = (index, e, item) => {
      // Update rankData based on user input
  };
  ```

## UI Structure

### Main Render

- **Accordion**: Each team is represented as an accordion item. The accordion displays the team name and allows the user to input a rank.

  ```jsx
  <AccordionItem key={idx}>
      <AccordionItemHeading>
          <AccordionItemButton>
              {/* Displays team name and input for rank */}
          </AccordionItemButton>
      </AccordionItemHeading>
      <AccordionItemPanel>
          {/* Displays team players information */}
      </AccordionItemPanel>
  </AccordionItem>
  ```

- **Submit Button**: Located at the bottom, it triggers the submission of rank data if all inputs are valid.

  ```jsx
  <Button type="submit" onClick={handleSubmit} disabled={rankData.length === 0 ? true : !disableSubmit}>
      Submit
  </Button>
  ```

### Error Handling

- Displays error messages if duplicate ranks are detected or other validation issues occur.

  ```jsx
  <Label className={errorForDuplicateTeamRank !== "" ? "errorMsgGames invalid-feedback" : ""}>
      {errorForDuplicateTeamRank}
  </Label>
  ```

## Usage

This component is designed for administrative users who need to assign ranks to teams in a tournament. It ensures that all teams have a unique rank and provides feedback if any issues occur during data input.

## Conclusion

The `ManualPlacementAddRankForTeam` component is an essential tool for tournament management, allowing precise control over team rankings. Its combination of React, Reactstrap, and other libraries ensures a user-friendly and accessible interface.

# AddTournaments.jsx Documentation

The `AddTournaments.jsx` file is a React component that allows users to add or edit tournaments in a web application. This document provides a detailed explanation of the component's functionality, including its props, state management, and various methods used to handle form submissions, validations, and UI interactions.

---

## Table of Contents

1. [Component Overview](#component-overview)
2. [State Variables](#state-variables)
3. [Props](#props)
4. [Lifecycle Methods and Hooks](#lifecycle-methods-and-hooks)
5. [Functions and Methods](#functions-and-methods)
6. [Form Validation and Submission](#form-validation-and-submission)
7. [UI Elements and Interactions](#ui-elements-and-interactions)
8. [Dependencies](#dependencies)

---

## Component Overview

The `AddTournaments` component is responsible for rendering a form that allows users to create a new tournament or edit an existing one. The form includes fields for tournament name, game type, entry fee, bracket style, seeding options, and more. It also manages file uploads and integrates with AWS S3 for storing files related to the tournament.

## State Variables

- **Form Handling**
  - `gameTypeMode`: Manages the selected game type mode (PPK or Traditional).
  - `selectedGame`: Tracks the selected game.
  - `selectedBracketStyle`: Stores the selected bracket style.
  - `selectedSeeding`: Manages seeding options.
  - `selectedMinTeam`, `selectedMaxTeam`: Store minimum and maximum team selections.

- **Tournament Details**
  - `tournamentName`: Holds the name of the tournament.
  - `entryFee`: Stores the entry fee for players.
  - `rules`, `tournamentRules`: Manage the rules entered for the tournament.

- **Time and Date Management**
  - `startTime`, `endTime`: Manage start and last entry times.
  - `userInputStartDate`: Holds the start date of the tournament.

- **Miscellaneous**
  - `showLoader`: Controls visibility of a loading spinner.
  - `isEdit`: Boolean flag indicating if the form is in edit mode.
  - `fileUpload`: Stores information about files to be uploaded to S3.

## Props

- `props.match.params.tournamentId`: Used to determine if the form is in edit mode.
- `props.game`: Contains game-related data fetched from Redux state.

## Lifecycle Methods and Hooks

- **`useEffect`**: Several `useEffect` hooks are employed to manage initial data fetching, form setup, and dynamic updates based on state changes.
  - Fetches tournament data if in edit mode.
  - Loads game data if not already present.
  - Sets up bracket styles and seeding options based on game type.

## Functions and Methods

### Form Handling

- **`handleValidSubmit`**: Validates and submits form data, managing both creation and editing of tournaments.
- **`handleInvalidSubmit`**: Handles validation errors, setting appropriate error messages for form fields.

### Data Management

- **`getTournamentEditData`**: Fetches data for an existing tournament to populate the form when in edit mode.
- **`mapDetailsToForm`**: Maps fetched tournament details to form inputs for editing.
- **`uploadToS3`**: Handles file uploads to AWS S3 and manages the response.
- **`uploadFormData`**: Submits form data to the server via API calls.

### UI Controls

- **`handleGameTypeChange`**: Adjusts form options based on selected game type.
- **`handleBracketStyleChange`**: Updates state when a user selects a different bracket style.
- **`handleSelectGroup`**: Updates game-related selections and options.

## Form Validation and Submission

The component uses `availity-reactstrap-validation` for form validation. Key validations include:

- Required fields: Tournament name, entry fee, game type.
- Numeric validations: Entry fee, team counts, and lobby size.
- Time validations: Ensuring the tournament start time is in the future.

## UI Elements and Interactions

- **React-Select**: Used for dropdowns to select game types, games, and other options.
- **Switches**: Used for toggling features like active status and free tournament setting.
- **Flatpickr**: Utilized for date and time selection.

## Dependencies

- **React & Reactstrap**: Core libraries for building the UI.
- **AWS S3 SDK**: Used for file uploads to Amazon S3.
- **Redux**: State management for shared game data.
- **React-Toastify**: Provides toast notifications for user feedback.
- **Availity Validation**: Handling form validation.

---

This documentation provides a comprehensive overview of the `AddTournaments.jsx` component, outlining its purpose, functionality, and integration within the larger application framework. The component is a critical part of the tournament management system, offering administrators flexible options for configuring tournaments.

# Documentation for `ManuallyAddWinnerModal.jsx` 📄

The `ManuallyAddWinnerModal.jsx` file is a React component that provides a user interface for manually selecting a winning team or teams for a match in a tournament. This component is particularly useful when automated systems cannot determine a winner, and manual intervention is required.

## Component Overview

### Imports
- `React`: The core library for building user interfaces.
- `AddManualWinner`: A child component that handles the logic and UI for selecting winners.
- `isEmpty`: A utility from Lodash to check if the provided object is empty.

### Component: `ManuallyAddWinnerModal`

#### Props
The component accepts the following props:
- **`teams`**: An array of team objects available to select as winners.
- **`matchId`**: The identifier for the match where a winner is being selected.
- **`gameTypeIsTraditional`**: A boolean indicating whether the game is of a traditional type, which affects winner selection logic.
- **`successCallBack`**: A callback function to invoke upon successful submission of a winner.
- **`closeAddWinnerModal`**: A function to close the modal after the winner is added.
- **`threshold`**: The maximum number of winners that can be selected.

#### Structure
- The component checks if the `teams` array is empty using `isEmpty`.
- If `teams` is empty, it displays a message "No Team Found".
- If `teams` are available, it renders the `AddManualWinner` component, passing down necessary props to manage the winner selection process.

### Usage
This component is typically used within a modal context where a tournament administrator can manually select a winner for a given match. It handles the display logic and delegates the functional logic to `AddManualWinner`.

### Example Usage
```jsx
<ManuallyAddWinnerModal
  teams={teamsData}
  matchId={123}
  gameTypeIsTraditional={true}
  successCallBack={handleSuccess}
  closeAddWinnerModal={closeModal}
  threshold={1}
/>
```

### Key Points
- **Flexibility**: The component supports both single and multiple winner selection modes based on the game type and threshold.
- **Reusability**: By delegating the primary logic to `AddManualWinner`, this component remains focused on controlling modal display and interaction.
- **Dependency**: Relies on the `AddManualWinner` component to handle detailed winner selection and submission logic.

By providing a clean interface to manually select match winners, `ManuallyAddWinnerModal` is an essential component in managing tournament results when automation falls short.

# 📑 Documentation for `PPKTeamsModal.jsx`

## Overview
The `PPKTeamsModal.jsx` file defines a React component that presents a modal dialog to display a list of teams for a specific match in a Player vs. Player Knockout (PPK) style tournament. The modal provides an organized view of the team details using a table component.

## Component Breakdown

### `PPKTeamsModal`
This is the main component exported from the file. It is a functional React component that uses Reactstrap's `Modal` for rendering a pop-up window.

#### Props
- **`show`**: A boolean that controls the visibility of the modal. If `true`, the modal is displayed.
- **`teams`**: An array containing team data to be displayed in the modal.
- **`match`**: A string or number representing the match identifier, used in the modal header.
- **`closeModal`**: A function to be called when the modal needs to be closed. This function typically changes the `show` state in the parent component to `false`.

### Reactstrap Components
- **`Modal`**: A container for the modal dialog.
- **`ModalHeader`**: Displays the header of the modal, including an optional close button.
- **`ModalBody`**: Contains the main content of the modal, which includes the team data table.

### Custom Components
- **`PPKTeamTable`**: This custom component is imported and used to render the team data in a table format within the modal body.

## Usage Example
The `PPKTeamsModal` component can be used in any parent component that manages the state for showing or hiding the modal and provides the necessary team data. Here is an example of how it might be integrated:

```jsx
import React, { useState } from 'react';
import PPKTeamsModal from './PPKTeamsModal';

const ExampleComponent = () => {
  const [showModal, setShowModal] = useState(false);
  const [teams, setTeams] = useState([...]); // Teams data
  const matchNumber = 1;

  const toggleModal = () => {
    setShowModal(!showModal);
  };

  return (
    <>
      <button onClick={toggleModal}>View Teams</button>
      <PPKTeamsModal
        show={showModal}
        teams={teams}
        match={matchNumber}
        closeModal={toggleModal}
      />
    </>
  );
};

export default ExampleComponent;
```

## Code Explanation

```jsx
import React from "react";
import { Modal, ModalBody, ModalHeader } from "reactstrap";
import PPKTeamTable from "../Table/PPKTeamTable";

const PPKTeamsModal = ({ show, teams, match, closeModal }) => {
  return (
    <Modal isOpen={show} scrollable={true} className="custom-modal w-706">
      <ModalHeader toggle={closeModal} tag="h4" className="text-capitalize">
        Match {match}
      </ModalHeader>
      <ModalBody className="events">
        <PPKTeamTable teams={teams} />
      </ModalBody>
    </Modal>
  );
};

export default PPKTeamsModal;
```

### Key Points
- **Modal Visibility**: Controlled by the `show` prop, making it flexible to integrate with various state management solutions.
- **Team Data Display**: Utilizes the `PPKTeamTable` component to format and present team information neatly.
- **Responsive Design**: The modal is designed to be scrollable, ensuring usability even with extensive data.

## Conclusion
The `PPKTeamsModal` component provides a clean and efficient way to display team-related information in a modal dialog. By leveraging Reactstrap for UI components, it maintains a consistent look that can be easily customized and integrated within larger applications.

# PrizeListModal.jsx Documentation 📜

## Overview
The `PrizeListModal.jsx` file is a React component that renders a modal dialog displaying a list of prizes associated with tournament positions. The component uses the Reactstrap library for styling and modal functionality.

## Component Structure

### Imports
- **React**: The core library for building the component.
- **appendSuffixToTournamentPosition**: A helper function from `../../../helpers/util` used to append ordinal suffixes to the tournament positions.
- **Modal, ModalBody, ModalHeader**: Components from the `reactstrap` library used to structure and style the modal.

### Component Definition
```jsx
const PrizeListModal = ({ show, prizelist, closeModal }) => {
  ...
};
```
- **Props**:
  - `show`: A boolean indicating whether the modal should be visible.
  - `prizelist`: An array of prize objects, each containing a `position` and `price`.
  - `closeModal`: A function to close the modal when invoked.

### Rendered Output
- **Modal**: The main container for the modal content.
  - **ModalHeader**: Displays the title "Prizes" and includes a toggle function to close the modal.
  - **ModalBody**: Contains the prize details wrapped in a flex container for layout.

### Prize List
The prize list is displayed as a series of div elements, each representing a prize position and its associated monetary value.

```jsx
<div className="d-flex flex-wrap prizes">
  {prizelist
    .sort((first, second) => {
      return first.position > second.position ? 1 : -1;
    })
    .map((item, idx) => {
      return (
        <div key={idx} className="prize-div" id={idx}>
          <p className="mb-0 color-white">
            {`${item.position}${appendSuffixToTournamentPosition(item.position)}`} Prize
          </p>
          <p className="mb-0 theme-color">$ {item.price}</p>
        </div>
      );
    })}
</div>
```

### Key Features
- **Sorting**: The prizes are sorted in ascending order based on their position.
- **Dynamic Styling**: Each prize is displayed with specific styling using classes like `color-white` and `theme-color`.
- **Ordinal Suffix**: The `appendSuffixToTournamentPosition` function is used to format the position with the correct ordinal suffix (e.g., "1st", "2nd", "3rd").

## Usage
This component is designed to be used in applications where displaying tournament prize information in a modal format is needed. It is flexible and can be easily integrated with other components through props for dynamic content control.

## Example
```jsx
<PrizeListModal
  show={isModalOpen}
  prizelist={[
    { position: 1, price: 500 },
    { position: 2, price: 300 },
    { position: 3, price: 200 },
  ]}
  closeModal={() => setModalOpen(false)}
/>
```

## Conclusion
The `PrizeListModal.jsx` component offers a clean and structured way to display tournament prize information in a modal dialog, with built-in sorting and formatting functionalities. It leverages Reactstrap for styling and responsive behavior, ensuring a seamless integration into any React project.

# Documentation for `ViewMoreTeamsModal.jsx`

The `ViewMoreTeamsModal.jsx` file is a React component that renders a modal to display a list of teams. It utilizes the `reactstrap` library for modal creation and includes a table component to organize and present the team data.

## Table of Contents

- [Component Overview](#component-overview)
- [Dependencies](#dependencies)
- [Component Props](#component-props)
- [Component Structure](#component-structure)
- [Usage](#usage)
- [Conclusion](#conclusion)

## Component Overview

The `ViewMoreTeamsModal` component is a modal that displays a detailed list of teams. It is designed to be flexible and reusable across different parts of an application that require viewing more information about teams.

## Dependencies

The component relies on the following dependencies:

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: A library that provides Bootstrap 4 components for React. Specifically, it uses `Modal`, `ModalBody`, and `ModalHeader` from this library.
- **ViewMoreTeamTable**: A custom component imported from the `../Table/ViewMoreTeamTable` path, which is used to render the table of teams inside the modal.

## Component Props

The `ViewMoreTeamsModal` component accepts the following props:

| Prop Name  | Type   | Description                                         |
|------------|--------|-----------------------------------------------------|
| `show`     | `bool` | Determines if the modal is open or not.             |
| `teamList` | `array`| An array containing the list of teams to display.   |
| `closeModal` | `func` | A function to close the modal.                     |
| `roundTable` | `bool` | A flag to indicate if the data is in round table format. |

## Component Structure

The component is structured as follows:

```jsx
import React from "react";
import { Modal, ModalBody, ModalHeader } from "reactstrap";
import ViewMoreTeamTable from "../Table/ViewMoreTeamTable";

function ViewMoreTeamsModal({ show, teamList, closeModal, roundTable }) {
  return (
    <Modal isOpen={show} scrollable={true} className="custom-modal w-706">
      <ModalHeader toggle={closeModal} tag="h4" className="text-capitalize">
        Teams
      </ModalHeader>
      <ModalBody className="events">
        <div className="view-more-teams">
          <ViewMoreTeamTable teamList={teamList} roundTable={roundTable} />
        </div>
      </ModalBody>
    </Modal>
  );
}

export default ViewMoreTeamsModal;
```

### Explanation

- **Modal**: The component uses the `Modal` component from `reactstrap` to encapsulate the team list in a modal dialog.
- **ModalHeader and ModalBody**: These components are used to structure the modal, with the header displaying the title "Teams" and the body containing the team table.
- **ViewMoreTeamTable**: This is the table component that receives the `teamList` and `roundTable` props for rendering the team data accordingly.
- **Props Spread**: The `show`, `teamList`, `closeModal`, and `roundTable` props are used to control the modal's visibility, data, and interactions.

## Usage

To use the `ViewMoreTeamsModal` component, you need to provide the required props when rendering it within your application:

```jsx
<ViewMoreTeamsModal 
  show={isModalOpen} 
  teamList={teamsArray} 
  closeModal={handleModalClose} 
  roundTable={isRoundTableFormat} 
/>
```

### Example

```jsx
function ParentComponent() {
  const [isModalOpen, setModalOpen] = useState(false);
  const teamsArray = [
    { name: "Team A", members: 5 },
    { name: "Team B", members: 4 },
  ];

  const handleModalClose = () => {
    setModalOpen(false);
  };

  return (
    <div>
      <button onClick={() => setModalOpen(true)}>View Teams</button>
      <ViewMoreTeamsModal 
        show={isModalOpen} 
        teamList={teamsArray} 
        closeModal={handleModalClose} 
        roundTable={false} 
      />
    </div>
  );
}
```

## Conclusion

The `ViewMoreTeamsModal` component is a simple yet effective way to display additional team information in a modal format. By leveraging `reactstrap` and a custom table component, it provides a clean and responsive solution for viewing team data.

# Documentation for `ViewStats.jsx`

The `ViewStats.jsx` component is designed to display a modal window that presents the stats for a particular game or tournament. This component is part of a larger application dealing with tournament management and player statistics. Below is a detailed explanation of the component, including its functionality and usage.

## Index
- [Overview](#overview)
- [Props](#props)
- [Component Structure](#component-structure)
- [Usage](#usage)
- [Dependencies](#dependencies)
- [Conclusion](#conclusion)

---

## Overview

The `ViewStats` component utilizes a modal to encapsulate and present player statistics and game data. This modal can be toggled to show or hide the statistics, providing a detailed view of the player's performance in a specific lobby or tournament context. 

## Props

The `ViewStats` component receives several props to customize its behavior:

| Prop Name   | Type      | Description                                                                 |
|-------------|-----------|-----------------------------------------------------------------------------|
| `loader`    | `boolean` | Indicates if the data is still loading. Displays a spinner when `true`.     |
| `show`      | `boolean` | Determines whether the modal is visible or not.                             |
| `player_stats` | `array` | Contains the statistics data for the players to be displayed.              |
| `game_data` | `object`  | Provides additional game-related data that can be used within the stats.    |
| `closeModal` | `function` | Function to close the modal, changing the visibility state.               |
| `isPPK`     | `boolean` | Flag indicating if the stats are related to a PPK (Pick, Play, Keep) game.  |

## Component Structure

```jsx
import React from "react";
import { Modal } from "react-bootstrap";
import LobbyResult from "../../LobbyList/LobbyResult";

function ViewStats({ loader, show, player_stats, game_data, closeModal, isPPK }) {
  return (
    <Modal show={show} onHide={closeModal} scrollable={true} className="custom-modal w-706" backdrop="static">
      <Modal.Header closeButton tag="h4">
        <Modal.Title className="text-capitalize">View Stats</Modal.Title>
      </Modal.Header>
      <Modal.Body className="events">
        {loader ? (
          <div class="spinner-grow transaction-spinner" role="status">
            <span class="sr-only">Loading...</span>
          </div>
        ) : (
          <div className="view-more-teams">
            <LobbyResult data={player_stats} gameData={game_data} isTournament={true} isPPK={isPPK} />
          </div>
        )}
      </Modal.Body>
    </Modal>
  );
}

export default ViewStats;
```

### Key Components:
- **Modal**: A Bootstrap component that creates a popup overlay for displaying content. It is used here to show player statistics.
- **LobbyResult**: A custom component that takes in player stats and game data to display results, tailored for tournaments or PPK scenarios.

## Usage

To use the `ViewStats` component, import it into the relevant parent component and supply the necessary props. The component will display a modal with a loading spinner until the data is ready, at which point it will render the `LobbyResult` component with the provided statistics.

Example usage:
```jsx
<ViewStats 
  loader={isLoading} 
  show={isModalVisible} 
  player_stats={stats} 
  game_data={gameInfo} 
  closeModal={handleClose} 
  isPPK={isPPKMode} 
/>
```

## Dependencies

- **React**: The JavaScript library for building user interfaces.
- **react-bootstrap**: A library providing Bootstrap components as React components.
- **LobbyResult**: A custom component used to format and display player statistics.

## Conclusion

The `ViewStats` component is integral for providing users a detailed view of player statistics within a tournament or game context. By utilizing a modal and incorporating a loader, it ensures a smooth UX even when data retrieval is pending. Its integration with Bootstrap's modal component ensures a responsive and visually appealing interface.

# TournamentDetailsTab.jsx Documentation

The `TournamentDetailsTab.jsx` component is designed to display the details of a specific tournament in a structured and user-friendly format. This documentation will guide you through the components, functionalities, and usage of this file.

## Overview

- **Purpose**: Display detailed information about a tournament, including its rules, game type, bracket style, teams, and more.
- **Libraries Used**: React, Reactstrap, Lodash, and external utilities for CSV conversion and HTML sanitization.

## Components and Functions

### Imports

- **React & Hooks**: 
  - `useEffect`, `useState` from React for managing component states and side effects.
- **Reactstrap**: 
  - Components like `Card`, `CardBody`, `Col`, and `Row` for layout structure.
- **Utilities**:
  - `csvConverterToPreviewFile`, `dateFormat`, `competitionStatus` from `helpers/util` for formatting data.
  - `sanitize` from `sanitize-html` for safe rendering of HTML content.
  - `isEmpty` from Lodash to check for empty objects or arrays.
- **Custom Components**:
  - `PrizeList` for displaying prize details.
  - `CsvView` for rendering CSV content.

### State Management

- **State Variables**:
  - `previewOldcsvData`: Stores the processed data from the CSV file associated with the tournament.

### Functions

- **`callUrl`**: Fetches the CSV file containing team rankings from the given URL and converts it into a format suitable for preview.
- **`useEffect`**: Automatically calls `callUrl` when the component mounts if a team rank file exists.

### JSX Structure

#### Card Structure

The main structure encapsulated within a `Card` and `CardBody` with several `Row` and `Col` components for layout purposes.

- **Tournament Basic Info**:
  - Tournament Name
  - Game Type and Game
  - Entry Fee
  - Bracket Style and Seeding

- **Conditional Display**:
  - If `seeding` is "Qualifiers", display the selected tournament.
  - If `game_type` is "PPK", display Lobby Size and Threshold.
  - If `seeding` is "Ranked Placement", show whether players can add ranks.

- **Team and Schedule Info**:
  - Minimum and Maximum Teams
  - Players Per Team
  - Enrolled Teams
  - Start Date and Time
  - Last Entry Time

- **Prize and Rules**:
  - Prize list using `PrizeList` component.
  - Game and Tournament rules rendered safely with `sanitize`.

- **Status Information**:
  - Active and Free status of the tournament.
  - Current tournament status derived from `competitionStatus`.

## Usage

This component is primarily used within a broader application managing tournaments. It expects a `details` prop containing all relevant information about a specific tournament.

### Example

```jsx
<TournamentDetailsTab details={tournamentDetails} />
```

Here, `tournamentDetails` would be an object containing fields such as `name`, `game_type`, `entry_fee`, `price`, and so on.

## Styling and Design

- Utilizes `Reactstrap` for a responsive and consistent layout.
- Ensures safe HTML rendering using `sanitize-html`.
- CSV data handling is performed using utility functions for seamless integration.

## Conclusion

The `TournamentDetailsTab` component provides a comprehensive view of tournament details, integrating various pieces of information and displaying them in an organized manner. With its use of state management and conditional rendering, it offers flexibility and robustness for displaying tournament data.

# Documentation for `StandingsTab.jsx`

## Overview
The `StandingsTab.jsx` file is a React component that renders the standings of a tournament. It displays the rankings of teams, the number of kills, and their scores in a tabular format. If the standings are not yet available, it informs the user that the standings are not available.

## Component Details

### Import Statements
- **React**: The core library for building the component.
- **Card, CardBody, Row**: Components from `reactstrap` used for layout and styling.
- **StandingsTable**: A custom component that displays the standings in a table format.

### Component: `StandingsTab`

#### Props
- **standingsDetails**: An array that contains details of the standings such as team rankings, number of kills, and scores.

#### Structure
- The component is wrapped in a `Card` from `reactstrap` for a structured layout.
- Inside the `CardBody`, a `Row` is used to vertically align the content.
- Depending on the content of `standingsDetails`, the component either displays the `StandingsTable` or a message indicating that standings are not available.

#### Conditional Rendering
- **Standings Available**: If `standingsDetails` contains data, it renders the `StandingsTable` component.
- **Standings Not Available**: If `standingsDetails` is empty, it renders a message saying "Standings not available yet".

### Usage
This component is used in a tournament management application to display the current standings based on the data passed to it. It is typically part of a larger interface where users can view various aspects of a tournament.

### Code Example
```jsx
import React from "react";
import { Card, CardBody, Row } from "reactstrap";
import StandingsTable from "../Table/StandingsTable";

const StandingsTab = ({ standingsDetails }) => {
  return (
    <Card className="mb-0">
      <CardBody>
        <Row>
          {standingsDetails?.length === 0 ? (
            <Card className="mb-0">
              <CardBody>
                <Row>Standings not available yet</Row>
              </CardBody>
            </Card>
          ) : (
            <StandingsTable standingsDetails={standingsDetails} />
          )}
        </Row>
      </CardBody>
    </Card>
  );
};

export default StandingsTab;
```

## Key Points
- **Responsive Design**: Utilizes `reactstrap` components to ensure the layout is responsive and consistent with other parts of the application.
- **Conditional Rendering**: Efficiently checks the availability of data before rendering the `StandingsTable`.
- **Reusability**: By using the `StandingsTable` component, the `StandingsTab` promotes reusability and separation of concerns.

This component is crucial for users who need to track the performance and rank of teams in an ongoing or completed tournament. It fits seamlessly into a larger dashboard or detailed view of tournament information.
# Documentation for `TeamsTab.jsx`

## Overview

The `TeamsTab.jsx` file is a React component responsible for displaying a list of teams participating in a tournament. It provides functionality to remove teams if necessary, and it includes details about each team member, such as their email, username, role in the team, invite status, and payment status.

## Components and Functionality

### Imports

- **React** and related hooks: Used for component creation and managing state.
- **reactstrap components**: `Button`, `Modal`: Used for UI elements and modals.
- **RemovePlayerModule**: A component for handling the removal of players from a team.
- **lodash's isEmpty**: Utility to check if objects or arrays are empty.
- **inviteStatus**: A utility to interpret invite status codes.

### State Management

- **`removeId`**: A state variable to store the ID of the team to be removed.
- **`openRemovalModal`**: A boolean state to control the visibility of the removal modal.

### Key Functions

1. **`handleRemove(id)`**: Sets the ID of the team to be removed and opens the modal.
2. **`handleClose()`**: Closes the removal modal.
3. **`handleRecallDetailApi()`**: Calls the API to refresh the tournament details after an action is taken.

### UI Structure

- **Table**: Displays the team details including:
  - Team Name
  - Email
  - Ryvals Username
  - Role (Creator or Member)
  - Invite Status
  - Payment Status
  - Action (Remove button for users with the necessary permissions)

### Conditional Rendering

- **No Teams Enrolled**: Displays a message when no teams are enrolled.
- **Action Button**: Rendered conditionally based on the `changePermission` prop, allowing team removal only if the user has the necessary permissions.

### Modals

- **Removal Modal**: Triggered when the "Remove" button is clicked, allowing the user to confirm the removal of a team.

## Usage

This component is typically used within a tournament management interface where administrators have the capability to manage team enrollments and ensure compliance with tournament rules.

## Code Example

```jsx
// Snippet demonstrating the rendering of a team row
<tbody>
  {isEmpty(details?.participants) ? (
    <tr>
      <td colspan="7">
        <h5 className="text-center my-5">No team enrolled yet</h5>
      </td>
    </tr>
  ) : (
    details?.participants.map((item, index) => {
      return item.players.sort(comparator).map((player, idx) => {
        return (
          <tr key={index}>
            {idx === 0 ? (
              <td rowspan={item.players.length}>
                {item?.name || "N/A"}
              </td>
            ) : null}
            <td>{player?.email || "N/A"}</td>
            <td>{player?.username || "N/A"}</td>
            <td>{player?.leader ? "Creator" : "Member"}</td>
            <td>{inviteStatus[player?.invite]}</td>
            <td>{player?.has_paid ? "Completed" : "Pending"}</td>
            {changePermission ? (
              idx === 0 ? (
                <td rowspan={item.players.length} className="teamName">
                  <Button
                    type="button"
                    color="primary"
                    className="ms-1"
                    onClick={() => handleRemove(player?.team)}
                    disabled={!details.is_team_removable}
                  >
                    Remove
                  </Button>
                </td>
              ) : null
            ) : null}
          </tr>
        );
      });
    })
  )}
</tbody>
```

## Conclusion

The `TeamsTab.jsx` component is an essential part of the tournament management system, providing administrators with an interface to view and manage teams participating in a tournament. Its integration with `RemovePlayerModule` allows for effective team management, ensuring that only valid teams remain in the competition.

# ScheduleTab Component Documentation

The `ScheduleTab.jsx` file is a React component that serves as a part of a larger application, likely dealing with tournament management or scheduling. This component leverages several other components and libraries to render a section of the application UI responsible for displaying tournament schedules.

## 📑 Component Overview

### Purpose

The `ScheduleTab` component is designed to render a card that contains a schedule view for a tournament. It uses the `AddTournamentSchedule` component to display detailed scheduling information and allows for additional functionalities like viewing mode and callbacks for further actions.

### Key Features

- **Integrates with `AddTournamentSchedule`**: This component is primarily a wrapper that includes the `AddTournamentSchedule` component, providing it with necessary props for functionality.
- **Uses Card Layout**: Utilizes a card layout from `reactstrap` for structured and styled presentation.
- **Supports Callbacks**: Allows for callbacks to be executed, likely intended for updating or fetching additional data when certain actions occur within the schedule view.

## 🧩 Component Structure

### Import Statements

- **React**: Core library for building the component.
- **reactstrap**: Used for UI components like `Card`, `CardBody`, and `Row` to structure and style the component.
- **AddTournamentSchedule**: A custom component that contains the logic and presentation for displaying and managing tournament schedules.

### Component Definition

```jsx
const ScheduleTab = ({ details, callBackToDetails }) => {
  return (
    <Card className="mb-0">
      <CardBody>
        <Row>
          <AddTournamentSchedule
            details={details}
            viewMode={true}
            stopApiCall={true}
            callBackToDetails={callBackToDetails}
          />
        </Row>
      </CardBody>
    </Card>
  );
};
```

### Props

- **details**: An object containing details about the tournament, passed down to `AddTournamentSchedule` for rendering the schedule.
- **callBackToDetails**: A function that acts as a callback. It is likely used to handle actions that require feedback or updates to the parent component.

### Component Usage

- **Card Layout**: The component employs a card layout, which is common in UI designs for encapsulating related content.
- **Integration with AddTournamentSchedule**: The main functionality relies on integrating the `AddTournamentSchedule` component, which is responsible for the core schedule management functions.

### Styling and Layout

- **CSS Classes**: Utilizes Bootstrap and potentially custom CSS classes (`"mb-0"`) for margin and layout control, ensuring a clean and aligned visual structure.

## ⚙️ Dependencies

- **React**: For building the component's structure and logic.
- **reactstrap**: Provides styled components for UI consistency.
- **AddTournamentSchedule**: A critical dependency that handles the logic for schedule display and interactions.

## Usage Example

The `ScheduleTab` component can be used in a parent component responsible for managing different sections of a tournament or game interface. It is suitable for situations where the user needs to view or interact with a tournament's schedule.

```jsx
<ScheduleTab
  details={tournamentDetails}
  callBackToDetails={handleScheduleUpdate}
/>
```

In this example, `tournamentDetails` would be an object containing information about the tournament, and `handleScheduleUpdate` is a function defined to manage updates to the schedule.

## Conclusion

The `ScheduleTab` component is a well-structured React component that serves a specific role within a tournament management system. Its integration with `AddTournamentSchedule` allows it to provide comprehensive scheduling functionalities while maintaining a clean and organized UI using `reactstrap`. The component's design facilitates easy integration and modularity within larger applications.

# MatchInfoTab.jsx Documentation

The `MatchInfoTab.jsx` file is a React component that displays match information within a tournament. It uses an accordion structure to organize and present data about matches in a tournament round. This component relies on several sub-components and libraries to provide a seamless user experience.

## Table of Contents

1. [Component Overview](#component-overview)
2. [Props](#props)
3. [Dependencies](#dependencies)
4. [Rendering Logic](#rendering-logic)
5. [Usage Example](#usage-example)
6. [Conclusion](#conclusion)

---

## Component Overview

The `MatchInfoTab` component is designed to display match-related data for a specific tournament round. It uses the `react-accessible-accordion` library to create an expandable and collapsible interface, making it easy for users to view detailed information about each match.

**Key Features:**
- Displays match information using an accordion.
- Handles cases where match info is unavailable.
- Integrates with other components to provide match data.

## Props

| Prop Name          | Type   | Description                                      |
|--------------------|--------|--------------------------------------------------|
| `matchInfo`        | Array  | An array of match information objects.           |
| `gameType`         | String | The type of game being played in the tournament. |
| `teamsInMatchesInfo` | Array | Additional information about teams in matches.   |

## Dependencies

- **react-accessible-accordion**: Used to create accessible and responsive accordion components.
- **reactstrap**: Provides styled components for layout and design.
- **MatchInfoTable**: A custom component used to display detailed match information.

## Rendering Logic

1. **Accordion Setup**: The component first checks if there is any `matchInfo` data available. If not, it displays a message indicating that match info is not available.
   
2. **Mapping Matches**: If `matchInfo` is present, it maps over the data to generate accordion items for each match round.

3. **AccordionItem**: Each item includes an accordion button displaying the round name and type. Within the panel, the `MatchInfoTable` component is used to display detailed match information if available.

4. **Condition Handling**: The component gracefully handles cases where no matches are found by displaying a "No data found" message.

### Code Snippet

```jsx
<Accordion className="add-tournament-schedule" allowZeroExpanded>
  {matchInfo && matchInfo.map((item, id) => (
    <AccordionItem key={id}>
      <AccordionItemHeading className="text-capitalize">
        <AccordionItemButton>
          {item.round}
          {item.tour_bracket_style === 2 && item.round_type != null ? `[${item.round_type}]` : null}
        </AccordionItemButton>
      </AccordionItemHeading>
      <AccordionItemPanel accordionId="1">
        {item?.matches?.length === 0 ? (
          <span>No data found</span>
        ) : (
          <MatchInfoTable subMatches={item} gameType={gameType} teamsInMatchesInfo={teamsInMatchesInfo} />
        )}
      </AccordionItemPanel>
    </AccordionItem>
  ))}
</Accordion>
```

## Usage Example

To use the `MatchInfoTab` component, you would typically import it and pass the necessary props like `matchInfo`, `gameType`, and `teamsInMatchesInfo` from a parent component managing tournament details.

```jsx
import React from 'react';
import MatchInfoTab from './MatchInfoTab';

const TournamentDetails = ({ tournamentData }) => {
  return (
    <MatchInfoTab 
      matchInfo={tournamentData.matchInfo} 
      gameType={tournamentData.gameType} 
      teamsInMatchesInfo={tournamentData.teamsInfo} 
    />
  );
};

export default TournamentDetails;
```

## Conclusion

The `MatchInfoTab.jsx` component is a versatile and user-friendly way to display match details in a tournament setting. By utilizing a combination of accordion components and conditional rendering, it provides a clear and organized view of match data, enhancing the user experience for tournament management applications.

--- 

This documentation provides a comprehensive overview of the `MatchInfoTab.jsx` component, detailing its purpose, usage, and integration within a tournament management system.

# Documentation for `ViewMoreTeamTable.jsx`

## Overview

The `ViewMoreTeamTable.jsx` file contains a React component that renders a table displaying a list of teams. This component is designed to be used within a modal or a larger component to show additional teams in a tournament setting. It provides a simple table layout to list team names and can be customized to show either general or specific round table information based on the `roundTable` prop.

## Component Structure

### `ViewMoreTeamTable`

This is the main and only component exported from the file. It is responsible for rendering the table of teams.

#### Props

- **`teamList`**: An array of objects representing the teams to be displayed in the table. Each object should contain the necessary information about a team, such as `team_id`, `id`, `team`, and `name`.
  
- **`roundTable`**: A boolean value that determines how the team names are displayed. If `true`, the component uses the `team` property to display the team name; otherwise, it uses the `name` property.

#### Render Logic

- The component uses a series of nested `<div>` elements and a standard HTML `<table>` element to render the team data.
  
- The table contains a single column with the heading "Team Name" and iterates over the `teamList` array to populate the rows.

- The `id` attribute for each row is set based on the index of the team in the list, while the key is determined using either `team_id` or `id` based on the `roundTable` prop.

```jsx
<div className="table-rep-plugin tournamentRound">
  <div className="table-responsive mb-0" data-pattern="priority-columns">
    <div className="table-responsrowspanive seize-wallet-table">
      <table className="table table-striped table-bordered manage-complaints-table lobbies-table add-schedule ppk-table">
        <thead>
          <tr>
            <th scope="col" rowSpan="2"> Team Name </th>
          </tr>
        </thead>
        <tbody>
          {teamList && teamList.map((item, index) => {
            return (
              <tr key={roundTable ? item.team_id : item.id} id={index}>
                <td className="text-capitalize">
                  {roundTable ? item.team : item.name}
                </td>
              </tr>
            );
          })}
        </tbody>
      </table>
    </div>
  </div>
</div>
```

## Usage Example

```jsx
import React from 'react';
import ViewMoreTeamTable from './ViewMoreTeamTable';

const teams = [
  { id: 1, name: 'Team Alpha' },
  { id: 2, name: 'Team Bravo' },
  { id: 3, name: 'Team Charlie' },
];

<ViewMoreTeamTable teamList={teams} roundTable={false} />;
```

## Styling and Responsiveness

- The component uses several CSS classes like `table-rep-plugin`, `tournamentRound`, and `ppk-table` to apply specific styles. These classes should be defined in an external CSS file to ensure the component renders correctly.

- The component is designed to be responsive, utilizing Bootstrap classes such as `table-responsive` to adjust the table layout for different screen sizes.

## Conclusion

The `ViewMoreTeamTable` component is a simple yet effective way to display a list of teams in a structured table format. Its design is minimalistic, focusing on listing team names with the flexibility to adapt based on the `roundTable` prop. This component is ideal for use within modals or sections of an application where additional team details need to be displayed.

# StandingsTable.jsx Documentation

The `StandingsTable.jsx` file is a React component designed to display the standings of teams in a tournament. It presents the data in a tabular format, showing each team's rank, name, number of kills, and score.

## Table of Contents

- [Component Overview](#component-overview)
- [Props](#props)
- [Structure](#structure)
- [Rendering Logic](#rendering-logic)
- [Usage Example](#usage-example)
- [Dependencies](#dependencies)

## Component Overview

The `StandingsTable` component provides a responsive table that lists the standings details of teams participating in a tournament. It is structured using the `reactstrap` and standard HTML table elements to ensure responsiveness and accessibility.

## Props

The component accepts the following props:

| Prop Name         | Type   | Description                            |
|-------------------|--------|----------------------------------------|
| `standingsDetails`| Array  | An array of objects containing details about the standings of each team, including their position, team name, number of kills, and points. |

## Structure

The component's structure is organized as follows:

```jsx
<div className="table-rep-plugin tournamentRound">
  <div className="table-responsive mb-0" data-pattern="priority-columns">
    <div className="table-responsrowspanive seize-wallet-table">
      <table className="table table-striped table-bordered manage-complaints-table lobbies-table add-schedule tounamnet-standing-tab">
        <thead>
          <tr>
            <th>Rank</th>
            <th>Team Name</th>
            <th>Number of Kills</th>
            <th>Score</th>
          </tr>
        </thead>
        <tbody>
          {standingsDetails && standingsDetails.map((standings, idx) => {
            return (
              <tr key={idx}>
                <td>{standings.position}</td>
                <td>{standings.team_name}</td>
                <td>{standings.kills}</td>
                <td>{standings.points}</td>
              </tr>
            );
          })}
        </tbody>
      </table>
    </div>
  </div>
</div>
```

## Rendering Logic

- The component renders a table with a header containing columns: "Rank", "Team Name", "Number of Kills", and "Score".
- It maps over the `standingsDetails` array to generate a row for each team, displaying their rank, team name, number of kills, and score.

## Usage Example

Here's how you might use the `StandingsTable` component in a parent component:

```jsx
import React from 'react';
import StandingsTable from './StandingsTable';

const tournamentStandings = [
  { position: 1, team_name: 'Team Alpha', kills: 15, points: 100 },
  { position: 2, team_name: 'Team Beta', kills: 12, points: 90 },
  // More standings data...
];

function TournamentDetails() {
  return (
    <div>
      <h2>Tournament Standings</h2>
      <StandingsTable standingsDetails={tournamentStandings} />
    </div>
  );
}

export default TournamentDetails;
```

## Dependencies

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: A library of React components that use Bootstrap for styling.

By utilizing these dependencies, the component ensures a consistent look and feel while maintaining responsiveness across different devices.

This documentation should provide a comprehensive understanding of the `StandingsTable` component, its purpose, and how it can be integrated into larger applications.

# Documentation: `PPKTeamTable.jsx`

The `PPKTeamTable.jsx` file is a React component that displays a table of teams participating in a PPK (Player vs Player Knockout) tournament round. The table highlights the winning teams using a tick icon.

## Table of Contents
- [Component Overview](#component-overview)
- [Props](#props)
- [Structure](#structure)
- [Rendering Logic](#rendering-logic)
- [Styling](#styling)
- [Usage Example](#usage-example)

## Component Overview

The `PPKTeamTable` component is designed to render a list of teams within a structured table format. It provides a simple visual indication of which teams are winners by appending a tick icon next to their names.

## Props

The component expects the following props:

| Prop Name | Type   | Description                               |
|-----------|--------|-------------------------------------------|
| `teams`   | Array  | An array of team objects, each containing details about the team, such as its name and whether it's a winner. |

## Structure

The component structure is as follows:

- A main container `div` with classes for styling and layout purposes.
- A responsive table that adapts to different screen sizes, ensuring the component is user-friendly on mobile devices.
- Table headers and body are organized within a standard HTML `<table>` structure.

## Rendering Logic

1. **Table Headers**: The table consists of a single header column labeled "Team Name".
2. **Table Body**:
   - Iterates over the `teams` array.
   - Each team is displayed in a table row with the team's name.
   - If a team is a winner (`is_winner` is `true`), a tick icon is displayed next to the team's name.

Here is a snippet that showcases the rendering logic for team rows:

```jsx
<tbody>
  {teams && teams.map((item, index) => {
    return (
      <tr key={index}>
        <td className={item.is_winner ? 'text-capitalize winner' : 'text-capitalize'}>
          {item.name} 
          {item.is_winner ? <img src={tick} alt="tick" className="win"/> : null}
        </td>
      </tr>
    );
  })}
</tbody>
```

## Styling

- **Table Styling**: The table uses the class `ppk-table` along with other utility classes for consistent styling and layout.
- **Responsive Design**: Wrapped within a `div` that uses classes for ensuring responsiveness (`table-rep-plugin`, `table-responsrowspanive`).
- **Winner Highlight**: The class `winner` is applied to winning teams, and a tick icon is displayed using an image (`tick`) imported from assets.

## Usage Example

To use the `PPKTeamTable` component, import it and provide the `teams` prop with the appropriate data structure:

```jsx
import PPKTeamTable from './PPKTeamTable';

// Sample usage
const teamsData = [
  { name: "Team A", is_winner: true },
  { name: "Team B", is_winner: false },
  // ...other teams
];

<PPKTeamTable teams={teamsData} />
```

This component is especially useful in scenarios where tournament results need to be displayed, providing a clear and concise view of participating teams and their statuses.

# MatchInfoTable.jsx Documentation

## Overview

The `MatchInfoTable.jsx` component is a part of a React application that provides a detailed view of matches within a tournament context. It displays information about each match within a table, allowing users to view more detailed information or statistics about specific matches. It supports both traditional match styles and PPK (Points Per Kill) styles.

## Component Structure

### Imports

- **React and Hooks**: The component uses React and several hooks (`useState`) for managing state within the component.
- **Utilities**: 
  - `dateTimeFormatterForTournamentMatchinfo`: A utility function for formatting date and time.
  - `getLobbyDetail`: A service function to fetch detailed lobby information.
- **Components**:
  - `ViewMoreTeamsModal`: A modal component for displaying more team details.
  - `ViewStats`: A modal component for displaying statistics of a match.

### Props

- `subMatches`: An object containing details about the sub-matches.
- `gameType`: A string indicating the type of game (e.g., "PPK").
- `teamsInMatchesInfo`: Information about teams participating in the matches.

### State Variables

- **`showMore`**: Manages the visibility of the `ViewMoreTeamsModal`.
- **`showMoreTeam`**: Stores data for teams to be shown in the `ViewMoreTeamsModal`.
- **`showStats`**: Manages the visibility of the `ViewStats` modal.
- **`loader`**: Indicates loading status for fetching tournament data.
- **`stats`**: Holds the statistics data fetched for a specific match.
- **`gameData`**: Contains game-related data fetched for a specific match.

### Functions

- **`handleShowMore`**: Opens the `ViewMoreTeamsModal` with the provided team data.
- **`handleClose`**: Closes the `ViewMoreTeamsModal`.
- **`handleShowStats`**: Opens the `ViewStats` modal and fetches statistics for a specific lobby.
- **`getTournament`**: Fetches detailed information for a specific lobby using the `getLobbyDetail` service.
- **`handleCloseStats`**: Closes the `ViewStats` modal.

### Rendering

- **Table Structure**: Renders a table to list match details such as match number, start date and time, competing teams, and available actions (like viewing stats).
- **Conditional Rendering**:
  - Displays "NA" (Not Available) for match numbers or teams when information is not available.
  - Provides "View more" and "View Stats" buttons to access additional information.
- **Modals**:
  - `ViewMoreTeamsModal`: Displays more team information when a match involves more than a few teams.
  - `ViewStats`: Displays statistical data for matches if available.

## Usage

This component is used within a tournament management interface to provide an overview and detailed insights into each match's status and participants. It supports both traditional and PPK gaming styles, adjusting its display logic accordingly.

## Key Considerations

- **Error Handling**: The component does not explicitly handle errors during data fetching from the server. It may be enhanced by integrating try-catch blocks or error boundaries.
- **Performance**: Consider optimizing data fetching and state updates to enhance performance, especially when handling large datasets or frequent updates.
- **Accessibility**: Ensure the component adheres to accessibility standards such as proper labeling and keyboard navigation support.

## Example JSX

```jsx
<MatchInfoTable
  subMatches={subMatchesData}
  gameType="PPK"
  teamsInMatchesInfo={teamMatchInfo}
/>
```

This component will render a table with match details, allowing users to interact and view further details or statistics about each match.

# Documentation for `PlayersRankInfoTable.jsx` 📄

## Overview

The `PlayersRankInfoTable.jsx` component is a React functional component designed to display a table with information about players and their respective ranks. This component is especially useful in tournament applications where player ranking is a crucial aspect. It presents the data in a structured and easily readable format.

## Component Structure

The component is structured using standard HTML table elements wrapped within React components to ensure scalability and maintainability. The table is styled using Bootstrap classes to ensure responsiveness and a clean UI.

## Code Breakdown

```jsx
import React from "react";

function PlayersRankInfoTable({ players }) {
  return (
    <div className="table-rep-plugin tournamentRound">
      <div className="table-responsive mb-0" data-pattern="priority-columns">
        <div className="table-responsrowspanive seize-wallet-table">
          <table className="table table-striped table-bordered manage-complaints-table lobbies-table add-schedule">
            <thead>
              <tr>
                <th scope="col" rowSpan="2"> Username </th>
                <th scope="col" rowSpan="2"> Player Rank </th>
              </tr>
            </thead>
            <tbody>
              {players && players.map((item, index) => {
                return (
                  <tr key={index}>
                    <td className="text-capitalize">{item.username}</td>
                    <td className="text-capitalize"> {item.player_rank || "NA"} </td>
                  </tr>
                );
              })}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  );
}

export default PlayersRankInfoTable;
```

### Key Features

- **Responsive Design**: The component uses Bootstrap classes such as `table-responsive` and `table-striped` to ensure that the table is responsive and maintains a consistent style across different device sizes.

- **Dynamic Data Rendering**: It dynamically maps over the `players` prop, which is expected to be an array of player objects, rendering each player's username and rank.

- **Fallback for Missing Data**: If a player's rank is not available, it displays "NA" as a fallback, ensuring that the UI remains stable even with incomplete data.

### Props

- **players**: An array of objects, where each object represents a player with at least the properties `username` and `player_rank`. Example:
  ```json
  [
    {
      "username": "Player1",
      "player_rank": "1"
    },
    {
      "username": "Player2",
      "player_rank": null
    }
  ]
  ```

### Usage Example

To use the `PlayersRankInfoTable` component, you need to pass the `players` data as a prop:

```jsx
import PlayersRankInfoTable from "./PlayersRankInfoTable";

const playersData = [
  { username: "Player1", player_rank: 1 },
  { username: "Player2", player_rank: 2 },
  { username: "Player3", player_rank: null }
];

<PlayersRankInfoTable players={playersData} />;
```

This will render a table with the usernames and ranks of the players provided in the `playersData` array.

## Conclusion

The `PlayersRankInfoTable` component is a simple yet effective way to display player ranking data in a tabular format. Its responsive design and ability to handle missing data gracefully make it a reliable component for any application dealing with tournament or player ranking information.