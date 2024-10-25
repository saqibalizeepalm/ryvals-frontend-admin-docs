# 📚 Project Documentation

This documentation covers the functionality and purpose of two JavaScript files: `DeleteModal.js` and `index.js`. These files are part of a React-based calendar application, which utilizes various libraries to provide a comprehensive user interface for managing events.

---

## Index

- [DeleteModal.js](#deletemodaljs)
  - [Overview](#overview)
  - [Key Components](#key-components)
  - [Props](#props)
  - [Usage](#usage)
- [index.js](#indexjs)
  - [Overview](#overview-1)
  - [Key Components](#key-components-1)
  - [Functions](#functions)
  - [Event Handling](#event-handling)
  - [Redux Integration](#redux-integration)
  - [Usage](#usage-1)

---

## DeleteModal.js

### Overview

The `DeleteModal.js` file defines a **React functional component** called `DeleteModal`. This component is a modal dialog that is used to confirm the deletion of an event in the calendar application.

### Key Components

- **Reactstrap Modal**: Utilizes `reactstrap` to provide a styled modal.
- **Icons and Buttons**: Includes an alert icon and two buttons for user interaction.

### Props

The `DeleteModal` component accepts the following props:

| Prop Name      | Type          | Description                                |
|----------------|---------------|--------------------------------------------|
| `show`         | `any`         | Determines if the modal is visible.        |
| `onDeleteClick`| `function`    | Callback function when "Yes, delete it!" is clicked. |
| `onCloseClick` | `function`    | Callback function when "Cancel" is clicked. |

### Usage

```javascript
<DeleteModal 
  show={deleteModal} 
  onDeleteClick={handleDeleteEvent} 
  onCloseClick={() => setDeleteModal(false)} 
/>
```

This modal is triggered to confirm deletion actions, providing a clear UI prompt to the user.

---

## index.js

### Overview

The `index.js` file contains the main calendar component of the application. It integrates with Redux for state management and utilizes the FullCalendar library to display and manage events.

### Key Components

- **FullCalendar**: A robust calendar interface with drag-and-drop, date selection, and event creation/editing capabilities.
- **Reactstrap Components**: Provides UI components like Cards, Buttons, and Modals.
- **Availity Reactstrap Validation**: Implements form validation for event details.

### Functions

1. **toggle()**: Manages the visibility of the event modal.
2. **toggleCategory()**: Manages the visibility of the category modal.
3. **handleDateClick(arg)**: Opens the event modal for a specific date.
4. **handleEventClick(arg)**: Populates the modal with event data for editing.
5. **handleValidEventSubmit(e, values)**: Validates and submits event data.
6. **handleDeleteEvent()**: Deletes the selected event.
7. **onDrop(event)**: Handles adding events via drag-and-drop.

### Event Handling

- **Date Click**: Opens a modal to create a new event.
- **Event Click**: Opens a modal to edit an existing event.
- **Drag and Drop**: Allows events to be dragged and dropped on the calendar.

### Redux Integration

The component connects to a Redux store to manage events and categories. It uses actions such as:

- `getEvents()`
- `getCategories()`
- `addNewEvent(event)`
- `updateEvent(event)`
- `deleteEvent(event)`

### Usage

```javascript
<FullCalendar
  plugins={[BootstrapTheme, dayGridPlugin, interactionPlugin]}
  headerToolbar={{
    left: "prev,next today",
    center: "title",
    right: "dayGridMonth,dayGridWeek,dayGridDay",
  }}
  events={events}
  editable={true}
  droppable={true}
  selectable={true}
  dateClick={handleDateClick}
  eventClick={handleEventClick}
  drop={onDrop}
/>
```

The `FullCalendar` component is configured to allow interaction and responsive design, integrating seamlessly with the rest of the UI.

---

This documentation provides a comprehensive overview of how the components and logic are structured in these files. They collectively allow for a dynamic, interactive calendar application that enables users to manage events effectively.

# TournamentDetailsTab.jsx Documentation

The `TournamentDetailsTab.jsx` component is designed to display the details of a specific tournament in a structured and user-friendly format. This documentation will guide you through the components, functionalities, and usage of this file.

## Overview

- **Purpose**: Display detailed information about a tournament, including its rules, game type, bracket style, teams, and more.
- **Libraries Used**: React, Reactstrap, Lodash, and external utilities for CSV conversion and HTML sanitization.

## Components and Functions

### Imports

- **React & Hooks**: 
  - `useEffect`, `useState` from React for managing component states and side effects.
- **Reactstrap**: 
  - Components like `Card`, `CardBody`, `Col`, and `Row` for layout structure.
- **Utilities**:
  - `csvConverterToPreviewFile`, `dateFormat`, `competitionStatus` from `helpers/util` for formatting data.
  - `sanitize` from `sanitize-html` for safe rendering of HTML content.
  - `isEmpty` from Lodash to check for empty objects or arrays.
- **Custom Components**:
  - `PrizeList` for displaying prize details.
  - `CsvView` for rendering CSV content.

### State Management

- **State Variables**:
  - `previewOldcsvData`: Stores the processed data from the CSV file associated with the tournament.

### Functions

- **`callUrl`**: Fetches the CSV file containing team rankings from the given URL and converts it into a format suitable for preview.
- **`useEffect`**: Automatically calls `callUrl` when the component mounts if a team rank file exists.

### JSX Structure

#### Card Structure

The main structure encapsulated within a `Card` and `CardBody` with several `Row` and `Col` components for layout purposes.

- **Tournament Basic Info**:
  - Tournament Name
  - Game Type and Game
  - Entry Fee
  - Bracket Style and Seeding

- **Conditional Display**:
  - If `seeding` is "Qualifiers", display the selected tournament.
  - If `game_type` is "PPK", display Lobby Size and Threshold.
  - If `seeding` is "Ranked Placement", show whether players can add ranks.

- **Team and Schedule Info**:
  - Minimum and Maximum Teams
  - Players Per Team
  - Enrolled Teams
  - Start Date and Time
  - Last Entry Time

- **Prize and Rules**:
  - Prize list using `PrizeList` component.
  - Game and Tournament rules rendered safely with `sanitize`.

- **Status Information**:
  - Active and Free status of the tournament.
  - Current tournament status derived from `competitionStatus`.

## Usage

This component is primarily used within a broader application managing tournaments. It expects a `details` prop containing all relevant information about a specific tournament.

### Example

```jsx
<TournamentDetailsTab details={tournamentDetails} />
```

Here, `tournamentDetails` would be an object containing fields such as `name`, `game_type`, `entry_fee`, `price`, and so on.

## Styling and Design

- Utilizes `Reactstrap` for a responsive and consistent layout.
- Ensures safe HTML rendering using `sanitize-html`.
- CSV data handling is performed using utility functions for seamless integration.

## Conclusion

The `TournamentDetailsTab` component provides a comprehensive view of tournament details, integrating various pieces of information and displaying them in an organized manner. With its use of state management and conditional rendering, it offers flexibility and robustness for displaying tournament data.