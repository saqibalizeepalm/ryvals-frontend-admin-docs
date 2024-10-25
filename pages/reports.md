# 📄 Reports.js Documentation

This documentation provides a comprehensive overview of the `Reports.js` file, which is a React component used in a web application for generating and displaying various reports. The component integrates multiple features such as tab navigation, date filtering, data fetching, and table rendering. 

## 📚 Index
1. **Overview**
2. **Dependencies**
3. **State Management**
4. **Functions**
5. **User Interface Components**
6. **Data Fetching**
7. **Exports**

## 🌟 Overview
The `Reports` component is designed to provide users with an interactive interface to view different types of reports such as transactions, users, lobbies, and complaints. It offers functionalities to filter reports based on date ranges, paginate through data, and download reports in CSV format.

## 📦 Dependencies
The component utilizes several third-party libraries and internal modules:
- **React**: Core library for building user interfaces.
- **Reactstrap**: Bootstrap components for React.
- **lodash**: Utility functions for deep cloning.
- **AWS SDK**: Used for accessing AWS S3 service for report downloads.
- **date-fns**: Utility library for date formatting and manipulation.

### Imported Libraries and Components
```javascript
import React, { useCallback, useEffect, useState } from "react";
import { Row, Col, Card, CardBody, CardTitle, Nav, NavItem, NavLink, TabContent, TabPane } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getCompliantReports, getTransactionReport, getUserReports, getLobbiesReport, getCSV } from "../../services/user_api_helper";
import DateFiltersReports from "../../components/Common/DateFiltersReports";
import { endOfMonth, endOfWeek, endOfYear, startOfMonth, startOfWeek, startOfYear } from "date-fns";
import { cloneDeep } from "lodash";
import FiltersResultInButton from "../../components/Common/FiltersResultInButton";
import TableBasedOnActiveTab from "../../components/Common/TableBasedOnActiveTab.js";
import { S3Client, GetObjectCommand } from "@aws-sdk/client-s3";
import { getSignedUrl } from "@aws-sdk/s3-request-presigner";
import { convertDateToHyphenFormat } from "../../helpers/util";
```

## 🗂️ State Management
The component manages multiple pieces of state using React's `useState` hook:
- **`isLoading`**: Tracks loading status for data fetching.
- **`activeTab`**: Stores the currently active tab.
- **`detailView`**: Indicates whether the detail view is enabled.
- **`dateRange`**: Holds the selected start and end dates for filtering.
- **`pageNum`**: Keeps track of pagination state for each report type.
- **`transactionFilter`**: Stores the current transaction filter criteria.
- **`model`**: Represents the current report query model.
- **`total`**: Total number of records fetched.
- **`active`**: Indicates the active filter for date range.
- **`clear`**: Flag to clear filters.
- **`fullLoader`** and **`tableLoader`**: Manage loading states for different sections.

### Example of State Initialization
```javascript
const [isLoading, setisLoading] = useState(false);
const [activeTab, setactiveTab] = useState(props.location.state === undefined ? "1" : props.location.state.active);
const [dateRange, setDateRange] = useState(props.location.state === undefined ? [null, null] : [props.location.state?.setDates[0], props.location.state?.setDates[1]]);
const [pageNum, setPageNum] = useState(intialPaginationState);
const [transactionFilter, setTransactionFilter] = useState(props.location.state === undefined ? 0 : props.location.state.filter);
```

## 🔨 Functions
The component contains several utility and event-handling functions:

### Date Handling Functions
- **`handleToday`**: Sets the date range to today's date.
- **`handleWeek`**: Sets the date range to the current week.
- **`handleMonth`**: Sets the date range to the current month.
- **`handleYear`**: Sets the date range to the current year.
- **`handleClear`**: Clears all date filters.

### Data Fetching and Export
- **`getReport`**: Fetches report data based on the active tab and date range.
- **`handleExport`**: Prepares and initiates the download of report data as a CSV file using AWS S3.

### API Call Wrappers
Functions that wrap API calls for each report type:
- **`callCompliant`**, **`callUsers`**, **`callTransaction`**, **`callLobbies`**: Fetch data for each report type using appropriate filters.

### Helper Functions
- **`filterModel`**: Constructs the filter model for API calls.
- **`showLoader`**: Manages loading states for the table.

## 🖼️ User Interface Components
The component uses various UI elements from `reactstrap` to render the interface:
- **Navigation Tabs**: For selecting report types.
- **Cards**: To display content within a styled card.
- **Tab Content and Panes**: To switch between different report views based on the active tab.

### Tab Navigation Example
```jsx
<Nav className="flex-row" pills>
  <NavItem>
    <NavLink className={activeTab === "1" ? "active d-flex" : "d-flex justify-content-center"} onClick={() => { /* Event handler */ }}>
      <img src={transaction_new} alt="transaction-icon" />
      <p className="fw-bold mt-3 transaction-icon">Transactions</p>
    </NavLink>
  </NavItem>
  {/* Additional NavItems for other tabs */}
</Nav>
```

## 📊 Data Fetching
The component integrates with backend services to fetch data for reports through the following methods:
- **`getCompliantReports`**
- **`getTransactionReport`**
- **`getUserReports`**
- **`getLobbiesReport`**

These functions are invoked based on the active report tab and the selected date range filters.

## 🔗 Exports
The component exports the `Reports` component as the default export:
```javascript
export default Reports;
```

## 🎨 Conclusion
The `Reports.js` file is a crucial part of the application, providing users with a dynamic interface for accessing various reports. It leverages modern React practices, such as hooks and context, to manage state and lifecycle, ensuring a smooth and responsive user experience.