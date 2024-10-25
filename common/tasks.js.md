# 📋 Documentation for `tasks.js`

This documentation provides an in-depth overview of the `tasks.js` file, which is a module responsible for managing tasks within a project. It includes tasks in various states, such as "Example", "In Progress", "Completed", and "Recent Tasks", as well as configuration for visualizing task data using charts. Below you will find detailed information about the structure and purpose of each component in the file.

## 📑 Table of Contents

1. [Overview](#overview)
2. [Tasks Structure](#tasks-structure)
3. [Chart Data](#chart-data)
4. [Chart Options](#chart-options)
5. [Status Classes](#status-classes)
6. [Exported Modules](#exported-modules)

## 📝 Overview

The `tasks.js` file is a JavaScript module that contains:
- A list of tasks categorized by their status.
- Configuration for visualizing the tasks using charts.
- Utility classes for styling task statuses.

## 📂 Tasks Structure

The tasks are organized into categories, each with a unique `id` and `title`. Each category contains a list of task objects with detailed properties:

```javascript
const tasks = [
  {
    id: 1,
    title: "Example",
    tasks: [
      {
        id: 11,
        description: "Create a Qovex Dashboard UI",
        name: 'Topnav layout design',
        date: '14 Oct, 2019',
        members: [
          { username: "", userImg: avatar2 },
          { username: "", userImg: avatar1 },
        ],
        status: "Waiting",
        badgecolor: "secondary",
        budget: "$145",
      },
      // More tasks...
    ],
  },
  // More categories...
];
```

### Task Properties

- **id**: Unique identifier for the task.
- **description**: Brief description of the task.
- **name**: Task name or title.
- **date**: Scheduled date for the task.
- **members**: Array of team members associated with the task, including their `username` and `userImg`.
- **status**: Current status of the task (e.g., "Waiting", "Complete").
- **badgecolor**: Color identifier for the task status.
- **budget**: Estimated budget for the task.

## 📊 Chart Data

The `series` array is used to store data for task visualization in charts:

```javascript
const series = [
  {
    name: "Complete Tasks",
    type: "column",
    data: [23, 11, 22, 27, 13, 22, 52, 21, 44, 22, 30],
  },
  {
    name: "All Tasks",
    type: "line",
    data: [23, 11, 34, 27, 17, 22, 62, 32, 44, 22, 39],
  },
];
```

### Data Structure

- **name**: Name of the data series (e.g., "Complete Tasks").
- **type**: Type of the chart (e.g., "column", "line").
- **data**: Array representing the data values for each month.

## 🎨 Chart Options

Configuration options for rendering the charts are defined in the `options` object:

```javascript
const options = {
  chart: {
    height: 280,
    type: "line",
    stacked: false,
    toolbar: { show: false }
  },
  stroke: { width: [0, 2, 5], curve: "smooth" },
  plotOptions: { bar: { columnWidth: "20%", endingShape: "rounded" } },
  colors: ["#556ee6", "#34c38f"],
  fill: { gradient: { inverseColors: false, shade: "light", type: "vertical", opacityFrom: 0.85, opacityTo: 0.55, stops: [0, 100, 100, 100] } },
  labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov"],
  markers: { size: 0 },
  yaxis: { min: 0 },
};
```

### Key Options

- **chart**: Defines chart type and display properties.
- **stroke**: Configures the appearance of lines in the chart.
- **plotOptions**: Customizes the bar chart options.
- **colors**: Array of colors used in the chart.
- **fill**: Gradient fill options for the chart.
- **labels**: Axis labels for the chart.
- **markers**: Marker configurations on data points.
- **yaxis**: Determines the minimum value for the Y-axis.

## 🚦 Status Classes

The `statusClasses` object maps task statuses to their respective CSS classes:

```javascript
const statusClasses = {
  waiting: "badge-soft-secondary",
  approved: "badge-soft-primary",
  complete: "badge-soft-success",
  pending: "badge-soft-warning",
};
```

## 🚀 Exported Modules

The following objects and arrays are exported for use in other modules:

- `tasks`: All task categories and their respective tasks.
- `series`: Data for task visualization charts.
- `options`: Configuration options for the charts.
- `statusClasses`: Utility classes for task statuses.

This structured and comprehensive documentation provides clarity on the purpose and functionality of the `tasks.js` module. It serves as a reliable reference for developers managing project tasks and visualizing task progress.