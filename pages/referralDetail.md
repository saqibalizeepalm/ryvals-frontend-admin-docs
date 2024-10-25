# 📃 ReferralDetails.js Documentation

Welcome to the comprehensive documentation for `ReferralDetails.js`. This component is part of a React application that manages and displays details about referral listings. Below, you will find a detailed explanation of its functionality, structure, and components used.

## Index

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [State Variables](#state-variables)
4. [Effects and Callbacks](#effects-and-callbacks)
5. [Helper Functions](#helper-functions)
6. [Render Method](#render-method)
7. [Components](#components)

## Introduction

**ReferralDetails.js** is a React component designed to display a list of referral users, their earnings, and other relevant details. This component allows for searching, sorting, and filtering through date ranges while providing a responsive, user-friendly interface.

## Imports

The file imports multiple modules and components essential for building the UI and functionality:

```javascript
import React, { useCallback, useEffect, useRef, useState } from "react";
import { Row, Col, Card, CardBody, Dropdown, DropdownItem, DropdownMenu, DropdownToggle } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getReferralList } from "../../services/referral_api_helper";
import { Link } from "react-router-dom";
import Paginator from "../../helpers/paginator/paginator";
import ReactDatePicker from "react-datepicker";
import { format } from "date-fns";
import calenderIcon from "../../assets/images/calendar.svg";
import { dateFormat, dropdownOptionsForReferral, getFilterText } from "../../helpers/util";
import { debounce } from "lodash";
import ClearButton from "../../components/ClearButton";
```

### Key Imports

- **React Components**: `useState`, `useEffect`, `useCallback`, `useRef` for handling component state and lifecycle.
- **Reactstrap Components**: For building UI elements like rows, columns, cards, and dropdowns.
- **React-Super-Responsive-Table**: For creating responsive tables.
- **React-Router-Dom**: For navigation within the application.
- **Date-Fns**: For date formatting.
- **Lodash**: For debouncing input changes.

## State Variables

State variables are used to manage the component's dynamic data:

```javascript
const [referrals, setReferrals] = useState([]);
const [singlebtn, setSinglebtn] = useState(false);
const [loader, setLoader] = useState(false);
const [selectedDropdown, setselectedDropdown] = useState(null);
const [totalCount, settotalCount] = useState(null);
const [pageNumber, setpageNumber] = useState(1);
const [searchTerm, setsearchTerm] = useState(null);
const [sortBy, setsortBy] = useState(null);
const [dateRange, setDateRange] = useState([null, null]);
const [startDate, setStartDate] = useState(null);
const [endDate, setEndDate] = useState(null);
const [tileObj, setTileObj] = useState({
  total_money_distributed: null,
  current_month_given: null,
  daily_money_given: null,
});
```

### Important State Variables

- **referrals**: Stores the list of referral data.
- **loader**: Manages loading state for asynchronous operations.
- **searchTerm**: Holds the search input value.
- **dateRange**: Manages the selected date range for filtering.
- **tileObj**: Contains summary data such as total money distributed.

## Effects and Callbacks

### useEffect Hook

Executes when specific dependencies change, primarily for fetching referral data:

```javascript
useEffect(() => {
  getReferralListing();
}, [sortBy, searchTerm, pageNumber, dateRange]);
```

### Callback Functions

- **handleChange**: Manages changes to the date picker.
- **debouncedResults**: A debounced version of the search handler to optimize performance.

## Helper Functions

### getReferralListing

Fetches and sets referral data based on current filters:

```javascript
const getReferralListing = () => {
  setLoader(true);
  const filters = filterModel();
  getReferralList(filters)
    .then((res) => {
      setReferrals(res.data);
      settotalCount(res.total);
      setLoader(false);
      setTileObj({
        total_money_distributed: res.total_money_distributed,
        current_month_given: res.current_month_given,
        daily_money_given: res.daily_money_given,
      });
    })
    .catch(() => {
      setLoader(false);
    });
};
```

### filterModel

Constructs an object representing the current filter state:

```javascript
function filterModel() {
  let model = {
    searchTerm: searchTerm,
    sortBy: sortBy,
    pageNumber: pageNumber,
    pageSize: pageSize,
    from_date: dateRange[0] && format(dateRange[0], "yyyy-MM-dd"),
    to_date: dateRange[1] && format(dateRange[1], "yyyy-MM-dd"),
  };
  return model;
}
```

## Render Method

The `ReferralDetails` component's render method consists of several UI elements structured to provide a detailed view of referral data:

- **Breadcrumbs**: Displays the current navigation path.
- **Search Box**: Allows users to search for referrals by various fields.
- **Dropdown**: Provides sorting options.
- **Date Picker**: Enables date range filtering.
- **Table**: Displays referral details in a tabular format.
- **Paginator**: Facilitates navigation through pagination.

## Components

### Custom Input for Date Picker

A custom input component for the `ReactDatePicker`:

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

## Conclusion

The **ReferralDetails.js** component is a complex yet user-friendly interface for managing and viewing referral data. It efficiently uses React hooks and state management to handle asynchronous data fetching, filtering, and rendering, providing a seamless user experience.

# 📄 ViewDetails.js Documentation

## 📋 Index
1. [Introduction](#introduction)
2. [Dependencies and Imports](#dependencies-and-imports)
3. [Component Overview](#component-overview)
4. [State Management](#state-management)
5. [Lifecycle Methods](#lifecycle-methods)
6. [Helper Functions](#helper-functions)
7. [Rendering Logic](#rendering-logic)
8. [Conclusion](#conclusion)

---

## 🌟 Introduction

The `ViewDetails.js` file is a **React component** designed to display detailed information about a user's referral data. It retrieves this data from an API and presents it in a structured and interactive format using a responsive table layout. This component is crucial for users to understand their referral earnings and connections.

---

## 📦 Dependencies and Imports

Here's a breakdown of the dependencies and imports used in `ViewDetails.js`:

| Dependency                    | Purpose                                                            |
|-------------------------------|--------------------------------------------------------------------|
| `React`                       | Core library for building user interfaces.                        |
| `reactstrap`                  | Provides Bootstrap 4 components for React.                        |
| `react-super-responsive-table`| Enables responsive table designs.                                 |
| `react-router-dom`            | Used for navigation and linking within the app.                   |
| `referral_api_helper`         | Custom service used to fetch referral data from the API.          |
| `Breadcrumb`                  | Displays a breadcrumb navigation for the user's location.         |

**Code Block: Import Statements**

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getReferralDetail } from "../../services/referral_api_helper";
import { Link } from "react-router-dom";
```

---

## 🖥️ Component Overview

The `ViewDetails` component is a functional component that utilizes **React hooks** to manage state and lifecycle events. It primarily serves to:

- Fetch and display user referral details.
- Show detailed earning information in a table format.
- Provide navigational links for better user experience.

---

## 🗂️ State Management

The component maintains three pieces of state using the `useState` hook:

1. **`referralDetail`**: Stores the main referral details of the user.
2. **`referralList`**: Contains a list of referral-specific earnings.
3. **`loader`**: A boolean to manage loading state during data fetching.

**Code Block: State Initialization**

```javascript
const [referralDetail, setReferrals] = useState([]);
const [referralList, setLists] = useState([]);
const [loader, setLoader] = useState(false);
```

---

## 🔄 Lifecycle Methods

The `useEffect` hook is used to trigger data fetching when the component mounts:

**Code Block: useEffect Hook**

```javascript
useEffect(() => {
    getReferralDetails();
}, []);
```

---

## 🛠️ Helper Functions

### `getReferralDetails`

This function retrieves the user ID from the URL parameters and calls `getReferralData` to fetch data.

**Code Block: getReferralDetails**

```javascript
const getReferralDetails = () => {
    let userId = props.match.params.userId;
    if (userId) {
        getReferralData(userId);
    }
};
```

### `getReferralData`

An **asynchronous function** that fetches referral data using the `getReferralDetail` service, updates the state with the fetched data, and handles loading states.

**Code Block: getReferralData**

```javascript
const getReferralData = async (id) => {
    try {
        setLoader(true);
        const res = await getReferralDetail(id);
        setLoader(false);
        setReferrals(res);
        setLists(res.referral_details);
    } catch (error) {
        setLoader(false);
    }
};
```

---

## 🖼️ Rendering Logic

The component returns a JSX structure that includes:

- **Breadcrumb Navigation**: Provides a navigation trail for the user.
- **Back Link**: Allows users to return to the previous page.
- **Loader**: Displays a loading spinner while data is being fetched.
- **Referral Details**: Displays user's referral information in a structured format.
- **Responsive Table**: Lists detailed earning information for each referral.

**Code Block: Main Render Method**

```javascript
return (
    <React.Fragment>
        <div className="page-content">
            <Breadcrumbs breadcrumbItem="REFERRAL Details" />
            <Row>
                <Row className="mb-4">
                    <Col>
                        <p>
                            <Link to={"/referrals"}>
                                <i className="mdi mdi-arrow-left"></i> back
                            </Link>
                        </p>
                    </Col>
                </Row>
                {loader ? (
                    <div class="spinner-grow spinner-class" role="status">
                        <span class="sr-only">Loading...</span>
                    </div>
                ) : (
                    <Col lg={12}>
                        <Card className="mb-0">
                            {referralDetail && (
                                <CardBody>
                                    // User details and Referral Earnings Table
                                </CardBody>
                            )}
                        </Card>
                    </Col>
                )}
            </Row>
        </div>
    </React.Fragment>
);
```

---

## 🔚 Conclusion

The `ViewDetails.js` component is a well-structured and efficient way to present referral details to users, leveraging the power of **React hooks** and **responsive design** techniques. It ensures a seamless user experience by handling asynchronous data fetching and providing intuitive navigation options.