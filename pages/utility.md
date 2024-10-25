# Documentation for `pages-timeline.js` 📜

This document provides detailed information about the `pages-timeline.js` file, which is a part of a React application. This component is designed to display a timeline with various events encapsulated in a visually appealing manner.

---

## Overview

The `PagesTimeline` component is a React functional component that utilizes the Reactstrap library for layout structuring. The component displays a series of events within a timeline format, each annotated with different dates and descriptions.

### Key Features

- **Breadcrumbs Navigation**: Provides a breadcrumb trail for navigation.
- **Responsive Timeline**: Displays events in a structured timeline format.
- **Event Details**: Each event contains a date, title, description, and optional images and actions.
- **Styling**: Utilizes Bootstrap classes for styling and layout.

---

## Code Explanation

```javascript
import React from "react";
import { Row, Col } from "reactstrap";
import { Link } from "react-router-dom";

// Import Breadcrumb
import Breadcrumbs from "../../components/Common/Breadcrumb";

// Import Images
import img2 from "../../assets/images/small/img-2.jpg";
import img5 from "../../assets/images/small/img-5.jpg";

const PagesTimeline = () => {
    return (
        <React.Fragment>
            <div className="page-content">
                {/* Render Breadcrumbs */}
                <Breadcrumbs title="Pages" breadcrumbItem="Timeline" />
                <Row>
                    <Col lg={12}>
                        <div className="card">
                            <div className="card-body">
                                <div className="timeline-count p-4">
                                    <Row>
                                        {/* Timeline Event 1 */}
                                        <div className="timeline-box col-lg-4">
                                            <div className="timeline-spacing">
                                                <div className="item-lable bg-primary rounded">
                                                    <p className="text-center text-white">April, 12</p>
                                                </div>
                                                <div className="timeline-line active">
                                                    <div className="dot bg-primary"></div>
                                                </div>
                                                <div className="vertical-line">
                                                    <div className="wrapper-line bg-light"></div>
                                                </div>
                                                <div className="bg-light p-4 rounded mx-3">
                                                    <h5>Timeline Event One</h5>
                                                    <p className="text-muted mt-1 mb-0">
                                                        Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium...
                                                    </p>
                                                </div>
                                            </div>
                                        </div>
                                        {/* Timeline Event 2 */}
                                        <div className="timeline-box col-lg-4">
                                            <div className="timeline-spacing">
                                                <div className="item-lable bg-primary rounded">
                                                    <p className="text-center text-white">April, 13</p>
                                                </div>
                                                <div className="timeline-line active">
                                                    <div className="dot bg-primary"></div>
                                                </div>
                                                <div className="vertical-line">
                                                    <div className="wrapper-line bg-light"></div>
                                                </div>
                                                <div className="bg-light p-4 rounded mx-3">
                                                    <h5>Timeline Event Two</h5>
                                                    <p className="text-muted mt-1 mb-0">
                                                        Vivamus ultrices massa tellus, sed convallis urna interdum eu...
                                                    </p>
                                                </div>
                                            </div>
                                        </div>
                                        {/* Timeline Event 3 */}
                                        <div className="timeline-box col-lg-4">
                                            <div className="timeline-spacing">
                                                <div className="item-lable bg-primary rounded">
                                                    <p className="text-center text-white">April, 26</p>
                                                </div>
                                                <div className="timeline-line active">
                                                    <div className="dot bg-primary"></div>
                                                </div>
                                                <div className="vertical-line">
                                                    <div className="wrapper-line bg-light"></div>
                                                </div>
                                                <div className="bg-light p-4 rounded mx-3">
                                                    <h5>Timeline Event Three</h5>
                                                    <p className="text-muted mt-1">
                                                        At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium...
                                                    </p>
                                                    <img src={img2} alt="" className="img-fluid rounded me-3" width="100" />
                                                    <img src={img5} alt="" className="img-fluid rounded" width="100" />
                                                </div>
                                            </div>
                                        </div>
                                    </Row>
                                    <Row>
                                        {/* Timeline Event 4 */}
                                        <div className="timeline-box col-lg-4">
                                            <div className="timeline-spacing">
                                                <div className="item-lable bg-primary rounded">
                                                    <p className="text-center text-white">April, 27</p>
                                                </div>
                                                <div className="timeline-line active">
                                                    <div className="dot bg-primary"></div>
                                                </div>
                                                <div className="vertical-line">
                                                    <div className="wrapper-line bg-light"></div>
                                                </div>
                                                <div className="bg-light text-start p-4 rounded mx-3">
                                                    <h5>Timeline Event End</h5>
                                                    <p className="text-muted mb-0">
                                                        Suspendisse tempor porttitor elit non maximus...
                                                    </p>
                                                </div>
                                            </div>
                                        </div>
                                        {/* Timeline Event 5 */}
                                        <div className="timeline-box col-lg-4">
                                            <div className="timeline-spacing">
                                                <div className="item-lable bg-primary rounded">
                                                    <p className="text-center text-white">April, 28</p>
                                                </div>
                                                <div className="timeline-line active">
                                                    <div className="dot bg-primary"></div>
                                                </div>
                                                <div className="vertical-line">
                                                    <div className="wrapper-line bg-light"></div>
                                                </div>
                                                <div className="bg-light text-start p-4 rounded mx-3">
                                                    <h5>Timeline Event Four</h5>
                                                    <p className="text-muted mb-0">
                                                        Excepturi, obcaecati, quisquam id molestias eaque asperiores...
                                                        <Link to="#">Read more</Link>
                                                    </p>
                                                </div>
                                            </div>
                                        </div>
                                        {/* Timeline Event 6 */}
                                        <div className="timeline-box col-lg-4">
                                            <div className="timeline-spacing">
                                                <div className="item-lable bg-primary rounded">
                                                    <p className="text-center text-white">April, 30</p>
                                                </div>
                                                <div className="timeline-line active">
                                                    <div className="dot bg-primary"></div>
                                                </div>
                                                <div className="vertical-line">
                                                    <div className="wrapper-line bg-light"></div>
                                                </div>
                                                <div className="bg-light text-start p-4 rounded mx-3">
                                                    <h5>Timeline Event Five</h5>
                                                    <p className="text-muted mb-0">
                                                        printing and typesetting industry. Lorem Ipsum has been the industry's standard...
                                                    </p>
                                                    <button type="button" className="btn btn-info btn-rounded waves-effect waves-light mt-4">
                                                        See more detail
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </Row>
                                </div>
                            </div>
                        </div>
                    </Col>
                </Row>
            </div>
        </React.Fragment>
    );
};

export default PagesTimeline;
```

---

## Components Used

- **Breadcrumbs**: A component to display breadcrumb navigation.
- **Row & Col (Reactstrap)**: For layout purposes, defining rows and columns.
- **Link (React Router)**: For navigation links within the timeline events.

---

## Timeline Structure

| Date       | Event Title        | Description                | Additional Elements         |
|------------|--------------------|----------------------------|-----------------------------|
| April, 12  | Timeline Event One | Brief description of event |                             |
| April, 13  | Timeline Event Two | Brief description of event |                             |
| April, 26  | Timeline Event Three | Brief description of event with images | Two images displayed    |
| April, 27  | Timeline Event End | Brief description of event |                             |
| April, 28  | Timeline Event Four | Brief description of event with read more link | "Read more" link      |
| April, 30  | Timeline Event Five | Brief description of event | "See more detail" button    |

---

## Styling and Layout

The timeline uses a combination of Bootstrap classes to ensure a clean, responsive design. Events are displayed within a card, each section with its own color-coded label, timeline line, and description box.

- **`bg-primary`**: Used for labeling and timeline dots.
- **`bg-light`**: Used for the background of the event description box.
- **`p-4`**: Adds padding to the event description box.
- **`rounded`**: Gives rounded corners to elements.

---

## Usage

To integrate the `PagesTimeline` component into your application, you can import and include it within your routing or as part of a parent component. This component effectively organizes information in a chronological order, making it ideal for showcasing historical data or step-by-step processes.

```javascript
import PagesTimeline from './path-to-component/pages-timeline';

function App() {
  return (
    <div>
      <PagesTimeline />
    </div>
  );
}
```

---

## Conclusion

The `PagesTimeline` component is a visually structured way to present events chronologically within a React application. It leverages Reactstrap for responsive design and provides a user-friendly interface for navigating through events.

# Documentation for `pages-starter.js` 📄

The `pages-starter.js` file is a simple React component that serves as a starter template for a page within a React application. This component primarily sets up a basic structure with a breadcrumb navigation feature. Below, we will dive into the details of how this component is structured and what it is intended for.

## Table of Contents
- [Overview](#overview)
- [Component Structure](#component-structure)
- [Code Explanation](#code-explanation)
- [Usage](#usage)
- [Dependencies](#dependencies)

## Overview

The **PagesStarter** component is designed to provide a basic layout for a new page in a React application. It includes a breadcrumb component that helps users navigate through the application. This component acts as a placeholder or template that can be expanded upon to create a fully-fledged page.

## Component Structure

The component is structured as follows:

```jsx
const PagesStarter = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        {/* Render Breadcrumbs */}
        <Breadcrumbs title="Pages" breadcrumbItem="Starter Page" />
      </div>
    </React.Fragment>
  )
}

export default PagesStarter
```

## Code Explanation

### Imports

- **React**: The core library for building user interfaces in JavaScript.
- **Breadcrumbs**: A component that is imported from a common components directory. It is used to display the breadcrumb navigation.

### Component Definition

- **PagesStarter**: This is a functional component defined using an arrow function. It utilizes React Fragments (`<React.Fragment>`) to group a list of children without adding extra nodes to the DOM.

### JSX Structure

- **div.page-content**: This `div` acts as a container for the page's content.
- **Breadcrumbs**: The breadcrumb component is rendered within the page content. It takes two props:
  - `title`: A string that serves as the main title for the breadcrumb.
  - `breadcrumbItem`: A string that represents the current page or item in the breadcrumb trail.

### Export

- The component is exported as a default export, making it available for import in other parts of the application.

## Usage

This component is used as a basic template for creating new pages within an application. Developers can use this starter component to quickly scaffold out new pages and add additional content or functionality as needed.

## Dependencies

- **React**: Ensure that React is installed in the project to use this component.
- **Breadcrumbs**: This component relies on a Breadcrumbs component located at `../../components/Common/Breadcrumb`. Ensure that this path is correct and that the Breadcrumbs component is available.

## Conclusion

The `pages-starter.js` component is a simple, boilerplate component that can be used to kickstart the creation of new pages in a React application. It provides a clean structure with a breadcrumb feature to enhance navigation within the app. This simplicity makes it easy for developers to expand and customize as needed.

# Documentation for `pages-maintenance.js`

**File Purpose:**  
The `pages-maintenance.js` file is a React component designed to display a maintenance page for a website. This page informs users that the site is currently under maintenance and provides additional information and support contact details.

---

## Table of Contents
- [Key Features](#key-features)
- [Component Structure](#component-structure)
- [Code Explanation](#code-explanation)
- [Usage](#usage)
- [Dependencies](#dependencies)

---

## Key Features
- **Maintenance Notice:** Displays a message indicating that the site is under maintenance.
- **Responsive Design:** Adjusts layout based on screen size using Bootstrap's grid system.
- **Information Cards:** Provides additional information on why the site is down, expected downtime, and support contact.
- **Navigation Button:** Offers a quick link back to the homepage.

---

## Component Structure

```jsx
import React, { useEffect } from "react";
import { Link } from "react-router-dom";
import { CardBody, Container, Row, Col, Card } from "reactstrap";

// Import Images
import logo from "../../assets/images/logo-dark.png";
import maintenance from "../../assets/images/maintenance.png";

const PagesMaintenance = () => {
    // Component logic goes here
    return (
        <React.Fragment>
            {/* JSX goes here */}
        </React.Fragment>
    );
}

export default PagesMaintenance;
```

---

## Code Explanation

### useEffect Hook
- **Purpose:** 
  - Adds a class `authentication-bg` to the body element when the component mounts to style the background appropriately for the maintenance page.
  - Removes the class when the component unmounts to prevent style leakage.

```jsx
useEffect(() => {
    document.body.className = "authentication-bg";
    return function cleanup() {
        document.body.className = "";
    };
}, []);
```

### JSX Structure

- **Navigation Button:** 
  - Provides a home icon button linking back to the main page.
  ```jsx
  <div className="home-btn d-none d-sm-block">
      <Link to="/" className="text-dark"><i className="fas fa-home h2"></i></Link>
  </div>
  ```

- **Main Container:** 
  - Contains the structured layout of the maintenance message and supportive information.
  - Utilizes `reactstrap` components for responsive design.

```jsx
<Container>
    <Row>
        <div className="col-12 text-center">
            <div className="home-wrapper">
                <div className="mb-5">
                    <Link to="/"> <img src={logo} alt="" height="24" /> </Link>
                </div>
                <Row className="justify-content-center">
                    <Col sm={4}>
                        <div className="maintenance-img">
                            <img src={maintenance} alt="" className="img-fluid mx-auto d-block" />
                        </div>
                    </Col>
                </Row>
                <h3 className="mt-5">Site is Under Maintenance</h3>
                <p>If several languages coalesce, the grammar of the resulting language is more simple and <br /> regular than that of the individual languages. </p>
                <Row>
                    { /* Additional Information Cards */ }
                </Row>
            </div>
        </div>
    </Row>
</Container>
```

- **Information Cards:**
  - Provide context on the maintenance, expected downtime, and support contact.
  - Each card includes a title and a descriptive paragraph.
  
```jsx
<Card className="mt-4 maintenance-box">
    <CardBody>
        <h5 className="font-size-15 text-uppercase">Why is the Site Down?</h5>
        <p className="text-muted mb-0">There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration.</p>
    </CardBody>
</Card>
```

---

## Usage

To use this component, integrate it into your React application where you handle routing. This could be displayed under certain conditions, such as when the site is undergoing scheduled maintenance.

---

## Dependencies

- **Reactstrap:** Utilized for responsive layout and styling via Bootstrap.
- **React-router-dom:** Provides routing functionality and navigation links.
- **Font Awesome:** Used for the home icon in the navigation button.

---

> **Note:** Ensure the images (`logo-dark.png` and `maintenance.png`) are located in the specified directory to avoid broken image links on the page.

This page serves as a friendly and informative way to communicate with users about site unavailability, expected duration, and support contact information.

# Documentation for `pages-pricing.js` 📄

## Overview

The `pages-pricing.js` file is part of a React application and is responsible for rendering a pricing page that displays different pricing plans using cards. This file utilizes components from the Reactstrap library for styling and structure, and it imports a custom `Breadcrumbs` component for navigation purposes.

## Table of Contents

1. [Imports](#imports)
2. [Pricing Data Structure](#pricing-data-structure)
3. [Component Breakdown](#component-breakdown)
4. [Usage](#usage)
5. [PropTypes](#proptypes)
6. [Conclusion](#conclusion)

## Imports

```javascript
import React from "react";
import { Row, Col } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import CardPricing from "./card-pricing";
```

### Imported Modules

1. **React**: The core library for building user interfaces.
2. **Reactstrap Components**: 
    - `Row` and `Col`: Used for grid layout.
3. **Breadcrumbs**: A custom component to display breadcrumb navigation.
4. **CardPricing**: A custom component used to display individual pricing cards.

## Pricing Data Structure

The file contains an array of pricing objects that define the properties for each pricing plan:

```javascript
const pricings = [
  {
    id: 1,
    title: "Starter",
    description: "Neque quis est",
    icon: "bx-walk",
    price: "19",
    duration: "Per month",
    link: "",
    features: [
      { title: "Unlimited access to licence" },
      { title: "GB Storage" },
      { title: "No Domain" },
      { title: "SEO optimization" },
      { title: "Unlmited Users" },
      { title: "500 GB Bandwidth" },
    ],
  },
  // More pricing objects...
];
```

### Attributes

- **id**: Unique identifier for the pricing plan.
- **title**: Name of the pricing plan.
- **description**: Brief description of the plan.
- **icon**: Icon class for the plan's illustration.
- **price**: Cost of the plan.
- **duration**: Time period for the given price.
- **link**: URL for the sign-up page (currently empty).
- **features**: List of features included in the pricing plan.

## Component Breakdown

### `PagesPricing` Component

The main component of this file, responsible for rendering the pricing page.

#### Structure

- **Breadcrumbs**: Displays navigation links for the page.
- **Title and Subtitle**: Provides an introduction to the pricing options.
- **Pricing Cards**: Iterates over the `pricings` array and renders a `CardPricing` component for each pricing plan.

#### JSX Layout

```jsx
<React.Fragment>
  <div className="page-content">
    <Breadcrumbs title="Pages" breadcrumbItem="Pricing" />
    <Row className="justify-content-center">
      <Col lg={6}>
        <div className="text-center mb-5">
          <h4>Choose your Pricing plan</h4>
          <p className="text-muted">
            To achieve this, it would be necessary to have uniform grammar, pronunciation and more common words If several languages coalesce
          </p>
        </div>
      </Col>
    </Row>
    <Row>
      {pricings.map((pricing, key) => (
        <CardPricing pricing={pricing} key={"_pricing_" + key} />
      ))}
    </Row>
  </div>
</React.Fragment>
```

## Usage

The `PagesPricing` component is used within a React application to display pricing options. The component is structured to be responsive and styled using Bootstrap classes through Reactstrap.

## PropTypes

The `CardPricing` component, which is used to render each pricing card, expects a prop type of an object for its `pricing` prop. This ensures that the component receives the correct data structure to render each pricing plan.

```javascript
CardPricing.propTypes = {
  pricing: PropTypes.object
};
```

## Conclusion

The `pages-pricing.js` file provides a clean and structured way to display pricing plans on a web page. It leverages React components and Reactstrap for styling, ensuring a responsive and visually appealing presentation. The data-driven approach using the `pricings` array allows for easy addition or modification of pricing plans.

# Documentation for `pages-faqs.js`

This document provides a detailed explanation of the `pages-faqs.js` file, which is a React component used to render a Frequently Asked Questions (FAQ) page. It includes tabs for different categories of questions such as General Questions, Privacy Policy, and Support.

## 📄 **File Overview**

- **Filename**: `pages-faqs.js`
- **Purpose**: To provide a structured FAQ page with navigable tabs for different categories of questions.
- **Libraries Used**:
  - `React`: For building the component.
  - `reactstrap`: For UI components like Card, Row, Col, etc.
  - `classnames`: To conditionally join class names.
  - `react-router-dom`: For navigation (imported but not used in this component).

## 🗂️ **Index**

1. [Component Description](#component-description)
2. [Key Features](#key-features)
3. [Code Explanation](#code-explanation)
4. [Prop Types](#prop-types)
5. [Usage](#usage)
6. [Styling](#styling)

## 📘 **Component Description**

The `PagesFaqs` component is designed to display FAQs categorized into three main tabs:

- **General Questions**
- **Privacy Policy**
- **Support**

Each tab contains a list of questions and answers, which can be navigated using the tab navigation provided on the page.

## ✨ **Key Features**

- **Tabbed Navigation**: Allows users to switch between different categories of FAQs.
- **Responsive Design**: Utilizes `reactstrap` components to ensure responsiveness.
- **Dynamic Content Rendering**: Renders different content based on the active tab.

## 🧩 **Code Explanation**

### Import Statements

```javascript
import React, { useState } from "react";
import { Row, Col, Card, CardBody, CardTitle, Nav, NavItem, NavLink, TabContent, TabPane } from "reactstrap";
import classnames from "classnames";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

- **React and Hooks**: The component uses `React` and the `useState` hook for managing the active tab state.
- **Reactstrap Components**: Used for layout and styling.
- **classnames**: Utilized for managing active tab classes.
- **Breadcrumbs**: A component for navigation breadcrumbs.

### State Management

```javascript
const [activeTab, setactiveTab] = useState("1");
```

- **activeTab**: A state hook to manage which tab is currently active.

### Render Function

The component returns a structured layout with breadcrumbs and a tabbed FAQ section:

```javascript
<React.Fragment>
  <div className="page-content">
    <Breadcrumbs title="Pages" breadcrumbItem="FAQs" />
    <div className="checkout-tabs">
      <Row>
        <Col lg="2">
          <Nav className="flex-column" pills>
            {/* Navigation Items for Tabs */}
          </Nav>
        </Col>
        <Col lg="10">
          <Card>
            <CardBody>
              <TabContent activeTab={activeTab}>
                <TabPane tabId="1">
                  {/* General Questions Content */}
                </TabPane>
                <TabPane tabId="2">
                  {/* Privacy Policy Content */}
                </TabPane>
                <TabPane tabId="3">
                  {/* Support Content */}
                </TabPane>
              </TabContent>
            </CardBody>
          </Card>
        </Col>
      </Row>
    </div>
  </div>
</React.Fragment>
```

### Tab and Content Structure

- **Nav and NavItems**: Each `NavItem` changes the active tab when clicked.
- **TabContent and TabPane**: Contains the content for each tab, displayed based on the `activeTab` state.

## 📦 **Prop Types**

This component does not utilize PropTypes as it is a self-contained component and does not receive any props from parent components.

## 🛠️ **Usage**

To use this component, simply import it and include it in your JSX code. Ensure that Reactstrap and classnames are installed in your project.

```javascript
import PagesFaqs from './pages-faqs';

// Usage in a parent component
<PagesFaqs />
```

## 🎨 **Styling**

The component relies on Bootstrap and custom styles from `reactstrap`. Ensure that Bootstrap CSS is properly linked in your project for the component to render correctly with its intended design.

## ✅ **Conclusion**

The `PagesFaqs` component provides a clean and structured way to present FAQs to users with easy navigation through different categories. Its use of Reactstrap ensures that the component is both responsive and visually appealing.

# Documentation for `pages-comingsoon.js`

## Overview

The `pages-comingsoon.js` file is a React component designed to serve as a "Coming Soon" page for an application. This page typically indicates that a feature, service, or website is under construction and will be available soon. It includes a countdown timer to a specified date, prominently displaying the remaining time until the launch.

## Table of Contents
1. [Components and Libraries Used](#components-and-libraries-used)
2. [File Structure](#file-structure)
3. [Functionality](#functionality)
4. [Code Walkthrough](#code-walkthrough)
5. [Usage](#usage)

---

## Components and Libraries Used

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library that provides Bootstrap 4 components as React components.
- **React Countdown**: A component to render a countdown timer.
- **Images**: Utilizes local assets for logos and coming soon images.

```javascript
import React, { useEffect } from "react";
import { Container, Row, Col } from "reactstrap";
import Countdown from "react-countdown";
```

## File Structure

The component is structured as follows:

- **Imports**: External libraries and images.
- **Component Definition**: A functional React component.
- **useEffect Hook**: To manage side-effects, specifically altering the `body` class.
- **Renderer Function**: For the countdown timer.
- **Return Statement**: JSX to render the component UI.

## Functionality

- **Countdown Timer**: Displays the time remaining until a specified date, broken down into days, hours, minutes, and seconds.
- **Responsive Design**: Utilizes Bootstrap's grid system to ensure proper alignment and responsiveness.
- **UI Components**: Includes a logo, a coming soon image, and a countdown timer.

## Code Walkthrough

### 1. Component Initialization

The component is defined as a functional component with `useEffect` to set and clean up the body class name:

```javascript
const PagesComingsoon = () => {
    useEffect(() => {
        document.body.className = "authentication-bg";
        return function cleanup() {
            document.body.className = "";
        };
    });
```

### 2. Countdown Renderer

Defines how the countdown is displayed:

```javascript
const renderer = ({ days, hours, minutes, seconds, completed }) => {
    if (completed) {
        return <span>You are good to go!</span>;
    } else {
        return (
            <>
                <div className="coming-box">{days} <span>Days</span></div>
                <div className="coming-box">{hours} <span>Hours</span></div>
                <div className="coming-box">{minutes} <span>Minutes</span></div>
                <div className="coming-box">{seconds} <span>Seconds</span></div>
            </>
        );
    }
};
```

### 3. JSX Structure

The JSX returned by the component includes layout and styling for the "Coming Soon" page:

```javascript
return (
    <React.Fragment>
        <div className="home-btn d-none d-sm-block">
            <a href="/" className="text-white"><i className="fas fa-home h2"></i></a>
        </div>
        <div className="my-5 pt-sm-5">
            <Container>
                <Row>
                    <Col lg={12}>
                        <div className="text-center">
                            <a href="/" className="d-block auth-logo">
                                <img src={logo} alt="" height="24" />
                            </a>
                            <Row className="justify-content-center mt-5">
                                <Col sm={4}>
                                    <div className="maintenance-img">
                                        <img src={commingsoon} alt="" className="img-fluid mx-auto d-block" />
                                    </div>
                                </Col>
                            </Row>
                            <h4 className="mt-5">Let's get started with Qovex</h4>
                            <p className="text-muted">It will be as simple as Occidental in fact it will be Occidental.</p>
                            <Row className="justify-content-center mt-5">
                                <Col md={8}>
                                    <div className="counter-number">
                                        <Countdown date="2021/12/31" renderer={renderer} className="counter-number" />
                                    </div>
                                </Col>
                            </Row>
                        </div>
                    </Col>
                </Row>
            </Container>
        </div>
    </React.Fragment>
);
```

## Usage

To use this component, simply import it into the desired file and include it within your JSX. Ensure that the `react-countdown` and `reactstrap` libraries are installed in your project, and adjust the countdown date as necessary.

```javascript
import PagesComingsoon from './path/to/pages-comingsoon';

function App() {
    return (
        <div className="App">
            <PagesComingsoon />
        </div>
    );
}

export default App;
```

### 🎨 Design Considerations

- **Styling**: The component uses Bootstrap classes for layout and styling, ensuring it's responsive across different device sizes.
- **Images**: Make sure to have the necessary images in your project structure, or update the paths accordingly.

This component provides a simple and effective way to create a "Coming Soon" page with a countdown timer for any application or website under maintenance or development.

# Documentation for `pages-404.js` 🚫

This document provides a comprehensive overview of the `pages-404.js` file, which is a React component designed to display a **404 error page**. This page typically appears when a user tries to access a URL that does not exist on the server.

## Table of Contents 📑
- [Overview](#overview)
- [Key Components and Libraries](#key-components-and-libraries)
- [Component Functionality](#component-functionality)
- [Code Breakdown](#code-breakdown)
- [Conclusion](#conclusion)

## Overview 📝
The `pages-404.js` file is part of a web application and provides users with a visual indication that the page they are looking for cannot be found. It includes an error message, a decorative image, and a button to navigate back to the homepage.

## Key Components and Libraries 🛠️

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library for React that provides Bootstrap components.
- **useEffect Hook**: A React hook used to handle side effects in functional components.
- **Container, Row, Col, Card, CardBody**: Components from Reactstrap used to layout the page.

## Component Functionality ⚙️

### Main Features:

- **Display a 404 Error Message**: The page prominently shows "404!" to indicate the error.
- **Error Image**: Displays an image to enhance the visual appeal of the error page.
- **Navigation Button**: Provides a button to redirect users back to the homepage.

### Usage of `useEffect`:

- **Purpose**: Sets the body class to `authentication-bg` to apply specific styles when the component mounts.
- **Cleanup**: Removes the added class when the component unmounts to prevent side effects in other parts of the application.

## Code Breakdown 🖥️

Below is a highlighted and annotated section of the code:

```javascript
import React, { useEffect } from "react";
import { Container, Row, Col, CardBody, Card } from "reactstrap";
// Import Images
import errorImage from "../../assets/images/error-img.png";

const Pages404 = () => {
  useEffect(() => {
    document.body.className = "authentication-bg";
    // Cleanup function to remove the background class
    return function cleanup() {
      document.body.className = "";
    };
  });

  return (
    <React.Fragment>
      <div className="account-pages my-5 pt-sm-5">
        <Container>
          <Row className="justify-content-center">
            <Col md={8} lg={6} xl={5}>
              <Card className="overflow-hidden">
                <CardBody>
                  <div className="text-center p-3">
                    <div className="img">
                      <img src={errorImage} className="img-fluid" alt="error" />
                    </div>
                    <h1 className="error-page mt-5"><span>404!</span></h1>
                    <h4 className="mb-4 mt-5">Sorry, page not found</h4>
                    <p className="mb-4 w-75 mx-auto">
                      It will be as simple as Occidental in fact, it will Occidental to an English person
                    </p>
                    <a className="btn btn-primary mb-4 waves-effect waves-light" href="/">
                      <i className="mdi mdi-home"></i> Back to Dashboard
                    </a>
                  </div>
                </CardBody>
              </Card>
            </Col>
          </Row>
        </Container>
      </div>
    </React.Fragment>
  );
};

export default Pages404;
```

### Explanation:

- **`useEffect` Hook**: Utilized to apply the `authentication-bg` class to the document body when the component mounts and remove it when the component unmounts.
- **JSX Structure**: Utilizes a combination of Reactstrap components to create a structured and responsive layout.
- **Error Display**: Utilizes an image and text to communicate the 404 error to the user effectively.

## Conclusion 📌

The `pages-404.js` component is a simple yet essential part of the web application. By providing a visually appealing and informative error page, it enhances the user experience by gracefully handling potential navigation errors. The use of Reactstrap and React's `useEffect` hook demonstrates efficient styling and lifecycle management within React functional components.

# Pages500 Component Documentation 📄

Welcome to the documentation for the **Pages500** component! This component is part of a web application that deals with displaying a 500 error page when something goes wrong on the server-side.

---

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Component Structure](#component-structure)
3. [Usage](#usage)
4. [Code Explanation](#code-explanation)
5. [Styling](#styling)
6. [Dependencies](#dependencies)
7. [Conclusion](#conclusion)

---

## Introduction 🏠

The **Pages500** component is a React functional component designed to display a user-friendly error message when a server error (HTTP 500) occurs. This page reassures users and provides them with a way to navigate back to the main dashboard.

---

## Component Structure 🏗️

The component consists of:

- **Container**: A responsive layout container.
- **Row and Col**: Used to align the card in the center of the page.
- **Card**: Displays the error message and an image.
- **CardBody**: Contains the main content of the error card.
- **Error Image**: An image that visually represents an error.
- **Error Message**: Text indicating a 500 error.
- **Navigation Link**: A button to navigate back to the dashboard.

---

## Usage ⚙️

To use the **Pages500** component, simply import it into your desired file and include it in your JSX:

```jsx
import Pages500 from './path/to/Pages500';

function App() {
  return (
    <div>
      <Pages500 />
    </div>
  );
}
```

Ensure that you have the necessary images and stylesheets referenced in your project.

---

## Code Explanation 🧩

Below is a detailed explanation of the **Pages500** component code:

```jsx
import React, { useEffect } from "react";
import { Container, Row, Col, Card, CardBody } from "reactstrap";

// Import Images
import errorImage from "../../assets/images/error-img.png";

const Pages500 = () => {
  // Set the body class for styling
  useEffect(() => {
    document.body.className = "authentication-bg";

    // Cleanup function to remove the class when the component unmounts
    return function cleanup() {
      document.body.className = "";
    };
  });

  return (
    <React.Fragment>
      <div className="account-pages my-5 pt-sm-5">
        <Container>
          <Row className="justify-content-center">
            <Col md={8} lg={6} xl={5}>
              <Card className="overflow-hidden">
                <CardBody>
                  <div className="text-center p-3">
                    <div className="img">
                      <img src={errorImage} className="img-fluid" alt="" />
                    </div>
                    <h1 className="error-page mt-5"><span>500!</span></h1>
                    <h4 className="mb-4 mt-5">Sorry, page not found</h4>
                    <p className="mb-4 w-75 mx-auto">
                      It will be as simple as Occidental in fact, it will Occidental to an English person
                    </p>
                    <a className="btn btn-primary mb-4 waves-effect waves-light" href="/">
                      <i className="mdi mdi-home"></i> Back to Dashboard
                    </a>
                  </div>
                </CardBody>
              </Card>
            </Col>
          </Row>
        </Container>
      </div>
    </React.Fragment>
  );
}

export default Pages500;
```

### Key Points:

- **useEffect Hook**: Sets a background style (`authentication-bg`) when the component is mounted and removes it when unmounted.
- **Error Image**: Positioned at the top to attract immediate attention.
- **Error Message**: Clearly indicates the error type (500) and provides a friendly message.
- **Navigation**: A button is provided to return to the homepage or dashboard, enhancing user experience.

---

## Styling 🎨

- The component uses **Bootstrap's Reactstrap** for layout and styling.
- Additional CSS classes (e.g., `authentication-bg`, `error-page`) are assumed to be defined elsewhere in your CSS files to style the background and text appropriately.

---

## Dependencies 📦

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: Bootstrap components built for React.
- **Images**: Ensure that `errorImage` is correctly referenced in your assets folder.

---

## Conclusion 🎉

The **Pages500** component provides a clean and efficient way to handle server-side errors in a React application. It ensures users are informed and offers a straightforward navigation path back to the homepage, enhancing the overall user experience.

Feel free to customize the styles, messages, and images as per your application's requirements. Happy coding! 👨‍💻👩‍💻

# Documentation for `li-horizontal-timeline.js`

---

## Overview

The `li-horizontal-timeline.js` file defines a React component named **`LiHorizontalTimeline`**. This component is used to represent an event in a horizontal timeline format. The component is designed to display information about specific events in a visually structured way, using a timeline layout.

---

## Table of Contents

1. [Component Description](#component-description)
2. [Component Properties](#component-properties)
3. [Code Explanation](#code-explanation)
4. [Usage](#usage)
5. [Visual Representation](#visual-representation)
6. [Conclusion](#conclusion)

---

## Component Description

The **`LiHorizontalTimeline`** component is a functional React component that uses **PropTypes** for type-checking the props. It structures an event with a title, date, and description, and visually distinguishes the current event from others in the timeline.

---

## Component Properties

| Prop  | Type          | Description                                                                                          |
|-------|---------------|------------------------------------------------------------------------------------------------------|
| event | `object`      | An object containing details about the event, such as ID, date, title, and description.             |
| key   | `any`         | A unique key for each event component, ensuring React can efficiently update and render components. |

### Event Object Structure

The `event` object should have the following structure:

- **id**: Unique identifier for the event.
- **date**: Date of the event.
- **title**: Title of the event.
- **desc**: Description of the event.

---

## Code Explanation

```jsx
import PropTypes from 'prop-types';
import React from "react";

const LiHorizontalTimeline = props => {
  return (
    <React.Fragment>
      <div
        className={props.event.id === 3 ? "item event-list active" : "item event-list"}
        key={props.key}
        style={{ width: 279 }}
      >
        <div>
          <div className="event-date">
            <div className="text-primary mb-1">{props.event.date}</div>
            <h5 className="mb-4">{props.event.title}</h5>
          </div>
          <div className="event-down-icon">
            <i className="bx bx-down-arrow-circle h1 text-primary down-arrow-icon" />
          </div>
          <div className="mt-3 px-3">
            <p className="text-muted">{props.event.desc}</p>
          </div>
        </div>
      </div>
    </React.Fragment>
  );
}

LiHorizontalTimeline.propTypes = {
  event: PropTypes.object,
  key: PropTypes.any
};

export default LiHorizontalTimeline;
```

### Key Components:

- **Conditional Class Application**: 
  - `className={props.event.id === 3 ? "item event-list active" : "item event-list"}`: This conditionally applies the "active" class if the event ID is 3, likely highlighting a specific event.
  
- **Event Display**:
  - The event's date, title, and description are displayed with specific styling.
  - An arrow icon is used to denote the timeline's flow or movement.

---

## Usage

To use the `LiHorizontalTimeline` component, import it into your desired file and pass in the required props:

```jsx
import LiHorizontalTimeline from './li-horizontal-timeline';

const event = {
  id: 1,
  date: "January 1, 2021",
  title: "New Year's Day",
  desc: "Celebration of the new year."
};

<LiHorizontalTimeline event={event} key={event.id} />
```

---

## Visual Representation

- **Active Event**: If the event ID is 3, it will be styled with an "active" class, which can be used to apply special CSS for emphasis.
- **Timeline Structure**: The component is structured to fit within a horizontal timeline, using consistent spacing and alignment for each event.

---

## Conclusion

The **`LiHorizontalTimeline`** component offers a straightforward method to visualize events in a timeline format. By utilizing props for flexibility and PropTypes for validation, it ensures that event data is displayed consistently and accurately. This component can be easily integrated into timelines for projects, historical events, or any sequence of activities.

---

# 📜 Documentation for `li-vertical-timeline.js`

This document provides a comprehensive overview of the `li-vertical-timeline.js` file, explaining its functionality, purpose, and structure. The file is part of a React-based project and is designed to render a vertical timeline component.

## Table of Contents

1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Props](#props)
4. [Usage](#usage)
5. [Code Explanation](#code-explanation)

## Overview

The `li-vertical-timeline.js` file defines a React component named `LiVerticalTimeline`. This component is used to display a single event in a vertical timeline. It leverages the `reactstrap` library for styling and uses icons to visually represent different statuses of events.

## Component Structure

The component is structured as follows:

- **Wrapper (`<li>`):** The outermost wrapper is a list item with the class `event-list`.
- **Dot Indicator:** A div containing an icon that represents a dot on the timeline. The icon changes style based on the status of the event.
- **Media Object:** A div structured as a media object, with an icon on the left and the event details on the right.

## Props

The `LiVerticalTimeline` component accepts the following props:

| Prop Name | Type   | Description                                   |
|-----------|--------|-----------------------------------------------|
| status    | Object | Contains the details of the event status.     |

### `status` Object Properties

- **id:** An identifier for the status, used to determine the icon's animation.
- **iconClass:** The class name for the status icon.
- **stausTitle:** The title of the status.
- **description:** A brief description of the status.

## Usage

To use the `LiVerticalTimeline` component, you need to import it and provide the necessary `status` prop. Here is a simple example:

```jsx
import LiVerticalTimeline from './li-vertical-timeline';

const status = {
  id: 1,
  iconClass: 'bx-calendar-check',
  stausTitle: 'Event Completed',
  description: 'This event was completed successfully.'
};

<LiVerticalTimeline status={status} />
```

## Code Explanation

```jsx
import PropTypes from 'prop-types'
import React from "react"

const LiVerticalTimeline = props => {
  return (
    <React.Fragment>
      <li className="event-list">
        <div className="event-timeline-dot">
          <i className={ props.status.id === 3 ? "bx bx-right-arrow-circle bx-fade-right" : "bx bx-right-arrow-circle" } />
        </div>
        <div className="media">
          <div className="me-3">
            <i className={"bx " + props.status.iconClass + " h2 text-primary"} />
          </div>
          <div className="media-body">
            <div>
              <h5>{props.status.stausTitle}</h5>
              <p className="text-muted">{props.status.description}</p>
            </div>
          </div>
        </div>
      </li>
    </React.Fragment>
  )
}

LiVerticalTimeline.propTypes = {
  status: PropTypes.object
}

export default LiVerticalTimeline
```

### Key Points:

- **Icon Logic:** The icon for the timeline dot changes animation if the `status.id` is `3`, indicating a specific condition.
- **Media Structure:** The component uses a media object pattern to display the icon and text efficiently.
- **PropTypes:** The component uses `PropTypes` to define the expected shape of the `status` prop, ensuring type safety and clarity.

### 📝 Notes:

- Ensure that the `status` object is correctly structured when using the component.
- The component relies on the `bx` icon library for icons, so ensure it is included in your project.

This documentation should provide a clear understanding of how to work with and implement the `LiVerticalTimeline` component in your projects. Happy coding! 🎉

# 📃 Invoice.js Documentation

Welcome to the documentation for **invoice.js**! This file is a React component that renders a detailed invoice page. It is designed using React and Reactstrap and includes various sections such as billing, shipping, payment details, order summary, and options to print or send the invoice. This component is part of a larger application, likely a dashboard or an e-commerce platform.

---

## Table of Contents

1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [Functionality](#functionality)
5. [Detailed Explanation](#detailed-explanation)
6. [CSS Classes Used](#css-classes-used)
7. [Props](#props)
8. [Conclusion](#conclusion)

---

## Overview

The **invoice.js** file is responsible for rendering an invoice page. It displays:

- **Order Number**
- **Billed To** and **Shipped To** addresses
- **Payment Method**
- **Order Date**
- **Order Summary** with itemized pricing
- **Total Amount**
- Options to **print** or **send** the invoice

---

## Dependencies

The component relies on several imports:

- **React**: Core library for building UI components.
- **Reactstrap**: Provides Bootstrap components as React components.
- **React Router**: For navigation, using the `Link` component.
- **Custom Components**: `Breadcrumbs` for navigation hierarchy.
- **Images**: Logo images for branding.

```javascript
import React from 'react';
import { CardBody, Row, Col, Card, Table } from 'reactstrap';
import { Link } from "react-router-dom";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import logo from "../../assets/images/logo-dark.png";
import logoLight from "../../assets/images/logo-light.png";
```

---

## Component Structure

The component is organized into:

- **Breadcrumbs**: Displays the navigation path.
- **Card**: Contains the invoice details.
- **Row and Col**: For layout management, utilizing the grid system.
- **Tables**: Display the order summary.
- **Links**: For print and send actions.

---

## Functionality

### Main Features

- **Invoice Header**: Displays the order number and logo.
- **Addresses**: Shows billing and shipping addresses.
- **Payment and Date**: Displays payment method and order date.
- **Order Summary**: Lists purchased items with their prices.
- **Total Calculation**: Summarizes the total cost, including shipping.
- **Actions**: Buttons for printing or sending the invoice.

---

## Detailed Explanation

### Header Section

- **Order Number**: Displayed at the top-right.
- **Logo**: Both dark and light versions are displayed for branding.

### Address Section

- **Billed To**: Contains the customer's billing address.
- **Shipped To**: Contains the shipping address.

### Payment and Order Details

- **Payment Method**: Shows the card type and masked card number.
- **Order Date**: Displays when the order was placed.

### Order Summary Table

- **Items Listed**: Each row corresponds to an item purchased.
- **Subtotal and Total**: Calculates and displays the subtotal, shipping, and total amount.

### Actions

- **Print Button**: Triggers a print dialog.
- **Send Button**: Intended to send the invoice, possibly via email.

```javascript
<div className="d-print-none">
  <div className="float-end">
    <Link to="#" className="btn btn-success waves-effect waves-light"><i className="fa fa-print"></i></Link>{" "}
    <Link to="#" className="btn btn-primary w-md waves-effect waves-light">Send</Link>
  </div>
</div>
```

---

## CSS Classes Used

The component uses various CSS classes to style elements:

- **invoice-title**: Styles the invoice title section.
- **font-size-16**: Sets font size for text.
- **mb-4, mt-3**: Margin classes for spacing.
- **text-end**: Aligns text to the right.
- **fw-bold**: Sets text to bold.
- **table-nowrap**: Prevents table text wrapping.
- **d-print-none**: Hides elements during print.

---

## Props

This component currently does not receive any props. It uses hard-coded data for demonstration purposes.

---

## Conclusion

The **invoice.js** component is a well-structured React component that effectively uses Reactstrap for layout and styling. It provides a clear and detailed invoice page that is essential for any e-commerce or business application. The use of React and modular components like `Breadcrumbs` makes it easy to integrate and scale within larger applications.

Feel free to customize and extend this component to suit your specific needs! 🛠️

---

🌟 **Thank you for using our documentation! We hope it helps you understand the `invoice.js` component better.** 🌟

# Card Pricing Component Documentation 📄

## Table of Contents
1. [Introduction](#introduction)
2. [Purpose](#purpose)
3. [Code Explanation](#code-explanation)
4. [Props](#props)
5. [Features](#features)
6. [Usage](#usage)
7. [Conclusion](#conclusion)

---

## Introduction

The **Card Pricing Component** is a React component designed for displaying pricing plans. This component utilizes several libraries and frameworks to provide a seamless user experience. It is designed to be used within a pricing page or section of a web application.

## Purpose

The primary purpose of the `CardPricing` component is to visually represent various pricing plans. This is achieved by displaying key information such as the plan's title, description, price, duration, and features.

## Code Explanation

Below is an explanation of the code structure and logic:

```javascript
import PropTypes from 'prop-types';
import React from "react";
import { Link } from "react-router-dom";
import { Card, CardBody, Col } from "reactstrap";

const CardPricing = props => {
    return (
        <React.Fragment>
            <Col xl="3" md="6">
                <Card className="plan-box">
                    <CardBody className="p-4">
                        <div className="d-flex align-items-start">
                            <div body className="flex-1 me-3">
                                <h5>{props.pricing.title}</h5>
                                <p className="text-muted">{props.pricing.description}</p>
                            </div>
                            <div className="ms-auto">
                                <i className={"bx " + props.pricing.icon + " h1 text-primary"} />
                            </div>
                        </div>
                        <div className="py-4 mt-4 text-center bg-soft-light">
                            <h1 className="m-0"><sup><small>$</small></sup> {props.pricing.price}/{" "}
                            <span className="font-size-13">{props.pricing.duration}</span></h1>
                        </div>
                        <div className="plan-features p-4 text-muted mt-2">
                            {props.pricing.features.map((feature, key) => (
                                <p key={"_feature_" + key}>
                                    <i className="mdi mdi-check-bold text-primary me-4" /> {feature.title}
                                </p>
                            ))}
                        </div>
                        <div className="text-center">
                            <Link to={props.pricing.link} className="btn btn-primary waves-effect waves-light">
                                Sign up Now
                            </Link>
                        </div>
                    </CardBody>
                </Card>
            </Col>
        </React.Fragment>
    );
}

CardPricing.propTypes = {
    pricing: PropTypes.object
};

export default CardPricing;
```

### Breakdown

- **Imports**: 
  - `PropTypes` for type checking.
  - `React` for component creation.
  - `Link` from `react-router-dom` for navigation.
  - `Card`, `CardBody`, `Col` from `reactstrap` for layout and styling.

- **Component Structure**:
  - **`Col`**: Used to define the column layout.
  - **`Card`**: Wrapper for the pricing information, assigned a class for styling.
  - **`CardBody`**: Contains the main content of the card including title, description, price, icon, features, and a signup link.

- **Dynamic Content**: 
  - Displays information based on `props.pricing` which includes title, description, icon, price, duration, features, and a link.

## Props

- **`pricing`**: An object containing:
  - **`title`**: The name of the pricing plan.
  - **`description`**: A brief description of the plan.
  - **`icon`**: Icon representing the plan.
  - **`price`**: Cost of the plan.
  - **`duration`**: Billing cycle (e.g., monthly, annually).
  - **`features`**: An array of features included in the plan.
  - **`link`**: Path to the signup page for the plan.

## Features

- **Responsive Design**: Utilizes `reactstrap` for a responsive layout that adapts to different screen sizes.
- **Icon Support**: Displays an icon for each plan.
- **Feature Listing**: Lists features included in the pricing plan with check marks.
- **Navigation**: Includes a call-to-action button to navigate users to a signup page.

## Usage

To use the `CardPricing` component, you need to pass a `pricing` object with the necessary fields. Below is an example of how you might integrate it:

```jsx
<CardPricing 
    pricing={{
        title: "Standard Plan",
        description: "Best for small teams",
        icon: "bx-dollar",
        price: "29",
        duration: "month",
        features: [
            { title: "10 Projects" },
            { title: "24/7 Support" },
            { title: "Unlimited Users" }
        ],
        link: "/signup"
    }}
/>
```

## Conclusion

The **Card Pricing Component** is a versatile and visually appealing way to showcase pricing plans on your application. By leveraging `reactstrap` for layout and `react-router-dom` for navigation, it ensures a smooth user experience. Its configurable nature allows for easy adaptation to different pricing strategies and plans. 

Feel free to modify and extend the component to suit your specific needs! 🌟