# 📄 Inbox.js Documentation

## 📚 Overview

`Inbox.js` is a React component that renders a styled inbox section. It is part of a larger application that uses React and Reactstrap for UI components, and React Router for navigation. This component displays a list of messages, each with an avatar, name, description, and timestamp.

## 📋 Table of Contents

1. [Component Structure](#component-structure)
2. [Imports](#imports)
3. [Inbox Data](#inbox-data)
4. [Render Method](#render-method)
5. [Styling and Layout](#styling-and-layout)
6. [Usage](#usage)

## 🔍 Component Structure

The `Inbox.js` file defines a functional React component named `Overview`. This component is responsible for displaying a list of messages in a card format. Here's a breakdown of the component structure:

- **Imports**: Import necessary libraries and assets.
- **Inbox Data**: Define the inbox data array with message details.
- **Render Method**: Render the component using JSX.
- **Export**: Export the component for use in other parts of the application.

## 📥 Imports

```javascript
import React from 'react';
import { Link } from 'react-router-dom';
import { Card, CardBody, Col } from 'reactstrap';

// Import images
import avatar1 from '../../assets/images/users/avatar-3.jpg';
import avatar2 from '../../assets/images/users/avatar-4.jpg';
import avatar3 from '../../assets/images/users/avatar-5.jpg';
import avatar4 from '../../assets/images/users/avatar-6.jpg';
```

- **React**: Main library for building user interfaces.
- **react-router-dom**: Provides navigation tools such as the `Link` component.
- **reactstrap**: A library that offers Bootstrap 4 components for React applications.
- **Images**: Import user avatars to be displayed in the inbox.

## 📬 Inbox Data

The `inbox` array holds the data for each message in the inbox:

```javascript
const inbox = [
  { id: 1, img: avatar1, name: 'Paul', desc: "Hey! there I'm available", time: '05 min' },
  { id: 2, img: avatar2, name: 'Mary', desc: "This theme is awesome!", time: '12 min' },
  { id: 3, img: avatar3, name: 'Cynthia', desc: "Nice to meet you", time: '18 min' },
  { id: 4, img: avatar4, name: 'Darren', desc: "I've finished it! See you so", time: '2hr ago' },
];
```

- Each object in the array represents a message.
- **Properties**:
  - `id`: Unique identifier for each message.
  - `img`: Avatar image source.
  - `name`: Sender's name.
  - `desc`: Short message description.
  - `time`: Timestamp for when the message was received.

## 🖼️ Render Method

The component uses JSX to render the inbox messages within a card layout:

```jsx
return (
  <React.Fragment>
    <Col lg={4}>
      <Card>
        <CardBody>
          <h4 className="card-title mb-4">Inbox</h4>
          <ul className="inbox-wid list-unstyled">
            {inbox.map((inbox, key) => (
              <li className="inbox-list-item" key={key}>
                <Link to="#">
                  <div className="d-flex align-items-start">
                    <div className="me-3 align-self-center">
                      <img src={inbox.img} alt="" className="avatar-sm rounded-circle" />
                    </div>
                    <div className="flex-1 overflow-hidden">
                      <h5 className="font-size-16 mb-1">{inbox.name}</h5>
                      <p className="text-truncate mb-0">{inbox.desc}</p>
                    </div>
                    <div className="font-size-12 ms-auto">
                      {inbox.time}
                    </div>
                  </div>
                </Link>
              </li>
            ))}
          </ul>
          <div className="text-center">
            <Link to="#" className="btn btn-primary btn-sm">Load more</Link>
          </div>
        </CardBody>
      </Card>
    </Col>
  </React.Fragment>
);
```

- **Card Component**: Renders the inbox messages inside a Bootstrap card.
- **List**: Maps through the `inbox` array and creates a list item for each message.
- **Link**: Wraps each message to enable navigation (currently links to `"#"`).
- **Avatar**: Displays user avatars using imported images.
- **Message Details**: Renders sender's name, message description, and time.

## 🎨 Styling and Layout

- **Card Layout**: Uses the `Card` and `CardBody` components from Reactstrap for a clean layout.
- **Responsive Design**: Utilizes Bootstrap's grid system with the `Col` component for responsiveness.
- **CSS Classes**: Includes various Bootstrap classes for spacing and styling (`mb-4`, `d-flex`, `align-self-center`, etc.).

## 🚀 Usage

To use the `Inbox` component, simply import it and include it in your JSX:

```javascript
import Overview from './Inbox';

function App() {
  return (
    <div>
      <Overview />
    </div>
  );
}

export default App;
```

## 📌 Conclusion

The `Inbox.js` component is a simple yet effective way to display messages in a structured and visually appealing manner. It leverages Bootstrap for styling and React Router for navigation, making it easy to integrate into larger applications. Use this component to keep users engaged with a quick overview of their communications.

# 📊 Dashboard Component Documentation

Welcome to the documentation for the **Dashboard** component! This component serves as the main layout and display page for various analytical widgets and visualizations within a React application. Below, we'll explore this component in detail, explaining its sections, imports, and overall structure.

## 📑 Table of Contents

- [Overview](#overview)
- [Dependencies](#dependencies)
- [Component Structure](#component-structure)
- [Key Features](#key-features)
- [Code Breakdown](#code-breakdown)
- [Conclusion](#conclusion)

---

## 🖥️ Overview

The `Dashboard` component is a central part of a web application designed to present data analytics and key performance indicators. It aggregates various smaller components to form a cohesive dashboard view.

## 📦 Dependencies

The **Dashboard** component relies on several libraries and other components to function:

- **React**: JavaScript library for building user interfaces.
- **Reactstrap**: Bootstrap 4 components for React, providing styled UI elements.
- **React-Router-Dom**: Declarative routing for React applications.
- **Custom Components**: 
  - `LineChart`
  - `RevenueChart`
  - `SalesAnalytics`
  - `ScatterChart`
  - `LatestTransaction`
  - `Overview`
  - `Reviews`
  - `Revenue`
  - `Inbox`

## 🏗️ Component Structure

The `Dashboard` component is structured using React and Reactstrap components to ensure a responsive and visually pleasant layout.

### Component Layout

```jsx
<React.Fragment>
  <div className="page-content">
    <Row>
      <Col lg={3}>
        {/* Order Card */}
      </Col>
      <Col lg={6}>
        <LineChart />
      </Col>
      <Col lg={3}>
        <RevenueChart />
      </Col>
    </Row>
    <Row>
      <Col lg={5}>
        <SalesAnalytics />
      </Col>
      <Col lg={4}>
        <ScatterChart />
      </Col>
      <Col lg={3}>
        {/* New Users Card */}
      </Col>
    </Row>
    <Row>
      <Overview />
      <Reviews />
      <Revenue />
    </Row>
    <Row>
      <Inbox />
      <LatestTransaction />
    </Row>
  </div>
</React.Fragment>
```

## 🌟 Key Features

- **Responsive Design**: Utilizes grid layout with `Row` and `Col` components for responsiveness.
- **Data Visualization**: Integrates various chart components to display data insights.
- **Modular Structure**: Breaks down the dashboard into smaller, reusable components.

## 🔍 Code Breakdown

### Header and Title

The Dashboard begins with a title and breadcrumb navigation, framed within a `Row` and `Col`.

```jsx
<div className="page-title-box d-flex align-items-center justify-content-between">
  <h4 className="page-title mb-0 font-size-18">Dashboard</h4>
  <div className="page-title-right">
    <ol className="breadcrumb m-0">
      <li className="breadcrumb-item active">Welcome to Qovex Dashboard</li>
    </ol>
  </div>
</div>
```

### New Orders and Users Cards

These cards display statistics on new orders and users, complete with icons, colors, and progress indicators.

```jsx
<Card>
  <CardBody>
    <div className="d-flex align-items-start">
      <div className="avatar-sm font-size-20 me-3">
        <span className="avatar-title bg-soft-primary text-primary rounded">
          <i className="mdi mdi-tag-plus-outline"></i>
        </span>
      </div>
      <div className="flex-1">
        <div className="font-size-16 mt-2">New Orders</div>
      </div>
    </div>
    <h4 className="mt-4">1,368</h4>
    <div className="row">
      <div className="col-7">
        <p className="mb-0"><span className="text-success me-2"> 0.28% <i className="mdi mdi-arrow-up"></i> </span></p>
      </div>
      <div className="col-5 align-self-center">
        <Progress value="62" color="primary" className="bg-transparent progress-sm" size="sm" />
      </div>
    </div>
  </CardBody>
</Card>
```

### Chart and Analytics Components

Integrates various chart components such as `LineChart`, `RevenueChart`, `SalesAnalytics`, and `ScatterChart`.

```jsx
<Col lg={6}>
  <LineChart />
</Col>
<Col lg={3}>
  <RevenueChart />
</Col>
```

### Overview, Reviews, Revenue, and Inbox

These sections bring together other components that give additional insights, such as user reviews, revenue statistics, etc.

```jsx
<Row>
  <Overview />
  <Reviews />
  <Revenue />
</Row>
<Row>
  <Inbox />
  <LatestTransaction />
</Row>
```

## 🏁 Conclusion

The **Dashboard** component is a versatile and comprehensive part of the application, integrating multiple smaller components and external libraries to provide a rich, interactive user experience. It effectively uses React and Reactstrap to create a visually appealing and responsive layout.

By breaking down the dashboard into multiple smaller components, it ensures that the application is scalable and each part is maintainable independently. This modular approach is key to managing complex React applications.

# 📊 Line Chart Component Documentation

Welcome to the **Line Chart** component documentation. This component is designed to display sales data using a combination of line and area charts, offering a clear and intuitive visualization of sales trends over a set period.

## 📁 File Overview

- **Filename:** `line-chart.js`
- **Purpose:** To render a line chart that visualizes sales data for 2018 and 2019.

## 📜 Code Breakdown

### 📥 Imports

```javascript
import React from "react";
import ReactApexChart from "react-apexcharts";
import { Card, CardBody } from "reactstrap";
```

- **React**: A JavaScript library for building user interfaces.
- **ReactApexChart**: A component for rendering ApexCharts, a modern charting library.
- **reactstrap**: A library for Bootstrap components in React, providing `Card` and `CardBody` for layout.

### 📈 Component Definition

```javascript
const LineChart = () => {
```

- **LineChart**: A functional component that utilizes React hooks to define the chart's data and configuration.

### 📊 Data Series

```javascript
const series = [
  { name: "2018", type: 'line', data: [20, 34, 27, 59, 37, 26, 38, 25], },
  { name: "2019", data: [10, 24, 17, 49, 27, 16, 28, 15], type: 'area', }
];
```

- **Data Series**: Represents sales data for two years, 2018 and 2019. Each year is visualized with a different chart type (line and area).

### ⚙️ Options Configuration

```javascript
const options = {
  chart: {
    toolbar: { show: false },
    zoom: { enabled: false }
  },
  colors: ['#45cb85', '#3b5de7'],
  dataLabels: { enabled: false },
  stroke: { curve: 'smooth', width: '3', dashArray: [4, 0] },
  markers: { size: 3 },
  xaxis: {
    categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug'],
    title: { text: 'Month' }
  },
  fill: { type: 'solid', opacity: [1, 0.1] },
  legend: { position: 'top', horizontalAlign: 'right' }
};
```

- **Chart Options**: Defines the chart's appearance and behavior, such as color schemes, axis labels, and legend positioning.
- **Toolbar & Zoom**: Disabled for a cleaner UI.
- **Stroke & Markers**: Adds a smooth curve to the lines with specific marker sizes.

### 🖼️ Render Method

```javascript
return (
  <React.Fragment>
    <Card>
      <CardBody>
        <h4 className="card-title mb-4">Sales Report</h4>
        <ReactApexChart options={options} series={series} height="260" type="line" className="apex-charts" />
      </CardBody>
    </Card>
  </React.Fragment>
);
```

- **Render**: The component is wrapped in a `Card` with a title for better presentation. The `ReactApexChart` component renders the chart using configured options and series.

### 📤 Export

```javascript
export default LineChart;
```

- **Export**: The component is exported as the default export, making it available for import in other modules.

## 🔍 Key Features

- **Dual Visualization**: Combines line and area charts to represent different datasets.
- **Responsive Design**: Adapts to various screen sizes due to the use of Bootstrap components.
- **Customizable**: Easily changeable chart options to suit specific requirements.

## ✔️ Usage

To use the **Line Chart** component, simply import it into your desired file and include it within your JSX:

```javascript
import LineChart from './line-chart';

function App() {
  return (
    <div>
      <LineChart />
    </div>
  );
}
```

## 🎨 Styles and Themes

- **Colors**: The chart uses a soothing green and blue color palette, enhancing visual appeal and clarity.
- **Typography**: Font sizes and styles are consistent with Bootstrap's default settings, offering a clean and professional look.

## 📚 Additional Notes

- The component is designed for simplicity and ease of integration into existing dashboards.
- Consider adjusting the `series` data and `options` configuration to reflect different datasets or enhance visual aesthetics.

Feel free to modify and adapt this component to fit your specific use case. Happy coding! 🚀

# 📜 Documentation for `latest-transaction.js`

## 📋 Overview

The `latest-transaction.js` file is a React component that provides functionality to display and manage the latest user transactions. This component is part of a larger dashboard, likely used for administrative tasks. It allows users to view transaction history, seize wallet balances, release or seize particular winnings, and paginate through transaction data.

## 🧩 Components and Functions

### Imports

- **React Components and Hooks**: Utilizes `React`, `useEffect`, `useState` for component lifecycle and state management.
- **Reactstrap Components**: Uses `Card`, `CardBody`, `Col`, `Button` for UI layout.
- **API Helper Methods**: Includes functions like `releaseWinningOfUser`, `seizeParticularWinningOfUser`, etc., to interact with backend APIs.
- **Utility Functions and Constants**: Utilizes utilities and constants from local imports for permission handling and payment methods.
- **Additional Libraries**: 
  - `SweetAlert` for alert modals.
  - `Paginator` for pagination.
  - `lodash` for utility functions.

### State Variables

- **Pagination and Transaction Data**: 
  - `pageNumber`, `totalCount` for pagination.
  - `transactionHistory` for storing transaction records.
  - `loader` to manage loading state.
  
- **Alerts and Messages**: 
  - `openSuccessMessage`, `successMessage` for success notifications.
  - `confirm_alert_For_Seize_Wallet` to manage wallet seize alert state.
  - `openSuccessMessage2`, `successMessage2` for additional success messages.
  
- **Permissions and Conditions**: 
  - `changePermission` to manage permission visibility.
  - `disableSwal`, `disableSwal2`, `disableSwalOnSeize` to disable buttons during async operations.

### Main Functionalities

- **`useEffect` Hook**: 
  - Calls `callTransaction` to fetch transaction data when component mounts or `pageNumber` changes.
  - Checks and sets permissions via `callSetPermission`.

- **Transaction Fetch**: 
  - `callTransaction`: Asynchronously fetches user transaction history and updates state.

- **Permission Handling**: 
  - `callSetPermission`: Configures component based on user permissions.

- **Wallet Seize and Release**: 
  - `openAlertForSeizeWallet`, `seizeWalletOnSubmit` manage wallet seizing operations.
  - `openHoldStatusTransaction`, `onRelease`, `onSeizeParticularTransaction` for seizing or releasing particular winnings.

- **Pagination**: 
  - `handlePageClick` updates the current page number.

### JSX Structure

- **Button for Seizing Wallet**: 
  - Conditional rendering based on permissions.
  
- **Table for Transaction History**: 
  - Displays transactions with details like date, payee, receiver, payment type, etc.
  - Conditional buttons for seizing/releasing amounts depending on transaction status and permissions.
  
- **Alerts**: 
  - Utilizes `SweetAlert` for confirmation dialogs and success notifications.
  
- **Pagination Component**: 
  - `Paginator` to navigate through pages of transaction data.

## 🛠️ Usage

This component is used within a dashboard to manage user transactions. It is integrated with backend APIs to fetch and update transaction data and provides administrators with tools to manage user finances securely.

## 🎨 User Interface

- **Responsive Design**: Uses `reactstrap` for responsive components.
- **Interactive Alerts**: Provides a user-friendly experience for actions requiring confirmation.
- **Pagination**: Allows easy navigation through large datasets.

## ⚙️ Dependencies

- React and React Hooks
- Reactstrap for UI components
- SweetAlert for modals
- Lodash for utility functions

## 🔗 Integration

This component should be integrated with a backend service that supports the provided API helper functions for full functionality. It's part of a larger dashboard, interacting with other components like `Paginator` and permission utilities.

---

This documentation provides a comprehensive overview of the `latest-transaction.js` file, explaining its purpose, functionality, and integration within a larger system. It is designed for developers looking to understand or modify this component.

# 📄 Recent Activity Component Documentation

## Overview

The **RecentActivity** component is a React component designed to display a list of recent activities within a card interface. It includes a dropdown to filter activities and utilizes simple scrolling for more user-friendly navigation of the activity log.

## Features

- 📋 **Activity Log**: Displays a list of recent activities with timestamps and descriptions.
- 🔽 **Dropdown Filter**: Allows users to filter the activity log based on different criteria.
- 🖱️ **Smooth Scrolling**: Implements smooth scrolling for the activity list using the `simplebar-react` library.

## Component Structure

### Import Statements

The component imports essential modules from React, Reactstrap, and other libraries:

- **React**: For creating the component.
- **Reactstrap**: For utilizing styled components like `Card`, `CardBody`, `Dropdown`, etc.
- **SimpleBar**: For enabling smooth, customizable scrolling.

```javascript
import React from "react";
import { Card, CardBody, DropdownToggle, DropdownMenu, DropdownItem, UncontrolledDropdown } from "reactstrap";
import SimpleBar from "simplebar-react";
```

### Component Definition

The **RecentActivity** component is defined as a functional component. It returns a structured JSX layout representing the recent activity card.

```javascript
const RecentActivity = () => {
  return (
    <Card>
      <CardBody>
        ...
      </CardBody>
    </Card>
  );
};
```

### Dropdown Filter

An unguarded dropdown component is utilized to offer filtering options:

- **DropdownToggle**: A clickable element to toggle the dropdown menu.
- **DropdownMenu**: Contains options like "Recent" and "By Users".

```javascript
<UncontrolledDropdown>
  <DropdownToggle tag="a" className="text-reset" id="dropdownMenuButton5" caret>
    <span className="text-muted">Recent<i className="mdi mdi-chevron-down ms-1"></i></span>
  </DropdownToggle>
  <DropdownMenu className="dropdown-menu-end">
    <DropdownItem href="#">Recent</DropdownItem>
    <DropdownItem href="#">By Users</DropdownItem>
  </DropdownMenu>
</UncontrolledDropdown>
```

### Activity Feed

A `SimpleBar` is used for smooth scrolling, providing a maximum height to ensure the content is scrollable:

- **Feed Items**: Display activity details such as date, time, and description.
- **Styling**: Each feed item is styled for readability including date and time in a muted font, and highlighted activity titles.

```javascript
<SimpleBar className="activity-feed mb-0 ps-2" style={{ maxHeight: '336px' }}>
  <li className="feed-item">
    <div className="feed-item-list">
      <p className="text-muted mb-1 font-size-13">Today<small className="d-inline-block ms-1">12:20 pm</small></p>
      <p className="mt-0 mb-0">Andrei Coman magna sed porta finibus, risus posted a new article: <span className="text-primary">Forget UX Rowland</span></p>
    </div>
  </li>
  {/* More feed items */}
</SimpleBar>
```

## Usage

To use the **RecentActivity** component in your project, ensure that all dependencies such as `reactstrap` and `simplebar-react` are installed. Import and include the component where you need a recent activity log.

```javascript
import RecentActivity from './recent-activity';

// Within your JSX
<RecentActivity />
```

## Conclusion

The **RecentActivity** component offers a straightforward method to display and interact with an activity feed. Its use of dropdown filters and smooth scrolling enhances user experience, making it a versatile component for modern web applications. 📝✨

## Dependencies

- **React**: ^16.8.0
- **Reactstrap**: ^8.0.0
- **SimpleBar**: ^5.0.0

> **Note**: Ensure you have React, Reactstrap, and SimpleBar installed in your project to use this component effectively.

# 📄 Overview.js Documentation

## 📋 Table of Contents
1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Functionality](#functionality)
4. [Code Explanation](#code-explanation)
5. [Conclusion](#conclusion)

## 📌 Introduction

The **Overview.js** file is a React component that provides an at-a-glance summary of key metrics such as New Visitors, Product Views, and Revenue. This component is typically used in dashboards to give users quick insights into performance statistics. It utilizes the **reactstrap** library for layout and styling, which is based on Bootstrap.

## 🏗️ Component Structure

The component is structured using Bootstrap's grid system, with a card that displays three main statistics:
- **New Visitors**
- **Product Views**
- **Revenue**

Each statistic is accompanied by a progress bar and a percentage change indicator.

## ⚙️ Functionality

The component displays:
- **New Visitors**: The total number of new visitors within a specified period.
- **Product Views**: The total number of product views.
- **Revenue**: The total revenue generated.

For each metric, it shows:
- The current value.
- A percentage change, indicating the direction of change with an arrow.
- A progress bar that visually represents the percentage change.

## 🧩 Code Explanation

Here's a detailed breakdown of the code:

```javascript
import React from 'react';
import { Card, CardBody, Col, Row } from 'reactstrap';

const Overview = () => {
    return (
        <React.Fragment>
            <Col xl={3}>
                <Card>
                    <CardBody>
                        <h4 className="card-title mb-4">Overview</h4>
                        <div>
                            <div className="pb-3 border-bottom">
                                <Row className="align-items-center">
                                    <Col xs={8}>
                                        <p className="mb-2">New Visitors</p>
                                        <h4 className="mb-0">3,524</h4>
                                    </Col>
                                    <Col xs={4}>
                                        <div className="text-end">
                                            <div> 2.06 % <i className="mdi mdi-arrow-up text-success ms-1"></i> </div>
                                            <div className="progress progress-sm mt-3">
                                                <div className="progress-bar" role="progressbar" style={{ width: '62%' }} aria-valuenow="62" aria-valuemin="0" aria-valuemax="100"></div>
                                            </div>
                                        </div>
                                    </Col>
                                </Row>
                            </div>
                            <div className="py-3 border-bottom">
                                <Row className="align-items-center">
                                    <Col xs={8}>
                                        <p className="mb-2">Product Views</p>
                                        <h4 className="mb-0">2,465</h4>
                                    </Col>
                                    <Col xs={4}>
                                        <div className="text-end">
                                            <div> 0.37 % <i className="mdi mdi-arrow-up text-success ms-1"></i> </div>
                                            <div className="progress progress-sm mt-3">
                                                <div className="progress-bar bg-warning" role="progressbar" style={{ width: '48%' }} aria-valuenow="48" aria-valuemin="0" aria-valuemax="100"></div>
                                            </div>
                                        </div>
                                    </Col>
                                </Row>
                            </div>
                            <div className="pt-3">
                                <Row className="align-items-center">
                                    <Col xs={8}>
                                        <p className="mb-2">Revenue</p>
                                        <h4 className="mb-0">$ 4,653</h4>
                                    </Col>
                                    <Col xs={4}>
                                        <div className="text-end">
                                            <div> 2.18 % <i className="mdi mdi-arrow-up text-success ms-1"></i> </div>
                                            <div className="progress progress-sm mt-3">
                                                <div className="progress-bar bg-success" role="progressbar" style={{ width: '78%' }} aria-valuenow="78" aria-valuemin="0" aria-valuemax="100"></div>
                                            </div>
                                        </div>
                                    </Col>
                                </Row>
                            </div>
                        </div>
                    </CardBody>
                </Card>
            </Col>
        </React.Fragment>
    )
}

export default Overview;
```

### Key Elements:
- **Col**: Uses Bootstrap's grid system to define layout.
- **Card & CardBody**: Used to create a container with a header and body.
- **Row & Col**: Nested within the card to organize the layout of the statistics.
- **Progress Bars**: Visual representation of percentage changes.

### Features:
- **Dynamic Content**: Though this example uses hardcoded numbers, the structure supports dynamic data integration.
- **Responsive Design**: Utilizes Bootstrap classes for responsive layout.

## 🏁 Conclusion

The **Overview.js** component is a simple but effective way to present key metrics in a dashboard. It leverages React and Reactstrap to ensure a clean, responsive design and can be easily extended to accommodate dynamic data sources. This component is a crucial part of any analytical dashboard, providing users with quick insights into their data.

# 📊 Revenue Chart Component Documentation

## Overview

The **RevenueChart** component is a React component that renders a bar chart to visualize revenue data across different categories (months). This component utilizes the `ReactApexChart` for rendering the chart and connects to a Redux store to access the layout properties. This allows the chart to adapt its width based on the layout context (e.g., whether it's boxed or full-width).

## Content

- [Component Structure](#component-structure)
- [Dependencies](#dependencies)
- [Props and State](#props-and-state)
- [Chart Configuration](#chart-configuration)
- [Color Coding](#color-coding)
- [Redux Integration](#redux-integration)
- [Usage](#usage)

## Component Structure

```jsx
import React from "react";
import ReactApexChart from "react-apexcharts";
import { Card, CardBody } from "reactstrap";
import { connect } from "react-redux";

const RevenueChart = (props) => {
  // Series and options for the chart
  const series = [
    { name: 'Series A', data: [11, 17, 15, 15, 21, 14] },
    { name: 'Series B', data: [13, 23, 20, 8, 13, 27] },
    { name: 'Series C', data: [44, 55, 41, 67, 22, 43] }
  ];

  const options = {
    chart: {
      stacked: true,
      toolbar: { show: false },
      zoom: { enabled: true }
    },
    plotOptions: {
      bar: {
        horizontal: false,
        columnWidth: '20%',
        endingShape: 'rounded'
      },
    },
    dataLabels: { enabled: false },
    xaxis: {
      categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
    },
    colors: ['#eef3f7', '#ced6f9', '#3b5de7'],
    fill: { opacity: 1 }
  };

  const width = props.layoutWidth === "boxed" ? 260 : 296.828;

  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <h4 className="card-title mb-4">Revenue</h4>
          <div id="revenuechart">
            <ReactApexChart options={options} series={series} width={width} height={260} type="bar" className="apex-charts" />
          </div>
        </CardBody>
      </Card>
    </React.Fragment>
  );
};

const mapStateToProps = state => {
  return { ...state.Layout };
};

export default connect(mapStateToProps, null)(RevenueChart);
```

## Dependencies

- **React**: For building the component.
- **React-ApexCharts**: For rendering the chart.
- **Reactstrap**: For using Bootstrap-styled components.
- **Redux**: To connect the component to the application's state.

## Props and State

- **Props**:
  - `layoutWidth`: Determines the width of the chart based on the layout context (boxed or full-width).

## Chart Configuration

- **Series Data**:
  - **Series A**: `[11, 17, 15, 15, 21, 14]`
  - **Series B**: `[13, 23, 20, 8, 13, 27]`
  - **Series C**: `[44, 55, 41, 67, 22, 43]`

- **Options**:
  - **Chart Type**: Bar
  - **Stacking**: Enabled
  - **Horizontal Bars**: Disabled
  - **Colors**: Different shades of blue for visual distinction.

## Color Coding

- **Series A**: `#eef3f7`
- **Series B**: `#ced6f9`
- **Series C**: `#3b5de7`

## Redux Integration

The component is connected to the Redux store to access layout properties, allowing dynamic width adjustment:

```javascript
const mapStateToProps = state => {
  return { ...state.Layout };
};
```

## Usage

To use the **RevenueChart** component, ensure that your Redux store has a `Layout` state with a `layoutWidth` attribute. Import the component and include it within your application layout:

```jsx
import RevenueChart from './revenue-chart';

const App = () => {
  return (
    <div>
      <RevenueChart />
    </div>
  );
};

export default App;
```

This component is ideal for dashboards where revenue visualization is required, and the dynamic width makes it adaptable for different screen sizes and layouts.

# Documentation for `Revenue.js` 📊

## Overview

The `Revenue.js` file is a React component that displays revenue analytics segregated by geographical location, particularly focusing on the United States. It utilizes a vector map to visually represent data, allowing for a more intuitive understanding of revenue distribution across different states.

---

## Table of Contents

1. [Component Structure](#component-structure)
2. [Dependencies](#dependencies)
3. [Key Features](#key-features)
4. [Code Explanation](#code-explanation)
5. [Usage](#usage)
6. [Visualization](#visualization)

---

## Component Structure

- **Component Name**: `Overview`
- **Export Type**: Default export
- **Primary Library Used**: `react-jvectormap`

---

## Dependencies

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: Used for Bootstrap 4 components in React.
- **react-jvectormap**: A React component for rendering vector maps.

---

## Key Features

- **Interactive Vector Map**: Displays a USA map highlighting revenue from different states.
- **Revenue Data Display**: Shows revenue figures for specific states like California and Nevada.
- **Responsive Design**: The component adjusts to various screen sizes, making it suitable for dashboards.

---

## Code Explanation

```javascript
import React from 'react';
import { Card, CardBody, Col, Row } from 'reactstrap';
import { VectorMap } from "react-jvectormap";

const map = React.createRef(null);

const Overview = () => {
    return (
        <React.Fragment>
            <Col lg={6}>
                <Card>
                    <CardBody>
                        <h4 className="card-title mb-4">Revenue by location</h4>
                        <Row>
                            <Col sm={6}>
                                <div id="usa-vectormap" style={{ height: '230px' }}>
                                    <VectorMap 
                                        map='us_aea' 
                                        backgroundColor="transparent" 
                                        ref={map} 
                                        handleWindowResize={true}
                                        containerStyle={{ width: "100%", height: "100%" }}
                                        regionStyle={{ initial: { fill: '#556ee6' } }}
                                        markerStyle={{
                                            initial: {
                                                r: 9,
                                                fill: '#556ee6',
                                                fillOpacity: 0.9,
                                                stroke: '#fff',
                                                strokeWidth: 7,
                                                strokeOpacity: 0.4
                                            },
                                            hover: {
                                                stroke: '#fff',
                                                fillOpacity: 1,
                                                strokeWidth: 1.5
                                            }
                                        }}
                                        containerClassName="map"
                                    />
                                </div>
                            </Col>
                            <Col sm={5} className="ms-auto">
                                <div className="mt-4 mt-sm-0">
                                    <p>Last month Revenue</p>
                                    <div className="d-flex align-items-start py-3">
                                        <div className="flex-1">
                                            <p className="mb-2">California</p>
                                            <h5 className="mb-0">$ 2,256</h5>
                                        </div>
                                        <div className="ms-auto">
                                            2.52 % <i className="mdi mdi-arrow-up text-success ms-1"></i>
                                        </div>
                                    </div>
                                    <div className="d-flex align-items-start py-3 border-top">
                                        <div className="flex-1">
                                            <p className="mb-2">Nevada</p>
                                            <h5 className="mb-0">$ 1,853</h5>
                                        </div>
                                        <div className="ms-auto">
                                            1.26 % <i className="mdi mdi-arrow-up text-success ms-1"></i>
                                        </div>
                                    </div>
                                </div>
                            </Col>
                        </Row>
                    </CardBody>
                </Card>
            </Col>
        </React.Fragment>
    )
}

export default Overview;
```

### Explanation

- **Vector Map**: Utilizes `VectorMap` from `react-jvectormap` to create an interactive map of the USA.
- **Revenue Information**: Shows revenue details for California and Nevada, including percentage changes.
- **Styling**: Uses Bootstrap classes for layout and styling, ensuring a consistent and responsive design.

---

## Usage

To use this component, ensure you have the necessary dependencies installed. You can include this component within a larger dashboard or analytics page to provide geographical revenue insights.

```javascript
import Overview from './Revenue';

// Usage within a larger component or page
<Overview />
```

---

## Visualization

- **Map**: The USA map highlights states with revenue data.
- **Revenue Display**: Presents numeric revenue data alongside percentage growth indicators.

---

This concludes the detailed documentation for the `Revenue.js` file. It provides a comprehensive view of how revenue is distributed geographically, making it an essential component for financial dashboards. 📈✨

# 📄 Documentation for `Reviews.js`

This document provides a comprehensive overview of the `Reviews.js` component, including its purpose, structure, and functionality. This component is designed to display customer reviews in a carousel format on a dashboard or similar interface.

## 📑 Table of Contents

1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Detailed Explanation](#detailed-explanation)
4. [Code Walkthrough](#code-walkthrough)

## 📘 Introduction

The **Reviews** component is a React functional component that displays a set of client reviews. It uses a carousel to cycle through different reviews, each accompanied by the reviewer's name and their position or company. The component is styled using Bootstrap's grid system and classes to ensure responsiveness and aesthetic appeal.

## 🏗️ Component Structure

The component is structured using several React and Bootstrap elements:

- **React.Fragment**: Used to wrap components without adding extra nodes to the DOM.
- **Col**: A Bootstrap column component to ensure the component fits well into a grid layout.
- **Card and CardBody**: Bootstrap components used to encapsulate the carousel and give it a card-style appearance.
- **Carousel**: A Bootstrap carousel for displaying reviews one at a time, with controls to navigate between them.

## 🔍 Detailed Explanation

### Purpose

The primary purpose of the `Reviews.js` component is to provide a compact and interactive way to display customer testimonials. It highlights positive feedback from clients, which can enhance the credibility and attractiveness of the service or product being offered.

### Features

- **Carousel Display**: The component employs a carousel to cycle through reviews, allowing users to view multiple testimonials in a limited space.
- **Client Details**: Each review includes the client's name, title, or position, which adds authenticity to the testimonials.
- **Interactivity**: Users can navigate through the reviews using the carousel controls.

## 🧩 Code Walkthrough

```jsx
import React from 'react';
import { Card, CardBody, Col } from 'reactstrap';

const Overview = () => {
    return (
        <React.Fragment>
            <Col lg={3} className="col-xl-3">
                <Card>
                    <CardBody>
                        <h4 className="card-title mb-4">Reviews</h4>
                        <div className="mb-4">
                            <h5><span className="text-primary">500</span>+ Satisfied clients</h5>
                        </div>
                        <div className="mb-3">
                            <i className="fas fa-quote-left h4 text-primary"></i>
                        </div>
                        <div id="reviewExampleControls" className="carousel slide review-carousel" data-ride="carousel">
                            <div className="carousel-inner">
                                <div className="carousel-item active">
                                    <div>
                                        <p>To achieve this, it would be necessary to have uniform grammar, pronunciation and more common words</p>
                                        <div className="d-flex align-items-start mt-4">
                                            <div className="avatar-sm me-3">
                                                <span className="avatar-title bg-soft-primary text-primary rounded-circle"> J </span>
                                            </div>
                                            <div className="flex-1">
                                                <h5 className="font-size-16 mb-1">Jessie Mitchell</h5>
                                                <p className="mb-2">CEO of ABC Company</p>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <!-- Additional carousel items -->
                            </div>
                            <a className="carousel-control-prev" href="#reviewExampleControls" role="button" data-bs-slide="prev">
                                <i className="mdi mdi-chevron-left carousel-control-icon"></i>
                            </a>
                            <a className="carousel-control-next" href="#reviewExampleControls" role="button" data-bs-slide="next">
                                <i className="mdi mdi-chevron-right carousel-control-icon"></i>
                            </a>
                        </div>
                    </CardBody>
                </Card>
            </Col>
        </React.Fragment>
    )
}

export default Overview;
```

### Key Components

- **`<Card>`**: Used to encapsulate the review content, providing a neat and organized layout.
- **`<Carousel>`**: Contains multiple `<carousel-item>` elements, each representing a single review.
- **Carousel Controls**: Allow the user to navigate between different reviews.

### Styling and Layout

- **Responsive Design**: Utilizes Bootstrap's grid system to ensure the component is responsive and fits well within various screen sizes.
- **Icons and Typography**: Incorporates icons and styled text to enhance the visual appeal.

## 🎨 Conclusion

The `Reviews.js` component is an elegant and interactive way to display client testimonials, leveraging Bootstrap for responsive design and React for component structure. It enhances the user interface by providing insightful feedback and increasing user engagement through interactive elements.

# 📊 Sales Analytics Module Documentation

This document provides a comprehensive overview of the **Sales Analytics** component implemented in the file `sales-analytics.js`. This component is designed to visualize sales data across different channels using a dynamic graphical representation.

---

## 📄 Overview

The `SalesAnalytics` component is a React class-based component that leverages **ReactApexChart** to display a donut chart illustrating the distribution of sales through various channels: **Online**, **Offline**, and **Marketing**. These visual insights are crucial for understanding the sales trends and making informed business decisions.

---

## 📂 File Structure

- **Component:** SalesAnalytics
- **Libraries Used:**
  - `React`
  - `reactstrap`
  - `ReactApexChart`

---

## 📜 Code Breakdown

Here's a detailed breakdown of the code within the `sales-analytics.js` file:

### **Imports**

```javascript
import React, { Component } from "react";
import { Row, Col, Card, CardBody } from "reactstrap";
import ReactApexChart from "react-apexcharts";
```

- **React, Component:** Core React library and class-based component structure.
- **reactstrap:** Provides Bootstrap 4 components as React components.
- **ReactApexChart:** A React component for ApexCharts that renders the chart.

### **Component Definition**

The `SalesAnalytics` component is defined as a class-based component extending from `React.Component`.

```javascript
class SalesAnalytics extends Component {
  // Constructor and state initialization
  constructor(props) {
    super(props);
    this.state = {
      series: [38, 26, 14],
      options: {
        labels: ["Online", "Offline", "Marketing"],
        plotOptions: {
          pie: {
            donut: {
              size: '75%',
            },
          },
        },
        legend: {
          show: false,
        },
        colors: ['#3b5de7', '#45cb85', '#eeb902'],
      },
    };
  }
}
```

#### **State Configuration**

- **series:** An array representing the percentages of sales through different channels.
- **options:** Object containing configuration for the chart such as labels, plot options, and colors.

### **Render Method**

The `render` method contains the JSX structure for rendering the component UI.

```javascript
render() {
  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <h4 className="card-title mb-4">Sales Analytics</h4>
          <Row className="align-items-center">
            <Col sm={6}>
              <ReactApexChart 
                options={this.state.options}
                series={this.state.series}
                type="donut"
                height={245}
                className="apex-charts"
              />
            </Col>
            <Col sm={6}>
              <div>
                <Row>
                  <div className="col-6">
                    <div className="py-3">
                      <p className="mb-1 text-truncate">
                        <i className="mdi mdi-circle text-primary me-1"></i>
                        Online
                      </p>
                      <h5>$ 2,652</h5>
                    </div>
                  </div>
                  <div className="col-6">
                    <div className="py-3">
                      <p className="mb-1 text-truncate">
                        <i className="mdi mdi-circle text-success me-1"></i>
                        Offline
                      </p>
                      <h5>$ 2,284</h5>
                    </div>
                  </div>
                  <div className="col-6">
                    <div className="py-3">
                      <p className="mb-1 text-truncate">
                        <i className="mdi mdi-circle text-warning me-1"></i>
                        Marketing
                      </p>
                      <h5>$ 1,753</h5>
                    </div>
                  </div>
                </Row>
              </div>
            </Col>
          </Row>
        </CardBody>
      </Card>
    </React.Fragment>
  );
}
```

### **UI Components**

- **Card & CardBody:** Wrapping container for the chart and sales details.
- **ReactApexChart:** The donut chart visualizing sales distribution.
- **Row & Col:** Bootstrap grid for layout management.
- **Icons & Labels:** Display sales data with corresponding icons and labels for different sales channels.

---

## 🔍 Key Features

- **Donut Chart:** Visual representation of sales distribution using a donut chart.
- **Channel Breakdown:** Sales figures categorized by channels - Online, Offline, and Marketing.
- **Responsive Design:** Leverages Bootstrap grid system for a responsive layout.

---

## 📈 Visual Representation

The component displays a donut chart with segments representing the percentage of sales from different channels, providing a clear and concise visual overview of sales performance.

---

## 💡 Usage

To integrate the SalesAnalytics component into a parent component or dashboard:

```javascript
import SalesAnalytics from './sales-analytics.js';

// Use within JSX
<SalesAnalytics />
```

Ensure that any required CSS for react-apexcharts and reactstrap is included in your project for proper styling and functionality.

---

## ✨ Conclusion

The `SalesAnalytics` component is a powerful tool for visualizing sales data, enabling businesses to quickly assess the performance of different sales channels. Its interactive and visually appealing design makes it an excellent addition to any analytics dashboard.

# Scatter-Analytics.js Documentation 📊

## Overview

The **scatter-analytics.js** file is a React component designed to render a scatter plot chart using the `ReactApexChart` library. This chart visualizes two series of data points, providing a quick visual representation of monthly sales or other comparative datasets.

## Purpose 🎯

The component is utilized to display a scatter chart within a dashboard or any React application that requires graphical representation of data. The scatter chart is an effective way to show relationships between two numerical axes, often used in sales analytics to compare different datasets.

## Component Structure

The component is a functional React component named `scatterChart` that returns a JSX structure with the necessary elements to render a chart.

### Key Imports

- **React**: The foundational library for building UI components.
- **ReactApexChart**: A React wrapper for ApexCharts, a modern charting library.
- **reactstrap**: Provides Bootstrap 4 components for React.

### Data Series 📈

Two data series are defined:

- **Series A**: Contains pairs of x and y coordinates.
- **Series B**: Contains another set of x and y coordinates, allowing for comparison with Series A.

```javascript
const series = [
  { name: "Series A", data: [[2, 5], [7, 2], [4, 3], ...] },
  { name: "Series B", data: [[15, 13], [7, 11], [5, 8], ...] }
];
```

### Chart Options ⚙️

- **Chart Type**: Scatter.
- **Zoom**: XY directional zoom is enabled for detailed analysis.
- **Colors**: Custom colors are set for each series for clear differentiation.
- **Legend Position**: Positioned at the top for easy identification of series.
- **Axis Configuration**: Custom tick amounts are set for both x and y axes.

```javascript
const options = {
  chart: {
    height: 350,
    type: 'scatter',
    toolbar: { show: false },
    zoom: { enabled: true, type: 'xy' }
  },
  colors: ['#3b5de7', '#45cb85'],
  xaxis: { tickAmount: 10 },
  legend: { position: 'top' },
  yaxis: { tickAmount: 7 }
};
```

### Rendering 🖼️

The chart is enclosed within a card layout for a neat presentation:

```jsx
<Card>
  <CardBody>
    <h4 className="card-title mb-4">Monthly Sales</h4>
    <ReactApexChart
      options={options}
      series={series}
      height="225"
      type="scatter"
      className="apex-charts"
    />
  </CardBody>
</Card>
```

### Export

The component is exported as the default export, making it easy to import and use in other parts of the application.

```javascript
export default scatterChart;
```

## Conclusion

The **scatter-analytics.js** file provides a visually engaging and customizable scatter chart component, utilizing the powerful `ReactApexChart` library. It is well-suited for applications requiring data visualization and can be easily integrated into any React-based dashboard or analytics page.

# 📄 Documentation for SocialSource.js

## Overview
The **SocialSource.js** file is a React component that displays a card with social media sales data. It incorporates dropdown menus for selecting the time period, icons representing different social media platforms, and visual indicators of sales performance.

## Table of Contents
- [Component Structure](#component-structure)
- [UI Elements](#ui-elements)
- [Code Explanation](#code-explanation)
- [Usage](#usage)

## Component Structure
- **Card**: The main container for the social media sales data.
- **Dropdown**: Allows users to select the time period for which data is displayed (Yearly, Monthly, Weekly).
- **Social Media Icons and Sales Data**: Displays sales figures for Facebook, Twitter, and Instagram.
- **Links**: Provides links to learn more or view all sources.

## UI Elements

| Element         | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| Card            | Contains the entire social source information.                              |
| Dropdown        | Allows selection of different time periods.                                 |
| Icon            | Visual representation of social media platforms (Facebook, Twitter, Instagram). |
| Sales Data      | Numerical display of sales from each platform.                              |
| Links           | Navigation links for additional information.                                |

## Code Explanation

```javascript
import React from "react"
import { Card, CardBody, UncontrolledDropdown, DropdownToggle, DropdownMenu, DropdownItem, Row, Col } from "reactstrap"
import { Link } from "react-router-dom"

const SocialSource = () => {
    return (
        <Card>
            <CardBody>
                <div className="float-end">
                    <UncontrolledDropdown>
                        <DropdownToggle tag="a" className="text-reset" id="dropdownMenuButton5" caret>
                            <span className="text-muted">Monthly<i className="mdi mdi-chevron-down ms-1"></i></span>
                        </DropdownToggle>
                        <DropdownMenu className="dropdown-menu-end">
                            <DropdownItem href="#">Yearly</DropdownItem>
                            <DropdownItem href="#">Monthly</DropdownItem>
                            <DropdownItem href="#">Weekly</DropdownItem>
                        </DropdownMenu>
                    </UncontrolledDropdown>
                </div>
                <h4 className="card-title">Social Source</h4>
                <div className="text-center">
                    <div className="avatar-sm mx-auto mb-4">
                        <span className="avatar-title rounded-circle bg-soft-primary font-size-24">
                            <i className="mdi mdi-facebook text-primary"></i>
                        </span>
                    </div>
                    <p className="font-16 text-muted mb-2"></p>
                    <h5><Link to="#" className="text-dark">Facebook - <span className="text-muted font-16">125 sales</span> </Link></h5>
                    <p className="text-muted">Maecenas nec odio et ante tincidunt tempus. Donec vitae sapien ut libero venenatis faucibus tincidunt.</p>
                    <Link to="#" className="text-reset font-16">Learn more <i className="mdi mdi-chevron-right"></i></Link>
                </div>
                <Row className="mt-4">
                    <Col className="col-4">
                        <div className="social-source text-center mt-3">
                            <div className="avatar-xs mx-auto mb-3">
                                <span className="avatar-title rounded-circle bg-primary font-size-16">
                                    <i className="mdi mdi-facebook text-white"></i>
                                </span>
                            </div>
                            <h5 className="font-size-15">Facebook</h5>
                            <p className="text-muted mb-0">125 sales</p>
                        </div>
                    </Col>
                    <Col className="col-4">
                        <div className="social-source text-center mt-3">
                            <div className="avatar-xs mx-auto mb-3">
                                <span className="avatar-title rounded-circle bg-info font-size-16">
                                    <i className="mdi mdi-twitter text-white"></i>
                                </span>
                            </div>
                            <h5 className="font-size-15">Twitter</h5>
                            <p className="text-muted mb-0">112 sales</p>
                        </div>
                    </Col>
                    <Col className="col-4">
                        <div className="social-source text-center mt-3">
                            <div className="avatar-xs mx-auto mb-3">
                                <span className="avatar-title rounded-circle bg-pink font-size-16">
                                    <i className="mdi mdi-instagram text-white"></i>
                                </span>
                            </div>
                            <h5 className="font-size-15">Instagram</h5>
                            <p className="text-muted mb-0">104 sales</p>
                        </div>
                    </Col>
                </Row>
                <div className="mt-3 text-center">
                    <Link to="#" className="text-primary font-size-14 fw-medium">View All Sources <i className="mdi mdi-chevron-right"></i></Link>
                </div>
            </CardBody>
        </Card>
    )
}

export default SocialSource
```

### Key Features
- **Dropdown Menu**: Allows users to switch between different time periods to view sales data.
- **Dynamic Icons and Figures**: Displays sales figures for each social media platform, with an icon representing each platform.
- **Interactive Links**: Provides links to additional resources or more detailed data.

## Usage
This component can be used in any React application where social media sales data needs to be displayed in a visually appealing manner. Simply import the `SocialSource` component and include it in your JSX.

```javascript
import SocialSource from './path/to/SocialSource';

// Usage in a React component
function App() {
    return (
        <div>
            <SocialSource />
        </div>
    );
}
```

This documentation provides a comprehensive overview of the **SocialSource.js** component, its structure, functionality, and usage in applications. With its interactive elements and clean design, it is a useful component for dashboards and analytics interfaces.

# Top Selling Products Component Documentation

## Overview

The **Top Selling Products** component is designed to display a list of products with their corresponding sales progress. It utilizes a combination of React and Reactstrap to create a user-friendly interface that allows users to quickly view and sort the top-selling products.

![Top Selling Products](https://img.icons8.com/color/48/000000/top-seller.png)

## File: `topselling-product.js`

### Purpose

This component is used to present a visual representation of the sales performance of various products using progress bars. Each product is displayed with a progress bar indicating the percentage of sales relative to other products.

### Functionality

- **Dropdown for Sorting:** Users can sort the product list by different time periods: Monthly, Yearly, or Weekly.
- **Progress Bars:** Each product has a progress bar showing its sales percentage with different colors for easy differentiation.
  
### Dependencies

- **React:** A JavaScript library for building user interfaces.
- **Reactstrap:** A library that provides Bootstrap 4 components as React components.

### Code Explanation

```javascript
import React from "react";
import { Card, CardBody, UncontrolledDropdown, DropdownToggle, DropdownMenu, DropdownItem, Row, Col, Progress } from "reactstrap";

const TopProduct = () => {
    // Define the product data with their progress value and color
    const progressbars = [
        { id: 1, title: 'Desktops', value: 52, color: 'primary' },
        { id: 2, title: 'iPhones', value: 45, color: 'info' },
        { id: 3, title: 'Android', value: 48, color: 'success' },
        { id: 4, title: 'Tablets', value: 78, color: 'warning' },
        { id: 5, title: 'Cables', value: 63, color: 'purple' },
    ];

    return (
        <React.Fragment>
            <Card>
                <CardBody>
                    <div className="float-end">
                        <UncontrolledDropdown>
                            <DropdownToggle tag="a" className="text-reset" id="dropdownMenuButton5" caret href="#">
                                <span className="fw-semibold">Sort By:</span> 
                                <span className="text-muted">Yearly<i className="mdi mdi-chevron-down ms-1"></i></span>
                            </DropdownToggle>
                            <DropdownMenu className="dropdown-menu-end">
                                <DropdownItem href="#">Monthly</DropdownItem>
                                <DropdownItem href="#">Yearly</DropdownItem>
                                <DropdownItem href="#">Weekly</DropdownItem>
                            </DropdownMenu>
                        </UncontrolledDropdown>
                    </div>
                    <h4 className="card-title mb-4">Top Selling Products</h4>
                    {progressbars.map((progressbar, key) => (
                        <Row className="align-items-center g-0 mt-3" key={key}>
                            <Col sm={3}>
                                <p className="text-truncate mt-1 mb-0">
                                    <i className="mdi mdi-circle-medium text-warning me-2"></i> {progressbar.title}
                                </p>
                            </Col>
                            <Col sm={9}>
                                <div className="mt-1" style={{ height: "6px" }}>
                                    <Progress value={progressbar.value} color={progressbar.color} size="sm" className="progress-sm" />
                                </div>
                            </Col>
                        </Row>
                    ))}
                </CardBody>
            </Card>
        </React.Fragment>
    );
};

export default TopProduct;
```

### Key Components

- **Card & CardBody:** Used to encapsulate the content of the component, providing a structured and styled layout.
- **UncontrolledDropdown, DropdownToggle, DropdownMenu, DropdownItem:** These components provide a dropdown menu feature for sorting the product list.
- **Row & Col:** Used for responsive layout, aligning the product titles and progress bars.
- **Progress:** Displays a progress bar indicating the sales percentage for each product.

### Usage

This component can be used in any React-based dashboard or analytics application where you need to display the sales performance of various products in a visually appealing manner.

### Styling

- The component uses various Bootstrap classes to ensure a responsive and clean design.
- Different colors are used for progress bars to make it easier to differentiate between products.

---

With this documentation, developers can easily understand the purpose and functionality of the **Top Selling Products** component and integrate it into their applications for enhanced sales visualization.

# Documentation for `topuser.js`

## Overview
The `topuser.js` file is a React component that displays a list of top users in a card format. It utilizes various libraries such as Reactstrap for UI components, SimpleBar for custom scrollbar styling, and includes avatar images for visual representation of users.

## Component Breakdown

### Imports
- **React**: The core library for building the UI.
- **Reactstrap Components**: 
  - `Card`, `CardBody`: Used for creating structured card components which encapsulate the UI elements.
  - `DropdownToggle`, `DropdownMenu`, `DropdownItem`, `UncontrolledDropdown`: Used to create a dropdown menu for filtering options.
  - `Table`: To display the list of users in a tabular format.
- **SimpleBar**: Provides a custom scrollbar look and feel.
- **Avatar Images**: Imported images to represent user avatars.

### Component Structure
```javascript
const TopUser = () => {
  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <div className="float-end">
            <UncontrolledDropdown>
              <DropdownToggle tag="a" className="text-reset" id="dropdownMenuButton5" caret>
                <span className="text-muted">All Members<i className="mdi mdi-chevron-down ms-1"></i></span>
              </DropdownToggle>
              <DropdownMenu className="dropdown-menu-end">
                <DropdownItem href="#">Locations</DropdownItem>
                <DropdownItem href="#">Revenue</DropdownItem>
                <DropdownItem href="#">Join Date</DropdownItem>
              </DropdownMenu>
            </UncontrolledDropdown>
          </div>
          <h4 className="card-title mb-4">Top Users</h4>
          <SimpleBar style={{ maxHeight: "336px" }}>
            <div className="table-responsive">
              <Table className="table-borderless table-centered table-nowrap">
                <tbody>
                  {/* User rows go here */}
                </tbody>
              </Table>
            </div>
          </SimpleBar>
        </CardBody>
      </Card>
    </React.Fragment>
  )
}
```

### Features
- **Dropdown Menu**: Offers sorting options such as by Location, Revenue, and Join Date.
- **Scrollable Table**: Displays user information using SimpleBar for an elegant scrollbar within the card.
- **User Details**: Each row in the table provides:
  - **Avatar**: A small circular image representing the user.
  - **Name**: The user's name.
  - **Location**: The user's location marked by a pin icon.
  - **Status Badge**: Indicates the user's status (e.g., Cancel, Success, Active, Pending) using color-coded badges.

### Usage
This component is designed to be a part of a larger dashboard or user management system, where it provides a quick overview of key users. It integrates well using React components and supports a responsive layout.

## Styling
- **Avatars**: Rounded and small-sized for a clean look.
- **Badges**: Color-coded and soft, indicating different user statuses.
- **Dropdown**: Provides a clean and intuitive interface for sorting user data.

## Dependencies
- **React**: For building the component.
- **Reactstrap**: For UI components and styling.
- **SimpleBar**: For custom scrollbar appearance.

## Conclusion
The `topuser.js` component efficiently displays a list of top users with interactive features such as sorting and custom scrollbar. It is a versatile component suitable for dashboards requiring user insights and analytics.