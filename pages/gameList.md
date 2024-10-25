# GamesList.js Documentation

Welcome to the **GamesList.js** documentation! This document provides a comprehensive overview of the `GamesList.js` file, which is responsible for displaying a list of games in a responsive table format. It includes permissions handling for actions that can be performed on each game, such as editing.

## Table of Contents

1. [Introduction](#introduction)
2. [Components and Libraries Used](#components-and-libraries-used)
3. [State Variables](#state-variables)
4. [Effects and Helper Functions](#effects-and-helper-functions)
5. [Render Method](#render-method)
6. [Permissions Handling](#permissions-handling)
7. [Conclusion](#conclusion)

## Introduction

The **GamesList.js** component is a React functional component that fetches and displays a list of games in a table. It uses a responsive table library to ensure that the table is adaptable to various screen sizes. Additionally, it incorporates permission-based rendering for certain actions like editing a game's details.

## Components and Libraries Used

Below is a list of the components and libraries used in this file:

| Component/Library           | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| `React`                     | A JavaScript library for building user interfaces.                          |
| `reactstrap`                | A library for Bootstrap 4 components in React.                              |
| `react-super-responsive-table` | A library for responsive tables in React.                                |
| `Breadcrumbs`               | A custom component for displaying breadcrumb navigation.                    |
| `getGameList`               | A helper function to fetch the list of games from an API.                   |
| `FilterPermission`          | A helper to filter permissions based on user roles.                         |
| `filterOutPermissionToShowHide` | Utility to determine visibility of actions based on permissions.         |
| `lodash`                    | A utility library providing various JavaScript functions.                   |

## State Variables

The component utilizes several `state` variables to manage data and UI states:

- **games**: Stores the list of games fetched from the API.
- **loader**: A boolean that indicates if data fetching is in progress.
- **changePermission**: A boolean that determines whether the user has permission to change the game data.

## Effects and Helper Functions

### `useEffect`

- **Purpose**: Fetches the list of games once the component is mounted and sets permission states.
- **Dependencies**: Executes once due to an empty dependency array `[]`.

Inside the `useEffect`, there are two main tasks:

1. Fetch the list of games using `getGameList` and store it in the `games` state variable.
2. Determine the user's permissions and update the `changePermission` state accordingly using the `callSetPermission` function.

### `callSetPermission`

- **Purpose**: Sets the permission state for editing game data based on user roles.
- **Functionality**: Filters user permissions for games and updates the `changePermission` state.

## Render Method

The component's render method is responsible for displaying the UI elements, including:

- **Breadcrumbs**: Displays navigation breadcrumbs with the current page labeled as "Games".
- **Responsive Table**: Displays the list of games using the `react-super-responsive-table` library.
  - **Table Headers**: "Game Image", "Game Name", "Game Type", and conditionally "Action" based on permissions.
  - **Table Body**: Iterates over the `games` array to display each game's image, name, type, and an edit action if permissions allow.
  - **Loader Spinner**: Displays a loading spinner while data is being fetched.

## Permissions Handling

The component leverages permission utilities to conditionally render the "Edit" button for each game:

- **Filtering Permissions**: Uses `FilterPermission` and `filterOutPermissionToShowHide` to determine if the current user has the right to see and interact with the edit action.
- **Conditional Rendering**: If `changePermission` is `true`, the "Action" column and the "Edit" button are rendered.

## Conclusion

The **GamesList.js** file is a robust component designed to efficiently display and manage a list of games with permission-based action handling. It ensures that only authorized users can access specific functionalities like editing game data. The use of modern React hooks and libraries allows for a responsive and user-friendly interface. 

Feel free to explore and extend the functionalities as per your application's requirements! 🕹️🎮

---

Thank you for reading the documentation for **GamesList.js**! If you have any questions or feedback, please don't hesitate to reach out. Happy coding! 🚀

# EditGame.js Documentation

This documentation provides a comprehensive overview of the `EditGame.js` file, part of a React project likely involved in managing game data within a web application. The file allows users to edit game metadata, including images and rules, through a user interface. Below is a detailed breakdown of the file's functionality and structure.

---

## Index

1. [Overview](#overview)
2. [Imports](#imports)
3. [Configuration](#configuration)
4. [State Management](#state-management)
5. [Core Functions](#core-functions)
    - [getGame](#getgame)
    - [onUpload](#onupload)
    - [editGameData](#editgamedata)
    - [syncViews](#syncviews)
    - [handleClickShowRaw](#handleclickshowraw)
6. [UI Rendering](#ui-rendering)
7. [Usage](#usage)
8. [Dependencies](#dependencies)

---

## Overview

The `EditGame.js` file is a React component designed to handle the modification of game details such as uploading images and editing game rules. It provides a form-based user interface for these tasks, employing various libraries and React hooks to manage state and side effects.

---

## Imports

The file imports several modules and components:

- **React and Hooks**: `useEffect`, `useState` for component lifecycle management and state handling.
- **UI Components**: `Row`, `Col`, `Card`, `CardBody`, `FormGroup`, `Button`, `CustomInput` from `reactstrap` for layout and form components.
- **Routing**: `Link` from `react-router-dom` for navigation.
- **Notifications**: `toast` from `react-toastify` for success/error messages.
- **Utilities**: `updateGameData`, `getGameBySlug` from a custom API helper, and `uploadFile` from `react-s3` for file uploads.
- **Text Editor**: `ReactQuill` and a custom toolbar for rich-text editing.

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, FormGroup, Button, CustomInput, } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Link } from "react-router-dom";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import { updateGameData, getGameBySlug } from "../../services/game_api_helper";
import { uploadFile } from "react-s3";
import ReactQuill from "react-quill";
import "react-quill/dist/quill.snow.css";
import EditorToolbar, { formats } from "../CMS/EditorToolbar";
```

---

## Configuration

The file contains AWS S3 configuration for file uploads, using environment variables for secure access:

```javascript
const config = {
  bucketName: process.env.REACT_APP_S3_BUCKET_NAME,
  region: process.env.REACT_APP_S3_REGION_NAME,
  accessKeyId: process.env.REACT_APP_S3_ACCESS_KEY,
  secretAccessKey: process.env.REACT_APP_S3_SECRET_KEY,
};
```

---

## State Management

The component uses multiple state variables to manage data such as images, rules, and loading states. Notable state variables include:

- **loader**: Tracks whether data is being loaded.
- **game**: Stores the current game data.
- **imagePreview, helperImage, apexTDMPreview**: Hold URLs for image previews.
- **rules**: Stores the HTML content of the game rules.
- **errorMsg, ruleFieldError**: Manage error messaging for form validation.

```javascript
const [loader, setLoader] = useState(false);
const [game, setGame] = useState(null);
const [imagePreview, setImagePreview] = useState(null);
const [rules, setRules] = useState("");
...
```

---

## Core Functions

### getGame

Fetches game data based on a slug and updates state accordingly. Displays a loader during the fetch process.

```javascript
const getGame = async () => {
  setLoader(true);
  await getGameBySlug(props.match.params.gameSlug)
    .then((res) => {
      setImagePreview(res.background_image);
      setGame(res);
      setLoader(false);
    })
    .catch(() => {
      setLoader(false);
    });
};
```

### onUpload

Handles image uploads, checks for valid file types, dimensions, and updates state with uploaded file URLs.

```javascript
const onUpload = (event, setSpinnerLoaderFunc, uploadFunc, setImageFunc, setTextFunc, showErrorFunc, setDisabledFunc, isHelper = false) => {
  setSpinnerLoaderFunc(true);
  // File validation logic
  // File upload logic
};
```

### editGameData

Validates form inputs and submits updated game data to the server.

```javascript
async function editGameData(e) {
  e.preventDefault();
  // Validation logic
  await updateGameData(model, props.match.params.gameId)
    .then((res) => {
      toast.success("Game updated successfully", toastrOptions);
      goToListing();
    })
    .catch((err) => {
      console.error(err);
    });
}
```

### syncViews

Synchronizes the displayed content between the raw HTML view and the formatted view.

```javascript
const syncViews = (fromRaw) => {
  if (fromRaw) {
    setRules(raw_html + "");
  } else {
    setRawHTML(rules || "");
  }
};
```

### handleClickShowRaw

Toggles between raw HTML view and formatted view for the rules.

```javascript
const handleClickShowRaw = () => {
  setShowRaw(!show_raw);
  if (show_raw) setRawHTML(rules || "");
  syncViews(show_raw);
};
```

---

## UI Rendering

The component renders a form with input fields for editing game images and rules. It uses conditional rendering to display loaders and error messages.

### JSX Structure

- **Breadcrumbs**: For navigational context.
- **Form**: Contains image upload inputs and a rich-text editor for rules.
- **Preview Images**: Display previews of uploaded images.
- **Error Handling**: Displays error messages conditionally based on state.

```jsx
return (
  <React.Fragment>
    <div className="page-content">
      <Breadcrumbs breadcrumbItem={" Edit Game"} />
      {loader ? (
        <div class="spinner-grow transaction-spinner" role="status">
          <span class="sr-only">...Processing file</span>
        </div>
      ) : (
        <Row>
          <Col lg={12}>
            <Card>
              <CardBody>
                <Row>
                  <Col>
                    <p>
                      <Link to="/games"><i className="mdi mdi-arrow-left"></i> back</Link>
                    </p>
                  </Col>
                </Row>
                <Row>
                  <Col className="col-8">
                    <form onSubmit={editGameData}>
                      <FormGroup>
                        <div className="mb-3 chooseImage">
                          <CustomInput
                            type="file"
                            id="exampleCustomFileBrowser"
                            name="customFile"
                            label={"Choose an image file"}
                            onChange={(event) => onUpload(event, setSpinnerLoader, uploadFile, setImagePreview, setText, showError, setDisabled)}
                          />
                          {errorMsg.isError ? null : <label>Width and Height dimension must be 412x1092</label>}
                          <label className="errorMsgGames">{imageFieldError?.length === 0 ? errorMsg.errorMsg : imageFieldError}</label>
                        </div>
                      </FormGroup>
                      <div className="mb-3 preview-img">
                        <h2>{text ? "Image" : "Preview Image"}</h2>
                        <div class="upload-img">
                          {spinnerLoader ? (
                            <div class="spinner-grow spinner-class" role="status" style={{ position: "inherit" }}></div>
                          ) : (
                            imagePreview && <img alt="Cropped" src={imagePreview} />
                          )}
                        </div>
                      </div>
                      <div className={show_raw ? "mb-3 showRaw" : "mb-3"}>
                        <label className={ruleFieldError.length === 0 ? "" : "errorMsgGames"}>Rules</label>
                        <EditorToolbar toolbarId="toolbar-1" onClickRaw={handleClickShowRaw} />
                        <ReactQuill
                          theme="snow"
                          modules={{
                            toolbar: { container: `#toolbar-1` },
                            clipboard: { matchVisual: false },
                          }}
                          formats={formats}
                          onChange={setRulesData}
                          value={rules || ""}
                          placeholder="Write something"
                        />
                        <textarea
                          className={"raw-editor"}
                          onChange={(e) => handleChangeRaw(e.target.value)}
                          value={raw_html}
                        />
                        <label className="errorMsgGames invalid-feedback">{ruleFieldError}</label>
                      </div>
                      <FormGroup>
                        <div className="mb-3 chooseImage">
                          <CustomInput
                            type="file"
                            id="exampleCustomFileBrowserHelper"
                            name="customFileHelper"
                            label={"Choose a Helper image file"}
                            onChange={(event) => onUpload(event, setSpinnerLoaderHelper, uploadFile, setHelperImage, setTextHelper, showErrorForHelperImage, setDisabled, true)}
                          />
                          {errorMsgForHelper.errorMsgForHelper.length === 0 ? null : (
                            <label className={errorMsgForHelper.errorMsgForHelper.length === 0 ? "" : "errorMsgGames invalid-feedback"}>
                              {errorMsgForHelper.errorMsgForHelper}
                            </label>
                          )}
                          {helperImageFieldError?.length === 0 ? null : (
                            <label className={helperImageFieldError?.length === 0 ? "" : "errorMsgGames invalid-feedback"}>
                              {helperImageFieldError?.length === 0 ? errorMsgForHelper.errorMsgForHelper : helperImageFieldError}
                            </label>
                          )}
                        </div>
                      </FormGroup>
                      <div className="mb-3 preview-img">
                        <h2>{textHelper ? (helperImage === null || helperImage === undefined ? "" : "Helper image") : "Helper image preview"}</h2>
                        <div class="upload-img">
                          {spinnerLoaderHelper ? (
                            <div class="spinner-grow spinner-class" role="status" style={{ position: "inherit" }}></div>
                          ) : (
                            helperImage && <img alt="preview" src={helperImage} />
                          )}
                        </div>
                      </div>
                      {game?.slug == "apex-legends" && (
                        <>
                          <FormGroup>
                            <div className="mb-3 chooseImage">
                              <CustomInput
                                type="file"
                                id="exampleCustomFileBrowserApexTDM"
                                name="customFileHelper"
                                label={"Choose an Apex TDM image file"}
                                onChange={(event) => onUpload(event, setSpinnerLoaderApexTDM, uploadFile, setApexTDMPreview, setTextApexTDM, showErrorMsgForApexTDM, setDisabled)}
                              />
                              {errorMsgForApexTDM.isError ? null : <label>Width and Height dimension must be 412x1092</label>}
                              <label className="errorMsgGames">{apexTDMImageFieldError?.length === 0 ? errorMsgForApexTDM.errorMsg : apexTDMImageFieldError}</label>
                            </div>
                          </FormGroup>
                          <div className="mb-3 preview-img">
                            <h2>{textApexTDM ? (apexTDMPreview === null || apexTDMPreview === undefined ? "" : "Apex TDM Image") : "Apex TDM Image preview"}</h2>
                            <div class="upload-img">
                              {spinnerLoaderApexTDM ? (
                                <div class="spinner-grow spinner-class" role="status" style={{ position: "inherit" }}></div>
                              ) : (
                                apexTDMPreview && <img alt="preview" src={apexTDMPreview} />
                              )}
                            </div>
                          </div>
                        </>
                      )}
                      <FormGroup style={{ marginTop: "7.5rem" }}>
                        <div>
                          <Button type="submit" color="primary" className="ms-1" disabled={disabled}>
                            Submit
                          </Button>
                        </div>
                      </FormGroup>
                    </form>
                  </Col>
                </Row>
              </CardBody>
            </Card>
          </Col>
        </Row>
      )}
    </div>
  </React.Fragment>
);
```

---

## Usage

To use this component, ensure your environment variables for AWS S3 are set up correctly for file uploads. The component should be integrated within a route that provides a game slug parameter to fetch and edit the corresponding game data.

---

## Dependencies

The component relies on several external libraries, including:

- React and React Router for component structure and routing.
- Reactstrap for UI components.
- React-Toastify for user notifications.
- React-Quill for rich-text editing.
- AWS S3 configuration for handling file uploads.

---

This documentation provides a complete understanding of the `EditGame.js` file, detailing its purpose, structure, and operation within the larger application context.