# FormXeditable.js Documentation

Welcome to the documentation for the **FormXeditable.js** component! This file is a part of a larger React application and is responsible for rendering a form with editable fields using the `react-bootstrap-editable` library. Below you will find detailed information about the structure and functionality of this component.

## Table of Contents
1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Dependencies](#dependencies)
4. [Usage](#usage)
5. [Code Explanation](#code-explanation)
6. [Editable Field Types](#editable-field-types)
7. [Conclusion](#conclusion)

## Introduction
FormXeditable.js is designed to create a form with inline editable elements. This functionality is particularly useful for applications that require dynamic data entry or editing directly within the user interface. The component leverages the **react-bootstrap-editable** library to provide a seamless and interactive user experience.

## Component Overview
- **Component Name**: FormXeditable
- **Library Used**: `react-bootstrap-editable`
- **Functionality**: Provides inline editable form fields that can be used to capture user input or edit existing data.

## Dependencies
Before you can use the FormXeditable component, ensure that the following dependencies are installed in your project:

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: Bootstrap 4 components for React.
- **react-bootstrap-editable**: A library that allows inline editing of form elements.

## Usage
To use the FormXeditable component, simply import it into your desired React component or page and include it within your JSX as follows:

```jsx
import FormXeditable from './path-to/FormXeditable';

const SomeComponent = () => (
  <div>
    <FormXeditable />
  </div>
);
```

## Code Explanation

### Imports
```javascript
import React from "react";
import { Table, Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import Editable from "react-bootstrap-editable";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

- **React**: Core library for building the component.
- **reactstrap**: Used for layout and styling.
- **Editable**: The main library for inline editing.
- **Breadcrumbs**: Navigation component for displaying the current page hierarchy.

### Component Structure
```javascript
const FormXeditable = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Form" breadcrumbItem="Form Xeditable" />
        <Row>
          <Col>
            <Card>
              <CardBody>
                <CardTitle className="h4">Inline Example</CardTitle>
                <p className="card-title-desc">
                  This library allows you to create editable elements on your page...
                </p>
                <div className="table-responsive">
                  <Table responsive striped className="table-nowrap mb-0">
                    <thead>
                      <tr>
                        <th style={{ width: "50%" }}>Inline</th>
                        <th>Examples</th>
                      </tr>
                    </thead>
                    <tbody>
                      {/* Editable Fields */}
                    </tbody>
                  </Table>
                </div>
              </CardBody>
            </Card>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
};

export default FormXeditable;
```

- **Breadcrumbs**: Displays the navigation path.
- **Table**: Displays different types of inline editable fields.

## Editable Field Types
The component demonstrates multiple types of editable fields using `Editable` from `react-bootstrap-editable`:

1. **Simple Text Field**: A basic text input.
2. **Empty Text Field, Required**: A text input that must be filled.
3. **Select with Local Array**: A dropdown selection with predefined options.
4. **Combodate**: A date picker input.
5. **Textarea with Special Submission**: A textarea that submits on `ctrl+enter`.

Each editable field can be customized in terms of behavior and appearance to fit the application's requirements.

## Conclusion
The **FormXeditable.js** component is a versatile and powerful tool for creating interactive forms with editable fields directly within the browser. It allows for a more dynamic and responsive user experience by integrating inline editing capabilities into your React application. Feel free to explore and customize the component to fit your project's needs!

# Documentation for `WizardFormThirdPage.js`

The `WizardFormThirdPage.js` file is a React component that renders the third page of a multi-step form, specifically for collecting bank details. This component is part of a wizard form process, often used for guided user input, where users complete a series of steps in a specific order.

## Table of Contents

1. [Component Overview](#component-overview)
2. [Props](#props)
3. [Form Structure](#form-structure)
4. [Validation](#validation)
5. [Navigation](#navigation)
6. [Code Explanation](#code-explanation)
7. [Usage](#usage)

## Component Overview

The `WizardFormThirdPage` component is designed to collect bank details from the user, including information such as the name on the card, credit card type, card number, verification number, and expiration date. It utilizes `redux-form` for managing form state and validation.

## Props

The component expects the following props:

- **handleSubmit**: A function to handle the form submission. This is provided by `redux-form`.
- **previousPage**: A function to navigate to the previous page in the form wizard.

## Form Structure

The form is divided into sections, each responsible for collecting specific pieces of information related to the user's bank details:

- **Name on Card**: Text input for the name as it appears on the card.
- **Credit Card Type**: Dropdown selection for the type of credit card.
- **Credit Card Number**: Text input for the card number.
- **Card Verification Number**: Text input for the CVV/CVC.
- **Expiration Date**: Text input for the expiration date.

## Validation

The form uses a validation function imported from `validate.js` to ensure that all fields are properly filled out before allowing the user to proceed. Validation checks include ensuring fields are not empty and that inputs conform to expected formats.

## Navigation

The component includes navigation buttons:

- **Previous**: Allows users to navigate back to the previous step of the form.
- **Next**: Proceeds to the next step after successful validation.

## Code Explanation

```javascript
import PropTypes from 'prop-types'
import React from "react"
import { reduxForm } from "redux-form"
import validate from "./validate"
import { Row, Col } from "reactstrap"

const WizardFormThirdPage = props => {
  const { handleSubmit, previousPage } = props
  return (
    <form onSubmit={handleSubmit}>
      <h6 className="text-muted">Bank Details</h6>
      <fieldset>
        <Row>
          <Col md={6}>
            <div className="form-group row">
              <label htmlFor="txtNameCard" className="col-lg-3 col-form-label"> Name on Card </label>
              <Col lg={9}>
                <input id="txtNameCard" name="txtNameCard" type="text" className="form-control" />
              </Col>
            </div>
          </Col>
          <Col md={6}>
            <div className="form-group row">
              <label htmlFor="ddlCreditCardType" className="col-lg-3 col-form-label"> Credit Card Type </label>
              <Col lg={9}>
                <select id="ddlCreditCardType" name="ddlCreditCardType" className="form-control">
                  <option value="">--Please Select--</option>
                  <option value="AE">American Express</option>
                  <option value="VI">Visa</option>
                  <option value="MC">MasterCard</option>
                  <option value="DI">Discover</option>
                </select>
              </Col>
            </div>
          </Col>
        </Row>
        <Row>
          <Col md={6}>
            <div className="form-group row">
              <label htmlFor="txtCreditCardNumber" className="col-lg-3 col-form-label"> Credit Card Number </label>
              <Col lg={9}>
                <input id="txtCreditCardNumber" name="txtCreditCardNumber" type="text" className="form-control" />
              </Col>
            </div>
          </Col>
          <Col md={6}>
            <div className="form-group row">
              <label htmlFor="txtCardVerificationNumber" className="col-lg-3 col-form-label"> Card Verification Number </label>
              <Col lg={9}>
                <input id="txtCardVerificationNumber" name="txtCardVerificationNumber" type="text" className="form-control" />
              </Col>
            </div>
          </Col>
        </Row>
        <Row>
          <Col md={6}>
            <div className="form-group row">
              <label htmlFor="txtExpirationDate" className="col-lg-3 col-form-label"> Expiration Date </label>
              <Col lg={9}>
                <input id="txtExpirationDate" name="txtExpirationDate" type="text" className="form-control" />
              </Col>
            </div>
          </Col>
        </Row>
      </fieldset>
      <div id="btn_div" className="float-right">
        <button type="button" className="btn btn-primary previous" onClick={previousPage}>
          {" "} Previous{" "}
        </button>{" "}
        &nbsp;
        <button type="submit" className="btn btn-primary next">
          {" "} Next{" "}
        </button>
      </div>
    </form>
  )
}

WizardFormThirdPage.propTypes = {
  handleSubmit: PropTypes.func,
  previousPage: PropTypes.func
}

export default reduxForm({
  form: "wizard", //Form name is same
  destroyOnUnmount: false,
  forceUnregisterOnUnmount: true, // <------ unregister fields on unmount
  validate,
})(WizardFormThirdPage)
```

## Usage

To use the `WizardFormThirdPage` component, it must be included as part of a redux-form workflow, typically within a larger wizard form setup. It should be combined with other pages in the wizard and integrated using the `redux-form` library to manage form state and validation. This component is designed to be simple to integrate into a step-by-step form process where user's input is captured across multiple pages.

### Example Integration

```jsx
import WizardFormThirdPage from './WizardFormThirdPage';

// In your main component
<WizardFormThirdPage
  handleSubmit={mySubmitFunction}
  previousPage={goToPreviousPage}
/>
```

This setup ensures a seamless flow between different form pages, allowing for a comprehensive data collection process in a structured manner.

# Documentation for `FormWizard.js`

## Overview

The `FormWizard.js` file is a React component that implements a multi-step form wizard using the `reactstrap` library. The wizard is designed to navigate through several tabs, each representing a form step. This component is part of a larger application and provides a user-friendly way to enter information in stages, making it easier to manage and review before final submission.

## Key Features

- **Multi-step Form Wizard**: The component divides the form into multiple steps or tabs, each containing different form fields.
- **Navigation Control**: Users can navigate between the steps using "Previous" and "Next" buttons.
- **Breadcrumb Integration**: Uses a `Breadcrumbs` component to show the current position within the form process.
- **Responsive Design**: Utilizes responsive layout components from `reactstrap` to ensure the form adapts to different screen sizes.

## Component Structure

### State Management

- **`activeTab`**: A state variable initialized to `1` that tracks the currently active tab in the form wizard.

### Methods

- **`toggleTab(tab)`**: A function to switch between tabs. It checks if the requested tab number is valid and updates the `activeTab` state.

### UI Elements

- **Breadcrumbs**: Displays the current form context, enhancing user navigation.
- **Tab Navigation**: Each tab corresponds to a step in the form wizard:
  - **Tab 1: Seller Details**: Collects basic seller information such as contact person, mobile number, and more.
  - **Tab 2: Company Document**: Gathers company-related documents like PAN Card and VAT/TIN No.
  - **Tab 3: Bank Details**: Captures financial details including credit card information.
  - **Tab 4: Confirm Detail**: Provides a confirmation page before final submission.

### Code Breakdown

```javascript
import React, { useState } from "react";
import { Card, CardBody, Col, Form, Input, NavItem, NavLink, Row, TabContent, TabPane } from "reactstrap";
import classnames from "classnames";
import { Link } from "react-router-dom";
import Breadcrumbs from "../../components/Common/Breadcrumb";

const FormWizard = () => {
  const [activeTab, setactiveTab] = useState(1);

  function toggleTab(tab) {
    if (activeTab !== tab) {
      if (tab >= 1 && tab <= 4) {
        setactiveTab(tab);
      }
    }
  }

  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Forms" breadcrumbItem="Form Wizard" />
        <Row>
          <Col lg="12">
            <Card>
              <CardBody>
                <h4 className="card-title">Jquery Steps Wizard</h4>
                <p className="card-title-desc">A powerful jQuery wizard plugin that supports accessibility and HTML5</p>
                <div className="form-wizard-wrapper wizard clearfix">
                  <div className="steps clearfix">
                    <ul>
                      <NavItem className={classnames({ current: activeTab === 1 })}>
                        <NavLink className={classnames({ current: activeTab === 1 })} onClick={() => { setactiveTab(1) }}>
                          <span className="number">1.</span> Seller Details
                        </NavLink>
                      </NavItem>
                      <NavItem className={classnames({ current: activeTab === 2 })}>
                        <NavLink className={classnames({ active: activeTab === 2 })} onClick={() => { setactiveTab(2) }}>
                          <span className="number">2.</span> Company Document
                        </NavLink>
                      </NavItem>
                      <NavItem className={classnames({ current: activeTab === 3 })}>
                        <NavLink className={classnames({ active: activeTab === 3 })} onClick={() => { setactiveTab(3) }}>
                          <span className="number">3.</span> Bank Details
                        </NavLink>
                      </NavItem>
                      <NavItem className={classnames({ current: activeTab === 4 })}>
                        <NavLink className={classnames({ active: activeTab === 4 })} onClick={() => { setactiveTab(4) }}>
                          <span className="number">4.</span> Confirm Detail
                        </NavLink>
                      </NavItem>
                    </ul>
                  </div>
                  <div className="content clearfix">
                    <TabContent activeTab={activeTab} className="body">
                      <TabPane tabId={1}>
                        {/* Form for Seller Details */}
                      </TabPane>
                      <TabPane tabId={2}>
                        {/* Form for Company Document */}
                      </TabPane>
                      <TabPane tabId={3}>
                        {/* Form for Bank Details */}
                      </TabPane>
                      <TabPane tabId={4}>
                        {/* Confirmation Page */}
                      </TabPane>
                    </TabContent>
                  </div>
                  <div className="actions clearfix">
                    <ul>
                      <li className={activeTab === 1 ? "previous disabled" : "previous"}>
                        <Link to="#" className="btn btn-primary" onClick={() => { toggleTab(activeTab - 1) }}> Previous </Link>
                      </li>
                      <li className={activeTab === 4 ? "next disabled" : "next"}>
                        <Link to="#" className="btn btn-primary" onClick={() => { toggleTab(activeTab + 1) }}> Next </Link>
                      </li>
                    </ul>
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

export default FormWizard;
```

## Usage

To use the `FormWizard` component, simply import it into your desired React component and render it. Ensure that you have the necessary styles and dependencies from `reactstrap` and `classnames` installed.

## Conclusion

The `FormWizard.js` component offers a structured approach to form submission with its step-by-step process. The use of `reactstrap` components ensures a sleek, responsive design, while the integration of a breadcrumb component aids users in navigation. This wizard-style form is particularly beneficial for lengthy forms that require user input in multiple stages.

# Documentation for WizardFormFourPage.js

The `WizardFormFourPage.js` file represents the fourth page in a multi-step form wizard using the `redux-form` library. This page is primarily focused on confirming user details and asking for agreement with terms and conditions before completing the form submission. Below is a detailed explanation of its structure and functionality.

## Table of Contents
- [Overview](#overview)
- [Components Used](#components-used)
- [Code Explanation](#code-explanation)
- [Props](#props)
- [Form Structure](#form-structure)
- [Form Handling](#form-handling)

## Overview

The `WizardFormFourPage` component is a React functional component integrated with `redux-form` to handle form state management. It includes a simple checkbox for agreeing to terms and conditions, and navigation buttons to move between different steps of the form.

## Components Used

- **React**: A JavaScript library for building user interfaces.
- **redux-form**: A library used for managing form state in Redux.
- **PropTypes**: A library for type-checking of props passed to components.

## Code Explanation

Here's a breakdown of the code structure and functionality:

### Import Statements

```javascript
import PropTypes from 'prop-types'
import React from "react"
import { reduxForm } from "redux-form"
import validate from "./validate"
```

- **PropTypes**: Used to validate the props passed to the component.
- **reduxForm**: Connects the form component to Redux.
- **validate**: An imported function used to validate the form inputs.

### WizardFormFourPage Component

```javascript
const WizardFormFourPage = props => {
  const { handleSubmit, previousPage } = props
  return (
    <form onSubmit={handleSubmit}>
      ...
    </form>
  )
}
```

- The component receives `handleSubmit` and `previousPage` as props, which are used to handle form submission and navigation respectively.

### Props

The component expects the following props:
- **handleSubmit**: A function that is called when the form is submitted.
- **previousPage**: A function to navigate back to the previous page in the wizard.

### Form Structure

```javascript
<form onSubmit={handleSubmit}>
  <h6 className="text-muted">Confirm Detail</h6>
  <fieldset>
    <div className="p-3">
      <div className="custom-control custom-checkbox">
        <input type="checkbox" className="custom-control-input" id="customCheck1" />
        <label className="custom-control-label" htmlFor="customCheck1">
          I agree with the Terms and Conditions.
        </label>
      </div>
    </div>
  </fieldset>
  <div id="btn_div" className="float-right">
    <button type="button" className="btn btn-primary previous" onClick={previousPage}>
      Previous
    </button>
    &nbsp;
    <button type="submit" className="btn btn-primary next">Finish</button>
  </div>
</form>
```

- The form includes a checkbox input for the user to agree to terms and conditions.
- It contains two buttons:
  - **Previous**: Navigates to the previous page in the wizard using the `previousPage` function.
  - **Finish**: Submits the form using the `handleSubmit` function.

### Form Handling

The form is connected to Redux using the `reduxForm` HOC:

```javascript
export default reduxForm({
  form: "wizard", // Form name is same
  destroyOnUnmount: false,
  forceUnregisterOnUnmount: true, // Unregister fields on unmount
  validate,
})(WizardFormFourPage)
```

- **form**: The form is named "wizard" to maintain consistency across the wizard steps.
- **destroyOnUnmount**: Set to `false` to preserve form data between navigations.
- **forceUnregisterOnUnmount**: Unregister fields when unmounted for better form state management.
- **validate**: The validate function ensures the form's data meets specified requirements.

This component is designed to be the final confirmation page in a multi-step form wizard, ensuring the user agrees to terms before proceeding.

# Documentation for `WizardFormSecondPage.js`

The `WizardFormSecondPage.js` file is a React component that provides the second step in a multi-step form wizard using Redux Form. It collects company document details and allows navigation between the previous and next steps of the form.

## Table of Contents
- [Overview](#overview)
- [Component Structure](#component-structure)
- [Props](#props)
- [Form Fields](#form-fields)
- [Navigation Controls](#navigation-controls)
- [Validation](#validation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)

## Overview
The `WizardFormSecondPage` component is designed to be used as the second page in a form wizard where users input various company document details. It relies on `redux-form` for state management and validation. This component is part of a multi-step form and allows transitioning between pages while maintaining the form state.

## Component Structure
```jsx
import PropTypes from 'prop-types';
import React from "react";
import { reduxForm } from "redux-form";
import validate from "./validate";
import { Row, Col } from "reactstrap";

const WizardFormSecondPage = props => {
  // ...
}

WizardFormSecondPage.propTypes = {
  handleSubmit: PropTypes.func,
  previousPage: PropTypes.func
}

export default reduxForm({
  form: "wizard",
  destroyOnUnmount: false,
  forceUnregisterOnUnmount: true,
  validate,
})(WizardFormSecondPage);
```

## Props
- **handleSubmit (function):** A function to handle the form submission for this page.
- **previousPage (function):** A function to navigate back to the previous page in the form wizard.

## Form Fields
The form includes the following fields related to company documents:
- **PAN Card**
- **VAT/TIN No.**
- **CST No.**
- **Service Tax No.**
- **Company UIN**
- **Declaration**

Each field is encapsulated within a `<Row>` and `<Col>` layout using Bootstrap's grid system for responsive design.

## Navigation Controls
- **Previous Button:** Navigates to the previous form page. This button uses the `previousPage` prop to trigger navigation.
- **Next Button:** Submits the form data for this step and moves to the next step. This button triggers the `handleSubmit` function passed via props.

## Validation
The form uses a validation function imported from `./validate` to ensure that all required fields are filled out correctly. This function is applied through `redux-form` to provide feedback and ensure data integrity.

## Usage
This component is wrapped in `reduxForm` to connect it to the Redux state and handle form validation. It should be used within a wizard flow where each step corresponds to a page in the form.

### Example Usage
```jsx
<WizardFormSecondPage
  handleSubmit={this.handleSubmitSecondPage}
  previousPage={this.navigateToFirstPage}
/>
```

## Code Explanation
- **Imports and Dependencies:** The component imports necessary React, Redux Form, and Reactstrap components. The `validate` function is also imported for form validation.
  
- **Component Definition:** `WizardFormSecondPage` is a functional component that receives `handleSubmit` and `previousPage` as props. It returns a form with various input fields for company document details.
  
- **Form Layout:** Utilizes `Row` and `Col` from Reactstrap for a responsive grid layout. Each form group is organized in a structured manner.
  
- **PropTypes:** The component uses `PropTypes` to enforce type checking for `handleSubmit` and `previousPage`.

- **Redux Form Integration:** The component is wrapped in `reduxForm`, linking it to the "wizard" form name, ensuring that the form's data persists across page transitions.

This documentation provides a comprehensive overview of the `WizardFormSecondPage.js` file, explaining its purpose, structure, and usage within a form wizard.

# Documentation for `WizardFormFirstPage.js` 🚀

This documentation provides a detailed explanation of the `WizardFormFirstPage.js` file, which is a part of a multi-step form wizard implemented using React and Redux Form. The form focuses on collecting seller details. Below, you'll find a breakdown of the file's components, their purpose, and how they work together.

## Table of Contents 📚

1. [Overview](#overview)
2. [Components](#components)
3. [Form Fields](#form-fields)
4. [Form Submission](#form-submission)
5. [Redux Form Integration](#redux-form-integration)
6. [Code Walkthrough](#code-walkthrough)

## Overview

The `WizardFormFirstPage.js` file contains a React component that represents the first page of a wizard form. This form collects seller information such as contact details, addresses, and product categories. The component leverages `redux-form` for form state management and validation.

## Components

- **`WizardFormFirstPage`**: The main React functional component that renders the form fields and controls the form submission process.

- **`reduxForm`**: A higher-order component from `redux-form` that binds the form component to the Redux store.

- **`validate`**: A validation function imported from another module, used to ensure the form fields meet certain criteria.

## Form Fields

The form includes several input fields structured in rows and columns using `reactstrap` components. The fields include:

- **Contact Person**: Input for entering the contact person's name.
- **Mobile No.**: Input for entering the mobile number.
- **Landline No.**: Input for entering the landline number.
- **Email Address**: Input for entering the email address.
- **Address 1**: Textarea for entering the primary address.
- **Warehouse Address**: Textarea for entering the warehouse address.
- **Company Type**: Input for entering the type of the company.
- **Live Market A/C**: Input for entering live market account details.
- **Product Category**: Input for entering the product category.
- **Product Sub Category**: Input for entering the product sub-category.

## Form Submission

The form submission is handled by the `handleSubmit` method passed as a prop to the component. This method is typically provided by the `redux-form` library to handle form submissions in a consistent manner.

## Redux Form Integration

The `WizardFormFirstPage` component is wrapped with the `reduxForm` higher-order component. This setup allows the form to communicate with the Redux store, enabling state management and validation. Key settings include:

- **`form`**: Specifies the form name as "wizard".
- **`destroyOnUnmount`**: Set to `false`, ensuring form data is not destroyed when unmounted.
- **`forceUnregisterOnUnmount`**: Set to `true`, unregisters fields when the component is unmounted.
- **`validate`**: Specifies the validation function to be used for form validation.

## Code Walkthrough

Below is a code walkthrough highlighting the key parts of the `WizardFormFirstPage.js` file:

```javascript
import React from "react";
import { reduxForm } from "redux-form";
import validate from "./validate";
import { Col, Row } from "reactstrap";

const WizardFormFirstPage = (props) => {
  const { handleSubmit } = props; // Destructure handleSubmit from props

  return (
    <form onSubmit={handleSubmit}> {/* Form submission handled by handleSubmit */}
      <h6 className="text-muted">Seller Details</h6>
      <fieldset> {/* Fieldset for form organization */}
        <Row> {/* Row for layout using Reactstrap */}
          <Col md={6}> {/* First column */}
            <Row className="form-group">
              <label htmlFor="txtFirstNameBilling" className="col-lg-3 col-form-label">
                Contact Person
              </label>
              <Col lg={9}>
                <input id="txtFirstNameBilling" name="txtFirstNameBilling" type="text" className="form-control" />
              </Col>
            </Row>
          </Col>
          <Col md={6}> {/* Second column */}
            <Row className="form-group">
              <label htmlFor="txtLastNameBilling" className="col-lg-3 col-form-label">
                Mobile No.
              </label>
              <Col lg={9}>
                <input id="txtLastNameBilling" name="txtLastNameBilling" type="text" className="form-control" />
              </Col>
            </Row>
          </Col>
        </Row>
        {/* Additional Rows and Columns for other form fields */}
      </fieldset>
      <div id="btn_div" className="float-right"> {/* Buttons for navigation */}
        <button type="button" className="btn btn-primary previous" disabled style={{ cursor: "no-drop" }}>
          Previous
        </button>
        &nbsp;
        <button type="submit" className="btn btn-primary next">
          Next
        </button>
      </div>
    </form>
  );
};

export default reduxForm({
  form: "wizard", // Form name
  destroyOnUnmount: false, // Preserve form data
  forceUnregisterOnUnmount: true, // Unregister fields
  validate, // Validation function
})(WizardFormFirstPage);
```

This component sets the groundwork for collecting seller details in a structured, step-by-step manner. The combination of `redux-form` and `reactstrap` ensures a robust and responsive form experience.

# Documentation for `validate.js` 📄

The `validate.js` file is a utility module designed to perform validation on form input values. It checks for the presence and correctness of specific fields and returns any errors found. This is commonly used in form validation processes within React applications, especially when using form libraries like Redux Form. Below is a detailed breakdown of its functionality and usage.

## Overview

The primary function in this file is `validate`, which accepts an object representing form values and returns an object containing any validation errors encountered.

## Function: `validate`

### **Purpose**

The `validate` function is responsible for ensuring that the form data adheres to certain validation rules, thereby ensuring that the user inputs are correct and complete.

### **Signature**

```javascript
const validate = values => { ... }
```

- **Parameters**: 
  - `values`: An object that contains the form field values keyed by field names.

- **Returns**: 
  - An object that contains any validation errors, keyed by the field names.

### **Validation Rules**

The function applies the following rules to its input:

1. **First Name Validation**:
   - Checks if `firstName` is provided.
   - **Error Message**: `"Required"`

2. **Last Name Validation**:
   - Checks if `lastName` is provided.
   - **Error Message**: `"Required"`

3. **Email Validation**:
   - Checks if `email` is provided.
   - Checks if `email` matches a standard email address pattern using a regular expression.
   - **Error Messages**:
     - If not provided: `"Required"`
     - If invalid format: `"Invalid email address"`

4. **Sex Validation**:
   - Checks if `sex` is provided.
   - **Error Message**: `"Required"`

5. **Favorite Color Validation**:
   - Checks if `favoriteColor` is provided.
   - **Error Message**: `"Required"`

### **Regular Expression Used**

For email validation, the function uses the following regular expression:

```regex
/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i
```

- This regex ensures that the email contains valid characters, an "@" symbol, a domain name, and a domain suffix of 2 to 4 characters.

### **Example Usage**

Below is a sample usage of the `validate` function in a form context:

```javascript
import validate from './validate';

const formValues = {
  firstName: 'John',
  lastName: '',
  email: 'john.doe@example.com',
  sex: 'male',
  favoriteColor: ''
};

const errors = validate(formValues);

console.log(errors);
// Output: { lastName: 'Required', favoriteColor: 'Required' }
```

### **Export**

The `validate` function is exported as the default export of the module.

```javascript
export default validate;
```

## Summary

The `validate.js` file provides a straightforward and efficient method for validating form data. By identifying missing or incorrectly formatted fields, it plays a crucial role in ensuring data integrity before submission. This utility is particularly useful when integrated into form management libraries, providing an easy way to enforce validation rules across different components.

# Documentation for `renderField.js`

## Overview

The `renderField.js` file contains a functional React component called `renderField`. This component is designed to render a form field with a label, input, and error message (if any). It is typically used in form handling to display individual form fields dynamically, including validation feedback.

## Table of Contents

1. [Component Structure](#component-structure)
2. [Props](#props)
3. [Usage](#usage)
4. [Example](#example)
5. [Styling and Customization](#styling-and-customization)

---

## Component Structure

The `renderField` component is a **functional component** that takes in props and returns a structured HTML element. Here's the basic JSX structure:

```jsx
const renderField = ({ input, label, type, meta: { touched, error } }) => (
  <div>
    <label>{label}</label>
    <div>
      <input {...input} placeholder={label} type={type} />
      {touched && error && <span>{error}</span>}
    </div>
  </div>
);
```

- **Label**: Displays the label for the input field.
- **Input**: The main input element where users can enter data. It uses the spread operator to receive multiple input-related properties.
- **Error Handling**: Displays an error message below the input if the field has been touched and an error exists.

## Props

The `renderField` component expects the following props:

| Prop Name | Type   | Description                                       |
|-----------|--------|---------------------------------------------------|
| `input`   | Object | Contains the properties necessary for the input element, typically provided by form libraries. |
| `label`   | String | The text label for the input field.               |
| `type`    | String | Specifies the type of input (e.g., text, number). |
| `meta`    | Object | Contains metadata for the field, such as `touched` and `error`. |

### Meta Object

- **touched**: A boolean indicating whether the input field has been interacted with.
- **error**: A string containing the error message to be displayed if validation fails.

## Usage

The `renderField` component is often used in conjunction with form libraries like Redux Form or React Final Form, which handle the state and validation of form inputs. The component can be included in a form to render various input fields dynamically based on the props provided.

## Example

Here is an example of how you might use the `renderField` component within a form:

```jsx
import React from 'react';
import { Field, reduxForm } from 'redux-form';
import renderField from './renderField';

const MyForm = () => (
  <form>
    <Field
      name="username"
      type="text"
      component={renderField}
      label="Username"
    />
    <Field
      name="email"
      type="email"
      component={renderField}
      label="Email"
    />
    <button type="submit">Submit</button>
  </form>
);

export default reduxForm({ form: 'myForm' })(MyForm);
```

In this example, the `Field` component from `redux-form` is used to wrap the `renderField` component, passing necessary props such as `name`, `type`, and `label`.

## Styling and Customization

While the `renderField` component provides basic functionality, you can enhance its styling and behavior:

- **CSS Styling**: Apply custom CSS classes to the label, input, and error span for better UI/UX.
- **Validation Logic**: Extend validation logic to handle different scenarios and error types.
- **Accessibility**: Ensure that labels are properly associated with inputs for screen readers.

The `renderField` component is a versatile tool in building dynamic and responsive forms in React applications, providing a clean and efficient way to render form fields with validation.

# 📚 SettingMenu.js Documentation

## Overview
The `SettingMenu.js` file contains a **React Component** named `SettingMenu`, which renders a settings dropdown menu using the `reactstrap` library. This component provides a user interface element that can be used to display various settings or actions in a dropdown format.

## Table of Contents
1. [Component Structure](#component-structure)
2. [Key Imports](#key-imports)
3. [State Management](#state-management)
4. [Render Method](#render-method)
5. [Styling and Classes](#styling-and-classes)
6. [Usage Example](#usage-example)
7. [Conclusion](#conclusion)

## Component Structure

### SettingMenu Class
```jsx
class SettingMenu extends Component {
  constructor(props) {
    super(props);
    this.state = {};
  }

  render() {
    return (
      <React.Fragment>
        {/* Dropdown component */}
      </React.Fragment>
    );
  }
}

export default SettingMenu;
```
The component is a **class-based** React component that uses internal state to manage the dropdown's open/close status.

## Key Imports
- `React, { Component }`: Core React library and Component class for creating React components.
- `{ Dropdown, DropdownToggle, DropdownMenu, DropdownItem }`: Components from the `reactstrap` library that provide a Bootstrap-styled dropdown menu.

## State Management

The component manages a piece of state called `setting_menu`, which determines whether the dropdown menu is open or closed. This is toggled using React's `setState` method.

### Initial State
```javascript
this.state = {
  setting_menu: false
};
```

### State Toggle
```javascript
toggle={() => this.setState({ setting_menu: !this.state.setting_menu })}
```
The `toggle` function inverts the current state of `setting_menu`, allowing the dropdown to open and close when clicked.

## Render Method

The `render` method returns JSX that renders a dropdown menu. Here's a breakdown of the JSX:

### Dropdown Component
```jsx
<Dropdown isOpen={this.state.setting_menu} toggle={this.toggle}>
  <DropdownToggle color="primary" className="arrow-none waves-effect waves-light">
    <i className="mdi mdi-settings ms-2"/> Settings
  </DropdownToggle>
  <DropdownMenu className="language-switch" right>
    <DropdownItem tag="a" href="#"> Action </DropdownItem>
    <DropdownItem tag="a" href="#"> Another action </DropdownItem>
    <DropdownItem tag="a" href="#"> Something else here </DropdownItem>
    <div className="dropdown-divider"/>
    <DropdownItem tag="a" href="#"> Separated link </DropdownItem>
  </DropdownMenu>
</Dropdown>
```

### Elements Explained
- **Dropdown**: Main container for the dropdown menu.
- **DropdownToggle**: Button that toggles the dropdown menu. It uses FontAwesome icons and Bootstrap classes for styling.
- **DropdownMenu**: Container for the dropdown items.
- **DropdownItem**: Individual items in the dropdown menu, each of which can have an action or link associated with it.
- **Dropdown Divider**: A horizontal line to separate groups of items.

## Styling and Classes
The component uses Bootstrap classes provided by `reactstrap` for styling. The classes ensure the dropdown is styled according to Bootstrap's design system.

## Usage Example
To use this component, simply import it into your desired file and include it in your JSX.

```jsx
import SettingMenu from './SettingMenu';

function App() {
  return (
    <div className="App">
      <SettingMenu />
    </div>
  );
}

export default App;
```

## Conclusion
The `SettingMenu.js` component provides a clean and simple way to implement a settings dropdown in a React application using `reactstrap`. It demonstrates the use of class-based components, state management, and Bootstrap styling in React.

Feel free to extend the functionality by adding more dropdown items or custom actions as needed. Happy coding! 🚀

# Documentation for `FormValidations.js` 📜

## Overview

The `FormValidations.js` file is a React component designed to demonstrate and handle various form validation techniques using the `availity-reactstrap-validation` library. This component showcases both normal and tooltip-based validation feedback for form inputs. It's part of a form handling interface that provides feedback directly to users, ensuring data integrity and improving user experience.

## Table of Contents

1. [Setup and Imports](#setup-and-imports)
2. [State Management](#state-management)
3. [Validation Functions](#validation-functions)
4. [Component Rendering](#component-rendering)
   - [React Validation](#react-validation)
   - [Bootstrap Validation with Tooltips](#bootstrap-validation-with-tooltips)
   - [Validation Type Examples](#validation-type-examples)
   - [Range Validation](#range-validation)
5. [Conclusion](#conclusion)

## Setup and Imports

The component relies on several imports:

```javascript
import React, { useState } from "react";
import { Row, Col, Card, CardBody, FormGroup, Button, CardTitle, CardSubtitle, Label, Input } from "reactstrap";
import { AvForm, AvField } from "availity-reactstrap-validation";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

- **React**: For building UI components.
- **reactstrap**: For using Bootstrap components in React.
- **availity-reactstrap-validation**: For form validation using Bootstrap styles.
- **Breadcrumbs**: A custom component for displaying navigation breadcrumbs.

## State Management

The component uses React's `useState` hook to manage validation states for various form fields:

```javascript
const [fnm, setfnm] = useState(false);
const [lnm, setlnm] = useState(false);
const [unm, setunm] = useState(false);
const [city, setcity] = useState(false);
const [stateV, setstateV] = useState(false);
```

Each state variable corresponds to a form field, indicating whether the input is valid (`true`) or invalid (`false`).

## Validation Functions

### `handleSubmit`

This function handles the form submission, checking whether each form field is filled out correctly and updating the state accordingly:

```javascript
function handleSubmit(e) {
    e.preventDefault();
    var fnm = document.getElementById("validationTooltip01").value;
    var lnm = document.getElementById("validationTooltip02").value;
    var unm = document.getElementById("validationTooltipUsername").value;
    var city = document.getElementById("validationTooltip03").value;
    var stateV = document.getElementById("validationTooltip04").value;

    setfnm(fnm !== "");
    setlnm(lnm !== "");
    setunm(unm !== "");
    setcity(city !== "");
    setstateV(stateV !== "");

    var d1 = document.getElementsByName("validate");
    document.getElementById("tooltipForm").classList.add("was-validated");
    for (var i = 0; i < d1.length; i++) {
        d1[i].style.display = "block";
    }
}
```

### `changeHandeler`

This function handles changes in input fields, toggling the display of validation tooltips:

```javascript
function changeHandeler(event, eleId) {
    document.getElementById(eleId).style.display = event.target.value !== "" ? "none" : "block";
}
```

## Component Rendering

### React Validation

Displays a form using `AvForm` and `AvField` for standard validation:

```jsx
<AvForm className="needs-validation">
    <Row>
        <Col md="6">
            <div className="mb-3">
                <Label htmlFor="validationCustom01">First name</Label>
                <AvField
                    name="firstname"
                    placeholder="First name"
                    type="text"
                    errorMessage="Enter First Name"
                    className="form-control"
                    validate={{ required: { value: true } }}
                    id="validationCustom01"
                />
            </div>
        </Col>
        {/* More fields here */}
    </Row>
</AvForm>
```

### Bootstrap Validation with Tooltips

Utilizes Bootstrap's tooltip classes to display validation messages:

```jsx
<form className="needs-validation" id="tooltipForm" onSubmit={e => handleSubmit(e)}>
    <Row>
        <Col md="4">
            <div className="mb-3 position-relative">
                <Label htmlFor="validationTooltip01">First name</Label>
                <Input
                    type="text"
                    className="form-control"
                    id="validationTooltip01"
                    placeholder="First name"
                    onChange={event => changeHandeler(event, "validate1")}
                />
                <div className={fnm ? "valid-tooltip" : "invalid-tooltip"} id="validate1">
                    {fnm ? "Looks good!" : "Please Enter Valid First Name"}
                </div>
            </div>
        </Col>
        {/* More fields here */}
    </Row>
</form>
```

### Validation Type Examples

Demonstrates various validation types including required fields, equal-to, email, digits, and more:

```jsx
<AvForm>
    <AvField
        name="username"
        label="Required"
        placeholder="Type Something"
        type="text"
        errorMessage="Enter Name"
        validate={{ required: { value: true } }}
    />
    {/* More validation examples */}
</AvForm>
```

### Range Validation

Utilizes `AvField` to validate inputs based on length and value ranges:

```jsx
<AvForm>
    <AvField
        name="Min_Length"
        label="Min Length"
        placeholder="Min 6 chars"
        type="number"
        errorMessage="Min 6 chars."
        validate={{ required: { value: true }, minLength: { value: 6, errorMessage: "Min 6 chars." } }}
    />
    {/* More range validations */}
</AvForm>
```

## Conclusion

The `FormValidations.js` component is a comprehensive example of implementing form validations in a React application. It leverages the `availity-reactstrap-validation` library to enforce data integrity and provide user feedback. By using both standard and tooltip feedback mechanisms, it ensures that users receive clear and immediate responses to their input, enhancing the overall user experience.

# FormUpload.js Documentation

Welcome to the documentation for the **FormUpload.js** file. This file is a React component designed to handle file uploads using a drag-and-drop interface. The component utilizes the `react-dropzone` library to provide an intuitive user experience for file uploads with image previews.

## Table of Contents

1. [Overview](#overview)
2. [Components and Libraries](#components-and-libraries)
3. [State Management](#state-management)
4. [Functions](#functions)
    - [handleAcceptedFiles](#handleAcceptedFiles)
    - [formatBytes](#formatBytes)
5. [Render Method](#render-method)
6. [Styling and Layout](#styling-and-layout)
7. [Usage](#usage)
8. [License](#license)

## Overview

The **FormUpload.js** component allows users to upload files by dragging and dropping them into a designated area or by clicking to select files. The component displays previews of the uploaded images and the size of each file in a readable format.

## Components and Libraries

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library providing Bootstrap 4 components for React.
- **React-Dropzone**: A library for creating drag-and-drop file upload components.
- **React Router**: Used for navigation between pages.
- **Breadcrumbs**: A custom component for displaying breadcrumb navigation.

## State Management

The component uses React's `useState` hook to manage the following state:

- `selectedFiles`: An array that holds the files selected by the user. Each file object includes a preview URL and a formatted size.

## Functions

### handleAcceptedFiles

```javascript
function handleAcceptedFiles(files) {
  files.map(file =>
    Object.assign(file, {
      preview: URL.createObjectURL(file),
      formattedSize: formatBytes(file.size),
    })
  );
  setselectedFiles(files);
}
```

- **Purpose**: Processes the files accepted by the dropzone, adding a preview URL and formatted size to each file.
- **Parameters**: `files` - An array of files selected by the user.
- **Returns**: Updates the `selectedFiles` state.

### formatBytes

```javascript
function formatBytes(bytes, decimals = 2) {
  if (bytes === 0) return "0 Bytes";
  const k = 1024;
  const dm = decimals < 0 ? 0 : decimals;
  const sizes = ["Bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB"];
  const i = Math.floor(Math.log(bytes) / Math.log(k));
  return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + " " + sizes[i];
}
```

- **Purpose**: Converts a file size in bytes to a human-readable string.
- **Parameters**: 
  - `bytes`: The size of the file in bytes.
  - `decimals`: The number of decimal places to include in the formatted size.
- **Returns**: A formatted string representing the file size.

## Render Method

The `render` method returns a JSX fragment that includes:

- A breadcrumb navigation for easy navigation.
- A card displaying the dropzone for file uploads.
- An area for displaying file previews.
- A button to send the uploaded files.

## Styling and Layout

- **Reactstrap** is used for layout and styling, providing a responsive grid system and components like `Card`, `Row`, `Col`, and `Button`.
- **Dropzone** provides the UI for file uploads, with a customizable drop area.

## Usage

To use this component, ensure you have `react-dropzone`, `reactstrap`, and `react-router-dom` installed in your project. Then, import and include the `FormUpload` component where needed.

```javascript
import FormUpload from './FormUpload';
```

```jsx
<FormUpload />
```

## License

This component is part of a larger project and is subject to the terms and conditions provided in the project's license.

---

Feel free to reach out if you have any questions or need further assistance with the **FormUpload.js** component! 😊

# FormMask.js Documentation

## Overview
The `FormMask.js` file is a React component that provides an example of using input masks in a form. Input masks are used to format user input into a specified pattern, which can be useful for ensuring data consistency, especially for specific data types like phone numbers, dates, and ISBNs.

## Table of Contents
1. [Usage](#usage)
2. [Components](#components)
3. [Input Masks](#input-masks)
4. [Dependencies](#dependencies)
5. [Code Explanation](#code-explanation)

## Usage
This component is part of a larger application and is used to demonstrate the implementation of input masks using `react-input-mask` and `@material-ui/core/Input`.

### Example
```jsx
<FormMask />
```

## Components
- **ISBN1, ISBN2, ISBN3:** Input masks for different ISBN formats.
- **IPV4:** Input mask for IPv4 addresses.
- **IPV6:** Input mask for IPv6 addresses.
- **TAX:** Input mask for Tax ID numbers.
- **Phone:** Input mask for phone numbers.
- **Currency:** Input mask for currency format.
- **Date1, Date2:** Input masks for date formats.

## Input Masks
| Mask       | Description                      | Example               |
|------------|----------------------------------|-----------------------|
| ISBN1      | ISBN format with dashes          | `999-99-999-9999-9`   |
| ISBN2      | ISBN format with spaces          | `999 99 999 9999 9`   |
| ISBN3      | ISBN format with slashes         | `999/99/999/9999/9`   |
| IPV4       | IPv4 address format              | `192.168.0.1`         |
| IPV6       | IPv6 address format              | `****:****:****:*:...`|
| TAX        | Tax ID format                    | `99-9999999`          |
| Phone      | Standard US phone number format  | `(999) 999-9999`      |
| Currency   | Currency format                  | `$ 999,999,999.99`    |
| Date1      | Date format with slashes         | `dd/mm/yyyy`          |
| Date2      | Date format with dashes          | `dd-mm-yyyy`          |

## Dependencies
- **react-input-mask:** Library to create input masks.
- **@material-ui/core/Input:** Material UI component for input fields.

## Code Explanation

### `ISBN1` Component
```jsx
const ISBN1 = props => (
  <InputMask mask="999-99-999-9999-99-9" value={props.value} className="form-control input-color" onChange={props.onChange}>
    {inputProps => (
      <MaterialInput {...inputProps} type="tel" disableUnderline />
    )}
  </InputMask>
)
```
This component uses `react-input-mask` to apply a mask to the input field, formatting input as an ISBN with dashes.

### `Currency` Component
```jsx
const Currency = props => (
  <InputMask mask="$ 999,999,999.99" value={props.value} className="form-control input-color" onChange={props.onChange}>
    {inputProps => (
      <MaterialInput {...inputProps} prefix="$" type="tel" disableUnderline />
    )}
  </InputMask>
)
```
The `Currency` component formats input as a currency value, including a dollar sign and commas for thousands.

### Rendering
The component is rendered within a `Card` containing a form with multiple input fields, each demonstrating a different input mask. The layout is managed using `reactstrap` components such as `Row`, `Col`, and `Form`.

## Conclusion
The `FormMask.js` component is a practical implementation of input masks, allowing users to input data in specific formats easily. It demonstrates versatility in handling different types of input, ensuring data consistency and ease of use in form fields.

# Documentation for `FormRepeater.js`

Welcome to the documentation for the `FormRepeater.js` file! This file is a part of a React application that deals with dynamic form fields, allowing users to add or remove fields as needed. This is particularly useful for forms where the number of inputs is not fixed.

## Table of Contents

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [Functionality](#functionality)
5. [Usage](#usage)
6. [Code Explanation](#code-explanation)

---

## Introduction

`FormRepeater.js` provides functionality for creating dynamic forms with repeatable sections. It includes features for both simple and nested repeatable elements, making it versatile for various form requirements.

## Dependencies

This file relies on the following imports to function correctly:

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap Components**: Various UI components such as `Row`, `Col`, `Card`, `CardBody`, etc., from the `reactstrap` library for layout and styling.
- **Breadcrumbs**: A custom component for navigation breadcrumbs.

## Component Structure

The main component in the file is `FormRepeater`, a functional component that uses React hooks for state management.

```jsx
const FormRepeater = () => {
  const [rows1, setrows1] = useState([]);
  const [rows2, setrows2] = useState([]);
  ...
  return (
    <React.Fragment>
      ...
    </React.Fragment>
  );
};
```

## Functionality

### State Management

- **rows1**: Manages the state of the nested phone number fields.
- **rows2**: Manages the state of the main form fields.

### Adding and Removing Rows

- **handleAddRowNested**: Adds a new entry to the `rows1` state, allowing the user to input an additional phone number.
- **handleAddRowNested1**: Adds a new entry to the `rows2` state, allowing the user to input another set of form details.

### Delete Button

Each form row has a delete button that removes the respective entry when clicked.

## Usage

To use this component, include it in a React application where dynamic form fields are needed. The component can be customized by altering the form fields or the styles according to the application's requirements.

## Code Explanation

### Key Sections

1. **Form Initialization**: Initially, the form is empty with predefined fields ready for user interaction.
2. **Dynamic Field Management**: Utilizing state arrays `rows1` and `rows2` to dynamically render input fields based on user action.
3. **Nested Form Structure**: Separate sections for main and nested forms, allowing complex form setups.

### Example Code

Here's a snippet showcasing how rows are added dynamically:

```jsx
function handleAddRowNested() {
  const item1 = { name1: "" };
  setrows1([...rows1, item1]);
}
```

This function appends a new item to the `rows1` array, which subsequently triggers a re-render to display the new input field.

### Rendering

The component renders a form with both simple repeatable fields and nested fields. The layout is constructed using `reactstrap` components, ensuring a responsive and styled user interface.

```jsx
<Form className="repeater" encType="multipart/form-data">
  ...
  <Button onClick={() => { handleAddRowNested1() }} color="success">
    Add
  </Button>
</Form>
```

## Conclusion

The `FormRepeater.js` file is designed to facilitate the creation of dynamic and repeatable form elements within a React application. By leveraging React hooks and the `reactstrap` library, it provides a flexible and user-friendly interface for managing complex form requirements.

# Documentation for `FormEditors.js` 📄

## Overview
The `FormEditors.js` file is a React component that provides a user interface for a rich text editor using the `react-draft-wysiwyg` library. This component is part of a larger form-related module and is designed to integrate with the rest of the application seamlessly. The editor allows users to input and format text in a WYSIWYG (What You See Is What You Get) manner, which is similar to a traditional word processor.

## Table of Contents
1. [File Import Dependencies](#file-import-dependencies)
2. [Component Structure](#component-structure)
3. [Editor Features](#editor-features)
4. [Usage](#usage)
5. [Customization and Styling](#customization-and-styling)
6. [Conclusion](#conclusion)

---

## 1. File Import Dependencies
The file imports several dependencies which are crucial for its functionality:

- **React**: The core library for building user interfaces in a declarative manner.
- **reactstrap**: Provides Bootstrap-based React components for building responsive layouts.
- **react-draft-wysiwyg**: A popular library for implementing WYSIWYG editors in React applications.
- **Breadcrumbs**: A custom component used for navigation within the application.

```javascript
import React from "react";
import { Form, Card, CardBody, Col, Row, CardTitle, CardSubtitle } from "reactstrap";
import { Editor } from "react-draft-wysiwyg";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

## 2. Component Structure
The `FormEditors` component is structured using React functional components and JSX. It utilizes Bootstrap classes for styling and layout.

```jsx
const FormEditors = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Form" breadcrumbItem="Form Editors" />
        <Row>
          <Col>
            <Card>
              <CardBody>
                <CardTitle>react-draft-wysiwyg</CardTitle>
                <CardSubtitle className="mb-3">
                  Bootstrap-wysihtml5 is a javascript plugin that makes it easy to create simple, beautiful wysiwyg editors with the help of wysihtml5 and Twitter Bootstrap.
                </CardSubtitle>
                <Form method="post">
                  <Editor
                    toolbarClassName="toolbarClassName"
                    wrapperClassName="wrapperClassName"
                    editorClassName="editorClassName"
                  />
                </Form>
              </CardBody>
            </Card>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
}
```

## 3. Editor Features
- **Toolbar**: The editor comes with a rich toolbar that allows users to format text (bold, italic, underline), insert links, images, lists, etc.
- **Responsive Design**: The editor adapts to different screen sizes using Bootstrap's grid system.
- **Customizable**: The editor's appearance and functionality can be customized via props and CSS classes.

## 4. Usage
To use the `FormEditors` component, simply import it and include it in your JSX. It can be embedded within any form or used standalone.

```jsx
import FormEditors from './FormEditors';

function App() {
  return (
    <div>
      <FormEditors />
    </div>
  );
}
```

## 5. Customization and Styling
The `react-draft-wysiwyg` editor allows for significant customization:
- **CSS Classes**: Customize the `toolbarClassName`, `wrapperClassName`, and `editorClassName` to style each part of the editor.
- **Editor Configuration**: Adjust settings such as available toolbar options, default content, and more via props.

### Example CSS Customization
```css
.toolbarClassName {
  background-color: #f1f1f1;
}

.wrapperClassName {
  border: 1px solid #ccc;
  padding: 10px;
}

.editorClassName {
  min-height: 300px;
  border: 1px solid #ddd;
  padding: 5px;
}
```

## 6. Conclusion
The `FormEditors.js` file provides a user-friendly and customizable WYSIWYG editor component for React applications. By leveraging the `react-draft-wysiwyg` library, developers can empower users with a rich text editing experience that integrates smoothly with the rest of the application. Whether you're building a blog platform, a CMS, or any application requiring text input, this component is a valuable asset.

---

**Note**: For further customization and feature extension, refer to the [react-draft-wysiwyg documentation](https://jpuri.github.io/react-draft-wysiwyg/#/) and the [reactstrap documentation](https://reactstrap.github.io/).

# 📄 FormLayouts.js Documentation

Welcome to the documentation for the **FormLayouts.js** file! This file is a React component that showcases various form layout styles using Bootstrap's grid and form components. The file is part of a larger setup where different form elements and layouts are demonstrated.

## 📑 Table of Contents

1. [Overview](#overview)
2. [Imports](#imports)
3. [Component: FormLayouts](#component-formlayouts)
   - [Form Grid Layout](#form-grid-layout)
   - [Horizontal Form Layout](#horizontal-form-layout)
   - [Auto Sizing](#auto-sizing)
   - [Inline Forms](#inline-forms)
   - [Floating Labels](#floating-labels)
4. [Conclusion](#conclusion)

## 🔍 Overview

The **FormLayouts.js** file provides various examples of form layouts using the Bootstrap framework. It demonstrates how forms can be styled using grid layouts, horizontal layouts, inline forms, and more. This file is useful for developers looking to understand how to structure forms in a responsive and visually appealing manner using React and Bootstrap.

## 📥 Imports

The file imports several components from React and Reactstrap, a popular Bootstrap component library for React, along with a breadcrumb component for navigation.

```javascript
import React from "react";
import { Card, Col, Container, Row, CardBody, CardTitle, Label, Button, Form, Input, InputGroup } from "reactstrap";
// Import Breadcrumb
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

## 🧩 Component: FormLayouts

The **FormLayouts** component is the main export of this file. It is a React functional component that renders various form layouts within a container. Here's a breakdown of the different sections within the component:

### 📐 Form Grid Layout

- **Description**: Displays a form using a grid layout with responsive columns.
- **Usage**: Demonstrates how to use Bootstrap's grid system to create a responsive form layout with fields for first name, email, password, city, state, and zip code.

```javascript
<Form>
  <div className="mb-3">
    <Label for="formrow-firstname-Input">First name</Label>
    <Input type="text" className="form-control" id="formrow-firstname-Input" />
  </div>
  <Row>
    <Col md={6}>
      <div className="mb-3">
        <Label for="formrow-email-Input">Email</Label>
        <Input type="email" className="form-control" id="formrow-email-Input" />
      </div>
    </Col>
    ...
  </Row>
  <button type="submit" className="btn btn-primary w-md">Submit</button>
</Form>
```

### ↔️ Horizontal Form Layout

- **Description**: Renders a form in a horizontal layout, aligning labels and inputs side by side.
- **Usage**: Useful for situations where space is limited horizontally, such as in sidebars or narrow screens.

```javascript
<Form>
  <div className="row mb-4">
    <Label for="horizontal-firstname-Input" className="col-sm-3 col-form-Label">First name</Label>
    <Col sm={9}>
      <Input type="text" className="form-control" id="horizontal-firstname-Input" />
    </Col>
  </div>
  ...
  <Button type="submit" color="primary" className="w-md">Submit</Button>
</Form>
```

### 🔄 Auto Sizing

- **Description**: Demonstrates how to create forms that automatically adjust to content size.
- **Usage**: Ideal for forms with dynamic content or when using inputs with varying lengths.

```javascript
<Form className="row gy-2 gx-3 align-items-center">
  <div className="col-sm-auto">
    <Label className="visually-hidden" for="autoSizingInput">Name</Label>
    <Input type="text" className="form-control" id="autoSizingInput" placeholder="Jane Doe" />
  </div>
  ...
  <button type="submit" className="btn btn-primary w-md">Submit</button>
</Form>
```

### 🆎 Inline Forms

- **Description**: Displays a form in a single line, useful for simple search or login bars.
- **Usage**: Compact form layout, often used in navigation bars or headers.

```javascript
<Form className="row row-cols-lg-auto g-3 align-items-center">
  <Col xs={12}>
    <label className="visually-hidden" for="inlineFormInputGroupUsername">Username</label>
    <InputGroup>
      <div className="input-group-text">@</div>
      <input type="text" className="form-control" id="inlineFormInputGroupUsername" placeholder="Username" />
    </InputGroup>
  </Col>
  ...
  <button type="submit" className="btn btn-primary w-md">Submit</button>
</Form>
```

### 🏷️ Floating Labels

- **Description**: Uses floating labels that sit on top of the input fields, providing a modern aesthetic.
- **Usage**: Enhances UX by clearly indicating which field is active or filled.

```javascript
<Form>
  <div className="form-floating mb-3">
    <input type="text" className="form-control" id="floatingnameInput" placeholder="Enter Name" value="Maria Laird" />
    <label for="floatingnameInput">Name</label>
  </div>
  ...
  <button type="submit" className="btn btn-primary w-md">Submit</button>
</Form>
```

## 🏁 Conclusion

The **FormLayouts.js** file is a comprehensive example of how to implement various form layouts using React and Bootstrap. It covers grid layouts, horizontal forms, auto-sizing, inline forms, and floating labels, providing developers with a robust set of examples to create responsive and user-friendly forms. Each layout serves a specific purpose and can be adapted to fit different UI requirements.

# Documentation for `BasicElements.js` 📜

## Overview
The `BasicElements.js` file is a React component designed to showcase a variety of basic form elements using Bootstrap's styling. This file primarily demonstrates different types of input fields, select options, checkboxes, radio buttons, switches, and file inputs. It's a comprehensive example of how to utilize Bootstrap's form controls in a React application.

## Table of Contents
1. [File Imports](#file-imports)
2. [Component Structure](#component-structure)
3. [Form Elements](#form-elements)
    - [Textual Inputs](#textual-inputs)
    - [Sizing Inputs](#sizing-inputs)
    - [Range Inputs](#range-inputs)
    - [Checkboxes](#checkboxes)
    - [Radios](#radios)
    - [Switches](#switches)
    - [File Browser](#file-browser)
4. [State Management](#state-management)
5. [Usage](#usage)

## File Imports
The file imports several components and libraries which are essential for creating the form elements and styling:
```javascript
import React, { useState } from "react";
import { Card, CardBody, Col, Row, CardTitle, Label, Input } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```
- **React**: Core library for building the component.
- **reactstrap**: Provides Bootstrap components as React components.
- **Breadcrumbs**: A custom component for displaying navigational breadcrumbs.

## Component Structure
The `BasicElements` component is structured as a functional component utilizing React hooks (`useState`) for managing local state. The component returns a React fragment which encompasses the entire UI layout, including breadcrumbs and a variety of form elements.

## Form Elements

### Textual Inputs
These are basic input fields for text, search, email, URL, telephone, password, number, date, time, etc., each demonstrating the use of Bootstrap's `.form-control` class.
```jsx
<Row className="mb-3">
  <label htmlFor="example-text-input" className="col-md-2 col-form-label">Text</label>
  <div className="col-md-10">
    <input className="form-control" type="text" defaultValue="Artisanal kale" />
  </div>
</Row>
```

### Sizing Inputs
Different input sizes are demonstrated, including default, small, and large input fields.
```jsx
<div className="mb-3">
  <Label className="form-label">Form Control sm</Label>
  <input className="form-control form-control-sm" type="text" placeholder=".form-control-sm" />
</div>
```

### Range Inputs
Custom range inputs are shown with different configurations for min, max, and steps.
```jsx
<Label for="customRange1" className="form-label">Example range</Label>
<Input type="range" className="form-range" id="customRange1" />
```

### Checkboxes
Demonstrates default and right-aligned checkboxes with checked and unchecked states.
```jsx
<div className="form-check mb-2">
  <input className="form-check-input" type="checkbox" value="" id="defaultCheck1" />
  <label className="form-check-label" htmlFor="defaultCheck1">Default Checkbox</label>
</div>
```

### Radios
Radio buttons are presented with both left and right alignment.
```jsx
<div className="form-check mb-2">
  <input className="form-check-input" type="radio" name="exampleRadios" id="exampleRadios1" value="option1" defaultChecked />
  <label className="form-check-label" htmlFor="exampleRadios1">Default Radio</label>
</div>
```

### Switches
Switches are implemented as toggle switches using custom checkboxes styled with Bootstrap.
```jsx
<div className="form-check form-switch" dir="ltr">
  <input type="checkbox" className="form-check-input" id="customSwitch2" defaultChecked onClick={e => { settoggleSwitch(!toggleSwitch) }} />
  <label className="form-check-label" htmlFor="customSwitch2">Checked switch checkbox input</label>
</div>
```

### File Browser
A simple file input is provided with Bootstrap styling.
```jsx
<div className="input-group">
  <Input type="file" className="form-control" id="inputGroupFile02" />
  <Label className="input-group-text" for="inputGroupFile02">Upload</Label>
</div>
```

## State Management
The component uses `useState` hooks to manage the state of checkboxes and toggle switches:
- `customchk` and `toggleSwitch` are used to manage the states of checkboxes and switches.
- State is updated using functions like `setcustomchk` and `settoggleSwitch`.

## Usage
To use this component, simply import `BasicElements` into your desired React file and include it within your JSX. Make sure to have `reactstrap` and any required stylesheets imported into your project for proper styling.

```javascript
import BasicElements from './path/to/BasicElements';

function App() {
  return (
    <div className="App">
      <BasicElements />
    </div>
  );
}
```

## Conclusion
The `BasicElements.js` file is a well-structured component demonstrating various form controls using Bootstrap in a React environment. It serves as a useful reference for implementing similar form elements in other parts of an application.

# Documentation for `BasicElements.js` 📄

Welcome to the comprehensive documentation for the **`BasicElements.js`** file. This file forms a core part of the user interface, providing a variety of basic form elements for a React application using Bootstrap-styled components from `reactstrap`.

## Table of Contents 📚

1. [Overview](#overview)
2. [Imports](#imports)
3. [Component State](#component-state)
4. [Component Structure](#component-structure)
5. [Form Elements](#form-elements)
6. [Usage](#usage)
7. [Conclusion](#conclusion)

## Overview

The **`BasicElements`** component is a React functional component that provides a comprehensive set of **form elements**. These elements include text inputs, checkboxes, radio buttons, switches, and file inputs, each styled with Bootstrap classes for a consistent look and feel. This component is intended to be a versatile building block for developing form-based interfaces.

## Imports

```javascript
import React, { useState } from "react"
import { Card, CardBody, Col, Row, CardTitle, Label, Input } from "reactstrap"
// Import Breadcrumb
import Breadcrumbs from "../../components/Common/Breadcrumb"
```

- **React** and **useState Hook**: For building the component and managing state.
- **`reactstrap` Components**: Utilizes `Card`, `CardBody`, `Col`, `Row`, `CardTitle`, `Label`, and `Input` from `reactstrap` to structure and style the component.
- **Breadcrumbs**: Imported to provide navigational aid within the application.

## Component State

The component uses the `useState` Hook to manage two pieces of state:

- **`customchk`**: A boolean state for managing the checked state of a custom checkbox.
- **`toggleSwitch`**: A boolean state for managing the state of a toggle switch.

```javascript
const [customchk, setcustomchk] = useState(true)
const [toggleSwitch, settoggleSwitch] = useState(true)
```

## Component Structure

The `BasicElements` component is structured into several sections, each wrapped in a `Card`. Each card contains different types of form elements with descriptive titles and examples.

## Form Elements

### Textual Inputs

- **Text**, **Search**, **Email**, **URL**, **Telephone**, **Password**, **Number**
- **Date and Time**, **Date**, **Month**, **Week**, **Time**, **Color**

Each input type is demonstrated with a default value to illustrate its functionality.

### Select and Datalists

- **Select**: A dropdown selection.
- **Datalists**: Provides suggestions while typing in the input.

### Sizing

- Demonstrates how to apply different sizes to inputs using Bootstrap classes like `.form-control-lg` and `.form-control-sm`.

### Range Inputs

- **Range Sliders**: Demonstrates basic, min-max, and stepped range inputs.

### Checkboxes and Radios

- **Checkboxes**: Demonstrates default and checked checkboxes, including right-aligned checkboxes.
- **Radios**: Showcases default and checked radio buttons, including right-aligned options.

### Switches

- Demonstrates toggle switches with a typical checked and disabled state.

### File Browser

- **File Input**: Provides a file input field for uploading files, accompanied by a label.

## Usage

To use **`BasicElements`** in your project, ensure that `reactstrap` and all necessary CSS files for Bootstrap are included in your project. Then, you can import and use the component like so:

```javascript
import BasicElements from 'path-to-BasicElements'

function App() {
  return (
    <div>
      <BasicElements />
    </div>
  )
}
```

## Conclusion

The **`BasicElements.js`** component serves as a robust example of how to implement various form elements using React and `reactstrap`. This component is well-suited for applications that need a standard set of form controls that are both functional and visually appealing.

By utilizing this component, developers can ensure that their applications have a consistent and professional form interface, ready to collect user inputs effectively.