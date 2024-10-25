# 📄 ActivityComp.js Documentation

## Overview

The `ActivityComp.js` file is a **React component** that displays a card with a list of activities. Each activity is accompanied by an icon, a date, and a brief description. This component is designed to be a part of a user interface where activity tracking or historical logs are required.

### Key Features

- **Display of Activities**: Shows a list of activities with associated dates and descriptions.
- **Interactive Elements**: Includes icons and links to enhance user interface interaction.
- **Reusable Component**: Can be integrated into larger applications where activity tracking is necessary.

## Table of Contents

1. [Installation](#installation)
2. [Component Structure](#component-structure)
3. [Usage](#usage)
4. [Code Explanation](#code-explanation)
5. [Styling and Dependencies](#styling-and-dependencies)
6. [Conclusion](#conclusion)

## Installation

To use the `ActivityComp` component, ensure you have **React** and **Reactstrap** installed in your project.

```bash
npm install react react-dom react-router-dom reactstrap
```

## Component Structure

The component is structured as follows:

- **Card**: The main container for the activities.
- **CardBody**: Holds the content of the card.
- **CardTitle**: Displays the title "Activity".
- **Activity List**: An unordered list of activities, each with an icon, date, and description.
- **View More Button**: A button to load or view more activities.

## Usage

To incorporate the `ActivityComp` component into your application, import it and include it in your JSX:

```jsx
import ActivityComp from './ActivityComp';

function App() {
  return (
    <div className="App">
      <ActivityComp />
    </div>
  );
}

export default App;
```

## Code Explanation

Here's a detailed explanation of the `ActivityComp` code:

```javascript
import React, { Component } from "react";
import { Card, CardBody, CardTitle } from "reactstrap";
import { Link } from "react-router-dom";

class ActivityComp extends Component {
  constructor(props) {
    super(props);
    this.state = {};
  }

  render() {
    return (
      <React.Fragment>
        <Card>
          <CardBody>
            <CardTitle className="h4 mb-5">Activity</CardTitle>
            <ul className="list-unstyled activity-wid">
              {/* Activity Items */}
              <li className="activity-list">
                <div className="activity-icon avatar-xs">
                  <span className="avatar-title bg-soft-primary text-primary rounded-circle">
                    <i className="mdi mdi-calendar-edit"></i>
                  </span>
                </div>
                <div className="d-flex align-items-start">
                  <div className="me-3">
                    <h5 className="font-size-14">20 Jan <i className="mdi mdi-arrow-right text-primary align-middle ms-2"></i></h5>
                  </div>
                  <div className="flex-1">
                    <div>Responded to need “Volunteer Activities”</div>
                  </div>
                </div>
              </li>
              {/* More Activity Items... */}
            </ul>
            <div className="text-center mt-4">
              <Link to="" className="btn btn-primary btn-sm">
                View More <i className="mdi mdi-arrow-right ms-1" />
              </Link>
            </div>
          </CardBody>
        </Card>
      </React.Fragment>
    );
  }
}

export default ActivityComp;
```

### Key Components

- **React.Fragment**: Used to wrap multiple elements without adding extra nodes to the DOM.
- **Card & CardBody**: Components from Reactstrap that provide a styled card layout.
- **CardTitle**: Displays the title of the card with specific styling.
- **Activity List**: Each `<li>` represents an activity with an icon, date, and description.
- **Link**: From `react-router-dom`, used for navigation.

## Styling and Dependencies

This component uses **Reactstrap** for styling and layout. It also utilizes icon fonts from **Material Design Icons (mdi)** for activity icons. Ensure these dependencies are correctly set up in your project for the component to display as intended.

### Example Styles

Ensure you have the following classes defined in your CSS for proper styling:

- `.activity-wid`
- `.activity-list`
- `.avatar-xs`, `.avatar-title`
- `.bg-soft-primary`, `.text-primary`
- `.rounded-circle`, `.d-flex`, `.align-items-start`

## Conclusion

The `ActivityComp` component is a versatile and reusable component that provides a structured layout for displaying user activities. It enhances user interface interaction with visual elements and is easily integrable into larger applications. With the help of Reactstrap for styling, it ensures a consistent look and feel across the application. 🛠️🎨

# 📊 `EarningChart.js` Documentation

Welcome to the documentation for the **EarningChart.js** component. This file is a part of a financial dashboard, and its purpose is to display earning statistics using a bar chart. Below, you'll find a detailed explanation of how this component works and what it is used for.

---

## Table of Contents

1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Key Features](#key-features)
4. [Dependencies](#dependencies)
5. [Code Walkthrough](#code-walkthrough)
6. [Usage](#usage)

---

## Overview

The **EarningChart.js** component is a React functional component designed to present earnings data visually. It utilizes the `ReactApexChart` library to render a horizontal bar chart that displays the amount of earnings over a six-month period.

### 🏷️ Features:
- Displays total earnings for a specified period.
- Compares earnings for the current month and the previous month.
- Visualizes data using a horizontal bar chart.

---

## Component Structure

The component is structured using several elements from the `reactstrap` library to create a responsive layout. It is divided into two main sections:

1. **Earnings Summary**: Displays textual information about the earnings.
2. **Earnings Chart**: Visual representation of the earnings data.

---

## Key Features

Here's a brief overview of the main features and elements used in this component:

| Feature             | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **ReactApexChart**  | Used for rendering the horizontal bar chart.                                |
| **Card & CardBody** | Provides a card layout to encapsulate the content.                          |
| **React Router**    | Utilizes `Link` from `react-router-dom` for navigation.                     |
| **Responsive Grid** | Uses `Row` and `Col` from `reactstrap` to maintain a responsive design.     |

---

## Dependencies

To function correctly, the component relies on the following libraries:

- **React**: The core library for building the component.
- **Reactstrap**: Provides Bootstrap 4 components for React.
- **ReactApexChart**: A popular library for creating dynamic charts.
- **React Router**: Used for navigation links within the application.

---

## Code Walkthrough

Below is an annotated walkthrough of the key sections in the **EarningChart.js** component:

```jsx
import React from 'react';
import { Row, Col, Card, CardBody, CardTitle } from 'reactstrap';
import ReactApexChart from "react-apexcharts";
import { Link } from "react-router-dom";

// Data for the chart
const series = [{ data: [3, 6, 4, 7, 9, 4] }];

// Configuration options for the chart
const options = {
  chart: {
    toolbar: { show: false },
  },
  plotOptions: {
    bar: { horizontal: true, barHeight: '24%', endingShape: 'rounded' }
  },
  dataLabels: { enabled: false },
  colors: ['#556ee6'],
  xaxis: {
    categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
    title: { text: 'thousands' },
  },
};

const EarningChart = () => {
  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <CardTitle className="h4 mb-4">Earning</CardTitle>
          <Row>
            <Col lg={6}>
              <div>
                <p>1 Jan - 31 Jan, 2020</p>
                <p className="mb-2">Total Earning</p>
                <h4>$ 12,362</h4>
              </div>
              <Row>
                <Col sm={6}>
                  <div className="mt-3">
                    <p className="mb-2 text-truncate">This Month</p>
                    <h5 className="d-inline-block align-middle mb-0">$ 9,245</h5>
                    <span className="badge badge-soft-success">+ 1.5 %</span>
                  </div>
                </Col>
                <Col sm={6}>
                  <div className="mt-3">
                    <p className="mb-2 text-truncate">Last Month</p>
                    <h5>$ 8,234</h5>
                  </div>
                </Col>
              </Row>
              <div className="mt-4">
                <Link to="#" className="btn btn-primary btn-sm">View more</Link>
              </div>
            </Col>
            <Col lg={6}>
              <div>
                <ReactApexChart options={options} series={series} type="bar" height="250" className="apex-charts" />
              </div>
            </Col>
          </Row>
        </CardBody>
      </Card>
    </React.Fragment>
  );
}

export default EarningChart;
```

### Detailed Breakdown:
- **Data and Options**: The `series` variable holds the data points, while `options` configures the appearance of the chart.
- **Earnings Summary**: This section displays textual information using headings and paragraphs.
- **Chart Rendering**: The `ReactApexChart` component is used here to render a bar chart with the data and options specified.

---

## Usage

To use the **EarningChart** component in your project, ensure all dependencies are installed and then import the component where needed:

```jsx
import EarningChart from './EarningChart';

// Use the component in your JSX
<EarningChart />
```

Ensure your project is set up with `reactstrap`, `ReactApexChart`, and `react-router-dom` for the component to function correctly.

---

### 🎨 Styling

The component uses Bootstrap classes through `reactstrap` for styling. Ensure Bootstrap CSS is linked in your project.

---

By following this documentation, you should have a comprehensive understanding of what the **EarningChart.js** component does and how to integrate it into your React project. 🎉

# 📄 Documentation for `index.js`

This file serves as the main dashboard component for a React application, integrating various sub-components to provide a comprehensive view of data related to business metrics. The dashboard is built using `React`, `Reactstrap`, and `React ApexCharts`.

## 📑 **Index**
- [Imports](#imports)
- [Constants](#constants)
- [Dashboard2 Component](#dashboard2-component)
  - [Breadcrumbs](#breadcrumbs)
  - [Orders and Revenue Cards](#orders-and-revenue-cards)
  - [Other Components](#other-components)
- [Export](#export)

## 🛠️ **Imports**

```javascript
import React from 'react';
import { Card, CardBody, Col, Row } from 'reactstrap';
import ReactApexChart from "react-apexcharts";
import Breadcrumbs from '../../components/Common/Breadcrumb';
import SalesReport from './SalesReport';
import EmailSent from './EmailSent';
import MiniWidget from './MiniWidget';
import EarningChart from './EarningChart';
import YearlySale from './YearlySale';
import ActivityComp from "./ActivityComp";
import PopularProduct from "./PopularProduct";
import SocialSource from "./SocialSource";
```

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: Components of Bootstrap 4 for React.
- **ReactApexChart**: A library for using ApexCharts in React.
- **Breadcrumbs, SalesReport, etc.**: Custom components used within the dashboard.

## 🎨 **Constants**

### Radial Bar Chart Settings

These are configurations for the radial bar charts used in the Orders and Revenue cards.

#### Orders Chart

```javascript
const series = [70];
const options = {
  plotOptions: {
    radialBar: {
      offsetY: -12,
      hollow: {
        margin: 5,
        size: '60%',
        background: 'rgba(59, 93, 231, .25)',
      },
      dataLabels: {
        name: { show: false },
        value: { show: true, fontSize: '12px', offsetY: 5 },
        style: { colors: ['#fff'] }
      }
    },
  },
  colors: ['#3b5de7'],
};
```

#### Revenue Chart

```javascript
const series1 = [81];
const options1 = {
  plotOptions: {
    radialBar: {
      offsetY: -12,
      hollow: {
        margin: 5,
        size: '60%',
        background: 'rgba(69, 203, 133, .25)',
      },
      dataLabels: {
        name: { show: false },
        value: { show: true, fontSize: '12px', offsetY: 5 },
        style: { colors: ['#fff'] }
      }
    },
  },
  colors: ['#45CB85'],
};
```

## 🖥️ **Dashboard2 Component**

The `Dashboard2` component is the main component that renders all the other components into a cohesive dashboard.

### 🧭 Breadcrumbs

```javascript
<Breadcrumbs title="Dashboard" breadcrumbItem="Dashboard 2" />
```

- **Breadcrumbs**: Displays the current location within the app.

### 📊 Orders and Revenue Cards

#### Orders

```javascript
<Col md={6}>
  <Card>
    <CardBody>
      <Row>
        <Col xs={8}>
          <div>
            <p className="text-muted fw-medium mt-1 mb-2">Orders</p>
            <h4>1,368</h4>
          </div>
        </Col>
        <div className="col-4">
          <div>
            <ReactApexChart options={options} series={series} type="radialBar" height="120" />
          </div>
        </div>
      </Row>
      <p className="mb-0"><span className="badge badge-soft-success me-2"> 0.8% <i className="mdi mdi-arrow-up"></i> </span> From previous period</p>
    </CardBody>
  </Card>
</Col>
```

- **Orders**: Displays the number of orders and a radial chart showing the percentage change.

#### Revenue

```javascript
<Col md={6}>
  <Card>
    <CardBody>
      <Row>
        <Col xs={8}>
          <div>
            <p className="text-muted fw-medium mt-1 mb-2">Revenue</p>
            <h4>$ 32,695</h4>
          </div>
        </Col>
        <Col xs={4}>
          <div>
            <ReactApexChart options={options1} series={series1} type="radialBar" height="120" />
          </div>
        </Col>
      </Row>
      <p className="mb-0"><span className="badge badge-soft-success me-2"> 0.6% <i className="mdi mdi-arrow-up"></i> </span> From previous period</p>
    </CardBody>
  </Card>
</Col>
```

- **Revenue**: Displays the total revenue and a radial chart for the percentage change.

### 📈 Other Components

- **SalesReport**: A detailed report of sales metrics.
- **EmailSent**: Metrics on emails sent.
- **MiniWidget**: Small widgets for quick insights.
- **EarningChart**: A chart showing earnings over a specified period.
- **YearlySale**: Displays yearly sales figures.
- **ActivityComp**: Component showing recent activities.
- **PopularProduct**: Displays the most popular products.
- **SocialSource**: Shows data on social media sources.

## 📤 **Export**

```javascript
export default Dashboard2;
```

- The `Dashboard2` component is exported as the default export of the module.

---

This documentation provides a detailed explanation of the `index.js` file within the context of a React dashboard application, highlighting its structure, functionality, and the components it integrates.

# 📄 EmailSent.js Documentation

## 🎯 Overview
The `EmailSent.js` file is a React component that represents a chart displaying the number of emails sent over a period of time. It provides a visual representation using different types of charts (column, area, and line) to show various series of data. This component is styled using the Reactstrap library and is part of a dashboard application.

## 📂 File Structure
```plaintext
EmailSent.js
```

## 🛠️ Component Details

### Import Statements
```javascript
import React from "react";
import { Card, CardBody, Col } from "reactstrap";
import ReactApexChart from "react-apexcharts";
import { Link } from "react-router-dom";
```
- **React**: The core library for building the user interface.
- **Reactstrap**: A library providing Bootstrap components for React, used for styling.
- **ReactApexChart**: A library for rendering charts in React using ApexCharts.
- **Link**: Part of `react-router-dom`, used for navigation within the application.

### 📊 Data Series and Chart Options
```javascript
const series = [
  { name: 'Series A', type: 'column', data: [23, 11, 53, 27, 13, 19, 22, 37, 21, 44, 22, 30] },
  { name: 'Series B', type: 'area', data: [36, 47, 33, 41, 22, 37, 43, 21, 41, 56, 27, 43] },
  { name: 'Series C', type: 'line', data: [46, 57, 43, 51, 32, 47, 53, 31, 51, 66, 37, 53] }
];

const options = {
  chart: {
    stacked: !1,
    toolbar: { show: !1 }
  },
  stroke: {
    width: [0, 2, 2],
    curve: 'smooth',
    dashArray: [0, 0, 4]
  },
  plotOptions: {
    bar: { columnWidth: '15%', endingShape: 'rounded' }
  },
  fill: {
    opacity: [0.85, 0.25, 1],
    gradient: {
      inverseColors: !1,
      shade: 'light',
      type: "vertical",
      opacityFrom: 0.85,
      opacityTo: 0.55,
      stops: [0, 100, 100, 100]
    }
  },
  xaxis: {
    categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
  },
  colors: ['#3b5de7', '#eeb902', '#5fd195'],
  markers: { size: 0 }
};
```
- **series**: Defines three different data series with column, area, and line types, representing different datasets over the months of the year.
- **options**: Configures the chart appearance, including stroke, plot options, fill settings, x-axis categories (months), and colors for each series.

### 📈 Component - Breadcrumb
```javascript
const Breadcrumb = props => {
  return (
    <React.Fragment>
      <Col lg={6}>
        <Card>
          <CardBody>
            <div className="float-end">
              <ul className="nav nav-pills">
                <li className="nav-item">
                  <Link className="nav-link" to="#">Week</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link" to="#">Month</Link>
                </li>
                <li className="nav-item">
                  <Link className="nav-link active" to="#">Year</Link>
                </li>
              </ul>
            </div>
            <h4 className="card-title mb-4">Email Sent</h4>
            <ReactApexChart options={options} series={series} type="line" height="275" className="apex-charts" />
          </CardBody>
        </Card>
      </Col>
    </React.Fragment>
  );
};
```
- **Col**: A layout component from Reactstrap, designates the width of the component on large screens.
- **Card**: A Bootstrap card component used to encapsulate the content.
- **CardBody**: The body section of the Card where the chart and navigation links are rendered.
- **ReactApexChart**: Renders the chart with the provided `options` and `series`.
- **Navigation Links**: `Week`, `Month`, `Year` links allow users to filter the data by time period, although only the `Year` link is active.

### 🌟 Features
- **Responsive Design**: Utilizes Bootstrap through Reactstrap for responsive layout.
- **Interactive Chart**: Powered by ApexCharts, it provides a smooth and interactive data visualization experience.
- **Navigation Links**: Facilitates easy transition between different time periods (though functionality needs to be implemented).

## 🚀 Usage
To use the `EmailSent` component, import it into your dashboard or any other React component and render it as a child component.

```javascript
import EmailSent from './EmailSent';

function Dashboard() {
  return (
    <div>
      <EmailSent />
    </div>
  );
}
```

## 📚 Conclusion
The `EmailSent.js` component is a well-structured and visually appealing component that visualizes email statistics over time. It combines React, Reactstrap, and ApexCharts to create an effective data representation tool for dashboards.

# 📄 Documentation: PopularProduct.js

The `PopularProduct.js` file is a React component designed to display a list of popular products and their sales statistics. Below is a detailed breakdown of the component's structure and functionality.

## 📋 Table of Contents
1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Code Explanation](#code-explanation)
4. [UI Elements](#ui-elements)
5. [Usage](#usage)

## Overview

The **PopularProduct** component is a simple, visually appealing card that displays the most popular products with their respective sales numbers. It uses Reactstrap for styling and layout, ensuring a responsive and consistent design.

## Component Structure

- **Dependencies**:
  - `React`: To utilize React's component structure.
  - `reactstrap`: Provides pre-styled components such as `Card`, `CardBody`, `CardTitle`, `Row`, and `Col` for easier layout management.

- **Main Functional Component**: 
  - `PopularProduct`: The primary component responsible for rendering the product information.

## Code Explanation

```javascript
import React from 'react';
import { Card, CardBody, CardTitle, Row, Col } from 'reactstrap';

function PopularProduct() {
  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <CardTitle className="h4 mb-4">Popular Products</CardTitle>
          <div className="d-flex">
            <h5 className="me-2"><i className="mdi mdi-cellphone-android text-primary me-2"></i> Mobile -</h5>
            <p className="mb-0">62 Product sold</p>
          </div>
          <div className="text-center">
            <Row>
              <Col sm={6}>
                <div className="pt-4">
                  <div className="avatar-sm mx-auto font-size-16">
                    <span className="avatar-title bg-soft-primary text-primary rounded-circle">
                      <i className="mdi mdi-monitor"></i>
                    </span>
                  </div>
                  <div className="mt-3">
                    <h5 className="mb-1">Desktop</h5>
                    <p className="text-truncate">45 Product sold</p>
                  </div>
                </div>
              </Col>
              <Col sm={6}>
                <div className="pt-4">
                  <div className="avatar-sm mx-auto font-size-16">
                    <span className="avatar-title bg-soft-primary text-primary rounded-circle">
                      <i className="mdi mdi-laptop"></i>
                    </span>
                  </div>
                  <div className="mt-3">
                    <h5 className="mb-1">Laptop</h5>
                    <p className="text-truncate">57 Product sold</p>
                  </div>
                </div>
              </Col>
              <Col sm={6}>
                <div className="pt-4">
                  <div className="avatar-sm mx-auto font-size-16">
                    <span className="avatar-title bg-soft-primary text-primary rounded-circle">
                      <i className="mdi mdi-tablet-android"></i>
                    </span>
                  </div>
                  <div className="mt-3">
                    <h5 className="mb-1">Tablet</h5>
                    <p className="text-truncate">31 Product sold</p>
                  </div>
                </div>
              </Col>
              <Col sm={6}>
                <div className="pt-4">
                  <div className="avatar-sm mx-auto font-size-16">
                    <span className="avatar-title bg-soft-primary text-primary rounded-circle">
                      <i className="mdi mdi-cellphone-android"></i>
                    </span>
                  </div>
                  <div className="mt-3">
                    <h5 className="mb-1">Mobile</h5>
                    <p className="text-truncate">62 Product sold</p>
                  </div>
                </div>
              </Col>
            </Row>
          </div>
        </CardBody>
      </Card>
    </React.Fragment>
  );
}

export default PopularProduct;
```

## UI Elements

- **Card**: The main container for the component, giving it a bordered and shadowed appearance.
- **CardTitle**: Displays the title "Popular Products".
- **Product Items**: Each product category (Mobile, Desktop, Laptop, Tablet) is displayed with an icon, name, and sold count.
- **Icons**: Uses Material Design Icons (mdi) for visual representation of product categories.

## Usage

To use the **PopularProduct** component, ensure that you have `React` and `reactstrap` installed in your project. Import the component wherever you need to display the popular products section.

```jsx
import PopularProduct from './PopularProduct';

// Usage in a parent component
function App() {
  return (
    <div className="App">
      <PopularProduct />
    </div>
  );
}
```

The component is designed to be easily integrable into any dashboard or analytics page where visual representation of product sales is required. The layout is responsive and adjusts according to screen size, making it optimal for use in various applications.

Feel free to customize the icons, product names, and sales numbers to fit your application's needs. 🎉

# MiniWidget.js Documentation 📄✨

Welcome to the **MiniWidget.js** documentation! This file is a React component that uses **Reactstrap** to create a set of small widget cards displaying various statistics, such as "Online", "Offline", and "Marketing" metrics. Below is a detailed breakdown of what the component does and how it is structured.

## Table of Contents
- [Introduction](#introduction)
- [Component Structure](#component-structure)
- [Properties and Methods](#properties-and-methods)
- [Usage Example](#usage-example)
- [Conclusion](#conclusion)

## Introduction

The **MiniWidget** component is designed to create a series of card-based widgets that display numerical data alongside a progress bar, making it ideal for dashboard interfaces. Each widget displays a specific category with its respective count and percentage change.

## Component Structure

The component is structured using **React** and **Reactstrap** components. Each widget is encapsulated within a `<Card>` component, which includes a `<CardBody>` for content organization.

### Import Statements
Here's the list of imports used in the component:
```jsx
import React from 'react';
import { Card, CardBody, Row, Progress } from 'reactstrap';
```

### The MiniWidget Component

The core component is a functional component named `MiniWidget`:

```jsx
const MiniWidget = () => {
  return (
    <React.Fragment>
      {/* Online Widget */}
      <Card>
        <CardBody>
          <Row className="align-items-center">
            <div className="col-8">
              <p className="mb-2">Online</p>
              <h4 className="mb-0">3,524</h4>
            </div>
            <div className="col-4">
              <div className="text-end">
                <div> 2.06 % <i className="mdi mdi-arrow-up text-success ms-1"></i> </div>
                <div className="mt-3">
                  <Progress value="62" color="primary" className="bg-transparent progress-sm" size="sm" />
                </div>
              </div>
            </div>
          </Row>
        </CardBody>
      </Card>
      {/* Additional Widgets... */}
    </React.Fragment>
  );
}
```

## Properties and Methods

### Properties

- **Card**: Used to create a card-like container.
- **CardBody**: Contains the content of the card.
- **Row**: Used for layout purposes, aligning the text and progress bar.
- **Progress**: Displays a progress bar reflecting the percentage change.

### Methods

The component does not include additional methods or state management as it is a simple functional component displaying static data.

## Usage Example

To include the **MiniWidget** component in your project, simply import it and use it as a JSX element:

```jsx
import MiniWidget from './MiniWidget';

function App() {
  return (
    <div>
      <MiniWidget />
    </div>
  );
}
```

## Conclusion

The **MiniWidget.js** component provides a straightforward way to create visually appealing, informative widgets for any React-based dashboard. Its use of **Reactstrap** ensures a responsive and consistent design, while the minimalist structure makes it easy to customize and extend.

Feel free to modify the data and styling to match your specific needs. Happy coding! 🚀🎨

# SalesReport.js Documentation 📊

`SalesReport.js` is a **React component** that provides a visual representation of sales data over a specific time period using a line chart. This component utilizes the `ReactApexChart` library to render the chart and is styled using `reactstrap`.

## Table of Contents
1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Chart Configuration](#chart-configuration)
4. [Usage](#usage)
5. [Dependencies](#dependencies)

## Overview
The **SalesReport** component displays a sales summary for a defined period, highlighting the total sales amount and the percentage change from a previous period. The data is presented through a line chart, offering a quick visual insight into sales trends.

## Component Structure
The component is structured as follows:

- **Card**: The main container for the sales report content.
  - **CardBody**: Holds the chart and sales data.
  - **Chart Title**: Displays "Sales Report".
  - **Sales Data**: Shows the sales period and total earnings.
  - **Trend Indicator**: Highlights the percentage change from the previous period.
  - **ReactApexChart**: Renders a line chart showing sales fluctuations.

Here is the component's JSX structure:

```jsx
<React.Fragment>
  <Card>
    <CardBody>
      <h4 className="card-title mb-4">Sales Report</h4>
      <Row>
        <Col sm={7}>
          <div>
            <p className="mb-2">01 Jan - 31 Jan, 2020</p>
            <h4>$ 27, 253</h4>
            <p className="mt-4 mb-0">
              <span className="badge badge-soft-success me-2">
                0.6% <i className="mdi mdi-arrow-up"></i>
              </span>
              From previous period
            </p>
          </div>
        </Col>
        <Col sm={4}>
          <div className="mt-4 mt-sm-0">
            <ReactApexChart
              options={options}
              series={series}
              type="line"
              height="100"
              className="apex-charts"
            />
          </div>
        </Col>
      </Row>
    </CardBody>
  </Card>
</React.Fragment>
```

## Chart Configuration
The chart is configured using the `options` and `series` objects:

### Series
- **Series A**: Represents the sales data over the given period.
  ```javascript
  const series = [{ name: "Series A", data: [24, 66, 42, 88, 62, 24, 45, 12, 36, 10] }];
  ```

### Options
- **Chart**: Configured as a sparkline chart with no toolbar.
- **Data Labels**: Disabled for a cleaner look.
- **Stroke**: Smooth curve with a width of 3 for visual appeal.
- **Colors**: Set to `'#3b5de7'` for line color.

```javascript
const options = {
  chart: {
    sparkline: {
      enabled: !0
    },
    toolbar: {
      show: !1
    },
  },
  dataLabels: {
    enabled: !1
  },
  stroke: {
    curve: 'smooth',
    width: 3
  },
  colors: ['#3b5de7'],
};
```

## Usage
To use the **SalesReport** component, simply import it into your React application and include it within your JSX:

```javascript
import SalesReport from './SalesReport';

// In your component's render method or function
<SalesReport />
```

## Dependencies
This component relies on the following libraries:

- **React**: For building the component.
- **reactstrap**: For styling and layout components.
- **ReactApexChart**: For rendering the charts.

---

This detailed documentation should provide a comprehensive understanding of the **SalesReport.js** component's functionality and usage. If you have any questions or need further clarification, feel free to ask! 😊

# Documentation: `SocialSource.js`

Welcome to the documentation for the `SocialSource.js` component. This React component is designed to display a detailed breakdown of social media sources and their contributions to total revenue. Below, you'll find a comprehensive explanation of what the component does, its purpose, and the structure of its implementation. 🎉

## Table of Contents
- [Introduction](#introduction)
- [Component Structure](#component-structure)
- [Key Features](#key-features)
- [Code Breakdown](#code-breakdown)
- [Usage](#usage)
- [Conclusion](#conclusion)

## Introduction

The `SocialSource` component is a **React functional component** that provides a visual representation of revenue generated from various social media platforms. It uses the `reactstrap` library for UI elements, ensuring a responsive and clean design. This component is particularly useful for dashboards and analytics pages where tracking the performance of social media sources is crucial. 📊

## Component Structure

This component is structured using several HTML and Reactstrap components:
- **Card**: A container for organizing the content.
- **CardBody**: Holds the main content of the card.
- **CardTitle**: Displays the title of the card.
- **Input**: A dropdown for selecting the month.
- **Various divs and spans**: For layout and styling purposes.

## Key Features

- **Dropdown Menu**: Allows users to select a specific month.
- **Dynamic Data Display**: Shows the total revenue from social sources.
- **Platform Breakdown**: Lists revenue contributions from Facebook, Twitter, and Instagram.
- **Percentage Change Indicators**: Displays percentage change with icons to indicate increase. 📈

## Code Breakdown

```javascript
import React from 'react';
import { Card, CardBody, CardTitle, Input } from 'reactstrap';

function SocialSource() {
    return (
        <React.Fragment>
            <Card>
                <CardBody>
                    <div className="float-end">
                        <div className="input-group input-group">
                            <Input type="select" className="form-select form-select-sm">
                                <option>Jan</option>
                                <option value="1">Dec</option>
                                <option value="2">Nov</option>
                                <option value="3">Oct</option>
                            </Input>
                            <label className="input-group-text">Month</label>
                        </div>
                    </div>
                    <CardTitle className="h4 mb-4">Social source</CardTitle>
                    <div className="align-items-start d-flex">
                        <div className="flex-1">
                            <p className="mb-2">Total Social source</p>
                            <h4>$ 8,974</h4>
                            <p className="mb-0">
                                <span className="badge badge-soft-success me-2"> 0.6% 
                                    <i className="mdi mdi-arrow-up"></i>
                                </span> From previous period
                            </p>
                        </div>
                    </div>
                    <div className="mt-3 social-source">
                        <div className="d-flex align-items-center social-source-list">
                            <div className="avatar-xs me-4">
                                <span className="avatar-title rounded-circle">
                                    <i className="mdi mdi-facebook"></i>
                                </span>
                            </div>
                            <div className="flex-1">
                                <p className="mb-1">Facebook</p>
                                <h5 className="mb-0">$ 2,352</h5>
                            </div>
                            <div className="ms-auto"> 2.06 % 
                                <i className="mdi mdi-arrow-up text-success ms-1"></i>
                            </div>
                        </div>
                        <div className="d-flex align-items-center social-source-list">
                            <div className="avatar-xs me-4">
                                <span className="avatar-title rounded-circle bg-info">
                                    <i className="mdi mdi-twitter"></i>
                                </span>
                            </div>
                            <div className="flex-1">
                                <p className="mb-1">Twitter</p>
                                <h5 className="mb-0">$ 1,925</h5>
                            </div>
                            <div className="ms-auto"> 1.28 % 
                                <i className="mdi mdi-arrow-up text-success ms-1"></i>
                            </div>
                        </div>
                        <div className="d-flex align-items-center social-source-list">
                            <div className="avatar-xs me-4">
                                <span className="avatar-title rounded-circle bg-pink">
                                    <i className="mdi mdi-instagram"></i>
                                </span>
                            </div>
                            <div className="flex-1">
                                <p className="mb-1">Instagram</p>
                                <h5 className="mb-0">$ 1,846</h5>
                            </div>
                            <div className="ms-auto"> 1.04 % 
                                <i className="mdi mdi-arrow-up text-success ms-1"></i>
                            </div>
                        </div>
                    </div>
                </CardBody>
            </Card>
        </React.Fragment>
    );
}

export default SocialSource;
```

### Explanation

- **Dropdown**: The `<Input>` component is used to allow selection of the month for which data is displayed.
- **Total Revenue**: Displays the total revenue from all social sources.
- **Platform Specific Revenue**: For each platform (Facebook, Twitter, Instagram), it shows the revenue and percentage increase.
- **Icons**: Uses `mdi` icons to visually represent platforms.

## Usage

To use this component, simply import it into your React application and include it in your component tree. It requires `reactstrap` and `mdi` icons for full functionality.

```javascript
import SocialSource from './SocialSource';
...
<SocialSource />
```

## Conclusion

The `SocialSource` component is a powerful tool for displaying the impact of various social media platforms on revenue. By leveraging React and Reactstrap, it provides a responsive and interactive user experience. Use it in dashboards or analytics pages to provide insights into social media performance. 📈✨

# YearlySale.js Documentation 📊

The `YearlySale.js` file is a React component that provides visual insights into yearly sales data using a radar chart. This component leverages the `reactstrap` and `ReactApexChart` libraries to create a visually appealing and informative chart.

## Table of Contents
- [Overview](#overview)
- [Component Breakdown](#component-breakdown)
  - [Imports](#imports)
  - [Data Series](#data-series)
  - [Chart Options](#chart-options)
  - [YearlySale Component](#yearlysale-component)
- [Usage](#usage)
- [Conclusion](#conclusion)

## Overview

The `YearlySale` component is designed to render a radar chart that displays sales data over a series of years. This component is useful for visualizing trends and comparing performances across different years.

## Component Breakdown

### Imports

```javascript
import React from 'react';
import { Card, CardBody, CardTitle } from 'reactstrap';
import ReactApexChart from "react-apexcharts";
```

The component imports essential React libraries and components:
- **React**: The core library for building user interfaces.
- **reactstrap**: Provides Bootstrap-based React components for building responsive UI elements.
- **ReactApexChart**: A charting library that enables rendering of various chart types in React applications.

### Data Series

```javascript
const series= [
  { name: 'Series 1', data: [80, 50, 30, 40, 100, 20] },
  { name: 'Series 2', data: [20, 30, 40, 80, 20, 80] },
  { name: 'Series 3', data: [44, 76, 78, 13, 43, 10] }
];
```

The `series` array contains multiple datasets, each representing sales data for a different series. These datasets will be plotted on the radar chart, allowing for comparative analysis.

### Chart Options

```javascript
const options= {
  chart: {
    dropShadow: {
      enabled: true,
      blur: 1,
      left: 1,
      top: 1
    },
    toolbar: { show: !1 },
  },
  stroke: { width: 0 },
  fill: { opacity: 0.4 },
  markers: { size: 0 },
  colors: ['#3b5de7', '#5fd195', '#eeb902'],
  xaxis: {
    categories: ['2014', '2015', '2016', '2017', '2018', '2019']
  }
};
```

The `options` object configures the appearance and behavior of the radar chart:
- **chart.dropShadow**: Adds a subtle shadow to the chart, enhancing its visual depth.
- **stroke & fill**: Customize the line stroke and fill opacity of the chart.
- **colors**: Specifies the colors for each series, making it easy to differentiate between them.
- **xaxis.categories**: Labels for each axis, representing different years in this context.

### YearlySale Component

```javascript
const YearlySale = () => {
  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <CardTitle className="h4 mb-4">Yearly sales</CardTitle>
          <ReactApexChart options={options} series={series} type="radar" height="250" className="apex-charts" />
        </CardBody>
      </Card>
    </React.Fragment>
  );
}

export default YearlySale;
```

The `YearlySale` component is a functional React component that renders a card containing a radar chart. The chart uses the `series` and `options` to plot sales data, providing a clear and interactive visualization.

## Usage

To integrate the `YearlySale` component into an application, you would typically import it and include it within a parent component or page layout. Ensure that `reactstrap` and `ReactApexChart` are installed in your project.

```javascript
import YearlySale from './YearlySale';

function App() {
  return (
    <div className="App">
      <YearlySale />
    </div>
  );
}
```

## Conclusion

The `YearlySale.js` component is a powerful tool for visualizing yearly sales data using a radar chart. Its design leverages modern React practices and integrates seamlessly with popular libraries for enhanced aesthetics and functionality. This component can be a valuable addition to any dashboard or reporting page, offering users an intuitive way to explore and analyze historical data trends.