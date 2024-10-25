# Documentation for `card-tasks.js` 📄

This file defines the **CardTasks** React component, which is responsible for rendering a list of tasks in a card format. Each task is displayed with options for marking as checked, associated team members, and status badges. This component is designed to be a part of a larger task management or Kanban board application.

## Table of Contents 📚

1. [Component Overview](#component-overview-)
2. [Props](#props-)
3. [Component Structure](#component-structure-)
4. [Styling and Libraries](#styling-and-libraries-)
5. [Usage Example](#usage-example-)
6. [Conclusion](#conclusion-)

## Component Overview 📋

The **CardTasks** component takes in a list of tasks and displays them in a card layout. Each task includes:
- A checkbox to mark the task as checked.
- A task title.
- Team members associated with the task.
- A badge indicating the task status.

## Props 🧩

The component accepts the following **props**:

| Prop Name  | Type          | Description                                   |
|------------|---------------|-----------------------------------------------|
| `data`     | `array`       | An array of task objects to display.          |
| `taskTitle`| `string`      | The title of the task card.                   |

Each task object in the `data` array should have the following structure:

```javascript
{
  id: number,
  isChecked: boolean,
  title: string,
  teamMembers: [
    {
      image: string, // URL or "Null"
      imgText: string
    }
  ],
  color: string, // Badge color
  tastStatus: string
}
```

## Component Structure 🏗️

```jsx
const CardTasks = props => {
  return (
    <React.Fragment>
      <Card>
        <CardBody>
          <CardTitle className="mb-4">{props.taskTitle}</CardTitle>
          <div className="table-responsive">
            <Table className="table-nowrap table-centered mb-0">
              <tbody>
                {props.data.map((task, i) => (
                  <tr key={i}>
                    <td style={{ width: "60px" }}>
                      <div className="custom-control custom-checkbox">
                        {task.isChecked ? (
                          <Input
                            type="checkbox"
                            className="custom-control-input"
                            checked
                            id={"customCheck1_" + task.id}
                          />
                        ) : (
                          <Input
                            type="checkbox"
                            className="custom-control-input"
                            id={"customCheck1_" + task.id}
                          />
                        )}
                        <Label className="custom-control-label" htmlFor={"customCheck1_" + task.id} />
                      </div>
                    </td>
                    <td>
                      <h5 className="text-truncate font-size-14 m-0">
                        <Link to="#" className="text-dark">
                          {task.title}
                        </Link>
                      </h5>
                    </td>
                    <td>
                      <div className="team">
                        {task.teamMembers.map(member =>
                          member.image !== "Null" ? (
                            <Link to="#" className="team-member d-inline-block">
                              <img
                                src={member.image}
                                className="rounded-circle avatar-xs m-1"
                                alt=""
                              />
                            </Link>
                          ) : (
                            <Link to="#" className="team-member d-inline-block">
                              <div className="avatar-xs">
                                <span className="avatar-title rounded-circle bg-soft-primary text-primary">
                                  {member.imgText}
                                </span>
                              </div>
                            </Link>
                          )
                        )}
                      </div>
                    </td>
                    <td>
                      <div className="text-center">
                        <Badge
                          color={task.color}
                          className={"badge-soft-" + task.color + " font-size-11"}
                          pill
                        >
                          {task.tastStatus}
                        </Badge>
                      </div>
                    </td>
                  </tr>
                ))}
              </tbody>
            </Table>
          </div>
        </CardBody>
      </Card>
    </React.Fragment>
  );
};
```

## Styling and Libraries 🎨

- **React**: The component is built using React.js.
- **Reactstrap**: Utilizes components from Reactstrap like `Card`, `CardBody`, `CardTitle`, `Input`, `Label`, `Table`, and `Badge` for UI elements.
- **React Router**: Uses `Link` from `react-router-dom` to handle navigation.
- **PropTypes**: Ensures type safety for props.

## Usage Example 🚀

Here's how you can use the **CardTasks** component in your React application:

```jsx
import React from 'react';
import CardTasks from './card-tasks';

const tasksData = [
  {
    id: 1,
    isChecked: false,
    title: "Complete project documentation",
    teamMembers: [
      { image: "https://example.com/image1.jpg", imgText: "A" },
      { image: "Null", imgText: "B" }
    ],
    color: "success",
    tastStatus: "In Progress"
  },
  // Add more tasks as needed
];

const TaskBoard = () => (
  <div>
    <CardTasks taskTitle="My Tasks" data={tasksData} />
  </div>
);

export default TaskBoard;
```

## Conclusion 🎉

The **CardTasks** component is a versatile and reusable component that fits well in task management applications. It provides a structured way to display tasks along with their status and associated team members. By leveraging React and Reactstrap, it ensures a responsive and modern UI design.

# 📄 Documentation for `card-task-box.js`

## Overview

The `card-task-box.js` file is a **React component** designed to display a card-like UI element. This component is used to showcase individual tasks with details such as task name, status, associated team members, and budget. It leverages the Reactstrap library for styling and layout.

---

## 📂 Table of Contents

1. [Component: CardTaskBox](#component-cardtaskbox)
2. [Props](#props)
3. [Usage](#usage)
4. [Key Features](#key-features)
5. [Dependencies](#dependencies)
6. [Code Explanation](#code-explanation)

---

## Component: `CardTaskBox`

The **`CardTaskBox`** component is a functional React component. It is responsible for rendering the task details in a card format, including the task's status badge, name, date, associated team members, and the allocated budget.

### 📋 Props

| Prop Name | Type   | Description                                  |
|-----------|--------|----------------------------------------------|
| `data`    | object | An object containing task details.           |

The `data` prop should be structured with the following keys: `badgecolor`, `status`, `name`, `date`.

### 🛠️ Usage

To utilize this component, you import it and pass the required `data` prop to display a task:

```jsx
import CardTaskBox from './card-task-box';

const taskData = {
  badgecolor: 'primary',
  status: 'In Progress',
  name: 'Design the homepage',
  date: '2023-10-05',
};

<CardTaskBox data={taskData} />
```

### 🌟 Key Features

- **Status Badge**: Displays a badge with a color and label representing the task's current status.
- **Task Details**: Shows the task's name and the due date.
- **Team Members**: Displays avatars of team members working on the task.
- **Budget Display**: Shows the task's budget in a summarized format.

### 📦 Dependencies

This component relies on the following libraries:

- `prop-types`: For type-checking the props.
- `react-router-dom`: For handling navigation links.
- `reactstrap`: For using Bootstrap-based components.

### 📝 Code Explanation

```jsx
<Card className="task-box">
  <CardBody className="borad-width">
    <div className="float-end ms-2">
      <Badge className={"badge rounded-pill font-size-12 badge-soft-" + props.data["badgecolor"]} pill>
        {props.data["status"]}
      </Badge>
    </div>
    <div>
      <h5 className="font-size-15">
        <Link to="#" className="text-dark">
          {props.data["name"]}
        </Link>
      </h5>
      <p className="text-muted mb-4">{props.data["date"]}</p>
    </div>
    <div className="team float-start">
      <div className="team-member d-inline-block">
        <Link to="#" className="d-inline-block">
          <img src={avatar4} className="rounded-circle avatar-xs m-1" alt="" />
        </Link>
      </div>
      <Link to="#" className="team-member d-inline-block">
        <img src={avatar5} className="rounded-circle avatar-xs m-1" alt="" />
      </Link>
      <Link to="#" className="team-member d-inline-block">
        <div className="avatar-xs">
          <span className="avatar-title rounded-circle bg-soft-primary text-primary">3 +</span>
        </div>
      </Link>
    </div>
    <div className="text-end">
      <h5 className="font-size-15 mb-1">$ 145</h5>
      <p className="mb-0 text-muted">Budget</p>
    </div>
  </CardBody>
</Card>
```

- **Badge**: The task's status is displayed using a Bootstrap badge styled with `badge-soft-` followed by the color from the `data` prop.
- **Task Name and Date**: Rendered as a heading and a paragraph, respectively.
- **Team Members**: Images are displayed in a circular avatar format, with a placeholder for additional team members.
- **Budget**: Displayed on the bottom right of the card.

This component is designed to be flexible and easily integrated into larger applications, especially those handling task management and team collaboration.

# 📜 Documentation for `render-card-title.js`

## 🎯 Purpose

The `render-card-title.js` file in this project is responsible for rendering a card title with an associated dropdown menu. This component is used to display titles on cards with options to edit or delete the content, providing a user-friendly interface for managing tasks or items.

## 🧩 Component Overview

### RenderCardTitle

- **Type:** Functional Component
- **Purpose:** Renders a card title with a dropdown menu for additional actions.
- **Props:**
  - `title` (string): The text to be displayed as the card title.

### 🖼️ Structure

The component is structured using React and styled with Reactstrap components. Here’s a breakdown of its structure:

```jsx
<React.Fragment>
  <UncontrolledDropdown className="float-end">
    <DropdownToggle href="#" className="arrow-none" tag="i">
      <i className="mdi mdi-dots-vertical m-0 text-muted h5" />
    </DropdownToggle>
    <DropdownMenu right>
      <DropdownItem href="#">Edit</DropdownItem>
      <DropdownItem href="#">Delete</DropdownItem>
    </DropdownMenu>
  </UncontrolledDropdown>
  <CardTitle className="mb-4">{props.title}</CardTitle>
</React.Fragment>
```

- **UncontrolledDropdown**: Provides a dropdown menu without requiring manual control of its state.
  - **DropdownToggle**: The trigger for the dropdown, styled as a vertical ellipsis (`mdi mdi-dots-vertical`).
  - **DropdownMenu**: Contains actions like `Edit` and `Delete`.

- **CardTitle**: Displays the main title of the card.

## 🔧 Props Validation

The component uses `PropTypes` to enforce type-checking on the `title` prop, ensuring it is always a string:

```jsx
RenderCardTitle.propTypes = {
  title: PropTypes.string
}
```

## 🚀 Usage

### Importing the Component

To use this component, import it into your React application as follows:

```javascript
import RenderCardTitle from './render-card-title';
```

### Implementing the Component

Here’s an example of how to implement the `RenderCardTitle` component:

```jsx
<RenderCardTitle title="Project Overview" />
```

This will render a card title with the text "Project Overview" and a dropdown menu with options to edit or delete.

## 🎨 Styling

The component utilizes Reactstrap for styling, including classes to handle layout and appearance:

- **Classes Used:**
  - `float-end`: Aligns the dropdown to the right.
  - `arrow-none`: Removes the default arrow styling.
  - `mdi mdi-dots-vertical`: Applies the vertical ellipsis icon.
  - `m-0`, `text-muted`, `h5`: Additional text and spacing styling.
  - `mb-4`: Adds margin to the bottom of the card title.

## ⚙️ Dependencies

This component relies on the following libraries:

- **React**: For building the component.
- **PropTypes**: For type-checking the component's props.
- **Reactstrap**: For UI components and styling.

## 📦 Export

The `RenderCardTitle` component is exported as the default export from the module:

```javascript
export default RenderCardTitle;
```

This allows it to be easily imported and used in other parts of the application.

---

This documentation provides a comprehensive guide to understanding and utilizing the `RenderCardTitle` component within your React projects. The component offers a streamlined way to integrate card titles with actionable dropdown menus, enhancing the user interaction experience.

# 📄 Documentation for `render-card-column.js`

Welcome to the documentation for the `render-card-column.js` file! This file contains a simple React component that serves a specific purpose within the application's UI. Let's dive into the details of this component.

## 📚 Overview

The `RenderCardColumn` component is a React functional component that renders a button. This button is styled to stand out and is designed to trigger additional actions or functionalities, typically used for adding new items or cards in a Kanban board interface or a similar UI layout.

## 📂 File Structure

- **Filename**: render-card-column.js
- **Component**: RenderCardColumn

## 🛠️ Component Description

### RenderCardColumn

This is a functional React component that returns a button element. Here's a breakdown of its functionality:

- **Purpose**: The button is styled with Bootstrap classes and an icon to indicate that it is used for adding new content or triggering an action. It's commonly used in interfaces that require the addition of new tasks, cards, or columns.

### Component Code

```javascript
import React from "react";
import { Link } from "react-router-dom";

const RenderCardColumn = () => {
  return (
    <React.Fragment>
      <div className="text-center">
        <Link
          to="#"
          className="btn btn-primary btn-block mt-1 waves-effect waves-light"
        >
          <i className="mdi mdi-plus ms-1" />
        </Link>
      </div>
    </React.Fragment>
  );
};

export default RenderCardColumn;
```

## ✨ Key Features

- **Button Styling**: The button is styled using Bootstrap classes such as `btn`, `btn-primary`, `btn-block`, `mt-1`, `waves-effect`, and `waves-light`. These classes ensure the button is prominent and provides visual feedback on interaction.
  
- **Icon Integration**: The button includes an icon (`mdi mdi-plus`), which is a common symbol for "add" or "new". This visual cue helps users understand the button's purpose at a glance.

- **Link Component**: The button is wrapped with a `Link` component from `react-router-dom`, indicating that it can be used to navigate to a different route or trigger client-side routing, which is useful for a single-page application (SPA).

## 🔗 Related Components

While this component is quite standalone, it's often used in conjunction with other components in a task management or Kanban board UI:

- **Task Cards**: Used alongside task cards to add new tasks.
- **Boards**: Can be used to add new boards or columns in a Kanban-style application.

## ⚙️ Usage

This component is meant to be used in places where you need a straightforward button to add new items. It is highly reusable and can be integrated into various parts of your UI that require similar functionality.

```javascript
// Example usage in a parent component
import RenderCardColumn from './render-card-column';

const TaskBoard = () => {
  return (
    <div>
      {/* Other components */}
      <RenderCardColumn />
      {/* Other components */}
    </div>
  );
};
```

## 📝 Conclusion

In summary, the `RenderCardColumn` component is a simple yet effective UI element that enhances user interaction by providing a clear call-to-action for adding new content. Its integration with the `Link` component allows for flexible routing and navigation in modern web applications.

Feel free to integrate and customize it further to fit your application's needs! 🚀

# Documentation for `tasks-create.js` 📄

The `tasks-create.js` file is a React component designed for creating new tasks within an application. It provides a user-friendly interface to input task details such as name, description, date, team members, and budget. This component utilizes several third-party libraries to enhance functionality, including Reactstrap for UI components, react-draft-wysiwyg for a rich text editor, and react-datepicker for date selection.

## Table of Contents
1. [Features](#features)
2. [Structure](#structure)
3. [Components and Props](#components-and-props)
4. [Functions](#functions)
5. [Dependencies](#dependencies)

---

## Features ✨

- **Task Name Input**: A field to enter the name of the task.
- **Rich Text Editor**: Allows users to input a detailed description with formatting options.
- **Date Picker**: Users can select a start and end date for the task.
- **Team Member Management**: Add or remove team members dynamically.
- **Budget Input**: Field to specify the budget for the task.
- **Breadcrumb Navigation**: Displays the current location within the application.

## Structure 🏗️

```jsx
<>
  <div className="page-content">
    <Breadcrumbs title="Tasks" breadcrumbItem="Create Task" />
    <Row>
      <Col lg="12">
        <Card>
          <CardBody>
            <CardTitle className="mb-4">Create New Task</CardTitle>
            <form className="outer-repeater">
              {/* Task Name */}
              {/* Task Description */}
              {/* Task Date */}
              {/* Team Members */}
              {/* Task Budget */}
            </form>
          </CardBody>
        </Card>
      </Col>
    </Row>
  </div>
</>
```

## Components and Props 🧩

- **Breadcrumbs**: A navigation aid in user interfaces.
  - `title`: The main title of the breadcrumb.
  - `breadcrumbItem`: The current page or section.

- **Row and Col**: Layout components from Reactstrap for responsive design.

- **Card, CardBody, CardTitle**: Used to create a styled card layout.

- **Input, FormGroup, Label, Button**: Form elements for user input.

## Functions 🔧

- **`handleAddFields()`**: Adds a new row for entering additional team members.
  ```jsx
  function handleAddFields() {
    const item1 = { name: "", file: "" }
    setinputFields([...inputFields, item1])
  }
  ```

- **`handleRemoveFields(idx)`**: Removes the specified team member input row.
  ```jsx
  function handleRemoveFields(idx) {
    document.getElementById("nested" + idx).style.display = "none"
  }
  ```

- **`startDateChange(date)`**: Updates the start date state.
  ```jsx
  const startDateChange = date => {
    setstartDate(date)
  }
  ```

- **`endDateChange(date)`**: Updates the end date state.
  ```jsx
  const endDateChange = date => {
    setendDate(date)
  }
  ```

## Dependencies 📦

- **React**: JavaScript library for building user interfaces.
- **Reactstrap**: Bootstrap components for React.
- **react-draft-wysiwyg**: A WYSIWYG editor component for React apps.
- **react-datepicker**: A simple and reusable Datepicker component for React.
- **reactstrap**: Simple React Bootstrap 5 components.

This component is a part of a task management application, offering a comprehensive form for creating new tasks with rich details and flexible inputs. By leveraging modern React practices and libraries, it ensures a smooth and interactive user experience.

# Documentation for `tasks-kanban.js` 📑

Welcome to the documentation for the **Tasks Kanban** component. This React component integrates a Kanban-style board within a task management application. It leverages Redux for state management and React Router for navigation. Let's dive into the details! 🚀

## Index 🔍
- [Overview](#overview-)
- [Component Structure](#component-structure-)
- [Props](#props-)
- [Redux Integration](#redux-integration-)
- [Usage](#usage-)
- [Additional Information](#additional-information-)

## Overview 🎯

The `TasksKanban` component is designed to render a Kanban board that displays tasks fetched from a Redux store. The component uses the `UncontrolledBoard` component to visualize tasks and columns on the board.

## Component Structure 🏗️

Below is the structure of the component:

```javascript
import React, { useEffect } from "react";
import PropTypes from "prop-types";
import { connect } from "react-redux";
import { withRouter } from "react-router-dom";
import { isEmpty, map } from "lodash";

// Import Breadcrumb
import Breadcrumbs from "../../components/Common/Breadcrumb";
// Import Task Cards
import UncontrolledBoard from "./UncontrolledBoard";

import "../../assets/scss/tasks.scss";
import { getTasks } from "../../store/tasks/actions";

const TasksKanban = props => {
  const { tasks, onGetTasks } = props;

  useEffect(() => {
    onGetTasks();
  }, [onGetTasks]); // Fetch tasks on component mount

  const data = map(tasks, task => ({ ...task, cards: task.tasks }));
  data.length = Math.min(data.length, 3); // Restrict to 3 columns

  return (
    <React.Fragment>
      <div className="page-content">
        {/* Render Breadcrumbs */}
        <Breadcrumbs title="Tasks" breadcrumbItem="Kanban Board" />

        {!isEmpty(data) && (
          <UncontrolledBoard board={{ columns: data }} content={tasks} />
        )}
      </div>
    </React.Fragment>
  );
};
```

## Props 📬

The `TasksKanban` component accepts the following props:

| Prop Name    | Type     | Description                                 |
|--------------|----------|---------------------------------------------|
| `tasks`      | `array`  | Array of task objects fetched from the store. |
| `onGetTasks` | `func`   | Function to dispatch an action to fetch tasks.|

### PropTypes

```javascript
TasksKanban.propTypes = {
  tasks: PropTypes.array,
  onGetTasks: PropTypes.func,
};
```

## Redux Integration 🏢

The component connects to the Redux store to access and fetch task data.

### `mapStateToProps`

Maps the `tasks` state from the Redux store to the component's props.

```javascript
const mapStateToProps = ({ tasks }) => ({
  tasks: tasks.tasks,
});
```

### `mapDispatchToProps`

Provides the dispatch function `onGetTasks` to fetch tasks.

```javascript
const mapDispatchToProps = dispatch => ({
  onGetTasks: () => dispatch(getTasks()),
});
```

The component is connected to the Redux store using the `connect` function from `react-redux`.

```javascript
export default connect(
  mapStateToProps,
  mapDispatchToProps
)(withRouter(TasksKanban));
```

## Usage 🛠️

This component is used within a larger application to provide a Kanban board view of tasks. The tasks are fetched and displayed in columns, allowing users to visualize and manage tasks efficiently.

## Additional Information ℹ️

- **Styling**: The component imports custom styles from `tasks.scss` for visual styling.
- **Dependencies**: Utilizes `lodash` for utility functions and `react-router-dom` for routing capabilities.
- **Breadcrumbs**: Integrates breadcrumbs for enhanced navigation within the application.

This documentation provides you with a comprehensive overview of the `tasks-kanban.js` component. Happy coding! 🎉

# UncontrolledBoard.js Documentation 📋

## Overview
The **UncontrolledBoard.js** file is a React component that utilizes the `@lourenci/react-kanban` library to render a Kanban board. It integrates other components like `CardTaskBox` and `RenderCardTitle` to provide a modular and interactive task management interface.

## Table of Contents
1. [Component Description](#component-description)
2. [Imports](#imports)
3. [Main Component](#main-component)
4. [Props](#props)
5. [Child Components](#child-components)
6. [Code Explanation](#code-explanation)

## Component Description

The **UncontrolledBoard** component is responsible for displaying a Kanban board with columns and cards. It uses child components to render individual cards and column headers, providing a customizable task management experience.

## Imports

```javascript
import React from "react";
import Board from "@lourenci/react-kanban";
import { Row, Col } from "reactstrap";
import CardTaskBox from "./card-task-box";
import RenderCardTitle from "./render-card-title";
```

- **React**: Core library for building user interfaces.
- **Board**: A Kanban board component from `@lourenci/react-kanban` library.
- **reactstrap**: Used for responsive grid layout (`Row` and `Col`).
- **CardTaskBox**: Custom component for rendering each task card.
- **RenderCardTitle**: Custom component for rendering the title of each column.

## Main Component

```javascript
const UncontrolledBoard = props => {
  const content = props.board;

  return (
    <React.Fragment>
      <Row className="mb-4">
        <Col>
          <Board
            initialBoard={content}
            renderColumnHeader={({ title }) => (
              <RenderCardTitle title={title} />
            )}
            renderCard={(data, { dragging }) => (
              <CardTaskBox data={data} dragging={dragging}>
                {data}
              </CardTaskBox>
            )}
            onNewCardConfirm={draftCard => ({
              id: new Date().getTime(),
              ...draftCard,
            })}
          />
        </Col>
      </Row>
    </React.Fragment>
  );
};

export default UncontrolledBoard;
```

## Props

### `props.board`
- **Type**: Object
- **Description**: The initial configuration of the Kanban board, which includes the columns and tasks/cards.

## Child Components

1. **CardTaskBox**: Renders individual task cards with data and dragging state.
2. **RenderCardTitle**: Displays the title of each Kanban column.

## Code Explanation

- **Layout**: The component uses `Row` and `Col` from `reactstrap` to structure the board layout.
- **Kanban Board**: Utilizes the `Board` component from `@lourenci/react-kanban` to manage columns and cards.
  - `initialBoard`: Sets the initial state of the board using `props.board`.
  - `renderColumnHeader`: Customizes the column header by rendering `RenderCardTitle`.
  - `renderCard`: Customizes card rendering using `CardTaskBox`, passing `data` and `dragging` state.
  - `onNewCardConfirm`: Defines how new cards are created, assigning a unique ID based on the current timestamp.

## Conclusion

The **UncontrolledBoard** component serves as a comprehensive solution for rendering a Kanban board in a React application. By leveraging modular components like `CardTaskBox` and `RenderCardTitle`, it ensures flexibility and ease of customization, making it suitable for dynamic task management applications.

# Tasks List Documentation

This documentation provides a comprehensive overview of the `tasks-list.js` file, which is designed to render a list of tasks in a React application. This file is a part of a task management system, utilizing Redux for state management and Reactstrap for UI components.

## Table of Contents

- [Overview](#overview)
- [Component Structure](#component-structure)
- [Key Functionalities](#key-functionalities)
- [PropTypes](#proptypes)
- [Redux Integration](#redux-integration)
- [UI and Styling](#ui-and-styling)
- [Code Breakdown](#code-breakdown)

## Overview

The `TasksList` component is responsible for displaying a detailed list of tasks, including task title, description, team members, and status. It also features a chart visualization for tasks using the `ReactApexChart` component.

## Component Structure

```jsx
import React, { useEffect } from "react";
import PropTypes from "prop-types";
import { connect } from "react-redux";
import { isEmpty, map, size } from "lodash";
import { Link, withRouter } from "react-router-dom";
import classNames from "classnames";
import { Card, CardBody, CardTitle, Col, Row } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import ReactApexChart from "react-apexcharts";
import { getTasks } from "../../store/tasks/actions";
import { options, series, statusClasses } from "../../common/data/tasks";
```

## Key Functionalities

- **Task Listing**: Displays tasks in a list format, allowing users to view task details such as team members and status.
- **Recent Tasks**: Shows a list of recent tasks separately.
- **Task Chart**: Visualizes task data using a line chart.
- **Dynamic Rendering**: Utilizes `map` from lodash to dynamically render tasks and team members.
- **Conditional Rendering**: Checks for recent tasks and only renders them if present.

## PropTypes

```jsx
TasksList.propTypes = {
  tasks: PropTypes.array,
  onGetTasks: PropTypes.func,
};
```

- `tasks`: An array of task objects that the component will render.
- `onGetTasks`: A function to dispatch the action to retrieve tasks.

## Redux Integration

The component is connected to the Redux store to manage the state of tasks. It uses `mapStateToProps` to access tasks from the state and `mapDispatchToProps` to dispatch actions.

### mapStateToProps

Maps the `tasks` state from the Redux store to the component's props.

### mapDispatchToProps

Defines the `onGetTasks` function which dispatches the `getTasks` action to fetch tasks from the backend or store.

## UI and Styling

- **Reactstrap Components**: Uses `Card`, `CardBody`, `CardTitle`, `Col`, and `Row` for layout and styling.
- **ClassNames**: Utilizes `classNames` library to conditionally apply styles based on task status.

## Code Breakdown

### Fetching Tasks

The component uses `useEffect` to fetch tasks when it mounts. This function ensures that the `onGetTasks` action is called, populating the Redux store with task data.

```jsx
useEffect(() => {
  onGetTasks();
}, [onGetTasks]);
```

### Rendering Task List

Tasks are rendered inside a loop using `map`, providing a card for each task. It displays task titles, descriptions, and members.

```jsx
{map(tasks, (task, i) => (
  <Card key={i}>
    <CardBody>
      <CardTitle className="mb-4">{task.title}</CardTitle>
      ...
    </CardBody>
  </Card>
))}
```

### Team Member Display

Displays team members with images or initials when an image is unavailable. It truncates the display if there are more than two members, showing a "+X" indicator.

```jsx
<div className="team">
  {map(item.members, (member, index) => index < 2 && (
    <Link to="#" className="team-member d-inline-block" key={index}>
      ...
    </Link>
  ))}
  {size(item.members) > 2 && (
    <Link to="#" className="d-inline-block">
      <div className="avatar-xs">
        <span className="avatar-title rounded-circle bg-soft-primary text-primary">
          {size(item.members) - 2} +
        </span>
      </div>
    </Link>
  )}
</div>
```

### Task Status

Applies a badge with style based on the task's status using `statusClasses`.

```jsx
<td>
  <div className="text-center">
    <span className={classNames("badge badge-pill font-size-11", statusClasses[item.status.toLowerCase()])}>
      {item.status}
    </span>
  </div>
</td>
```

## Conclusion

The `TasksList` component effectively displays tasks with detailed information, leveraging Redux for state management and Reactstrap for UI styling. It ensures dynamic and responsive task rendering, making it a crucial part of the task management system. The integration of charts enhances the visual representation of task data, providing valuable insights into task progress and status.