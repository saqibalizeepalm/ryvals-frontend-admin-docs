# 📄 AddDemoPage.js Documentation

Welcome to the documentation for the **AddDemoPage.js** component. This file is a React component designed to provide functionality for adding a demo page in a web application. Let's explore the component in detail:

---

## 📚 Table of Contents

1. [Overview](#overview)
2. [Component Breakdown](#component-breakdown)
3. [Dependencies](#dependencies)
4. [Use State and Effects](#use-state-and-effects)
5. [Functions](#functions)
6. [Rendering](#rendering)
7. [Conclusion](#conclusion)

---

## 🌟 Overview

The **AddDemoPage.js** component is responsible for rendering a form that allows users to add a demo page with various attributes such as game name, title, content, YouTube link, and more. It integrates several UI elements such as select dropdowns, rich text editors, and switches to enhance user interaction.

---

## 🏗️ Component Breakdown

The component is structured as follows:

- **Imports**: Importing necessary libraries and components.
- **State and Effects**: Managing component state and side effects using hooks.
- **Functions**: Defining functions to handle form submissions and data fetching.
- **Rendering**: Rendering the UI elements and handling user input.

---

## 📦 Dependencies

The component utilizes various libraries and components:

- **React**: Core library for building UI components.
- **Reactstrap**: Bootstrap components for React.
- **Availity-reactstrap-validation**: Validation for form inputs.
- **React-router-dom**: Navigation within the app.
- **React-toastify**: Notifications and alerts.
- **React-quill**: Rich text editor.
- **React-switch**: Toggle switch component.
- **React-select**: Select dropdown component.
- **Multiselect-react-dropdown**: Multiselect dropdown.
- **Custom Components**: Breadcrumbs, Loader, GoBack, OnSymbol, OffSymbol.

---

## 🔄 Use State and Effects

The component uses various pieces of state to manage input values and UI behavior:

- **isLoading**: To show/hide the loader.
- **optionGroup**: To store game options for the select dropdown.
- **selectedGame**: To store the selected game from the dropdown.
- **contentText**: To store the rich text content.
- **active**: To toggle active status.
- **pinDemo**: To toggle the pin status.
- **options**: To store options for the "Replace With" feature.

**Effects** are used to fetch game and pinned list data when the component mounts:

```javascript
useEffect(() => {
  gameList();
  pinnedList();
}, []);
```

---

## 🛠️ Functions

### gameList

Fetches the list of games and updates the state for the select options.

### pinnedList

Fetches the pinned list and sets options for the "Replace With" multiselect.

### handleSelectGroup

Handles game selection from the dropdown.

### setContent

Updates the content state with the rich text editor's content.

### handleValidSubmit

Handles form submission, validates inputs, and sends data to the server.

### selectPinned

Handles selection of a pinned demo for replacement.

### handleClickShowRaw and handleChangeRaw

Manages the raw HTML view of the content editor.

---

## 🎨 Rendering

The component renders a form with the following elements:

1. **Select Dropdown**: For selecting a game.
2. **Text Fields**: For title and YouTube link.
3. **Rich Text Editor**: For adding content.
4. **Switches**: For toggling pin status and active status.
5. **Multiselect Dropdown**: For selecting a demo to replace.
6. **Button**: Submit button to add the demo.

Here's a snippet of how the form is structured:

```jsx
<AvForm onValidSubmit={(e, v) => { handleValidSubmit(e, v); }}>
  <div className="mb-3">
    <label>Game Name*</label>
    <Select onChange={handleSelectGroup} options={optionGroup} />
    {selectGameError && <label className="errorMsgGames">{selectGameError}</label>}
  </div>
  <div className="mb-3">
    <AvField name="title" label="Add Title*" placeholder="Enter here" type="text" validate={...} />
  </div>
  <div className={show_raw ? "mb-3 showRaw" : "mb-3"}>
    <label>Add Content*</label>
    <EditorToolbar toolbarId="toolbar-1" onClickRaw={handleClickShowRaw} />
    <ReactQuill value={contentText || ""} onChange={setContent} placeholder="Enter content here" />
  </div>
  <FormGroup className="mt-4">
    <Button type="submit" color="primary" className="ms-1" disabled={isLoading}>Submit</Button>
  </FormGroup>
</AvForm>
```

---

## 🏁 Conclusion

The **AddDemoPage.js** component is a comprehensive form for adding demo pages to a web application. It combines multiple UI elements and state management to ensure a smooth user experience. By utilizing libraries like React-Select and React-Quill, it provides enhanced functionality and interactivity.

For further customization or functionality expansion, developers can delve deeper into the component's state management and function logic. Happy coding! 🚀

---

# Documentation for `DemoPageList.js`

Welcome to the documentation for the **DemoPageList.js** file. This documentation will help you understand the purpose and functionalities of this file, as well as how it fits into the larger application.

## Index

1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Key Functions and Features](#key-functions-and-features)
4. [Dependencies](#dependencies)
5. [UI Components and Interactions](#ui-components-and-interactions)
6. [State Management](#state-management)
7. [API Integration](#api-integration)
8. [Permissions Handling](#permissions-handling)

---

## Overview

The **DemoPageList** component is responsible for rendering and managing a list of demo pages within the application. This includes functionalities such as viewing, filtering, pinning, deleting, and updating demos.

![Demo Page](https://via.placeholder.com/800x150.png?text=Demo+Page+List+UI)

## Component Structure

This component is structured as a React functional component. It makes use of hooks such as `useState` and `useEffect` for managing component state and lifecycle events.

```javascript
const DemoPageList = (props) => {
    // Component code goes here
};
```

### Key Props

- **`props.permission`**: An array containing user permissions which dictate available actions.

## Key Functions and Features

### `useEffect`

- **Purpose**: Fetches demo listings and applies user permissions when the component mounts or when dependencies change.
- **Dependencies**: `searchByGame`, `pageNumber`.

### `getDemoListing`

- **Purpose**: Fetches the list of demos and games from the server. Also fetches pinned demos to manage maximum allowed pins.
- **Calls**: `getDemoList`, `getGameList`, `getPinnedList`.

### `handlePinChange`

- **Purpose**: Toggles the pinned status of a demo. If the maximum pin count is reached, it shows a modal to replace an existing pin.

### `handleStatusChange`

- **Purpose**: Changes the status of the demo between active and inactive.

### `deleteSelectedDemo`

- **Purpose**: Deletes a selected demo from the list.

### `handleUploadBackgroundFile`

- **Purpose**: Validates and uploads a background image for a game demo.

## Dependencies

The component uses several libraries and custom components:

- **Reactstrap**: For UI components like `Card`, `Modal`, `Table`.
- **react-super-responsive-table**: For responsive table design.
- **Toasts and Alerts**: `react-toastify` and `react-bootstrap-sweetalert` for notifications.
- **Switch**: `react-switch` for toggle switches.
- **Uploader**: `react-s3` for file uploads.

## UI Components and Interactions

### Tables

- **Game Background Image Table**: Displays games and allows image uploads.
- **Game Demos Table**: Lists all demos with actions for pinning, status toggle, edit, and delete.

### Modals and Alerts

- **Replace Modal**: Prompt for replacing a pinned demo when the max pin count is reached.
- **Delete Alert**: Confirmation prompt before deleting a demo.

### Dropdowns and Inputs

- **Game Filter Dropdown**: Filters demos by game.
- **File Input**: For uploading background images.

## State Management

The component manages a variety of state variables:

- **`demo`**: Array of demo objects.
- **`games`**: List of game objects.
- **`isLoading`**: Loading state for data fetches.
- **`pinDemo`**: Boolean state for demo pinning.
- **`selectedDemo`**: ID of the currently selected demo for deletion.

## API Integration

The component communicates with APIs for various actions:

- **Fetching Data**: `getDemoList`, `getGameList`, `getPinnedList`.
- **Updating Status**: `updateDemoPagePinStatus`.
- **Deleting Demos**: `deleteSelectedDemoApi`.

## Permissions Handling

The component dynamically adjusts the UI based on the user's permissions:

- **Change, Delete, Add Permissions**: Dictate what actions are displayed.
- **FilterPermission**: Utility function to filter and apply permissions.

---

This concludes the documentation for the **DemoPageList.js** file. By understanding the structure and functionality outlined above, developers can effectively work with and modify this component as needed within the application.

# Documentation for `EditDemoPage.js`

### Overview

The `EditDemoPage.js` file is a React component designed to facilitate the editing of an existing demo page in a game demo management application. This component provides a user interface that allows users to edit various attributes of a demo page, such as the game name, title, content, YouTube link, pin status, and more. The component uses various libraries and custom components to achieve its functionality.

### Table of Contents

1. [Imports](#imports)
2. [Component Structure](#component-structure)
3. [State Variables](#state-variables)
4. [Effect Hooks](#effect-hooks)
5. [Functions](#functions)
6. [Rendering](#rendering)
7. [Conclusion](#conclusion)

---

### Imports

The component makes use of several libraries and custom components:

- **React and Hooks**: For creating the component and managing state and side effects.
- **Reactstrap**: For responsive UI components like Row, Col, Card, etc.
- **Availity Reactstrap Validation**: For form validation.
- **React Router**: For navigation support.
- **React Quill**: For rich text editing.
- **React Switch**: For toggle switches.
- **React Select**: For dropdowns.
- **React Toastify**: For notifications.
- **Multiselect Dropdown**: For selecting multiple options.
- **Custom Components**: Such as `Breadcrumbs`, `Loader`, `GoBack`, etc.
- **API Services**: Functions to fetch and update data.

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, FormGroup, Button } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { withRouter } from "react-router-dom";
import Loader from "../../components/Common/Loader";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import ReactQuill from "react-quill";
import 'react-quill/dist/quill.snow.css';
import Switch from "react-switch";
import Select from "react-select";
import { getGameList } from "../../services/game_api_helper";
import { getEditDemoDataById, getPinnedList, editDemoPage } from "../../services/demo_api_helper";
import { Multiselect } from "multiselect-react-dropdown";
import EditorToolbar, { formats } from "../CMS/EditorToolbar";
import { ERROR_MESSAGES, SUCCESS_MESSAGES } from "../../helpers/StringConstant";
import { OffSymbol } from "../../components/Switch/OffSymbol";
import { OnSymbol } from "../../components/Switch/OnSymbol";
import { GoBack } from "../../components/GoBack";
```

---

### Component Structure

The `EditDemoPage` component is structured as a functional component that utilizes hooks for state management and side effects. It is wrapped with `withRouter` to access routing props.

```javascript
const EditDemoPage = (props) => {
  // Component logic here
};

export default withRouter(EditDemoPage);
```

---

### State Variables

The component uses several state variables to manage the data and UI interactions:

- **Loading States**: `isLoading` to show a loading spinner during data fetch.
- **Form Fields**: `optionGroup`, `selectedGame`, `contentText`, `activeEdit`, etc.
- **Errors**: `contentFieldErrorEdit`, `selectGameError`, `errMsg`.
- **Options**: `options`, `replaceWith`.
- **Data**: `data`, `game`.

```javascript
const [isLoading, setLoading] = useState(false);
const [optionGroup, setOptionGroup] = useState(null);
const [selectedGame, setSelectedGame] = useState(null);
const [contentText, setContents] = useState(null);
const [contentFieldErrorEdit, setContentFieldErrorEdit] = useState("");
const [selectGameError, setGameError] = useState("");
const [activeEdit, setActiveEdit] = useState(false);
const [errMsg, setErrorMessage] = useState("");
const [options, setOptions] = useState([]);
const [replaceWith, setReplaceWith] = useState(null);
const [pinDemoEdit, setPinDemoEdit] = useState(false);
const [data, setData] = useState({});
const [game, setGame] = useState({});
```

---

### Effect Hooks

`useEffect` hooks are utilized for initial data fetching and component updates:

- Fetch game list and pinned list when the component mounts.
- Fetch demo data to populate the form fields.

```javascript
useEffect(() => {
  gameList();
  pinnedList();
  getEditDemoData();
}, []);
```

---

### Functions

The component defines several functions for handling various interactions:

- **`gameList`**: Fetches the list of games.
- **`pinnedList`**: Fetches the list of pinned demos.
- **`getEditDemoData`**: Fetches the data of the demo page to be edited.
- **`handleSelectGroup`**: Handles the game selection.
- **`setContent`**: Updates the content state from the editor.
- **`handleValidSubmitEdit`**: Validates data and submits the form.

```javascript
const gameList = () => {
  getGameList().then((res) => {
    // handle response
  });
};

const handleValidSubmitEdit = async (event, values) => {
  event.preventDefault();
  // Validation and form submission logic here
};
```

---

### Rendering

The component renders a form with various input fields and controls to edit the demo page:

- **Breadcrumbs**: For navigation path display.
- **Form Fields**: Game name, title, content using `AvForm` and `AvField`.
- **Rich Text Editor**: Using `ReactQuill`.
- **Switches**: For toggleable options like pin status.
- **Multiselect**: For replacement options.

```jsx
return (
  <React.Fragment>
    <Loader showLoader={isLoading} />
    <div className="page-content">
      <Breadcrumbs breadcrumbItem={"Edit Demo page"} />
      <Row>
        <Col lg={12}>
          <Card>
            <CardBody>
              <GoBack backUrl="/gameDemo" />
              <Row className="add-staff-member">
                <Col className="col-lg-8 col-md-8 col-sm-8 col-12">
                  <AvForm onValidSubmit={(e, v) => { handleValidSubmitEdit(e, v); }}>
                    {/* Form elements here */}
                  </AvForm>
                </Col>
              </Row>
            </CardBody>
          </Card>
        </Col>
      </Row>
    </div>
  </React.Fragment>
);
```

---

### Conclusion

The `EditDemoPage.js` component is a well-structured React component that provides an interface for editing demo pages within a game demo application. Through the use of various libraries and custom components, it offers a rich set of features and a user-friendly interface, allowing users to update demo page details efficiently.