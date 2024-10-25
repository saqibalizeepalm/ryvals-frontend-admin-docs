# CommunityList.js Documentation

Welcome to the documentation for the **CommunityList.js** file. This component is a key part of a React application designed to manage and display a list of community video clips. The component provides functionalities to view, add, edit, and delete community entries, leveraging a responsive table layout for optimal viewing across different devices.

---

## Index

- [Overview](#overview)
- [Component Structure](#component-structure)
- [Key Features](#key-features)
- [Dependencies](#dependencies)
- [State Management](#state-management)
- [Event Handlers](#event-handlers)
- [Rendering Logic](#rendering-logic)
- [Permissions](#permissions)
- [Conclusion](#conclusion)

---

## Overview

The **CommunityList.js** file is responsible for rendering a list of communities fetched from an API. It uses a responsive table to display the data and provides options to paginate through the entries, add new entries, edit existing ones, and delete entries. The component ensures that user permissions are respected through conditional rendering of action buttons.

---

## Component Structure

```javascript
const CommunityList = (props) => {
  // States
  const [community, setCommunity] = useState([]);
  const [isLoading, setisLoading] = useState(false);
  const [totalCount, settotalCount] = useState(null);
  const [deleteId, setDeleteId] = useState(null);
  const [deleteModal, setdeleteModal] = useState(false);
  const [disableSwal2, setDisabled2] = useState(false);
  const [pageNumber, setpageNumber] = useState(1);
  const [changePermission, setChange] = useState(false);
  const [deletePermission, setDelete] = useState(false);
  const [addPermission, setAdd] = useState(false);

  // Effects and Functions
  useEffect(() => {
    getList();
    callSetPermission();
  }, [pageNumber]);

  const getList = async () => { /* Fetch list logic */ };
  const handlePageClick = (pageNum) => { setpageNumber(pageNum); };
  const openAlert = (id) => { setDeleteId(id); setdeleteModal(true); };
  async function deleteCommunitySwal() { /* Delete logic */ }
  const closeAlert = () => { setdeleteModal(false); };

  // Rendering
  return (/* JSX code */);
};

export default CommunityList;
```

---

## Key Features

- **Responsive Table**: Displays community data in a responsive table format for various screen sizes.
- **Pagination**: Allows users to navigate through pages of community entries.
- **CRUD Operations**: Provides functionality to add, edit, and delete community entries.
- **Conditional Rendering**: Displays action buttons based on user permissions.
- **Loading State**: Displays a spinner while data is being fetched or actions are being processed.
- **Alerts & Notifications**: Utilizes sweet alerts for confirmation dialogs and toast notifications for success messages.

---

## Dependencies

The component relies on several dependencies for its functionality and UI:

- **React & React Hooks**: For component structure and state management.
- **Reactstrap & Bootstrap**: For UI components like buttons, cards, and grid layout.
- **React Super Responsive Table**: For a responsive table layout.
- **Sweet Alert & React Toastify**: For alerts and notifications.
- **Lodash**: For utility functions like `isEmpty`.

---

## State Management

The component uses React's `useState` hooks to manage various states:

| State Variable    | Purpose                                       |
|-------------------|-----------------------------------------------|
| `community`       | Stores the list of community entries.         |
| `isLoading`       | Indicates whether data is currently being loaded. |
| `totalCount`      | Stores the total number of community entries. |
| `deleteId`        | Holds the ID of a community entry to be deleted. |
| `deleteModal`     | Controls the visibility of the delete confirmation modal. |
| `disableSwal2`    | Disables the SweetAlert2 confirmation button while processing deletion. |
| `pageNumber`      | Tracks the current page number for pagination. |
| `changePermission`| Determines if the edit action is permissible. |
| `deletePermission`| Determines if the delete action is permissible. |
| `addPermission`   | Determines if the add action is permissible. |

---

## Event Handlers

- **`getList`**: Fetches the list of community entries from the API based on the current page number.
- **`handlePageClick`**: Updates the `pageNumber` state when a pagination link is clicked.
- **`openAlert`**: Opens a Sweet Alert confirmation dialog for deleting a community entry.
- **`deleteCommunitySwal`**: Handles the confirmation and deletion of a community entry.
- **`closeAlert`**: Closes the Sweet Alert dialog without taking any action.

---

## Rendering Logic

The component renders a **Breadcrumb** for navigation, a **button** to add new entries (if permitted), and a **responsive table** to display the community data. The table includes columns for:

- Serial Number
- YouTube Link
- Lobby Name
- Username
- Create Date
- Description
- Pinned Video

If the user has permissions, **Edit** and **Delete** buttons are rendered within each table row.

---

## Permissions

The component respects user permissions, which determine whether the user can:

- **Add** new community entries.
- **Edit** existing entries.
- **Delete** entries.

These permissions are checked using utility functions (`FilterPermission`, `filterOutPermissionToShowHide`) and are set during the component's mounting phase.

---

## Conclusion

The **CommunityList.js** component is a robust and flexible part of the application, providing comprehensive management of community video clips while respecting user permissions. It ensures that users have the necessary tools and feedback to interact effectively with the community data.

# `AddEditCommunity.js` Documentation 📄

## Table of Contents
1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Key Features](#key-features)
4. [Imports and Dependencies](#imports-and-dependencies)
5. [State Management](#state-management)
6. [Lifecycle Methods](#lifecycle-methods)
7. [Form Handling](#form-handling)
8. [Utility Methods](#utility-methods)
9. [Rendering the Component](#rendering-the-component)
10. [Usage](#usage)
11. [Visual Components](#visual-components)

---

## Overview

The `AddEditCommunity.js` file defines a React component used for adding and editing community details. This component is part of a larger application where users can manage community information linked to various platforms (such as YouTube, Twitter, and Twitch) and assign them to specific lobbies and usernames.

---

## Component Structure

- **Class Component:** The component is implemented as a class component extending `React.Component`.
- **Constructor:** Initializes state and binds methods.
- **Lifecycle Methods:** Utilizes `componentDidMount` to fetch initial data.
- **Form Submission:** Handles form submission with validation and API calls.
  
---

## Key Features

- **Add/Edit Modes:** Capable of both adding new communities and editing existing ones based on URL parameters.
- **Form Validation:** Uses `availity-reactstrap-validation` for form validation.
- **Data Fetching:** Retrieves lobby and username lists to populate dropdowns.
- **State Management:** Manages form data and loading states.
- **Switch Component:** Toggles a 'Pinned' status for the community.

---

## Imports and Dependencies 📦

The component relies on several libraries and services:

| **Import**              | **Purpose**                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------|
| `React`, `Component`    | Core React library and base class for the component.                                          |
| `reactstrap`            | UI components like `Row`, `Col`, `Card`, `FormGroup`, `Button`, etc.                          |
| `availity-reactstrap-validation` | Form validation components such as `AvForm` and `AvField`.                             |
| `react-switch`          | Custom switch component for toggling boolean states.                                          |
| `react-toastify`        | Notifications for success and error messages.                                                 |
| `multiselect-react-dropdown` | Multi-select dropdown for selecting lobbies and usernames.                                |
| `react-player`          | For embedding YouTube videos within the component.                                            |
| `react-router-dom`      | Navigation and URL parameter utilities.                                                       |
| `community_api_helper`  | Custom API helper functions for interacting with the community backend.                       |

---

## State Management

The component uses React's state to manage data:

- **`isLoading`:** Boolean indicating if data is being fetched or submitted.
- **`editMode`:** Boolean to determine if the form is in edit mode.
- **`lobbyId`:** Numeric ID of the current lobby.
- **`optionGroup`, `optionGroupUser`:** Arrays for dropdown options.
- **`errorMsg`, `errorMessage`, `errorMessageUser`:** Strings for error messages.
- **Links and Descriptions:** Strings for social media links and descriptions.
- **`status`:** Boolean for the 'Pinned' switch.
- **Selections:** Arrays for selected game and username.

---

## Lifecycle Methods

- **`componentDidMount`:** Checks if a `lobbyId` is present from the route parameters to determine edit mode and fetches the necessary data for the form.

---

## Form Handling

### Form Submission

- **`handleValidSubmit`:** Handles the form submission with validation and conditional logic for creating or editing a community.

### Validation

- **Validation is performed using `AvField` components with custom error messages for required fields and pattern matching for URLs.**

---

## Utility Methods

- **`lobbyDetail(lobbyId)`:** Fetches details of a specific lobby for editing.
- **`lobbyList` / `userNameList`:** Fetches lists of lobbies and usernames for dropdown options.
- **`mapDetailsToForm(res)`:** Maps fetched data to form fields.
- **`showLoader`:** Controls the loading indicator.
- **`handleChange`:** Generic method to update state on input change.

---

## Rendering the Component

The component renders a form with fields for:

- **YouTube, Twitter, Twitch links**
- **Description**
- **Lobby and Username selectors**
- **Pinned toggle switch**
- **Video preview using `ReactPlayer`**

The form uses `AvForm` and `AvField` for validated inputs, and a `Switch` component for the Pinned status.

---

## Usage

This component is utilized in applications where users can manage community data associated with different platforms. It offers capabilities to add new entries or edit existing ones. To navigate back to the community list, a breadcrumb link is provided.

---

## Visual Components 🎨

The component uses visual components from `reactstrap` for layout and `Multiselect` for selection of items. A `Switch` toggles the pinned status, providing a user-friendly interface for interaction.

---

This documentation provides a comprehensive overview of the functionality and structure of the `AddEditCommunity.js` component. By understanding these aspects, developers can effectively utilize and modify the component within their projects.