# 📄 UserDetail.js Documentation

Welcome to the comprehensive documentation for the **UserDetail.js** component! This guide will walk you through the purpose, structure, and functionality of this intricate component used in a React application. 

---

## 📚 Index

- [Overview](#overview)
- [Imports](#imports)
- [Component Structure](#component-structure)
- [State](#state)
- [Lifecycle Methods](#lifecycle-methods)
- [Utility Functions](#utility-functions)
- [Event Handlers](#event-handlers)
- [Render Method](#render-method)
- [Dependencies](#dependencies)

---

## 📖 Overview

The **UserDetail.js** component is a React class component designed to display detailed information about a user within an application. It manages user data, handles user status changes (activation/deactivation), and displays transaction history. It's designed with permissions in mind, allowing only certain actions based on the user's roles.

---

## 📦 Imports

Here's a breakdown of the modules and components imported into **UserDetail.js**:

```javascript
import { Link, withRouter } from "react-router-dom"; // Navigation and routing components
import { Card, CardBody, Col, Row, Button, TabContent, TabPane, NavLink, NavItem, Nav, } from "reactstrap"; // UI components from Reactstrap
import Breadcrumbs from "../../components/Common/Breadcrumb"; // Custom Breadcrumb component
import { getUserDetail, activateDeactivateUser, } from "../../services/user_api_helper"; // API service functions
import React, { Component } from "react"; // React dependencies
import SweetAlert from "react-bootstrap-sweetalert"; // Alert for confirmation dialogs
import classnames from "classnames"; // Utility for conditional class names
import LatestTransaction from "../Dashboard/latest-transaction"; // Component for displaying transaction history
import EarningTimeline from "../../helpers/EarningTimeline"; // Helper for earnings
import FilterPermission from "../../helpers/FilterPermission"; // Permission utility
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils"; // Permission utility
import EditReferral from "../../helpers/EditReferral"; // Component for editing referrals
import EditFreeLobby from "../../helpers/EditFreeLobby"; // Component for editing free lobby limits
import { isEmpty } from "lodash"; // Utility for checking empty objects
```

---

## 🏗️ Component Structure

The `UserDetail` component is a class-based component extending from `React.Component`. It manages its own state and lifecycle to render user details dynamically.

### Constructor

The constructor initializes the state with several properties related to user data, loading indicators, and permission checks.

```javascript
constructor(props) {
    super(props);
    this.state = {
        user: null,
        loader: true,
        deactivate_alert: false,
        activate_alert: false,
        deactivateReason: null,
        activeTab: this.props.location?.data?.activeTab == "1" ? "2" : "1",
        selectedUser: null,
        deactivateUserSuccessMessage: false,
        disableSwal: false,
        editEarning: false,
        permission: [],
        permissionTransaction: [],
        changePermission: false,
        deletePermission: false,
        viewPermission: false,
        changePermissionTransaction: false,
        viewPermissionTransaction: false,
    };
}
```

---

## 🔄 Lifecycle Methods

### `componentDidMount`

This method fetches user details when a user ID is present and sets permissions based on the current user's roles.

```javascript
componentDidMount() {
    this.setState({ loader: true });
    let userId = this.props.match.params.userId;
    if (userId) {
        this.getDetailOfUser(userId);
    }
    if (isEmpty(this.props.permission)) {
        this.setState({ changePermission: true, deletePermission: true, viewPermission: true });
    } else {
        this.callSetPermission();
    }
}
```

---

## ⚙️ Utility Functions

### `callSetPermission`

This function sets the permissions for the user and transaction details based on the roles.

```javascript
callSetPermission = () => {
    const type = "Users";
    const typeChange = "change_user";
    const typeDelete = "delete_user";
    const typeView = "view_user";
    const filteredPermission = FilterPermission(this.props.permission, type);
    // Additional logic for permissions
};
```

### `getDetailOfUser`

Fetches the user detail from the API and updates the state.

```javascript
async getDetailOfUser(userId) {
    try {
        this.setState({ loader: true });
        const res = await getUserDetail(userId);
        this.setState({ user: res, loader: false });
    } catch (error) {
        this.setState({ loader: false });
    }
}
```

---

## 🎛️ Event Handlers

### `handleDeactivateText`

Handles the input change for the deactivation reason.

```javascript
handleDeactivateText(e) {
    e.preventDefault();
    this.setState({ deactivateReason: e.target.value });
}
```

### `deactivateUserStatus`

Handles the activation/deactivation of a user.

```javascript
async deactivateUserStatus() {
    this.setState({ disableSwal: true, deactivate_alert: false, activate_alert: false });
    if (this.state.selectedUser.status === 1)
        if (!this.state.deactivateReason || this.state.deactivateReason === "") {
            return;
        }
    // Additional logic for user activation/deactivation
};
```

---

## 🖼️ Render Method

The `render` method constructs the JSX layout for user details and transaction history with tabs for navigation.

```javascript
render() {
    return (
        <React.Fragment>
            <div className="page-content">
                <Breadcrumbs breadcrumbItem="User Detail" />
                <Row>
                    {/* Additional JSX layout */}
                </Row>
            </div>
        </React.Fragment>
    );
}
```

### Key Components in Render

- **Breadcrumbs**: Displays the navigation path.
- **Loader**: Shows a loading indicator while data is being fetched.
- **Tabs**: Offers navigation between user details and transaction history.
- **Buttons**: Allow editing and activating/deactivating users.

---

## 📦 Dependencies

The component relies on several third-party libraries and custom components:

- **react-router-dom**: For routing and navigation.
- **reactstrap**: For UI components.
- **lodash**: For utility functions.
- **react-bootstrap-sweetalert**: For alert dialogs.
- **classnames**: For conditional CSS classes.

---

This documentation provides a detailed overview of the **UserDetail.js** component, explaining its structure, functionality, and integrations within a React application. We hope this guide aids in understanding and maintaining the component effectively! 🚀