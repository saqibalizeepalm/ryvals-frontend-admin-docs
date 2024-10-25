    # 📄 AdminUserDetail.js Documentation

## 📜 Table of Contents
1. [Introduction](#introduction)
2. [File Overview](#file-overview)
3. [Key Components and Functions](#key-components-and-functions)
    - [Imports](#imports)
    - [Class and Constructor](#class-and-constructor)
    - [Lifecycle Method: componentDidMount](#lifecycle-method-componentdidmount)
    - [Navigation Method: goToListing](#navigation-method-gotolisting)
    - [Render Method](#render-method)
4. [UI Components](#ui-components)
5. [Conclusion](#conclusion)

---

## 📢 Introduction
This document provides a comprehensive guide to the `AdminUserDetail.js` file. This file is part of a React application and is responsible for displaying detailed information about an admin user. Let's delve deeper into each part of the code to understand its functionality.

---

## 📁 File Overview
`AdminUserDetail.js` is a React component that fetches and displays details of a specific admin user. It utilizes React Router for navigation and Reactstrap for UI components.

---

## 🔑 Key Components and Functions

### 📥 Imports
The file begins with several import statements that bring in necessary dependencies and components:
- **React & Component**: Core React library and component class.
- **Link & withRouter**: For navigation and routing.
- **Card, CardBody, Col, Row**: UI components from Reactstrap.
- **Breadcrumbs**: Custom component for displaying the page breadcrumb.
- **getAdminUserDetail**: A service function to fetch admin user details.

```javascript
import { Link, withRouter } from "react-router-dom";
import { Card, CardBody, Col, Row } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import React, { Component } from "react";
import { getAdminUserDetail } from "../../services/admin_user_api_helper";
```

### 🏷️ Class and Constructor
The `AdminUserDetail` class extends `Component` and initializes the state with `adminUser` set to `null`. This state will hold the user data fetched from the API.

```javascript
class AdminUserDetail extends Component {
  constructor(props) {
    super(props);
    this.state = { adminUser: null };
  }
```

### 🚀 Lifecycle Method: componentDidMount
This method is invoked immediately after the component is mounted. It retrieves the `adminId` from the URL parameters and fetches the corresponding user details using the `getAdminUserDetail` API call. If an error occurs, it navigates back to the listing page.

```javascript
componentDidMount() {
  let userId = this.props.match.params.adminId;
  if (userId) {
    getAdminUserDetail(userId)
      .then((res) => {
        this.setState({ adminUser: res });
      })
      .catch((err) => {
        this.goToListing();
      });
  }
}
```

### 🌐 Navigation Method: goToListing
This method redirects the user to the `/staff` route, which presumably lists all staff members.

```javascript
goToListing() {
  this.props.history.push("/staff");
}
```

### 🖥️ Render Method
The `render` method constructs the UI of the component. It uses conditional rendering to display the `adminUser` details only if they are available. It employs Reactstrap components for layout and styling.

```javascript
render() {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs breadcrumbItem="Staff Member Detail" />
        <Row>
          <Col>
            <Card>
              {this.state.adminUser && (
                <CardBody>
                  <Row className="mb-4">
                    <Col>
                      <p>
                        <Link to="/staff">
                          <i className="mdi mdi-arrow-left"></i> back
                        </Link>
                      </p>
                    </Col>
                  </Row>
                  <Row className="mb-3">
                    <Col className="col-12">
                      <h4 className="mb-4">
                        {this.state.adminUser?.first_name}{" "}
                        {this.state.adminUser?.last_name}
                      </h4>
                    </Col>
                    <Col className="col-12 mb-3">
                      <strong className="capitalize">Username:</strong>{" "}
                      <span>{this.state.adminUser?.username}</span>
                    </Col>
                    <Col className="col-12 mb-3">
                      <strong className="capitalize">Email address:</strong>{" "}
                      <span>{this.state.adminUser?.email || "NA"}</span>
                    </Col>
                    <Col className="col-12 mb-3">
                      <strong className="capitalize">Phone Number:</strong>{" "}
                      <span>{this.state.adminUser?.phone || "NA"}</span>
                    </Col>
                    <Col className="col-12 mb-3">
                      <strong className="capitalize">Address:</strong>{" "}
                      <span>{this.state.adminUser?.address?.full || "NA"}</span>
                    </Col>
                    <Col className="col-12 mb-3">
                      <strong className="capitalize">Profile Status:</strong>{" "}
                      <span>
                        {this.state.adminUser?.profile?.is_verified
                          ? "Verified"
                          : "Unverified"}
                      </span>
                    </Col>
                  </Row>
                </CardBody>
              )}
            </Card>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
}
```

---

## 🌈 UI Components
- **Breadcrumbs**: Displays the current page location within the app.
- **Link**: Navigates back to the staff listing.
- **Card & CardBody**: Encapsulates the UI components for user details.
- **Row & Col**: Arranges the layout of the user details.

---

## 🏁 Conclusion
The `AdminUserDetail.js` component is a vital part of the admin section of the application, allowing users to view detailed information about an admin user. It efficiently fetches data from an API and displays it using React components and Reactstrap for styling. Understanding this component is crucial for managing and navigating the admin user details within the application.