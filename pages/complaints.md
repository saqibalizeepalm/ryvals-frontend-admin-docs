# Documentation for `ComplaintDetail.js`

Welcome to the documentation for the `ComplaintDetail.js` file! This file is part of a complaint management system and is primarily responsible for displaying detailed information about a specific complaint. It is built using React and integrates with various APIs and components to deliver its functionality.

## 📑 Index

1. [File Overview](#file-overview)
2. [Key Imports](#key-imports)
3. [Component Structure](#component-structure)
4. [State and Variables](#state-and-variables)
5. [Functions and Methods](#functions-and-methods)
6. [Component Rendering](#component-rendering)
7. [Permissions and Navigation](#permissions-and-navigation)

## 📝 File Overview

The `ComplaintDetail` component serves to fetch and display detailed information about a specific complaint identified by its `complaint ID`. It manages state for complaint details and user permissions, and handles navigation back to the complaints list.

## 📦 Key Imports

Here is a breakdown of the main imports:

| Import Name                 | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| `React`, `useEffect`, `useState` | Core React imports for component structure and state management.          |
| `Link`, `withRouter`        | From `react-router-dom`, used for navigation and routing capabilities.      |
| `Breadcrumbs`               | A component to display breadcrumb navigation.                               |
| `Card`, `CardBody`, `Col`, `Row`, `FormGroup`, `Button` | Bootstrap components for styling and layout.                   |
| `getComplaintDetail`        | A function to fetch complaint details from an API.                         |
| `Loader`                    | A component to indicate loading state.                                      |
| `FilterPermission`          | Utility to filter user permissions.                                         |
| `filterOutPermissionToShowHide` | Helper function to determine visibility based on permissions.              |

## 🏗️ Component Structure

The `ComplaintDetail` component is a functional component defined with React hooks for managing state and side effects.

```jsx
const ComplaintDetail = (props) => {
  // component code
};
```

## 🔧 State and Variables

The component utilizes `useState` to manage several pieces of state:

- **`complaint`**: Stores the details of the complaint.
- **`isLoading`**: Boolean to indicate if the data is currently being loaded.
- **`viewUser`**: Boolean to control the visibility of user-related actions based on permissions.

Additionally, it derives the `complaint ID` from the current URL:

```jsx
const compid = window.location.href;
const compId = compid.substring(compid.lastIndexOf("/") + 1);
```

## ⚙️ Functions and Methods

### `useEffect`

Executes side effects based on changes in `compId`:

- Fetches complaint details.
- Sets user permissions.

### `getDetail`

Fetches and sets the complaint details from the API:

```jsx
const getDetail = async () => {
  setisLoading(true);
  await getComplaintDetail(compId)
    .then((res) => {
      setcomplaint(res);
      setisLoading(false);
    })
    .catch(() => {
      setcomplaint(null);
      setisLoading(false);
      goToBack();
    });
};
```

### `callSetPermission`

Sets the `viewUser` state based on user permissions:

```jsx
const callSetPermission = () => {
  const typeUser = "Users";
  const typeUserView = "view_user";
  const filteredPermissionUser = FilterPermission(props.permission, typeUser);
  if (filteredPermissionUser.length != 0) {
    const setViewuser = filterOutPermissionToShowHide(filteredPermissionUser[0]?.permissions, typeUserView);
    setViewUser(setViewuser);
  }
};
```

### `goToBack`

Redirects the user back to the complaints list:

```jsx
const goToBack = () => {
  props.history.push(returnUrl);
};
```

## 🖼️ Component Rendering

The component renders a detailed view of the complaint, including:

- **Breadcrumbs**: For navigation context.
- **Loader**: Displayed during data fetching.
- **Complaint Details**: Including reporter, accused, registration date, message, and status.

```jsx
<CardBody>
  <Row className="mb-3">
    <Col className="col-12">
      <h4 className="mb-4">{complaint?.lobby?.name}</h4>
    </Col>
    <Col className="col-12 mb-3">
      <strong className="capitalize">Reporter :</strong> {complaint?.reporter?.username}
    </Col>
    <!-- Additional complaint details -->
  </Row>
</CardBody>
```

## 🔐 Permissions and Navigation

The component includes logic to display user-specific actions based on permissions:

- **Viewing User Actions**: Conditional rendering based on `viewUser`.
- **Navigation Links**: To navigate back to the list or to user details.

```jsx
{viewUser ? (
  <Col className="col-12 mb-3">
    <FormGroup className="mt-4">
      <div>
        <Link to={{ pathname: "/user/" + complaint?.offender?.id, data: window.location.pathname }}>
          <Button color="primary" className="ms-1"> Go to Accused Account </Button>
        </Link>
      </div>
    </FormGroup>
  </Col>
) : null}
```

---

Thank you for exploring the documentation. If you have any questions or need further clarification, feel free to reach out! 🌟

# 📜 ComplaintList.js Documentation

Welcome to the **ComplaintList.js** documentation! This guide provides an in-depth look at the `ComplaintList.js` file in your project. This file is designed to display a list of complaints, allowing users to view, filter, and paginate through them. Below, you will find a detailed explanation of its functionality, structure, and components.

---

## 📚 Index

- [Introduction](#-introduction)
- [Imports](#-imports)
- [State Variables](#-state-variables)
- [Functions and Methods](#-functions-and-methods)
  - [useEffect Hook](#useeffect-hook)
  - [callSetPermission](#callsetpermission)
  - [getList](#getlist)
  - [handlePageClick](#handlepageclick)
- [Rendering Logic](#-rendering-logic)
- [Permissions](#-permissions)
- [Components Breakdown](#-components-breakdown)
- [Conclusion](#-conclusion)

---

## 🌟 Introduction

The **ComplaintList.js** component is a central piece of the user interface responsible for managing and displaying a list of user complaints. It leverages various React hooks and libraries to ensure a seamless user experience. This component is equipped with pagination, user permissions checks, and responsive tables for efficient data presentation.

---

## 📥 Imports

At the top of the file, we import several essential libraries and components:

```javascript
import React, { useEffect, useState } from "react";
import { getComplaintList } from "../../services/complaint_user_api_helper";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Link } from "react-router-dom";
import { Row, Col, Card, CardBody } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Paginator from "../../helpers/paginator/paginator";
import FilterPermission from "../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils";
import { permissionsStrings } from "../../helpers/StringConstant";
import { isEmpty } from "lodash";
```

**Category of Imports:**
- **React & Hooks**: Core functionality for building the component.
- **API Helpers**: To fetch complaint data.
- **UI Components**: For layout and styling (`reactstrap`, `react-super-responsive-table`).
- **Pagination & Permissions**: To handle navigation and user access.

---

## 🔗 State Variables

State management is handled using React's `useState` hook. Key state variables include:

| Variable      | Type    | Description                                         |
|---------------|---------|-----------------------------------------------------|
| `complains`   | Array   | Stores the list of complaints fetched from the API. |
| `isLoading`   | Boolean | Indicates if the data is currently being loaded.    |
| `totalCount`  | Number  | Total number of complaints available.               |
| `pageNumber`  | Number  | Current page number for pagination.                 |
| `viewPermission` | Boolean | Controls access to view certain table columns.   |
| `viewUser`    | Boolean | Controls access to user-specific actions/columns.  |

---

## ⚙️ Functions and Methods

### useEffect Hook

The `useEffect` hook is used to initialize data fetching and permission settings when the component mounts or when `pageNumber` changes.

```javascript
useEffect(() => {
    if (isEmpty(props.permission)) {
        setView(true);
    } else {
        callSetPermission();
    }
    getList();
}, [pageNumber]);
```

### callSetPermission

This function checks the user's permissions and updates the view-related state variables accordingly.

```javascript
const callSetPermission = () => {
    const type = permissionsStrings.complaintList;
    const typeView = permissionsStrings.typeComplaintListView;
    const filteredPermission = FilterPermission(props.permission, type);
    
    if (filteredPermission.length !== 0) {
        const setview = filterOutPermissionToShowHide(filteredPermission[0]?.permissions, typeView);
        setView(setview);
    }
    const typeUser = permissionsStrings.userList;
    const typeUserView = permissionsStrings.typeUserListView;
    const filteredPermissionUser = FilterPermission(props.permission, typeUser);
    if (filteredPermissionUser.length != 0) {
        const setViewuser = filterOutPermissionToShowHide(filteredPermissionUser[0]?.permissions, typeUserView);
        setViewUser(setViewuser);
    }
};
```

### getList

Fetches the complaint list from the API and updates the component state with the fetched data.

```javascript
const getList = async () => {
    setisLoading(true);
    await getComplaintList()
        .then((res) => {
            setcomplains(res);
            settotalCount(0);
            setisLoading(false);
        })
        .catch(() => {
            setisLoading(false);
        });
};
```

### handlePageClick

Updates the `pageNumber` when a different page is clicked in the paginator.

```javascript
const handlePageClick = (pageNum) => {
    setpageNumber(pageNum);
};
```

---

## 🖼️ Rendering Logic

The `ComplaintList` component renders a responsive table displaying the list of complaints. It includes conditional rendering based on the `viewPermission` and `viewUser` flags to show or hide specific actions.

---

## 🔐 Permissions

Permissions play a crucial role in determining what actions or data a user can access. The component uses `FilterPermission` and `filterOutPermissionToShowHide` to manage user permissions effectively.

---

## 🛠️ Components Breakdown

- **Breadcrumbs**: Displays the navigation path.
- **Table**: Shows complaints with columns like Serial Number, Lobby Name, Reporter, Accused Username, Complaint Date, Status, and optionally Actions.
- **Paginator**: Allows navigation through the pages of complaints.

---

## 🏁 Conclusion

The **ComplaintList.js** component is a powerful, permission-sensitive UI element for managing complaints in the application. Its utilization of modern React patterns and robust permission handling ensures that it meets the requirements of a dynamic user interface efficiently.

Feel free to explore and modify the component to suit your specific needs! If you have any questions, don't hesitate to reach out. 😊

---