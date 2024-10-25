# RemovePlayerModule.jsx Documentation 📄

This document provides comprehensive information on the `RemovePlayerModule.jsx` component, explaining its purpose, functionality, and usage.

## Overview 🚀

The **RemovePlayerModule** component is designed as a modal form to facilitate the removal of players or teams from a lobby or tournament. It offers various predefined reasons for removal and allows the entry of a custom reason if needed.

## Table of Contents 📚

1. [Component Structure](#component-structure)
2. [Props](#props)
3. [State Variables](#state-variables)
4. [Functions](#functions)
5. [Form Structure](#form-structure)
6. [Usage Example](#usage-example)

## Component Structure 🏗️

The component leverages several key libraries and components:
- **React**: For component-based structure.
- **reactstrap**: For styled UI components.
- **availity-reactstrap-validation**: For form validation.
- **react-toastify**: For notifications.
- **Modal** elements from `reactstrap`: For displaying the module as a popup.

Here's a snippet of the import statements:

```javascript
import React, { useState } from "react";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import { removeSoloPlayer, removeTeam } from "../../services/lobby_api_helper";
import PropTypes from "prop-types";
import { AvForm, AvCheckboxGroup, AvCheckbox, AvGroup, AvInput, AvFeedback } from "availity-reactstrap-validation";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import { FormGroup, Button, ModalBody, ModalHeader } from "reactstrap";
import { removeTeamFromTournament } from "../../services/bracket_tournaments_api_helper";
```

## Props 🎛️

| Prop Name       | Type     | Description                                                                 |
|-----------------|----------|-----------------------------------------------------------------------------|
| `OnClose`       | function | Callback function to handle modal close action.                              |
| `OnComplete`    | function | Callback function triggered after a player/team is successfully removed.    |
| `callLobbyDetail` | function | Optional callback to refresh lobby details after a change.                   |
| `Mode`          | string   | Indicates whether the operation is for "solo", "team", or "tournament".     |
| `PlayerId`      | string   | ID of the player to be removed.                                             |
| `LobbyId`       | string   | ID of the lobby the player/team is in.                                      |
| `TeamId`        | string   | ID of the team to be removed.                                               |
| `TournamentId`  | string   | ID of the tournament from which the team is to be removed (when in "tournament" mode). |

## State Variables 📊

| State Variable | Type    | Description                                 |
|----------------|---------|---------------------------------------------|
| `showOtherBox` | boolean | Determines if the "Other" reason input box is displayed. |
| `disabled`     | boolean | Determines if the submit button is disabled. |

## Functions ⚙️

- **showOther()**: Toggles the visibility of the "Other" reason input box.
- **handleClose()**: Triggers the `OnClose` prop to close the modal.
- **handleValidSubmit(event, values)**: Handles the form submission, removing a player or team based on the selected reasons and mode.

### handleValidSubmit Logic

Depending on the mode (`solo`, `team`, or `tournament`), it composes the data object with appropriate IDs and reasons. It then calls the respective API helper function to perform the removal action and provides feedback via `react-toastify`.

```javascript
const handleValidSubmit = async (event, values) => {
  setDisabled(true);
  const array = values.ManualReason.length !== 0 ? [...values.MultiReason, values.otherReason] : [...values.MultiReason];

  if (props.Mode === "tournament") {
    let data = { team_id: props.TeamId, reasons: array.toString() };
    // API call for tournament removal
  } else if (props.Mode === "solo") {
    let data = { player_id: props.PlayerId, lobby_id: props.LobbyId, reason: array.toString() };
    // API call for solo player removal
  } else {
    let data = { team_id: props.TeamId, lobby_id: props.LobbyId, reason: array.toString() };
    // API call for team removal
  }
};
```

## Form Structure 📝

The form consists of:

1. **Predefined Reasons**: A series of checkboxes allowing users to select reasons like "Suspicious User", "Cheating", etc.
2. **Other Reason**: An optional text area for entering a custom reason.
3. **Submit Button**: Submits the form after validation checks.

```jsx
<AvForm onValidSubmit={(e, v) => { handleValidSubmit(e, v); }}>
  <AvCheckboxGroup inline name="MultiReason" label="Reasons">
    <div className="d-grid removePLayer">
      <AvCheckbox label="Suspicious User" value="Suspicious User" />
      <AvCheckbox label="Cheating" value="Cheating" />
      <AvCheckbox label="Fraudulent Activity" value="Fraudulent Activity" />
    </div>
  </AvCheckboxGroup>
  <AvCheckboxGroup inline name="ManualReason">
    <AvCheckbox label="Other (Max 50 characters)" value="Other" onClick={() => showOther()} />
  </AvCheckboxGroup>
  {showOtherBox && (
    <AvGroup>
      <AvInput type="textarea" name="otherReason" id="otherReason" placeholder="Type your reasons" required />
      <AvFeedback>Please type your reason</AvFeedback>
    </AvGroup>
  )}
  <FormGroup>
    <Button type="submit" color="primary" disabled={disabled}>
      {disabled && <span className="spinner-border spinner-border-sm mr-4"></span>}
      Submit
    </Button>
  </FormGroup>
</AvForm>
```

## Usage Example 🌟

To use this component, you would typically render it within a modal component, passing in the necessary props for handling player or team removal.

```jsx
<RemovePlayerModule
  Mode="solo"
  PlayerId="12345"
  LobbyId="67890"
  OnClose={() => console.log("Modal closed")}
  OnComplete={() => console.log("Player/Team removed")}
/>
```

## Conclusion 📌

The **RemovePlayerModule** component is a versatile and reusable solution for managing the removal of players or teams from a lobby or tournament setting. It provides a rich user interface with validation, notifications, and a clear structure for managing different modes of operation.

# 📄 LobbyResult.js Documentation

## Overview
The `LobbyResult.js` file is a React component responsible for displaying the results of a gaming lobby. It handles different game types and formats the data accordingly to show various statistics such as kills, winnings, assists, and more. The component is designed to be responsive, utilizing the `reactstrap` and `react-super-responsive-table` libraries for styling and layout.

## Table of Contents
- [Key Features](#key-features)
- [Component Structure](#component-structure)
- [Props](#props)
- [Sorting Logic](#sorting-logic)
- [Rendering Logic](#rendering-logic)
- [Dependencies](#dependencies)

## Key Features
- 📊 Displays detailed statistics for each player/team in a lobby.
- 🏆 Sorts statistics based on different criteria such as winnings or kills.
- 🎮 Supports multiple game types, including Apex Legends and Valorant.
- 🧩 Uses responsive tables for a clean and accessible UI.
- 📈 Handles both tournament and non-tournament data formats.

## Component Structure
The component is structured to render a table of results based on the `props` it receives. The main sections include:
1. **Data Sorting**: Depending on the game type and challenge mode, the data is sorted to highlight key statistics.
2. **Table Rendering**: Conditionally renders tables for different game types and includes specific columns relevant to each game.

## Props
The `LobbyResult` component accepts several props:

| Prop Name  | Type   | Description                                              |
|------------|--------|----------------------------------------------------------|
| `data`     | Array  | An array of player statistics to be displayed.           |
| `type`     | String | Indicates the type of lobby (e.g., "challenge").         |
| `gameData` | Object | Information about the game being played.                 |
| `isTournament` | Boolean | Determines if the lobby is a tournament.            |
| `isPPK`    | Boolean | Indicates if the game format is "Points Per Kill".      |

## Sorting Logic
The component applies different sorting logic based on the game and challenge type:
- **Challenge Mode**: Sorts by `player_winning`.
- **Valorant**: Sorts by `winnings`.
- **Default (e.g., Apex Legends)**: Sorts by `kills`.

This ensures that the most relevant statistics are highlighted for each game type.

## Rendering Logic
The rendering logic is dependent on the `props` and game type:
- For **challenge** type, a table with columns like Team Name, Player Name, Kills, Winnings, etc., is rendered.
- For **Apex Legends** and **Valorant**, specific headers and columns are used based on predefined arrays from `../../helpers/util`.
- For other games, a generic table structure is applied, including survival time and assists.

### Example Table Rendering
```jsx
<table className="table results-table table-striped table-bordered lobbies-table responsiveTable">
  <thead>
    <tr>
      <th>Team Name</th>
      <th>Player Name</th>
      <th>Kills</th>
      <th>Winnings</th>
      <th>Assists</th>
      <th>Damage Dealt</th>
      <th>Survival Time</th>
      <th>Platform</th>
    </tr>
  </thead>
  <tbody>
    {/* Data rows */}
  </tbody>
</table>
```

## Dependencies
- **React**: Core library for building the component.
- **Reactstrap**: Provides Bootstrap components as React components.
- **react-super-responsive-table**: Ensures tables are responsive across different devices.

This component is a key part of the lobby results management, allowing users to see the outcomes of their competitive matches effectively. It is designed to be flexible and accommodate various game types and formats.

# Documentation for `LobbyList.js` 🎮📑

## Overview

The `LobbyList.js` file is a React component that renders a user interface for managing and displaying a list of game lobbies. It allows users to filter, sort, and manage lobbies with various attributes such as game name, lobby status, game type, and more. This component is a crucial part of a gaming platform where users can view and interact with different game lobbies.

## Table of Contents
1. [Imports](#imports)
2. [Component State](#component-state)
3. [Utility Functions](#utility-functions)
4. [Effect Hooks](#effect-hooks)
5. [Render Function](#render-function)
6. [Permissions Handling](#permissions-handling)
7. [Filtering and Sorting](#filtering-and-sorting)
8. [PropTypes](#proptypes)

## Imports

The component utilizes several libraries and components to function:

- **React and Reactstrap**: For building the UI and handling component state.
- **Super Responsive Table**: For rendering responsive tables.
- **React Router**: To handle navigation within the application.
- **React Toastify**: For displaying notifications.
- **Lodash**: For utility functions.
- **Helper Functions and Components**: Such as `Paginator`, `Breadcrumbs`, `ClearButton`, and several API helpers.

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, DropdownToggle, DropdownMenu, Dropdown, DropdownItem } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getLobbyList } from "../../services/lobby_api_helper";
import { getGameList } from "../../services/game_api_helper";
import { Link } from "react-router-dom";
import Paginator from "../../helpers/paginator/paginator";
...
```

## Component State

The component maintains several state variables to keep track of lobbies, filters, sort options, current page, permissions, and loading status.

```javascript
const [lobbies, setLobbies] = useState([]);
const [singlebtn, setSinglebtn] = useState(false);
const [isLoading, setisLoading] = useState(false);
const [totalCount, settotalCount] = useState(null);
const [pageNumber, setpageNumber] = useState(1);
const [sortBy, setsortBy] = useState(null);
const [games, setGames] = useState([]);
const [isUploadingFile, setIsUploadingFile] = useState(false);
...
```

## Utility Functions

### Fetching Data

- `getListing`: Fetches the list of lobbies and games, applying current filters and sort options.

### Filtering and Sorting

- `filterModel`: Constructs the filter model from current filter states.
- `handleSearch`, `dropdownChange`, `dropdownChangeByGameName`, etc.: Handle user interactions for filtering and sorting.

### File Upload

- `uploadCsv`: Handles CSV file uploads for bulk lobby management.

## Effect Hooks

The component uses `useEffect` to fetch data when dependencies change, such as sorting or filtering options.

```javascript
useEffect(() => {
    getListing();
    if (isEmpty(props.permission)) {
        setChange(true);
        setAdd(true);
    } else {
        callSetPermission();
    }
}, [sortBy, searchByGame, pageNumber, searchByLobby, searchByGameType]);
```

## Render Function

The render function constructs the UI, including:

- **Breadcrumbs**: To display the navigation path.
- **Dropdowns**: For sorting and filtering lobbies.
- **Table**: Displays the list of lobbies with details like game name, lobby type, start date, etc.
- **Pagination**: Allows users to navigate through pages of lobbies.
- **Buttons**: For adding new lobbies and uploading files.

```jsx
return (
    <React.Fragment>
        <div className="page-content">
            <Breadcrumbs breadcrumbItem="Manage Lobbies" />
            <Row>
                <Col className="col-12">
                    <Card>
                        <CardBody>
                            <Row className="search-box">
                                <Col className="col-xl-2 col-lg-4 col-md-3 col-sm-3 col-xs-6">
                                    <Dropdown isOpen={singlebtn} toggle={() => setSinglebtn(!singlebtn)}>
                                        <DropdownToggle caret color="primary" className="dropdown-toggle-split sort-by-btn">
                                            <span> {selectedDropdown === null ? "Sort By" : getFilterText(dropdownOptions, selectedDropdown)} </span>
                                            <i className="mdi mdi-chevron-down" />
                                        </DropdownToggle>
                                        <DropdownMenu className="lobbies-menuListing">
                                            {dropdownOptions.map((item, index) => {
                                                return (
                                                    <DropdownItem key={index} onClick={() => dropdownChange(item.value)} dropdownvalue={item.value}>
                                                        {item.text} &nbsp; &nbsp; {selectedDropdown === item.value ? (<i className="mdi mdi-check-circle-outline"></i>) : null}
                                                    </DropdownItem>
                                                );
                                            })}
                                        </DropdownMenu>
                                    </Dropdown>
                                </Col>
                                ...
                            </Row>
                            <div className="table-rep-plugin">
                                <div className="table-responsive mb-0" data-pattern="priority-columns">
                                    <Table id="tech-companies-1" className="table table-striped table-bordered lobbies-table">
                                        <Thead>
                                            <Tr>
                                                <Th>Game Name</Th>
                                                <Th data-priority="1">Lobby Type</Th>
                                                ...
                                            </Tr>
                                        </Thead>
                                        <Tbody>
                                            {isLoading ? (
                                                <div class="spinner-grow transaction-spinner" role="status">
                                                    <span class="sr-only">Loading...</span>
                                                </div>
                                            ) : lobbies.length === 0 ? (
                                                <tr>
                                                    <td colspan="15" className="text-center mt-4"> No Lobbie(s) Found </td>
                                                </tr>
                                            ) : (
                                                lobbies.map((item, index) => (
                                                    <Tr key={index}>
                                                        <Td>{item?.game?.name}</Td>
                                                        <Th>
                                                            <Link to={{ pathname: `/lobby/${item?.id}`, state: { item }, }}>
                                                                {item?.name}
                                                            </Link>
                                                            <br />
                                                            <small>$ {item?.reward}</small>
                                                        </Th>
                                                        ...
                                                    </Tr>
                                                ))
                                            )}
                                        </Tbody>
                                    </Table>
                                </div>
                            </div>
                            <Paginator totalCount={totalCount} pageSize={pageSize} pageClick={handlePageClick} forcePage={pageNumber} />
                        </CardBody>
                    </Card>
                </Col>
            </Row>
        </div>
    </React.Fragment>
);
```

## Permissions Handling

The component checks user permissions to determine which actions are available, such as adding or editing lobbies. It filters permissions based on game types and user roles.

## Filtering and Sorting

The component features dropdowns for filtering the lobby list by game name, lobby type, game type, and status. It also includes sorting options to order lobbies by start date.

## PropTypes

The component expects `props.permission` as input to handle permissions.

```javascript
LobbyList.propTypes = {
    permission: PropTypes.array,
};
```

## Conclusion

The `LobbyList.js` component is a sophisticated part of a gaming platform that facilitates lobby management. It incorporates dynamic filtering, sorting, and permission-based actions to provide a comprehensive interface for users to interact with game lobbies efficiently.

# 📄 Documentation for `FormAndAddTeamToLobby.js`

This documentation provides a detailed explanation of the `FormAndAddTeamToLobby.js` file in a web application. The primary purpose of this file is to facilitate the creation and addition of teams to a lobby within a gaming context.

## 📚 Table of Contents

1. [Overview](#overview)
2. [Key Components](#key-components)
3. [Functionality](#functionality)
4. [Important Functions](#important-functions)
5. [PropTypes](#proptypes)
6. [Styling and Dependencies](#styling-and-dependencies)

## Overview

The `FormAndAddTeamToLobby.js` provides a user interface for forming a new team and adding it to a specific lobby. This component is designed to handle two primary tasks:

- **Search and Add Existing Teams**: It allows users to search for existing teams and add them to the lobby.
- **Create and Add New Teams**: It provides a form to create a new team by selecting team members from a list of users.

The component uses React and various libraries for form validation, UI components, and API interactions.

## Key Components

- **AddTeam Component**: Manages the addition of existing teams to the lobby.
- **FormAndAddTeamToLobby Component**: Handles the creation of new teams and manages the overall UI for lobby interactions.

## Functionality

### AddTeam Component

- **Search Team**: Users can search for teams by name and add them to the lobby.
- **Debounced Search**: Implements a debounced search to reduce API calls while typing.
- **Submit Team**: On form submission, the selected team is added to the lobby.

### FormAndAddTeamToLobby Component

- **Fetch Lobby Details**: Retrieves lobby details to configure the team creation form.
- **Create Team**: Allows users to create a new team by selecting a team name and members.
- **User Search**: Implements a user search to select team members.
- **Submit Team**: Validates and submits the new team to be added to the lobby.

## Important Functions

### `handleSearch(value)`

- **Purpose**: Handles the search functionality for teams.
- **Debounced**: Prevents excessive API calls by delaying execution.
- **API Call**: Calls `getTeams` to fetch teams matching the search query.

### `handleValidAddTeamSubmit(event, values)`

- **Purpose**: Validates and submits the selected team to the lobby.
- **API Interaction**: Uses `addTeamToLobby` to add the team to the lobby.
- **Error Handling**: Displays error messages using `toast` for feedback.

### `handleValidSubmit(event, values)`

- **Purpose**: Validates and submits the newly created team.
- **Team Model**: Constructs a team model with selected members and submits it.
- **Error Handling**: Validates team member selection and handles errors.

## PropTypes

The component does not explicitly define `PropTypes`, but it uses properties from `props` to access the `lobby` details and routing parameters.

## Styling and Dependencies

- **Styling**: Uses Bootstrap for layout and styling, along with custom styles in `lobby.scss`.
- **Dependencies**: Utilizes libraries like `react-toastify`, `reactstrap`, `availity-reactstrap-validation`, and `lodash`.

### External Libraries

- **`react-toastify`**: For notification messages.
- **`react-bootstrap`**: For UI components like `ListGroup`.
- **`lodash`**: Specifically the `debounce` function for optimizing search inputs.
- **`availity-reactstrap-validation`**: Provides validation components for forms.

## Conclusion

The `FormAndAddTeamToLobby.js` is a vital component within the application, enabling users to efficiently manage teams and their integration into lobbies. By leveraging modern React practices and UI libraries, it ensures a smooth user experience in team management. The implementation of debounced searches and form validations enhances its performance and usability.

# Documentation for `EnrolledTeamList.js`

Welcome to the documentation for the `EnrolledTeamList.js` file! This component is a part of a React application and is responsible for managing and displaying the list of enrolled teams in a gaming lobby. It provides functionalities to update, publish, and manage players within each team.

## 📋 Table of Contents

1. [Overview](#-overview)
2. [Key Features](#-key-features)
3. [Component Structure](#-component-structure)
4. [State Management](#-state-management)
5. [Functions and Methods](#-functions-and-methods)
6. [Props](#-props)
7. [External Libraries and Dependencies](#-external-libraries-and-dependencies)
8. [Usage](#-usage)
9. [Contributors](#-contributors)

## 📖 Overview

The `EnrolledTeamList.js` file defines a React functional component that renders a table of teams enrolled in a specific game lobby. It allows users to view team details, update player information, publish team lists, and remove players or teams from the lobby.

## ✨ Key Features

- **Team Display**: Shows a list of enrolled teams with their players.
- **Player Information Update**: Provides a form to update player details such as gamer ID and kills.
- **Multiselect Dropdowns**: Allows selecting players from a list using a dropdown.
- **Publish and Update**: Enables publishing and updating team lists.
- **Remove Functionality**: Offers the ability to remove players or entire teams from the lobby.
- **Responsive Design**: Ensures the table is responsive and user-friendly.

## 🏗️ Component Structure

This component is structured as follows:

- **State Management**: Utilizes React hooks for state management.
- **Rendering**: Renders a responsive table containing team and player details.
- **Event Handling**: Handles events such as form submission and button clicks.

## 🔧 State Management

The component uses various states to manage data:

| State Variable        | Description                                               |
|-----------------------|-----------------------------------------------------------|
| `players`             | Object mapping team IDs to their respective player lists. |
| `loader`              | Boolean indicating loading state during network requests. |
| `playersObj`          | Object for storing player information.                    |
| `teamIdNameMap`       | Ref mapping team IDs to team names.                       |
| `initialPlayersStateRef` | Ref storing initial player state for reset purposes.   |
| `playersOptions`      | Array for available player options in the dropdown.       |
| `manualSelect`        | Array for manually selected players.                      |
| `removeId`            | ID of the player or team to be removed.                   |
| `openRemovalModal`    | Boolean to control the visibility of the removal modal.   |

## 📜 Functions and Methods

### Main Functions

- **`useEffect`**: Initializes player and team data based on `playerList` prop.
- **`checkMultiSelect`**: Handles player selection from the dropdown.
- **`updateList`**: Sends a network request to update the player list.
- **`publishList`**: Sends a network request to publish the player list.
- **`cancelList`**: Resets the player list to its initial state.
- **`addToRefs`**: Adds dropdown elements to refs for easier manipulation.
- **`removeSelectedOptions`**: Filters out already selected player options.
- **`getPlayersList`**: Constructs a list of players based on current selections.
- **`isMatched`**: Checks if a player is already matched in the OCR results.

### Event Handlers

- **`handleRemove`**: Opens a modal to confirm removal of a player or team.
- **`handleClose`**: Closes the removal modal.
- **`handleRecallDetailApi`**: Calls a function to refresh lobby details.

## 📦 Props

The component expects the following props:

| Prop Name         | Type     | Description                                  |
|-------------------|----------|----------------------------------------------|
| `callLobbyDetail` | Function | Function to refresh the lobby details.       |
| `gameType`        | Object   | Object containing game type details.         |
| `playerList`      | Array    | List of players enrolled in the lobby.       |

## 📚 External Libraries and Dependencies

The component leverages several external libraries:

- **React**: Core library for building user interfaces.
- **Reactstrap**: Provides Bootstrap components for React.
- **Multiselect-React-Dropdown**: For multi-select dropdowns.
- **React-Toastify**: For displaying toast notifications.
- **Availity-Reactstrap-Validation**: For form validation.
- **React-Router-Dom**: For navigation and routing.

## 🚀 Usage

To use the `EnrolledTeamList` component, ensure all dependencies are installed and import it into your application. Pass the necessary props as outlined in the Props section.

```jsx
import EnrolledTeamList from './EnrolledTeamList';

// Usage in a parent component
<EnrolledTeamList
  callLobbyDetail={refreshLobbyDetails}
  gameType={gameTypeObject}
  playerList={enrolledPlayers}
/>
```

## 🤝 Contributors

This component is part of a larger project and may have contributions from multiple developers. If you have any questions or suggestions, please refer to the project's main repository for more information.

---

With this documentation, you should have a comprehensive understanding of the `EnrolledTeamList.js` component, its features, and how to integrate it into your application. Happy coding! 🌟

# EnrolledPlayersList.js Documentation 📜

## Table of Contents
1. [Introduction](#introduction-)
2. [Component Overview](#component-overview-)
3. [Key Functionalities](#key-functionalities-)
4. [State Management](#state-management-)
5. [Main Functions](#main-functions)
6. [Props](#props-)
7. [Dependencies](#dependencies-)
8. [Conclusion](#conclusion-)

---

## Introduction 🌟

The **EnrolledPlayersList.js** file is a React component that handles the display and management of enrolled players within a lobby. It provides functionality to view, update, publish, and cancel enrolled players' data, focusing mainly on the integration with player selection and results management.

---

## Component Overview 🚀

The `EnrolledPlayersList` component is designed to manage a list of players enrolled in a particular game lobby. It leverages several React hooks and third-party libraries to offer a seamless and interactive user experience.

### Main Features:
- Display enrolled players in a tabular format.
- Integrate with a multi-select dropdown for player selection.
- Manage player data updates, publishing, and cancellation.
- Allow player removal with modal confirmation.

---

## Key Functionalities 🛠️

1. **Player List Management**: Display players with their gaming details like username, gamer ID, kills, etc.
2. **Multi-select Dropdown**: Integrate a dropdown for selecting players and updating player details.
3. **Publish and Update**: Options to update or publish the list of enrolled players.
4. **Cancel Changes**: Reset changes made to the player selection.
5. **Remove Player Module**: Ability to remove a player through a modal.

---

## State Management 💾

This component manages several state variables using React's `useState` and `useRef` hooks:

- **loader**: Boolean state to manage loading status during async operations.
- **playersObj**: Object that keeps track of the players' data.
- **playersOptions**: Options for the multiselect dropdown.
- **manualSelect**: Array to track manually selected players.
- **PlayersDropDownrefs**: Ref array for managing multiselect dropdown references.
- **initialPlayersStateRef**: Ref that captures the initial state of players for resetting purposes.
- **removeId & openRemovalModal**: State to handle player removal logic.

---

## Main Functions ⚙️

### `useEffect`
- Initializes the players' object based on the provided player list and handles component updates.

### `checkMultiSelect`
- Handles player selection from the multi-select dropdown and updates the state.

### `updateList`
- Prepares and sends an update request for the players' list to the server.

### `publishList`
- Similar to `updateList` but marks the list as published.

### `cancelList`
- Resets the player selections to their initial state.

### `addToRefs`
- Adds dropdown references to the `PlayersDropDownrefs` array.

### `getPlayersList`
- Compiles the list of manually selected players for submission.

### `isMatched`
- Checks if a player ID matches any existing player in the results.

---

## Props 📬

- **callLobbyDetail**: A function prop to refresh or fetch the lobby details after an update.

---

## Dependencies 📦

The component makes use of several libraries and components:

- **React**: Core library for building UI components.
- **PropTypes**: For type-checking of props.
- **Reactstrap**: For Bootstrap styled components.
- **Multiselect React Dropdown**: To handle multi-select dropdowns.
- **Toastify**: For notification alerts.
- **Availity Reactstrap Validation**: For form validation.
- **RemovePlayerModule**: A custom module for handling player removal.

---

## Conclusion 🎉

The **EnrolledPlayersList** component is crucial for managing player enrollments within a game lobby interface. By leveraging robust state management and third-party integrations, it ensures that users can effectively view, update, and manage player data with minimal friction. This component is integral to maintaining accurate and up-to-date player information within the game lobby ecosystem.

---

This documentation provides a comprehensive overview of the `EnrolledPlayersList.js` file, detailing its purpose, functionality, and the technology stack it relies upon.