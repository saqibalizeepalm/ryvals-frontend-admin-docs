# 📄 ClearButton.js Documentation

## Overview

The `ClearButton.js` file defines a React component named **`ClearButton`**. This component is designed to render a button that, when clicked, triggers a clear action. It is built using **React** and **reactstrap**, a popular library of React components that leverage Bootstrap styles.

---

## 🌟 Features

- **React Component**: The `ClearButton` is a functional component created with React, utilizing React's functional component syntax.
- **Bootstrap Styling**: The button is styled using **reactstrap**, which provides Bootstrap-themed components.
- **Event Handling**: The component accepts a function as a prop, `handleClear`, which is executed when the button is clicked.

---

## 📜 Code Explanation

```javascript
import React from "react";
import { Button } from "reactstrap";

function ClearButton({ handleClear }) {
  return (
    <Button className="new-filter" color="primary" onClick={handleClear}>
      Clear
    </Button>
  );
}

export default ClearButton;
```

### 🔍 Breakdown

1. **Imports**: 
   - `React` is imported to use JSX syntax and to define the component.
   - `{ Button }` is imported from `reactstrap` to utilize a pre-styled button component.

2. **ClearButton Component**:
   - **Function Declaration**: `ClearButton` is a functional component that accepts `props`. Here, the destructured `handleClear` function is passed as a prop.
   - **Rendering**: 
     - The `Button` component from `reactstrap` is used to create a button element.
     - **Class & Color**: The button uses `className="new-filter"` for additional styling and `color="primary"` for Bootstrap's primary color.
     - **Event Handling**: The `onClick` event is set to trigger the `handleClear` function when the button is clicked.

3. **Export**: 
   - The `ClearButton` component is exported as the default export of the module, making it available for import in other files.

---

## 🎨 Props

| Prop Name   | Type     | Description                                |
|-------------|----------|--------------------------------------------|
| `handleClear` | Function | **Required**. A function that is called when the button is clicked. |

---

## 💡 Usage Example

Below is an example of how to use the `ClearButton` component:

```jsx
import React, { useState } from 'react';
import ClearButton from './ClearButton';

function ExampleComponent() {
  const [text, setText] = useState("Some text");

  const clearText = () => {
    setText("");
  };

  return (
    <div>
      <p>{text}</p>
      <ClearButton handleClear={clearText} />
    </div>
  );
}

export default ExampleComponent;
```

### Explanation

- **State Management**: The `ExampleComponent` manages a piece of state called `text`, initialized with "Some text".
- **Clear Function**: The `clearText` function clears the `text` state by setting it to an empty string.
- **Component Usage**: The `ClearButton` component is used within the `ExampleComponent`, with the `clearText` function passed as the `handleClear` prop.

---

## 🛠️ Customization

- **Styling**: You can customize the button's appearance by modifying the `className` or directly altering the styles in your CSS.
- **Functionality**: The logic within the `handleClear` function can be tailored to suit your needs, whether it's clearing input fields, resetting states, or any other clear action.

---

## ⚙️ Dependencies

- **React**: Ensure that React is properly installed and set up in your project.
- **reactstrap**: Install `reactstrap` and its peer dependency `bootstrap` to ensure the button is styled correctly. 

```bash
npm install reactstrap bootstrap
```

Add Bootstrap's CSS in your `index.js` or `App.js` file:

```javascript
import 'bootstrap/dist/css/bootstrap.min.css';
```

---

## Conclusion

The `ClearButton` component is a simple yet effective way to incorporate a clear or reset functionality into your React applications. By leveraging the styling capabilities of `reactstrap`, it provides a visually appealing button that can be easily integrated and customized for various use cases.

# 📄 Documentation for `GoBack.jsx`

## 📚 Index
1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Dependencies](#dependencies)
4. [Props](#props)
5. [Code Breakdown](#code-breakdown)
6. [Usage Example](#usage-example)

---

## 📖 Introduction

The `GoBack.jsx` component is a simple yet effective React component used to navigate back to a previous page in a web application. It leverages React and Reactstrap libraries to provide both functionality and styling. This component is commonly used to enhance user experience by allowing easy navigation with a consistent UI design.

---

## 🛠 Component Overview

The `GoBack.jsx` component renders a **back button** that users can click to return to a specified URL. It utilizes the `reactstrap` library for layout purposes and the `react-router-dom` library for navigation.

---

## 📦 Dependencies

The component relies on the following libraries:

- **Reactstrap**: Provides responsive layout components.
- **React Router DOM**: Facilitates navigation within a React application.

---

## 📋 Props

The `GoBack` component accepts the following prop:

| Prop Name | Type   | Description                                   |
|-----------|--------|-----------------------------------------------|
| `backUrl` | String | The URL to which the user will be redirected. |

---

## 🔍 Code Breakdown

Here's a detailed explanation of the code in `GoBack.jsx`:

```javascript
import { Row, Col } from "reactstrap";
import { Link } from "react-router-dom";

export const GoBack = ({ backUrl }) => {
    return (
        <Row className="mb-4">
            <Col>
                <p>
                    <Link to={backUrl}>
                        <i className="mdi mdi-arrow-left"></i> back
                    </Link>
                </p>
            </Col>
        </Row>
    );
};
```

### Explanation:

- **Imports**:
  - **Row, Col** from `reactstrap`: These components are used to create a responsive grid layout.
  - **Link** from `react-router-dom`: This component is used to create navigational links that allow routing without a full page refresh.

- **Component Function**: `GoBack`
  - Receives a prop `backUrl` that determines where the link should redirect.
  - Returns a JSX structure containing:
    - A `Row` and `Col` from `reactstrap` to provide layout.
    - A `<Link>` component wrapping an icon and the text "back". This link navigates to the `backUrl` when clicked.
    - A Material Design Icon (`mdi mdi-arrow-left`) is used to visually indicate a back action.

---

## 💡 Usage Example

Here's an example of how you might integrate the `GoBack` component within your application:

```javascript
import React from "react";
import { GoBack } from "./GoBack";

const SomeComponent = () => {
  return (
    <div>
      <GoBack backUrl="/previous-page" />
      <h1>Welcome to Some Page</h1>
      {/* Additional content here */}
    </div>
  );
};

export default SomeComponent;
```

### Explanation:

- **Import and Use**: The `GoBack` component is imported and used by providing a `backUrl` prop, which specifies the target URL for the back navigation.
- **Integration**: It can be easily integrated into any component where a back navigation feature is needed.

---

## 🎨 Styling

The component utilizes default styles provided by Reactstrap and Material Design Icons. You may further customize the styles through CSS classes such as `mb-4` for margin adjustments.

---

This concludes the detailed documentation for the `GoBack.jsx` component. This component is part of a larger React application, serving a specific use-case for seamless navigation. Feel free to extend or modify it as per your application's requirements! 🚀

# 📄 Documentation for `IconsToolTip.jsx`

## 📋 Table of Contents
1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Component Props](#component-props)
4. [Usage Example](#usage-example)
5. [Conclusion](#conclusion)

## 🌟 Introduction
The `IconsToolTip.jsx` file defines a simple yet powerful React component that is used to display an icon with a tooltip. This component is particularly useful for providing additional information or context when users hover over an icon.

## ⚙️ Component Overview
```jsx
import React from "react";

function IconsToolTip({ image, altImageText, text }) {
  return (
    <>
      <img alt={altImageText} src={image} />
      <span className="edit-tournament-tooltip tooltiptext" data-tip data-for="loginTip">
        {text}
      </span>
    </>
  );
}

export default IconsToolTip;
```

- The component is a **functional component**.
- It uses **React** to manage the UI.
- It displays an image (`<img>`) and a tooltip (`<span>`), which appears when the user hovers over the image.

## 📜 Component Props

The `IconsToolTip` component accepts the following props:

| Prop Name     | Type   | Description                                                                 |
| ------------- | ------ | --------------------------------------------------------------------------- |
| `image`       | String | The URL of the image to be displayed as an icon.                            |
| `altImageText`| String | The alt text for the image, which improves accessibility.                   |
| `text`        | String | The text to be displayed in the tooltip when the user hovers over the icon. |

### 📝 Example Prop Usage
- **`image`**: "path/to/icon.png"
- **`altImageText`**: "Icon Description"
- **`text`**: "This is a tooltip message"

## 🚀 Usage Example

Here is how you can use the `IconsToolTip` component in a React application:

```jsx
import React from 'react';
import IconsToolTip from './IconsToolTip';

const App = () => (
  <div>
    <h1>Welcome to the Application</h1>
    <IconsToolTip 
      image="https://example.com/icon.png" 
      altImageText="Example Icon"
      text="This icon is used for demonstration purposes."
    />
  </div>
);

export default App;
```

### 🖼️ Explanation
- The `IconsToolTip` component is imported and used within another component (`App` in this case).
- It displays an image and, upon hovering, reveals a tooltip with the provided text.

## 🏁 Conclusion

The `IconsToolTip.jsx` component is a reusable piece of UI for displaying icons with tooltips. It's designed to enhance the user experience by providing additional context or information through hover interactions. By simply passing in the appropriate props, this component can be utilized in various parts of an application where icons and tooltips are needed.

### 🎨 Visual Representation
```html
<img alt="Example Icon" src="https://example.com/icon.png" />
<span className="edit-tournament-tooltip tooltiptext" data-tip data-for="loginTip">
  This icon is used for demonstration purposes.
</span>
```

This is how the component might render in a browser, showcasing its structure and functionality. With its straightforward design, `IconsToolTip` can be easily customized and extended to fit diverse application needs.

# 📄 NonAuthLayout.js Documentation

## 📚 Index

1. [Overview](#overview)
2. [Components and Imports](#components-and-imports)
3. [Class: NonAuthLayout](#class-nonauthlayout)
   - [Constructor](#constructor)
   - [Method: capitalizeFirstLetter](#method-capitalizefirstletter)
   - [Lifecycle Method: componentDidMount](#lifecycle-method-componentdidmount)
   - [Render Method](#render-method)
4. [PropTypes](#proptypes)
5. [Export](#export)
6. [Conclusion](#conclusion)

## 🌟 Overview

The `NonAuthLayout.js` file is a **React** component that serves as a layout wrapper for non-authenticated pages in a web application. This component is designed to handle the layout for pages that do not require user authentication, providing a consistent structure and functionality across such pages.

## 📦 Components and Imports

- **PropTypes**: Used for type-checking the properties passed to the component, ensuring they are of the expected type.
- **React, Component**: Base library for building user interfaces and the base class for the component.
- **withRouter**: A higher-order component from `react-router-dom` that provides access to the history object's properties and the closest `<Route>`'s match.

```javascript
import PropTypes from "prop-types";
import React, { Component } from "react";
import { withRouter } from "react-router-dom";
```

## 🏗️ Class: NonAuthLayout

### 📜 Constructor

The constructor initializes the component's state and binds class methods.

```javascript
constructor(props) {
    super(props);
    this.state = {};
    this.capitalizeFirstLetter.bind(this);
}
```

### ✂️ Method: capitalizeFirstLetter

This method takes a string and returns it with the first letter capitalized. It is presumably intended for formatting purposes, though its usage in this component is unclear.

```javascript
capitalizeFirstLetter = (string) => {
    return string.charAt(1).toUpperCase() + string.slice(2);
};
```

### ⏰ Lifecycle Method: componentDidMount

This method is invoked after the component is mounted. It sets the document title to "Ryvals", providing a custom title for the application when this layout is rendered.

```javascript
componentDidMount() {
    document.title = "Ryvals";
}
```

### 🖼️ Render Method

The render method outputs the children elements wrapped within a `React.Fragment`, ensuring that any child components passed to `NonAuthLayout` are rendered as expected.

```javascript
render() {
    return <React.Fragment>{this.props.children}</React.Fragment>;
}
```

## 📏 PropTypes

The `NonAuthLayout` component uses PropTypes to specify the types of its props, enhancing reliability and maintainability by ensuring that the expected data types are used.

```javascript
NonAuthLayout.propTypes = {
    children: PropTypes.any,
    location: PropTypes.object,
};
```

- **children**: This prop can be any type and represents the child components to be rendered within the layout.
- **location**: An object that represents the current location, typically used for routing purposes.

## 🚀 Export

The component is exported using the `withRouter` higher-order component to enable routing capabilities.

```javascript
export default withRouter(NonAuthLayout);
```

## 🔍 Conclusion

The `NonAuthLayout.js` component provides a simple yet effective layout for non-authenticated pages within a React application. By leveraging `React.Fragment` and setting the document title, it ensures a consistent user experience across different non-authenticated views. The use of `PropTypes` and `withRouter` further enhances the component's utility in managing unprotected routes in the application.

# 📄 Documentation for `Breadcrumb.js`

## 🗂 Table of Contents
1. [Overview](#overview)
2. [Component Details](#component-details)
3. [Usage](#usage)
4. [Props](#props)
5. [Code Explanation](#code-explanation)
6. [Installation & Setup](#installation--setup)

---

## Overview

The `Breadcrumb.js` file contains a **React functional component** named `Breadcrumb`. This component is designed to display a breadcrumb navigation element, which is typically used in user interfaces to indicate the current page's location within a site's hierarchy.

---

## Component Details

- **File Name**: `Breadcrumb.js`
- **Component**: `Breadcrumb`
- **Dependencies**: 
  - `React`: For building user interfaces.
  - `PropTypes`: For typechecking of props.
  - `reactstrap`: For responsive layout using `Row` and `Col`.

---

## Usage

To include the `Breadcrumb` component in your React application, you can import and use it as shown below:

```jsx
import React from 'react';
import Breadcrumb from './Breadcrumb';

function App() {
  return (
    <div>
      <Breadcrumb breadcrumbItem="Dashboard" />
    </div>
  );
}

export default App;
```

---

## Props

The `Breadcrumb` component accepts the following props:

| Prop Name      | Type   | Description                          |
|----------------|--------|--------------------------------------|
| `breadcrumbItem` | string | Represents the current page name displayed in the breadcrumb. |
| `title`         | string | (Optional) Represents the main title if needed. |

> **Note**: The `title` prop is mentioned in `PropTypes`, but it is not used within the component. This could be intentional for future enhancements or might be an oversight.

---

## Code Explanation

Here's a detailed breakdown of the `Breadcrumb` component:

```javascript
import React from "react";
import PropTypes from "prop-types";
import { Row, Col } from "reactstrap";

// Define the Breadcrumb functional component
const Breadcrumb = (props) => {
  return (
    <Row>
      <Col className="col-12">
        <div className="page-title-box d-flex align-items-start align-items-center justify-content-between">
          <h4 className="page-title mb-0 font-size-18">
            {props.breadcrumbItem}
          </h4>
        </div>
      </Col>
    </Row>
  );
};

// Define expected prop types for better documentation and debugging
Breadcrumb.propTypes = {
  breadcrumbItem: PropTypes.string,
  title: PropTypes.string,
};

// Export the Breadcrumb component as default
export default Breadcrumb;
```

- **Structure**: The component uses `Row` and `Col` from `reactstrap` to align the breadcrumb title within a responsive grid system.
- **Styling**: The component applies several Bootstrap classes for basic styling and layout (`d-flex`, `align-items-start`, etc.).
- **PropTypes**: `PropTypes` is used to specify the types of props expected by the component, aiding in development and debugging.

---

## Installation & Setup

Ensure you have the necessary packages installed:

```bash
npm install react react-dom prop-types reactstrap bootstrap
```

Include Bootstrap CSS in your project, typically in your main `index.js` or `App.js` file:

```javascript
import 'bootstrap/dist/css/bootstrap.min.css';
```

You can now use the `Breadcrumb` component in your application as described in the [Usage](#usage) section.

--- 

This documentation should provide a comprehensive understanding of the `Breadcrumb.js` file and its role in a React application. If you have further questions or need clarification, feel free to reach out! 😊

# 📄 DeleteAlertModal.jsx Documentation

## Overview

The **`DeleteAlertModal.jsx`** file is a React component that provides a user interface for a modal dialog box that prompts the user to confirm the deletion of a tournament. It uses several third-party libraries to enhance the user experience, such as `react-bootstrap-sweetalert` for the alert modal and `react-toastify` for displaying toast notifications.

## 🏗️ Component Structure

```jsx
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import PropTypes from "prop-types";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import SweetAlert from "react-bootstrap-sweetalert";
import { deleteTournament } from "../../services/bracket_tournaments_api_helper";

const DeleteAlertModal = (props) => {
  const [disableSwal2, setDisabled2] = useState(false);

  const handleDelete = async () => {
    props.Loader();
    props.onClose();
    setDisabled2(true);
    await deleteTournament(props.DeleteId)
      .then((res) => {
        toast.success("Tournament deleted successfully", toastrOptions);
        props.StopLoader();
        props.callApi();
        setDisabled2(false);
      })
      .catch(() => {
        props.onClose();
        props.StopLoader();
        setDisabled2(false);
      });
  };

  const closeAlert = () => {
    props.onClose();
  };

  return (
    <SweetAlert
      title="Delete Tournament"
      warning
      showCancel
      confirmButtonText="Yes"
      confirmBtnBsStyle="success"
      cancelButtonText="No"
      cancelBtnBsStyle="danger"
      onConfirm={() => handleDelete()}
      onCancel={() => closeAlert()}
      disabled={props.currentstat === 2 ? true : disableSwal2}
    >
      {props.currentstat === 2 ? (
        <p>
          Sorry, You cannot delete the tournament as the tournament has already
          been started{" "}
        </p>
      ) : (
        <p>Are you sure you want to delete this tournament?</p>
      )}
    </SweetAlert>
  );
};

DeleteAlertModal.propTypes = {
  onClose: PropTypes.func,
  callApi: PropTypes.func,
  Loader: PropTypes.func,
  StopLoader: PropTypes.func,
};

export default DeleteAlertModal;
```

## 📚 Detailed Explanation

### Imports and Dependencies

- **React**: Core library for building the component.
- **useState**: React Hook for managing component state.
- **PropTypes**: Used for type-checking the component's props.
- **react-toastify**: Library for showing toast notifications.
- **react-bootstrap-sweetalert**: Provides a sweet alert modal.
- **deleteTournament**: Function from an API helper to delete a tournament.

### Component Functionality

- **State Management**: 
  - `disableSwal2`: A state variable to control the disabled state of the SweetAlert.

- **handleDelete Function**: 
  - Initiates the loading state by calling `props.Loader()`.
  - Closes the modal by calling `props.onClose()`.
  - Disables further interactions with the alert by setting `setDisabled2(true)`.
  - Calls the `deleteTournament` API function and handles the promise:
    - On success: Displays a success toast and calls `props.callApi()` to refresh the data.
    - On failure: Ensures the loader is stopped and the modal is closed.

- **closeAlert Function**: 
  - Simply closes the alert by calling `props.onClose()`.

### Render Method

- **SweetAlert Component**: 
  - Displays a modal with options to confirm or cancel the deletion.
  - The confirmation button triggers `handleDelete`.
  - The cancel button triggers `closeAlert`.
  - Displays a condition-based message:
    - If `props.currentstat === 2`, it shows a message that the tournament cannot be deleted.
    - Otherwise, it asks for deletion confirmation.

### PropTypes

- **onClose**: Function to close the modal.
- **callApi**: Function to refresh the parent component's data.
- **Loader**: Function to start a loading indicator.
- **StopLoader**: Function to stop the loading indicator.

## 🌟 Usage

This component is used within applications where tournament data can be managed and deleted. It provides a user-friendly interface to confirm deletions and handles API interactions gracefully with feedback through toasts and modals.

## Key Features

- **User Feedback**: Provides clear feedback through toasts and modal dialogs.
- **State Management**: Efficiently manages loading and disabling states.
- **Error Handling**: Catches and handles errors from API calls.

## 🚀 Conclusion

The **`DeleteAlertModal`** component is a robust solution for handling tournament deletions in a React application, providing necessary user interactions and feedback with the help of modern libraries.

# Documentation for `Loader.js` 📄

Welcome to the documentation for the `Loader.js` file! This component is used to display a loading spinner to indicate that content is being loaded or an operation is in progress. Below is a detailed explanation of the file's functionality and usage.

## Table of Contents
1. [Overview](#overview)
2. [Component Description](#component-description)
3. [Props](#props)
4. [Code Explanation](#code-explanation)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

---

## Overview

The `Loader.js` file exports a React component named `Loader`. This component is designed to show a spinner animation when a particular condition is met, typically used to indicate loading states in an application.

---

## Component Description

The **Loader** component is a functional component that takes in props to control its display. It renders a spinner animation when `showLoader` is set to `true`. An optional `isTransparent` prop can be used to alter the style of the loader, changing its background to a transparent one.

---

## Props

The **Loader** component accepts the following props:

| Prop Name     | Type    | Description                                                    |
|---------------|---------|----------------------------------------------------------------|
| `showLoader`  | Boolean | Determines whether the loader should be displayed (`true`) or not (`false`). |
| `isTransparent` | Boolean | Optional. If `true`, applies a transparent style to the loader. |

---

## Code Explanation

Let's break down the code of `Loader.js`:

```javascript
import React from "react";
import PropTypes from "prop-types";

function Loader(props) {
  return (
    <React.Fragment>
      {props.showLoader ? (
        <div id={props.isTransparent ? "transparent-loader" : "preloader"}>
          <div id="status">
            <div className="spinner-chase">
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
            </div>
          </div>
        </div>
      ) : null}
    </React.Fragment>
  );
}

Loader.propTypes = {
  showLoader: PropTypes.bool,
  isTransparent: PropTypes.bool
};

export default Loader;
```

### Key Points:
- **Conditional Rendering**: The loader is displayed based on the `showLoader` prop. If `true`, the spinner is rendered.
- **Spinner Structure**: The spinner consists of a series of div elements with the class `chase-dot` to create a rotating effect.
- **Styling Options**: The `isTransparent` prop allows for styling flexibility, giving the option to use a transparent background.

---

## Usage

To use the `Loader` component in your application, simply import it and include it in your JSX. You can control its visibility and style with the `showLoader` and `isTransparent` props.

```jsx
import Loader from './Loader';

function App() {
  return (
    <div>
      <Loader showLoader={true} isTransparent={false} />
      {/* Other components */}
    </div>
  );
}
```

---

## Conclusion

The **Loader** component is a simple but effective way to indicate that a process is occurring in the background. By controlling its visibility and appearance with props, developers can easily integrate it into various parts of their applications to improve user experience during loading states.

Feel free to customize and extend this component to suit the needs of your project! 🎨

# 📜 Documentation for `index.js`

This documentation provides a detailed overview of the `index.js` file which serves the purpose of providing date filtering options for reports and logs in a React application. 📆✨

---

## 📋 Table of Contents

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Components](#components)
    - [DateFiltersReports](#datefiltersreports)
    - [CustomInput](#custominput)
4. [Usage](#usage)
5. [Props](#props)
6. [Conclusion](#conclusion)

---

## 📖 Introduction

The `index.js` file contains the `DateFiltersReports` component that allows users to filter data based on date ranges. It provides options to quickly select common time frames like today, this week, month, and year. It also includes functionality to export data to CSV. The file utilizes React and several third-party libraries.

---

## 📦 Imports

```javascript
import React from "react";
import ReactDatePicker from "react-datepicker";
import "react-datepicker/dist/react-datepicker.css";
import { Link } from "react-router-dom";
import calenderIcon from "../../../assets/images/calendar.svg";
import { Button } from "reactstrap";
```

- **React**: A JavaScript library for building user interfaces.
- **ReactDatePicker**: A date picker component for React.
- **react-router-dom**: For navigation within the app.
- **calendar.svg**: An icon used in the custom date input.
- **reactstrap**: A library for Bootstrap components in React.

---

## 🧩 Components

### DateFiltersReports

This is the main component that provides date filtering functionality.

#### Features
- Allows selection of a date range using a date picker.
- Provides buttons for quick date selections like Today, This Week, This Month, This Year.
- Includes a Clear button to reset filters.
- Offers an Export to CSV button for data extraction.

#### Code Snippet
```javascript
function DateFiltersReports({
  startDate, endDate, updateDateFromPicker, handleToday, handleMonth, 
  handleWeek, handleExport, handleYear, handleClear, detailView, 
  setDetailView, resetPagination, active, activeTab,
}) {
  const handleChange = (dates) => {
    updateDateFromPicker(dates);
  };

  return (
    <>
      {window.location.pathname == "/activitylog" ? (
        <div className="d-flex align-items-center flex-wrap ms-2">
          <ReactDatePicker
            className="new-filter datepicker-width"
            selectsRange={true}
            startDate={startDate}
            endDate={endDate}
            dateFormat="MM/dd/yyyy"
            onChange={handleChange}
            placeholderText="MM/DD/YYYY-MM/DD/YYYY"
            showMonthDropdown
            showYearDropdown
            dropdownMode="select"
            yearDropdownItemNumber={6}
            customInput={<CustomInput startDate={startDate} endDate={endDate} />}
          />
          <Button className={active.today === "1" ? "active ms-2 new-filter" : "ms-2 new-filter"} color="primary" onClick={handleToday}> Today </Button>
          <Button className={active.week === "2" ? "active ms-2 new-filter" : "ms-2 new-filter"} color="primary" onClick={handleWeek}> This Week </Button>
          <Button className={active.month === "3" ? "active ms-2 new-filter" : "ms-2 new-filter"} color="primary" onClick={handleMonth}> This Month </Button>
          <Button className={active.year === "4" ? "active ms-2 new-filter" : "ms-2 new-filter"} color="primary" onClick={handleYear}> This Year </Button>
          <Button className={active.clear === "5" ? "active ms-2 new-filter" : "ms-2 new-filter"} color="primary" onClick={handleClear}> Clear </Button>
        </div>
      ) : (
        <>
          {detailView ? (
            <div class="row">
              <div class="col">
                <p onClick={resetPagination}>
                  <Link to="/report">
                    <i className="mdi mdi-arrow-left"></i> back
                  </Link>
                </p>
              </div>
            </div>
          ) : null}
          <div className="d-flex align-items-center ms-2 flex-wrap mb-4">
            <span className="filterBy">Filter By : </span>
            {/* Date Picker and Buttons */}
          </div>
        </>
      )}
    </>
  );
}
```

### CustomInput

A custom input component for the `ReactDatePicker` to display the calendar icon and selected dates.

#### Code Snippet
```javascript
const CustomInput = React.forwardRef((props, ref) => {
  return (
    <div className="form-control dateFilterIcon d-flex" onClick={props.onClick} ref={ref}>
      <img src={calenderIcon} alt="calendar-icon" />
      <label className={`${props.startDate && props.endDate ? "selectedDate" : ""}`}>
        {props.value || props.placeholder}
      </label>
    </div>
  );
});
```

---

## 🛠️ Usage

To use the `DateFiltersReports` component, you need to pass the required props such as `startDate`, `endDate`, and handler functions for various date options.

```javascript
<DateFiltersReports
  startDate={startDate}
  endDate={endDate}
  updateDateFromPicker={updateDateFromPicker}
  handleToday={handleToday}
  handleMonth={handleMonth}
  handleWeek={handleWeek}
  handleExport={handleExport}
  handleYear={handleYear}
  handleClear={handleClear}
  detailView={detailView}
  setDetailView={setDetailView}
  resetPagination={resetPagination}
  active={active}
  activeTab={activeTab}
/>
```

---

## 🗂️ Props

| Prop Name            | Type       | Description                                    |
|----------------------|------------|------------------------------------------------|
| `startDate`          | `Date`     | The starting date of the range.                |
| `endDate`            | `Date`     | The ending date of the range.                  |
| `updateDateFromPicker` | `Function` | Updates the date range selected by the user.   |
| `handleToday`        | `Function` | Handler for setting today's date.              |
| `handleMonth`        | `Function` | Handler for setting this month's date range.   |
| `handleWeek`         | `Function` | Handler for setting this week's date range.    |
| `handleExport`       | `Function` | Handler for exporting data to CSV.             |
| `handleYear`         | `Function` | Handler for setting this year's date range.    |
| `handleClear`        | `Function` | Handler for clearing all filters.              |
| `detailView`         | `Boolean`  | Determines if the detail view is active.       |
| `setDetailView`      | `Function` | Sets the detail view state.                    |
| `resetPagination`    | `Function` | Resets pagination when navigating back.        |
| `active`             | `String`   | Indicates the active filter button.            |
| `activeTab`          | `String`   | Indicates the active tab for extra functionality.|

---

## 🔚 Conclusion

The `index.js` file is an essential part of the React application, providing a robust and user-friendly interface for date-based filtering. It enhances the user's ability to analyze data over different time periods and export it as needed. The combination of `ReactDatePicker` and Bootstrap components makes it both functional and aesthetically pleasing. 🌟

---

For any updates or issues, please refer to the project repository or contact the development team. Happy coding! 🖥️🎈

# Documentation for the `index.js` File

## Overview

This file defines a **React component** named `ReportsCard`. It is designed to display a card with a header and body content, which is used to show information such as financial reports or any other data in a card format.

## Table of Contents

- [File Structure](#file-structure)
- [Component: ReportsCard](#component-reportscard)
  - [Props](#props)
  - [Usage](#usage)
- [Exports](#exports)

## File Structure

The file structure is straightforward, consisting of a single React component:

```javascript
import React from "react";
import { Card, CardBody, CardHeader, CardText } from "reactstrap";

function ReportsCard({ label = "", units = "", value = "" }) {
  return (
    <Card className="my-2 p-2" color="light">
      <CardHeader>{label}</CardHeader>
      <CardBody>
        <CardText>{units + value}</CardText>
      </CardBody>
    </Card>
  );
}

export default ReportsCard;
```

## Component: ReportsCard

### Purpose

The `ReportsCard` component is used to create a card layout using **Reactstrap** components. It displays a header and a piece of text within the card body, which is typically used to present data like report metrics.

### Props

The `ReportsCard` component accepts the following props:

| Prop   | Type   | Default Value | Description                                         |
|--------|--------|---------------|-----------------------------------------------------|
| `label` | String | `""`          | The text to display in the card header.             |
| `units` | String | `""`          | Units or prefix to be displayed with the value.     |
| `value` | String | `""`          | The main value or text to display in the card body. |

### Usage

Here’s an example of how to use the `ReportsCard` component:

```jsx
<ReportsCard
  label="Revenue"
  units="$"
  value="1,000"
/>
```

This will render a card with "Revenue" as the header and "$1,000" as the body text.

## Exports

The file exports the `ReportsCard` component as the default export:

```javascript
export default ReportsCard;
```

---

This concludes the documentation for the `index.js` file, which defines the `ReportsCard` component. The component is a simple, reusable card structure that can be used to display various types of data in a visually appealing manner using the **Reactstrap** library.

# Documentation for Project Components

Welcome to the documentation of the various React components used in this project. This document will provide detailed insights into the purpose and functionality of each component, allowing developers to understand and use them effectively in the application.

## Index

1. [ClearButton.js](#clearbuttonjs)
2. [GoBack.jsx](#gobackjsx)
3. [IconsToolTip.jsx](#iconstooltipjsx)
4. [NonAuthLayout.js](#nonauthlayoutjs)
5. [Breadcrumb.js](#breadcrumbjs)
6. [DeleteAlertModal.jsx](#deletealertmodaljsx)
7. [Loader.js](#loaderjs)
8. [DateFiltersReports (index.js)](#datefiltersreports-indexjs)
9. [FiltersResultInButton (index.js)](#filtersresultinbutton-indexjs)
10. [ReportNavigationLink (index.js)](#reportnavigationlink-indexjs)
11. [ReportsCard (index.js)](#reportscard-indexjs)
12. [IMG (index.js)](#img-indexjs)

---

## ClearButton.js

### Description
The **ClearButton** component is a simple, reusable button component designed to trigger a clear action when clicked. It makes use of the `reactstrap` library for styling.

### Code
```javascript
import React from "react";
import { Button } from "reactstrap";

function ClearButton({ handleClear }) {
  return (
    <Button className="new-filter" color="primary" onClick={handleClear}>
      Clear
    </Button>
  );
}

export default ClearButton;
```

### Props
- **handleClear**: A function passed as a prop that gets called when the button is clicked.

### Usage
This component is useful in scenarios where a user needs to reset or clear filters or forms. It is styled with a primary color for prominence and includes a custom class `new-filter` for further styling.

---

## GoBack.jsx

### Description
The **GoBack** component provides a navigational link that takes users back to a specified URL. It leverages `reactstrap` components for layout and `react-router-dom` for routing.

### Code
```javascript
import { Row, Col } from "reactstrap";
import { Link } from "react-router-dom";

export const GoBack = ({ backUrl }) => {
  return (
    <Row className="mb-4">
      <Col>
        <p>
          <Link to={backUrl}>
            <i className="mdi mdi-arrow-left"></i> back
          </Link>
        </p>
      </Col>
    </Row>
  );
};
```

### Props
- **backUrl**: A string representing the URL to navigate back to.

### Usage
This component is ideal for implementing back navigation functionality within an application, enhancing user experience by allowing easy navigation to previous pages.

---

## IconsToolTip.jsx

### Description
The **IconsToolTip** component is designed to display an image along with a tooltip containing additional information. It enhances user interaction by providing context through tooltips.

### Code
```javascript
import React from "react";

function IconsToolTip({ image, altImageText, text }) {
  return (
    <>
      <img alt={altImageText} src={image} />
      <span
        className="edit-tournament-tooltip tooltiptext"
        data-tip
        data-for="loginTip"
      >
        {text}
      </span>
    </>
  );
}

export default IconsToolTip;
```

### Props
- **image**: The source URL for the image to be displayed.
- **altImageText**: Alternate text for the image, used for accessibility.
- **text**: The text content of the tooltip.

### Usage
Use this component to add informative tooltips to icons or images, assisting users in understanding the functionality or purpose of the icons.

---

## NonAuthLayout.js

### Description
The **NonAuthLayout** component serves as a layout wrapper for non-authenticated routes or pages. It sets a default document title and renders its children.

### Code
```javascript
import PropTypes from "prop-types";
import React, { Component } from "react";
import { withRouter } from "react-router-dom";

class NonAuthLayout extends Component {
  constructor(props) {
    super(props);
    this.state = {};
    this.capitalizeFirstLetter.bind(this);
  }

  capitalizeFirstLetter = (string) => {
    return string.charAt(1).toUpperCase() + string.slice(2);
  };

  componentDidMount() {
    document.title = "Ryvals";
  }

  render() {
    return <React.Fragment>{this.props.children}</React.Fragment>;
  }
}

NonAuthLayout.propTypes = {
  children: PropTypes.any,
  location: PropTypes.object,
};

export default withRouter(NonAuthLayout);
```

### Props
- **children**: The content to be rendered within the layout.
- **location**: The location object from `react-router-dom`.

### Usage
This component is intended for pages that do not require user authentication, such as public-facing pages. It ensures a consistent layout and document title.

---

## Breadcrumb.js

### Description
The **Breadcrumb** component is a simple breadcrumb navigation component that displays the current page title or navigation item.

### Code
```javascript
import React from "react";
import PropTypes from "prop-types";
import { Row, Col } from "reactstrap";

const Breadcrumb = (props) => {
  return (
    <Row>
      <Col className="col-12">
        <div className="page-title-box d-flex align-items-start align-items-center justify-content-between">
          <h4 className="page-title mb-0 font-size-18">
            {props.breadcrumbItem}
          </h4>
        </div>
      </Col>
    </Row>
  );
};

Breadcrumb.propTypes = {
  breadcrumbItem: PropTypes.string,
  title: PropTypes.string,
};

export default Breadcrumb;
```

### Props
- **breadcrumbItem**: The current breadcrumb item to be displayed.
- **title**: Title for the breadcrumb, though it's not used in the component.

### Usage
Utilize the Breadcrumb component to provide users with a navigational aid that shows their current location within the application's hierarchy.

---

## DeleteAlertModal.jsx

### Description
The **DeleteAlertModal** component provides a modal dialog for confirming the deletion of an item. It utilizes a sweet alert for a user-friendly confirmation interface.

### Code
```javascript
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import PropTypes from "prop-types";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import SweetAlert from "react-bootstrap-sweetalert";
import { deleteTournament } from "../../services/bracket_tournaments_api_helper";

const DeleteAlertModal = (props) => {
  const [disableSwal2, setDisabled2] = useState(false);

  const handleDelete = async () => {
    props.Loader();
    props.onClose();
    setDisabled2(true);
    await deleteTournament(props.DeleteId)
      .then((res) => {
        toast.success("Tournament deleted successfully", toastrOptions);
        props.StopLoader();
        props.callApi();
        setDisabled2(false);
      })
      .catch(() => {
        props.onClose();
        props.StopLoader();
        setDisabled2(false);
      });
  };

  const closeAlert = () => {
    props.onClose();
  };

  return (
    <SweetAlert
      title="Delete Tournament"
      warning
      showCancel
      confirmButtonText="Yes"
      confirmBtnBsStyle="success"
      cancelButtonText="No"
      cancelBtnBsStyle="danger"
      onConfirm={() => handleDelete()}
      onCancel={() => closeAlert()}
      disabled={props.currentstat === 2 ? true : disableSwal2}
    >
      {props.currentstat === 2 ? (
        <p>
          Sorry, You cannot delete the tournament as the tournament has already
          been started{" "}
        </p>
      ) : (
        <p>Are you sure you want to delete this tournament?</p>
      )}
    </SweetAlert>
  );
};

DeleteAlertModal.propTypes = {
  onClose: PropTypes.func,
  callApi: PropTypes.func,
  Loader: PropTypes.func,
  StopLoader: PropTypes.func,
};

export default DeleteAlertModal;
```

### Props
- **onClose**: Function to close the modal.
- **callApi**: Function to call an API after deletion.
- **Loader**: Function to show loading.
- **StopLoader**: Function to stop loading.

### Usage
This component is perfect for scenarios where confirmation is needed before performing a destructive action, such as deleting an item.

---

## Loader.js

### Description
The **Loader** component displays a loading spinner based on the `showLoader` prop. It includes an optional transparency feature.

### Code
```javascript
import React from "react";
import PropTypes from "prop-types";

function Loader(props) {
  return (
    <React.Fragment>
      {props.showLoader ? (
        <div id={props.isTransparent ? "transparent-loader" : "preloader"}>
          <div id="status">
            <div className="spinner-chase">
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
              <div className="chase-dot"></div>
            </div>
          </div>
        </div>
      ) : null}
    </React.Fragment>
  );
}

Loader.propTypes = {
  showLoader: PropTypes.bool,
};

export default Loader;
```

### Props
- **showLoader**: Boolean to show or hide the loader.
- **isTransparent**: Optional boolean to set the loader as transparent.

### Usage
Use this component to indicate background processes or loading states to users, enhancing user experience by providing visual feedback.

---

## DateFiltersReports (index.js)

### Description
The **DateFiltersReports** component is a complex component that provides various date filtering options for reports. It includes functionality for selecting a date range and applying pre-defined date filters such as "Today," "This Week," etc.

### Code
```javascript
// The code is extensive; hence, only the use case and highlights are provided in the documentation.
```

### Usage
This component is suitable for applications that require detailed date-based filtering options, allowing users to narrow down data displayed in reports.

### Key Features
- **Date Range Picker**: Allows users to select a custom date range.
- **Pre-defined Filters**: Provides buttons to quickly apply common date filters like today, this week, etc.
- **Export Functionality**: Includes an option to export filtered data to CSV.

---

## FiltersResultInButton (index.js)

### Description
The **FiltersResultInButton** component renders a set of card components based on provided data, with interactive filters.

### Code
```javascript
// The code is extensive; hence, only the use case and highlights are provided in the documentation.
```

### Usage
This component is designed for displaying summarized data within cards, with the ability to filter results dynamically. It is beneficial for dashboard-like interfaces.

### Key Features
- **Dynamic Cards**: Renders cards based on data and configuration.
- **Interactive Filters**: Allows users to filter the displayed cards by interacting with them.

---

## ReportNavigationLink (index.js)

### Description
The **ReportNavigationLink** component is a navigational component that utilizes React Router to link to a report page, passing various state data.

### Code
```javascript
import React from "react";
import { Link } from "react-router-dom";

function ReportNavigationLink({
  children,
  activeTab,
  transactionFilter,
  detailView,
  url,
  activeFilter,
  setDates,
  userTab,
  nameOfGame,
}) {
  return (
    <Link
      to={{
        pathname: url,
        data: {
          prevPath: window.location.pathname,
          activeTab,
          filter: transactionFilter,
          activeFilter,
          detailView,
          setDates,
          userTab,
          nameOfGame,
        },
      }}
    >
      {children}
    </Link>
  );
}

export default ReportNavigationLink;
```

### Props
- **url**: The URL to navigate to.
- **children**: Content to render inside the link.
- **activeTab**, **transactionFilter**, **detailView**, etc.: Various state data to pass to the linked page.

### Usage
This component is useful for creating navigation links that carry over application state, ensuring continuity in user experience when navigating between pages.

---

## ReportsCard (index.js)

### Description
The **ReportsCard** component is a simple card component that displays a label, units, and a value, used to present data in a structured format.

### Code
```javascript
import React from "react";
import { Card, CardBody, CardHeader, CardText } from "reactstrap";

function ReportsCard({ label = "", units = "", value = "" }) {
  return (
    <Card className="my-2 p-2" color="light">
      <CardHeader>{label}</CardHeader>
      <CardBody>
        <CardText>{units + value}</CardText>
      </CardBody>
    </Card>
  );
}

export default ReportsCard;
```

### Props
- **label**: The label to display in the card header.
- **units**: The units of the value displayed.
- **value**: The value to display in the card body.

### Usage
Use this component to display concise and organized data points within a card, making it a great fit for dashboards or report summaries.

---

## IMG (index.js)

### Description
The **IMG** component provides a stylized image element with a tooltip, offering additional information based on the provided data.

### Code
```javascript
import info from "../../../assets/images/info-icon.svg";

export const IMG = (data) => {
  return (
    <>
      Statistic Code*
      <span className="info-icon stats-infoIcon">
        <img
          src={info}
          alt="info"
          className="info-image"
          data-tip
          data-for="loginTip"
        />
        <span class="tooltiptext">
          {data?.data === "valorant"
            ? "Please update any one player's riot ID to generate game stats."
            : "Please make sure the code being entered matches exactly whats provided by Games."}
        </span>
      </span>
    </>
  );
};
```

### Props
- **data**: Object containing data to determine tooltip content.

### Usage
This component is useful in scenarios where additional context or instructions are necessary, enhancing user understanding through tooltips.

---

This documentation provides an overview and detailed description of each component within the project, allowing developers to effectively utilize and customize these components as needed.

# Documentation: `utils.js`

Welcome to the documentation for `utils.js`. This file plays a crucial role in managing dynamic table values for transaction data in a React application. It provides a mapping for table headings, which can be modified or expanded as per the application's requirements.

---

## Table of Contents

1. [Overview](#overview)
2. [Code Explanation](#code-explanation)
3. [Usage](#usage)
4. [Customization](#customization)

---

## Overview

The `utils.js` file contains a JavaScript object named `dynamicTableValuesTransactions`, which serves as a configuration or mapping for styling or class assignments for different table headings based on their index.

### Why is it useful?

- **Modular Configuration**: It provides a centralized place to manage table heading styles, making it easier to update and maintain.
- **Dynamic Styling**: Allows for dynamic assignment of styles to table headers, aiding in a consistent and scalable UI design strategy.

---

## Code Explanation

Here's a breakdown of the code found in `utils.js`:

```javascript
export const dynamicTableValuesTransactions = {
  0: "tableHead",
  1: "tableHead",
  2: "tableHead",
  3: "tableHead",
  4: "tableHead",
  5: "tableHead",
  6: "tableHead",
  7: "tableHead",
  8: "tableHeadUnclaimed",
  9: "tableHead",
  10: "tableHead",
  11: "tableHeadDormant",
  12: "tableHeadInactivity",
};
```

### Key Points:

- The object `dynamicTableValuesTransactions` maps numerical indices to string values. These strings typically represent CSS class names.
- Indices `0-7` and `9-10` are assigned the class "tableHead".
- Index `8` is given the class "tableHeadUnclaimed".
- Index `11` is assigned to "tableHeadDormant".
- Index `12` uses "tableHeadInactivity".

---

## Usage

This file is typically imported into other components where table rendering occurs. Here's a hypothetical example of how it might be used:

```javascript
import { dynamicTableValuesTransactions } from './utils';

// Example usage in a component
const TableComponent = () => {
  return (
    <table>
      <thead>
        <tr>
          {Object.keys(dynamicTableValuesTransactions).map((key) => (
            <th className={dynamicTableValuesTransactions[key]} key={key}>
              {/* Render the table header content here */}
            </th>
          ))}
        </tr>
      </thead>
      <tbody>
        {/* Render table body here */}
      </tbody>
    </table>
  );
};
```

### Explanation:

- The `dynamicTableValuesTransactions` object is iterated over to dynamically assign classes to each `<th>` element.
- This pattern allows for flexible and easy updates to how table headings are styled in the UI.

---

## Customization

### Adding New Styles:

To add new styles, simply append new key-value pairs to the `dynamicTableValuesTransactions` object:

```javascript
export const dynamicTableValuesTransactions = {
  ...,
  13: "newTableHeadStyle",
};
```

### Changing Existing Styles:

To change existing styles, update the value associated with the desired key:

```javascript
export const dynamicTableValuesTransactions = {
  11: "updatedTableHeadDormant",
};
```

With this approach, you can efficiently manage and maintain table heading styles across your application from a single file.

---

By using this modular and dynamic configuration file, developers can ensure a consistent and maintainable approach to styling table headings throughout the React application.

# Documentation for `index.js`

This document provides a comprehensive overview of the `index.js` file, explaining its purpose, functionality, and usage in a React application. This file primarily deals with the rendering of a dynamic table based on active tabs, handling permissions, and integrating navigation links for detailed views.

## Table of Contents
1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Component: `TableBasedOnActiveTab`](#component-tablebasedonactivetab)
   - [Props](#props)
   - [Component Logic](#component-logic)
   - [Rendering Logic](#rendering-logic)
4. [Helper Functions](#helper-functions)
5. [Exports](#exports)

## Overview

The `index.js` file defines the `TableBasedOnActiveTab` component, which is responsible for displaying a table of data that changes based on the active tab. It incorporates pagination, dynamic headers, and utilizes permissions to control the visibility of detailed views.

## Dependencies

```jsx
import React, { useEffect, useState } from "react";
import { Row, Col } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import { reportsTableConstant } from "../../../constants/reportsTableConstant";
import Paginator from "../../../helpers/paginator/PaginatorReport";
import FilterPermission from "../../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../../helpers/PermissionUtils";
import ReportNavigationLink from "../ReportNavigationLink";
import { dynamicTableValuesTransactions } from "./utils";
import { FreeText, getPaymentMethod } from "../../../helpers/util";
```

## Component: `TableBasedOnActiveTab`

### Props

| Prop               | Type     | Description                                                    |
|--------------------|----------|----------------------------------------------------------------|
| `data`             | Object   | Data to be displayed in the table.                             |
| `type`             | Number   | Indicates the type of data being handled.                      |
| `setDetailView`    | Function | Function to toggle the detailed view.                          |
| `detailView`       | Boolean  | Controls whether the detailed view is active.                  |
| `totalCount`       | Number   | Total number of records available.                             |
| `handlePageClick`  | Function | Function to handle pagination clicks.                          |
| `pageNum`          | Object   | Current page number for pagination.                            |
| `transactionFilter`| Number   | Filter value for transactions.                                 |
| `props`            | Object   | Contains permission data and other properties.                 |
| `active`           | Boolean  | Indicates if the current tab is active.                        |
| `setDates`         | Function | Function to set date range for filtering.                      |

### Component Logic

The `TableBasedOnActiveTab` component makes use of several state variables and effect hooks to manage its behavior:

- **State Variables**: 
  - `viewPermission`, `codMobile`, `fortnite`, `pubgmobile`, `pubgpc`: Used to store permission states for various modules.
  
- **Effect Hook**: 
  - The `useEffect` hook is used to set permissions based on the `props.permission` data when the component mounts or `props.permission` changes.

### Rendering Logic

- **Dynamic Headers**: The headers of the table are generated based on the active tab and the `transactionFilter`.
  
- **Table Data**: Dynamic data rendering logic is based on the type of entry and permissions. Conditional rendering is used extensively to ensure only authorized data is shown.
  
- **Navigation Links**: The component uses `ReportNavigationLink` to provide navigation to detailed views for entries based on permissions.

### Example Usage

```jsx
<TableBasedOnActiveTab
  data={data}
  type={1}
  setDetailView={setDetailView}
  detailView={detailView}
  totalCount={100}
  handlePageClick={handlePageClick}
  pageNum={{ 1: 1 }}
  transactionFilter={1}
  props={{ permission: userPermissions }}
  active={true}
  setDates={setDates}
/>
```

## Helper Functions

- **`dynamicTableHeader`**: Generates table headers dynamically based on the current active tab and transaction filter.
  
- **`dynamicTableValue`**: Determines the value to be displayed for each cell in the table based on the data type and permissions.

## Exports

```jsx
export default TableBasedOnActiveTab;
```

The `index.js` file exports the `TableBasedOnActiveTab` component as the default export, making it available for import and use in other parts of the application.

---

This documentation provides a detailed explanation of the `index.js` file, highlighting its purpose, usage, and integration within a React application. The file is pivotal in rendering a dynamic and interactive table interface, tailored to user permissions and active tab configurations.