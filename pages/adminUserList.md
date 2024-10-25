# 📚 AdminUserList.js Documentation

Welcome to the documentation for the **AdminUserList.js** file. This React component is responsible for managing and displaying a list of admin users, allowing for operations such as searching, sorting, and managing permissions. Below, we will break down each part of the file to help you understand its functionality and purpose.

---

## 🗂️ Index

1. [Overview](#overview)
2. [Imports](#imports)
3. [State Variables](#state-variables)
4. [Effect Hooks](#effect-hooks)
5. [Helper Functions](#helper-functions)
6. [Event Handlers](#event-handlers)
7. [Rendering](#rendering)
8. [Dependencies](#dependencies)

---

## 📝 Overview

The **AdminUserList** component is a React component that provides a user interface to manage a list of admin users. It includes features such as:

- Displaying a list of admin users.
- Searching and filtering the user list.
- Sorting the user list by specific fields.
- Enabling or disabling user accounts.
- Managing user permissions.
- Pagination for navigating through large lists.

---

## 📦 Imports

Here's a list of the key imports and their purposes:

| Module                         | Description                                                                                                        |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------|
| React                          | Core React library for building UI components.                                                                    |
| Reactstrap                      | Provides Bootstrap 4 components as React components.                                                              |
| React Super Responsive Table   | A responsive Table component for displaying data tables.                                                          |
| Breadcrumbs                    | A breadcrumb component for navigation.                                                                            |
| React Router DOM               | For navigation and linking within the application.                                                                |
| Paginator                      | Custom pagination component for navigating through pages.                                                         |
| Admin User API Helper          | Contains helper functions for API calls related to admin users.                                                   |
| React Bootstrap SweetAlert     | A library for displaying beautiful alerts.                                                                        |
| React Toastify                 | A library for displaying notifications.                                                                           |
| Lodash                         | Utility library for JavaScript, used here for functions like `debounce` and `isEmpty`.                            |
| FilterPermission               | Helper for filtering permissions based on user roles.                                                             |
| PermissionUtils                | Utility functions for handling permissions.                                                                       |
| ClearButton                    | A component to clear search fields and filters.                                                                   |
| Util Helper                    | Contains utility functions, like `getFilterText`, used for obtaining display text for dropdowns.                  |

---

## 🗃️ State Variables

The component manages several state variables to control its behavior:

- **admins**: Stores the list of admin users fetched from the server.
- **isLoading**: Indicates if the data is currently being loaded.
- **disableDelBtn**: Controls the disabled state of delete buttons.
- **totalCount**: The total count of admin users for pagination purposes.
- **selectedUser**: Stores the currently selected user for actions like delete or status change.
- **deleteModal**: Controls the visibility of the modal for deleting or changing user status.
- **pageSize**: The number of users per page.
- **pageNumber**: The current page number.
- **changePermission, deletePermission, addPermission**: Flags for user permissions.
- **selectedDropdown**: The currently selected sorting option.
- **sortBy**: The field by which the list is sorted.
- **searchTerm**: The current search term entered by the user.
- **singlebtn**: Controls the dropdown toggle state.
- **disableSwal**: Controls the disabled state of the SweetAlert confirm button.

---

## ⏳ Effect Hooks

The component uses `useEffect` to perform side effects:

- **Fetching Admin User List**: When the `sortBy`, `searchTerm`, or `pageNumber` changes, it fetches the admin user list.
- **Setting Permissions**: Calls `callSetPermission` to set the appropriate permissions based on user roles.

---

## 🛠️ Helper Functions

Several helper functions are defined to manage operations:

- **getListing**: Fetches the list of admin users based on current filters.
- **filterModel**: Constructs the filter model for API requests.
- **callSetPermission**: Sets user permissions for actions based on roles.
- **changeUserStatus**: Changes the status of a selected user (active/inactive).
- **handlePageClick**: Updates the current page number.
- **handleDelete**: Deletes a selected admin user.
- **handleSearch**: Updates the search term based on user input.
- **dropdownChange**: Updates sorting options based on user selection.
- **handleClear**: Resets search and filter fields to initial state.

---

## 🖱️ Event Handlers

- **debouncedResults**: Utilizes Lodash's `debounce` to handle search input efficiently.
- **openAlert & closeAlert**: Manage the opening and closing of status change alerts.

---

## 🖼️ Rendering

The component renders a complete UI for managing admin users, including:

- **Breadcrumb Navigation**: Shows the current path in the application.
- **Search and Filter Controls**: Allows users to search and sort the admin list.
- **Admin User Table**: Displays admin users with options for edit, delete, and status change.
- **Pagination**: Provides navigation controls for paginating through the user list.
- **Alerts**: SweetAlert for confirming user status changes.

### ❗ Conditional Rendering

- **Permission-Based Actions**: Only shows certain actions (edit, delete) if the user has appropriate permissions.

---

## 📦 Dependencies

The component relies on several external libraries and custom utilities for its functionality:

- **React and Reactstrap**: For component structure and styling.
- **React Super Responsive Table**: To ensure the table is responsive across devices.
- **React Bootstrap SweetAlert**: For alert modals.
- **React Toastify**: For toast notifications.
- **Lodash**: For debouncing search input and handling empty checks.
- **Custom Helpers and Utilities**: For handling permissions, API interactions, and UI elements.

---

By understanding each part of this component, you can effectively manage and extend its functionality to suit the needs of your application. Happy coding! 😊