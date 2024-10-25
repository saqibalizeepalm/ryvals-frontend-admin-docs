# LobbyDetail.js Documentation

Welcome to the detailed documentation of the **LobbyDetail.js** file. This document aims to provide a comprehensive understanding of the code, its functionalities, and its purpose within the application.

---

## 🗂️ Index

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Class: LobbyDetail](#class-lobbydetail)
4. [Component Lifecycle](#component-lifecycle)
5. [Methods](#methods)
    - [callSetPermission](#callsetpermission)
    - [changeLobbyStatus](#changelobbystatus)
    - [delLobby](#dellobby)
    - [overrideLobby](#overridelobby)
    - [fetchStatsLobby](#fetchstatslobby)
    - [cancelLobby](#cancellobby)
    - [getLobbyData](#getlobbydata)
    - [toggle](#toggle)
    - [closeAlert](#closealert)
    - [goToListing](#gotolisting)
    - [isValidType](#isvalidtype)
    - [sendFileLength](#sendfilelength)
    - [handleSubmit](#handlesubmit)
    - [handleAcceptedFiles](#handleacceptedfiles)
    - [remove](#remove)
    - [showPreview](#showpreview)
    - [handleClose](#handleclose)
6. [Render Method](#render-method)
7. [Conclusion](#conclusion)

---

## 🎉 Introduction

**LobbyDetail.js** is a React component that provides detailed information and administrative functionalities for a specific lobby in a gaming application. It allows users to view, modify, and manage the lobby's details, such as game type, status, players, and results.

---

## 📦 Imports

The file imports various libraries and components to build a robust and interactive user interface:

- **React and React-Router-Dom**: For building the component and routing.
- **Reactstrap**: For UI components like cards, buttons, modals, etc.
- **SweetAlert**: For displaying alerts.
- **React-Toastify**: For notification messages.
- **AWS SDK**: For handling file uploads to Amazon S3.
- **Other Custom Components and Helpers**: For permissions, utility functions, and data management.

```jsx
import { withRouter, Link } from "react-router-dom";
import { Card, CardBody, Col, Row, Button, TabContent, TabPane, NavLink, NavItem, Nav, Modal, ModalBody, ModalHeader, } from "reactstrap";
import SweetAlert from "react-bootstrap-sweetalert";
import { toast } from "react-toastify";
import S3 from "react-aws-s3";
import { S3Client, PutObjectCommand, GetObjectCommand } from "@aws-sdk/client-s3";
import { getSignedUrl } from "@aws-sdk/s3-request-presigner";
import Dropzone from "react-dropzone";
```

---

## 🛠️ Class: LobbyDetail

**LobbyDetail** is a React component class extending `Component` from React. It manages the state and lifecycle of the lobby details view.

### State Variables

- `lobby`, `enroll`, `tournamentData`: Contains lobby-related data.
- `confirm_alert`, `delete_alert`, etc.: Boolean flags for modals and alerts.
- `activeTab`: Current active tab in the UI.
- `imageUrls`, `files`: Manages uploaded images and files.
- `permission`: Stores user permissions.
- `isLoading`, `processingLoader`: Boolean flags for loading states.

---

## ⏱️ Component Lifecycle

### componentDidMount()

Executed after the component is mounted. It extracts the lobby's ID from the URL and fetches its data. It also sets up permissions based on the game type.

```jsx
componentDidMount() {
    const { location } = this.props;
    const params = new URLSearchParams(location.search);
    const data = JSON.parse(decodeURIComponent(params.get("data")));
    this.setState({ tournamentData: data });
    let lobbyId = this.props.match.params.lobbyId;
    if (lobbyId == "add") {
        this.props.history.push("/lobby");
    } else {
        if (lobbyId) {
            this.getLobbyData(lobbyId);
        }
        if (isEmpty(this.props.permission)) {
            this.setState({
                changePermission: true,
                deletePermission: true,
                viewPermission: true,
                uploadPermission: true,
            });
        } else {
            this.callSetPermission();
        }
    }
}
```

---

## 📜 Methods

### callSetPermission

Sets user permissions based on the game type. It checks if the game is "Apex Legends", "COD Mobile", etc., and assigns permissions accordingly.

```jsx
callSetPermission = () => {
    const { location } = this.props;
    const params = new URLSearchParams(location.search);
    const data = JSON.parse(decodeURIComponent(params.get("data")));
    if (this.props.location.state?.item.game.name == "Apex Legends" || data?.nameOfGame == "Apex Legends") {
        // Set permissions for Apex Legends
    }
    // Other game types...
};
```

### changeLobbyStatus

Changes the status of the lobby between activated and deactivated.

```jsx
async changeLobbyStatus() {
    const changeStatus = this.state.lobby.status === 1 ? 2 : 1;
    this.setState({ isLoading: true });
    await changeStatusLobby(this.state.lobby.id, changeStatus)
        .then(() => {
            this.closeAlert();
            this.getLobbyData(this.state.lobby.id);
        })
        .catch((err) => {
            console.error(err);
            this.closeAlert();
            toast.error(err, toastrOptions);
        });
}
```

### delLobby

Deletes the lobby and notifies users of the deletion.

```jsx
async delLobby() {
    this.setState({ isLoading: true });
    await deleteLobby(this.state.lobby.id)
        .then((res) => {
            toast.success(res.message, toastrOptions);
            this.closeAlert();
            this.goToListing();
        })
        .catch((err) => {
            this.closeAlert();
            toast.error(err, toastrOptions);
        });
}
```

### overrideLobby

Overrides the lobby's start time and sends notifications to players.

```jsx
async overrideLobby() {
    this.setState({ isLoading: true });
    await overrideLobby(this.state.lobby.id)
        .then((res) => {
            toast.success(res.message, toastrOptions);
            this.closeAlert();
            this.goToListing();
        })
        .catch((err) => {
            this.closeAlert();
            toast.error(err, toastrOptions);
        });
}
```

### fetchStatsLobby

Fetches statistics for the lobby if they have arrived.

```jsx
async fetchStatsLobby() {
    this.setState({ isLoading: true });
    await fetchStats({ lobby_id: this.state.lobby.id })
        .then((res) => {
            let lobbyId = this.props.match.params.lobbyId;
            this.closeAlert();
            this.getLobbyData(lobbyId);
            toast.success(res.message, toastrOptions);
        })
        .catch((err) => {
            this.closeAlert();
            console.error(err);
        });
}
```

### cancelLobby

Cancels the lobby and refunds players as applicable.

```jsx
async cancelLobby() {
    this.setState({ isLoading: true });
    await cancelLobby({ lobby_id: this.state.lobby.id })
        .then((res) => {
            toast.success(res.message, toastrOptions);
            this.closeAlert();
            this.goToListing();
        })
        .catch((err) => {
            this.closeAlert();
            console.error(err);
            toast.error(err, toastrOptions);
        });
}
```

### getLobbyData

Fetches detailed data for a specific lobby.

```jsx
async getLobbyData(lobbyId) {
    try {
        const res = await getLobbyDetail(lobbyId);
        this.setState({ lobby: res });
        this.setState({ fileUploadSucess: { fileBoolean: false, fileMessage: "" } });
    } catch (error) {
        toast.error(error, toastrOptions);
    }
}
```

### toggle

Toggles the current active tab in the UI.

```jsx
toggle(tab) {
    if (this.state.activeTab !== tab) {
        this.setState({ activeTab: tab });
    }
}
```

### closeAlert

Closes any active alerts and resets loading states.

```jsx
closeAlert() {
    this.setState({
        confirm_alert: false,
        delete_alert: false,
        lobby_override_alert: false,
        cancel_alert: false,
        results_alert: false,
        isLoading: false,
    });
}
```

### goToListing

Redirects the user back to the lobby listing page.

```jsx
goToListing() {
    this.props.history.push("/lobby");
}
```

### isValidType

Checks if the uploaded file type is valid based on the lobby's game settings.

```jsx
isValidType = (data) => {
    const ext = this.state.lobby.game.stats_file_format.map((statsFileData) => {
        return statsFileData;
    });
    return ext.some((el) => data.endsWith(el));
};
```

### sendFileLength

Sends the length of the uploaded files to the server for processing.

```jsx
async sendFileLength(imageLength) {
    this.setState({ processingLoader: true });
    const data = { count: imageLength, pubg_images: this.state.imageUrls };
    await sendImageCount(data, this.state.lobby.id)
        .then((res) => {
            this.setState({
                fileUploadSucess: { fileBoolean: true, fileMessage: "Uploaded Successfully" },
            });
            setTimeout(() => {
                let lobbyId = this.props.match.params.lobbyId;
                if (lobbyId) {
                    this.getLobbyData(lobbyId);
                    this.setState({ csvData: [], csvFileName: "", files: [], disableSubmit: false });
                }
            }, 1000);
            this.setState({ processingLoader: false });
        })
        .catch((err) => {
            console.log(err);
            this.setState({ processingLoader: false });
        });
}
```

### handleSubmit

Handles file upload submissions, processing each file and uploading it to S3.

```jsx
handleSubmit = async () => {
    this.setState({ disableSubmit: true, processingLoader: true });
    if (this.state.lobby?.game?.is_multiple_upload) {
        for (let i = 0; i < this.state.files.length; ++i) {
            // Process each file for multiple uploads...
        }
    } else {
        // Process single file upload...
    }
};
```

### handleAcceptedFiles

Handles accepted files from the dropzone, validates them, and updates the state.

```jsx
handleAcceptedFiles = (files) => {
    if (this.state.lobby?.game?.is_multiple_upload) {
        for (let i = 0; i < files.length; ++i) {
            let fname = files[i].name;
            if (!this.isValidType(fname)) {
                this.setState({
                    invalidFile: { invalidFileBoolean: true, invalidFileMsg: `Please upload a valid file format` },
                });
                return false;
            } else {
                // Process valid files...
            }
        }
    } else {
        // Handle single file...
    }
};
```

### remove

Removes a specific file from the upload list.

```jsx
remove = (file) => {
    const newFiles = [...this.state.files];
    newFiles.splice(file, 1);
    this.setState({ files: newFiles });
    this.setState({ csvData: [], csvFileName: "" });
};
```

### showPreview

Opens a modal to preview the selected file.

```jsx
showPreview = (index) => {
    this.setState({ openPreviewModal: true, selectedPreviewId: index });
};
```

### handleClose

Closes the preview modal.

```jsx
handleClose = () => {
    this.setState({ openPreviewModal: false });
};
```

---

## 🖼️ Render Method

The `render` method constructs the UI, using Reactstrap components for layout and interactivity. It includes:

- **Breadcrumbs**: For navigation context.
- **Tabs**: To switch between lobby details, enrolled players, and results.
- **Cards and Tables**: To display the lobby information and player statistics.
- **Modals and Alerts**: For confirmations and previews.
- **Dropzone**: For file uploads.

```jsx
render() {
    return (
        <React.Fragment>
            <Loader isTransparent={true} showLoader={this.state.isLoading} />
            <div className="page-content">
                <Breadcrumbs breadcrumbItem="Lobby Detail" />
                <Row>
                    <Col>
                        <Nav tabs>
                            <NavItem>
                                <NavLink
                                    className={classnames({ active: this.state.activeTab === "1" })}
                                    onClick={() => this.toggle("1")}
                                >
                                    Lobby Details
                                </NavLink>
                            </NavItem>
                            {this.state.uploadPermission || this.state.changePermission ? (
                                <NavItem>
                                    <NavLink
                                        className={classnames({ active: this.state.activeTab === "2" })}
                                        onClick={() => this.toggle("2")}
                                    >
                                        Enrolled players
                                    </NavLink>
                                </NavItem>
                            ) : null}
                            {this.state.lobby?.current_status === 3 ? (
                                <NavItem>
                                    <NavLink
                                        className={classnames({ active: this.state.activeTab === "3" })}
                                        onClick={() => this.toggle("3")}
                                    >
                                        View Results
                                    </NavLink>
                                </NavItem>
                            ) : null}
                        </Nav>
                    </Col>
                    <TabContent activeTab={this.state.activeTab} className="p-3 text-muted lobby-details-view">
                        <TabPane tabId="1">
                            <Card className="mb-0">
                                {this.state.lobby && (
                                    <CardBody>
                                        <Row>
                                            <Col className="col-12">
                                                <h4 className="mb-4">{this.state.lobby?.name}</h4>
                                            </Col>
                                            {/* Display lobby details */}
                                        </Row>
                                    </CardBody>
                                )}
                            </Card>
                        </TabPane>
                        {/* TabPane for enrolled players and results */}
                    </TabContent>
                </Row>
            </div>
        </React.Fragment>
    );
}
```

---

## 🎉 Conclusion

The **LobbyDetail.js** file is an integral part of the gaming application, providing detailed functionalities to manage lobbies, including viewing, editing, deleting, and handling file uploads. This documentation serves as a guide to understanding its components and operations.

Feel free to reach out for any questions or further clarifications! 😊