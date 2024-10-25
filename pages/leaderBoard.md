# 📜 Documentation for `index.js` - LeaderBoard Component

## 📑 Table of Contents

1. [Introduction](#introduction)
2. [Imports and Dependencies](#imports-and-dependencies)
3. [Component State and Variables](#component-state-and-variables)
4. [Functions and Methods](#functions-and-methods)
5. [Component Structure and Return](#component-structure-and-return)
6. [Usage and Implementation](#usage-and-implementation)
7. [Conclusion](#conclusion)

---

## 🌟 Introduction

The `index.js` file is a **React** component named `LeaderBoard`. This component is designed to display a leaderboard for tournaments. It allows users to select different tournaments and view their standings with features like pagination, dynamic loading (infinite scroll), and filtering based on tournament status.

---

## 📦 Imports and Dependencies

The component relies on several libraries and custom components:

| Library/Component                  | Description                                                                 |
|------------------------------------|-----------------------------------------------------------------------------|
| `React`, `useEffect`, `useState`   | Core React library and hooks for managing component lifecycle and state.    |
| `react-bootstrap`                  | UI components like `Card`, `Col`, and `Row`.                                |
| `Breadcrumbs`                      | Custom component for navigation breadcrumbs.                                |
| `InfiniteScrollDropDown`           | Component for infinite scrolling dropdown to select tournaments.            |
| `bracket_tournaments_api_helper`   | Service functions to fetch leaderboard standings and tournaments.           |
| `Paginator`                        | Custom pagination helper component.                                         |
| `leaderboard.svg`                  | Image asset for the leaderboard.                                            |
| `react-super-responsive-table`     | Responsive table components (`Table`, `Thead`, `Tbody`, `Tr`, `Th`, `Td`).  |
| `reactstrap`                       | Additional UI components like `Dropdown`, `DropdownItem`, etc.              |
| `util`                             | Utility functions for text filtering and options.                           |

---

## 🧩 Component State and Variables

The `LeaderBoard` component utilizes several state variables and constants to manage the UI and data:

- **State Variables:**
  - `selectedTournament`: Holds the current selected tournament ID.
  - `leaderboardData`: Stores the data for the leaderboard.
  - `showLoader`: Boolean to manage the loading spinner.
  - `pageNumber`: Current page number for pagination.
  - `statusFilter`: Boolean to toggle the tournament status dropdown.
  - `selectedDropdownByStatusFilter`: Stores the selected status filter option.
  - `totalCount`: Total count of leaderboard entries for pagination.

- **Constants:**
  - `pageSize`: Number of entries per page for pagination (set to 10).

---

## 🔧 Functions and Methods

- **`updateTournamentId(id)`:** Updates the `selectedTournament` state with the provided ID.
  
- **`handlePageClick(newPageNum)`:** Sets the current page number for the leaderboard pagination.

- **`getLeaderBoardData()`:** An asynchronous function that fetches the leaderboard data based on the current state (pagination, selected tournament). It updates `leaderboardData` and `totalCount` accordingly.

- **`dropdownChangeByStatusFilter(value)`:** Toggles the tournament status filter and resets the page number to 1.

- **`useEffect`:** React hook that triggers the `getLeaderBoardData` function whenever `selectedTournament` or `pageNumber` changes.

---

## 🖼️ Component Structure and Return

The `LeaderBoard` component returns a structured React fragment containing:

1. **Breadcrumbs:** Displays the navigation path with `breadcrumbItem` set to "Leaderboard".

2. **Tournament Selection and Filters:**
   - **Image and Title:** Leaderboard image and title "Leadership Board".
   - **Status Filter Dropdown:** Allows filtering based on tournament status.
   - **Infinite Scroll Dropdown:** For selecting tournaments dynamically.

3. **Leaderboard Table:**
   - Displays the leaderboard data with columns for "Team Name", "Score", and "Kills".
   - Displays a loading spinner when data is being fetched or a message if no data is available.

4. **Pagination:** Utilizes the `Paginator` component to navigate through pages of leaderboard data.

---

## 🚀 Usage and Implementation

To use the `LeaderBoard` component, ensure that all dependencies are installed and configured. The component can be integrated into any existing React project where displaying tournament leaderboards is required.

### Example Usage

```jsx
import LeaderBoard from './path/to/LeaderBoard';

function App() {
  return (
    <div className="App">
      <LeaderBoard />
    </div>
  );
}

export default App;
```

### 🛠️ Customization

- **Styles:** The component uses Bootstrap and custom styles, allowing for easy customization through CSS classes.
- **API Integration:** Ensure that the API services (`getLeaderboardStandings`, `getTournamentsForLeaderBoard`) are properly configured to fetch data.

---

## 📚 Conclusion

The `LeaderBoard` component is a comprehensive UI element for displaying, filtering, and paginating tournament leaderboard data. By leveraging React hooks, responsive design, and dynamic data fetching, it provides a seamless and interactive experience for users looking to track tournament standings.