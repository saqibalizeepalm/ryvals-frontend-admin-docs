# 📜 ActivityLog.js Documentation

## Table of Contents
1. [Introduction](#introduction)
2. [Imports and Dependencies](#imports-and-dependencies)
3. [Component State Management](#component-state-management)
4. [Utility Functions](#utility-functions)
5. [Event Handlers](#event-handlers)
6. [Rendering](#rendering)
7. [Conclusion](#conclusion)

---

## Introduction

The `ActivityLog.js` file is a React component that provides a comprehensive and interactive user interface for displaying and managing activity logs. This component is built using various libraries and components to deliver a responsive and dynamic user experience, especially for filtering and viewing activities logged by users or the system.

---

## Imports and Dependencies

| Library/Component | Description |
|-------------------|-------------|
| `React`, `useState`, `useEffect`, `useCallback` | Core React libraries for building the component. |
| `reactstrap` | A library for responsive React components based on Bootstrap. |
| `react-super-responsive-table` | For creating responsive tables. |
| `Breadcrumbs` | Custom component for navigation breadcrumbs. |
| `user_api_helper` | Contains API methods like `getActivityList` and `getEventList`. |
| `Paginator` | Custom paginator component for managing pagination. |
| `Date-fns` | For date manipulation functions. |
| `lodash` | Utility library; used here for `cloneDeep` and `debounce` functions. |
| `util` | Custom utility functions such as `convertDateToHyphenFormat` and `getFilterText`. |

### Reactstrap Components
- **Row, Col, Card, CardBody**: For layout and card structure.
- **Dropdown, DropdownItem, DropdownMenu, DropdownToggle**: For dropdown menu functionalities.
- **Button, Modal, ModalBody, ModalHeader, ModalFooter, Label**: For buttons and modals.

### React Super Responsive Table
- **Table, Thead, Tbody, Tr, Th, Td**: To render a responsive table structure.

---

## Component State Management

The component uses multiple state variables to manage its dynamic UI:

- **logs, loader, active**: To manage logs data, loading state, and active date filters.
- **pagination**: `totalCount`, `pageNumber`, `pageSize` to handle pagination.
- **dropdown**: `singlebtn`, `selectedDropdown`, `sortBy` for dropdown management.
- **dateRange**: Manages the date filter range (`startDate`, `endDate`).
- **events**: `playerEvent`, `adminEvent`, `otherEvent` and their constants for event categorization.
- **selectedEventListId**: Arrays to manage selected events for each category (player, admin, other).

---

## Utility Functions

- **dropdownChange**: Updates the selected dropdown filter and resets the page number.
- **handleToday/Week/Month/Year/Clear**: Set date filters to specific ranges or clear them.
- **updateDateFromPicker**: Update date range from date picker input.
- **getListing**: Fetches event list based on selected type and updates the state.
- **handlePageClick**: Update page number based on paginator click.
- **filterModel**: Builds a filter model object for API requests based on UI selections.
- **applyEvents**: Triggered to apply selected events and fetch logs.

---

## Event Handlers

- **handleSelectEvent**: Manage selection of events in each category.
- **openModal/closeModal**: Manage the opening and closing of the modal for event selection.
- **callLogs**: Fetches logs data based on filter criteria.
- **handleChange**: Handles changes in the search input and filters events accordingly.
- **handleSelectAllEvent**: Selects or deselects all events within a category.
- **handleShowMore/ShowLess**: Toggles the visibility of additional events in the modal view.

---

## Rendering

The component renders various UI elements conditionally based on state:

- **Breadcrumbs** for navigation.
- **Search and Dropdown** controls for filtering.
- **Responsive Table** displaying logs with headers for username, email, events, IP, VPN status, and date/time.
- **Paginator** for navigating through logs pages.
- **Modal** for filtering events, with search and selection capabilities.

### Table Structure
```jsx
<Table>
  <Thead>
    <Tr>
      <Th>User Name</Th>
      <Th>Email</Th>
      <Th>Events</Th>
      <Th>IP Address</Th>
      <Th>VPN</Th>
      <Th>Date & Time</Th>
    </Tr>
  </Thead>
  <Tbody>
    {/* Conditional rendering based on logs data */}
  </Tbody>
</Table>
```

### Modal Structure
```jsx
<Modal>
  <ModalHeader>View All Events</ModalHeader>
  <ModalBody>
    {/* Event selection and search */}
  </ModalBody>
  <ModalFooter>
    <Button>Cancel</Button>
    <Button>Apply</Button>
  </ModalFooter>
</Modal>
```

---

## Conclusion

The `ActivityLog.js` component is a robust and feature-rich implementation designed to manage and display activity logs efficiently. It leverages modern React practices, such as hooks, to maintain a clean and responsive user interface. By using a combination of third-party libraries and custom utilities, the component ensures flexibility and scalability for future enhancements.

# CustomSelect.js Documentation 📄

## Overview

The **CustomSelect** component is a custom wrapper around the `react-select` library component. It provides a custom dropdown selection feature with an optional "Select All" functionality. This component is designed to be flexible and reusable, allowing developers to easily integrate it into their React applications.

## Table of Contents

1. [Installation](#installation)
2. [Purpose](#purpose)
3. [Component Explanation](#component-explanation)
4. [Props](#props)
5. [Usage Example](#usage-example)
6. [Conclusion](#conclusion)

---

## Installation

To use this component, ensure you have the `react-select` library installed in your project:

```bash
npm install react-select
```

---

## Purpose

The **CustomSelect** component is used to provide a dropdown menu in a React application. It extends the functionality of the `react-select` component by allowing an "Select All" option, which enables users to select all available options in the dropdown at once.

---

## Component Explanation

The **CustomSelect** component is a functional component in React. Here's a breakdown of its functionality:

- **Import Statements**
  - Imports necessary modules and components, including React, PropTypes for type-checking, and the `react-select` component.

- **CustomSelect Component**
  - The component checks if the `allowSelectAll` prop is true. If so, it prepends an "Select All" option to the list of options.
  - Uses the `onChange` handler to manage the selection logic. If the "Select All" option is selected, it selects all available options.
  - Renders a `ReactSelect` component with the provided props and manages its state and behavior.

---

## Props

The **CustomSelect** component accepts the following props:

| Prop           | Type                       | Default                             | Description                                                                                |
|----------------|----------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| `options`      | `array`                    | `[]`                                | Array of options to display in the dropdown.                                               |
| `value`        | `any`                      | `undefined`                         | The current selected value(s) in the dropdown.                                             |
| `onChange`     | `func`                     | `undefined`                         | Callback function triggered when the selection changes.                                    |
| `closeMenu`    | `func`                     | `undefined`                         | Callback function to close the menu.                                                       |
| `allowSelectAll` | `bool`                  | `false`                             | If true, adds an "Select All" option to the dropdown.                                      |
| `allOption`    | `shape` (label, value)     | `{ label: "Select all", value: "*"}`| Defines the label and value for the "Select All" option.                                   |

---

## Usage Example

Here's an example of how to use the **CustomSelect** component in a React application:

```jsx
import React, { useState } from "react";
import CustomSelect from "./CustomSelect";

const options = [
  { label: "Option 1", value: "1" },
  { label: "Option 2", value: "2" },
  { label: "Option 3", value: "3" }
];

const MyComponent = () => {
  const [selectedOptions, setSelectedOptions] = useState([]);

  const handleChange = (selected) => {
    setSelectedOptions(selected);
  };

  return (
    <div>
      <h1>My Custom Select</h1>
      <CustomSelect
        options={options}
        value={selectedOptions}
        onChange={handleChange}
        allowSelectAll
      />
    </div>
  );
};

export default MyComponent;
```

---

## Conclusion

The **CustomSelect** component is a powerful and flexible tool for creating dropdowns with "Select All" functionality in React applications. By leveraging the `react-select` library, it offers a rich set of features and can be easily customized to fit the needs of any project.