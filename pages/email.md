# 📧 Email Basic Template Documentation

**File:** `email-basic-templte.js`

## 📑 **Table of Contents**

1. [Introduction](#introduction)
2. [Purpose](#purpose)
3. [Components and Libraries](#components-and-libraries)
4. [Code Explanation](#code-explanation)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

---

## 📝 **Introduction**

The `email-basic-templte.js` file is a React component designed to create a basic email template. This template is useful for sending standardized email communications, such as confirmation emails, which are vital for maintaining effective user engagement and communication.

## 🎯 **Purpose**

The purpose of this file is to render a structured email layout using React and associated libraries. It is designed to be responsive and visually pleasing, ensuring that it can serve as a reliable template for email communications.

## 📚 **Components and Libraries**

The file utilizes several libraries and components to achieve its functionality:

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library providing Bootstrap 4 components built with React.
- **React Router**: A library used for routing in React applications.
- **Breadcrumbs**: A custom component for displaying breadcrumb navigation.

## 🔍 **Code Explanation**

Below is a detailed breakdown of the code and its functionality:

```javascript
import React from "react";
import { Row, Col } from "reactstrap";
import { Link } from "react-router-dom";

// Import Breadcrumb
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

- **Imports**: The file starts by importing necessary libraries and components. `React` is essential for creating the component, `reactstrap` provides grid components (`Row`, `Col`), and `Link` from `react-router-dom` is used for navigation. The `Breadcrumbs` component is used for displaying breadcrumb navigation.

```javascript
const EmailBasicTemplte = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <div className="container-fluid">
          <Breadcrumbs title="Email Template" breadcrumbItem="Basic Action" />
```

- **Component Definition**: A functional component named `EmailBasicTemplte` is defined. It returns a JSX element wrapped in a `React.Fragment`.

- **Breadcrumbs**: The `Breadcrumbs` component provides navigation with the titles "Email Template" and "Basic Action".

```javascript
<Row className="email-template">
  <Col md="12">
    <table className="body-wrap" style={{ fontFamily: "'Helvetica Neue',Helvetica,Arial,sans-serif", ... }}>
      <tbody>
        <tr>
          <td></td>
          <td className="container" width="600">
            <div className="content">
              <table className="main" width="100%" cellPadding="0" cellSpacing="0" itemProp="action" itemScope itemType="http://schema.org/ConfirmAction">
                <tbody>
                  <tr>
                    <td className="content-wrap">
                      <meta itemProp="name" content="Confirm Email" />
                      <table width="100%" cellPadding="0" cellSpacing="0">
                        <tbody>
                          <tr>
                            <td className="content-block">Please confirm your email address by clicking the link below.</td>
                          </tr>
                          <tr>
                            <td className="content-block">We may need to send you critical information about our service...</td>
                          </tr>
                          <tr>
                            <td className="content-block" itemProp="handler" itemScope itemType="http://schema.org/HttpActionHandler">
                              <Link to="#" color="primary" itemProp="url" style={{ ... }}>
                                Confirm email address
                              </Link>
                            </td>
                          </tr>
                          <tr>
                            <td className="content-block">
                              <b>Qovex</b>
                              <p>Support Team</p>
                            </td>
                          </tr>
                          <tr>
                            <td className="content-block" style={{ textAlign: "center" }}>© {new Date().getFullYear()} Qovex</td>
                          </tr>
                        </tbody>
                      </table>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </Col>
</Row>
```

- **Email Template Structure**: The layout is structured using `Row` and `Col` from Reactstrap. A table-based structure is used for the email content to ensure compatibility across email clients. The main table contains:
  - **Content Blocks**: These are sections of the email containing text prompts for the user.
  - **Confirmation Link**: A `Link` component styled to appear as a button, prompting the user to confirm their email.
  - **Footer**: Includes company branding and support team information.

## 🛠️ **Usage**

To use this component, simply import it into your desired React application page and render it within your JSX. This will output a styled, basic email template ready for customization and sending.

## 🎉 **Conclusion**

The `email-basic-templte.js` file provides a simple yet effective template for sending basic email confirmations. It ensures that essential communication with users is both professional and consistent, leveraging React and various components to create a flexible and robust solution.

This documentation should guide you through understanding and implementing the email template effectively. If further customization is needed, consider modifying the styles and content blocks to match your specific requirements.

# 📧 Email Inbox Component Documentation

Welcome to the detailed documentation for the **Email Inbox Component**. This document serves as a guide to understanding the functionality and structure of the `email-inbox.js` file. It explains the purpose of the component, its parts, and how they work together to create an email inbox interface. 

---

## 📑 Index

1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Key Elements](#key-elements)
4. [Features and Usage](#features-and-usage)
5. [Code Breakdown](#code-breakdown)
6. [Conclusion](#conclusion)

---

## 📜 Introduction

The **Email Inbox Component** is a React component designed to simulate an email inbox. It integrates various subcomponents to provide a functional and visually appealing user interface, resembling a traditional email client. It is part of a larger email management system, allowing users to navigate through and interact with their emails easily.

---

## 🏗️ Component Structure

The component is structured using several React and Reactstrap elements, providing both functionality and styling. Here's a quick overview:

- **Breadcrumbs**: Provides navigation feedback to the user.
- **EmailSidebar**: A sidebar for additional navigation and email management options.
- **EmailToolbar**: A top toolbar for managing emails (e.g., mark as read/unread, delete).
- **Email List**: Displays the list of emails with their subject, sender, date, etc.
- **Pagination Controls**: Allows navigation between pages of emails.

---

## 🔑 Key Elements

| Element        | Description                                                             |
|----------------|-------------------------------------------------------------------------|
| `Breadcrumbs`  | Displays the current location within the email system.                  |
| `EmailSidebar` | A sidebar component for additional options (not detailed in this file). |
| `EmailToolbar` | A toolbar for quick actions on emails (not detailed in this file).      |
| `Email List`   | The main area where emails are listed and can be interacted with.       |
| `Pagination`   | Controls to navigate through different pages of the email list.         |

---

## 🚀 Features and Usage

- **Check Email**: Users can select emails using checkboxes.
- **Star Emails**: Users can mark important emails with a star.
- **Navigation**: Navigate through different pages of emails.
- **Categorization**: Emails can be tagged with categories like `Freelance`, `Support`, etc.
- **Responsive Design**: Utilizes Reactstrap for a responsive and modern UI.

---

## 🖥️ Code Breakdown

Here's a closer look at the key sections of the code:

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { Row, Col, Button, Input, Label, Card } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import EmailSideBar from "./email-sidebar";
import EmailToolbar from "./email-toolbar";
```

- **Imports**: The component imports necessary libraries and other components for functionality and layout.

```jsx
const EmailInbox = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Email" breadcrumbItem="Inbox" />
        <Row>
          <Col xs="12">
            <EmailSideBar />
            <div className="email-rightbar mb-3">
              <Card>
                <EmailToolbar />
                <ul className="message-list">
                  {/* Email Items */}
                </ul>
              </Card>
              <Row>
                <Col xs="7">Showing 1 - 20 of 1,524</Col>
                <Col xs="5">
                  <div className="btn-group float-end">
                    <Button type="button" color="success" size="sm" className="waves-effect">
                      <i className="fa fa-chevron-left" />
                    </Button>
                    <Button type="button" color="success" size="sm" className="waves-effect">
                      <i className="fa fa-chevron-right" />
                    </Button>
                  </div>
                </Col>
              </Row>
            </div>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
};
```

- **Component**: Defines the `EmailInbox` component using React functional component syntax.
- **Layout**: Utilizes `Reactstrap` for layout with `Row` and `Col`.
- **Breadcrumbs**: Renders navigation breadcrumbs.
- **Email List**: Iterates over and renders a list of emails.
- **Pagination**: Provides buttons to navigate through email pages.

---

## 🔚 Conclusion

The **Email Inbox Component** is a robust and flexible component designed for simulating an email inbox interface. Through the use of React and Reactstrap, it offers a clean and functional user experience, integrating seamlessly with other components to form a comprehensive email management system.

Feel free to explore further and customize it according to your specific needs! If you have any questions or run into issues, don't hesitate to reach out. Happy coding! 🚀

# 📧 Email Module Documentation

This documentation provides a detailed explanation of the `email-basic-templte.js`, `email-inbox.js`, and `email-read.js` files, which are part of a React-based email system. These files are responsible for rendering different components of an email application, including basic email templates, the inbox view, and the email reading view.

---

## 🗂️ Table of Contents
1. [email-basic-templte.js](#email-basic-templte-js)
2. [email-inbox.js](#email-inbox-js)
3. [email-read.js](#email-read-js)

---

## 📄 email-basic-templte.js

### Description
`email-basic-templte.js` is a React component that generates a basic email template used for email confirmation actions. This component includes a simple structure with a header, body text, a confirmation link, and a footer with branding details.

### Code Explanation
- **Imports**:
  - `React`: Core library for building user interfaces.
  - `reactstrap`: Provides Bootstrap 4 components as React components.
  - `react-router-dom`: Enables navigation between different components.
  - `Breadcrumbs`: Component for displaying breadcrumb navigation.
  
- **Components**:
  - `Row` and `Col`: Used to create responsive grid layouts.
  - `Link`: For navigation links within the application.
  
- **Structure**:
  - **Breadcrumbs**: Displays the navigation path as "Email Template > Basic Action".
  - **Email Content**:
    - Uses a table layout to structure the email.
    - Contains text prompting the user to confirm their email address with a styled Button link.
    - Footer includes the company name and a dynamic copyright year.

### Key Features
- **Responsive Design**: Utilizes Bootstrap components for a responsive layout.
- **Custom Styling**: Inline styles are used for precise control over the appearance.
- **Dynamic Content**: Includes JavaScript expressions for dynamic data, such as the current year.

### Sample Code Snippet
```javascript
<Link to="#" color="primary" itemProp="url" style={{ ... }}>
  Confirm email address
</Link>
```

---

## 📬 email-inbox.js

### Description
The `email-inbox.js` file defines a React component that renders an email inbox interface. This includes a list of email messages, a sidebar for navigation, and a toolbar for email actions.

### Code Explanation
- **Imports**:
  - Similar to the previous file, it imports `React`, `reactstrap` components, `react-router-dom`, and `Breadcrumbs`.
  - `EmailSideBar` and `EmailToolbar`: Components to render the sidebar and toolbar.

- **Components**:
  - **Email List**: Displays a list of email messages with checkboxes, subject lines, and other metadata.
  - **Pagination**: Provides navigation through the email list with next and previous buttons.

- **Structure**:
  - **Breadcrumbs**: Indicates the current view as "Email > Inbox".
  - **Sidebar**: Provides navigation options within the email application.
  - **Email Toolbar**: Offers actions such as compose, delete, and mark as read.
  - **Messages**: Each email is represented as a list item with sender, subject, teaser, and date information.

### Key Features
- **Interactive Elements**: Checkboxes for selecting emails, buttons for pagination, and star toggles for marking favorites.
- **Dynamic Layout**: Supports a dynamic email list that updates based on user actions or data changes.
- **Custom Badges**: Uses Bootstrap badges to categorize emails by type (e.g., Social, Support).

### Sample Code Snippet
```javascript
<ul className="message-list">
  <li>
    <div className="col-mail col-mail-1">
      ...
    </div>
    <div className="col-mail col-mail-2">
      ...
    </div>
  </li>
</ul>
```

---

## 📖 email-read.js

### Description
`email-read.js` is a React component that renders a detailed view of a selected email message. It includes the sender's information, the email content, and options for replying and downloading attachments.

### Code Explanation
- **Imports**:
  - Alongside common imports, it includes images for avatars and other media.
  - `EmailSideBar` and `EmailToolbar`: Components used again for consistency in navigation and actions.

- **Components**:
  - **Email Header**: Displays sender details and the email subject.
  - **Email Body**: Contains the main content of the email.
  - **Attachments**: Provides links to download attached files.

- **Structure**:
  - **Breadcrumbs**: Shows navigation as "Email > Read Email".
  - **Sender Section**: Includes the sender's avatar, name, and email address.
  - **Content**: Displays a greeting, email text, and closing remarks.
  - **Action Buttons**: Reply button for email response and download links for attachments.

### Key Features
- **Avatar and Images**: Displays sender's avatar for personalization.
- **Attachment Handling**: Offers download options for files attached to the email.
- **Responsive Design**: Maintains a responsive layout using Bootstrap's grid system.

### Sample Code Snippet
```javascript
<div className="d-flex mb-4">
  <img className="d-flex me-3 rounded-circle avatar-sm" src={avatar2} alt="Qovex" />
  <div className="flex-1">
    <h5 className="font-size-14 mt-1"> Humberto D. Champion </h5>
    <small className="text-muted">support@domain.com</small>
  </div>
</div>
```

---

This documentation provides an overview of how each component works and the features they offer. These components can be further customized and extended to fit specific requirements of an email application.

# 📄 Documentation for `email-sidebar.js`

## 📋 Overview

`email-sidebar.js` is a React component that serves as the sidebar for an email application. It provides a convenient interface for users to navigate through their email functionalities such as Inbox, Sent Mail, Drafts, and more. Additionally, it includes a chat section for quick interactions and a modal for composing new emails.

### 🛠 Features:
- **Email Navigation**: Navigate through Inbox, Starred, Important, Drafts, Sent Mail, and Trash.
- **Labels**: Organize emails using customizable labels.
- **Chat Interface**: Quick chat access to recent conversations.
- **Email Composition**: Compose new emails using a modal with a rich text editor.

---

## 📑 Table of Contents
1. [Code Structure](#code-structure)
2. [Component Breakdown](#component-breakdown)
3. [Key Functionalities](#key-functionalities)
4. [How It Works](#how-it-works)
5. [Dependencies](#dependencies)

---

## 📦 Code Structure

The component structure is designed to be intuitive and easy to extend:

```javascript
import React, { useState } from "react";
import { Link } from "react-router-dom";
import { Button, Modal, ModalHeader, ModalBody, ModalFooter, Input, Card } from "reactstrap";
import { Editor } from "react-draft-wysiwyg";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css";
import avatar2 from "../../assets/images/users/avatar-2.jpg";
import avatar3 from "../../assets/images/users/avatar-3.jpg";
import avatar4 from "../../assets/images/users/avatar-4.jpg";
import avatar6 from "../../assets/images/users/avatar-6.jpg";
```

## 📚 Component Breakdown

### EmailSideBar

- **State Management**:
  - `modal`: A boolean state to handle the visibility of the compose email modal.

- **Render Elements**:
  - **Navigation Links**: Links to different email sections.
  - **Labels**: Allows categorization of emails for easier management.
  - **Chat Section**: Displays recent chats with avatars and brief messages.
  - **Compose Button**: Triggers the modal to compose a new email.

- **Modal for Email Composition**:
  - **Includes**: To field, subject field, and a rich-text editor for email body.

```javascript
const EmailSideBar = () => {
    const [modal, setmodal] = useState(false);
    return (
        <React.Fragment>
            {/* Render Email Sidebar Content */}
            {/* Render Compose Modal */}
        </React.Fragment>
    );
};
```

## 🎯 Key Functionalities

### 1. Navigation Links
- Each link is equipped with an icon, text, and a count of items (e.g., number of emails in the inbox).
  
### 2. Labels
- Uses icons and colors to differentiate between email categories.

### 3. Chat Section
- Displays a list of recent chat contacts with their avatars and last message snippets.

### 4. Modal for New Email
- Activated by the "Compose" button, allowing the user to write and send new emails using a rich-text editor.

## 🔍 How It Works

- **Navigation**: Users can click on different sections to view their emails.
- **Modal Toggle**: The `setmodal` state controls the visibility of the email composition modal.
- **Chat**: Provides quick access to recent chats without leaving the email interface.

## 📦 Dependencies

- **React**: Core library for building the component.
- **Reactstrap**: Provides Bootstrap components for a responsive design.
- **React-Draft-Wysiwyg**: A rich text editor for composing emails.
- **React Router**: For handling navigation between different parts of the email app.

---

## 📝 Conclusion

The `email-sidebar.js` component is a versatile sidebar for an email application. It enhances user experience by providing easy navigation, quick chat access, and a convenient interface for composing new emails. Its modular structure and integration with popular libraries like Reactstrap and React-Draft-Wysiwyg make it a robust choice for modern web applications.

# 📧 Email Template Alert Documentation

**File:** `email-template-alert.js`

## 🌟 Overview

The `email-template-alert.js` file contains a React component that renders an alert email template. This template is typically used to notify users about important updates or warnings regarding their account status. The component is styled to ensure responsiveness and visual appeal, using Reactstrap components and custom styles. 

## 🗂 Index

- [Component Structure](#-component-structure)
- [Key Components](#-key-components)
- [Styling](#-styling)
- [Usage](#-usage)

## 📑 Component Structure

The `EmailAlertTemplte` component is a functional React component that uses Reactstrap for layout and styling. Below is a high-level structure of the component:

```jsx
import React from "react";
import { Row, Col } from "reactstrap";
import { Link } from "react-router-dom";
import Breadcrumbs from "../../components/Common/Breadcrumb";

const EmailAlertTemplte = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Email Template" breadcrumbItem="Alert Email" />
        <Row className="email-template">
          <Col md={12}>
            <table className="body-wrap" style={{ /* styles */ }}>
              <tbody>
                <tr>
                  <td></td>
                  <td className="container" width="600">
                    <div className="content">
                      <table className="main" width="100%">
                        <tbody>
                          <tr>
                            <td className="alert alert-warning" align="center">
                              Warning: You're approaching your limit. Please upgrade.
                            </td>
                          </tr>
                          <tr>
                            <td className="content-wrap">
                              <table width="100%">
                                <tbody>
                                  <tr>
                                    <td className="content-block">
                                      You have <strong>1 free report</strong> remaining.
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block">
                                      Add your credit card now to upgrade your account.
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block">
                                      <Link to="#" className="btn-primary">
                                        Upgrade my account
                                      </Link>
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block">
                                      Thanks for choosing <b>Qovex</b> Admin.
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block">
                                      <b>Qovex</b> <p>Support Team</p>
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block" style={{ textAlign: "center" }}>
                                      © {new Date().getFullYear()} Qovex
                                    </td>
                                  </tr>
                                </tbody>
                              </table>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
};

export default EmailAlertTemplte;
```

## 🔑 Key Components

- **React.Fragment**: Used to wrap the component without adding extra nodes to the DOM.
- **Breadcrumbs**: Displays the navigation path to the current email template page.
- **Row and Col (Reactstrap)**: Utilized for responsive grid layout.
- **Table Structure**: Organizes email content with a main email body and alert message.
- **Link (React Router)**: Provides navigation functionality for buttons and links.

## 🎨 Styling

The component uses inline styles along with CSS classes to achieve a clean and modern design. Key styling elements include:

- **Background Colors**: Light grey (`#f6f6f6`) for the overall background and white (`#fff`) for the main content area.
- **Alert Box**: A prominent blue alert box (`#556ee6`) with white text, for warning messages.
- **Buttons**: Styled with a green background (`#34c38f`) for noticeable call-to-action buttons.

## 🛠 Usage

This component is designed to be used as a part of an email template system within a web application. It can be integrated into dashboards or administrative panels where email alerts are required to notify users about account status or other critical updates.

```jsx
import EmailAlertTemplte from './path/to/email-template-alert';

// Usage within a parent component
const ParentComponent = () => {
  return (
    <div>
      {/* Other components */}
      <EmailAlertTemplte />
    </div>
  );
};
```

This documentation should help developers understand the structure and usage of the `email-template-alert.js` component, ensuring seamless integration and modification as needed.

# 📄 Email Template Billing Component Documentation

This document provides a detailed overview of the `email-template-billing.js` file. This file is a React component designed to render a billing email template using the Reactstrap library for UI components and styling.

---

## 📚 Table of Contents

1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Key Elements](#key-elements)
4. [Styling](#styling)
5. [Usage](#usage)
6. [Dependencies](#dependencies)

---

## Overview

The **EmailTemplateBilling** component is a functional React component used for generating a billing email template. The template includes a breadcrumb for navigation, a billing invoice summary with itemized charges, and a summary of contact information.

### 📦 Component Purpose

- **Display Billing Information**: Showcases a list of items billed along with their prices.
- **Enhance User Interface**: Provides a visually appealing billing email template.
- **Reusable UI Component**: Can be used in various parts of an application where billing information needs to be displayed in an email format.

---

## Component Structure

Here is the structural breakdown of the component:

```jsx
import React from "react";
import { Row, Col } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";

const EmailTemplateBilling = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="Email Template" breadcrumbItem="Billing Email" />
        <Row className="email-template">
          <Col md="12">
            <table className="body-wrap" style={bodyWrapStyle} bgcolor="#f6f6f6">
              <tbody>
                <tr>
                  <td></td>
                  <td className="container" width="600" valign="top">
                    <div className="content" style={contentStyle}>
                      <table className="main" width="100%" style={mainTableStyle}>
                        <tbody>
                          <tr>
                            <td className="content-wrap aligncenter" valign="top" style={contentWrapStyle}>
                              <table width="100%">
                                <tbody>
                                  <tr>
                                    <td className="content-block" valign="top">
                                      <h2 className="aligncenter" style={headingStyle}>
                                        Thanks for using <b>Qovex</b>.
                                      </h2>
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block aligncenter" valign="top" style={alignCenterStyle}>
                                      <table className="invoice" style={invoiceStyle}>
                                        <tbody>
                                          <tr>
                                            <td valign="top">
                                              <b>Company Name</b> <br />
                                              Invoice #6521 <br />
                                              August 01 2017
                                            </td>
                                          </tr>
                                          <tr>
                                            <td valign="top">
                                              <table className="invoice-items" cellPadding="0" cellSpacing="0" style={invoiceItemsStyle}>
                                                <tbody>
                                                  <tr>
                                                    <td valign="top">BS-200 (1 Pc)</td>
                                                    <td className="alignright" valign="top">$10.99</td>
                                                  </tr>
                                                  <tr>
                                                    <td valign="top">BS-400 (2 Pcs)</td>
                                                    <td className="alignright" valign="top">$60.00</td>
                                                  </tr>
                                                  <tr>
                                                    <td valign="top">BS-1000 (1 Pc)</td>
                                                    <td className="alignright" valign="top">$600.00</td>
                                                  </tr>
                                                  <tr className="total">
                                                    <td className="alignright" valign="top">Total</td>
                                                    <td className="alignright" valign="top">$670.99</td>
                                                  </tr>
                                                </tbody>
                                              </table>
                                            </td>
                                          </tr>
                                        </tbody>
                                      </table>
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block aligncenter" valign="top">
                                      Qovex Inc. 2896 Howell Rd, Russellville, AR, 72823
                                    </td>
                                  </tr>
                                  <tr>
                                    <td className="content-block" valign="top">
                                      © {new Date().getFullYear()} Qovex
                                    </td>
                                  </tr>
                                </tbody>
                              </table>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
};

export default EmailTemplateBilling;
```

---

## Key Elements

- **Breadcrumbs**: Provides navigation within the email templates.
- **Body Table**: The main structure holding the email content.
- **Invoice Table**: Displays detailed billing information including item descriptions and prices.

### 🧾 Invoice Details

The email includes itemized details, such as:

| Item          | Quantity | Price  |
|---------------|----------|--------|
| **BS-200**    | 1 Pc     | $10.99 |
| **BS-400**    | 2 Pcs    | $60.00 |
| **BS-1000**   | 1 Pc     | $600.00|
| **Total**     |          | $670.99|

---

## Styling

The component uses inline styles for layout and design. Key style properties include:

- **Font Family**: `Helvetica Neue, Helvetica, Arial, sans-serif`
- **Background Color**: `#f6f6f6` for the body wrap
- **Text Alignment**: Centered alignment for headings and invoice summary
- **Borders**: Used for invoice table and total calculation

---

## Usage

To use the `EmailTemplateBilling` component, simply import and include it within a parent component, ensuring that necessary dependencies like `reactstrap` are installed and configured.

```jsx
import EmailTemplateBilling from './path-to/email-template-billing';

// Usage within another component
function App() {
  return (
    <div>
      <EmailTemplateBilling />
    </div>
  );
}
```

---

## Dependencies

The component relies on the following:

- **React**: For building the component structure.
- **Reactstrap**: To utilize Bootstrap components in React.
- **Breadcrumbs Component**: Custom component for navigation breadcrumbs.

---

This provides a comprehensive understanding of the **EmailTemplateBilling** component, its structure, purpose, and how to integrate it within a React application.

# 📄 Documentation for `email-toolbar.js`

## 📋 Index
1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Core Functionality](#core-functionality)
4. [Code Explanation](#code-explanation)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

---

## Introduction

The `email-toolbar.js` file contains a React component named **`EmailToolbar`**. This component provides a set of toolbar actions commonly used in email applications, such as moving emails to folders, tagging, and additional actions like marking emails as unread or important. This toolbar enhances user interaction with the email interface by providing quick access to common functionalities.

---

## Component Overview

The `EmailToolbar` component utilizes React and Reactstrap to create a responsive and interactive email toolbar. It leverages dropdown menus and buttons to offer various email management actions.

### Key Features:
- **Inbox Management**: Buttons for trashing, marking important, and other inbox actions.
- **Dropdown Menus**: Organize emails into folders, add tags, and access more features.
- **Responsive Design**: Adapts to different screen sizes using Bootstrap classes.

---

## Core Functionality

The toolbar allows users to perform quick actions on emails like:
- **Move to Folder**: Organize emails by moving them to specific folders.
- **Add Tags**: Tag emails for better categorization.
- **Additional Actions**: Such as marking as unread, adding stars, and more.

---

## Code Explanation

```javascript
import React, { useState } from "react";
import { Button, Dropdown, DropdownToggle, DropdownMenu, DropdownItem } from "reactstrap";

const EmailToolbar = () => {
  // State management for dropdown menus
  const [folder_Menu, setfolder_Menu] = useState(false);
  const [tag_Menu, settag_Menu] = useState(false);
  const [more_Menu, setmore_Menu] = useState(false);

  return (
    <React.Fragment>
      <div className="btn-toolbar p-3" role="toolbar">
        <div className="btn-group me-2 mb-2 mb-sm-0">
          {/* Action buttons */}
          <Button type="button" color="primary" className="waves-light waves-effect">
            <i className="fa fa-inbox" />
          </Button>
          <Button type="button" color="primary" className="waves-light waves-effect">
            <i className="fa fa-exclamation-circle" />
          </Button>
          <Button type="button" color="primary" className="waves-light waves-effect">
            <i className="far fa-trash-alt" />
          </Button>
        </div>

        {/* Dropdown for folders */}
        <Dropdown isOpen={folder_Menu} toggle={() => { setfolder_Menu(!folder_Menu) }} className="btn-group me-2 mb-2 mb-sm-0">
          <DropdownToggle className="btn btn-primary waves-light waves-effect dropdown-toggle" tag="i">
            <i className="fa fa-folder" /> <i className="mdi mdi-chevron-down ms-1" />
          </DropdownToggle>
          <DropdownMenu>
            <DropdownItem to="#">Updates</DropdownItem>
            <DropdownItem to="#">Social</DropdownItem>
            <DropdownItem to="#">Team Manage</DropdownItem>
          </DropdownMenu>
        </Dropdown>

        {/* Dropdown for tags */}
        <Dropdown isOpen={tag_Menu} toggle={() => { settag_Menu(!tag_Menu) }} className="btn-group me-2 mb-2 mb-sm-0">
          <DropdownToggle className="btn btn-primary waves-light waves-effect dropdown-toggle" tag="i">
            <i className="fa fa-tag" /> <i className="mdi mdi-chevron-down ms-1" />
          </DropdownToggle>
          <DropdownMenu>
            <DropdownItem to="#">Updates</DropdownItem>
            <DropdownItem to="#">Social</DropdownItem>
            <DropdownItem to="#">Team Manage</DropdownItem>
          </DropdownMenu>
        </Dropdown>

        {/* Dropdown for more actions */}
        <Dropdown isOpen={more_Menu} toggle={() => { setmore_Menu(!more_Menu) }} className="btn-group me-2 mb-2 mb-sm-0">
          <DropdownToggle className="btn btn-primary waves-light waves-effect dropdown-toggle" tag="div">
            More <i className="mdi mdi-dots-vertical ms-2" />
          </DropdownToggle>
          <DropdownMenu>
            <DropdownItem to="#">Mark as Unread</DropdownItem>
            <DropdownItem to="#">Mark as Important</DropdownItem>
            <DropdownItem to="#">Add to Tasks</DropdownItem>
            <DropdownItem to="#">Add Star</DropdownItem>
            <DropdownItem to="#">Mute</DropdownItem>
          </DropdownMenu>
        </Dropdown>
      </div>
    </React.Fragment>
  );
};

export default EmailToolbar;
```

### Explanation:
- **State Management**: Uses React hooks (`useState`) to manage the state of dropdown menus (folder, tag, and more).
- **Button Group**: Contains buttons for common email actions: Inbox, Important, and Trash.
- **Dropdowns**: Each dropdown menu provides options for organizing and tagging emails, as well as additional actions.

---

## Usage

To incorporate the `EmailToolbar` component into your email application:
1. Import the component:
   ```javascript
   import EmailToolbar from './email-toolbar';
   ```
2. Use it within your email interface as needed:
   ```jsx
   <EmailToolbar />
   ```

This component is ideal for integration within an email client interface where toolbar functionalities are required.

---

## Conclusion

The `EmailToolbar` component is a versatile and essential tool for managing emails efficiently. With its intuitive design and functionality, it enhances the user experience by providing quick access to common email actions. By using React and Reactstrap, it ensures responsiveness and ease of use across various devices.