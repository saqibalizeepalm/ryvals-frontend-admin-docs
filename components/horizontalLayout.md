# 📄 Footer.js Documentation

## Overview

The `Footer.js` file is a React component responsible for rendering the footer section of a web application. This component utilizes the `reactstrap` library to handle layout and styling, providing a responsive and easily customizable footer for your web pages.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Component Structure](#component-structure)
4. [Code Explanation](#code-explanation)
5. [Styling](#styling)
6. [Conclusion](#conclusion)

---

## Introduction

The **Footer** component is a functional component in React that serves as the bottom section of a webpage. It is designed to display copyright information and credits for design and development. The component utilizes the `reactstrap` library, which is based on Bootstrap, to ensure responsiveness across various devices.

## Installation

To use this component, ensure you have the following dependencies installed:

```bash
npm install react react-dom reactstrap
```

## Component Structure

The **Footer** component is structured using React and `reactstrap` components. Here's a breakdown of its structure:

- **React.Fragment**: Encapsulates the footer to avoid adding extra nodes to the DOM.
- **footer**: Main HTML element to denote the footer section.
- **Container**: A responsive fixed-width container from `reactstrap`.
- **Row**: A flexbox container for organizing columns within the `Container`.
- **Col**: A column for arranging content inside the `Row`.

## Code Explanation

Let's break down the code in `Footer.js`:

```javascript
import React from "react";
import { Container, Row, Col } from "reactstrap";

const Footer = () => {
  return (
    <React.Fragment>
      <footer className="footer">
        <Container fluid={true}>
          <Row>
            <Col md={6}>{new Date().getFullYear()} © Qovex.</Col>
            <Col md={6}>
              <div className="text-sm-end d-none d-sm-block">
                Design & Develop by Themesbrand
              </div>
            </Col>
          </Row>
        </Container>
      </footer>
    </React.Fragment>
  );
}

export default Footer;
```

### Key Points:

- **Dynamic Year**: The footer displays the current year dynamically using `new Date().getFullYear()`.
- **Company Name**: Displays `© Qovex` as the company name.
- **Credits**: Provides credit for design and development by "Themesbrand".
- **Responsive Layout**: Uses `Row` and `Col` from `reactstrap` to ensure the footer is responsive and adapts to different screen sizes.

## Styling

The styling for this component is managed through classes like `footer`, `text-sm-end`, `d-none`, and `d-sm-block`. These classes are typically defined in an external CSS file or are part of the Bootstrap framework.

- **footer**: Custom class for the footer section.
- **text-sm-end**: Aligns text to the end on small devices and up.
- **d-none d-sm-block**: Hides the element on extra-small devices and displays it on small devices and up.

## Conclusion

The **Footer.js** file provides a simple yet effective way to implement a responsive footer in a React application. It leverages the power of `reactstrap` for layout management and ensures that the footer content is always up-to-date and professionally displayed.

Feel free to customize the text and styling to better suit your application's branding and requirements. The structure provided can be easily extended with additional content or links as needed.

# 📜 Documentation for `Header.js`

## 📑 Index

1. [Introduction](#introduction)
2. [Component Functionality](#component-functionality)
3. [Code Breakdown](#code-breakdown)
4. [PropTypes](#proptypes)
5. [Redux Integration](#redux-integration)
6. [Internationalization (i18n)](#internationalization-i18n)
7. [Conclusion](#conclusion)

## Introduction

The `Header.js` file is a **React component** designed to serve as the header section of a web application UI. It integrates with Redux for state management and i18next for internationalization. This component includes interactive features such as a responsive navbar, search functionality, language selection, and a user profile menu.

## Component Functionality

The `Header` component is responsible for:

- Displaying the application’s logo.
- Toggling the left sidebar menu.
- Managing fullscreen toggle functionality.
- Incorporating a search feature.
- Providing access to language selection and user profile settings.
- (Commented out) Notification dropdown feature.

## Code Breakdown

The `Header.js` file imports necessary dependencies and defines a functional component. It uses hooks and Redux for state management and includes several interactive elements.

### 🧩 Imports

```javascript
import React, { useState } from "react";
import PropTypes from "prop-types";
import { connect } from "react-redux";
import { Link } from "react-router-dom";
```

- **React & Hooks**: Used to build the component and manage local state with `useState`.
- **PropTypes**: For type-checking the props passed to the component.
- **Redux**: Connects to the Redux store for state management.
- **React Router**: Provides navigation functionality within the app.

### 📦 Redux Actions

```javascript
import { showRightSidebarAction, toggleLeftmenu } from "../../store/actions";
```

These actions help manage the visibility of the right sidebar and the state of the left menu.

### 🖼️ Assets & Components

```javascript
import logo from "../../assets/images/ryvals-logo.png";
import Navbar from "./Navbar";
```

- **Logos**: Different versions of the application logo.
- **Navbar**: A separate component for the navigation bar.

### 🌐 Internationalization

```javascript
import { withTranslation } from "react-i18next";
```

Allows the component to support multiple languages using the `i18next` library.

### 🛠️ Component Definition

```javascript
const Header = (props) => {
    const [isSearch, setSearch] = useState(false);

    function toggleFullscreen() {
        // Fullscreen toggle logic
    }

    return (
        <React.Fragment>
            <div className="navbar-header">
                <div className="d-flex">
                    <div className="navbar-brand-box">
                        {/* Logo links */}
                    </div>
                    <button type="button" className="btn btn-sm px-3 font-size-16 d-lg-none header-item"
                        onClick={() => { props.toggleLeftmenu(!props.leftMenu); }}>
                        <i className="fa fa-fw fa-bars" />
                    </button>
                    <Navbar menuOpen={isMenuOpened} />
                </div>
                <div className="d-flex">
                    {/* Search, Language, Profile, and Settings */}
                </div>
            </div>
        </React.Fragment>
    );
};
```

- **State Management**: Utilizes `useState` for the search feature.
- **Fullscreen Functionality**: The `toggleFullscreen` function provides a way to switch the view to fullscreen mode.
- **Responsive Design**: Includes breakpoints for different screen sizes.

## PropTypes

```javascript
Header.propTypes = {
    leftMenu: PropTypes.any,
    showRightSidebar: PropTypes.any,
    showRightSidebarAction: PropTypes.func,
    t: PropTypes.any,
    toggleLeftmenu: PropTypes.func,
};
```

Defines the expected types for each prop, ensuring the component receives the correct data types from its parent or Redux store.

## Redux Integration

The component is connected to the Redux store, allowing it to dispatch actions and access the state:

```javascript
const mapStatetoProps = (state) => {
    const { layoutType, showRightSidebar, leftMenu } = state.Layout;
    return { layoutType, showRightSidebar, leftMenu };
};

export default connect(mapStatetoProps, { showRightSidebarAction, toggleLeftmenu, })(withTranslation()(Header));
```

- **mapStatetoProps**: Retrieves the necessary state attributes from the Redux store.
- **connect**: Connects the component to the Redux store for dispatching actions and subscribing to state changes.

## Internationalization (i18n)

The component uses the `withTranslation` higher-order component to provide translated text:

```javascript
export default withTranslation()(Header);
```

This allows the header to display content in different languages based on user preferences.

## Conclusion

The **Header component** is a dynamic and versatile part of the web application. It integrates multiple functionalities such as Redux for state management, responsive design, and internationalization. By providing an interactive and user-friendly UI, this component enhances the overall user experience of the application.

# 📄 Documentation for `index.js`

## Table of Contents
1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [State Management](#state-management)
4. [Lifecycle Methods](#lifecycle-methods)
5. [Rendering Logic](#rendering-logic)
6. [PropTypes](#proptypes)
7. [Redux Integration](#redux-integration)
8. [Conclusion](#conclusion)

## Introduction
The `index.js` file serves as the main layout component for a React application. It incorporates various sub-components like the `Header`, `Footer`, and an optional `Rightbar`. The layout is responsible for handling the overall structure and theme-specific settings, ensuring a consistent look and feel across the application.

## Component Structure
The `index.js` file defines a `Layout` component as a class component, making it a stateful component that provides lifecycle methods and local state management:

- **Imports**
  - **React** and **PropTypes** for defining and validating component props.
  - **Redux** functions for connecting the component to the global state.
  - **React Router** to enhance component functionality with routing capabilities.
  - Various sub-components (`Header`, `Footer`, `Rightbar`) and Redux actions (`changeLayout`, `changeTopbarTheme`, `changeLayoutWidth`).

- **Sub-components**
  - `Header`: Displays the top navigation bar, customizable with themes.
  - `Footer`: Displays the footer section.
  - `Rightbar`: An optional component that can be toggled to show additional options or settings.

## State Management
The component maintains a local state with the following key:

- `isMenuOpened`: A boolean value used to track whether the mobile menu is open or closed.

### State Initialization
```javascript
constructor(props) {
    super(props);
    this.state = {
        isMenuOpened: false,
    };
}
```

## Lifecycle Methods
The `Layout` component utilizes the `componentDidMount` lifecycle method to perform operations immediately after the component is mounted:

- **Preloader Handling**: Displays a loading spinner if `isPreloader` is true, and hides it after a set timeout.
- **Document Title**: Sets the document title to "Ryvals".
- **Theme and Layout Configuration**: Applies the theme and layout settings from the Redux store using the provided prop values.

### Example Usage
```javascript
componentDidMount() {
    if (this.props.isPreloader === true) {
        document.getElementById("preloader").style.display = "block";
        document.getElementById("status").style.display = "block";
        setTimeout(function () {
            document.getElementById("preloader").style.display = "none";
            document.getElementById("status").style.display = "none";
        }, 2500);
    }
    window.scrollTo(0, 0);
    document.title = "Ryvals";
    this.props.changeLayout("horizontal");
    if (this.props.topbarTheme) {
        this.props.changeTopbarTheme(this.props.topbarTheme);
    }
    if (this.props.layoutWidth) {
        this.props.changeLayoutWidth(this.props.layoutWidth);
    }
}
```

## Rendering Logic
The `render` method is responsible for the layout's HTML structure, embedding it in a responsive container. It includes logic to conditionally display the `Rightbar` component based on a prop value.

### Example Render Method
```javascript
render() {
    return (
        <React.Fragment>
            <div id="preloader">
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
            <div className="container-fluid">
                <div id="layout-wrapper">
                    <header id="page-topbar">
                        <Header theme={this.props.topbarTheme} isMenuOpened={this.state.isMenuOpened} openLeftMenuCallBack={this.openMenu} />
                    </header>
                    <div className="main-content">
                        {this.props.children}
                        <Footer />
                    </div>
                </div>
            </div>
            {this.props.showRightSidebar ? <Rightbar /> : null}
        </React.Fragment>
    );
}
```

## PropTypes
The `Layout` component is equipped with PropTypes for type-checking props, ensuring that incorrect prop usage is caught during development.

| Prop Name           | Type     | Description                                  |
|---------------------|----------|----------------------------------------------|
| `changeLayout`      | Function | Action to change the layout type.            |
| `changeLayoutWidth` | Function | Action to change the layout width.           |
| `changeTopbarTheme` | Function | Action to change the topbar theme.           |
| `children`          | Object   | Child components to be rendered inside main content. |
| `isPreloader`       | Any      | Determines if the preloader should be shown. |
| `layoutWidth`       | Any      | Width of the layout (e.g., full, boxed).     |
| `location`          | Object   | The current route location object.           |
| `showRightSidebar`  | Any      | Controls the visibility of the right sidebar.|
| `topbarTheme`       | Any      | Theme style for the topbar.                  |

## Redux Integration
The component connects to the Redux store using the `connect` function, allowing it to map state and dispatch actions as props.

### mapStatetoProps
This function maps the relevant parts of the Redux state to component props.

```javascript
const mapStatetoProps = (state) => {
    return {
        ...state.Layout,
    };
};
```

### Export
The component is wrapped with `connect` and `withRouter` before being exported, providing it with routing capabilities and access to the Redux store.

```javascript
export default connect(mapStatetoProps, {
    changeTopbarTheme,
    changeLayout,
    changeLayoutWidth,
})(withRouter(Layout));
```

## Conclusion
The `index.js` file provides a comprehensive layout component that integrates crucial UI elements, manages layout and theme settings, and connects to the Redux store for dynamic state management. With well-structured PropTypes and lifecycle methods, it ensures a scalable and maintainable architecture for the application's layout.

# Navbar.js Documentation

*Welcome to the comprehensive documentation for the **Navbar.js** component! This file is an integral part of your React application, providing a dynamic and interactive navigation bar for users.*

---

## 📚 **Table of Contents**

1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [State Variables](#state-variables)
4. [Effects and Functions](#effects-and-functions)
5. [Render Method](#render-method)
6. [Prop Types](#prop-types)
7. [Redux Integration](#redux-integration)
8. [Conclusion](#conclusion)

---

## 🌟 **Introduction**

The **Navbar.js** file is a React component that constructs a responsive, multi-level navigation bar. It facilitates easy navigation through different sections of the application with dropdown menus and supports internationalization.

---

## 🧩 **Component Overview**

```javascript
import PropTypes from "prop-types";
import React, { useState, useEffect } from "react";
import { Row, Col, Collapse } from "reactstrap";
import { Link, withRouter } from "react-router-dom";
import classname from "classnames";
import { withTranslation } from "react-i18next";
import { connect } from "react-redux";
```

- **Imports**:
  - **React**: Core library for building UI components.
  - **Reactstrap**: Provides Bootstrap 4 components for React.
  - **React Router**: Manages navigation in a React app.
  - **i18next**: Internationalization library for supporting multiple languages.
  - **Redux**: State management library to connect component state to the global store.

---

## 🏗️ **State Variables**

- `dashboard`, `ui`, `app`, `email`, `task`, `component`, `form`, `table`, `chart`, `icon`, `map`, `extra`: **Boolean state variables** that handle the toggle state for dropdown menus.

### Example:

```javascript
const [dashboard, setdashboard] = useState(false);
```

These states are used to track whether the corresponding dropdown menu is open or closed.

---

## ⚙️ **Effects and Functions**

### **useEffect**:
- This hook is utilized to activate parent dropdowns based on the current path, ensuring that the correct menu item is highlighted when the page loads.

```javascript
useEffect(() => {
  var matchingMenuItem = null;
  var ul = document.getElementById("navigation");
  var items = ul.getElementsByTagName("a");
  
  for (var i = 0; i < items.length; ++i) {
    if (props.location.pathname === items[i].pathname) {
      matchingMenuItem = items[i];
      break;
    }
  }
  
  if (matchingMenuItem) {
    activateParentDropdown(matchingMenuItem);
  }
});
```

### **activateParentDropdown**:
- A function to add the class `active` to the selected menu item and its parent elements for styling and visibility purposes.

```javascript
function activateParentDropdown(item) {
  item.classList.add("active");
  const parent = item.parentElement;
  if (parent) {
    parent.classList.add("active");
    // Continues up to 6 levels of parent elements
  }
  return false;
}
```

---

## 🖼️ **Render Method**

The render method constructs the navigation bar using **React Fragment** and **Reactstrap's Collapse** component. It includes:

- **Dropdown Menus**: Each menu item can expand/collapse based on its state.
- **Links**: Navigation links that leverage `react-router-dom` for in-app navigation.

### Example:

```javascript
<li className="nav-item dropdown">
  <Link to="/#" onClick={e => { e.preventDefault(); setapp(!app); }} className="nav-link dropdown-toggle arrow-none">
    {props.t("Apps")} <div className="arrow-down"></div>
  </Link>
  <div className={classname("dropdown-menu", { show: app })}>
    <Link to="calendar" className="dropdown-item"> {props.t("Calendar")} </Link>
  </div>
</li>
```

This snippet showcases a dropdown menu for "Apps" that toggles open/close when clicked.

---

## 🧩 **Prop Types**

The component defines expected prop types using `PropTypes` to ensure correct data types for:

- `leftMenu`: Controls the visibility of the left menu.
- `location`: Provides the current route information.
- `menuOpen`: Boolean to handle menu open state.
- `t`: Function for translating strings.

### Example:

```javascript
Navbar.propTypes = {
  leftMenu: PropTypes.any,
  location: PropTypes.any,
  menuOpen: PropTypes.any,
  t: PropTypes.any,
};
```

---

## 🔗 **Redux Integration**

- **mapStatetoProps**: Connects the component to the Redux store to access the `leftMenu` state.

```javascript
const mapStatetoProps = state => {
  const { leftMenu } = state.Layout;
  return { leftMenu };
};
```

- **withRouter**: Enhances the component to access the router's state and properties.

- **withTranslation**: Wraps the component to enable multi-language support.

### Export:

```javascript
export default withRouter(connect(mapStatetoProps, {})(withTranslation()(Navbar)));
```

---

## 🏁 **Conclusion**

The **Navbar.js** component is a robust and dynamic part of your React application. It provides users with an intuitive navigation experience, supporting multiple languages and responsive design. By integrating Redux, it ensures state management is handled effectively across your application.

---

*Feel free to explore, modify, and expand this component to suit your application needs!* 🎉