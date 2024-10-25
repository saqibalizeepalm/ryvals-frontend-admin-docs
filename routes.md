# 📚 AllRoutes.js Documentation

Welcome to the comprehensive documentation for the **`allRoutes.js`** file. This file is a crucial component of a React application that manages routing. It defines and exports two sets of routes: `userRoutes` and `authRoutes`. These routes are essential for navigating different pages within the application, especially in the context of user authentication and authorization.

---

## 📑 **Index**

1. [Overview](#overview)
2. [Import Statements](#import-statements)
3. [Local Storage Check](#local-storage-check)
4. [Common Paths Definition](#common-paths-definition)
5. [User Routes](#user-routes)
6. [Auth Routes](#auth-routes)
7. [Route Export](#route-export)
8. [Conclusion](#conclusion)

---

## 🎯 **Overview**

The **`allRoutes.js`** file contains the configuration for client-side routing in a React application using `react-router-dom`. It defines which components should be rendered for specific URL paths, contributing to the smooth navigation experience in a Single Page Application (SPA).

---

## 📥 **Import Statements**

The file begins by importing various React components and utility functions required for routing. These imports include:

- **React** and **Redirect** from `react-router-dom` for routing capabilities.
- Pages for handling errors and specific features, such as `Pages404`, `Pages500`, etc.
- Authentication-related pages like `Login`, `Logout`, etc.
- Inner pages including user lists, game lists, and more.
- Utility functions for permissions and local storage.

Here's a snippet showing some of the imports:

```javascript
import React from "react";
import { Redirect } from "react-router-dom";
import Pages404 from "../pages/Utility/pages-404";
import Pages500 from "../pages/Utility/pages-500";
import Login from "../pages/Authentication/Login";
import Logout from "../pages/Authentication/Logout";
import { getFromLocalStorage } from "../helpers/util";
```

---

## ✅ **Local Storage Check**

The file checks the local storage to determine if an authenticated user is present. This check is used to decide whether certain pages (like static pages) should be included in the routes:

```javascript
const obj = getFromLocalStorage("authUser");
const notFound = obj === null ? true : obj.extras?.permissions.some((objItem) => {
  return objItem.label === "Static Page";
});
```

- **`getFromLocalStorage("authUser")`**: Retrieves the authenticated user details from local storage.
- **`notFound`**: A boolean flag that indicates whether the user has access to "Static Page" permissions.

---

## 🛤️ **Common Paths Definition**

The `commonPath` array defines routes that are always included, regardless of the user's permissions:

```javascript
const commonPath = [
  { path: "/users", component: UserList, commonName: "/users", codename: "view_user" },
  { path: "/games", component: GamesList, commonName: "/games", codename: "view_game" },
  // More routes here...
];
```

Each object in the array represents a route with properties:

- **`path`**: The URL path.
- **`component`**: The component to render.
- **`commonName`** and **`codename`**: Additional metadata for permissions, if applicable.

---

## 👥 **User Routes**

The `userRoutes1` array is conditionally defined based on the `notFound` flag, incorporating common paths and additional pages if necessary:

```javascript
const userRoutes1 = notFound ? [
  ...commonPath,
  { path: "/cms", component: CMS, commonName: "/cms", codename: "view_staticpage" },
  { path: "/", exact: true, component: () => <Redirect to="/users" /> },
] : [
  ...commonPath,
  { path: "/cms", component: CMS, commonName: "/cms", codename: "view_question" },
  { path: "/", exact: true, component: () => <Redirect to="/users" /> },
];
```

- **`userRoutes1`**: Includes paths from `commonPath` and additional conditional routes.
- **Redirect**: Defaults to the `/users` page if no specific route is matched.

Also, it defines `userRoutes` using a filtering function for permissions:

```javascript
const filterOutGivenPermissionPath = SearchPath(userRoutes1);
const findPaths = filterOutGivenPermissionPath == null ? userRoutes1 : findPathsBetweenTwo(filterOutGivenPermissionPath);
const userRoutes = filterOutGivenPermissionPath == null ? userRoutes1 : findPaths;
```

---

## 🔐 **Auth Routes**

The `authRoutes` array lists routes associated with authentication tasks:

```javascript
const authRoutes = [
  { path: "/login", component: Login },
  { path: "/forgot-password", component: ForgetPwd },
  { path: "/reset-password", component: ResetPassword },
  { path: "/pages-404", component: Pages404 },
  { path: "/pages-500", component: Pages500 },
];
```

- **`authRoutes`**: Contains routes for logging in, password management, and error handling.

---

## 📤 **Route Export**

Finally, the file exports `userRoutes` and `authRoutes` for use in other parts of the application:

```javascript
export { userRoutes, authRoutes };
```

---

## 🎉 **Conclusion**

The **`allRoutes.js`** file is an essential part of the routing mechanism in this React application. It dynamically configures routes based on user permissions and authentication status, providing a robust foundation for navigational logic in the app.

Feel free to explore and customize this setup as per your application's requirements! 🚀

# Documentation for Authmiddleware.js 📄

**Authmiddleware.js** is a middleware component in a React application that manages routing based on user authentication and permission levels. It ensures that users are redirected appropriately based on their authentication status and permissions when trying to access different routes.

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Props](#component-props)
4. [Functionality](#functionality)
5. [Usage](#usage)
6. [Code Breakdown](#code-breakdown)
7. [Conclusion](#conclusion)

---

## Introduction 🌟

The **Authmiddleware** component acts as a gatekeeper for route access in a React application. It determines whether a user is authenticated and decides if they should be granted access to a specific route or redirected to a login page. Additionally, it handles route permissions, ensuring that users can only access routes they have permission for.

## Dependencies 📦

The following libraries are imported and used in this component:

- **React**: A JavaScript library for building user interfaces.
- **PropTypes**: A library for type-checking props in React components.
- **react-router-dom**: A collection of navigational components that compose declaratively with your application.

Additionally, the component imports utility functions and data:

- **userRoutes**: From `allRoutes.js`, which provides the application's route definitions.
- **PermissionPath**: A helper function to manage permission-based routing.
- **getFromLocalStorage**: A utility function to retrieve data from local storage.

## Component Props 🧩

The **Authmiddleware** component expects the following props:

| Prop Name       | Type          | Description                                                                 |
|-----------------|---------------|-----------------------------------------------------------------------------|
| `component`     | `Component`   | The component to render if access is granted.                               |
| `layout`        | `Layout`      | The layout component that wraps around the rendered component.              |
| `isAuthProtected` | `bool`     | Determines if the route requires authentication.                            |
| `permission`    | `any`         | Permissions required to access the route.                                   |
| `path`          | `string`      | The path of the route.                                                      |
| `...rest`       | `object`      | Any additional props to pass down to the `Route` component.                 |

## Functionality ⚙️

1. **Authentication Check**:
   - If the route is protected (`isAuthProtected = true`), the component checks if the user is authenticated.
   - If unauthenticated, the user is redirected to the login page.

2. **Permission Check**:
   - If the route is protected, the component checks the user's permissions.
   - Renders the component if the user has the necessary permissions, otherwise redirects.

3. **Redirection Logic**:
   - For authenticated users, redirects them to a path based on their permissions.
   - For unauthenticated users trying to access public routes, renders the component directly.

## Usage 🛠️

To use **Authmiddleware**, wrap your route definitions with this component to enforce authentication and permission checks. Ensure that your routes are correctly defined in `allRoutes.js` and that user permissions are managed properly.

## Code Breakdown 🧵

Here's a detailed look at the code:

```javascript
import React from "react";
import PropTypes from "prop-types";
import { Route, Redirect } from "react-router-dom";
import { userRoutes } from "../allRoutes";
import PermissionPath from "../../helpers/PermissionPath";
import { getFromLocalStorage } from "../../helpers/util";

const Authmiddleware = ({ component: Component, layout: Layout, isAuthProtected, permission, path, ...rest }) => {
    const user = getFromLocalStorage("authUser");

    return (
        <Route
            {...rest}
            render={(props) => {
                const redirectPath = PermissionPath();

                if (isAuthProtected && !user) {
                    return (
                        <Redirect to={{ pathname: "/login", state: { from: props.location } }} />
                    );
                }

                if (!isAuthProtected && user) {
                    return (
                        <Redirect to={{
                            pathname: user ? redirectPath[1]?.pathname : path,
                            state: { from: user ? redirectPath[1]?.pathname : props.location },
                        }} />
                    );
                }

                if (isAuthProtected) {
                    if (!user) {
                        return (
                            <Redirect to={{ pathname: "/login", state: { from: props.location } }} />
                        );
                    } else {
                        return (
                            <Layout>
                                <Component {...props} permission={permission !== null ? permission : user?.extras?.permissions?.length ? user.extras.permissions : null} />
                            </Layout>
                        );
                    }
                } else {
                    if (user) {
                        return (
                            <Redirect to={{ pathname: userRoutes[0].path }} />
                        );
                    } else {
                        return (
                            <Layout>
                                <Component {...props} />
                            </Layout>
                        );
                    }
                }
            }}
        />
    );
};

Authmiddleware.propTypes = {
    isAuthProtected: PropTypes.bool,
    component: PropTypes.any,
    location: PropTypes.object,
    permission: PropTypes.any,
    layout: PropTypes.any,
};

export default Authmiddleware;
```

### Key Points:
- **Route Configuration**: Uses the `Route` component from `react-router-dom` to define the rendering logic.
- **Redirection**: Uses `Redirect` to navigate users based on their authentication state and permissions.
- **Conditionals**: Logical checks determine the flow of rendering or redirecting.

## Conclusion ✅

The **Authmiddleware.js** component plays a crucial role in managing user access to different parts of a React application, ensuring security and proper access control. It effectively handles authentication and permission checks, making the application robust and user-centric. By using this middleware, developers can maintain clear and secure routing logic within their applications.