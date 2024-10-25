# Rightbar.js Documentation 📚

Welcome to the documentation for the **Rightbar.js** file! This component is a part of a web application and serves as a configurable right sidebar, allowing users to customize various aspects of the application's layout and appearance. Let's dive into the details of this component.

---

## Table of Contents 🗂
1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Props](#props)
4. [Functions](#functions)
5. [UI Elements](#ui-elements)
6. [Libraries and Dependencies](#libraries-and-dependencies)
7. [Conclusion](#conclusion)

---

## Introduction

**Rightbar.js** is a React component that provides a sidebar for setting application layout configurations. It allows users to adjust settings like layout orientation, width, sidebar type, sidebar theme, topbar theme, and enables/disables a preloader. It integrates with Redux for managing state changes.

---

## Component Structure 🏗️

```jsx
import React from "react";
import PropTypes from 'prop-types';
import { FormGroup } from "reactstrap";
import { connect } from "react-redux";
import {
    changeLayout,
    changeLayoutWidth,
    changeSidebarTheme,
    changeSidebarType,
    changePreloader,
    changeTopbarTheme,
    showRightSidebarAction,
} from "../../store/actions";
import SimpleBar from "simplebar-react";
import { Link } from "react-router-dom";
import "./rightbar.scss";

// Import images
import layout1 from "../../assets/images/layouts/layout-1.jpg";
import layout2 from "../../assets/images/layouts/layout-2.jpg";
import layout3 from "../../assets/images/layouts/layout-3.jpg";

const RightSidebar = props => {
    return (
        <React.Fragment>
            {/* Right Sidebar with SimpleBar for scrolling */}
            <div className="right-bar">
                <SimpleBar style={{ height: "900px" }}>
                    {/* Content of the sidebar */}
                </SimpleBar>
            </div>
            <div className="rightbar-overlay" />
        </React.Fragment>
    );
};

// PropTypes for type-checking
RightSidebar.propTypes = {
    changeLayout: PropTypes.func,
    changeLayoutWidth: PropTypes.func,
    changePreloader: PropTypes.func,
    changeSidebarTheme: PropTypes.func,
    changeSidebarType: PropTypes.func,
    changeTopbarTheme: PropTypes.func,
    isPreloader: PropTypes.any,
    layoutType: PropTypes.any,
    layoutWidth: PropTypes.any,
    leftSideBarTheme: PropTypes.any,
    leftSideBarType: PropTypes.any,
    showRightSidebarAction: PropTypes.func,
    topbarTheme: PropTypes.any
};

// Mapping state to props
const mapStateToProps = state => {
    return {
        ...state.Layout
    };
};

// Connecting component to Redux
export default connect(mapStateToProps, {
    changeLayout,
    changeSidebarTheme,
    changeSidebarType,
    changeLayoutWidth,
    changeTopbarTheme,
    changePreloader,
    showRightSidebarAction,
})(RightSidebar);
```

---

## Props 📦

The **RightSidebar** component receives several props, which are functions and state values, primarily used to manage and update the application's layout settings.

| Prop Name         | Type       | Description                                   |
|-------------------|------------|-----------------------------------------------|
| `changeLayout`    | Function   | Updates the layout orientation (vertical/horizontal). |
| `changeLayoutWidth` | Function | Adjusts the layout width (fluid/boxed).       |
| `changePreloader` | Function   | Toggles the preloader on or off.              |
| `changeSidebarTheme` | Function | Changes the sidebar theme (light/dark/colored). |
| `changeSidebarType` | Function | Alters the sidebar type (default/compact/icon). |
| `changeTopbarTheme` | Function | Modifies the topbar theme.                    |
| `isPreloader`     | Any        | Boolean indicating the state of the preloader.|
| `layoutType`      | Any        | Current layout orientation.                   |
| `layoutWidth`     | Any        | Current layout width.                         |
| `leftSideBarTheme`| Any        | Current sidebar theme.                        |
| `leftSideBarType` | Any        | Current sidebar type.                         |
| `showRightSidebarAction` | Function | Hides or shows the right sidebar.        |
| `topbarTheme`     | Any        | Current topbar theme.                         |

---

## Functions ⚙️

The component utilizes several functions to interact with the Redux store and update the UI:

- **`changeLayout(value)`**: Updates the layout orientation based on user selection.
- **`changeLayoutWidth(value)`**: Adjusts the width of the layout.
- **`changePreloader(value)`**: Toggles the preloader spinner.
- **`changeSidebarTheme(value)`**: Changes the theme of the sidebar.
- **`changeSidebarType(value)`**: Modifies the type of sidebar displayed.
- **`changeTopbarTheme(value)`**: Changes the topbar's theme based on user input.
- **`showRightSidebarAction(value)`**: Controls the visibility of the right sidebar.

---

## UI Elements 🖥️

The sidebar includes several interactive elements:

- **Radio Buttons**: For selecting layout options such as orientation, width, and themes.
- **Checkbox**: To enable or disable the preloader functionality.
- **Images**: Display layout previews and provide links to external layout demos.
- **Links**: To navigate or trigger certain actions like closing the sidebar.

---

## Libraries and Dependencies 📚

- **React**: The core library for building the UI component.
- **PropTypes**: For type-checking the props passed to the component.
- **Reactstrap**: Provides Bootstrap 4 components for React.
- **React-Redux**: For connecting the component to the Redux store.
- **React-Router-DOM**: For handling route navigation.
- **SimpleBar**: A library for creating custom scrollbars.

---

## Conclusion 🎉

The **Rightbar.js** component is a dynamic and configurable sidebar that enhances user experience by allowing customization of the application's layout and appearance. By leveraging Redux for state management, it ensures seamless updates to the UI based on user interactions.

Feel free to explore and modify the component to suit your application's needs! For any further clarification, please refer to the comments within the code or reach out to the development team.

Happy coding! 🚀

# 📜 Documentation for `LanguageDropdown.js`

## 🎯 Overview

The `LanguageDropdown.js` file defines a **React functional component** named `LanguageDropdown`. This component is responsible for providing a dropdown menu in the user interface, allowing users to select and change the language of the application dynamically. It uses **Reactstrap** for UI components and **i18next** for internationalization.

---

## 📂 Index

- [Features](#features)
- [Component Structure](#component-structure)
- [State Management](#state-management)
- [Functionality](#functionality)
- [Usage](#usage)
- [Dependencies](#dependencies)

---

## 🌟 Features

- **Dynamic Language Selection**: Users can select a language from a dropdown menu.
- **Persistent Language Setting**: The selected language is stored in `localStorage` for consistency across sessions.
- **Responsive UI**: Utilizes Reactstrap for a responsive and modern UI.

---

## 🏗️ Component Structure

The `LanguageDropdown` component is structured as follows:

```jsx
const LanguageDropdown = () => {
  const [selectedLang, setSelectedLang] = useState("");
  const [menu, setMenu] = useState(false);

  useEffect(() => {
    const currentLanguage = localStorage.getItem("I18N_LANGUAGE");
    setSelectedLang(currentLanguage);
  }, []);

  const changeLanguageAction = lang => { /* Function to change language */ }
  const toggle = () => { /* Function to toggle dropdown */ }

  return (
    <Dropdown isOpen={menu} toggle={toggle} className="d-none d-sm-inline-block">
      <DropdownToggle className="btn header-item waves-effect" tag="button">
        <img src={get(languages, `${selectedLang}.flag`)} alt="Header Language" height="16" />
      </DropdownToggle>
      <DropdownMenu className="dropdown-menu-end" right>
        {map(Object.keys(languages), key => (
          <DropdownItem key={key} onClick={() => changeLanguageAction(key)} className={`notify-item ${selectedLang === key ? "active" : "none"}`}>
            <img src={get(languages, `${key}.flag`)} alt="Qovex" className="me-1" height="12" />
            <span className="align-middle">{get(languages, `${key}.label`)}</span>
          </DropdownItem>
        ))}
      </DropdownMenu>
    </Dropdown>
  );
}
```

---

## 🗃️ State Management

| State Variable | Type    | Description                                              |
|----------------|---------|----------------------------------------------------------|
| `selectedLang` | String  | Stores the currently selected language code.             |
| `menu`         | Boolean | Tracks the open state of the dropdown menu (open/close). |

---

## ⚙️ Functionality

### `useEffect`

- **Purpose**: Initializes the `selectedLang` state with the language stored in `localStorage` when the component mounts.

### `changeLanguageAction(lang)`

- **Purpose**: Changes the application's language.
- **Process**:
  1. Updates the language setting in `i18n`.
  2. Stores the selected language in `localStorage`.
  3. Updates the `selectedLang` state.

### `toggle()`

- **Purpose**: Toggles the visibility of the dropdown menu.

### Dropdown Rendering

- **DropdownToggle**: Displays the currently selected language's flag.
- **DropdownMenu**: Lists all available languages as `DropdownItem`s, allowing users to change the language.

---

## 📜 Usage

Integrating the `LanguageDropdown` component into an application is straightforward. Here's an example:

```jsx
import LanguageDropdown from './path/to/LanguageDropdown';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <LanguageDropdown />
      </header>
    </div>
  );
}
```

---

## 📦 Dependencies

- **React**: For building the component and managing state.
- **Reactstrap**: Provides the dropdown UI components.
- **lodash**: Utilized for its utility functions like `get` and `map`.
- **i18next**: Manages the internationalization and language changes.
- **withTranslation**: Higher-order component for enhancing the component with translation capabilities.

---

This documentation provides a comprehensive overview of how the `LanguageDropdown` component works and how it can be integrated into any React application to manage language settings dynamically. 🌐📘

# NotificationDropdown.js Documentation 📬

Welcome to the detailed documentation of the **NotificationDropdown.js** component. This file is an essential React component that provides a dropdown menu for displaying notifications in a user interface.

## Index 📑

1. [Overview](#overview)
2. [Component Breakdown](#component-breakdown)
3. [Props](#props)
4. [State Variables](#state-variables)
5. [Dependencies](#dependencies)
6. [Code Walkthrough](#code-walkthrough)
7. [Styling and Layout](#styling-and-layout)

---

## Overview 📖

The **NotificationDropdown** component is a part of a user interface that allows users to view notifications in a dropdown format. It provides an interactive menu that can be toggled open or closed, displaying a list of notification items. Each notification item includes information such as the notification title, a brief message, and a timestamp.

## Component Breakdown ⚙️

The component is structured as follows:

- **Dropdown**: The main container for the dropdown menu.
- **DropdownToggle**: A button that toggles the visibility of the dropdown menu.
- **DropdownMenu**: Contains the actual notification items displayed when the dropdown is active.
- **Notification Items**: Individual notifications, each comprising an icon or avatar, title, message, and timestamp.

## Props 🎁

The component uses the following prop:

| Prop | Type     | Description                              |
|------|----------|------------------------------------------|
| `t`  | `any`    | Translation function for multi-language support. |

## State Variables 🗄️

The component maintains the following state variable:

- **menu**: A boolean state (`true` or `false`) that controls the visibility of the dropdown menu.

## Dependencies 📦

This component relies on several external libraries and assets:

- **React**: For building the component.
- **PropTypes**: For type-checking the props.
- **Reactstrap**: For UI components like `Dropdown`, `DropdownToggle`, and `DropdownMenu`.
- **SimpleBar**: To provide a custom scrollbar for the notifications list.
- **withTranslation**: From `react-i18next` for internationalization and translation support.
- **Avatar images**: Imported images are used for user notifications.

## Code Walkthrough 🛠️

```javascript
import React, { useState } from "react";
import PropTypes from 'prop-types';
import { Link } from "react-router-dom";
import { Dropdown, DropdownToggle, DropdownMenu, Row, Col } from "reactstrap";
import SimpleBar from "simplebar-react";

// Import images
import avatar3 from "../../../assets/images/users/avatar-3.jpg";
import avatar4 from "../../../assets/images/users/avatar-4.jpg";

// i18n
import { withTranslation } from "react-i18next";
```

### Functionality

1. **State Management**: 
   - The `menu` state is used to toggle the dropdown visibility.
   - `useState` hook initializes and manages the `menu` state.

2. **Dropdown Toggle**:
   - The `DropdownToggle` button toggles the `menu` state, which in turn shows or hides the `DropdownMenu`.

3. **Notifications Display**:
   - The notifications are wrapped in individual `Link` components, providing clickable items.

4. **Custom Scrollbar**:
   - `SimpleBar` is used to wrap the list of notifications, offering a smooth scrolling experience.

### Example Usage

The component can be included in a top navigation bar to display notifications for the user. The notifications update dynamically and can be extended with additional data.

## Styling and Layout 🎨

- **Icons and Badges**: Used to provide visual cues for user interaction (`mdi-bell-outline`, `badge` for notification count).
- **Responsive Design**: Utilizes Bootstrap grid system (`Row`, `Col`) for layout management.
- **Interactive Elements**: All notifications are encapsulated in `Link` components ensuring they are interactive.

---

By using this component, developers can easily integrate a notification dropdown in their applications, enhancing the user experience with interactive and translated notifications. The component is designed to be responsive and customizable to fit various UI needs.

# ProfileMenu.js Documentation

Welcome to the documentation for the **ProfileMenu.js** file! This component is part of a React application and handles user profile interactions, specifically allowing users to log out and navigate to the change password page.

## Table of Contents
1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [State Variables](#state-variables)
4. [Props](#props)
5. [Functions](#functions)
6. [UI and JSX Structure](#ui-and-jsx-structure)
7. [Dependencies](#dependencies)
8. [Usage](#usage)

---

## Introduction

The `ProfileMenu` component is a dropdown menu located in the application's header. It allows users to:
- Change their password
- Log out of the application

The component utilizes React's state management to control the visibility of the dropdown and handle asynchronous logout operations.

---

## Component Structure

Below is an overview of the structure of the `ProfileMenu.js` file:

```javascript
import React, { useState, useEffect } from "react";
import PropTypes from "prop-types";
import {
  Dropdown,
  DropdownToggle,
  DropdownMenu,
  DropdownItem,
  Button,
} from "reactstrap";
import { withRouter, Link } from "react-router-dom";
import { logoutuserEvent } from "../../../services/auth_api_helper";
import Loader from "../../Common/Loader";

const ProfileMenu = (props) => {
  // State variables
  const [menu, setMenu] = useState(false);
  const [username, setusername] = useState(null);
  const [isLoading, setisLoading] = useState(false);

  // Effects
  useEffect(() => {
    if (localStorage.getItem("authUser")) {
      const obj = JSON.parse(localStorage.getItem("authUser"));
      setusername(obj.extras.username);
    }
  }, [props.success]);

  // Functions
  const handleLogout = async () => {
    setisLoading(true);
    await logoutuserEvent()
      .then((res) => {
        localStorage.removeItem("authUser");
        props.history.push("/login");
        window.location.reload();
        setisLoading(false);
      })
      .catch(() => {
        setisLoading(false);
      });
  };

  return (
    <React.Fragment>
      <Loader showLoader={isLoading} />
      <Dropdown isOpen={menu} toggle={() => setMenu(!menu)} className="d-inline-block">
        <DropdownToggle className="btn header-item waves-effect" id="page-header-user-dropdown" tag="button">
          <span className="d-inline-block ms-1">{username}</span>{" "}
          <i className="mdi mdi-chevron-down d-inline-block"></i>{" "}
        </DropdownToggle>
        <DropdownMenu className="dropdown-menu-end">
          <DropdownItem>
            <Link to="/change-password" className="dropdown-item text-danger">
              <svg width="15" height="15" fill="none" className="me-1">
                <!-- SVG Path -->
              </svg>
              <span>Change password</span>
            </Link>
          </DropdownItem>
          <DropdownItem>
            <Button color="link" onClick={handleLogout} disabled={isLoading}>
              <i className="bx bx-power-off font-size-16 align-middle text-danger"></i>{" "}
              <span className="logoutSpan">Logout</span>
            </Button>
          </DropdownItem>
        </DropdownMenu>
      </Dropdown>
    </React.Fragment>
  );
};

ProfileMenu.propTypes = {
  success: PropTypes.any,
  t: PropTypes.any,
};

export default withRouter(ProfileMenu);
```

---

## State Variables

- **`menu`**: A boolean state that controls the visibility of the dropdown menu.
- **`username`**: Stores the username fetched from local storage.
- **`isLoading`**: A boolean state that indicates if the logout process is ongoing.

---

## Props

| Prop      | Type     | Description                                      |
|-----------|----------|--------------------------------------------------|
| `success` | `any`    | Used to trigger effects based on success status. |
| `t`       | `any`    | Translation function (i18n).                     |

---

## Functions

- **`handleLogout`**: Asynchronously logs the user out by calling `logoutuserEvent`. It removes the user data from local storage and redirects to the login page.

- **`setMenu`**: Toggles the menu's visibility.

---

## UI and JSX Structure

The component's UI is structured with Reactstrap's Dropdown components:

- **Dropdown**: Contains the profile options.
- **DropdownToggle**: Displays the username and a downward chevron icon.
- **DropdownMenu**: Contains options to change password and log out.
- **Loader**: Displays a loading spinner during logout operations.

---

## Dependencies

- **React**: Core library for building UI components.
- **Reactstrap**: Bootstrap components for React.
- **React Router**: For handling navigation and routing.
- **i18next**: For internationalization and translations.
- **PropTypes**: Type-checking for props.

---

## Usage

To integrate the `ProfileMenu` component into a React application:

1. **Import the Component**:
   ```javascript
   import ProfileMenu from 'path/to/ProfileMenu';
   ```

2. **Use within a Component**:
   ```javascript
   const Header = () => (
     <header>
       <ProfileMenu />
     </header>
   );
   ```

This component provides a seamless way for users to interact with their profile settings and manage account actions within the application.

---

Thank you for using the ProfileMenu component! If you have further questions or need assistance, please refer to the source code or contact the development team.