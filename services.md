# Documentation for `versus_team_api_helper.js`

Welcome to the documentation for the `versus_team_api_helper.js` file. This file contains a set of functions aimed at handling various operations related to managing teams in a gaming lobby environment. 

## Table of Contents
1. [Introduction](#introduction)
2. [Function Documentation](#function-documentation)
    - [addTeamToLobby](#addTeamToLobby)
    - [formNewTeam](#formNewTeam)
    - [getTeams](#getTeams)

---

## Introduction

This file utilizes the `axiosApi` instance to communicate with backend services for managing teams within a gaming lobby context. This includes adding teams to lobbies, forming new teams, and retrieving team information based on specific criteria.

---

## Function Documentation

### 1. `addTeamToLobby`

- **Purpose**: Adds an existing team to a specified lobby.
- **Parameters**: 
  - `model`: An object containing details about the team and the target lobby.
- **Returns**: The result of the API call, which typically includes a confirmation of the team being added to the lobby.
- **Usage**:

```javascript
const teamModel = {
  teamId: "12345",
  lobbyId: "67890",
  // other necessary details
};

addTeamToLobby(teamModel).then(response => {
  console.log("Team added to lobby successfully:", response);
}).catch(error => {
  console.error("Error adding team to lobby:", error);
});
```

### 2. `formNewTeam`

- **Purpose**: Creates a new team for participation in versus matches.
- **Parameters**: 
  - `model`: An object containing information required to form a new team, such as team name and members.
- **Returns**: The result of the API call, usually including details about the newly formed team.
- **Usage**:

```javascript
const newTeamModel = {
  teamName: "Warriors",
  members: ["user1", "user2", "user3"],
  // other necessary details
};

formNewTeam(newTeamModel).then(response => {
  console.log("New team formed successfully:", response);
}).catch(error => {
  console.error("Error forming new team:", error);
});
```

### 3. `getTeams`

- **Purpose**: Retrieves a list of teams based on a name query, game ID, and mode.
- **Parameters**: 
  - `name`: A string representing the team's name or part of it.
  - `game_id`: The identifier of the game for which teams are to be fetched.
  - `mode`: The mode of the game or the team's participation mode.
- **Returns**: A list of teams that match the search criteria.
- **Usage**:

```javascript
const teamName = "Warriors";
const gameId = "00123";
const playMode = "competitive";

getTeams(teamName, gameId, playMode).then(response => {
  console.log("Teams found:", response);
}).catch(error => {
  console.error("Error retrieving teams:", error);
});
```

---

This documentation provides a comprehensive overview of the `versus_team_api_helper.js` file's functionalities, allowing developers to effectively manage team-related operations within their applications. If you have any further questions, please feel free to ask!

# `user_api_helper.js` Documentation 📄

This file provides utility functions for interacting with a user management API. These functions facilitate operations such as retrieving user lists, user details, activating or deactivating users, updating earnings, and generating various reports. The functions leverage `axios` for HTTP requests, ensuring seamless communication with the server.

## Table of Contents
- [Function Overview](#function-overview)
- [Functions](#functions)
  - [getUserList](#getuserlist)
  - [getUserDetail](#getuserdetail)
  - [activateDeactivateUser](#activatedeactivateuser)
  - [seizeWalletOfUser](#seizewalletofuser)
  - [userTransactionHistory](#usertransactionhistory)
  - [seizeWinningAmountOfUser](#seizewinningamountofuser)
  - [releaseWinningOfUser](#releasewinningofuser)
  - [seizeParticularWinningOfUser](#seizeparticularwinningofuser)
  - [changeAdminPassword](#changeadminpassword)
  - [updateEarning](#updateearning)
  - [Reports](#reports)
    - [getCompliantReports](#getcompliantreports)
    - [getUserReports](#getuserreports)
    - [getTransactionReport](#gettransactionreport)
    - [getLobbiesReport](#getlobbiesreport)
    - [getCSV](#getcsv)
  - [Activity Logs](#activity-logs)
    - [getEventList](#geteventlist)
    - [getActivityList](#getactivitylist)
  - [Edit Referral](#edit-referral)
  - [Update Free Lobby Limit](#update-free-lobby-limit)
  - [getUsers](#getusers)

---

## Function Overview

| Function Name                      | Description                                                        |
|------------------------------------|--------------------------------------------------------------------|
| `getUserList`                      | Fetches a paginated list of users with optional filters.           |
| `getUserDetail`                    | Retrieves detailed information about a specific user.              |
| `activateDeactivateUser`           | Activates or deactivates a user account with a specified reason.   |
| `seizeWalletOfUser`                | Locks the user’s wallet to prevent access.                         |
| `userTransactionHistory`           | Fetches the transaction history of a user.                         |
| `seizeWinningAmountOfUser`         | Seizes a specific winning amount from a user.                      |
| `releaseWinningOfUser`             | Releases a seized winning amount back to the user.                 |
| `seizeParticularWinningOfUser`     | Specifically seizes a particular winning amount from the user.     |
| `changeAdminPassword`              | Changes the password for an administrator user.                    |
| `updateEarning`                    | Updates the affiliate earnings for a user.                         |
| `getCompliantReports`              | Fetches complaint reports based on filters.                        |
| `getUserReports`                   | Retrieves user-related reports with filters.                       |
| `getTransactionReport`             | Generates a report for transactions within a date range.           |
| `getLobbiesReport`                 | Fetches lobby-related reports with filters.                        |
| `getCSV`                           | Exports report data to a CSV format.                               |
| `getEventList`                     | Retrieves a list of all event types.                               |
| `getActivityList`                  | Gets a list of user activities based on filters and sorting.       |
| `updateReferral`                   | Updates the referral code for a specific user.                     |
| `updateFreeLobbyLimit`             | Updates the free lobby limit for a user.                           |
| `getUsers`                         | Searches users by name.                                            |

---

## Functions

### `getUserList`

Fetches a list of users, allowing for filtering by search term, sorting options, and pagination controls.

```javascript
export async function getUserList(filterModel) {
    let params = new URLSearchParams();
    if (filterModel.searchTerm && filterModel.searchTerm !== "")
        params.append("query", filterModel.searchTerm);
    if (filterModel.sortBy && filterModel.sortBy !== "")
        params.append("sort_by", filterModel.sortBy);
    if (filterModel.pageNumber) params.append("page", filterModel.pageNumber);
    if (filterModel.pageSize) params.append("page_size", filterModel.pageSize);
    return await axiosApi.get("users/", { params });
}
```

### `getUserDetail`

Retrieves detailed information about a specific user by their `userId`.

```javascript
export async function getUserDetail(userId) {
    return await axiosApi.get(`users/${userId}/`);
}
```

### `activateDeactivateUser`

Activates or deactivates a user's account with a given reason.

```javascript
export async function activateDeactivateUser(userId, activeStatus, reason) {
    return await axiosApi.put(`users/${userId}/change-activation/`, {
        status: activeStatus,
        reason: reason,
    });
}
```

### `seizeWalletOfUser`

Locks the wallet of a user to prevent access.

```javascript
export async function seizeWalletOfUser(userId) {
    return await axiosApi.put(`seize-money/${userId}/`);
}
```

### `userTransactionHistory`

Fetches the transaction history for a specific user, with pagination options.

```javascript
export async function userTransactionHistory(userId, pageNumber, pageSize) {
    let params = new URLSearchParams();
    if (pageNumber) params.append("page", pageNumber);
    if (pageSize) params.append("page_size", pageSize);
    return await axiosApi.get(`users/${userId}/transaction-history/`, { params })
        .then((response) => {
            return { data: response.results, total: response.total };
        });
}
```

### `seizeWinningAmountOfUser`

Seizes a specific winning amount from a user by transaction ID.

```javascript
export async function seizeWinningAmountOfUser(userId, transactionId) {
    return await axiosApi.put(`seize-money/${userId}/`, { transactionId: transactionId });
}
```

### `releaseWinningOfUser`

Releases a previously seized winning amount back to the user.

```javascript
export async function releaseWinningOfUser(userId, transactionId) {
    return await axiosApi.put(`users/${userId}/transaction-status`, { transaction_id: transactionId });
}
```

### `seizeParticularWinningOfUser`

Seizes a particular winning amount from a user by transaction ID.

```javascript
export async function seizeParticularWinningOfUser(userId, transactionId) {
    return await axiosApi.put(`seize-money/${userId}/`, { transaction_id: transactionId });
}
```

### `changeAdminPassword`

Allows an administrator to change their password.

```javascript
export async function changeAdminPassword(model) {
    return await axiosApi.put(`/change-password/`, model);
}
```

### `updateEarning`

Updates the earnings for a user based on affiliate days.

```javascript
export async function updateEarning(userId, model) {
    return await axiosApi.put(`users/affiliate-days/${userId}/`, model);
}
```

### Reports

#### `getCompliantReports`

Fetches complaint reports based on the provided filters.

```javascript
export async function getCompliantReports(filterModel) {
    let params = new URLSearchParams();
    if (filterModel.from_date) params.append("from_date", filterModel.from_date);
    if (filterModel.to_date) params.append("to_date", filterModel.to_date);
    if (filterModel.page_size) params.append("page_size", filterModel.page_size);
    if (filterModel.page) params.append("page", filterModel.page);
    if (filterModel.type && filterModel.type != 0) params.append("type", filterModel.type);
    return await axiosApi.get("report/complaints/", { params });
}
```

#### `getUserReports`

Retrieves user-related reports with specified filters.

```javascript
export async function getUserReports(filterModel) {
    let params = new URLSearchParams();
    if (filterModel.from_date) params.append("from_date", filterModel.from_date);
    if (filterModel.to_date) params.append("to_date", filterModel.to_date);
    if (filterModel.page_size) params.append("page_size", filterModel.page_size);
    if (filterModel.page) params.append("page", filterModel.page);
    if (filterModel.type && filterModel.type != 0) params.append("type", filterModel.type);
    return await axiosApi.get("report/users/", { params });
}
```

#### `getTransactionReport`

Generates a transaction report within a specified date range.

```javascript
export async function getTransactionReport({ from_date, to_date, page_size, type, page, }) {
    let params = new URLSearchParams();
    if (from_date) params.append("from_date", from_date);
    if (to_date) params.append("to_date", to_date);
    if (page_size) params.append("page_size", page_size);
    if (type) params.append("type", type);
    if (page) params.append("page", page);
    return await axiosApi.get(`reports/transactions/`, { params });
}
```

#### `getLobbiesReport`

Fetches lobby-related reports with specified filters.

```javascript
export async function getLobbiesReport({ from_date, to_date, page_size, type, page, }) {
    let params = new URLSearchParams();
    if (from_date) params.append("from_date", from_date);
    if (to_date) params.append("to_date", to_date);
    if (page_size) params.append("page_size", page_size);
    if (type) params.append("type", type);
    if (page) params.append("page", page);
    return await axiosApi.get(`report/lobby/`, { params });
}
```

#### `getCSV`

Exports report data to a CSV format based on provided filters.

```javascript
export async function getCSV({ from_date, to_date, report, type }) {
    let params = new URLSearchParams();
    if (from_date) params.append("from_date", from_date);
    if (to_date) params.append("to_date", to_date);
    if (report) params.append("report", report);
    if (type) params.append("type", type);
    if (report === "transactions") params.append("page_size", 0);
    return await axiosApi.get(`report/export-csv/`, { params });
}
```

### Activity Logs

#### `getEventList`

Retrieves a list of all available event types.

```javascript
export async function getEventList() {
    return await axiosApi.get(`events/`);
}
```

#### `getActivityList`

Fetches a list of user activities with optional filters for events, dates, and sorting.

```javascript
export async function getActivityList({ event, from_date, to_date, type, page, page_size, sortBy, }) {
    let params = new URLSearchParams();
    if (sortBy && sortBy !== "")
        params.append(
            sortBy === "create_date" || sortBy === "-create_date" ? "date" : "order",
            sortBy
        );
    if (type.length != 0) params.append("type", `${type},`);
    if (event.length != 0) params.append("event", `${event},`);
    if (from_date) params.append("from_date", from_date);
    if (to_date) params.append("to_date", to_date);
    if (page) params.append("page", page);
    if (page_size) params.append("page_size", page_size);
    return await axiosApi.get("logs/", { params })
        .then((response) => {
            return { data: response.results, total: response.total };
        });
}
```

### Edit Referral

Updates the referral code for a specific user.

```javascript
export async function updateReferral(userId, model) {
    return await axiosApi.put(`users/referral-code/${userId}/`, model);
}
```

### Update Free Lobby Limit

Updates the free lobby limit for a specific user.

```javascript
export async function updateFreeLobbyLimit(userId, model) {
    return await axiosApi.put(`users/free-lobby-limit/${userId}/`, model);
}
```

### `getUsers`

Searches for users by a given name, returning matched usernames.

```javascript
export async function getUsers(name) {
    const url = `users/usernames/?name=${name}`;
    return await axiosApi.get(url);
}
```

---

This documentation provides a comprehensive overview of the `user_api_helper.js` file, detailing each function, its purpose, and how to use it within your project. If you have any questions about specific implementations or need further clarification, feel free to reach out. Happy coding! 🎉

# `referral_api_helper.js` Documentation 📘

This documentation provides an overview of the utility functions defined in the `referral_api_helper.js` file. These functions are primarily used to interact with the referral-related endpoints of an API. 

---

## Table of Contents

1. [Overview](#overview)
2. [Functions](#functions)
   - [getReferralList](#getreferrallist)
   - [getReferralDetail](#getreferraldetail)
3. [Dependencies](#dependencies)

---

## Overview

The `referral_api_helper.js` file contains API helper functions that allow for the fetching of referral lists and referral details for specific users. These functions handle constructing the required HTTP requests and parsing the responses received from the server.

## Functions

The following functions are available in this file:

### `getReferralList`

- **Purpose**: To retrieve a list of referrals.
- **Parameters**: 
  - `filterModel`: An object used to filter the referral list. It may contain properties like `searchTerm`, `sortBy`, `pageNumber`, `pageSize`, `from_date`, and `to_date`.
- **Returns**: A promise that resolves to an object containing:
  - `data`: The results array from the API response.
  - `total`: The total number of referrals.
  - `total_money_distributed`: Total money distributed through referrals.
  - `daily_money_given`: Money given out daily.
  - `current_month_given`: Money given out in the current month.
- **Usage**:
  ```javascript
  const filterModel = {
    searchTerm: "John",
    sortBy: "name",
    pageNumber: 1,
    pageSize: 10,
    from_date: "2023-01-01",
    to_date: "2023-12-31"
  };
  getReferralList(filterModel).then((referralData) => {
    console.log(referralData);
  });
  ```

### `getReferralDetail`

- **Purpose**: To fetch detailed information for a specific referral user.
- **Parameters**:
  - `userId`: The unique identifier for the user whose referral details are being requested.
- **Returns**: A promise that resolves to the referral details of the specified user.
- **Usage**:
  ```javascript
  const userId = 123;
  getReferralDetail(userId).then((referralDetail) => {
    console.log(referralDetail);
  });
  ```

## Dependencies

This file relies on the following dependencies:

- **axiosApi**: An Axios instance configured with interceptors for handling requests and responses, imported from the `index.js` file.

---

This documentation should provide a comprehensive understanding of the `referral_api_helper.js` file and how to use its functions to interact with referral-related API endpoints. 

Feel free to reach out if you have any questions or need further clarification! 😊

# Documentation for `lobby_api_helper.js` 📚

This documentation provides an overview and explanation of the `lobby_api_helper.js` file, which contains a series of functions designed to interact with the lobby-related API endpoints. These functions allow you to perform CRUD operations and manage lobbies within the application.

## Table of Contents
1. [Functions Overview](#functions-overview)
2. [Function Details](#function-details)
   - [getLobbyList](#getlobbylist)
   - [getLobbyDetail](#getlobbydetail)
   - [deleteLobby](#deletelobby)
   - [overrideLobby](#overridelobby)
   - [addLobby](#addlobby)
   - [editLobby](#editlobby)
   - [changeStatusLobby](#changestatuslobby)
   - [sendImageCount](#sendimagecount)
   - [sendUpdateList](#sendupdatelist)
   - [sendPublishList](#sendpublishlist)
   - [removeSoloPlayer](#removesoloplayer)
   - [removeTeam](#removeteam)
   - [fetchStats](#fetchstats)
   - [cancelLobby](#cancellobby)

---

## Functions Overview

The `lobby_api_helper.js` file includes the following functions:

| Function Name       | Description                                                   |
|---------------------|---------------------------------------------------------------|
| `getLobbyList`      | Retrieves a list of lobbies based on filters.                 |
| `getLobbyDetail`    | Fetches detailed information about a specific lobby.          |
| `deleteLobby`       | Deletes a specific lobby.                                     |
| `overrideLobby`     | Overrides the start of a specific lobby.                      |
| `addLobby`          | Adds a new lobby.                                             |
| `editLobby`         | Edits the details of an existing lobby.                       |
| `changeStatusLobby` | Changes the activation status of a lobby.                     |
| `sendImageCount`    | Sends an update for the number of images associated with a lobby. |
| `sendUpdateList`    | Sends an updated list of stats for a lobby.                   |
| `sendPublishList`   | Publishes the list of stats for a lobby.                      |
| `removeSoloPlayer`  | Removes a solo player from a lobby.                           |
| `removeTeam`        | Removes a team from a lobby.                                  |
| `fetchStats`        | Fetches stats for a lobby.                                    |
| `cancelLobby`       | Cancels a lobby.                                              |

---

## Function Details

### `getLobbyList`

```javascript
export async function getLobbyList(filterModel)
```

This function retrieves a list of lobbies based on various filters provided in `filterModel`. The filters include sorting options, date range, game filters, pagination, and lobby type.

- **Parameters**: 
  - `filterModel`: An object containing filters such as sortBy, dateTo, dateFrom, gameFilter, pageSize, pageNumber, lobbyFilter, and gameType.
- **Returns**: A promise resolving to the API response containing the list of lobbies.

### `getLobbyDetail`

```javascript
export async function getLobbyDetail(lobbyId)
```

Fetches detailed information about a specific lobby by its ID.

- **Parameters**:
  - `lobbyId`: The ID of the lobby to retrieve.
- **Returns**: A promise resolving to the detailed information of the lobby.

### `deleteLobby`

```javascript
export async function deleteLobby(lobbyId)
```

Deletes a specific lobby identified by its ID.

- **Parameters**:
  - `lobbyId`: The ID of the lobby to delete.
- **Returns**: A promise indicating the success or failure of the operation.

### `overrideLobby`

```javascript
export async function overrideLobby(lobbyId)
```

Overrides the start of a specific lobby, potentially used to manually start a lobby.

- **Parameters**:
  - `lobbyId`: The ID of the lobby to override.
- **Returns**: A promise indicating the success or failure of the operation.

### `addLobby`

```javascript
export async function addLobby(model)
```

Adds a new lobby based on the provided model.

- **Parameters**:
  - `model`: An object containing the details of the new lobby.
- **Returns**: A promise resolving to the API response after adding the lobby.

### `editLobby`

```javascript
export async function editLobby(lobbyId, model)
```

Edits the details of an existing lobby identified by its ID.

- **Parameters**:
  - `lobbyId`: The ID of the lobby to edit.
  - `model`: An object containing the updated details of the lobby.
- **Returns**: A promise indicating the success or failure of the update.

### `changeStatusLobby`

```javascript
export async function changeStatusLobby(lobbyId, lobbyStatus)
```

Changes the activation status of a lobby.

- **Parameters**:
  - `lobbyId`: The ID of the lobby to change status.
  - `lobbyStatus`: The new status of the lobby.
- **Returns**: A promise indicating the success or failure of the status change.

### `sendImageCount`

```javascript
export async function sendImageCount(data, lobbyId)
```

Sends an update for the number of images associated with a lobby.

- **Parameters**:
  - `data`: The data containing the image count.
  - `lobbyId`: The ID of the lobby to update.
- **Returns**: A promise indicating the success or failure of the update.

### `sendUpdateList`

```javascript
export async function sendUpdateList(data, lobbyId)
```

Sends an updated list of stats for a lobby.

- **Parameters**:
  - `data`: The data containing the updated stats.
  - `lobbyId`: The ID of the lobby to update.
- **Returns**: A promise indicating the success or failure of the update.

### `sendPublishList`

```javascript
export async function sendPublishList(data, lobbyId)
```

Publishes the list of stats for a lobby.

- **Parameters**:
  - `data`: The data containing the stats to publish.
  - `lobbyId`: The ID of the lobby to publish.
- **Returns**: A promise indicating the success or failure of the publish operation.

### `removeSoloPlayer`

```javascript
export async function removeSoloPlayer(data)
```

Removes a solo player from a lobby.

- **Parameters**:
  - `data`: The data containing the information of the player to remove.
- **Returns**: A promise indicating the success or failure of the removal.

### `removeTeam`

```javascript
export async function removeTeam(data)
```

Removes a team from a lobby.

- **Parameters**:
  - `data`: The data containing the information of the team to remove.
- **Returns**: A promise indicating the success or failure of the removal.

### `fetchStats`

```javascript
export async function fetchStats(model)
```

Fetches stats for a lobby.

- **Parameters**:
  - `model`: An object containing the parameters for fetching stats.
- **Returns**: A promise resolving to the fetched stats.

### `cancelLobby`

```javascript
export async function cancelLobby(model)
```

Cancels a lobby based on the provided model.

- **Parameters**:
  - `model`: An object containing the details of the lobby to cancel.
- **Returns**: A promise indicating the success or failure of the cancellation.

---

This comprehensive set of functions allows for effective management and operation of lobbies within the application, enabling users to perform a wide range of actions programmatically.

# Documentation for `index.js`

Welcome to the documentation for the **`index.js`** file, a core component of our API helper utilities. This file is responsible for configuring the Axios instance used throughout our application for making HTTP requests. It also manages authentication headers and token refresh logic.

---

## Table of Contents

- [Overview](#overview)
- [Axios Configuration](#axios-configuration)
- [Request Interceptors](#request-interceptors)
- [Response Interceptors](#response-interceptors)
- [Token Refresh Logic](#token-refresh-logic)
- [Exports](#exports)

---

## Overview

This file is crucial for setting up the Axios instance with a base URL, handling authentication headers, and managing request-response interceptors to streamline API interactions. Additionally, it includes logic for handling token refresh to ensure seamless user authentication.

---

## Axios Configuration

```javascript
import axios from "axios";
import authHeader from "../helpers/jwt-token-access/authHeader";
import { toast } from "react-toastify";
import toastrOptions from "../helpers/toastr-options/toastr-options";

const API_URL = process.env.REACT_APP_APIURL;

export const axiosApi = axios.create({
  baseURL: API_URL,
});
```

The Axios instance `axiosApi` is created with a base URL extracted from environment variables, ensuring that all requests are directed to the correct server endpoint.

---

## Request Interceptors

The request interceptor is set up to automatically append the `Authorization` header to each request using a JWT token from the `authHeader` function.

```javascript
axiosApi.interceptors.request.use(
  (config) => {
    config.headers["Authorization"] = authHeader();
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);
```

This functionality ensures that all API requests are authenticated without needing to manually attach the token each time.

---

## Response Interceptors

The response interceptor handles various response status codes, including token refresh logic and error handling.

### Status Code Handling

- **500 Internal Server Error**: Displays a toast error message and logs the user out if the error occurs during token refresh.
- **401 Unauthorized**: Triggers token refresh logic to obtain a new access token.

```javascript
let isRefreshing = false;
let failedQueue = [];

axiosApi.interceptors.response.use(
  (response) => response.data,
  async (error) => {
    let errStatus = error?.response?.status;
    const originalRequest = error.config;

    if (errStatus === 500) {
      handleInternalServerError(error, originalRequest);
    } else if (errStatus === 401) {
      handleUnauthorizedError(error, originalRequest);
    } else {
      handleOtherErrors(error);
    }
  }
);
```

### Error Handling

For other errors, it processes the response data to extract and display error messages using `toast`.

---

## Token Refresh Logic

The token refresh logic is critical for maintaining user sessions without requiring frequent logins.

### Token Refresh Functions

- **`subscribeTokenRefresh(cb)`**: Adds a callback to a queue to be called once a new token is obtained.
- **`onRrefreshed(accessToken)`**: Executes all queued callbacks with the new access token.

### Refresh Flow

When a 401 error occurs, it triggers the `refershTokenUpdate()` function to refresh the tokens and retries the original request with the new token.

```javascript
export async function refershTokenUpdate() {
  const url = process.env.REACT_APP_BASEURL + `accounts/token/`;
  const obj = JSON.parse(localStorage.getItem("authUser"));
  let body = {
    refresh_token: obj.extras.refresh_token,
    access_token: obj.extras.access_token,
  };
  let headers = {
    "Content-Type": "application/json",
  };
  return await axiosApi.post(url, body, { headers });
}
```

---

## Exports

- **`axiosApi`**: The Axios instance configured with interceptors.
- **`refershTokenUpdate()`**: A function to refresh JWT tokens.

---

This documentation provides comprehensive coverage of the `index.js` file's functionality, offering insights into its configuration and error-handling mechanisms. By understanding these components, developers can effectively manage API requests and ensure a seamless user experience.

# Documentation for `group_api_helper.js` 📄

This file provides helper functions to interact with the Group and Admin User APIs. It primarily deals with managing groups and admin users, including retrieving lists, adding, editing, and deleting entities. The interactions are implemented using the `axiosApi` instance configured in the `index.js`.

## Table of Contents 📚

1. [Overview](#overview)
2. [API Methods](#api-methods)
    - [Get Group List](#get-group-list)
    - [Get Admin User Detail](#get-admin-user-detail)
    - [Add/Edit Admin User](#addedit-admin-user)
    - [Change Admin Status](#change-admin-status)
    - [Get Group Lists](#get-group-lists)
    - [Get Permission Lists](#get-permission-lists)
    - [Get Staff Detail by ID](#get-staff-detail-by-id)
    - [Delete Admin](#delete-admin)
3. [Error Handling](#error-handling)
4. [Dependencies](#dependencies)

## Overview

The `group_api_helper.js` file is designed to assist with operations related to groups and admin users within an application. The file includes methods for retrieving lists, details, and performing CRUD operations. It utilizes the `axiosApi` instance for making HTTP requests and includes token management via the `setToken` function.

## API Methods

### Get Group List

**Function**: `getGroupList()`

Retrieves a list of groups. The function sets the token for authentication and then makes a GET request to fetch the group data.

```javascript
export async function getGroupList() {
    setToken();
    return await axiosApi.get("groups/").then((response) => {
        return { data: response };
    });
}
```

### Get Admin User Detail

**Function**: `getAdminUserDetail(userId)`

Fetches the details of a specific admin user by their `userId`.

```javascript
export async function getAdminUserDetail(userId) {
    setToken();
    return await axiosApi.get(`staff/${userId}/`);
}
```

### Add/Edit Admin User

**Function**: `addeditAdminUser(model, mode, adminId)`

Adds a new admin user or edits an existing one. If `mode` is true, it edits the user; otherwise, it adds a new user.

```javascript
export async function addeditAdminUser(model, mode, adminId) {
    setToken();
    if (mode) {
        return await axiosApi.put(`staff/${adminId}/`, model);
    } else {
        return await axiosApi.post(`staff/`, model);
    }
}
```

### Change Admin Status

**Function**: `changeAdminStatus(userId, activeStatus)`

Updates the status of an admin user, setting them as active or inactive based on `activeStatus`.

```javascript
export async function changeAdminStatus(userId, activeStatus) {
    setToken();
    return await axiosApi.put(`staff/${userId}/update-status/`, { status: activeStatus });
}
```

### Get Group Lists

**Function**: `getGroupLists()`

Retrieves a comprehensive list of groups, similar to `getGroupList`.

```javascript
export async function getGroupLists() {
    setToken();
    return await axiosApi.get("groups/");
}
```

### Get Permission Lists

**Function**: `getPermissionLists()`

Fetches the list of permissions available for staff members.

```javascript
export async function getPermissionLists() {
    setToken();
    return await axiosApi.get("staff-permissions/");
}
```

### Get Staff Detail by ID

**Function**: `getStaffDetailByID(adminId)`

Retrieves the details of a staff member using their `adminId`.

```javascript
export async function getStaffDetailByID(adminId) {
    setToken();
    return await axiosApi.get(`staff/${adminId}/`);
}
```

### Delete Admin

**Function**: `deleteAdmin(id)`

Deletes an admin user based on their `id`.

```javascript
export async function deleteAdmin(id) {
    setToken();
    return await axiosApi.delete(`staff/${id}/`);
}
```

## Error Handling

The file leverages promise-based error handling with `.then()` and `.catch()` methods to manage responses and errors from API requests. This ensures that any issues with the API calls are appropriately managed and can be logged or displayed using toast notifications.

## Dependencies

- **axiosApi**: Custom axios instance for HTTP requests.
- **setToken**: Function to set authentication tokens in request headers.
- **react-toastify**: Provides toast notifications for user feedback.
- **toastr-options**: Configuration for toastr notifications.

With these methods, developers can efficiently manage groups and admin users within their applications, ensuring robust backend communication and user management. 🌟

# Global Settings API Helper Documentation

The `globalSettings_api_helper.js` file is a module that provides helper functions to interact with the global settings API of an application. These helper functions utilize Axios to send HTTP requests to the server to retrieve or update global application settings.

## Table of Contents
- [Overview](#overview)
- [Functions](#functions)
  - [getGlobalSettings](#getglobalsettings)
  - [setGlobalSettings](#setglobalsettings)

## Overview

This module provides two primary functions to interact with the global settings of the application. It uses `axiosApi`, which is an instance of Axios configured to communicate with the API. The functions are designed to handle HTTP GET and PUT requests.

## Functions

### getGlobalSettings

🔍 **Purpose:**  
Retrieve the current global settings from the server.

📥 **Parameters:**  
None.

📤 **Returns:**  
A promise that resolves to the response of the GET request. The response contains the current global settings data.

💻 **Usage:**

```javascript
import { getGlobalSettings } from './globalSettings_api_helper';

async function fetchSettings() {
  try {
    const settings = await getGlobalSettings();
    console.log('Current Global Settings:', settings);
  } catch (error) {
    console.error('Error fetching global settings:', error);
  }
}

fetchSettings();
```

### setGlobalSettings

🔄 **Purpose:**  
Update the global settings on the server with new data.

📥 **Parameters:**  
- `model` (Object): An object containing the settings data to be updated.

📤 **Returns:**  
A promise that resolves to the response of the PUT request. This response indicates the success or failure of the update operation.

💻 **Usage:**

```javascript
import { setGlobalSettings } from './globalSettings_api_helper';

async function updateSettings(newSettings) {
  try {
    const response = await setGlobalSettings(newSettings);
    console.log('Settings updated successfully:', response);
  } catch (error) {
    console.error('Error updating settings:', error);
  }
}

const newSettings = {
  theme: 'dark',
  notificationsEnabled: true,
};

updateSettings(newSettings);
```

## Conclusion

The `globalSettings_api_helper.js` file provides essential functions to manage global settings within an application. By using these functions, developers can easily retrieve and update settings, ensuring that they reflect the current state and preferences of the application. With these utilities, maintaining and configuring global settings becomes a streamlined process.

# Documentation for `game_api_helper.js` 📚🎮

The `game_api_helper.js` file is a JavaScript module designed to interface with a gaming-related API. It provides functions to perform various operations related to games, such as retrieving game information and updating game data.

## Table of Contents

1. [Setup and Imports](#setup-and-imports)
2. [Functions Overview](#functions-overview)
   - [getGameList](#getGameList)
   - [updateGameData](#updateGameData)
   - [getGameBySlug](#getGameBySlug)
3. [Usage](#usage)

### Setup and Imports

```javascript
import { axiosApi } from "./index";
```

The file imports the `axiosApi` instance from the `index.js` file. This instance is used to make HTTP requests to the API.

### Functions Overview

#### 1. `getGameList`

```javascript
export async function getGameList(searchTerm = null) {
    let params = new URLSearchParams();
    if (searchTerm) params.append("name", searchTerm);
    return await axiosApi.get("games/", { params });
}
```

- **Purpose**: Fetches a list of games from the API, optionally filtered by a search term.
- **Parameters**:
  - `searchTerm` (optional): A string used to filter the games by name.
- **Returns**: A promise that resolves to the API response containing the list of games.

#### 2. `updateGameData`

```javascript
export async function updateGameData(model, id) {
    return await axiosApi.put(`game-update/${id}/`, model);
}
```

- **Purpose**: Updates the data of a specific game by its ID.
- **Parameters**:
  - `model`: An object containing the game data to be updated.
  - `id`: The unique identifier of the game to be updated.
- **Returns**: A promise that resolves to the API response after updating the game data.

#### 3. `getGameBySlug`

```javascript
export async function getGameBySlug(slug) {
    return await axiosApi.get(`games/${slug}/`);
}
```

- **Purpose**: Retrieves detailed information about a specific game using its slug.
- **Parameters**:
  - `slug`: A unique string identifier used to retrieve the game details.
- **Returns**: A promise that resolves to the API response containing the game details.

### Usage

To use any of these functions, you would typically import them into your application code and call them with the appropriate parameters. Below is an example usage of the `getGameList` function:

```javascript
import { getGameList } from './game_api_helper';

async function fetchGames(searchTerm) {
    try {
        const response = await getGameList(searchTerm);
        console.log('Games:', response.data);
    } catch (error) {
        console.error('Error fetching games:', error);
    }
}

fetchGames('Super Mario');
```

In this example, `fetchGames` is an asynchronous function that calls `getGameList` with a search term and logs the list of games to the console. The same pattern can be followed for other functions like `updateGameData` and `getGameBySlug`.

This module provides a clear and concise interface for interacting with the game-related API, making it easier to manage game data within an application.

# Documentation for `demo_api_helper.js` 📄

This document provides a detailed explanation of the `demo_api_helper.js` file, which is used to manage the game demo functionalities via API calls. The file primarily uses the `axiosApi` instance to make HTTP requests to a backend service. Below is a breakdown of the functions available in this file:

## Table of Contents 📚

- [Functions Overview](#functions-overview)
  - [getDemoList](#getdemolist)
  - [getPinnedList](#getpinnedlist)
  - [addDemoPage](#adddemopage)
  - [deleteSelectedDemoApi](#deleteselecteddemoapi)
  - [updateDemoPagePinStatus](#updatedemopagepinstatus)
  - [getEditDemoDataById](#geteditdemodatabyid)
  - [editDemoPage](#editdemopage)

## Functions Overview 📜

### getDemoList

```javascript
export async function getDemoList(filterModel)
```

**Description**: Fetches a list of game demos based on the provided filters.

- **Parameters**: 
  - `filterModel`: An object containing filter criteria such as `gameFilter`, `pageSize`, and `pageNumber`.
  
- **Returns**: An object containing the `data` array of demos and the `total` count of demos.

- **Usage**:
  ```javascript
  const filterModel = { gameFilter: 'action', pageSize: 10, pageNumber: 1 };
  const demoList = await getDemoList(filterModel);
  ```

### getPinnedList

```javascript
export async function getPinnedList()
```

**Description**: Retrieves a list of pinned game demos.

- **Parameters**: None
- **Returns**: A list of pinned game demos.
  
- **Usage**:
  ```javascript
  const pinnedDemos = await getPinnedList();
  ```

### addDemoPage

```javascript
export async function addDemoPage(model)
```

**Description**: Adds a new demo page with the provided data model.

- **Parameters**: 
  - `model`: An object containing the data of the new demo page to be added.
  
- **Returns**: The response from the server after adding the demo page.

- **Usage**:
  ```javascript
  const newDemo = { title: 'New Game', description: 'Exciting new game demo' };
  const response = await addDemoPage(newDemo);
  ```

### deleteSelectedDemoApi

```javascript
export async function deleteSelectedDemoApi(delId)
```

**Description**: Deletes a specific demo page identified by the given ID.

- **Parameters**: 
  - `delId`: The ID of the demo page to be deleted.
  
- **Returns**: The response from the server after attempting to delete the demo.

- **Usage**:
  ```javascript
  const demoId = 123;
  const response = await deleteSelectedDemoApi(demoId);
  ```

### updateDemoPagePinStatus

```javascript
export async function updateDemoPagePinStatus(game_id, model)
```

**Description**: Updates the pin status of a demo page.

- **Parameters**: 
  - `game_id`: The ID of the game demo.
  - `model`: An object containing the updated pin status.
  
- **Returns**: The response from the server after updating the pin status.

- **Usage**:
  ```javascript
  const gameId = 456;
  const pinStatusUpdate = { pinned: true };
  const response = await updateDemoPagePinStatus(gameId, pinStatusUpdate);
  ```

### getEditDemoDataById

```javascript
export async function getEditDemoDataById(id)
```

**Description**: Fetches the data of a specific demo by its ID for editing purposes.

- **Parameters**: 
  - `id`: The ID of the demo to be fetched.
  
- **Returns**: The demo data for the specified ID.

- **Usage**:
  ```javascript
  const demoId = 789;
  const demoData = await getEditDemoDataById(demoId);
  ```

### editDemoPage

```javascript
export async function editDemoPage(model)
```

**Description**: Edits an existing demo page with the provided data model.

- **Parameters**: 
  - `model`: An object containing the updated data for the demo page.
  
- **Returns**: The response from the server after editing the demo page.

- **Usage**:
  ```javascript
  const updatedDemo = { id: 789, title: 'Updated Game', description: 'Updated description for the game demo' };
  const response = await editDemoPage(updatedDemo);
  ```

---

This file provides an API interface to handle CRUD operations for game demos, which includes listing demos, adding new ones, deleting, and editing existing demos. These functions facilitate seamless interaction with the backend for demo management.

# File Upload API Helper Documentation

## Overview
The `file_upload_api_helper.js` script is designed to handle file uploads through an API endpoint. It provides a simple interface to upload bulk files to a server using HTTP POST requests. This functionality is often used in applications where large amounts of data or various files need to be uploaded simultaneously for processing or storage.

## Functions

### `uploadBulkFileUpload`

This function is responsible for uploading files in bulk to a specified endpoint.

#### Function Signature

```javascript
export async function uploadBulkFileUpload(model)
```

#### Parameters

- **model**: The data model containing the files and any additional metadata required for the upload. Typically, this would include file objects and possibly other relevant information that needs to accompany the files.

#### Returns

- A promise that resolves to the response from the server after attempting to upload the files. The response will generally contain information about the success or failure of the upload operation.

#### Usage

```javascript
// Assuming you have a model with the necessary files and metadata
const model = {
  files: [file1, file2, ...],
  metadata: { ... }
};

uploadBulkFileUpload(model)
  .then(response => {
    console.log("Files uploaded successfully:", response);
  })
  .catch(error => {
    console.error("Error uploading files:", error);
  });
```

## Dependencies

- **axiosApi**: This utility is used to make HTTP POST requests. It is imported from the `index.js` file, which likely contains the configuration for the Axios instance including base URL and any necessary headers.

## API Endpoint

- **Endpoint**: `file-uploads/upload/`
  - This endpoint is responsible for handling the bulk file uploads.
  - It processes the incoming file data and might perform actions like saving files to a server, validating file types/sizes, etc.

## Considerations

- Ensure that the files being uploaded adhere to any backend constraints such as file size limits, allowed file types, and the necessary structure for the `model`.
- Handle errors gracefully to provide feedback on what went wrong during the upload process, such as network issues or server rejections due to file validation checks.

## Summary

The `file_upload_api_helper.js` helps simplify the process of uploading multiple files to a backend server. By abstracting away the details of the HTTP request, it allows developers to focus on the data and logic of their application rather than the specifics of the file upload mechanism.


# 📄 Documentation: `complaint_user_api_helper.js`

This module provides helper functions to interact with the backend APIs related to user complaints and banned locations. It utilizes `axios` for making HTTP requests and provides a set of functions to perform CRUD operations.

## 📚 Index

- [Functions](#functions)
  - [getComplaintList](#getcomplaintlist)
  - [getComplaintDetail](#getcomplaintdetail)
  - [getBannedCountryList](#getbannedcountrylist)
  - [addBanCountry](#addbancountry)
  - [deleteCountryState](#deletecountrystate)
  - [editBanCountry](#editbancountry)

## 🚀 Functions

### 1. `getComplaintList`

Fetches the list of all user complaints from the server.

```javascript
export async function getComplaintList() {
  return await axiosApi.get(`complaint/`).then((response) => response);
}
```

- **Returns**: A promise that resolves to the response of the complaints list.

### 2. `getComplaintDetail`

Retrieves detailed information for a specific complaint by its ID.

```javascript
export async function getComplaintDetail(id) {
  return await axiosApi.get(`complaint/${id}/`).then((response) => response);
}
```

- **Parameters**:
  - `id`: The unique identifier of the complaint.
- **Returns**: A promise that resolves to the detailed response of the specified complaint.

### 3. `getBannedCountryList`

Obtains the list of countries that are currently banned.

```javascript
export async function getBannedCountryList() {
  return await axiosApi.get(`banned-locations/`).then((response) => response);
}
```

- **Returns**: A promise that resolves to the response containing the list of banned countries.

### 4. `addBanCountry`

Adds a new country to the banned list.

```javascript
export async function addBanCountry(model) {
  return await axiosApi.post(`banned-locations/`, model);
}
```

- **Parameters**:
  - `model`: An object containing the details of the country to be banned.
- **Returns**: A promise that resolves once the country has been successfully added to the banned list.

### 5. `deleteCountryState`

Deletes a country or state from the banned list by its ID.

```javascript
export async function deleteCountryState(id) {
  return await axiosApi.delete(`banned-locations/${id}`);
}
```

- **Parameters**:
  - `id`: The unique identifier of the country or state to be removed from the banned list.
- **Returns**: A promise that resolves once the specified country or state has been successfully removed.

### 6. `editBanCountry`

Edits the details of a banned country.

```javascript
export async function editBanCountry(model, id) {
  return await axiosApi.put(`banned-locations/${id}/`, model);
}
```

- **Parameters**:
  - `model`: An object containing the updated details of the banned country.
  - `id`: The unique identifier of the country to be edited.
- **Returns**: A promise that resolves once the country's details have been successfully updated.

---

This module serves as a crucial part of the application's backend communication, handling user complaints and managing the list of banned countries or regions effectively. 🛠️

# Documentation for `config_api_helper.js` 📄

## Overview 🌟

The `config_api_helper.js` file is a configuration and API helper module designed for handling HTTP requests and responses with authentication mechanisms. It leverages the Axios library to interact with back-end services, providing functionalities like token refresh, error handling, and various configuration-related API calls.

## Table of Contents 📚

- [Initialization](#initialization)
- [Request Interceptors](#request-interceptors)
- [Response Interceptors](#response-interceptors)
- [Helper Functions](#helper-functions)
- [API Functions](#api-functions)

---

## Initialization 🚀

The script starts by importing essential libraries and components:
- `axios` for HTTP requests.
- `authHeader` for generating authorization headers.
- `toast` and `toastrOptions` for displaying notifications.

```javascript
import axios from "axios";
import authHeader from "../helpers/jwt-token-access/authHeader";
import { toast } from "react-toastify";
import toastrOptions from "../helpers/toastr-options/toastr-options";
```

### Axios Instance 🌐

An Axios instance is created with a base URL, which is set from environment variables:

```javascript
const API_URL = process.env.REACT_APP_BASEURL;
const axiosApi = axios.create({ baseURL: API_URL });
```

---

## Request Interceptors 🛡️

The request interceptor automatically appends the authorization header to each request using the `authHeader` function.

```javascript
axiosApi.interceptors.request.use(
  (config) => {
    config.headers["Authorization"] = authHeader();
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);
```

---

## Response Interceptors 🔄

### Error Handling ⚠️

The response interceptor handles different response statuses:
- **500**: Displays an error using `toast`.
- **401**: Manages token refresh logic to handle expired tokens.

```javascript
axiosApi.interceptors.response.use(
  (response) => response.data,
  async (error) => {
    let errStatus = error?.response?.status;
    const originalRequest = error.config;
    if (errStatus === 500) {
      toast.error(error.response.data.detail, toastrOptions);
    } else if (errStatus === 401) {
      // Token refresh logic
    } else {
      // General error handling
    }
  }
);
```

### Token Refresh Logic 🔄

The module handles token expiration by refreshing tokens and retrying failed requests:

```javascript
let isRefreshing = false;
const failedQueue = [];

function subscribeTokenRefresh(cb) {
  failedQueue.push(cb);
}

function onRrefreshed(accessToken) {
  failedQueue.forEach((cb) => cb(accessToken));
}
```

---

## Helper Functions 🛠️

### `subscribeTokenRefresh(cb)`

Adds the callback to a queue that will be called once the token is refreshed.

### `onRrefreshed(accessToken)`

Executes all callbacks in the queue with the new access token.

---

## API Functions 🌐

### `refershTokenUpdate()`

Handles the token refresh process by sending the current tokens to the server and updating the local storage with new tokens.

```javascript
export async function refershTokenUpdate() {
  const url = process.env.REACT_APP_BASEURL + `accounts/token/`;
  const obj = JSON.parse(localStorage.getItem("authUser"));
  const body = {
    refresh_token: obj.extras.refresh_token,
    access_token: obj.extras.access_token,
  };
  const headers = { "Content-Type": "application/json" };
  return await axiosApi.post(url, body, { headers });
}
```

### `getCountries()`

Fetches the list of countries from the server.

```javascript
export async function getCountries() {
  return await axiosApi.get("config/countries/");
}
```

### `getStates(id)`

Retrieves states/regions based on a given country ID.

```javascript
export async function getStates(id) {
  return await axiosApi.get(`config/regions/${id}`);
}
```

### `getAzureToken()`

Obtains the Azure SAS token configuration.

```javascript
export async function getAzureToken() {
  return await axiosApi.get(`config/azure/sas/`);
}
```

---

This documentation provides a detailed overview of the `config_api_helper.js` file, explaining its purpose, functionality, and the various utilities it offers for managing API requests and configurations effectively.
# 📜 Community API Helper Documentation

**Filename:** `community_api_helper.js`

This module provides a set of helper functions to interact with the community-related API endpoints. It enables operations such as retrieving community lists, fetching community details, adding, editing, and deleting community entries, as well as getting lobby and username lists. 

## 📂 Index

1. [Functions](#functions)
   - [getCommunityList](#getcommunitylist)
   - [getCommunityDetail](#getcommunitydetail)
   - [addCommunity](#addcommunity)
   - [deleteCommunity](#deletecommunity)
   - [editCommunity](#editcommunity)
   - [getLobbyList](#getlobbylist)
   - [getUserNameList](#getusernamelist)
2. [Dependencies](#dependencies)

## 🌟 Functions

### 1. getCommunityList

```javascript
export async function getCommunityList(filterModel)
```

**Description:**  
Fetches a list of communities with pagination support.

**Parameters:**

- `filterModel`: An object containing filter options.
  - `pageSize`: Number of entries per page.
  - `pageNumber`: The page number to fetch.

**Returns:**  
A promise that resolves to an object containing:
- `data`: The list of community entries.
- `total`: Total number of community entries.

**Usage Example:**
```javascript
const filterModel = { pageSize: 10, pageNumber: 1 };
const communityList = await getCommunityList(filterModel);
```

---

### 2. getCommunityDetail

```javascript
export async function getCommunityDetail(id)
```

**Description:**  
Fetches details of a specific community by its ID.

**Parameters:**

- `id`: The unique identifier of the community.

**Returns:**  
A promise that resolves to the community details.

**Usage Example:**
```javascript
const communityDetail = await getCommunityDetail(123);
```

---

### 3. addCommunity

```javascript
export async function addCommunity(model)
```

**Description:**  
Adds a new community entry.

**Parameters:**

- `model`: An object representing the new community's data.

**Returns:**  
A promise that resolves once the community is successfully added.

**Usage Example:**
```javascript
const newCommunity = { name: "New Community", description: "Description here" };
await addCommunity(newCommunity);
```

---

### 4. deleteCommunity

```javascript
export async function deleteCommunity(id)
```

**Description:**  
Deletes a community entry by its ID.

**Parameters:**

- `id`: The unique identifier of the community to delete.

**Returns:**  
A promise that resolves once the community is successfully deleted.

**Usage Example:**
```javascript
await deleteCommunity(123);
```

---

### 5. editCommunity

```javascript
export async function editCommunity(id, model)
```

**Description:**  
Edits an existing community entry.

**Parameters:**

- `id`: The unique identifier of the community to edit.
- `model`: An object representing the new data for the community.

**Returns:**  
A promise that resolves once the community is successfully edited.

**Usage Example:**
```javascript
const updatedCommunity = { name: "Updated Community", description: "Updated description" };
await editCommunity(123, updatedCommunity);
```

---

### 6. getLobbyList

```javascript
export async function getLobbyList()
```

**Description:**  
Fetches a list of all lobbies.

**Returns:**  
A promise that resolves to an object containing lobby data.

**Usage Example:**
```javascript
const lobbyList = await getLobbyList();
```

---

### 7. getUserNameList

```javascript
export async function getUserNameList()
```

**Description:**  
Fetches a list of all usernames without pagination.

**Returns:**  
A promise that resolves to an object containing username data.

**Usage Example:**
```javascript
const usernameList = await getUserNameList();
```

---

## 📦 Dependencies

- **axiosApi**: The module relies on `axiosApi` from the `index.js` file to perform HTTP requests.

---

By utilizing these functions, developers can efficiently manage community-related data within their applications, ensuring smooth integration with the backend services.

# 📄 CMS API Helper Documentation

Welcome to the documentation for the `cms_api_helper.js` file. This module manages content management system (CMS) interactions, specifically for retrieving and updating legal pages and FAQs. Below you'll find detailed descriptions of each function, their purposes, and how to use them.

## Index
1. [Terms and Conditions](#terms-and-conditions)
2. [Privacy Policies](#privacy-policies)
3. [Frequently Asked Questions (FAQs)](#frequently-asked-questions-faqs)
4. [Topics Management](#topics-management)

---

### Terms and Conditions

#### 1. `getTermsAndCondition()`
- **Description**: Fetches the terms and conditions from the server.
- **Returns**: A promise that resolves to the server's response containing the terms and conditions data.

```javascript
export async function getTermsAndCondition() {
    return await axiosApi.get(`pages/terms-and-conditions`).then((response) => response);
}
```

#### 2. `addTermsCMS(model)`
- **Description**: Adds new terms and conditions content.
- **Parameters**: 
  - `model`: An object containing the terms data to be added.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function addTermsCMS(model) {
    return await axiosApi.post(`pages/`, model).then((response) => response);
}
```

#### 3. `editTermsCMS(model)`
- **Description**: Updates the existing terms and conditions.
- **Parameters**: 
  - `model`: An object containing the updated terms data.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function editTermsCMS(model) {
    return await axiosApi.put(`pages/terms-and-conditions/`, model).then((response) => response);
}
```

### Privacy Policies

#### 1. `getPrivacyPolicy()`
- **Description**: Retrieves the privacy policy from the server.
- **Returns**: A promise that resolves to the privacy policy data.

```javascript
export async function getPrivacyPolicy() {
    return await axiosApi.get(`pages/privacy-policy`).then((response) => response);
}
```

#### 2. `getCaliforniaPrivacyPolicy()`
- **Description**: Fetches the California-specific privacy policy.
- **Returns**: A promise that resolves to the policy data.

```javascript
export async function getCaliforniaPrivacyPolicy() {
    return await axiosApi.get(`pages/california-privacy`).then((response) => response);
}
```

#### 3. `addPrivacyCMS(model)`
- **Description**: Adds new privacy policy content.
- **Parameters**: 
  - `model`: An object containing the privacy policy data.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function addPrivacyCMS(model) {
    return await axiosApi.post(`pages/`, model).then((response) => response);
}
```

#### 4. `addCaliforniaPrivacyCMS(model)`
- **Description**: Adds a new California-specific privacy policy.
- **Parameters**: 
  - `model`: An object containing the policy data.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function addCaliforniaPrivacyCMS(model) {
    return await axiosApi.post(`pages/california-privacy`, model).then((response) => response);
}
```

#### 5. `editPrivacyCMS(model)`
- **Description**: Updates an existing privacy policy.
- **Parameters**: 
  - `model`: An object containing the updated policy data.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function editPrivacyCMS(model) {
    return await axiosApi.put(`pages/privacy-policy/`, model).then((response) => response);
}
```

#### 6. `editCaliforniaPrivacyCMS(model)`
- **Description**: Updates an existing California-specific privacy policy.
- **Parameters**: 
  - `model`: An object containing the updated policy data.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function editCaliforniaPrivacyCMS(model) {
    return await axiosApi.put(`pages/california-privacy/`, model).then((response) => response);
}
```

### Frequently Asked Questions (FAQs)

#### 1. `getQuestions({ filter = "" })`
- **Description**: Retrieves a list of FAQ questions, optionally filtered by type.
- **Parameters**: 
  - `filter`: A string used to filter the FAQs by type.
- **Returns**: A promise that resolves to the list of FAQs.

```javascript
export async function getQuestions({ filter = "" }) {
    return await axiosApi.get(`faq/?type=${filter}`).then((response) => response);
}
```

#### 2. `postQuestion(model)`
- **Description**: Adds a new FAQ question.
- **Parameters**: 
  - `model`: An object containing the FAQ data to be added.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function postQuestion(model) {
    return await axiosApi.post(`faq/`, model).then((response) => response);
}
```

#### 3. `editQuestion({ payload, questionId })`
- **Description**: Edits an existing FAQ question.
- **Parameters**: 
  - `payload`: An object containing the updated data.
  - `questionId`: The ID of the question to be edited.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function editQuestion({ payload, questionId }) {
    return await axiosApi.put(`faq/${questionId}/`, payload).then((response) => response);
}
```

#### 4. `deleteQuestion({ questionId })`
- **Description**: Deletes an FAQ question by ID.
- **Parameters**: 
  - `questionId`: The ID of the question to be deleted.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function deleteQuestion({ questionId }) {
    return await axiosApi.delete(`faq/${questionId}`).then((response) => response);
}
```

### Topics Management

#### 1. `deleteTopic({ topicSlug })`
- **Description**: Deletes a topic by its slug.
- **Parameters**: 
  - `topicSlug`: The slug of the topic to be deleted.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function deleteTopic({ topicSlug }) {
    return await axiosApi.delete(`faq/topics/${topicSlug}`).then((response) => response);
}
```

#### 2. `getTopics({ topicType })`
- **Description**: Retrieves a list of topics, optionally filtered by type.
- **Parameters**: 
  - `topicType`: A string used to filter topics by type.
- **Returns**: A promise that resolves to the list of topics.

```javascript
export async function getTopics({ topicType }) {
    return axiosApi.get(`faq/topics/?type=${topicType}`).then((response) => response);
}
```

#### 3. `editTopic({ payload, topicSlug })`
- **Description**: Edits an existing topic.
- **Parameters**: 
  - `payload`: An object containing the updated data.
  - `topicSlug`: The slug of the topic to be edited.
- **Returns**: A promise that resolves to the server's response.

```javascript
export async function editTopic({ payload, topicSlug }) {
    return await axiosApi.put(`faq/topics/${topicSlug}/`, payload).then((response) => response);
}
```

---

This concludes the documentation for `cms_api_helper.js`. Each function plays a vital role in managing CMS content, specifically legal documents and FAQ management. Use these methods to interact seamlessly with the backend CMS services.

# Documentation for `challenges_api_helper.js` 📄

Welcome to the documentation for the `challenges_api_helper.js` file. This file is designed to manage API interactions related to challenges in an application. Below, you'll find detailed information about each function provided within this helper.

## Table of Contents 📚

- [Overview](#overview)
- [Functions](#functions)
  - [getChallengesList](#getchallengeslist)
  - [getChallengesById](#getchallengesbyid)
  - [deleteChallenge](#deletechallenge)
  - [editChallenge](#editchallenge)

## Overview

The `challenges_api_helper.js` file is a module that facilitates communication with a backend API to perform operations related to challenges. These operations include retrieving a list of challenges, fetching details of a specific challenge, deleting a challenge, and editing challenge information. It utilizes `axiosApi` for making HTTP requests.

## Functions

### `getChallengesList` 📜

**Purpose**:  
Fetches a paginated list of challenges based on specific filter criteria.

**Parameters**:
- `filterModel`: An object containing filter criteria such as `sortBy`, `challengeMode`, `game`, `status`, `pageNumber`, and `pageSize`.

**Returns**:  
A promise that resolves to an object containing `data` (the list of challenges) and `total` (the total number of challenges).

**Example Usage**:
```javascript
const filterModel = {
  sortBy: "1",
  challengeMode: "single",
  game: "chess",
  status: "active",
  pageNumber: 1,
  pageSize: 10
};
const challenges = await getChallengesList(filterModel);
```

### `getChallengesById` 🔍

**Purpose**:  
Retrieves detailed information about a specific challenge by its ID.

**Parameters**:
- `challengeId` (string): The ID of the challenge to fetch.

**Returns**:  
A promise that resolves to the challenge details.

**Example Usage**:
```javascript
const challengeDetails = await getChallengesById("12345");
```

### `deleteChallenge` 🗑️

**Purpose**:  
Deletes a challenge identified by its ID.

**Parameters**:
- `delId` (string): The ID of the challenge to delete.

**Returns**:  
A promise indicating the success or failure of the deletion.

**Example Usage**:
```javascript
await deleteChallenge("12345");
```

### `editChallenge` ✏️

**Purpose**:  
Updates the information of a challenge.

**Parameters**:
- `challengeId` (string): The ID of the challenge to edit.
- `model` (object): An object containing the updated information for the challenge.

**Returns**:  
A promise indicating the success or failure of the update.

**Example Usage**:
```javascript
const updatedModel = {
  name: "New Challenge Name",
  status: "completed"
};
await editChallenge("12345", updatedModel);
```

---

This documentation provides a comprehensive guide to using the `challenges_api_helper.js` file, allowing developers to efficiently manage challenges within their applications. If you have further questions or need assistance, feel free to reach out.

# Bracket Tournaments API Helper Documentation 🏆

This document provides a comprehensive guide to the `bracket_tournaments_api_helper.js` file, which is responsible for handling API interactions related to bracket tournaments within the application. The helper functions in this file facilitate fetching, adding, editing, and deleting tournaments, as well as managing rounds, schedules, and leaderboard data.

## Index 📑

1. [Setup and Configuration](#setup-and-configuration)
2. [API Methods](#api-methods)
   - [1. Fetching Tournaments](#fetching-tournaments)
   - [2. Managing Tournaments](#managing-tournaments)
   - [3. Rounds and Scheduling](#rounds-and-scheduling)
   - [4. Tournament Administration](#tournament-administration)
   - [5. Leaderboard and Seeding](#leaderboard-and-seeding)
   - [6. Templates and Miscellaneous](#templates-and-miscellaneous)

---

## Setup and Configuration ⚙️

The file begins by importing necessary dependencies and setting up base URLs for API requests:

```javascript
import { axiosApi } from "./index";
const urlTournament = process.env.REACT_APP_BASEURL + `tournament/tournament/`;
const urlTournamentBaseUrl = process.env.REACT_APP_BASEURL;
```

These URLs are constructed using environment variables, ensuring that the API endpoints are configurable based on the deployment environment.

---

## API Methods 🛠️

### 1. Fetching Tournaments

- **Get Brackets and Tournaments Dropdown List**

  Retrieves a list of available brackets and tournaments:

  ```javascript
  export async function getBracketsAndTournamentsDropdownList() {
      return await axiosApi.get(urlTournament);
  }
  ```

- **Get Tournament List**

  Fetches a paginated list of tournaments with various filtering options:

  ```javascript
  export async function getTournamentList(filterModel) {
      let params = new URLSearchParams();
      if (filterModel.from_date) params.append("from_date", filterModel.from_date);
      if (filterModel.to_date) params.append("to_date", filterModel.to_date);
      // ... other filters ...
      return await axiosApi.get(urlTournament, { params }).then((response) => {
          return { data: response.results, total: response.total };
      });
  }
  ```

### 2. Managing Tournaments

- **Add Tournament**

  Adds a new tournament:

  ```javascript
  export async function addTournament(model) {
      return await axiosApi.post(urlTournament, model);
  }
  ```

- **Edit Tournament**

  Updates an existing tournament by ID:

  ```javascript
  export async function editTournament(id, model) {
      return await axiosApi.put(`${urlTournament}${id}/`, model);
  }
  ```

- **Delete Tournament**

  Deletes a tournament by ID:

  ```javascript
  export async function deleteTournament(tournamentId) {
      return await axiosApi.delete(`${urlTournament}${tournamentId}/`);
  }
  ```

### 3. Rounds and Scheduling

- **Get Tournament Round List**

  Retrieves the list of rounds for a specific tournament:

  ```javascript
  export async function getTournamentRoundList(id) {
      return await axiosApi.get(`${urlTournament}${id}/round/`);
  }
  ```

- **Add Schedule**

  Adds a match schedule to a tournament round:

  ```javascript
  export async function addSchedule(model, tournamentId, roundId, modalId) {
      return await axiosApi.post(`${urlTournament}${tournamentId}/round/${roundId}/match/${modalId}/add-matches/`, model);
  }
  ```

### 4. Tournament Administration

- **Get Admin User List for Tournament Dropdown**

  Fetches a list of administrators for a specific tournament:

  ```javascript
  export async function getAdminUserListTournamentForDropdown(id) {
      return await axiosApi.get(`${urlTournament}${id}/admins/`);
  }
  ```

- **Update Assigned Admin for Tournament**

  Updates the assigned administrator for a specific match in a tournament:

  ```javascript
  export async function updateAssignedAdminForTournament(tournamentId, matchId, model) {
      return await axiosApi.put(`${urlTournament}${tournamentId}/match/${matchId}/`, model);
  }
  ```

### 5. Leaderboard and Seeding

- **Get Leaderboard Standings**

  Retrieves leaderboard standings for a specific tournament:

  ```javascript
  export async function getLeaderboardStandings({ page, page_size, tournament_id }) {
      let params = new URLSearchParams();
      if (page_size) params.append("page_size", page_size);
      if (page) params.append("page", page);
      return await axiosApi.get(`${urlTournament}leaderboard/${tournament_id}`, { params });
  }
  ```

- **Send Manual Rank by Admin**

  Allows an admin to manually rank teams in a tournament:

  ```javascript
  export async function sendManualRankByAdmin(tournamentId, data) {
      return await axiosApi.put(`${urlTournamentBaseUrl}tournament/${tournamentId}/seeding/`, data);
  }
  ```

### 6. Templates and Miscellaneous

- **Get Brackets Template**

  Fetches the bracket template for a specific tournament:

  ```javascript
  export async function getBracketsTempalate(bracketId) {
      let params = new URLSearchParams();
      params.append("type", "admin");
      return await axiosApi.get(`${urlTournamentBaseUrl}tournament/iframe/${bracketId}/template/`, { params });
  }
  ```

- **Add Manual Winner**

  Allows manually adding a winner to a match:

  ```javascript
  export async function addManualWinner(matchId, model) {
      return await axiosApi.post(`${urlTournament}${matchId}/add-winners/`, model);
  }
  ```

---

This documentation provides a detailed look into the `bracket_tournaments_api_helper.js` file, offering insights into its functionality and how each API method contributes to the management of tournaments within the application. The use of environment variables ensures flexibility across different environments, making it adaptable for various deployment scenarios.

# 📜 Banner API Helper Documentation

Welcome to the documentation for the `banner_api_helper.js` file! This file contains functions for interacting with banner-related API endpoints. Below, you'll find a detailed explanation of each function, what it does, and how it can be used.

## 🚀 Index

- [Introduction](#introduction)
- [Functions Overview](#functions-overview)
- [Detailed Function Descriptions](#detailed-function-descriptions)
  - [getBannerList](#getbannerlist)
  - [getBannerDetail](#getbannerdetail)
  - [editBanner](#editbanner)
  - [addBanner](#addbanner)
  - [removeBanner](#removebanner)

---

## 🌟 Introduction

The `banner_api_helper.js` file is designed to facilitate interactions with the banner-related endpoints of an API. This is particularly useful in applications where banners, such as slider images, are displayed and need to be managed dynamically.

## 📚 Functions Overview

Below is a summary table of the functions available in `banner_api_helper.js`:

| Function       | Purpose                                           |
|----------------|---------------------------------------------------|
| `getBannerList`    | Fetches a list of all available banners.       |
| `getBannerDetail`  | Retrieves detailed information about a specific banner. |
| `editBanner`    | Updates an existing banner with new data.           |
| `addBanner`     | Adds a new banner to the system.                  |
| `removeBanner`  | Deletes a specified banner.                       |

---

## 📖 Detailed Function Descriptions

### 🔍 getBannerList

```javascript
export async function getBannerList() {
  return await axiosApi.get("sliderimage/");
}
```

- **Purpose**: Fetches a list of all banners.
- **Returns**: A promise that resolves to the list of banners.
- **Usage**: Use this function when you need to display a list of all banners in the application.

### 🧐 getBannerDetail

```javascript
export async function getBannerDetail(sliderId) {
  return await axiosApi.get(`sliderimage/${sliderId}/`);
}
```

- **Purpose**: Retrieves detailed information for a specific banner identified by `sliderId`.
- **Parameters**:
  - `sliderId` (number|string): The unique identifier for the banner.
- **Returns**: A promise that resolves to the detailed information of the specified banner.
- **Usage**: Use this function to get detailed information about a specific banner, such as when displaying a banner's details in a modal or separate view.

### ✏️ editBanner

```javascript
export async function editBanner(id, model) {
  return await axiosApi.put(`sliderimage/${id}/`, model);
}
```

- **Purpose**: Updates an existing banner with the data provided in `model`.
- **Parameters**:
  - `id` (number|string): The unique identifier for the banner to update.
  - `model` (object): The data to update the banner with.
- **Returns**: A promise that resolves when the banner has been successfully updated.
- **Usage**: Use this function to update an existing banner's details.

### ➕ addBanner

```javascript
export async function addBanner(model) {
  return await axiosApi.post(`sliderimage/`, model);
}
```

- **Purpose**: Adds a new banner to the system.
- **Parameters**:
  - `model` (object): The data for the new banner.
- **Returns**: A promise that resolves when the banner has been successfully added.
- **Usage**: Use this function to add a new banner to the application.

### ❌ removeBanner

```javascript
export async function removeBanner(id) {
  return await axiosApi.delete(`sliderimage/${id}/`, {});
}
```

- **Purpose**: Deletes a specified banner from the system.
- **Parameters**:
  - `id` (number|string): The unique identifier for the banner to be deleted.
- **Returns**: A promise that resolves when the banner has been successfully deleted.
- **Usage**: Use this function to remove a banner when it is no longer needed.

---

This concludes the documentation for the `banner_api_helper.js` file. Use these functions to manage banners efficiently in your application. Happy coding! 🎉

# Azure Blob API Helper Documentation 📦

The `azure_blob_api_helper.js` file is designed to assist with operations related to Azure Blob Storage, specifically focusing on generating URLs for accessing images stored in Azure Blob Storage. Although parts of the code are commented out, this documentation will cover both the active and commented sections to provide a comprehensive understanding of how to interact with Azure Blob Storage.

## Index 📑

1. [Overview](#overview)
2. [Functions](#functions)
   - [getImageUrl](#getimageurl)
   - [createBlobInContainer (Commented)](#createblobincontainer-commented)
   - [uploadFileToBlob (Commented)](#uploadfiletoblob-commented)
3. [Environment Variables](#environment-variables)
4. [Usage Example](#usage-example)

## Overview

Azure Blob Storage is a scalable, cost-effective, and secure object storage solution for cloud applications, data lakes, and more. This helper provides a function to generate public URLs for accessing images and includes commented-out code that demonstrates how to upload files to Azure Blob Storage using the Azure SDK for JavaScript.

## Functions

### getImageUrl

```javascript
const getImageUrl = (fileName) => {
    return `https://${storageAccountName}.blob.core.windows.net/${containerName}/${fileName}`;
};
```

- **Purpose**: Generates a URL for accessing a file stored in Azure Blob Storage.
- **Parameters**: 
  - `fileName`: The name of the file for which the URL is to be generated.
- **Returns**: A string URL pointing to the specified file in the Azure Blob Storage.

### createBlobInContainer (Commented)

```javascript
// const createBlobInContainer = async (containerClient, file) => {
//     const blobClient = containerClient.getBlockBlobClient(file.name);
//     const options = { blobHTTPHeaders: { blobContentType: file.type } };
//     await blobClient.uploadBrowserData(file, options);
// };
```

- **Purpose**: Uploads a file to a specified container in Azure Blob Storage.
- **Parameters**:
  - `containerClient`: The client for the container where the file will be uploaded.
  - `file`: The file object to be uploaded.
- **Details**: This function creates a block blob client for the specified file and uploads it with appropriate MIME type headers.

### uploadFileToBlob (Commented)

```javascript
// const uploadFileToBlob = async (file, azureToken, azureUrl) => {
//     if (!file) return null;
//     const blobService = new BlobServiceClient(azureUrl);
//     const containerClient = blobService.getContainerClient(containerName);
//     try {
//         await createBlobInContainer(containerClient, file);
//         return getImageUrl(file.name);
//     } catch (error) {
//         return null;
//     }
// };
```

- **Purpose**: Manages the full lifecycle of uploading a file to Azure Blob Storage and retrieving its URL.
- **Parameters**:
  - `file`: The file to be uploaded.
  - `azureToken`: The SAS token for Azure authentication.
  - `azureUrl`: The base URL for Azure Blob Storage.
- **Returns**: The URL of the uploaded file if successful; otherwise, `null`.

## Environment Variables

The functionality of this helper relies on several environment variables. Make sure these are correctly set in your environment:

- `REACT_APP_AZURE_SAS_TOKEN`: The SAS token for authenticating with Azure.
- `REACT_APP_AZURE_CONTAINER_NAME`: The name of the Azure Blob Storage container.
- `REACT_APP_AZURE_STORAGE_NAME`: The name of the Azure Storage account.

## Usage Example

To use the `getImageUrl` function, ensure your environment variables are correctly configured, then call the function with the file name:

```javascript
const imageUrl = getImageUrl("example-image.jpg");
console.log(imageUrl); // Outputs the URL for the specified image
```

> ⚠️ **Note**: The upload functionality (`uploadFileToBlob` and `createBlobInContainer`) is currently commented out. To activate it, uncomment the necessary code and ensure you have the Azure Storage Blob SDK installed and properly configured.

This documentation provides a complete overview of the `azure_blob_api_helper.js` file, detailing its purpose, functionality, and how to use it effectively within your application.

# 📚 Admin User API Helper Documentation

The `admin_user_api_helper.js` file contains several functions that facilitate interaction with an API for managing admin users and groups within a system. The file primarily utilizes **`axiosApi`**, a promise-based HTTP client, to send HTTP requests to various endpoints. Below is a comprehensive breakdown of the functionalities provided by this helper file.

## 📜 Table of Contents
1. [Admin User Management](#admin-user-management)
   - [Get Admin User List](#get-admin-user-list)
   - [Get Admin User Detail](#get-admin-user-detail)
   - [Add/Edit Admin User](#addedit-admin-user)
   - [Change Admin Status](#change-admin-status)
   - [Delete Admin](#delete-admin)
   - [Get Admin User List for Lobby and Dropdown](#get-admin-user-list-lobby)
2. [Group Management](#group-management)
   - [Get Group List](#get-group-list)
   - [Add/Edit Groups](#addedit-groups)
   - [Get Group Detail by ID](#get-group-detail-by-id)
   - [Delete Group](#delete-group)
3. [Utility Functions](#utility-functions)
   - [Get Group Lists](#get-group-lists)
   - [Get Permission Lists](#get-permission-lists)
   - [Get Staff Detail by ID](#get-staff-detail-by-id)

---

## ⚙️ Admin User Management

### Get Admin User List
**Function:** `getAdminUserList(filterModel)`

This function retrieves a list of admin users based on a given filter model. It supports search and sorting parameters as well as pagination.

```javascript
async function getAdminUserList(filterModel) {
    let params = new URLSearchParams();
    if (filterModel.searchTerm) params.append("query", filterModel.searchTerm);
    if (filterModel.sortBy) params.append("sort_by", filterModel.sortBy);
    if (filterModel.pageNumber) params.append("page", filterModel.pageNumber);
    if (filterModel.pageSize) params.append("page_size", filterModel.pageSize);

    return await axiosApi.get("staff/", { params }).then(response => {
        return { data: response.results, total: response.total };
    });
}
```

### Get Admin User Detail
**Function:** `getAdminUserDetail(userId)`

Fetches detailed information about a specific admin user identified by `userId`.

```javascript
async function getAdminUserDetail(userId) {
    return await axiosApi.get(`staff/${userId}/`);
}
```

### Add/Edit Admin User
**Function:** `addeditAdminUser(model, mode, adminId)`

Adds a new admin user or edits an existing one based on the `mode` parameter.

```javascript
async function addeditAdminUser(model, mode, adminId) {
    if (mode) {
        return await axiosApi.put(`staff/${adminId}/`, model);
    } else {
        return await axiosApi.post(`staff/`, model);
    }
}
```

### Change Admin Status
**Function:** `changeAdminStatus(userId, activeStatus)`

Updates the status (active/inactive) of an admin user.

```javascript
async function changeAdminStatus(userId, activeStatus) {
    return await axiosApi.put(`staff/${userId}/update-status/`, { status: activeStatus });
}
```

### Delete Admin
**Function:** `deleteAdmin(id)`

Deletes an admin user identified by `id`.

```javascript
async function deleteAdmin(id) {
    return await axiosApi.delete(`staff/${id}/`);
}
```

### Get Admin User List for Lobby
**Functions:** `getAdminUserListLobby`, `getAdminUserListLobbyForDropdown`

Retrieves a list of admin users for lobby purposes and for dropdown selection.

```javascript
async function getAdminUserListLobby() {
    return await axiosApi.get(`staff-members/`);
}

async function getAdminUserListLobbyForDropdown() {
    return await axiosApi.get(`staff-members/?no_page`);
}
```

## 👥 Group Management

### Get Group List
**Function:** `getGroupList()`

Fetches a list of all groups.

```javascript
async function getGroupList() {
    return await axiosApi.get("groups/").then(response => {
        return { data: response };
    });
}
```

### Add/Edit Groups
**Function:** `addEditGroups(model, mode, groupId)`

Adds a new group or edits an existing group based on the `mode` parameter.

```javascript
async function addEditGroups(model, mode, groupId) {
    if (mode) {
        return await axiosApi.put(`groups/${groupId}/`, model);
    } else {
        return await axiosApi.post(`groups/`, model);
    }
}
```

### Get Group Detail by ID
**Function:** `getGroupDetailByID(groupId)`

Fetches detailed information about a specific group identified by `groupId`.

```javascript
async function getGroupDetailByID(groupId) {
    return await axiosApi.get(`groups/${groupId}/`);
}
```

### Delete Group
**Function:** `deleteGroup(id)`

Deletes a group identified by `id`.

```javascript
async function deleteGroup(id) {
    return await axiosApi.delete(`groups/${id}/`);
}
```

## 🔧 Utility Functions

### Get Group Lists
**Function:** `getGroupLists()`

Fetches a list of all available groups.

```javascript
async function getGroupLists() {
    return await axiosApi.get("groups/");
}
```

### Get Permission Lists
**Function:** `getPermissionLists()`

Retrieves a list of all available permissions.

```javascript
async function getPermissionLists() {
    return await axiosApi.get("permissions/");
}
```

### Get Staff Detail by ID
**Function:** `getStaffDetailByID(adminId)`

Fetches detailed information about a staff member identified by `adminId`.

```javascript
async function getStaffDetailByID(adminId) {
    return await axiosApi.get(`staff/${adminId}/`);
}
```

---

This file is essential for managing admin users and groups within an application. It provides a robust API interface for performing CRUD operations, managing user status, and retrieving necessary lists for user interfaces. Each function is designed to interact with specific endpoints and return the necessary data in a structured format.

# 📜 `auth_api_helper.js` Documentation

Welcome to the documentation for the **`auth_api_helper.js`** file. This file is an API helper for managing authentication-related tasks such as login, password reset, and logout. It leverages `axios` for making HTTP requests and interacts with environment variables to configure its behavior. Below is a detailed breakdown of its functions and how they work.

## 📋 Index

- [Dependencies](#dependencies)
- [Environment Variables](#environment-variables)
- [Functions](#functions)
  - [Login](#login)
  - [Forgot Password](#forgot-password)
  - [Confirm Password](#confirm-password)
  - [Logout User Event](#logout-user-event)

## 📦 Dependencies

- **`axios`**: The `axiosApi` instance from the `index.js` file is used to perform HTTP requests.

## ⚙️ Environment Variables

- **`REACT_APP_APIURL`**: Base URL for API requests.
- **`REACT_APP_PRODUCTION`**: Flag to determine if the environment is production.
- **`REACT_APP_CLIENTTOKEN`**: Client token used for authentication in non-production environments.

## 🔧 Functions

### 🔑 Login

```javascript
export async function login({ email, password }) { ... }
```

**Purpose**: Authenticates a user using their email and password.

**Parameters**:
- `email`: The user's email address.
- `password`: The user's password.

**Process**:
1. Constructs an API request body with email and password.
2. Builds the API URL by appending `"login/"` to the base URL.
3. Sets headers if not in a production environment.
4. Sends a POST request to the API to log the user in.
5. Stores the response in `localStorage` under the key `"authUser"` if successful.

**Returns**: Promise resolving with the API response or undefined in the case of an error.

### 📧 Forgot Password

```javascript
export async function forgotpassword(email) { ... }
```

**Purpose**: Initiates a password reset process for the user.

**Parameters**:
- `email`: The user's email address.

**Process**:
1. Constructs an API request body with the email.
2. Builds the API URL by appending `"forgot-password/"` to the base URL.
3. Sets headers if not in a production environment.
4. Sends a POST request to the API to initiate the password reset.

**Returns**: Promise resolving with the API response.

### 🔐 Confirm Password

```javascript
export async function confirmpassword(password, id, token) { ... }
```

**Purpose**: Resets the user's password using a confirmation ID and token.

**Parameters**:
- `password`: The new password.
- `id`: The reset request identifier.
- `token`: The token received for password reset verification.

**Process**:
1. Constructs an API request body with the new password.
2. Builds the API URL by appending `"reset-password/"` with query parameters `id` and `token`.
3. Sets headers if not in a production environment.
4. Sends a PUT request to the API to reset the password.

**Returns**: Promise resolving with the API response.

### 🚪 Logout User Event

```javascript
export async function logoutuserEvent() { ... }
```

**Purpose**: Logs out the currently authenticated user.

**Process**:
1. Sends a PUT request to the `"/logout/"` endpoint to log the user out.

**Returns**: Promise resolving with the API response.

---

This completes the documentation for `auth_api_helper.js`. Each function is designed to perform specific authentication tasks, utilizing environment variables to adapt to different environments. This modular approach ensures easy maintenance and flexibility for various deployment stages. 🛠️✨