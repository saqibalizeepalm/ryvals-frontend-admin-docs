# ResetPassword.js Documentation

Welcome to the **ResetPassword.js** documentation. This file is part of a user authentication system that provides users with the ability to reset their password. Below you will find a detailed description of the code, its functionality, and its purpose.

## Table of Contents
1. [Introduction](#introduction)
2. [Key Features](#key-features)
3. [Code Walkthrough](#code-walkthrough)
4. [Components and Libraries](#components-and-libraries)
5. [User Interface](#user-interface)
6. [Event Handling](#event-handling)
7. [Conclusion](#conclusion)

---

## Introduction

The **ResetPassword.js** file is a React component designed for resetting passwords in a web application. It handles user input for a new password and confirmation, verifies inputs, and submits them to the backend for processing. The component also provides feedback to the user in the form of success or error messages.

## Key Features

- **Password Reset Form**: Collects user input for new password and confirmation.
- **Validation**: Ensures that password fields are filled and match.
- **Feedback Mechanism**: Displays success or error messages based on user actions.
- **Loader**: Shows a loading indicator while processing the reset request.
- **Redirection**: Redirects users to the login page upon successful password reset.

## Code Walkthrough

### Imports

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, Alert, Container } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { Link, withRouter } from "react-router-dom";
import logo from "../../assets/images/logo-sm-dark.png";
import Loader from "../../components/Common/Loader";
import { confirmpassword } from "../../services/auth_api_helper";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
```

**Dependencies**:
- **React** and **React Router** for component rendering and navigation.
- **reactstrap** for UI components.
- **availity-reactstrap-validation** for form validation.
- **react-toastify** for toast notifications.
- Custom components and services for handling API calls and displaying loaders.

### Component Definition

The component maintains the following states:
- **isLoading**: To manage the loading state.
- **successMsg** and **errorMsg**: To store and display success and error messages.
- **showPassword** and **showConfirmPassword**: To toggle visibility of password fields.

### URL Parameters

The component extracts `id` and `token` from the URL to verify the password reset request:
```javascript
var url_string = window.location.href;
var url = new URL(url_string);
const id = url.searchParams.get("id");
const token = url.searchParams.get("token");
```

### Form Handling

**handleValidSubmit**: This function handles form submission, validates inputs, and makes an API call to reset the password.

```javascript
async function handleValidSubmit(event, values) {
    event.preventDefault();
    showLoader(true);
    setsuccessMsg(null);
    seterrorMsg(null);
    await confirmpassword(values.newpassword, id, token)
        .then((res) => {
            showLoader(false);
            setsuccessMsg(res.success);
            toast.success(res.success, toastrOptions);
            props.history.push("/login");
        })
        .catch((err) => {
            showLoader(false);
            seterrorMsg(err);
        });
}
```

### Component Lifecycle

**useEffect**: Used to set the background class on component mount and remove it on unmount.

### UI Components

- **Loader**: Displays a loading indicator while the password reset is being processed.
- **Success and Error Messages**: Alerts to inform the user of status updates.
- **Password Fields**: Input fields for new password and confirmation, with toggle visibility icons.

## Components and Libraries

| Component/Library            | Description                                              |
|------------------------------|----------------------------------------------------------|
| **React**                    | Frontend library for building user interfaces.           |
| **reactstrap**               | Library for Bootstrap 4 components in React.             |
| **availity-reactstrap-validation** | Form validation library using reactstrap components. |
| **react-router-dom**         | Library for routing in React applications.               |
| **react-toastify**           | Library for displaying toast notifications.              |

## User Interface

The user interface consists of a form with fields for the new password and the confirmation password. It includes validation rules to ensure that both fields are filled out and match. The UI also provides visual feedback through alerts and a loading spinner.

## Event Handling

- **Password Field Toggle**: Allows users to show/hide password inputs using eye icons.
- **Form Submission**: Handles submission with validation and API interaction.

## Conclusion

The **ResetPassword.js** component is a crucial part of the user authentication flow, allowing users to securely reset their passwords. It combines comprehensive form validation, user feedback, and seamless integration with the backend API to provide a smooth user experience.

# Documentation for `user-profile.js` 📄

## Overview 🌟

The `user-profile.js` file is a React component that renders a user profile page. This component allows users to view and edit their profile information, such as their username and email address. It integrates with Redux for state management and uses `availity-reactstrap-validation` for form validation.

## Table of Contents 📚

1. [Imports](#imports)
2. [Component Description](#component-description)
3. [State Management](#state-management)
4. [Lifecycle Methods](#lifecycle-methods)
5. [Form Handling](#form-handling)
6. [Rendering](#rendering)
7. [Prop Types](#prop-types)
8. [Redux Integration](#redux-integration)

## Imports 📥

```javascript
import PropTypes from "prop-types";
import React, { useState, useEffect } from "react";
import { Row, Col, Card, Alert, CardBody, Button } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { connect } from "react-redux";
import { withRouter } from "react-router-dom";
import Breadcrumb from "../../components/Common/Breadcrumb";
import avatar from "../../assets/images/users/avatar-1.jpg";
```

- **React and PropTypes**: For building the component and type-checking props.
- **Reactstrap**: For layout components like `Row`, `Col`, and form elements.
- **Availity Reactstrap Validation**: For form validation.
- **Redux**: For managing application state.
- **React Router**: For routing.
- **Other Imports**: Include Breadcrumb for navigation and an avatar image.

## Component Description 📝

The **`UserProfile`** component manages the display and updating of a user’s profile. It retrieves user data from `localStorage`, displays it, and allows the user to update their username.

## State Management 🗄️

The component uses the `useState` hook to maintain local state:

- **`email`**: Stores the user's email.
- **`name`**: Stores the user's name.
- **`idx`**: Stores the user ID.

## Lifecycle Methods 🔄

The component uses the `useEffect` hook to execute side effects:

- **`useEffect`**: On component mount, retrieves user data from `localStorage` and sets the state. It also resets the profile update flag after a successful update.

```javascript
useEffect(() => {
    if (localStorage.getItem("authUser")) {
        const obj = JSON.parse(localStorage.getItem("authUser"));
        if (process.env.REACT_APP_DEFAULTAUTH === "firebase") {
            setname(obj.displayName);
            setemail(obj.email);
            setidx(obj.uid);
        }
        // Similar setup for other authentication methods
        setTimeout(() => {
            resetProfileFlag();
        }, 3000);
    }
}, [props.success, resetProfileFlag]);
```

## Form Handling 📝

The component handles form submissions to update the user profile:

- **`handleValidSubmit`**: Handles form submissions. Calls `props.editProfile` with the form values.

```javascript
function handleValidSubmit(event, values) {
    props.editProfile(values);
}
```

## Rendering 🎨

The component renders a profile page with:

- **Breadcrumb**: For navigation.
- **Profile Information**: Including an avatar, name, email, and user ID.
- **Edit Form**: Allows the user to update their username.

```jsx
<div className="page-content">
    <Breadcrumb title="Qovex" breadcrumbItem="Profile" />
    <Row>
        <Col lg="12">
            {props.error ? <Alert color="danger">{props.error}</Alert> : null}
            {props.success ? <Alert color="success">{props.success}</Alert> : null}
            <Card>
                <CardBody>
                    <div className="d-flex">
                        <img src={avatar} alt="" className="avatar-md rounded-circle img-thumbnail" />
                        <div className="flex-1 align-self-center">
                            <div className="text-muted">
                                <h5>{name}</h5>
                                <p className="mb-1">{email}</p>
                                <p className="mb-0">Id no: #{idx}</p>
                            </div>
                        </div>
                    </div>
                </CardBody>
            </Card>
        </Col>
    </Row>
    <Card>
        <CardBody>
            <AvForm onValidSubmit={(e, v) => handleValidSubmit(e, v)}>
                <AvField name="username" label="User Name" value={name} required />
                <Button type="submit" color="danger">Edit User Name</Button>
            </AvForm>
        </CardBody>
    </Card>
</div>
```

## Prop Types 📏

The component defines prop types to ensure correct usage:

```javascript
UserProfile.propTypes = {
    editProfile: PropTypes.func,
    error: PropTypes.any,
    success: PropTypes.any,
};
```

- **`editProfile`**: Function to dispatch profile edit actions.
- **`error`**: Error message, if any.
- **`success`**: Success message, if available.

## Redux Integration 🔗

The component connects to the Redux store to receive error and success messages:

```javascript
const mapStatetoProps = (state) => {
    const { error, success } = state.Profile;
    return { error, success };
};

export default withRouter(connect(mapStatetoProps)(UserProfile));
```

This setup allows the component to react to changes in the Redux store, providing a seamless user experience for profile updates.

---

This documentation provides a comprehensive overview of the `user-profile.js` component, explaining its purpose, structure, and functionality in detail. Feel free to refer back to it for any clarification on how the user profile management is implemented. 😊

# Login.js Documentation

Welcome to the documentation for the `Login.js` file. This component is responsible for handling user authentication through a login form. It provides functionality for user input validation, error handling, and redirects upon successful login.

## Table of Contents
- [Overview](#overview)
- [Dependencies](#dependencies)
- [Component Structure](#component-structure)
- [State Variables](#state-variables)
- [Effect Hook](#effect-hook)
- [Functions](#functions)
- [Return Statement](#return-statement)
- [PropTypes](#proptypes)
- [Redux Connection](#redux-connection)

## Overview
The `Login.js` component is a React component that allows users to authenticate by entering their email (or username) and password. It utilizes Redux for state management and React Router for navigation. Upon successful login, the user is redirected to an appropriate page based on their permissions.

## Dependencies
```javascript
import PropTypes from "prop-types";
import React, { useEffect, useState } from "react";
import { Row, Col, Alert, Container } from "reactstrap";
import { connect } from "react-redux";
import { withRouter, Link } from "react-router-dom";
import { AvForm, AvField } from "availity-reactstrap-validation";
import logo from "../../assets/images/ryvals-logo.png";
import { login } from "../../services/auth_api_helper";
import PermissionPath from "../../helpers/PermissionPath";
```

## Component Structure
The `Login` component is a functional component that makes use of hooks for state management and lifecycle methods.

## State Variables
- **errorMessage**: Stores any error messages encountered during login.
- **isLoading**: Indicates whether a login request is in progress.
- **showPassword**: Toggles the visibility of the password input field.

## Effect Hook
The `useEffect` hook is used to apply a specific class to the body element for styling purposes when the component is mounted, and it cleans up this styling when the component is unmounted.

## Functions

### `handleValidSubmit`
This function is triggered upon form submission if the form is valid. It prepares the request body with the user's email and password, invokes the login API, and handles the response.

```javascript
async function handleValidSubmit(event, values) {
    event.preventDefault();
    let body = { email: values.email, password: values.password };
    toggleLoader(true);
    seterrorMessage(null);
    await login(body)
        .then((res) => {
            const redirectPath = PermissionPath();
            setTimeout(() => {
                toggleLoader(false);
                props.history.push(
                    redirectPath === null ? "/users" : redirectPath[0].pathname
                );
            }, 3000);
        })
        .catch((err) => {
            toggleLoader(false);
            seterrorMessage(err);
        });
}
```

### `toggleLoader`
A utility function to toggle the loading spinner.

### `toggleShow`
A function to toggle the visibility of the password field.

## Return Statement
The return statement renders the login form, including:
- An input field for email/username with validation.
- A password input field with a toggle for visibility.
- A submit button that triggers the login process.
- Links for forgotten password and sign-up if applicable.
- Conditional rendering of error messages and loading states.

```jsx
<React.Fragment>
    <div className="account-pages my-5 pt-sm-5">
        <Container>
            <Row className="justify-content-center">
                <Col md={8} lg={6} xl={5}>
                    <div className="card overflow-hidden">
                        <div className="bg-login text-center">
                            <div className="bg-login-overlay"></div>
                            <div className="position-relative">
                                <h5 className="text-white font-size-20">Welcome Back!</h5>
                                <p className="text-white-50 mb-0">Sign in</p>
                                <Link to="/" className="logo logo-admin mt-4">
                                    <img src={logo} alt="" height="30" />
                                </Link>
                            </div>
                        </div>
                        <div className="card-body pt-5">
                            <div className="p-2">
                                <AvForm className="form-horizontal" onValidSubmit={(e, v) => { handleValidSubmit(e, v); }}>
                                    {props.error && typeof props.error === "string" ? (
                                        <Alert color="danger">{props.error}</Alert>
                                    ) : null}
                                    <div className="mb-3">
                                        <AvField name="email" label="Email/Username" className="form-control" placeholder="Enter email/username" validate={{
                                            required: { value: true, errorMessage: "Email/username is required" },
                                            minLength: { value: 5, errorMessage: "Your email/username must be between 5 and 50 characters" },
                                            maxLength: { value: 50, errorMessage: "Your email/username must be between 5 and 50 characters" },
                                        }} autoComplete="off" />
                                    </div>
                                    <div className="mb-3">
                                        <AvField name="password" label="Password" type={showPassword ? "text" : "password"} placeholder="Enter Password" maxLength="50" validate={{
                                            required: { value: true, errorMessage: "Password is required" },
                                        }} autoComplete="off" />
                                        <i onClick={toggleShow} className={showPassword ? "fa fa-eye" : "fa fa-eye-slash"} aria-hidden="true" style={{ cursor: "pointer" }}></i>
                                    </div>
                                    {errorMessage ? (
                                        <p className="error-msg">{errorMessage}</p>
                                    ) : null}
                                    <div className="mt-3">
                                        <button className="btn btn-primary w-100 waves-effect waves-light" type="submit" disabled={isLoading}>
                                            {isLoading && (
                                                <span className="spinner-border spinner-border-sm mr-4"></span>
                                            )}
                                            Log In
                                        </button>
                                    </div>
                                    <div className="mt-4 text-center">
                                        <Link to="/forgot-password" className="text-muted">
                                            <i className="mdi mdi-lock me-1"></i> Forgot your password ?
                                        </Link>
                                    </div>
                                </AvForm>
                            </div>
                        </div>
                    </div>
                </Col>
            </Row>
        </Container>
    </div>
</React.Fragment>
```

## PropTypes
The component defines PropTypes to type-check the props passed to it.

```javascript
Login.propTypes = {
    error: PropTypes.any,
    history: PropTypes.object,
};
```

## Redux Connection
The component is connected to Redux to access the global state and dispatch actions. It utilizes `mapStateToProps` to map the error state to the component's props.

```javascript
const mapStateToProps = (state) => {
    const { error } = state.Login;
    return { error };
};

export default withRouter(connect(mapStateToProps)(Login));
```

This documentation outlines the various aspects and functionalities of the `Login.js` component, providing a comprehensive guide to understanding and using this code.

# Logout.js Documentation 📄

## Overview
The `Logout.js` file is a React component responsible for handling user logout functionality. This component is designed to trigger the logout process as soon as it is mounted, ensuring that the user session is terminated and the user is redirected accordingly.

## Features
- **Automated Logout**: Automatically logs the user out when the component is mounted.
- **Redux Integration**: Utilizes Redux for managing logout actions, ensuring state consistency across the application.
- **Routing Support**: Utilizes `react-router-dom` for seamless navigation and redirection after logout.

## Code Breakdown

### Imports
```javascript
import PropTypes from "prop-types";
import React, { useEffect } from "react";
import { connect } from "react-redux";
import { withRouter } from "react-router-dom";
import { logoutUser } from "../../store/actions";
```
- **PropTypes**: Used for type-checking the props passed to the component.
- **React**: The core library for building user interfaces.
- **useEffect**: A React hook that lets you perform side effects in function components.
- **connect**: A function from `react-redux` to connect the component to the Redux store.
- **withRouter**: A higher-order component from `react-router-dom` to give the component access to the history object's properties.
- **logoutUser**: An action creator imported from the application's store to dispatch logout actions.

### Component Definition
```javascript
const Logout = (props) => {
    useEffect(() => {
        props.logoutUser(props.history);
    });

    return <></>;
};
```
- **useEffect Hook**: 
  - The `useEffect` hook is used here to call the `logoutUser` function with the `history` object as soon as the component is mounted.
  - This ensures that the logout process is initiated immediately, without any additional user action.

### Prop Types
```javascript
Logout.propTypes = {
    history: PropTypes.object,
    logoutUser: PropTypes.func,
};
```
- **PropTypes**: 
  - `history`: Ensures the component receives the `history` object, which is necessary for navigation.
  - `logoutUser`: Ensures the component receives the `logoutUser` function as a prop, which is necessary to perform the logout operation.

### Export
```javascript
export default withRouter(connect(null, { logoutUser })(Logout));
```
- **withRouter**: Wraps the component to inject routing-related props, such as `history`.
- **connect**: Connects the component to the Redux store and provides the `logoutUser` action as a prop to the component.

## Usage 💡
- The `Logout` component is designed to be used in scenarios where a user needs to be logged out from the application. It can be rendered as a standalone component that will automatically handle the logout process.
- **Example Usage**:
  ```jsx
  <Route path="/logout" component={Logout} />
  ```

## Key Points ✨
- **Automated Process**: No additional user interaction is required; the component handles everything upon mounting.
- **State Management**: Integrates with Redux for efficient state management.
- **Routing Integration**: Works seamlessly with `react-router-dom` for navigation after logout.

By utilizing this component, developers can ensure a clean and efficient logout process within their React applications.

# 📄 ForgetPassword.js Documentation

Welcome to the documentation for the `ForgetPassword.js` file. This component is part of a React application and is designed to handle the password reset process for users who have forgotten their password. Below, you'll find a detailed breakdown of its functionality, purpose, and how it integrates with other parts of the application.

---

## 📑 Index

1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Key Features](#key-features)
4. [Code Walkthrough](#code-walkthrough)
5. [Dependencies](#dependencies)
6. [UI Elements](#ui-elements)
7. [How It Works](#how-it-works)
8. [Conclusion](#conclusion)

---

## 🌟 Introduction

The **ForgetPassword.js** component allows users to reset their passwords by entering their email address. Once the email is submitted, the application will initiate a password reset process, typically sending an email to the user with further instructions.

## 🚀 Component Overview

- **Functionality**: Allows users to request a password reset link.
- **Primary UI Elements**: Email input, Submit button, Success/Failure alerts.
- **Dependencies**: React, Reactstrap, Availity Reactstrap Validation, and custom services/components.

## 🛠 Key Features

- **Email Submission Form**: Collects the user's email address.
- **Validation**: Ensures the email format is correct and not empty.
- **Feedback**: Displays success or error messages based on the API response.
- **Loading Indicator**: Shows a loader while the request is being processed.

## 📜 Code Walkthrough

### Import Statements

The component begins by importing necessary dependencies, including React hooks, Reactstrap components, routing utilities, validation tools, and custom services.

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Alert, Container } from "reactstrap";
import { withRouter, Link } from "react-router-dom";
import { AvForm, AvField } from "availity-reactstrap-validation";
import logo from "../../assets/images/logo-sm-dark.png";
import { forgotpassword } from "../../services/auth_api_helper";
import Loader from "../../components/Common/Loader";
```

### Component Definition

The `ForgetPasswordPage` component is a functional component utilizing React hooks for state management and side effects:

- **State Variables**:
  - `successMsg`: Stores success message on successful submission.
  - `isLoading`: Indicates if the submission is being processed.
  - `errorMessage`: Stores error message if the submission fails.

```javascript
const ForgetPasswordPage = (props) => {
    const [successMsg, setsuccessMsg] = useState(null);
    const [isLoading, setisLoading] = useState(false);
    const [errorMessage, seterrorMessage] = useState(null);

    useEffect(() => {
        document.body.className = "authentication-bg";
        return function cleanup() {
            document.body.className = "";
        };
    });
```

### Form Handling

- **handleValidSubmit**: Function that handles form submission. It makes an API call to request a password reset link.

```javascript
    async function handleValidSubmit(event, values) {
        event.preventDefault();
        toggleLoader(true);
        setsuccessMsg(null);
        seterrorMessage(null);
        await forgotpassword(values.email)
            .then((res) => {
                toggleLoader(false);
                setsuccessMsg(res.message);
            })
            .catch((err) => {
                toggleLoader(false);
                if (err) {
                    seterrorMessage(err);
                }
            });
    }
```

- **toggleLoader**: Utility function to manage the loading state.

```javascript
    function toggleLoader(isLoad) {
        setisLoading(isLoad);
    }
```

### JSX Structure

The component's UI is structured using Reactstrap for layout and styling:

```javascript
return (
    <React.Fragment>
        <Loader showLoader={isLoading} />
        <div className="account-pages my-5 pt-sm-5">
            <Container>
                <Row className="justify-content-center">
                    <Col md={8} lg={6} xl={5}>
                        <div className="card overflow-hidden">
                            <div className="bg-login text-center">
                                <div className="bg-login-overlay"></div>
                                <div className="position-relative">
                                    <h5 className="text-white font-size-20">Reset Password</h5>
                                    <a href="/" className="logo logo-admin mt-4">
                                        <img src={logo} alt="" height="30" />
                                    </a>
                                </div>
                            </div>
                            <div className="card-body pt-5">
                                <div className="p-2">
                                    {successMsg ? (
                                        <Alert color="success" className="text-center mb-4" style={{ marginTop: "13px" }}>
                                            {successMsg}
                                        </Alert>
                                    ) : null}
                                    <AvForm className="form-horizontal" onValidSubmit={(e, v) => handleValidSubmit(e, v)}>
                                        <div className="mb-3">
                                            <AvField
                                                name="email"
                                                label="Email"
                                                className="form-control"
                                                placeholder="Enter email"
                                                validate={{
                                                    email: { value: true, errorMessage: "Invalid email address format" },
                                                    required: { value: true, errorMessage: "Email address is required" },
                                                    maxLength: { value: 50, errorMessage: "Email address can have 50 characters max" },
                                                }}
                                                autoComplete="off"
                                            />
                                        </div>
                                        {errorMessage ? <p className="error-msg">{errorMessage}</p> : null}
                                        <Row className="row mb-0">
                                            <Col className="col-12 text-end">
                                                <button className="btn btn-primary w-md waves-effect waves-light" type="submit">
                                                    Reset
                                                </button>
                                            </Col>
                                        </Row>
                                        <div className="mt-5 text-center">
                                            <p> Remember It?{" "} <Link to="/login" className="fw-medium text-primary"> Sign In here </Link>{" "} </p>
                                        </div>
                                    </AvForm>
                                </div>
                            </div>
                        </div>
                    </Col>
                </Row>
            </Container>
        </div>
    </React.Fragment>
);
```

### Export Statement

Finally, the component is exported using the `withRouter` HOC, enabling it to access the router's props and methods.

```javascript
export default withRouter(ForgetPasswordPage);
```

## 📦 Dependencies

- **React**: For building the component.
- **Reactstrap**: For UI components.
- **Availity Reactstrap Validation**: For form validation.
- **React Router**: For navigation.

## 🎨 UI Elements

- **Email Input**: Captures the user's email address.
- **Reset Button**: Triggers the password reset process.
- **Success/Error Messages**: Provides feedback to the user.
- **Loader**: Indicates loading state during API call.

## 🔄 How It Works

1. **User Visits Page**: The component renders a form with an email input field.
2. **User Submits Email**: Upon entering a valid email and submitting the form, the `handleValidSubmit` function is triggered.
3. **API Call**: The email is sent to the backend to initiate the password reset process.
4. **Feedback**: The user receives a success or error message based on the API response.
5. **Loader**: A loading indicator is shown while the request is processed.

## 🏁 Conclusion

The `ForgetPassword.js` component is a crucial part of any application's authentication process, providing users with a way to regain access to their accounts if they have forgotten their passwords. Its integration of form validation, API calls, and user feedback ensures a smooth user experience.

# ChangePassword.js Documentation 📄

Welcome to the **ChangePassword.js** documentation! This document provides an in-depth look into the code and functionality of the ChangePassword component. This React component is used to handle the process of changing an admin user's password. It ensures that users can update their credentials in a secure and user-friendly manner.

## Index 📚

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component State](#component-state)
4. [Functions and Methods](#functions-and-methods)
5. [UI Components](#ui-components)
6. [Usage](#usage)
7. [Summary](#summary)

---

## Introduction 📖

The `ChangePassword.js` file contains a React component that is part of an authentication system. The component allows the user to change their password by providing the current password and the new password. It features real-time validation and user feedback.

## Dependencies 📦

The component utilizes several external libraries and components:

- **React**: Core library for building UI components.
- **reactstrap**: For responsive layout and form components.
- **availity-reactstrap-validation**: Provides form validation.
- **react-router-dom**: Used for navigation and routing.
- **react-toastify**: Displays notifications.
- **Custom Imports**:
  - `changeAdminPassword`: API helper function to update the password.
  - `toastrOptions`: Configuration for toast notifications.
  - `Breadcrumbs`: Component for displaying navigation breadcrumbs.

## Component State 📊

The component uses the following state variables:

| State Variable       | Type    | Description                                      |
|----------------------|---------|--------------------------------------------------|
| `loader`             | Boolean | Indicates if the form is in a loading state.     |
| `showPassword`       | Boolean | Determines visibility of the new password field. |
| `showConfirmPassword`| Boolean | Determines visibility of the confirm password field. |
| `showCurrentPassword`| Boolean | Determines visibility of the current password field. |
| `disableSubmit`      | Boolean | Disables the submit button when true.            |

## Functions and Methods 🛠️

### handleValidSubmit

This asynchronous function is triggered on form submission. It handles the password change logic.

```javascript
async function handleValidSubmit(event, values) {
    event.preventDefault();
    let model = {
        current_password: values.currentpassword,
        new_password: values.newpassword,
        confirm_password: values.confirmpassword,
    };
    setLoader(true);
    setDisableSubmit(true);
    await changeAdminPassword(model)
        .then((res) => {
            setLoader(false);
            setDisableSubmit(false);
            toast.success(res.message, toastrOptions);
            setTimeout(() => {
                props.history.push("/logout");
            }, 2000);
        })
        .catch((err) => {
            setLoader(false);
            setDisableSubmit(false);
        });
}
```

### Toggle Functions

These functions toggle the visibility of password fields.

- `toggleCurrentShow`: Toggles the current password field visibility.
- `toggleShow`: Toggles the new password field visibility.
- `toggleConfirmPassword`: Toggles the confirm password field visibility.

## UI Components 🖥️

- **Breadcrumbs**: Displays the "CHANGE PASSWORD" breadcrumb.
- **Form Fields**: 
  - Current Password
  - New Password
  - Confirm Password
- **Submit Button**: Toggles between enabled/disabled states based on form validity.

### Loading Spinner

Displays a loading spinner when the form is in a loading state.

```jsx
{loader ? (
    <div class="spinner-grow spinner-class" role="status" style={{ marginTop: "40px" }}>
        <span class="sr-only">Loading...</span>
    </div>
) : (
    // Form goes here
)}
```

## Usage 🚀

To use this component, simply include it in your application where password change functionality is needed. Make sure you have the necessary services and helper functions configured, as well as the required dependencies installed.

## Summary 📝

The **ChangePassword.js** component is a vital part of the user authentication system, providing an intuitive interface for users to securely change their passwords. It features a responsive design, form validation, and provides feedback through toast notifications, ensuring a seamless user experience.