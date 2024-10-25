# 📄 Documentation: `Footer.js`

Welcome to the documentation for the `Footer.js` file. This file is a component of a React application and is responsible for rendering the footer section of the web application. This documentation will guide you through the structure, purpose, and functionality of the `Footer.js` component.

## 🌈 Table of Contents

1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Code Explanation](#code-explanation)
4. [Key Features](#key-features)
5. [Dependencies](#dependencies)
6. [Conclusion](#conclusion)

## 📝 Introduction

The `Footer.js` file defines a functional React component named `Footer`. This component uses **Reactstrap**, a popular library for Bootstrap components in React, to create a responsive and aesthetically pleasing footer for the web application. 

## 🏗️ Component Structure

The component uses the following structure:

- **React.Fragment**: Used to wrap the component elements without adding extra nodes to the DOM.
- **Container**: A Bootstrap container that provides a responsive fixed-width container.
- **Row**: A Bootstrap row that serves as a horizontal layout.
- **Col**: A Bootstrap column used to divide the space into sections.

## 🔍 Code Explanation

Here's a detailed explanation of the code in `Footer.js`:

```jsx
import React from "react"; 
import { Container, Row, Col } from "reactstrap"; 

const Footer = () => { 
  return ( 
    <React.Fragment> 
      <footer className="footer"> 
        <Container fluid={true}> 
          <Row> 
            <Col sm={6}>
              {new Date().getFullYear()} © Ryvals.
            </Col> 
            <Col sm={6}> 
              <div className="text-sm-end d-none d-sm-block"></div> 
            </Col> 
          </Row> 
        </Container> 
      </footer> 
    </React.Fragment> 
  ); 
}; 

export default Footer;
```

### Breakdown

- **Imports**: 
  - `React` is imported to create a React component.
  - `Container`, `Row`, and `Col` are imported from `reactstrap` to utilize Bootstrap's grid system.

- **Footer Component**:
  - The component is defined as a functional component using an arrow function.
  - **Container** is set to `fluid={true}`, allowing it to span the entire width of the viewport.
  - **Row** consists of two columns:
    - The first column (`Col sm={6}`) displays the current year dynamically using `new Date().getFullYear()` followed by the text "© Ryvals."
    - The second column is prepared for additional content with classes `text-sm-end` (aligns text to the end on small screens) and `d-none d-sm-block` (hides content on extra-small screens).

- **Export**: 
  - The `Footer` component is exported as the default export of the file.

## ✨ Key Features

- **Responsive Design**: Utilizes Bootstrap’s grid system to ensure the footer is responsive across different device sizes.
- **Dynamic Year Display**: Automatically updates the displayed year to the current year.
- **Scalability**: Easily extendable for future links or additional information in the footer.

## 📦 Dependencies

The `Footer.js` component relies on the following dependencies:

| Dependency | Description |
|------------|-------------|
| `react`    | Core library for building user interfaces using React. |
| `reactstrap` | A Bootstrap component library for React that provides ready-to-use components. |

## 📚 Conclusion

The `Footer.js` component is a simple yet effective part of a React application, serving the essential purpose of displaying a footer with the current year and company name. By leveraging `reactstrap`, it maintains a responsive design, ensuring that it looks good on all devices. This component can be further customized or extended to include additional information or links as needed. 

Feel free to explore, modify, and integrate this component into your projects to enhance the user interface of your application! 😊

# 📄 Header.js Documentation

Welcome to the detailed documentation for the `Header.js` file of our React application. This file is responsible for rendering the header section of the web application and manages several functionalities related to the UI layout and interactions. Let's delve into the specifics! 🌟

## 📑 Index

1. [Overview](#overview)
2. [Imports](#imports)
3. [Component Description](#component-description)
4. [Functions and Logic](#functions-and-logic)
5. [PropTypes](#proptypes)
6. [Redux Integration](#redux-integration)
7. [Conclusion](#conclusion)

## Overview

The **Header** component serves as the top navigation bar for the application. It includes logos, a profile menu, and controls for toggling the sidebar. It also retrieves a list of games from an API when the component is mounted.

## Imports

Let's look at what this component imports and why:

```javascript
import PropTypes from "prop-types"; // Used for runtime type checking
import React, { useEffect } from "react"; // React library and useEffect hook
import { connect, useDispatch, useSelector } from "react-redux"; // Redux state management
import { Container } from "reactstrap"; // Bootstrap component
import { Link } from "react-router-dom"; // Routing
import ProfileMenu from "../CommonForBoth/TopbarDropdown/ProfileMenu"; // Profile dropdown component

// Importing logos
import logoSm from "../../assets/images/ryvals-logo.png";
import logo from "../../assets/images/ryvals-logo.png";

// i18n translation support
import { withTranslation } from "react-i18next";

// Redux actions
import { showRightSidebarAction, toggleLeftmenu, changeSidebarType, setGames } from "../../store/actions";
import { getGameList } from "../../services/game_api_helper"; // API helper function
```

## Component Description

The `Header` component is a functional React component that uses hooks and Redux to manage state and side effects. Here's how it structures the UI:

- **Navbar**: Contains the logo and a profile menu.
- **Logo**: Clickable link that redirects to the homepage.
- **Toggle Button**: A hamburger menu icon that appears on smaller screens for toggling the sidebar.

## Functions and Logic

### `tToggle()`

This function toggles the sidebar between a collapsed and expanded state, depending on the screen width:

```javascript
function tToggle() {
    var body = document.body;
    if (window.screen.width <= 768) {
        body.classList.toggle("sidebar-enable");
    } else {
        body.classList.toggle("vertical-collpsed");
        body.classList.toggle("sidebar-enable");
    }
}
```

### `getGames()`

An asynchronous function that fetches a list of games from an API and dispatches the result to the Redux store:

```javascript
const getGames = async () => {
    try {
        const res = await getGameList();
        dispatch(setGames(res));
    } catch (error) {}
};
```

### useEffect Hook

```javascript
useEffect(() => {
    if (!games.length) {
        getGames();
    }
}, []);
```

This hook ensures that the game list is fetched when the component mounts and only if the games array is empty.

## PropTypes

The `Header` component uses `PropTypes` for type checking its props:

```javascript
Header.propTypes = {
    changeSidebarType: PropTypes.func,
    leftMenu: PropTypes.any,
    leftSideBarType: PropTypes.any,
    showRightSidebar: PropTypes.any,
    showRightSidebarAction: PropTypes.func,
    t: PropTypes.any,
    toggleLeftmenu: PropTypes.func,
};
```

## Redux Integration

The component connects to the Redux store to manage global state:

- **State Mapping**: Maps layout-related state properties to component props.
- **Actions**: Imports and connects actions like `showRightSidebarAction`, `toggleLeftmenu`, and `changeSidebarType`.

```javascript
const mapStatetoProps = (state) => {
    const { layoutType, showRightSidebar, leftMenu, leftSideBarType } = state.Layout;
    return { layoutType, showRightSidebar, leftMenu, leftSideBarType };
};

export default connect(mapStatetoProps, { showRightSidebarAction, toggleLeftmenu, changeSidebarType })(withTranslation()(Header));
```

## Conclusion

The `Header.js` component is a dynamic and interactive part of the application that utilizes React hooks and Redux for state management. It provides essential UI elements and functionality for user interaction and navigation. 🏆

Feel free to extend or modify the component as per your project requirements! If you have any questions or need further assistance, feel free to reach out.

# 📚 Sidebar.js Documentation

---

**File Purpose:**  
The `Sidebar.js` file is responsible for rendering the sidebar component of a web application. It dynamically constructs the sidebar based on user permissions, retrieved from local storage. This enhances user experience by showing relevant content tailored to the user's role or access level.

---

## 📂 Index

- [Overview](#overview)
- [Components and Libraries Used](#components-and-libraries-used)
- [Core Functionalities](#core-functionalities)
- [Props and State](#props-and-state)
- [Redux Integration](#redux-integration)
- [Code Walkthrough](#code-walkthrough)

---

## 📖 Overview

The sidebar is a vertical menu component that dynamically displays user-specific information. It fetches the user's details from local storage upon loading and displays the user's name and permissions. It integrates with Redux to potentially manage and respond to global state changes.

---

## 🛠️ Components and Libraries Used

**Libraries:**

- **React**: A JavaScript library for building user interfaces.
- **React-Redux**: Official React bindings for Redux to manage application state.
- **React Router DOM**: Declarative routing for React applications.
- **i18next**: Internationalization library for JavaScript.
- **PropTypes**: Runtime type checking for React props.

**Components:**

- **SidebarContent**: A child component responsible for rendering the actual content inside the sidebar.

---

## 🔍 Core Functionalities

- **Fetch User Data**: Retrieves user data from local storage to personalize the sidebar experience.
- **Display User Information**: Shows the full name and permissions of the logged-in user.
- **Dynamic Content**: Utilizes the `SidebarContent` component to render sidebar items based on user permissions.

---

## ⚙️ Props and State

### **State Variables:**

- **`username`**: Holds the concatenated first and last name of the user.
- **`permissions`**: Stores the permissions associated with the user.

### **PropTypes:**

| Prop Name | Type   | Description                                  |
|-----------|--------|----------------------------------------------|
| `type`    | string | Describes the type of sidebar (not utilized directly in the code). |

---

## 🔗 Redux Integration

The `Sidebar` component is connected to the Redux store, allowing it to access and potentially dispatch actions based on the global state.

### **mapStatetoProps**:

This function maps the Redux state to the component's props, although in this implementation it only provides access to the `layout` property from the Redux store, which could be used for more advanced layout control.

---

## 📝 Code Walkthrough

```javascript
import PropTypes from "prop-types";
import React, { useEffect, useState } from "react";
import { connect } from "react-redux";
import { withRouter } from "react-router-dom";
//i18n
import { withTranslation } from "react-i18next";
import SidebarContent from "./SidebarContent";
```
- **Imports**: The file imports necessary libraries and components, including `React`, `PropTypes`, `React-Redux`, and more, indicating its reliance on modern React features and internationalization.

```javascript
const Sidebar = (props) => {
  const [username, setusername] = useState(null);
  const [permissions, setPermissions] = useState("");
```
- **State Initialization**: Uses `useState` to declare state variables for `username` and `permissions`.

```javascript
  useEffect(() => {
    if (localStorage.getItem("authUser")) {
      const obj = JSON.parse(localStorage.getItem("authUser"));
      setusername(obj.extras.first_name + " " + obj.extras.last_name);
      setPermissions(obj.extras.permissions);
    }
  }, [props.success]);
```
- **useEffect Hook**: Runs on component mount and when `props.success` changes. It retrieves the authenticated user's data from local storage and updates the state accordingly.

```javascript
  return (
    <React.Fragment>
      <div className="vertical-menu">
        <div className="h-100">
          <div className="user-wid text-center py-4">
            <div className="mt-3">
              <p className="text-dark fw-medium font-size-24 username asdfgh">
                {username}
              </p>
            </div>
          </div>
          <div data-simplebar className="h-100">
            <SidebarContent permissions={permissions} />
          </div>
        </div>
      </div>
    </React.Fragment>
  );
};
```
- **Rendering**: The component renders a vertical menu with user information and the `SidebarContent` component, passing the user's permissions as props.

```javascript
Sidebar.propTypes = {
  type: PropTypes.string,
};
```
- **PropTypes**: `type` is defined for type-checking, though it does not appear to be used within the component logic.

```javascript
const mapStatetoProps = (state) => {
  return {
    layout: state.Layout,
  };
};

export default connect(
  mapStatetoProps,
  {}
)(withRouter(withTranslation()(Sidebar)));
```
- **Redux Connection**: Connects to the Redux store and wraps the component with routing and translation capabilities.

---

This file provides the foundational structure for a personalized and interactive sidebar component, leveraging both React and Redux for state management and user data handling.

# Documentation for `index.js` 🎉

This documentation provides a comprehensive overview of the `index.js` file, which is a central component of the layout system in a React application. It integrates various elements like the `Header`, `Sidebar`, and `Footer` to build the main structure of the page.

---

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Structure](#structure)
3. [Components and Imports](#components-and-imports)
4. [State and Props](#state-and-props)
5. [Lifecycle Methods](#lifecycle-methods)
6. [Render Method](#render-method)
7. [PropTypes](#proptypes)
8. [Redux Integration](#redux-integration)
9. [Summary](#summary)

---

## Introduction

The `index.js` file defines the `Layout` component, which serves as the core layout structure for the application. It assembles various sub-components into a cohesive layout and manages layout-related configurations using Redux for state management.

---

## Structure

The `Layout` component is a **class component**, providing methods to manage component lifecycle and interactions with the DOM.

```javascript
class Layout extends Component {
  constructor(props) { ... }
  componentDidMount() { ... }
  render() { ... }
}
```

---

## Components and Imports

The file imports several dependencies and sub-components necessary for building the layout:

- **React and PropTypes**: For building the component and type-checking.
- **React-Redux and React-Router**: For state management and routing.
- **Action Creators**: Functions to change layout properties.
- **Sub-Components**: `Header`, `Sidebar`, and `Footer`.

```javascript
import Header from "./Header";
import Sidebar from "./Sidebar";
import Footer from "./Footer";
```

---

## State and Props

- **State**: Tracks whether the device is mobile using a regex test on the user agent.
  ```javascript
  this.state = {
    isMobile: /iPhone|iPad|iPod|Android/i.test(navigator.userAgent),
  };
  ```

- **Props**: Passed from Redux to manage layout configurations like sidebar theme and layout width.

---

## Lifecycle Methods

### `componentDidMount()`
- **Purpose**: Initializes layout settings once the component mounts.
- **Actions**:
  - Displays a preloader if enabled.
  - Sets document title.
  - Configures layout, sidebar, and topbar based on props.
  
```javascript
componentDidMount() {
  // Logic to handle preloader and layout settings
}
```

---

## Render Method

The `render()` function defines the JSX structure for the layout, incorporating the `Header`, `Sidebar`, `Footer`, and the content passed as children.

```javascript
render() {
  return (
    <React.Fragment>
      <div id="preloader">...</div>
      <div className="container-fluid">
        <div id="layout-wrapper">
          <Header toggleMenuCallback={this.toggleMenuCallback} />
          <Sidebar ... />
          <div className="main-content">
            {this.props.children}
            <Footer />
          </div>
        </div>
      </div>
    </React.Fragment>
  );
}
```

---

## PropTypes

The `Layout` component uses `PropTypes` to define expected props and their types, ensuring that correct data is passed down from Redux and other parts of the app.

```javascript
Layout.propTypes = {
  changeLayoutWidth: PropTypes.func,
  // Other PropTypes...
};
```

---

## Redux Integration

The component connects to the Redux store using `connect`, allowing it to dispatch actions to change layout properties and to access state data.

- **mapStatetoProps**: Maps layout state from Redux to component props.
- **Action Dispatchers**: Functions to alter layout settings like `changeLayout`, `changeSidebarTheme`, etc.

```javascript
export default connect(mapStatetoProps, {
  changeLayout,
  // Other actions...
})(withRouter(Layout));
```

---

## Summary

The `index.js` file constructs the main layout of the application, integrating multiple components and managing layout settings through Redux. It handles the initialization and rendering of the layout, ensuring a responsive and dynamic user interface.

This documentation serves as a detailed guide to understanding the structure and functionality of the `Layout` component, as well as its interaction with Redux for state management.

# 📚 Documentation for SidebarContent.js

This document provides a comprehensive overview of the `SidebarContent.js` file, detailing its purpose, functionality, and components. This file is responsible for rendering the sidebar menu of the application, which navigates users to various sections based on permissions and paths. Below is an organized and detailed breakdown of the file.

## **Table of Contents**

1. [Overview](#overview)
2. [Imports](#imports)
3. [Functional Components](#functional-components)
   - [useState Hook](#usestate-hook)
   - [useEffect Hook](#useeffect-hook)
   - [useCallback Hook](#usecallback-hook)
4. [Render Function](#render-function)
5. [Props](#props)
6. [Sidebar Links](#sidebar-links)
7. [Export](#export)

## **1. Overview** <a name="overview"></a>

The `SidebarContent.js` file defines a React functional component that manages the display and functionality of a sidebar menu. It uses hooks to manage state and lifecycle events, ensuring the sidebar reflects the current user's permissions and path settings.

## **2. Imports** <a name="imports"></a>

```javascript
import PropTypes from "prop-types";
import React, { useState, useEffect, useRef, useCallback } from "react";
import community from "../../assets/images/community.svg";
import referrals from "../../assets/images/referrals.svg";
import globalsettings from "../../assets/images/globalsettings.svg";
import demopage from "../../assets/images/demo-icon.svg";
import SimpleBar from "simplebar-react";
import MetisMenu from "metismenujs";
import { withRouter, Link } from "react-router-dom";
import { withTranslation } from "react-i18next";
import PermissionPath from "../../helpers/PermissionPath";
```

### **Purpose of Imports**

- **React and Hooks**: Used for creating the component and managing state and side effects.
- **Images**: SVG images for menu icons.
- **Libraries**: `SimpleBar` for custom scrollbars and `MetisMenu` for menu behaviors.
- **Router**: For navigation (`Link`, `withRouter`).
- **Internationalization**: `withTranslation` for translating menu items.
- **PermissionPath**: Helper for determining accessible paths based on permissions.

## **3. Functional Components** <a name="functional-components"></a>

### **useState Hook** <a name="usestate-hook"></a>

- **`allPath`**: Stores all available paths from the `PermissionPath` helper.
- **`ref`**: References the `SimpleBar` component for accessing DOM manipulation.

### **useEffect Hook** <a name="useeffect-hook"></a>

- **First `useEffect`**: Initializes the menu and checks for the current path to highlight the active menu item.
- **Second `useEffect`**: Updates the `allPath` state with all permissions paths.

### **useCallback Hook** <a name="usecallback-hook"></a>

- **`activateParentDropdown`**: Function to activate dropdowns for the current menu based on user permissions. Efficiently manages class additions to show active paths.

## **4. Render Function** <a name="render-function"></a>

The render function returns a sidebar structure encapsulated in `SimpleBar` for a smooth scrolling experience. It uses conditional rendering to display different menus based on permissions:

```jsx
return (
  <React.Fragment>
    <SimpleBar ref={ref} className="vertical-simplebar">
      <div id="sidebar-menu">
        <ul className="metismenu list-unstyled" id="side-menu">
          {props.permissions.length == 0 ? (
            // Default menu without specific permissions
            <>
              <li>
                <Link to="/reports" className="sidenav-links waves-effect">
                  <i className="mdi mdi-account-group-outline"></i>
                  <span>{props.t("Reports")}</span>
                </Link>
              </li>
              {/* Additional default links */}
            </>
          ) : (
            // Menu based on permissions
            allPath.map((item, idx) => {
              return (
                <li key={idx}>
                  <Link
                    to={item.pathname}
                    className={item.pathname === props.location.pathname ? "sidenav-links waves-effect active" : "sidenav-links waves-effect"}
                  >
                    <img src={item.icon} className="demoPage" />
                    <span>{props.t(item.label)}</span>
                  </Link>
                </li>
              );
            })
          )}
        </ul>
      </div>
    </SimpleBar>
  </React.Fragment>
);
```

## **5. Props** <a name="props"></a>

- **`location`**: Object containing the current pathname, used to highlight the active link.
- **`t`**: Translation function provided by `react-i18next`.
- **`permissions`**: Array of permission strings used to determine which paths to display in the menu.

### **PropTypes Validation**

```javascript
SidebarContent.propTypes = {
  location: PropTypes.object.isRequired,
  t: PropTypes.func.isRequired,
  permissions: PropTypes.array.isRequired,
};
```

## **6. Sidebar Links** <a name="sidebar-links"></a>

The sidebar displays different links based on the user's permissions. If no permissions are set, a default list is shown. Otherwise, links are generated dynamically from the `allPath`.

### **Default Links**

- **Reports**
- **Staff**
- **Users**
- **Games**
- **Lobbies**
- **CMS**
- **Complaints**
- **Banned Locations**
- **Community**
- **Groups**
- **Referrals**
- **Global Settings**
- **Game Demo**
- **Activity Logs**

## **7. Export** <a name="export"></a>

The component is wrapped with `withRouter` and `withTranslation` to handle routing and translation, respectively, before being exported:

```javascript
export default withRouter(withTranslation()(SidebarContent));
```

---

This documentation provides a detailed guide to the `SidebarContent.js` file, helping developers understand its structure and functionality. If there are any questions or clarifications needed, feel free to reach out! 🎉

# SidebarContentStaff.js Documentation 📚

This documentation provides a detailed overview of the `SidebarContentStaff.js` component. This component is part of a React application and is used to render a sidebar menu specifically for staff users. The sidebar includes links to various sections of the application, and it utilizes the MetisMenu for menu management and SimpleBar for custom scrollbar implementation.

## Table of Contents

1. [Component Overview](#component-overview)
2. [Imports and Dependencies](#imports-and-dependencies)
3. [Component Functionality](#component-functionality)
4. [Prop Types](#prop-types)
5. [Code Breakdown](#code-breakdown)
6. [Usage Example](#usage-example)

---

## Component Overview

The **SidebarContentStaff** component is designed to display a navigation menu intended for staff users. It dynamically highlights the active menu item based on the current route, offering a structured way to navigate through different sections of the application.

## Imports and Dependencies

The component relies on several external libraries and modules:

- **PropTypes**: For type-checking props.
- **React**: Core library for building the component.
- **SimpleBar**: Provides a custom scrollbar interface.
- **MetisMenu**: Handles the interactive and collapsible nature of the sidebar menu.
- **react-router-dom**: Manages navigation and URL routing.
- **react-i18next**: Supports internationalization.

```javascript
import PropTypes from "prop-types";
import React, { useEffect, useRef, useCallback } from "react";
import referrals from "../../assets/images/referrals.svg";
import SimpleBar from "simplebar-react";
import MetisMenu from "metismenujs";
import { withRouter } from "react-router-dom";
import { Link } from "react-router-dom";
import { withTranslation } from "react-i18next";
```

## Component Functionality

- **Menu Initialization**: Uses MetisMenu to initialize and manage the menu structure.
- **Dynamic Active State**: Highlights the menu item corresponding to the current route.
- **Custom Scrollbar**: Implements SimpleBar for a custom scrollbar experience.
- **Responsive Design**: Ensures the sidebar is responsive and accessible on various devices.

## Prop Types

The component expects the following props:

| Prop        | Type   | Description                                     |
|-------------|--------|-------------------------------------------------|
| `location`  | Object | Contains the current router location object.    |
| `t`         | Any    | Translation function provided by i18next.       |

```javascript
SidebarContentStaff.propTypes = {
  location: PropTypes.object,
  t: PropTypes.any,
};
```

## Code Breakdown

### useRef and useCallback

- **useRef**: Utilized to maintain a reference to the SimpleBar instance, allowing recalculation of its state.
- **useCallback**: Optimizes the `activateParentDropdown` function, ensuring it does not get re-instantiated on every render.

### Menu Activation

- The `activateParentDropdown` function is responsible for highlighting the active menu item and ensuring all parent elements are visible.

### useEffect Hooks

- **First useEffect**: Initializes the MetisMenu and sets up the active menu item based on the current path.
- **Second useEffect**: Recalculates the SimpleBar instance when the component is first rendered.

### Scroll Management

- The `scrollElement` function ensures that if a menu item is below the visible area, the sidebar scrolls to bring it into view.

## Usage Example

To utilize the **SidebarContentStaff** component within an application, ensure it is wrapped with routing and internationalization providers as follows:

```javascript
import SidebarContentStaff from './SidebarContentStaff';

// Usage within a main component
function App() {
  return (
    <Router>
      <SidebarContentStaff />
    </Router>
  );
}

export default withTranslation()(App);
```

By integrating the **SidebarContentStaff** component, you can provide an intuitive and responsive navigation experience for staff users within your React application. Keep in mind to handle routing and translations appropriately to fully leverage its capabilities.