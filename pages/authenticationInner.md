# 📄 Register.js Documentation

This document provides a comprehensive overview of the `Register.js` file, which is part of a user authentication system. The file is responsible for rendering the user registration page, handling form submissions, and managing the registration process through the Redux store.

## 📑 Index

1. [Overview](#overview)
2. [Imports](#imports)
3. [Component Structure](#component-structure)
4. [Key Features](#key-features)
5. [Prop Types](#prop-types)
6. [Redux Integration](#redux-integration)
7. [Styling and Classes](#styling-and-classes)

## 📝 Overview

The `Register.js` file is a React component that provides a registration form for new users to create accounts. It uses `availity-reactstrap-validation` for form validation and Redux for state management. The form includes fields for email, username, and password, and it displays success or error messages based on the registration outcome.

## 📦 Imports

Let's take a look at the libraries and modules imported in this file:

| Module | Purpose |
|--------|---------|
| `PropTypes` | For type-checking React props. |
| `React` | For creating React components and using hooks. |
| `reactstrap` | For Bootstrap components like `Row`, `Col`, `Card`, etc. |
| `availity-reactstrap-validation` | For form validation components. |
| `redux` | For connecting the component to the Redux store. |
| `react-router-dom` | For navigation and links. |

```javascript
import PropTypes from "prop-types";
import React, { useEffect } from "react";
import { Row, Col, Card, Alert, Container } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { registerUser, apiError, registerUserFailed } from "../../store/actions";
import { connect } from "react-redux";
import { Link } from "react-router-dom";
import logo from "../../assets/images/logo-sm-dark.png";
```

## 🏗️ Component Structure

The `Register` component is structured to display a registration form, handle form submissions, and display appropriate feedback messages.

### JSX Structure

- **Home Button**: A link to the home page.
- **Account Pages**: A container for the registration form.
- **Card**: Contains the registration form and feedback messages.
- **Form**: Includes fields for email, username, and password.

```javascript
const Register = props => {
    // handleValidSubmit
    const handleValidSubmit = (event, values) => {
        props.registerUser(values);
    };

    useEffect(() => {
        props.apiError("");
        document.body.className = "authentication-bg";
        return function cleanup() {
            document.body.className = "";
        };
    });

    return (
        <React.Fragment>
            <div className="home-btn d-none d-sm-block">
                <Link to="/" className="text-dark">
                    <i className="fas fa-home h2"></i>
                </Link>
            </div>
            <div className="account-pages my-5 pt-sm-5">
                <Container>
                    <Row className="justify-content-center">
                        <Col md={8} lg={6} xl={5}>
                            <Card className="overflow-hidden">
                                <div className="bg-login text-center">
                                    <div className="bg-login-overlay"></div>
                                    <div className="position-relative">
                                        <h5 className="text-white font-size-20">Free Register</h5>
                                        <p className="text-white-50 mb-0">Get your free Qovex account now</p>
                                        <Link to="/" className="logo logo-admin mt-4">
                                            <img src={logo} alt="" height="30" />
                                        </Link>
                                    </div>
                                </div>
                                <div className="card-body pt-5">
                                    <div className="p-2">
                                        <AvForm className="form-horizontal" onValidSubmit={(e, v) => { handleValidSubmit(e, v) }}>
                                            {props.user && props.user ? (
                                                <Alert color="success"> Register User Successfully </Alert>
                                            ) : null}
                                            {props.registrationError && props.registrationError ? (
                                                <Alert color="danger"> {props.registrationError} </Alert>
                                            ) : null}
                                            <div className="mb-3">
                                                <AvField id="email" name="email" label="Email" className="form-control" placeholder="Enter email" type="email" required />
                                            </div>
                                            <div className="mb-3">
                                                <AvField name="username" label="Username" type="text" required placeholder="Enter username" />
                                            </div>
                                            <div className="mb-3">
                                                <AvField name="password" label="Password" type="password" required placeholder="Enter Password" />
                                            </div>
                                            <div className="mt-4">
                                                <button className="btn btn-primary w-100 waves-effect waves-light" type="submit">Register</button>
                                            </div>
                                            <div className="mt-4 text-center">
                                                <p className="mb-0"> By registering you agree to the Qovex{" "} <Link to="#" className="text-primary"> Terms of Use </Link> </p>
                                            </div>
                                        </AvForm>
                                    </div>
                                </div>
                            </Card>
                            <div className="mt-5 text-center">
                                <p>Already have an account ? <a href="/pages-login" className="fw-medium text-primary"> Login</a></p>
                                <p>© {new Date().getFullYear()} Qovex. Crafted with <i className="mdi mdi-heart text-danger"></i> by Themesbrand</p>
                            </div>
                        </Col>
                    </Row>
                </Container>
            </div>
        </React.Fragment>
    );
};
```

## 🌟 Key Features

- **Form Validation**: Utilizes `availity-reactstrap-validation` for ensuring that the input fields are filled correctly.
- **Feedback Messages**: Displays alerts for successful registration or errors encountered during the process.
- **Responsive Design**: Uses Bootstrap components for a responsive layout.
- **Redux Integration**: Connects to the Redux store to dispatch registration actions and manage state.
- **Navigation Links**: Includes links to login and home pages.

## 🔗 Prop Types

The component uses `PropTypes` to enforce the type and presence of certain props.

```javascript
Register.propTypes = {
    registerUser: PropTypes.func,
    registerUserFailed: PropTypes.func,
    registrationError: PropTypes.any,
    user: PropTypes.any,
};
```

## 🔄 Redux Integration

The component is connected to the Redux store to handle registration actions and manage error states.

### Map State to Props

Maps Redux state to component props for user data and registration errors.

```javascript
const mapStatetoProps = state => {
    const { user, registrationError, loading } = state.Account;
    return { user, registrationError, loading };
};
```

### Map Dispatch to Props

Connects actions to component props for dispatching user registration and error handling actions.

```javascript
export default connect(mapStatetoProps, { registerUser, apiError, registerUserFailed, })(Register);
```

## 🎨 Styling and Classes

The component utilizes Bootstrap's grid system and custom CSS classes for layout and styling.

- **Background and Overlays**: Uses CSS classes like `.bg-login`, `.bg-login-overlay`, and `.authentication-bg`.
- **Buttons and Links**: Styled using Bootstrap button classes and custom classes for additional effects.

---

This documentation provides an in-depth look at the `Register.js` component, detailing its functionality, structure, and integration within the larger application ecosystem. 🎉

## 📄 Documentation for `Recoverpw.js`

This documentation provides a detailed explanation of the `Recoverpw.js` file, which is a React component used to implement the password recovery feature in a web application. This component is part of a larger user authentication system, typically employed in applications that require user login functionality.

---

### 📜 Table of Contents
1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Key Features](#key-features)
4. [Code Explanation](#code-explanation)
5. [Props](#props)
6. [External Dependencies](#external-dependencies)

---

### 🖥️ Overview

The `Recoverpw.js` file is a React component designed to provide users with the ability to reset their passwords. This component includes a form where users input their email addresses to receive password reset instructions. It also handles the display of success and error messages related to the password recovery process.

---

### 🏗️ Component Structure

The `Recoverpw` component is structured as a functional component using React Hooks. It leverages the `useEffect` hook to manage component lifecycle events, specifically for applying and cleaning up CSS class names related to page styling.

- **Imports**:
  - **React and Reactstrap**: For building the UI and handling form submissions.
  - **React Router**: For navigation between routes.
  - **Availity Reactstrap Validation**: For form validation.
  - **Assets**: Logo image for the application branding.

- **UI Components**:
  - **Container/Row/Col**: Used for layout structuring.
  - **Card and CardBody**: To encapsulate the form elements.
  - **Alert**: To show error and success messages.
  - **AvForm and AvField**: For creating and validating the email input form.

---

### ✨ Key Features

- **Password Reset Form**: A form that only requires the user's email to initiate the password reset process.
- **Validation**: Utilizes `availity-reactstrap-validation` for ensuring that the email input is correctly formatted.
- **Dynamic Alerts**: Displays success or error messages based on the response from the password reset request.
- **Responsive Design**: Ensures that the UI is adaptable to different screen sizes using Bootstrap's grid system.

---

### 📝 Code Explanation

```javascript
import React, { useEffect } from "react";
import { Row, Col, Alert, Container } from "reactstrap";
import { Link } from "react-router-dom";
import { AvForm, AvField } from "availity-reactstrap-validation";
import logo from "../../assets/images/logo-sm-dark.png";
```
- **Imports**: The component imports necessary modules for UI elements, form handling, and navigation.

```javascript
const Recoverpw = props => {
    useEffect(() => {
        document.body.className = "authentication-bg";
        return function cleanup() {
            document.body.className = "";
        };
    });
```
- **useEffect Hook**: Applies a background class to the body when the component is mounted and removes it on unmount.

```javascript
<AvForm className="form-horizontal">
    <div className="mb-3">
        <AvField name="email" label="Email" className="form-control" placeholder="Enter email" type="email" required />
    </div>
    <Row className="row mb-0">
        <Col className="col-12 text-end">
            <button className="btn btn-primary w-md waves-effect waves-light" type="submit"> Reset </button>
        </Col>
    </Row>
</AvForm>
```
- **Form**: Consists of a single input field for the user's email and a button to trigger the password reset process.
- **Validation**: Ensures the email field is filled out correctly before submission.

---

### 📥 Props

- **`forgetError`**: A prop that contains any error messages related to the password recovery process.
- **`forgetSuccessMsg`**: A prop that contains success messages indicating a successful password reset initiation.

---

### 📦 External Dependencies

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library for Bootstrap 4 components in React.
- **React Router**: A standard routing library for React.
- **Availity Reactstrap Validation**: A library for validating forms built with Reactstrap.

---

This component is essential for maintaining a secure and user-friendly password recovery mechanism in applications, ensuring users can regain access to their accounts in case they forget their passwords.

# Documentation for `page-confirm-mail.js` 📧

Welcome to the documentation for the `page-confirm-mail.js` file. This file is part of a React application and is responsible for rendering a confirmation mail page. This page typically informs users that a particular action related to their email has been successfully processed.

## Table of Contents 📜

1. [Overview](#overview-🔍)
2. [Components Utilized](#components-utilized-🧩)
3. [Functional Details](#functional-details-⚙️)
4. [Code Breakdown](#code-breakdown-🛠)
5. [Styling & UX](#styling--ux-🎨)
6. [Conclusion](#conclusion-✅)

## Overview 🔍

The **ConfirmMail** component serves as a simple confirmation page, displaying a success message to users. It is typically used after a successful email verification or similar operation.

## Components Utilized 🧩

This file uses several components and libraries to construct the confirmation page:

- **React**: The core library used for building the UI.
- **React Router**: Used for navigation (`Link` component).
- **Reactstrap**: A library of React components based on Bootstrap, used here for layout and styling (`Card`, `CardBody`, `Col`, `Container`, `Row`).

### Images

- **LogoDark**: A dark-themed logo for branding.
- **LogoLight**: A light-themed logo for alternative branding.

## Functional Details ⚙️

### Key Features:

- **Success Message**: Displays a success message to the user.
- **Navigation**: Provides a button to navigate back to the home/dashboard.
- **Responsive Design**: Utilizes Bootstrap's grid system for a responsive layout.

## Code Breakdown 🛠

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { Card, CardBody, Col, Container, Row } from "reactstrap";

// Import images
import logodark from "../../assets/images/logo-dark.png";
import logolight from "../../assets/images/logo-light.png";

const ConfirmMail = () => {
  return (
    <React.Fragment>
      <div className="account-pages my-5 pt-sm-5">
        <Container>
          <Row>
            <Col lg={12}>
              <div className="text-center mb-5 text-muted">
                <Link to="dashboard" className="d-block auth-logo">
                  <img src={logodark} alt="" height="20" className="auth-logo-dark mx-auto" />
                  <img src={logolight} alt="" height="20" className="auth-logo-light mx-auto" />
                </Link>
                <p className="mt-3">Responsive Bootstrap 5 Admin Dashboard</p>
              </div>
            </Col>
          </Row>
          <Row className="justify-content-center">
            <Col md={8} lg={6} xl={5}>
              <Card>
                <CardBody>
                  <div className="p-2">
                    <div className="text-center">
                      <div className="avatar-md mx-auto">
                        <div className="avatar-title rounded-circle bg-light">
                          <i className="bx bx-mail-send h1 mb-0 text-primary"></i>
                        </div>
                      </div>
                      <div className="p-2 mt-4">
                        <h4>Success!</h4>
                        <p className="text-muted">
                          At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium voluptatum deleniti atque corrupti quos dolores et
                        </p>
                        <div className="mt-4">
                          <Link to="dashboard" className="btn btn-success">Back to Home</Link>
                        </div>
                      </div>
                    </div>
                  </div>
                </CardBody>
              </Card>
              <div className="mt-5 text-center">
                <p>© {new Date().getFullYear()} Qovex. Crafted with <i className="mdi mdi-heart text-danger"></i> by Themesbrand</p>
              </div>
            </Col>
          </Row>
        </Container>
      </div>
    </React.Fragment>
  );
};

export default ConfirmMail;
```

### Breakdown:

- **Header and Logo**: Displays logos and a brief tagline.
- **Success Icon**: A circular icon indicating a successful email operation.
- **Message Section**: Contains a title "Success!" and a descriptive paragraph.
- **Navigation Button**: A button linking back to the home/dashboard.
- **Footer**: Credits and current year display.

## Styling & UX 🎨

The component uses Bootstrap's grid system for layout with Reactstrap components for easy styling. It provides a clear and concise user interface with a focus on user experience, ensuring an intuitive and responsive design.

## Conclusion ✅

The `page-confirm-mail.js` file is a straightforward and essential component for confirming email-related actions within the application. It effectively combines React and Reactstrap to deliver a responsive and user-friendly interface. This component is crucial in providing users with feedback after email confirmation processes.

# Documentation for `Login.js` 📄

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Key Features](#key-features)
4. [Code Explanation](#code-explanation)
5. [Props and State](#props-and-state)
6. [Visual Components](#visual-components)
7. [Conclusion](#conclusion)

## Introduction 🚀

The `Login.js` file is a React component designed to handle user authentication by providing a login interface. It integrates with Redux for state management and uses the `availity-reactstrap-validation` library to handle form validation. This component is an integral part of applications that require user authentication.

## Component Structure 🏗️

The `Login.js` component is organized as follows:

- **Imports**: Import necessary libraries and files.
- **Functional Component**: Define the `Login` functional component.
- **Effects**: Use `useEffect` to manage component lifecycle.
- **Event Handlers**: Define functions to handle form submissions.
- **Render Method**: Return JSX to display the login form.
- **Prop Types**: Define the expected properties using `PropTypes`.

## Key Features ✨

- **Form Validation**: Utilizes `availity-reactstrap-validation` for robust form validation.
- **Redux Integration**: Connects to Redux for state management and authentication actions.
- **Responsive Design**: Uses `reactstrap` components for a responsive UI.
- **Error Handling**: Displays error messages if authentication fails.

## Code Explanation 🧐

### Imports

```javascript
import PropTypes from "prop-types";
import React, { useEffect } from "react";
import { Row, Col, Alert, Container } from "reactstrap";
import { connect } from "react-redux";
import { withRouter, Link } from "react-router-dom";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { loginUser, apiError, socialLogin } from "../../store/actions";
import logo from "../../assets/images/logo-sm-dark.png";
```

- **Libraries**: Imports React, PropTypes, and other libraries for component functionality.
- **Assets**: Imports the logo image for branding.

### Component Definition

```javascript
const Login = (props) => {
  useEffect(() => {
    document.body.className = "authentication-bg";
    return function cleanup() {
      document.body.className = "";
    };
  });
```

- **useEffect**: Sets a background class for styling when the component mounts and cleans up on unmount.

### Form Submission

```javascript
const handleValidSubmit = (event, values) => {
  props.loginUser(values, props.history);
};
```

- **handleValidSubmit**: Submits the form values to the `loginUser` action for authentication processing.

### Render Method

```jsx
return (
  <React.Fragment>
    <div className="home-btn d-none d-sm-block">
      <Link to="/" className="text-dark">
        <i className="fas fa-home h2" />
      </Link>
    </div>
    <div className="account-pages my-5 pt-sm-5">
      <Container>
        <Row className="justify-content-center">
          <Col md={8} lg={6} xl={5}>
            <div className="card overflow-hidden">
              <div className="bg-login text-center">
                <div className="bg-login-overlay"></div>
                <div className="position-relative">
                  <h5 className="text-white font-size-20">Welcome Back !</h5>
                  <p className="text-white-50 mb-0">Sign in to continue to Qovex.</p>
                  <Link to="/" className="logo logo-admin mt-4">
                    <img src={logo} alt="" height="30" />
                  </Link>
                </div>
              </div>
              <div className="card-body pt-5">
                <div className="p-2">
                  <AvForm
                    className="form-horizontal"
                    onValidSubmit={(e, v) => {
                      handleValidSubmit(e, v);
                    }}
                  >
                    {props.error && typeof props.error === "string" ? (
                      <Alert color="danger">{props.error}</Alert>
                    ) : null}
                    <div className="mb-3">
                      <AvField
                        name="email"
                        label="Email"
                        value="admin@themesbrand.com"
                        className="form-control"
                        placeholder="Enter email"
                        type="email"
                        required
                      />
                    </div>
                    <div className="mb-3">
                      <AvField
                        name="password"
                        label="Password"
                        value="123456"
                        type="password"
                        required
                        placeholder="Enter Password"
                      />
                      <img src={`assets/images/no-eye.svg`} />
                    </div>
                    <div className="form-check">
                      <input type="checkbox" className="form-check-input" id="customControlInline" />
                      <label className="form-check-label" htmlFor="customControlInline">
                        Remember me
                      </label>
                    </div>
                    <div className="mt-3">
                      <button className="btn btn-primary w-100 waves-effect waves-light" type="submit">
                        Log In
                      </button>
                    </div>
                    <div className="mt-4 text-center">
                      <Link to="/page-recoverpw" className="text-muted">
                        <i className="mdi mdi-lock me-1"></i> Forgot your password?
                      </Link>
                    </div>
                  </AvForm>
                </div>
              </div>
            </div>
            <div className="mt-5 text-center">
              <p>
                Don't have an account ?{" "}
                <Link to="/pages-register" className="fw-medium text-primary">
                  {" "}
                  Signup now{" "}
                </Link>{" "}
              </p>
              <p>
                © {new Date().getFullYear()} Qovex. Crafted with{" "}
                <i className="mdi mdi-heart text-danger"></i> by Themesbrand
              </p>
            </div>
          </Col>
        </Row>
      </Container>
    </div>
  </React.Fragment>
);
```

- **Form Components**: Uses `AvForm` and `AvField` for form creation and validation.
- **Alerts**: Displays error messages if there are issues with login.
- **Links**: Provides navigation to other parts of the application.

### Redux Connection

```javascript
const mapStateToProps = (state) => {
  const { error } = state.Login;
  return { error };
};

export default withRouter(connect(mapStateToProps, { loginUser, apiError, socialLogin })(Login));
```

- **mapStateToProps**: Maps Redux state to component props for error handling.
- **connect**: Connects the component to Redux actions and state.

### Prop Types

```javascript
Login.propTypes = {
  error: PropTypes.any,
  history: PropTypes.object,
  loginUser: PropTypes.func,
  socialLogin: PropTypes.func,
};
```

- **PropTypes**: Ensures the correct types of props are passed to the component.

## Props and State 🌟

- **Props**: 
  - `error`: Error message for failed login attempts.
  - `history`: React Router history object for navigation.
  - `loginUser`: Function to dispatch the login action.
  - `socialLogin`: Function to handle social logins (not utilized in this component).

## Visual Components 🎨

- **Logo**: Displays the application logo.
- **Form**: Email and Password fields with validation.
- **Buttons**: Login button and navigation links.

## Conclusion 🎉

The `Login.js` component is a comprehensive solution for handling user authentication in a React application. By utilizing Redux, it efficiently manages states and actions related to user login, while providing a clean and responsive user interface with `reactstrap` components and `availity-reactstrap-validation` for form management. This component is essential for applications that require secure user access and navigation.

# 📄 Auth Lock Screen Documentation

Welcome to the documentation of the **auth-lock-screen.js** file! This file is part of a React application and manages the lock screen component functionality. Below, you'll find a detailed breakdown of its structure, purpose, and the various elements used in the code.

## Index
1. [Overview](#overview)
2. [Imports](#imports)
3. [Component: LockScreen](#component-lockscreen)
4. [Return Structure](#return-structure)
5. [Styling and Layout](#styling-and-layout)
6. [External Resources](#external-resources)
7. [License and Credits](#license-and-credits)

---

## Overview
The **auth-lock-screen.js** file implements a React functional component named `LockScreen`. This component provides a UI interface for users to unlock their screen by entering their password. It's typically used in applications for security purposes when a session is inactive for a certain period of time.

## Imports
The component utilizes several libraries and assets, which are imported at the beginning of the file:

- **React**: The core library for building the UI.
- **Availity Reactstrap Validation**: Provides form validation tools (`AvForm`, `AvField`).
- **React Router DOM**: For navigation (`Link`).
- **Reactstrap**: For styling and layout components (`Container`, `Row`, `Col`, `CardBody`, `Card`, `Button`).
- **Images**: Logo and avatar images from the asset directory.

```javascript
import React from "react";
import { AvForm, AvField } from "availity-reactstrap-validation";
import { Link } from "react-router-dom";
import { Container, Row, Col, CardBody, Card, Button } from "reactstrap";
import logo from "../../assets/images/logo-sm-dark.png";
import avatar1 from "../../assets/images/users/avatar-1.jpg";
```

## Component: LockScreen
The `LockScreen` component is a simple functional component that returns a JSX structure. It doesn't maintain any state or lifecycle methods, making it lightweight and straightforward.

### Key Features:
- **Lock Screen Interface**: Prompts the user to re-enter their password.
- **User Information**: Displays a user avatar and name.
- **Navigation Links**: Allows users to return home or navigate to the sign-in page.

## Return Structure
The component returns a complex JSX structure, structured as follows:

- **Home Button**: A link to return to the homepage.
- **Account Pages Container**: The main content area for the lock screen.
- **Card Component**: Contains the lock screen form.
- **Form Elements**: Password input field and unlock button.
- **Footer Navigation**: Additional links for navigation.

```jsx
const LockScreen = () => {
  return (
    <React.Fragment>
      <div className="home-btn d-none d-sm-block">
        <Link to="/" className="text-dark">
          <i className="fas fa-home h2" />
        </Link>
      </div>
      ...
    </React.Fragment>
  );
};
```

## Styling and Layout
The styling is heavily reliant on CSS classes provided by Bootstrap and custom styling:

- **Responsive Design**: Uses Bootstrap's grid system (`Container`, `Row`, `Col`) for layout.
- **Cards and Form**: Utilizes `Card` and `AvForm` components for a structured design.
- **Typography**: Enhanced with Bootstrap classes to ensure readability and aesthetics.

## External Resources
- **Images**: Logo and avatar are used to personalize the experience.
- **Icons**: Font Awesome and Material Design icons for visual cues.

## License and Credits
The component includes a footer crediting **Themesbrand** for crafting the theme, indicating its use in a themed application.

```jsx
<p> © {new Date().getFullYear()} Qovex. Crafted with{" "}
  <i className="mdi mdi-heart text-danger" /> by Themesbrand </p>
```

---

Thank you for exploring the documentation for the **auth-lock-screen.js** file. This lock screen component offers a secure and visually appealing way to manage user sessions. If you have any questions or need further clarification, feel free to reach out! 😊