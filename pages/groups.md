# Documentation for `AddEditGroup.js` 📄

Welcome to the documentation for `AddEditGroup.js`, an essential component of a React application for managing user groups with specific permissions. This file is a complex form that allows users to add or edit groups and manage their associated permissions. Below, you will find a detailed breakdown of the code and its functionality.

---

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Imports and Dependencies](#imports-and-dependencies)
3. [Component Structure](#component-structure)
4. [State Variables](#state-variables)
5. [Lifecycle Methods](#lifecycle-methods)
6. [Methods and Functions](#methods-and-functions)
7. [Render Method](#render-method)
8. [Conclusion](#conclusion)

---

## Introduction

The `AddEditGroup` component is a React class component that provides a user interface for adding or editing groups within an application. It allows users to assign specific permissions to groups, which is crucial for managing user access and capabilities within the system.

---

## Imports and Dependencies

Here's a quick look at the files and libraries used in `AddEditGroup.js`:

```javascript
import React, { Component } from "react";
import { Row, Col, Card, CardBody, FormGroup, Button } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Link, withRouter } from "react-router-dom";
import Loader from "../../components/Common/Loader";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import { addEditGroups, getGroupLists, getPermissionLists, getGroupDetailByID } from "../../services/admin_user_api_helper";
import FindPermission from "../../helpers/Find_Permission";
import FindAllowedPermission from "../../helpers/FindAllowedPermission";
import { defaultCheckedPermissions, givenAndUploadpermission, } from "../../helpers/PermissionUtils";
import { defaultViewPermission } from "../../helpers/PermissionUtils";
import { assignDefaultViewPermission } from "../../helpers/PermissionUtils";
import { deleteGivenPermission } from "../../helpers/PermissionUtils";
import { findViewPermissionId } from "../../helpers/PermissionUtils";
```

### Key Libraries Used:

- **React and Reactstrap:** For building the UI components.
- **AvForm and AvField:** For form validation.
- **React Router:** To handle navigation and routing.
- **React Toastify:** For displaying success and error messages.
- **Custom Helpers and Services:** For handling permissions and API calls.

---

## Component Structure

The `AddEditGroup` component extends the `React.Component` class and is exported using `withRouter` to have access to the router's props. It uses several lifecycle methods and custom functions to manage the state and interact with the backend API.

### Constructor

The constructor initializes the component's state, binding necessary methods.

```javascript
constructor(props) {
  super(props);
  this.state = {
    editMode: false,
    groupId: null,
    errorMsg: null,
    groupName: null,
    assignedPermissionLists: [],
    allPermissions: [],
    givenPermission: [],
    allowedPermission: [],
    showPermission: false,
    defaultViewPermissionIds: [],
    uploadPermission: [],
  };
  this.handleChange = this.handleChange.bind(this);
}
```

---

## State Variables

Below is a table summarizing the key state variables used in the component:

| State Variable             | Description                                                      |
|----------------------------|------------------------------------------------------------------|
| `editMode`                 | Indicates if the component is in edit mode or add mode.          |
| `groupId`                  | Stores the ID of the group being edited.                         |
| `errorMsg`                 | Stores any error messages generated during validation or submission. |
| `groupName`                | Holds the name of the group being created or edited.             |
| `assignedPermissionLists`  | Holds permissions assigned to the group.                         |
| `allPermissions`           | Stores all available permissions for groups.                     |
| `givenPermission`          | List of permissions currently given to the group.                |
| `allowedPermission`        | Permissions that are allowed to be assigned.                     |
| `defaultViewPermissionIds` | IDs of default view permissions.                                 |
| `uploadPermission`         | List of upload permissions assigned to the group.                |

---

## Lifecycle Methods

### `componentDidMount`
This lifecycle method is called after the component is mounted. It initializes the permissions and checks if the component is in edit mode.

```javascript
componentDidMount() {
  this.getAllPermissionList();
  const groupId = this.props.match.params.groupId;
  if (groupId) {
    this.setState({
      editMode: true,
      groupId: groupId,
    });
    this.getGroupDetail(groupId);
  }
}
```

---

## Methods and Functions

### `handleValidSubmit`
Handles the form submission after successful validation. It checks for permissions and either creates or updates a group.

```javascript
async handleValidSubmit(event) {
  event.preventDefault();
  // Logic to check permissions and submit data...
}
```

### `getGroupDetail`
Fetches group details by ID when editing an existing group.

```javascript
async getGroupDetail(groupId) {
  try {
    const res = await getGroupDetailByID(groupId);
    this.mapDetailsToForm(res);
  } catch (error) {
    // Error handling
  }
}
```

### `getAllPermissionList`
Fetches all available permissions to display in the form.

```javascript
async getAllPermissionList() {
  try {
    const res = await getPermissionLists();
    this.setState({ allPermissions: res, showPermission: true });
  } catch (error) {
    // Error handling
  }
}
```

### `mapDetailsToForm`
Maps the fetched group details to the form state.

```javascript
mapDetailsToForm(res) {
  this.setState({
    groupName: res.name,
    assignedPermissionLists: res.permissions,
  });
  this.callPermission(res.permissions);
}
```

### `handleChange`
Handles changes in form fields and updates the state.

```javascript
handleChange(event) {
  this.setState({ [event.target.name]: event.target.value });
}
```

---

## Render Method

The render method returns the JSX to display the form, including permission checkboxes and radio buttons. It utilizes `Reactstrap` components for layout and design.

```javascript
render() {
  return (
    <React.Fragment>
      <Loader showLoader={this.state.isLoading} />
      <div className="page-content">
        <Breadcrumbs breadcrumbItem={(this.state.editMode ? "Edit" : "Add") + " Group"} />
        <Row>
          <Col lg={12}>
            <Card>
              <CardBody>
                <Row className="mb-4">
                  <Col>
                    <p>
                      <Link to="/groups">
                        <i className="mdi mdi-arrow-left"></i> back
                      </Link>
                    </p>
                  </Col>
                </Row>
                <Row className="add-staff-member">
                  <Col className="col-lg-8 col-md-8 col-sm-8 col-12">
                    <AvForm onValidSubmit={(e, v) => { this.handleValidSubmit(e, v); }}>
                      <div className="mb-3">
                        <AvField
                          name="groupName"
                          label="Group Name*"
                          placeholder="Enter group name here"
                          type="text"
                          value={this.state.groupName}
                          onChange={this.handleChange}
                          validate={{
                            required: { value: true, errorMessage: "Group name is required" },
                            maxLength: { value: 50, errorMessage: "Group name can have 50 characters max" },
                          }}
                        />
                      </div>
                      {this.state.showPermission ? (
                        <div className="mb-3 permissionsBoxes">
                          // Code for displaying permissions...
                        </div>
                      ) : null}
                      {this.state.errorMsg ? (
                        <p className="error-msg">{this.state.errorMsg}</p>
                      ) : null}
                      <FormGroup className="mt-4">
                        <div>
                          <Button type="submit" color="primary" className="ms-1" disabled={this.state.isLoading}>
                            Submit
                          </Button>
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
}
```

### Highlights:
- The form includes input for group name and dynamic permission checkboxes.
- Utilizes `AvForm` for validation.
- Displays a loader during API operations.
- Displays error messages when applicable.

---

## Conclusion

The `AddEditGroup` component is a robust tool for managing user groups and permissions within a React application. It leverages a combination of state management, API interactions, and form validation to provide a seamless user experience. Understanding its structure and functionality is crucial for maintaining and extending the application's capabilities.

Feel free to explore and modify this component to best fit your application's needs! 🛠️

# Documentation for `GroupList.js` 📄

This document provides a comprehensive overview and explanation of the `GroupList.js` file, a React component responsible for displaying and managing a list of user groups. This component renders a table showcasing the available groups, their permissions, and provides options for adding, editing, or deleting groups based on user permissions.

---

## Table of Contents 📑

1. [Overview](#overview-)
2. [Component Structure](#component-structure-)
3. [Key Functionalities](#key-functionalities-)
4. [State Management](#state-management-)
5. [Permissions Handling](#permissions-handling-)
6. [Loading and Error Handling](#loading-and-error-handling-)
7. [Code Explanation](#code-explanation-)
8. [Conclusion](#conclusion-)

---

## Overview 📝

The `GroupList` component is a functional React component designed to manage and display a list of groups and their associated permissions. It utilizes several third-party libraries like `reactstrap` for UI components, `react-super-responsive-table` for responsive table layouts, and `react-toastify` for notifications.

---

## Component Structure 🏗️

Here’s a breakdown of the `GroupList` component’s structure and the primary imports utilized:

- **UI Components**: Leverages `reactstrap` for UI elements like `Row`, `Col`, `Card`, and `Button`.
- **Table Components**: Uses `react-super-responsive-table` to ensure tables are mobile-friendly.
- **Breadcrumb**: Utilizes a custom `Breadcrumbs` component for navigation context.
- **Routing**: Implements `react-router-dom` for navigation links.
- **API Helpers**: Imports functions to fetch and manipulate group data from the backend.
- **Toaster Notifications**: Uses `react-toastify` to show success and error messages.

---

## Key Functionalities 🔧

The `GroupList` component provides several key functionalities:

- **Fetching and Displaying Groups**: Retrieves a list of groups from the backend and displays them in a responsive table format.
- **Permissions Management**: Controls the visibility of actions (Add, Edit, Delete) based on user permissions.
- **Responsive Design**: Ensures tables are viewable and functional on a variety of screen sizes.
- **Interactive Actions**: Allows users to add, edit, or delete groups based on their permissions.

---

## State Management 🗂️

The component utilizes React's `useState` hook to manage its internal state:

- **groups**: An array that holds the list of groups fetched from the server.
- **isLoading**: A boolean that indicates if the data is currently being loaded.
- **Permissions**: Booleans (`changePermission`, `deletePermission`, `addPermission`) that determine if the user has the rights to perform certain actions.

---

## Permissions Handling 🔐

The component manages permissions through the following steps:

1. **Initialization**: Checks if any permissions are passed through props.
2. **Filtering**: Uses helper functions to determine which UI elements (Add, Edit, Delete buttons) should be displayed based on the user's permissions.
3. **Rendering**: Conditionally renders UI elements based on the evaluated permissions.

---

## Loading and Error Handling ⏳❗

- **Loading Spinner**: Displays a spinner while data is being fetched.
- **Error Messages**: Uses `react-toastify` to notify users of any errors like failure to fetch data or delete a group.

---

## Code Explanation 📜

Here is a detailed look at the primary segments of code:

```javascript
// Import necessary modules and components
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, Button } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Link } from "react-router-dom";
import { getGroupList, deleteGroup } from "../../services/admin_user_api_helper";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import FilterPermission from "../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils";
import { isEmpty } from "lodash";

// Define the GroupList functional component
const GroupList = (props) => {
    // Define state variables
    const [groups, setGroups] = useState([]);
    const [isLoading, setisLoading] = useState(false);
    const [changePermission, setChange] = useState(false);
    const [deletePermission, setDelete] = useState(false);
    const [addPermission, setAdd] = useState(false);

    // Fetch group data and set permissions on component mount
    useEffect(() => {
        getListing();
        if (isEmpty(props.permission)) {
            setChange(true);
            setDelete(true);
            setAdd(true);
        } else {
            callSetPermission();
        }
    }, []);

    // Define functions to handle permissions and data retrieval
    const callSetPermission = () => {
        const type = "Group";
        const typeChange = "change_group";
        const typeDelete = "delete_group";
        const typeAdd = "add_group";
        const filteredPermission = FilterPermission(props.permission, type);
        if (filteredPermission.length !== 0) {
            const setchange = filterOutPermissionToShowHide(filteredPermission[0].permissions, typeChange);
            const setdelete = filterOutPermissionToShowHide(filteredPermission[0].permissions, typeDelete);
            const setadd = filterOutPermissionToShowHide(filteredPermission[0].permissions, typeAdd);
            setChange(setchange);
            setDelete(setdelete);
            setAdd(setadd);
        }
    };

    async function getListing() {
        setisLoading(true);
        await getGroupList()
            .then((res) => {
                setGroups(res.data);
                setisLoading(false);
            })
            .catch(() => {
                setisLoading(false);
            });
    }

    const handleDelete = async (delId) => {
        setisLoading(true);
        await deleteGroup(delId)
            .then(() => {
                getListing();
                toast.success("Deleted Successfully", toastrOptions);
                setisLoading(true);
            })
            .catch(() => {
                setisLoading(false);
            });
    };

    // Render the component
    return (
        <React.Fragment>
            <div className="page-content">
                <Breadcrumbs breadcrumbItem="Manage Groups" />
                <Row>
                    <Col className="col-12">
                        <Card>
                            <CardBody>
                                {addPermission ? (
                                    <Row className="search-box">
                                        <Col className="col-lg-2 col-sm-4">
                                            <Link to="/groups/add">
                                                <button className="btn btn-primary"> Add Groups </button>
                                            </Link>
                                        </Col>
                                    </Row>
                                ) : null}
                                <div className="table-rep-plugin">
                                    <div className="table-responsive mb-0">
                                        <Table className="table table-striped table-bordered staff-table">
                                            <Thead>
                                                <Tr>
                                                    <Th>Level</Th>
                                                    <Th data-priority="1">Permission</Th>
                                                    {changePermission || deletePermission ? (
                                                        <Th data-priority="6">Actions</Th>
                                                    ) : null}
                                                </Tr>
                                            </Thead>
                                            <Tbody>
                                                {isLoading ? (
                                                    <div className="spinner-grow transaction-spinner"></div>
                                                ) : groups.length === 0 ? (
                                                    <h5 className="text-center mt-4"> No Group(s) Found </h5>
                                                ) : (
                                                    groups.map((item, index) => (
                                                        <Tr key={index}>
                                                            <Td>{item?.name}</Td>
                                                            <Td>
                                                                {item.permissions.map((list, id) => (
                                                                    <ul key={id}>
                                                                        <li>
                                                                            {list.name} {list.permission_name && `(${list.permission_name})`}
                                                                        </li>
                                                                    </ul>
                                                                ))}
                                                            </Td>
                                                            {changePermission ? (
                                                                <Td>
                                                                    <Link to={`/groups/edit/${item?.id}`}>
                                                                        <Button className="btn btn-sm complaint-view-btn btn-secondary">
                                                                            Edit
                                                                        </Button>
                                                                    </Link>
                                                                </Td>
                                                            ) : null}
                                                            {deletePermission ? (
                                                                <Td className="location-delete-btn">
                                                                    <button
                                                                        className="btn btn-sm complaint-view-btn btn-secondary"
                                                                        onClick={() => handleDelete(item?.id)}
                                                                    >
                                                                        Delete
                                                                    </button>
                                                                </Td>
                                                            ) : null}
                                                        </Tr>
                                                    ))
                                                )}
                                            </Tbody>
                                        </Table>
                                    </div>
                                </div>
                            </CardBody>
                        </Card>
                    </Col>
                </Row>
            </div>
        </React.Fragment>
    );
};

// Export the component
export default GroupList;
```

---

## Conclusion 🔍

The `GroupList.js` component is a crucial part of managing user groups within the application. It effectively uses state and props to handle permissions dynamically, ensuring that users with the correct permissions can manage groups efficiently. Its responsive design and user-friendly interface make it a robust solution for group management tasks in web applications. By utilizing React hooks and third-party libraries, the component maintains a clean codebase while delivering a seamless user experience.