# 📄 EditLocation.js Documentation

## Overview

The `EditLocation.js` file is a React component designed to handle the editing of locations, specifically focusing on countries and their associated states. This component provides a form interface where users can update the states associated with a country, delete states, and navigate back to a list of locations.

## Table of Contents

1. [Imports](#imports)
2. [Component State](#component-state)
3. [Lifecycle Methods](#lifecycle-methods)
4. [Event Handlers](#event-handlers)
5. [Helper Functions](#helper-functions)
6. [Render Method](#render-method)
7. [Conclusion](#conclusion)

## Imports

The file begins with a series of imports that bring in necessary modules and components:

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, FormGroup, Button } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Link } from "react-router-dom";
import Loader from "../../components/Common/Loader";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import { editBanCountry, deleteCountryState } from "../../services/complaint_user_api_helper";
import { getStates } from "../../services/config_api_helper";
import { Multiselect } from "multiselect-react-dropdown";
import whiteCrossIcon from "../../assets/images/white-cross-icon.svg";
import { SUCCESS_MESSAGES } from "../../helpers/StringConstant";
```

### Key Imports:

- **React and Hooks**: For creating and managing the component's lifecycle and state.
- **Reactstrap Components**: For UI layout and form handling.
- **Availity Form Components**: For form validation.
- **Router and Navigation**: For navigation between pages.
- **Loader and Toast Notification**: For user feedback on form submission and loading states.
- **API Helpers**: For interacting with backend services to update or delete location data.
- **Multiselect Dropdown**: For selecting multiple states in the form.

## Component State

The component maintains several pieces of state:

- **`isLoading`**: Tracks whether a loading operation is in progress.
- **`state`**: Stores the list of states associated with the selected country.
- **`isDisabled`**: Determines whether the submit button should be disabled.
- **`addMoreState`**: Keeps track of states added or removed from the selection.

```javascript
const [isLoading, setIsloading] = useState(false);
const [state, setState] = useState([]);
const [isDisabled, setIsDisabled] = useState(true);
const [addMoreState, setAddMoreState] = useState([]);
```

## Lifecycle Methods

### useEffect

The `useEffect` hook is used to fetch the initial list of states when the component mounts:

```javascript
useEffect(() => {
  getStateList(data.country_id);
}, []);
```

## Event Handlers

### handleValidSubmit

Handles form submissions. It checks if any states are selected and makes the appropriate API call to update or delete states:

```javascript
const handleValidSubmit = async (event, values) => {
  event.preventDefault();
  if (addMoreState.length === 0) {
    showLoader(true);
    await deleteCountryState(data.country_id).then((res) => {
      showLoader(false);
      toast.success(SUCCESS_MESSAGES.deletedSuccess, toastrOptions);
      goToListing();
    }, (err) => {
      showLoader(false);
    });
  } else {
    let model = {
      country_id: data.country_id,
      location_id: addMoreState,
      location_type: "state",
    };
    showLoader(true);
    await editBanCountry(model, data.country_id).then((_) => {
      showLoader(false);
      toast.success(SUCCESS_MESSAGES.updateSuccess, toastrOptions);
      goToListing();
    }, (err) => {
      showLoader(false);
    });
  }
};
```

### checkMultiSelectState and onRemoveState

These functions manage the state selection for the multiselect dropdown:

```javascript
const checkMultiSelectState = (selectedList, selectedItem) => {
  setAddMoreState(Array.isArray(selectedList) ? selectedList.map((x) => x.id) : []);
  setIsDisabled(false);
};

const onRemoveState = (selectedList, removedItem) => {
  setAddMoreState(Array.isArray(selectedList) ? selectedList.map((x) => x.id) : []);
  setIsDisabled(false);
};
```

## Helper Functions

### getStateList

Fetches the list of states for a given country:

```javascript
const getStateList = async (id) => {
  await getStates(id).then((res) => {
    setState(res);
  });
};
```

### getMultiStateNames

Maps state IDs to names for pre-selection in the multiselect dropdown:

```javascript
const getMultiStateNames = (options, values) => {
  const finall = [];
  options.map((opt) => {
    for (let i = 0; i < values.length; i++) {
      if (values[i].state_id === opt.id) {
        finall.push({ name: opt.name, id: opt.id });
      }
    }
  });
  return finall;
};
```

## Render Method

The component renders a form that allows users to edit the states associated with a country. It includes a breadcrumb for navigation, a loader for visual feedback during operations, and a form with validation to ensure user inputs are correct.

```javascript
return (
  <React.Fragment>
    <Loader showLoader={isLoading} />
    <div className="page-content">
      <Breadcrumbs breadcrumbItem={" Edit location"} />
      <Row>
        <Col lg={12}>
          <Card>
            <CardBody>
              <Row className="mb-4">
                <Col>
                  <p>
                    <Link to="/locationLists">
                      <i className="mdi mdi-arrow-left"></i> back
                    </Link>
                  </p>
                </Col>
              </Row>
              <Row>
                <Col className="col-8">
                  <AvForm onValidSubmit={(e, v) => { handleValidSubmit(e, v); }}>
                    <div className="mb-3">
                      <AvField name="country" label="Country*" placeholder="Enter country here" type="input" value={data.country_name} disabled ></AvField>
                    </div>
                    <div className="mb-3">
                      <label>State</label>
                      <Multiselect placeholder="Select state" options={state} displayValue="name" onSelect={checkMultiSelectState} onRemove={onRemoveState} selectedValues={getMultiStateNames(state, data.all_states)} customCloseIcon={<img alt="white-cross-icon" className="whiteCrossIcon" src={whiteCrossIcon} />} />
                    </div>
                    <FormGroup className="mt-4">
                      <div>
                        <Button type="submit" color="primary" className="ms-1" disabled={isDisabled ? isDisabled : isLoading}> Submit </Button>
                      </div>
                    </FormGroup>
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

## Conclusion

The `EditLocation.js` component is a well-structured React component that efficiently handles the editing of location data with support for asynchronous operations and user feedback. With its use of multiselect dropdowns, form validation, and state management, it provides a robust solution for managing location data in a user-friendly manner.

# BanLocation.js Documentation 📄

Welcome to the documentation for the **BanLocation.js** file, a React component used for managing location bans within an application. This component allows users to ban specific countries or states from a list.

## Table of Contents 📜

1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Imports](#imports)
4. [State Variables](#state-variables)
5. [Lifecycle Methods](#lifecycle-methods)
6. [Helper Methods](#helper-methods)
7. [Render Method](#render-method)
8. [Usage](#usage)

## Overview 📝

The **BanLocation** component is a React class-based component that provides a user interface for banning countries or states. Users can select a country or state from a dropdown list, and upon submission, the selected locations will be marked as banned. The component also provides back navigation to the location listing page.

## Component Structure 🏗️

The structure of the component is as follows:

- **Constructor**: Initializes state variables and references.
- **Lifecycle Method**: `componentDidMount()` to fetch initial country data.
- **Helper Methods**: Methods for fetching data, handling form submissions, and managing dropdown selections.
- **Render Method**: Renders the user interface for the component.

## Imports 📦

The component imports several dependencies:

| **Import**                  | **Description**                                                                             |
|-----------------------------|---------------------------------------------------------------------------------------------|
| React, Component            | Core React library and `Component` class for creating React components.                     |
| Row, Col, Card, CardBody, FormGroup, Button | UI components from `reactstrap` for layout and styling.                          |
| AvForm                      | Form handling from `availity-reactstrap-validation`.                                        |
| Breadcrumbs                 | Custom component for displaying breadcrumb navigation.                                      |
| Link, withRouter            | React Router components for navigation.                                                     |
| Loader                      | Custom `Loader` component to indicate loading states.                                       |
| toast, toastrOptions        | Libraries for showing toast notifications.                                                   |
| addBanCountry               | API helper function for banning a country.                                                  |
| getCountries, getStates     | API helper functions for fetching country and state data.                                   |
| Multiselect                 | Dropdown component for selecting countries/states.                                          |
| whiteCrossIcon              | Image asset used as a custom close icon in the dropdown.                                     |
| SUCCESS_MESSAGES            | Constants for success messages displayed upon successful operations.                        |

## State Variables 🧠

The component manages the following state variables:

| **State Variable**  | **Description**                                                              |
|---------------------|------------------------------------------------------------------------------|
| `isLoading`         | Boolean indicating if data is being loaded.                                  |
| `editMode`          | Boolean indicating if the form is in edit mode.                               |
| `errorMsg`          | String to store error messages.                                              |
| `countries`         | Array holding the list of countries.                                         |
| `state`             | Array holding the list of states for a selected country.                     |
| `country`           | Currently selected country.                                                  |
| `isDisabled`        | Boolean controlling the disabled state of the submit button.                 |
| `selectedCountryList` | Array of selected countries.                                                |
| `addMoreCountry`     | Array of countries to be added for banning.                                  |
| `selectedStateList`  | Array of selected states.                                                    |
| `addMoreState`       | Array of states to be added for banning.                                     |

## Lifecycle Methods ⏳

### `componentDidMount()`

- **Purpose**: Fetches the list of countries when the component mounts.
- **Method**: Calls `getCountryList()` to fetch data.

## Helper Methods ✨

### `getCountryList()`

- **Purpose**: Fetches the list of countries from the API and updates the state.
- **Usage**: Called in `componentDidMount()`.

### `getStateList(id)`

- **Purpose**: Fetches the list of states for a selected country.
- **Parameters**: `id` - The ID of the selected country.

### `handleValidSubmit(event, values)`

- **Purpose**: Handles form submission, adds selected countries or states to the banned list.
- **Parameters**: `event` - The form submission event, `values` - Form values.

### `goToListing()`

- **Purpose**: Navigates back to the location listing page.

### `showLoader(isLoad)`

- **Purpose**: Updates the loading state.
- **Parameters**: `isLoad` - Boolean indicating if loading is in progress.

### `checkMultiSelect(selectedList, selectedItem)`

- **Purpose**: Handles selection in the country multiselect dropdown.
- **Parameters**: `selectedList` - List of selected items, `selectedItem` - Currently selected item.

### `onRemove(selectedList, removedItem)`

- **Purpose**: Handles the removal of items from the country multiselect dropdown.
- **Parameters**: `selectedList` - Remaining selected items, `removedItem` - Item removed.

### `checkMultiSelectState(selectedList, selectedItem)`

- **Purpose**: Handles selection in the state multiselect dropdown.
- **Parameters**: `selectedList` - List of selected items, `selectedItem` - Currently selected item.

### `onRemoveState(selectedList, removedItem)`

- **Purpose**: Handles the removal of items from the state multiselect dropdown.
- **Parameters**: `selectedList` - Remaining selected items, `removedItem` - Item removed.

## Render Method 🖼️

The `render()` method returns the JSX for the component's UI. It includes:

- A loader to indicate loading states.
- Breadcrumb navigation.
- A form with:
  - A country multiselect for selecting countries.
  - A state multiselect for selecting states.
  - A submit button to handle form submission.

## Usage 🚀

To use the **BanLocation** component, it should be rendered within a React Router context to handle navigation. Ensure that necessary services and helper functions are correctly implemented and imported.

This component is a part of an application for managing location bans. It interacts with backend services to fetch and manage data, displaying success messages when operations are completed successfully.

---

By following this documentation, developers can understand the purpose of the **BanLocation.js** component, its structure, and how to integrate it within a React application. This component is vital for managing location-based restrictions within the system.

# 📄 LocationList.js Documentation

## Table of Contents
1. [Overview](#overview)
2. [Components and Libraries Used](#components-and-libraries-used)
3. [State Management](#state-management)
4. [Lifecycle Methods](#lifecycle-methods)
5. [Key Functions](#key-functions)
6. [UI Rendering](#ui-rendering)
7. [Permissions](#permissions)

---

## Overview

The `LocationList.js` component is a **React** component that displays a list of banned countries and their respective states. This component provides functionalities such as viewing, editing, and deleting banned locations, and includes pagination for easier navigation through the list.

---

## Components and Libraries Used

Here is a list of key components and external libraries that are utilized in the `LocationList.js` component:

| Component/Library             | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| `React`                       | A library for building user interfaces.                                     |
| `reactstrap`                  | Provides Bootstrap 4 components as React components.                        |
| `react-super-responsive-table`| A responsive table component for React.                                     |
| `react-bootstrap-sweetalert`  | Provides alert dialogs for confirming actions.                              |
| `react-toastify`              | Provides notifications in the form of toasts.                               |
| `lodash`                      | A utility library delivering consistency and modularity.                     |

---

## State Management

The component uses React's `useState` hook to manage various pieces of state:

- **`counrtyList`**: Stores the list of banned countries retrieved from the server.
- **`isLoading`**: A boolean that indicates whether the data is still being fetched.
- **`selectedCountryName`**: Stores the ID of the country selected for deletion.
- **`deleteModal`**: Controls the visibility of the delete confirmation modal.
- **`totalCount`**: Tracks the total number of countries for pagination.
- **`pageNumber`**: Stores the current page number in the pagination.
- **Permissions**: (`changePermission`, `deletePermission`, `addPermission`) Boolean flags to control permission-based UI elements.

---

## Lifecycle Methods

The `useEffect` hook is used to trigger side effects:

- **Initial Load**: Fetches the banned countries list when the component mounts or the `pageNumber` changes.
- **Permissions Setup**: Sets user permissions based on props passed to the component.

---

## Key Functions

- **`getBannedCountry`**: Asynchronously fetches the list of banned countries from the API and updates the state.
- **`handlePageClick`**: Updates the `pageNumber` state when a new page in the paginator is selected.
- **`openAlert`**: Opens the delete confirmation modal for a selected country.
- **`deleteCountryName`**: Deletes a selected country and updates the list after successful deletion.
- **`closeAlert`**: Closes the delete confirmation modal.

---

## UI Rendering

The component utilizes `reactstrap` components to layout the page and `react-super-responsive-table` to display the list of countries and states:

- **Breadcrumb**: Provides navigational context.
- **Table**: Displays the list of banned countries and states.
- **Buttons**: Allow navigation to add/edit locations and trigger delete actions.
- **Paginator**: Manages pagination of the table view.
- **SweetAlert**: Confirms delete actions with the user.

---

## Permissions

Permissions are handled using flags (`changePermission`, `deletePermission`, `addPermission`) which are set based on user roles and passed permissions. These control the visibility of certain UI elements like the "Edit" and "Delete" buttons, ensuring that only authorized users can perform specific actions.

---

This documentation provides a comprehensive overview of the `LocationList.js` file, explaining its purpose, structure, and functionality in detail. The component is crucial for managing locations within the application, providing administrators with the tools needed to maintain the banned locations list effectively.