# Documentation for ToastUIChart.js 📊

## Table of Contents
1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Main Component: `ToastUIChart`](#main-component-toastuichart)
4. [Chart Components](#chart-components)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

---

## Introduction

**ToastUIChart.js** is a React component that renders a variety of charts using the Toast UI Chart library. This library provides a comprehensive suite of chart types which are rendered in a responsive and visually appealing manner. The component organizes its charts within a grid layout using Bootstrap's grid system.

## Imports

The **ToastUIChart.js** file begins by importing necessary React components and utility functions, as well as specific chart components that it will render:

```javascript
import React from "react";
import { Row, Col, Card, CardBody, CardTitle, Container } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";

// Import all charts
import BarChartToast from "../AllCharts/toastui/BarChartToast";
import ColumnChartToast from "../AllCharts/toastui/ColumnChartToast";
import LineChartToast from "../AllCharts/toastui/LineChartToast";
import AreaChartToast from "../AllCharts/toastui/AreaChartToast";
import BubbleChartToast from "../AllCharts/toastui/BubbleChartToast";
import ScatterChartToast from "../AllCharts/toastui/ScatterChartToast";
import PieChartToast from "../AllCharts/toastui/PieChartToast";
import DonutChartToast from "../AllCharts/toastui/DonutChartToast";
import HeatmapChartToast from "../AllCharts/toastui/HeatmapChartToast";
import TreeMapChart from "../AllCharts/toastui/TreeMapChart";
import MapChart from "../AllCharts/toastui/TreeMapChart";
import BoxPlotChart from "../AllCharts/toastui/BoxPlotChart";
import BulletChart from "../AllCharts/toastui/BulletChart";
import RadialChart from "../AllCharts/toastui/RadialChart";
```

## Main Component: `ToastUIChart`

The **ToastUIChart** component is a functional React component that uses Reactstrap for layout. It begins by determining the `chartWidth` based on the current window width, ensuring responsiveness:

```javascript
const ToastUIChart = () => {
    const chartWidth = window.innerWidth > 991 ? parseInt((window.innerWidth - 420) / 2) : parseInt(window.innerWidth - 100);
    return (
        <React.Fragment>
            <div className="page-content">
                <Breadcrumbs title="Charts" breadcrumbItem="Toast Ui charts" />
                <Row>
                    {/* Various Chart Components */}
                </Row>
            </div>
        </React.Fragment>
    );
};
```

### Chart Components

Each chart is wrapped within a `<Card>` component for styling and structure. Here's an example of how one of the chart components is rendered:

```javascript
<Col lg="6">
    <Card>
        <CardBody>
            <CardTitle className="mb-4">Bar Chart</CardTitle>
            <BarChartToast chartWidth={chartWidth} />
        </CardBody>
    </Card>
</Col>
```

### List of Chart Components

- **Bar Chart**: `BarChartToast`
- **Column Chart**: `ColumnChartToast`
- **Line Chart**: `LineChartToast`
- **Area Chart**: `AreaChartToast`
- **Bubble Chart**: `BubbleChartToast`
- **Scatter Chart**: `ScatterChartToast`
- **Pie Chart**: `PieChartToast`
- **Donut Chart**: `DonutChartToast`
- **Heatmap Chart**: `HeatmapChartToast`
- **Treemap Chart**: `TreeMapChart`
- **Map Chart**: `MapChart`
- **Boxplot Chart**: `BoxPlotChart`
- **Bullet Chart**: `BulletChart`
- **Radial Chart**: `RadialChart`

## Usage

To integrate this component in a React application, make sure that all the necessary chart components are correctly implemented and imported from their respective paths. The component is designed to be part of a larger dashboard or analytics page due to its use of Reactstrap's grid and card components.

## Conclusion

The **ToastUIChart.js** component is a versatile and comprehensive charting solution for React applications. By employing various chart types and ensuring responsiveness, it is well-suited for dynamic data visualization needs within web applications. It leverages the powerful Toast UI Chart library to provide interactive and attractive charts.

# SparklineChart.js Documentation 📈

Welcome to the detailed documentation for the **SparklineChart.js** file. This file is a React component designed to render various Sparkline charts using the `react-sparklines` library. Below, you'll find a comprehensive guide to understanding and utilizing this component in your projects. 🌟

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Import Statements](#import-statements)
3. [Component Structure](#component-structure)
4. [Chart Types](#chart-types)
5. [Customization Options](#customization-options)
6. [Usage](#usage)
7. [Conclusion](#conclusion)

---

## Introduction 📝

The `SparklineChart.js` component leverages the `react-sparklines` library to create compact and beautiful charts that are ideal for data-rich dashboards. These charts can be used to provide insights at a glance and are highly customizable to fit your needs.

## Import Statements 📥

```javascript
import React from "react";
import { Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import {
    Sparklines,
    SparklinesLine,
    SparklinesBars,
    SparklinesSpots,
    SparklinesReferenceLine,
    SparklinesCurve,
} from "react-sparklines";
```

- **React and Reactstrap**: Essential for creating the component structure and styling.
- **Breadcrumbs**: Provides navigational breadcrumbs.
- **Sparklines Components**: Various components from `react-sparklines` to render different types of charts.

## Component Structure 🏗️

The `SparklineChart` component is structured using React functional component with JSX. It uses Bootstrap's grid system via Reactstrap to layout the charts.

### JSX Structure

- **Breadcrumbs**: Displays the navigation path.
- **Rows and Columns**: Used to organize multiple charts neatly.
- **Cards**: Each chart is encapsulated within a card for a clean UI presentation.

## Chart Types 📊

The component renders several types of Sparkline charts:

1. **Spots Chart**: Highlights specific data points with spots.
2. **Bar Chart**: Displays data using bars for comparison.
3. **Line Chart**: A simple line chart for trends over time.
4. **Composite Bar Chart**: Combines bars with a line for more context.
5. **Reference Line Charts**: Adds a reference line for average or mean values.
6. **Real World Chart**: A more dynamic chart representing real-world data.
7. **Normal Band**: Shows a normal band with a mean reference line.

Each type is placed in a separate card, making it easy to display them in a grid format.

## Customization Options 🎨

The `Sparklines` component provides several customization options:

- **Data**: Each chart has its own data set, which can be customized.
- **Styles**: Customize stroke width, colors, fill, and more.
- **Dimensions**: Adjust height and width of the charts.
- **Reference Lines**: Easily add reference lines to highlight important thresholds.

### Example Customization

```javascript
<SparklinesLine
    style={{
        strokeWidth: 1,
        stroke: "#336aff",
        fill: "none",
    }}
/>
```

## Usage 🚀

To use the `SparklineChart` component, simply import it into your React application and include it within your render method:

```javascript
import SparklineChart from './path-to/SparklineChart';

function App() {
    return (
        <div>
            <SparklineChart />
        </div>
    );
}
```

This will render a set of Sparkline charts organized in cards, ready to be integrated into your dashboard.

## Conclusion 🎉

The **SparklineChart.js** component is a powerful and flexible way to add compact data visualizations to your React applications. With easy customization and a variety of chart types, it can fit a wide range of use cases.

Feel free to adjust data, styles, and layout to suit your application needs and provide valuable insights to your users at a glance. Happy charting! 📊✨

---

# EChart.js Documentation 📊

Welcome to the documentation for the **EChart.js** file, a React component that renders a variety of interactive charts using the ECharts library. This component is part of a larger application and is designed to provide a comprehensive dashboard of data visualizations. Below, you'll find detailed information about the structure, purpose, and functionality of this component.

## Table of Contents
1. [Overview](#overview)
2. [Imports](#imports)
3. [Component Structure](#component-structure)
4. [Charts Included](#charts-included)
5. [Usage](#usage)
6. [Customization](#customization)
7. [Conclusion](#conclusion)

## Overview

The **EChart.js** component is responsible for rendering a variety of chart types using ECharts, a powerful charting and visualization library. It is structured to display eight different chart types within a responsive card layout, allowing users to gain insights at a glance.

## Imports

This component makes use of several imports to bring in necessary React components, styles, and specific chart types:

```javascript
import React from "react";
import { Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import Gauge from "../AllCharts/echart/gaugechart";
import Line from "../AllCharts/echart/linechart";
import LineBar from "../AllCharts/echart/linebarchart";
import Doughnut from "../AllCharts/echart/doughnutchart";
import Pie from "../AllCharts/echart/piechart";
import Scatter from "../AllCharts/echart/scatterchart";
import Bubble from "../AllCharts/echart/bubblechart";
import Candlestick from "../AllCharts/echart/candlestickchart";
```

### Key Imports
- **React**: Core library for building the component.
- **Reactstrap**: Provides responsive grid layout using `Row` and `Col`, along with styled card components.
- **Breadcrumbs**: Renders navigational breadcrumbs for better UX.
- **ECharts Components**: Specific chart components imported from a centralized chart directory.

## Component Structure

The component is structured using a functional React component with JSX to define the layout and content:

```javascript
const EChart = () => {
    return (
        <React.Fragment>
            <div className="page-content">
                <Breadcrumbs title="Charts" breadcrumbItem="E-Charts" />
                {/* Chart Rows */}
                ...
            </div>
        </React.Fragment>
    );
}
```

### Layout
- **Page Content**: The entire content is wrapped within a `div` with the class "page-content".
- **Breadcrumbs**: Provides navigation context at the top of the page.
- **Rows and Columns**: Utilizes `Row` and `Col` from Reactstrap to create a responsive grid layout for each chart type.

## Charts Included

The component includes the following chart types, each rendered within a card:

1. **Line Chart** 📈
   - Displays data as a continuous line.
   
2. **Mix Line-Bar Chart** 📊
   - Combines line and bar charts for comparative analysis.

3. **Doughnut Chart** 🍩
   - A circular chart with a hole in the center.

4. **Pie Chart** 🥧
   - Classic pie chart to show parts of a whole.

5. **Scatter Chart** 🌌
   - Plots points on a graph to show distribution.

6. **Bubble Chart** 🟢
   - Similar to scatter but with varying bubble sizes.

7. **Candlestick Chart** 📉
   - Used primarily for stock market analysis.

8. **Gauge Chart** ⏲️
   - Displays numerical values with a gauge-like appearance.

## Usage

To use the **EChart** component, it should be included in a React application where data visualization is required. It can be rendered directly in a page component as follows:

```javascript
import EChart from './path/to/EChart';

function App() {
    return (
        <div className="App">
            <EChart />
        </div>
    );
}

export default App;
```

## Customization

Customization of the charts is possible by modifying the individual chart components imported into **EChart.js**. Each chart component can be tailored with specific data, color schemes, and configurations to meet the needs of the application.

## Conclusion

The **EChart.js** component serves as a robust and versatile tool for visualizing datasets using a variety of chart types. By leveraging the capabilities of ECharts and Reactstrap, it provides an interactive and responsive user experience. This documentation should help you understand the component's structure, purpose, and how to integrate it into your project. 🌟

Feel free to explore and modify the component to suit your specific data visualization needs!

# 📊 `charts-knob.js` Documentation

Welcome to the documentation for the `charts-knob.js` file! This file is a React component that implements various examples of jQuery Knob charts. These charts are interactive, touchable dials that can be used to represent data in a visually appealing way.

---

## Table of Contents

1. [Overview](#overview)
2. [Key Features](#key-features)
3. [Code Structure](#code-structure)
4. [Usage](#usage)
5. [Examples](#examples)
6. [State Management](#state-management)
7. [Dependencies](#dependencies)
8. [Conclusion](#conclusion)

---

## Overview

The `charts-knob.js` component leverages the jQuery Knob library to create customizable and interactive knob-style charts. These charts are often used in dashboards to display data that can be manipulated by the user, providing real-time feedback and adjustments.

---

## Key Features

- **Interactive Knobs**: Users can interact with the knobs to change values.
- **Customizable Appearance**: Change colors, sizes, and other properties easily.
- **Multiple Configurations**: Support for various configurations like angle offset, read-only mode, and cursor mode.
- **Responsive Design**: Utilizes Reactstrap for grid layout, ensuring responsiveness.

---

## Code Structure

```javascript
import React, { useState } from "react";
import { Row, Col, Card, CardBody } from "reactstrap";
import Knob from "../AllCharts/knob/knob"; // Import Knob component
import Breadcrumbs from "../../components/Common/Breadcrumb"; // Import Breadcrumbs component

const ChartsKnob = () => {
  // State variables for knob values
  const [value1, setvalue] = useState(35);
  const [value_cur, setvalue_cur] = useState(29);
  const [value_prev, setvalue_prev] = useState(44);
  const [angle, setangle] = useState(24);
  const [steps, setsteps] = useState(-11000);
  const [angleArc, setangleArc] = useState(29);
  const [ang_offset_arc, setang_offset_arc] = useState(75);
  const [readonly, setreadonly] = useState(80);

  // Event handler functions
  const handleChange = newValue => { setvalue(newValue); };
  const handleChangecursor = newValue => { setvalue_cur(newValue); };
  const handleChangeprev = newValue => { setvalue_prev(newValue); };

  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Charts" breadcrumbItem="Jquery Knob charts" />
        <Row>
          <Col xs="12">
            <Card>
              <CardBody>
                <h4 className="card-title">Examples</h4>
                <p className="card-title-desc">Nice, downward compatible, touchable, jQuery dial</p>
                {/* Knob components with various configurations */}
              </CardBody>
            </Card>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
};

export default ChartsKnob;
```

---

## Usage

To use this component within your React application, simply import it and include it in your JSX:

```javascript
import ChartsKnob from './path/to/charts-knob';

const App = () => {
  return (
    <div>
      <ChartsKnob />
    </div>
  );
};
```

---

## Examples

### 📈 Knob Examples

1. **Disable Display Input**: A knob with the display input disabled.
2. **Cursor Mode**: The knob cursor changes position.
3. **Display Previous Value**: Shows the previously set value.
4. **Angle Offset**: Adjusts the angle offset and arc.
5. **5-Digit Values**: Supports large ranges with step intervals.
6. **Read-Only**: A non-interactive knob for display purposes.

---

## State Management

The component uses React's `useState` hook to manage the state of various knob attributes:

- `value1`, `value_cur`, `value_prev`: Store current values.
- `angle`, `steps`, `angleArc`, `ang_offset_arc`, `readonly`: Manage additional knob configurations.

Event handlers such as `handleChange` allow for updating these states when knob values change.

---

## Dependencies

- **React**: JavaScript library for building user interfaces.
- **Reactstrap**: Provides Bootstrap components as React components.
- **jQuery Knob**: A jQuery plugin for creating knob inputs.

Ensure you have these dependencies installed to successfully run the `charts-knob.js` component.

---

## Conclusion

The `charts-knob.js` file is an excellent resource for creating interactive and visually appealing knob-style charts within a React application. With customizable options and responsive design, it can significantly enhance the user experience of any data-driven application.

Feel free to explore and modify the knobs to suit your needs! 🎨

---

✨ **Happy Charting!** 📈✨

# 📊 ChartjsChart.js Documentation

## 📄 Overview

The `ChartjsChart.js` file is a React component designed to render various types of charts using the **Chart.js** library. It utilizes the `reactstrap` library for styling and layout, providing a clean and responsive design for the charts. This component is a part of a larger application, which likely includes a dashboard or data visualization interface.

## 🗂️ Table of Contents

1. [File Structure](#file-structure)
2. [Component Details](#component-details)
3. [Charts Rendered](#charts-rendered)
4. [Dependencies](#dependencies)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

## 📁 File Structure

```plaintext
ChartjsChart.js
```

## 🛠️ Component Details

### Function: `ChartjsChart`

- **Type**: Functional Component
- **Purpose**: Renders a variety of charts using Chart.js in a structured and styled manner.
- **Structure**: 
  - The component is wrapped in a `<React.Fragment>` for grouping purposes without adding extra nodes to the DOM.
  - The main content is wrapped in a `<div>` with the class `page-content`, indicating it is likely part of a larger page or dashboard.

### Return Structure

- **Breadcrumbs**: Utilizes a `Breadcrumbs` component to display navigational links titled "Charts" with a breadcrumb item "Chartjs charts".
- **Rows and Columns**: Uses `reactstrap`'s `<Row>` and `<Col>` components to organize the charts into a grid layout.
- **Cards**: Each chart is enclosed within a `<Card>` component for separation and styling, with a `<CardBody>` and `<CardTitle>`.

## 📊 Charts Rendered

The component renders the following charts:

| Chart Type   | Component Used       | Description                        |
|--------------|----------------------|------------------------------------|
| Line Chart   | `<LineChart />`      | Displays data in a line graph.     |
| Bar Chart    | `<BarChart />`       | Displays data in a bar graph.      |
| Pie Chart    | `<PieChart />`       | Displays data in a pie graph.      |
| Donut Chart  | `<DountChart />`     | Displays data in a donut graph.    |
| Polar Chart  | `<PolarChart />`     | Displays data in a polar graph.    |
| Radar Chart  | `<RadarChart />`     | Displays data in a radar graph.    |

### Chart Details

- Each chart is accompanied by basic statistics displayed above the chart (Activated, Pending, Deactivated).
- The statistics are structured using `<Row>` and `<div>` elements with specific classes for styling.

## 📦 Dependencies

### External Libraries

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: A library that provides Bootstrap 4 components as React components.
- **Chart.js**: A simple yet flexible JavaScript charting library.

### Components

- **Breadcrumbs**: Used for displaying navigation links.
- **Various Chart Components**: Imported from `"../AllCharts/chartjs/"` directory, each representing a different type of chart.

## 📝 Usage

To use this component, ensure that you have the necessary dependencies installed (`React`, `reactstrap`, `Chart.js`) and include it within your application where you want to display the charts.

Example:

```jsx
import ChartjsChart from './ChartjsChart';

function App() {
  return (
    <div className="App">
      <ChartjsChart />
    </div>
  );
}

export default App;
```

## 🏁 Conclusion

The `ChartjsChart.js` component is a versatile and well-structured component for displaying various chart types using the Chart.js library. It leverages `reactstrap` for responsive design, ensuring that the charts are neatly organized and visually appealing within a dashboard or data visualization application.

# 📈 Apexcharts.js Documentation

Welcome to the documentation for the **Apexcharts.js** file. This file is a React component that serves as a dashboard for displaying various types of charts using the ApexCharts library. It utilizes Reactstrap for UI components and is structured to provide a user-friendly interface for data visualization.

## 🌟 Index

1. [Overview](#overview)
2. [File Imports](#file-imports)
3. [Component Structure](#component-structure)
4. [Chart Types](#chart-types)
5. [UI Components](#ui-components)
6. [Conclusion](#conclusion)

---

## Overview

The **Apexcharts.js** file is designed to render a variety of chart types using React and the ApexCharts library. It leverages several pre-defined chart components and arranges them into a cohesive layout. This provides users with a powerful tool for visualizing data in multiple formats.

## File Imports

The file begins by importing necessary dependencies and components:

```javascript
import React from "react";
import { Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

### Chart Components

- **LineApexChart**
- **DashedLine**
- **SplineArea**
- **Apaexlinecolumn**
- **ColumnWithDataLabels**
- **BarChart**
- **LineColumnArea**
- **RadialChart**
- **PieChart**
- **DonutChart**

These components are imported from various files within the `../AllCharts/apex/` directory and are used to display specific chart types.

## Component Structure

The main component, `Apexchart`, is structured to render a series of chart cards on a page:

```javascript
const Apexchart = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Charts" breadcrumbItem="Apex charts" />
        <Row>
          {/* Chart Rows */}
        </Row>
      </div>
    </React.Fragment>
  );
};
```

### Chart Rows

Each chart is encapsulated within a `Row` and `Col` from Reactstrap, and these are repeated for each type of chart:

```javascript
<Row>
  <Col lg={6}>
    <Card>
      <CardBody>
        <CardTitle className="h4 mb-4">Line with Data Labels</CardTitle>
        <LineApexChart />
      </CardBody>
    </Card>
  </Col>
  {/* Additional Columns */}
</Row>
```

## Chart Types

The component showcases the following chart types:

- **Line Chart with Data Labels**: A standard line chart with additional data labels.
- **Dashed Line Chart**: A variation of the line chart with dashed lines.
- **Spline Area Chart**: A smooth area chart.
- **Column Chart**: Displays data using vertical bars.
- **Column with Data Labels**: A column chart with labels on each bar.
- **Bar Chart**: A horizontal bar chart.
- **Line, Column & Area Chart**: Combines line, column, and area charts into one.
- **Radial Chart**: A circular chart, often used for showing progress.
- **Pie Chart**: A circular chart divided into sectors.
- **Donut Chart**: Similar to a pie chart but with a central hole.

## UI Components

The UI is built using **Reactstrap**, which provides:

- **Row** and **Col**: For responsive grid layout.
- **Card**, **CardBody**, and **CardTitle**: For card-based UI elements.

Each card holds a chart component and is neatly organized to provide a clean layout.

## Conclusion

The **Apexcharts.js** file offers a robust framework for displaying various chart types using React and ApexCharts. By leveraging pre-built components and Reactstrap, it provides an intuitive dashboard for data visualization. This setup is ideal for developers looking to integrate dynamic charts into their React applications. 🎨📊

Feel free to explore and customize the charts to suit your specific data needs! 🚀