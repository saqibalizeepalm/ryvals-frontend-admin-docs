# 📄 UserList.js Documentation

Welcome to the comprehensive documentation for `UserList.js`! This file is a React component that serves as a user management interface in a web application. It provides functionalities for listing, searching, sorting, and modifying user data. Below is a detailed explanation of the code, its components, and its purpose.

## Index

1. [📋 Overview](#overview)
2. [📦 Imports](#imports)
3. [🔧 State Management](#state-management)
4. [📜 useEffect Hooks](#useeffect-hooks)
5. [🔍 Search and Filter](#search-and-filter)
6. [🔄 User Activation/Deactivation](#user-activationdeactivation)
7. [🛠️ Editing User Details](#editing-user-details)
8. [🧩 Render Function](#render-function)
9. [👥 User Table](#user-table)
10. [⚙️ Utilities and Helpers](#utilities-and-helpers)
11. [📬 Modals and Alerts](#modals-and-alerts)
12. [📜 Export Statement](#export-statement)

---

## 📋 Overview

The `UserList.js` component is a part of a larger user management system. It is used to display a list of users with options to search, sort, and perform actions such as viewing details, editing attributes, and toggling user activation status.

---

## 📦 Imports

**Libraries and Components:**

- **React**: Core library for building user interfaces.
- **Reactstrap**: Provides Bootstrap 4 components as React components.
- **react-super-responsive-table**: A responsive table component.
- **SweetAlert**: A beautiful replacement for JavaScript's `alert`.
- **React Router**: For navigation and linking between different parts of the application.
- **Lodash**: Utility library providing functions like `debounce`.

**Custom Imports:**

- **Breadcrumbs**: A component for displaying breadcrumb navigation.
- **Paginator**: Custom pagination component.
- **EarningTimeline, EditReferral, EditFreeLobby**: Components for editing respective user details.
- **FilterPermission**: Helper for permission-based UI changes.
- **IconsToolTip**: Component for displaying icons with tooltips.

---

## 🔧 State Management

The component uses React's `useState` hook to manage various state variables:

- **`users`**: List of users fetched from the server.
- **`singlebtn`**: Boolean for dropdown toggle.
- **`loader`**: Boolean to indicate loading state.
- **`deleteModal` & `activeModal`**: Booleans for showing modals.
- **`deactivateReason`**: Stores the reason for deactivation.
- **`selectedUser`**: Stores the currently selected user for actions.
- **`pageNumber`, `pageSize`**: Used for pagination.
- **`searchTerm`, `sortBy`**: Used for search and sorting.
- **`dropdownOptions`**: Options for sorting dropdown.
- **Editing states**: Booleans and IDs for managing edit components (earnings, referral, free lobby).

---

## 📜 useEffect Hooks

- **`useEffect`**: Called on component mount and when `sortBy`, `searchTerm`, or `pageNumber` changes to fetch and display the user list.
- **`cleanup function`**: Cancels any debounced search requests when the component unmounts.

---

## 🔍 Search and Filter

- **`handleSearch`**: Updates the `searchTerm` and resets the page number when the user inputs a search query.
- **`dropdownChange`**: Sets the sorting criterion based on user selection.

---

## 🔄 User Activation/Deactivation

- **`openAlert`**: Opens a modal to confirm user activation/deactivation.
- **`deactivateUserStatus`**: Toggles user status and updates the list on successful operation.
- **`closeAlert`**: Closes the active modal.

---

## 🛠️ Editing User Details

Functions for handling editing:

- **`handleEditEarning`**
- **`handleEditReferral`**
- **`handleEditFreeLobby`**

These functions open respective modals/components for editing user information.

---

## 🧩 Render Function

The render function returns JSX that constructs the UI:

- **Breadcrumbs**: Displays the navigation path.
- **Search Box**: Input field for searching users.
- **Dropdown**: Allows sorting by different criteria.
- **Clear Button**: Resets filters and search terms.

---

## 👥 User Table

- **Table Layout**: Uses a responsive table to display user data with columns for username, contact info, status, etc.
- **Conditional Rendering**: Based on user permissions, specific columns and actions may be shown or hidden.
- **Action Buttons**: Include view, edit, activate, and deactivate options.

---

## ⚙️ Utilities and Helpers

- **`filterModel`**: Constructs the filter object for API requests.
- **`handlePageClick`**: Updates the current page displayed in the paginator.

---

## 📬 Modals and Alerts

- **`SweetAlert`**: Used for confirm dialogs when activating or deactivating users.
- **Success Message**: Displays a success alert upon successful status change.

---

## 📜 Export Statement

Exports the `UserList` component as the default export, allowing it to be imported and used in other parts of the application.

```javascript
export default UserList;
```

---

This concludes the detailed documentation for `UserList.js`. The component integrates several features and utilities, making it a robust tool for managing user data within the application. If you have any questions or need further clarification, feel free to reach out! 😊