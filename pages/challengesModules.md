# Documentation for Challenge Management Components

Welcome to the documentation for the challenge management components within our application. This documentation will guide you through each component's purpose, functionality, and how they interconnect to manage challenges within a gaming platform.

## Index

1. [ApexCodesChallenge Component](#1-apexcodeschallenge-component)
2. [ChallengesDetail Component](#2-challengesdetail-component)
3. [DeleteAlert Component](#3-deletealert-component)
4. [ChallengesList Component](#4-challengeslist-component)
5. [EnrolledChallengeTeamList Component](#5-enrolledchallengeteamlist-component)

---

## 1. ApexCodesChallenge Component

### Description

The `ApexCodesChallenge` component is designed to handle the updating of challenges, allowing an admin to select and assign an administrator to a specific challenge. It integrates various form validations and user interactions to ensure smooth update operations.

### Key Features

- **Admin Selection**: Dropdown to select the admin responsible for the challenge.
- **Form Fields**: Includes fields for admin code, participant code, and statistic code, each with validation.
- **Update Logic**: Handles submission and validation of updates to a challenge.
- **Permissions Check**: Ensures actions are only available to users with the correct permissions.
- **Edit Buffer Check**: Prevents editing if the challenge has ended or if the editing permissions are not met.

### Code Snippet

```jsx
<AvForm onValidSubmit={(e, v) => { handleValidSubmit(e, v); }}>
  <div className="mb-3">
    <Label>Select Admin*</Label>
    <Select
      value={admin_id}
      onChange={handleAdminSelectGroup}
      options={adminList}
      isDisabled={isEditBufferExceeded() || !canPerform(...)}
    />
  </div>
  {/* Additional form fields */}
  <Button type="submit" color="primary">Update</Button>
</AvForm>
```

### Dependencies

- **React**: Core library for building UI.
- **React-Redux**: For accessing global state.
- **React-Select**: For custom dropdown menus.
- **Reactstrap & AvForm**: For form handling and UI components.

---

## 2. ChallengesDetail Component

### Description

The `ChallengesDetail` component provides a detailed view of a specific challenge. It includes information about the challenge, enrolled teams, and results if available. This component facilitates navigation between different views like challenge details, enrolled teams, and results.

### Key Features

- **Breadcrumb Navigation**: Guides users back to the previous page.
- **Tabs for Navigation**: Toggle between challenge details, enrolled teams, and results.
- **Challenge Information**: Displays comprehensive details about the challenge.
- **Enrolled Teams**: Lists teams that have enrolled in the challenge.
- **Delete Functionality**: Allows deletion of a challenge with proper permissions.

### Tabs

- **Challenge Details**: Displays all relevant information about a challenge.
- **Enrolled Teams**: Shows a list of teams enrolled in the challenge.
- **View Results**: Displays results for challenges that have concluded.

### Code Snippet

```jsx
<Nav tabs>
  <NavItem>
    <NavLink onClick={() => { toggle("1"); }}>Challenge Details</NavLink>
  </NavItem>
  <NavItem>
    <NavLink onClick={() => { toggle("2"); }}>Enrolled Teams</NavLink>
  </NavItem>
  {/* Conditional rendering for third tab based on challenge status */}
</Nav>
```

### Dependencies

- **React Router**: For navigation.
- **Reactstrap**: For UI components.
- **DeleteAlert**: Component for handling challenge deletions.
- **ApexCodesChallenge**: Integrated for challenge updates.

---

## 3. DeleteAlert Component

### Description

The `DeleteAlert` component is a confirmation dialog used to confirm and execute the deletion of a challenge. It ensures safe operations by confirming the user's intent and handling the deletion process.

### Key Features

- **Confirmation Dialog**: Displays a warning and confirmation options before deletion.
- **Async Deletion Handling**: Manages loading states and error handling during the deletion process.
- **Feedback**: Uses `react-toastify` to provide feedback upon successful or failed deletion.

### Code Snippet

```jsx
<SweetAlert
  title="Delete Challenge"
  warning
  showCancel
  confirmButtonText="Yes"
  cancelButtonText="No"
  onConfirm={handleDelete}
  onCancel={closeAlert}
>
  <p>Are you sure you want to delete this challenge?</p>
</SweetAlert>
```

### Dependencies

- **SweetAlert**: For beautiful alert dialogs.
- **React-Toastify**: For toast notifications.

---

## 4. ChallengesList Component

### Description

The `ChallengesList` component serves as the main interface for viewing and managing a list of challenges. It provides sorting, filtering, and pagination functionalities to efficiently navigate through challenges.

### Key Features

- **Filter and Sort**: Users can filter challenges by various criteria and sort them accordingly.
- **Pagination**: Allows navigation through multiple pages of challenges.
- **Action Buttons**: Includes options to view details or delete challenges.
- **Loading States**: Displays a loading spinner while data is being fetched.
- **Clear Filters**: Easy reset of all filters to default state.

### Code Snippet

```jsx
<Table>
  <Thead>
    <Tr>
      <Th>Game Name</Th>
      {/* Additional columns */}
      <Th colSpan="2">Actions</Th>
    </Tr>
  </Thead>
  <Tbody>
    {challenges.map((item, index) => (
      <Tr key={index}>
        <Td>{getGameFromId(games, item.game)?.name}</Td>
        {/* Additional columns */}
        <Td>
          <Link to={`/challenges/${item.id}`}>View</Link>
        </Td>
        <Td>
          <Button onClick={() => openAlert(item.id, item.versus)}>Delete</Button>
        </Td>
      </Tr>
    ))}
  </Tbody>
</Table>
```

### Dependencies

- **React Super Responsive Table**: For mobile-friendly tables.
- **React Router**: For navigation.
- **DeleteAlert**: Integrated for handling deletions.

---

## 5. EnrolledChallengeTeamList Component

### Description

The `EnrolledChallengeTeamList` component is responsible for displaying all teams enrolled in a specific challenge. It organizes players by team and provides details for each player.

### Key Features

- **Team Organization**: Groups players by their respective teams.
- **Leader Identification**: Highlights the team leader.
- **Player Details**: Displays username, gamer ID, invite status, and payment status.
- **Responsive Table**: Ensures data is viewable on various devices.

### Code Snippet

```jsx
<table className="table table-striped">
  <thead>
    <tr>
      <td>Team Name</td>
      <td>Ryvals Username</td>
      {/* Additional columns */}
    </tr>
  </thead>
  <tbody>
    {Object.entries(players).map((item) => (
      item[1].map((player, index) => (
        <tr key={index}>
          {index == 0 && <td rowSpan={item[1].length}>{teamIdNameMap.current[item[0]]}</td>}
          <td>{player.username}</td>
          {/* Additional columns */}
        </tr>
      ))
    ))}
  </tbody>
</table>
```

### Dependencies

- **Reactstrap**: For card and other UI elements.

---

This documentation provides a deep dive into the components used for managing challenges within the application. Each component serves a specific role, and together, they create a robust system for challenge management. 🏆🎮

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

# Documentation for `StandingsTab.jsx`

## Overview
The `StandingsTab.jsx` file is a React component that renders the standings of a tournament. It displays the rankings of teams, the number of kills, and their scores in a tabular format. If the standings are not yet available, it informs the user that the standings are not available.

## Component Details

### Import Statements
- **React**: The core library for building the component.
- **Card, CardBody, Row**: Components from `reactstrap` used for layout and styling.
- **StandingsTable**: A custom component that displays the standings in a table format.

### Component: `StandingsTab`

#### Props
- **standingsDetails**: An array that contains details of the standings such as team rankings, number of kills, and scores.

#### Structure
- The component is wrapped in a `Card` from `reactstrap` for a structured layout.
- Inside the `CardBody`, a `Row` is used to vertically align the content.
- Depending on the content of `standingsDetails`, the component either displays the `StandingsTable` or a message indicating that standings are not available.

#### Conditional Rendering
- **Standings Available**: If `standingsDetails` contains data, it renders the `StandingsTable` component.
- **Standings Not Available**: If `standingsDetails` is empty, it renders a message saying "Standings not available yet".

### Usage
This component is used in a tournament management application to display the current standings based on the data passed to it. It is typically part of a larger interface where users can view various aspects of a tournament.

### Code Example
```jsx
import React from "react";
import { Card, CardBody, Row } from "reactstrap";
import StandingsTable from "../Table/StandingsTable";

const StandingsTab = ({ standingsDetails }) => {
  return (
    <Card className="mb-0">
      <CardBody>
        <Row>
          {standingsDetails?.length === 0 ? (
            <Card className="mb-0">
              <CardBody>
                <Row>Standings not available yet</Row>
              </CardBody>
            </Card>
          ) : (
            <StandingsTable standingsDetails={standingsDetails} />
          )}
        </Row>
      </CardBody>
    </Card>
  );
};

export default StandingsTab;
```

## Key Points
- **Responsive Design**: Utilizes `reactstrap` components to ensure the layout is responsive and consistent with other parts of the application.
- **Conditional Rendering**: Efficiently checks the availability of data before rendering the `StandingsTable`.
- **Reusability**: By using the `StandingsTable` component, the `StandingsTab` promotes reusability and separation of concerns.

This component is crucial for users who need to track the performance and rank of teams in an ongoing or completed tournament. It fits seamlessly into a larger dashboard or detailed view of tournament information.

# Documentation for `TeamsTab.jsx`

## Overview

The `TeamsTab.jsx` file is a React component responsible for displaying a list of teams participating in a tournament. It provides functionality to remove teams if necessary, and it includes details about each team member, such as their email, username, role in the team, invite status, and payment status.

## Components and Functionality

### Imports

- **React** and related hooks: Used for component creation and managing state.
- **reactstrap components**: `Button`, `Modal`: Used for UI elements and modals.
- **RemovePlayerModule**: A component for handling the removal of players from a team.
- **lodash's isEmpty**: Utility to check if objects or arrays are empty.
- **inviteStatus**: A utility to interpret invite status codes.

### State Management

- **`removeId`**: A state variable to store the ID of the team to be removed.
- **`openRemovalModal`**: A boolean state to control the visibility of the removal modal.

### Key Functions

1. **`handleRemove(id)`**: Sets the ID of the team to be removed and opens the modal.
2. **`handleClose()`**: Closes the removal modal.
3. **`handleRecallDetailApi()`**: Calls the API to refresh the tournament details after an action is taken.

### UI Structure

- **Table**: Displays the team details including:
  - Team Name
  - Email
  - Ryvals Username
  - Role (Creator or Member)
  - Invite Status
  - Payment Status
  - Action (Remove button for users with the necessary permissions)

### Conditional Rendering

- **No Teams Enrolled**: Displays a message when no teams are enrolled.
- **Action Button**: Rendered conditionally based on the `changePermission` prop, allowing team removal only if the user has the necessary permissions.

### Modals

- **Removal Modal**: Triggered when the "Remove" button is clicked, allowing the user to confirm the removal of a team.

## Usage

This component is typically used within a tournament management interface where administrators have the capability to manage team enrollments and ensure compliance with tournament rules.

## Code Example

```jsx
// Snippet demonstrating the rendering of a team row
<tbody>
  {isEmpty(details?.participants) ? (
    <tr>
      <td colspan="7">
        <h5 className="text-center my-5">No team enrolled yet</h5>
      </td>
    </tr>
  ) : (
    details?.participants.map((item, index) => {
      return item.players.sort(comparator).map((player, idx) => {
        return (
          <tr key={index}>
            {idx === 0 ? (
              <td rowspan={item.players.length}>
                {item?.name || "N/A"}
              </td>
            ) : null}
            <td>{player?.email || "N/A"}</td>
            <td>{player?.username || "N/A"}</td>
            <td>{player?.leader ? "Creator" : "Member"}</td>
            <td>{inviteStatus[player?.invite]}</td>
            <td>{player?.has_paid ? "Completed" : "Pending"}</td>
            {changePermission ? (
              idx === 0 ? (
                <td rowspan={item.players.length} className="teamName">
                  <Button
                    type="button"
                    color="primary"
                    className="ms-1"
                    onClick={() => handleRemove(player?.team)}
                    disabled={!details.is_team_removable}
                  >
                    Remove
                  </Button>
                </td>
              ) : null
            ) : null}
          </tr>
        );
      });
    })
  )}
</tbody>
```

## Conclusion

The `TeamsTab.jsx` component is an essential part of the tournament management system, providing administrators with an interface to view and manage teams participating in a tournament. Its integration with `RemovePlayerModule` allows for effective team management, ensuring that only valid teams remain in the competition.