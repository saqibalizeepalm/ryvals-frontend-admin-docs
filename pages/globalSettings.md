# Documentation for `GlobalSettings.js` 📜

The `GlobalSettings.js` file is a React component that manages the global settings for an application. This module is primarily responsible for handling the user interface and logic associated with updating and maintaining global configuration data. The component integrates with various services and libraries to provide a robust settings management system.

---

## Index 📋

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [State Management](#state-management)
4. [Effects](#effects)
5. [Functions](#functions)
6. [Rendering the Component](#rendering-the-component)
7. [Dependencies](#dependencies)
8. [Conclusion](#conclusion)

---

## Introduction

The **GlobalSettings** component is designed to allow users to view and update various global configuration settings. These settings may include parameters for referral bonuses, inactivity timelines, and other operational metrics that can be adjusted via a form interface.

---

## Imports

The component utilizes several libraries and custom modules:

```javascript
import React, { useEffect, useState } from "react";
import { Col, Row, FormGroup, Button, Label } from "reactstrap";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getGlobalSettings, setGlobalSettings } from "../../services/globalSettings_api_helper";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import { AvForm, AvField, AvInput, AvGroup } from "availity-reactstrap-validation";
import SweetAlert from "react-bootstrap-sweetalert";
import FilterPermission from "../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils";
import info from "../../assets/images/info-icon.svg";
import { MESSAGES, permissionsStrings, SUCCESS_MESSAGES } from "../../helpers/StringConstant";
```

### Key Libraries and Their Purpose

- **React and Hooks**: For building the component and managing state and lifecycle.
- **Reactstrap**: For responsive UI components.
- **Availity Reactstrap Validation**: Used for form validation.
- **React Bootstrap SweetAlert**: For confirmation dialogues.
- **Toastify**: For notifications.
- **Custom Modules**: Various helpers and services that manage permissions, API calls, and constants.

---

## State Management

The component uses hooks to manage state:

- **`globals`**: Stores the global settings fetched from the server.
- **`disableSubmit`**: A boolean to control the submit button's disabled state.
- **`loader`**: Indicates if the component is in a loading state.
- **`state`**: Holds the form data for each setting.
- **`openModal`**: Controls the visibility of the confirmation modal.
- **`values`**: Stores the form values to be submitted.
- **`changePermission`**: Manages permission-based changes.

---

## Effects

### `useEffect` Hooks

- **Initial Data Fetch**: Fetches global settings and sets permissions on component mount.
  ```javascript
  useEffect(() => {
    getGlobalListing();
    if (props.permission.length !== 0) {
      callSetPermission();
    } else {
      setChange(true);
    }
  }, []);
  ```

- **Form Change Detection**: Enables or disables the submit button based on changes in form data.
  ```javascript
  useEffect(() => {
    if (/* condition to check changes */) {
      setDisableSubmit(true);
    } else {
      setDisableSubmit(false);
    }
  }, [state, globals]);
  ```

---

## Functions

### Data Fetching and Submission Functions

- **`getGlobalListing`**: Fetches the global settings from the API and updates the state.

- **`handleValidSubmit`**: Prepares data for submission and triggers the confirmation modal.

- **`handleValidSubmit2`**: Sends updated settings to the API and provides feedback to the user.

### Helper Functions

- **`handleChange`**: Updates the state when form inputs change.

- **`openAlert`, `confirmBox`, `closeAlert`**: Manage the SweetAlert confirmation dialog state.

- **`validateInactivityRemnder`**: Custom validation for inactivity reminders.

---

## Rendering the Component

```jsx
return (
  <React.Fragment>
    <div className="page-content">
      <Breadcrumbs breadcrumbItem="GLOBAL SETTINGS" />
      <Row>
        {loader ? (
          <div class="spinner-grow spinner-class" role="status" style={{ marginTop: "40px" }}>
            <span class="sr-only">Loading...</span>
          </div>
        ) : (
          <Col className="col-12">
            <AvForm onValidSubmit={(e, v) => { handleValidSubmit(e, v); }}>
              <fieldset disabled={!changePermission}>
                {/* Form fields for each setting go here */}
                <FormGroup className="mt-4">
                  <Button type="submit" color="primary" className="ms-1" disabled={disableSubmit}>Submit</Button>
                  {openModal ? (
                    <SweetAlert
                      title="Confirmation"
                      warning
                      showCancel
                      confirmButtonText="Yes"
                      confirmBtnBsStyle="success"
                      cancelButtonText="No"
                      cancelBtnBsStyle="danger"
                      onConfirm={() => confirmBox()}
                      onCancel={() => closeAlert()}
                      focusCancelBtn
                    >
                      Are you sure you want to continue ?
                    </SweetAlert>
                  ) : null}
                </FormGroup>
              </fieldset>
            </AvForm>
          </Col>
        )}
      </Row>
    </div>
  </React.Fragment>
);
```

### Form Fields

Each form field uses `AvField` or `AvInput` to create inputs with built-in validation. They are wrapped in a `fieldset` that can be disabled based on permissions.

---

## Dependencies

### External Libraries

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: Bootstrap 4 components for React.
- **Availity Reactstrap Validation**: Provides validation for forms using Reactstrap.
- **React Bootstrap SweetAlert**: For alert dialogs with SweetAlert.
- **React Toastify**: Adds notifications to your React app.

### Custom Modules

- **Helper and Service Files**: Handle API interactions, permission filtration, and string constants.

---

## Conclusion

The `GlobalSettings.js` component is an essential part of the application's administrative interface, allowing for dynamic adjustments to global settings. By leveraging a combination of React hooks, form validation, and responsive design, it ensures users can easily manage configuration data with immediate feedback and confirmation.