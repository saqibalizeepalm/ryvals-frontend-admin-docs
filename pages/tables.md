# ResponsiveTables.js Documentation 📄

ResponsiveTables.js is a React component designed to provide an elegant solution for rendering responsive tables that accommodate complex data. This component leverages the `react-super-responsive-table` library to ensure that tables remain usable and readable across different screen sizes. Below, you'll find a detailed breakdown of the file, its purpose, and how it works.

## Table of Contents 📚

1. [Overview](#overview)
2. [Imports](#imports)
3. [Component Structure](#component-structure)
4. [Features](#features)
5. [Code Explanation](#code-explanation)
6. [Usage](#usage)

## Overview

The **ResponsiveTables.js** file is part of a React application and is responsible for displaying a responsive table layout that can adapt to various screen sizes. This component is particularly useful for applications that require complex data representation while ensuring accessibility and usability on both desktop and mobile devices.

## Imports

Here's a breakdown of the libraries and components imported in this file:

- **React**: The core library for building the component.
- **reactstrap**: Provides Bootstrap 4 components as React components.
  - `Row`, `Col`, `Card`, `CardBody`, `CardTitle`: Used for layout and styling.
- **react-super-responsive-table**: A library to make tables responsive.
  - `Table`, `Thead`, `Tbody`, `Tr`, `Th`, `Td`: Used to create a responsive table structure.
- **react-super-responsive-table/dist/SuperResponsiveTableStyle.css**: CSS styles for responsive tables.
- **Breadcrumbs**: A custom component for breadcrumb navigation.

## Component Structure

The **ResponsiveTables** component is a functional component that returns a React fragment containing the layout and table structure.

### JSX Structure

```jsx
<React.Fragment>
  <div className="page-content">
    <Breadcrumbs title="Tables" breadcrumbItem="Responsive Table" />
    <Row>
      <Col className="col-12">
        <Card>
          <CardBody>
            <CardTitle className="h4">Example</CardTitle>
            <p className="card-title-desc">
              This is an experimental awesome solution for responsive tables with complex data.
            </p>
            <div className="table-rep-plugin">
              <div className="table-responsive mb-0" data-pattern="priority-columns">
                <Table id="tech-companies-1" className="table table-striped table-bordered">
                  {/* Table Headings */}
                  <Thead>
                    <Tr>
                      <Th>Company</Th>
                      <Th data-priority="1">Last Trade</Th>
                      <Th data-priority="3">Trade Time</Th>
                      <Th data-priority="1">Change</Th>
                      <Th data-priority="3">Prev Close</Th>
                      <Th data-priority="3">Open</Th>
                      <Th data-priority="6">Bid</Th>
                      <Th data-priority="6">Ask</Th>
                      <Th data-priority="6">1y Target Est</Th>
                    </Tr>
                  </Thead>
                  {/* Table Body */}
                  <Tbody>
                    {/* Data Rows */}
                    <Tr>
                      <Th>GOOG <span className="co-name">Google Inc.</span></Th>
                      <Td>597.74</Td>
                      <Td>12:12PM</Td>
                      <Td>14.81 (2.54%)</Td>
                      <Td>582.93</Td>
                      <Td>597.95</Td>
                      <Td>597.73 x 100</Td>
                      <Td>597.91 x 300</Td>
                      <Td>731.10</Td>
                    </Tr>
                    {/* Additional Rows... */}
                  </Tbody>
                </Table>
              </div>
            </div>
          </CardBody>
        </Card>
      </Col>
    </Row>
  </div>
</React.Fragment>
```

## Features

- **Responsive Design**: Utilizes `react-super-responsive-table` to create tables that adapt to screen size changes.
- **Complex Data Handling**: Capable of displaying intricate sets of data without losing readability.
- **Stylish Layout**: Integrates with Bootstrap for a sleek and professional interface.
- **Accessibility**: Ensures tables are accessible across devices, enhancing user experience.

## Code Explanation

- **Breadcrumbs**: Provides navigation aids within the application.
- **Card Layout**: Encases the table within a card component for a structured look.
- **Table Structure**: Composed of `Thead` for headers and `Tbody` for data rows, ensuring a clear separation of table components.
- **Priority Columns**: Uses `data-priority` to determine which columns are essential when the table is viewed on smaller screens.

## Usage

To use this component, simply import and render it within your React application:

```jsx
import ResponsiveTables from './ResponsiveTables';

function App() {
  return (
    <div>
      <ResponsiveTables />
    </div>
  );
}

export default App;
```

By doing so, you can easily integrate responsive tables into your web application to display complex datasets gracefully across devices.

---

This component ensures that your data remains accessible and visually appealing, regardless of the device being used. With the power of `react-super-responsive-table`, you can deliver excellent user experiences in data-heavy applications. 🚀

# 📚 EditableTables.js Documentation

Welcome to the documentation for **EditableTables.js**. This file is responsible for creating an editable table component using React and several third-party libraries. This component allows users to modify table data directly in the browser, providing a seamless editing experience.

## 📄 File Overview

**EditableTables.js** is a React component that utilizes:

- **React-Bootstrap-Table**: A library that provides Bootstrap-styled tables with extensive customization options.
- **React-Bootstrap-Table2-Editor**: An extension for React-Bootstrap-Table that adds editing capabilities.
- **Reactstrap**: A popular library that provides Bootstrap components for React.

## 📑 Index

1. [Imports](#imports)
2. [Data Setup](#data-setup)
3. [Columns Configuration](#columns-configuration)
4. [EditableTables Component](#editabletables-component)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

---

## 1. 📥 Imports

```javascript
import React from "react";
import { Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import BootstrapTable from "react-bootstrap-table-next";
import cellEditFactory, { Type } from "react-bootstrap-table2-editor";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

### Description

- **React**: Core library for building UI components.
- **Reactstrap Components**: Used for layout and styling (`Row`, `Col`, `Card`, `CardBody`, `CardTitle`).
- **BootstrapTable**: Component from `react-bootstrap-table-next` to create tables.
- **cellEditFactory**: Function to enable editing capabilities within the table.
- **Breadcrumbs**: A component for displaying navigation breadcrumbs.

---

## 2. 📋 Data Setup

```javascript
const products = [
  { id: 1, age: 25, type: "Male", name: "David McHenry" },
  { id: 2, age: 34, type: "Male", name: "Frank Kirk" },
  { id: 3, age: 67, type: "Male", name: "Rafael Morales" },
  { id: 4, age: 23, type: "Male", name: "Mark Ellison" },
  { id: 5, age: 78, type: "Female", name: "Minnie Walter" },
];
```

### Description

- The `products` array contains a list of objects representing table rows.
- Each object includes an `id`, `age`, `type`, and `name`.

---

## 3. 📊 Columns Configuration

```javascript
const columns = [
  { dataField: "id", text: "ID" },
  { dataField: "name", text: "Name" },
  { dataField: "age", text: "Age(AutoFill)" },
  {
    dataField: "type",
    text: "Gender(AutoFill and Editable)",
    editor: {
      type: Type.SELECT,
      options: [
        { value: 'Male', label: 'Male' },
        { value: 'Female', label: 'Female' }
      ],
    },
  },
];
```

### Description

- **`id` and `name`**: Basic non-editable columns.
- **`age`**: Shown as "Age(AutoFill)" indicating it's autofilled.
- **`type`**: Editable with a dropdown list for "Male" or "Female".

---

## 4. 🖊️ EditableTables Component

```javascript
const EditableTables = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Tables" breadcrumbItem="Editable Table" />
        <Row>
          <Col>
            <Card>
              <CardBody>
                <CardTitle className="h4">Datatable Editable</CardTitle>
                <p className="card-title-desc">
                  Table Edits is a lightweight jQuery plugin for making table rows editable.
                </p>
                <div className="table-responsive">
                  <BootstrapTable
                    keyField="id"
                    data={products}
                    columns={columns}
                    cellEdit={cellEditFactory({ mode: "click" })}
                  />
                </div>
              </CardBody>
            </Card>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
};
```

### Components Explained

- **Breadcrumbs**: Displays navigation path.
- **BootstrapTable**: Renders the table with data and columns.
- **cellEditFactory**: Configures the table to be editable on click.

---

## 5. 🚀 Usage

To use the **EditableTables** component:

1. Ensure all required libraries are installed:
   ```bash
   npm install react-bootstrap-table-next react-bootstrap-table2-editor reactstrap
   ```

2. Import and use the component in your React application:
   ```javascript
   import EditableTables from './path/to/EditableTables';

   function App() {
     return <EditableTables />;
   }

   export default App;
   ```

---

## 6. 🏁 Conclusion

The **EditableTables.js** component provides a robust and user-friendly interface for displaying and editing table data. Leveraging powerful libraries, it offers extensive customization and flexibility, making it a great choice for any React application that requires editable tables. 🎉

Feel free to modify the data and columns configuration to suit your application's needs. Happy coding! 💻✨

# 📄 DatatableTables.js Documentation

Welcome to the documentation for **DatatableTables.js**! This file is a part of a React application and is responsible for rendering datatables with the help of `MDBDataTable` from the `mdbreact` library. This component is useful for displaying tabular data with enhanced features like sorting, pagination, and responsive design.

---

## 📚 Index

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Overview](#component-overview)
4. [Data Structure](#data-structure)
5. [Features](#features)
6. [Usage](#usage)

---

## 🔍 Introduction

**DatatableTables.js** is a React component file that renders a data table using the `MDBDataTable` component from the `mdbreact` library. It provides an interactive and responsive way to display data, making it easy to sort, search, and paginate through information.

---

## 📦 Dependencies

This component relies on several dependencies, which are essential for its functionality:

- **React**: A JavaScript library for building user interfaces.
- **mdbreact**: A React UI Kit based on Material Design for Bootstrap, which provides the `MDBDataTable` component.
- **reactstrap**: A library that provides Bootstrap 4 components as React components.
- **Breadcrumbs Component**: Used to display the navigation path.

```javascript
import React from "react";
import { MDBDataTable } from "mdbreact";
import { Row, Col, Card, CardBody, CardTitle, CardSubtitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import "./datatables.scss";
```

---

## 🏗️ Component Overview

The **DatatableTables** component is structured as a functional component, which returns a JSX layout. It includes:

- A breadcrumb for navigation.
- A responsive data table utilizing `MDBDataTable`.
- A card layout from `reactstrap` to encapsulate the data table.

```javascript
const DatatableTables = () => {
    // JSX rendering logic here...
};
```

---

## 📊 Data Structure

The data rendered in the table is defined in a structured format with `columns` and `rows`:

### Columns

- **label**: The header label of the column.
- **field**: The key used to map to the data in the rows.
- **width**: The width of the column.

### Rows

Each row object corresponds to a row of data and includes the following fields:

- **name**: Employee's name.
- **position**: Job position of the employee.
- **office**: Location of the office.
- **age**: Age of the employee.
- **date**: Start date of employment.
- **salary**: Salary information.

```javascript
const data = {
  columns: [
    { label: "Name", field: "name", width: 150 },
    { label: "Position", field: "position", width: 270 },
    { label: "Office", field: "office", width: 200 },
    { label: "Age", field: "age", width: 100 },
    { label: "Start date", field: "date", width: 150 },
    { label: "Salary", field: "salary", width: 100 },
  ],
  rows: [
    { name: "Tiger Nixon", position: "System Architect", office: "Edinburgh", age: "61", date: "2011/04/25", salary: "$320" },
    // Additional row data...
  ],
};
```

---

## 🌟 Features

- **Responsive Design**: The table adjusts itself according to the screen size.
- **Striped Rows**: Rows are displayed with alternating background colors.
- **Pagination**: Facilitates easy navigation through different pages of data.
- **Search Functionality**: Allows users to search for specific data within the table.
- **Sortable Columns**: Columns can be sorted to organize data alphabetically or numerically.

---

## ⚙️ Usage

To use the **DatatableTables** component, import it into your desired file and render it within your JSX. Ensure that all dependencies, especially `mdbreact` and `reactstrap`, are properly installed in your project.

```javascript
import DatatableTables from "./path/to/DatatableTables";

function App() {
  return (
    <div className="App">
      <DatatableTables />
    </div>
  );
}
```

---

This concludes the documentation for **DatatableTables.js**. This file provides a robust and efficient way to present data in a tabular format with various interactions, enhancing the user's ability to manage and interpret data effectively. 🚀

# 📚 BasicTables.js Documentation

Welcome to the **BasicTables.js** documentation! This file is part of a React application and leverages `reactstrap` components to display various types of tables. Tables are an essential UI component for displaying data in a structured and readable format. Let's dive into the details of what each section of this file does.

## 📑 Index

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [Table Types Explained](#table-types-explained)
   - [Basic Example](#basic-example)
   - [Dark Table](#dark-table)
   - [Table Head](#table-head)
   - [Striped Rows](#striped-rows)
   - [Bordered Table](#bordered-table)
   - [Borderless Table](#borderless-table)
   - [Hoverable Table](#hoverable-table)
   - [Small Table](#small-table)
   - [Contextual Classes](#contextual-classes)
   - [Captions](#captions)
   - [Responsive Tables](#responsive-tables)
5. [Conclusion](#conclusion)

## 📜 Introduction

The **BasicTables.js** file defines a React component that renders several types of tables using `reactstrap`, a popular library for React Bootstrap components. These tables demonstrate various styles and functionalities that can be applied to standard HTML tables.

## 📦 Dependencies

This component relies on the following imports:

```javascript
import React from "react";
import { Table, Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: Provides Bootstrap components as React components.
- **Breadcrumbs**: A custom component for navigational breadcrumb.

## 🏗️ Component Structure

The component is structured using several `reactstrap` components:

- **Breadcrumbs**: Displays the navigational path for the tables page.
- **Row** and **Col**: Organize the layout.
- **Card** and **CardBody**: Group each table with a title and description.
- **Table**: The main component for displaying tabular data.

## 📊 Table Types Explained

### 🟢 Basic Example

**Description**: A simple table with light padding and horizontal dividers.
**Class**: `.table`

```javascript
<Table className="table mb-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 🌑 Dark Table

**Description**: Inverted colors with light text on a dark background.
**Class**: `.table-dark`

```javascript
<Table className="table table-dark mb-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 🌗 Table Head

**Description**: Light or dark gray table headers.
**Class**: `.table-light` or `.table-dark` for `<thead>`

```javascript
<thead className="table-light">
  <tr>...</tr>
</thead>
```

### 🦓 Striped Rows

**Description**: Zebra-striping for rows for better readability.
**Class**: `.table-striped`

```javascript
<Table className="table table-striped mb-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 🟥 Bordered Table

**Description**: Adds borders to all sides of the table and cells.
**Class**: `.table-bordered`

```javascript
<Table className="table table-bordered mb-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 🟦 Borderless Table

**Description**: Removes borders from the table.
**Class**: `.table-borderless`

```javascript
<Table className="table table-borderless mb-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 🖱️ Hoverable Table

**Description**: Highlights rows when hovered over.
**Class**: `.table-hover`

```javascript
<Table className="table table-hover mb-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 📏 Small Table

**Description**: Compact table with reduced cell padding.
**Class**: `.table-sm`

```javascript
<Table className="table table-sm m-0">
  <thead>...</thead>
  <tbody>...</tbody>
</Table>
```

### 🎨 Contextual Classes

**Description**: Color table rows or individual cells using Bootstrap contextual classes like `table-light`, `table-success`, etc.

```javascript
<tr className="table-light">...</tr>
<tr className="table-success">...</tr>
```

### 🎓 Captions

**Description**: A `<caption>` tag to provide a title for the table, useful for accessibility.

```javascript
<caption>List of users</caption>
```

### 📱 Responsive Tables

**Description**: Wraps the table in `.table-responsive` to allow horizontal scrolling on small devices.

```javascript
<div className="table-responsive">
  <Table className="table mb-0">...</Table>
</div>
```

## 🏁 Conclusion

The **BasicTables.js** file demonstrates various table styles that can be achieved using `reactstrap` components. By utilizing different classes and structures, developers can create visually appealing and functional tables that enhance the overall user experience. Whether you need simple styling, complex contextual rows, or fully responsive tables, this component has you covered! 🚀