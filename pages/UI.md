# UiColors.js Documentation

## Overview

The `UiColors.js` file is a React component that demonstrates the use of different color utilities in a user interface. It showcases various Bootstrap color classes applied to elements to create visually appealing UI components. This component can be used as a reference for adding color styles to your React applications.

## Structure

The component is structured using React and Reactstrap for styling. It employs a grid layout to display different color variations, including primary, success, info, warning, danger, dark, and secondary colors. Each color is presented with its respective hexadecimal code, a gradient variation, and a soft variation.

## Components and Usage

### Breadcrumbs

The `Breadcrumbs` component imported from `../../components/Common/Breadcrumb` is used to display the current navigation path with the titles "UI Elements" and "Colors". This helps users understand their location within the application.

```jsx
<Breadcrumbs title="UI Elements" breadcrumbItem="Colors" />
```

### Color Cards

Each color is represented in a `Card` component, containing a `CardBody`. The body includes three variations of the color:

1. **Solid Color Box**: Displays the solid color with its hexadecimal code.
2. **Gradient Box**: Shows a gradient variation of the color.
3. **Soft Gradient Box**: Displays a soft, muted gradient variation.

The `CardTitle` for each color is dynamically styled to match the color being showcased.

Here's an example structure for a color card:

```jsx
<Col xl={3} md={6}>
    <Card>
        <CardBody className="text-center">
            <div className="color-box bg-primary p-4">
                <h5 className="my-2 text-white">#3b5de7</h5>
            </div>
            <div className="color-box bg-primary bg-gradient p-4">
                <h5 className="my-2 text-white">bg-gradient</h5>
            </div>
            <div className="color-box bg-soft-primary bg-gradient p-4">
                <h5 className="my-2 text-primary">bg-soft-primary</h5>
            </div>
            <h5 className="mb-0 mt-3 text-primary">Primary</h5>
        </CardBody>
    </Card>
</Col>
```

### Colors Demonstrated

- **Primary**
  - Hex: `#3b5de7`
  - Variants: Standard, Gradient, Soft Gradient

- **Success**
  - Hex: `#45cb85`
  - Variants: Standard, Gradient, Soft Gradient

- **Info**
  - Hex: `#0caadc`
  - Variants: Standard, Gradient, Soft Gradient

- **Warning**
  - Hex: `#eeb902`
  - Variants: Standard, Gradient, Soft Gradient

- **Danger**
  - Hex: `#ff715b`
  - Variants: Standard, Gradient, Soft Gradient

- **Dark**
  - Hex: `#343a40`
  - Variants: Standard, Gradient, Soft Gradient

- **Secondary**
  - Hex: `#9095ad`
  - Variants: Standard, Gradient, Soft Gradient

## How to Use

To implement this component in your project, ensure you have the necessary dependencies installed, including React, Reactstrap, and Bootstrap. You can then import and use `UiColors` within your React application to display a color palette and experiment with different color styles.

```jsx
import UiColors from './path/to/UiColors';

function App() {
  return (
    <div>
      <UiColors />
    </div>
  );
}

export default App;
```

## Conclusion

The `UiColors.js` component is a simple yet effective way to visualize different color options within a UI. By utilizing React and Reactstrap, it provides a clean and responsive design that can easily be integrated into any React project to enhance its visual appeal.

# UiDropdown Component Documentation

The `UiDropdown` component is a React component that provides a collection of dropdown elements using Bootstrap's dropdown functionality. This component demonstrates various styles and configurations of dropdowns, including single button dropdowns, split button dropdowns, different button variants, and dropdown position variations such as dropup, dropright, and dropleft.

## Table of Contents

1. [Component Overview](#component-overview)
2. [Features](#features)
3. [Usage](#usage)
4. [Code Explanation](#code-explanation)
5. [Conclusion](#conclusion)

## Component Overview

The `UiDropdown` component utilizes the following Reactstrap components:
- `Dropdown`
- `DropdownMenu`
- `DropdownItem`
- `DropdownToggle`
- `ButtonDropdown`
- `Button`
- `Card`
- `CardBody`
- `CardTitle`
- `Row`
- `Col`

Additionally, the component includes breadcrumb navigation using the `Breadcrumbs` component.

## Features

- **Single Button Dropdowns**: Simple dropdowns triggered by a single button.
- **Split Button Dropdowns**: Dropdowns with a separate toggle button.
- **Button Variants**: Dropdowns with different button styles (e.g., primary, secondary, success).
- **Sizing**: Dropdowns with varied button sizes (small, large).
- **Dropdown Position Variations**: Includes dropup, dropright, and dropleft configurations.
- **Menu Alignment**: Right-aligned dropdown menus.

## Usage

```jsx
import UiDropdown from './UiDropdown';

// Render the component
<UiDropdown />
```

## Code Explanation

The `UiDropdown` component is defined as a functional component using React hooks for managing the open states of multiple dropdowns. Each dropdown uses `useState` to track whether it is open or closed.

### Key Elements

- **Dropdown States**: Various `useState` hooks are used to manage the open/close state of each dropdown.
- **Dropdown and ButtonDropdown Components**: These components provide the structure for individual dropdowns and split dropdowns.
- **DropdownToggle**: Used to toggle the visibility of the dropdown menu.
- **DropdownMenu and DropdownItem**: Define the contents of each dropdown, which can include actions or additional links.
- **Direction and Alignment**: Dropdowns can be customized to drop in different directions (`up`, `right`, `left`) and align menus to the right.

### Example of a Single Button Dropdown

```jsx
<Dropdown isOpen={singlebtn} toggle={() => setSinglebtn(!singlebtn)}>
    <DropdownToggle className="btn btn-secondary" caret>
        Dropdown button <i className="mdi mdi-chevron-down" />
    </DropdownToggle>
    <DropdownMenu>
        <DropdownItem>Action</DropdownItem>
        <DropdownItem>Another action</DropdownItem>
        <DropdownItem>Something else here</DropdownItem>
    </DropdownMenu>
</Dropdown>
```

### Example of a Split Button Dropdown

```jsx
<ButtonDropdown isOpen={drp_primary1} toggle={() => setDrp_primary1(!drp_primary1)}>
    <Button id="caret" color="primary"> Primary </Button>
    <DropdownToggle caret color="primary" className="dropdown-toggle-split">
        <i className="mdi mdi-chevron-down" />
    </DropdownToggle>
    <DropdownMenu>
        <DropdownItem header>Header</DropdownItem>
        <DropdownItem disabled>Action</DropdownItem>
        <DropdownItem>Another Action</DropdownItem>
        <DropdownItem divider />
        <DropdownItem>Another Action</DropdownItem>
    </DropdownMenu>
</ButtonDropdown>
```

### Dropdown Variants and Sizes

The component demonstrates how dropdowns can be styled with various button colors and sizes. For instance, dropdown buttons can have `primary`, `secondary`, `success`, `info`, `warning`, and `danger` styles. Sizes can also be adjusted using classes like `btn-lg` and `btn-sm`.

### Position Variations

To create different dropdown positions, such as `dropup`, `dropright`, and `dropleft`, the component uses the `direction` prop in the `Dropdown` or `ButtonDropdown` components.

## Conclusion

The `UiDropdown` component provides a comprehensive demonstration of Bootstrap-styled dropdowns in React, utilizing Reactstrap for ease of integration. By leveraging different states, styles, and configurations, this component serves as a versatile tool for adding dropdowns to any React application.

# Slide with Fade Documentation

This document provides an overview of the `slidewithfade.js` file, which implements a React component for a carousel with fade transition effects, using the `reactstrap` library.

## Table of Contents
1. [Introduction](#introduction)
2. [Component Overview](#component-overview)
3. [Key Features](#key-features)
4. [Usage](#usage)
5. [Code Explanation](#code-explanation)
6. [Customization](#customization)
7. [Conclusion](#conclusion)

## Introduction
The `Slidewithfade` component is a React-based carousel that leverages the `reactstrap` library to create a smooth fading transition between slides. This component is ideal for displaying a collection of images or content blocks in a visually appealing manner.

## Component Overview
The `Slidewithfade` component is structured as a class component that manages its own state to track the active slide index and handles slide transitions with a fading effect.

## Key Features
- **Fade Transition:** Smooth fading effect between slides.
- **Responsive Design:** Utilizes `img-fluid` class to ensure images are responsive.
- **Indicators and Controls:** Includes carousel indicators and navigation controls for user interaction.

## Usage
To use the `Slidewithfade` component, import it into your React application and include it within your JSX. Ensure that you have `reactstrap` and its dependencies installed.

### Example
```jsx
import Slidewithfade from './path/to/slidewithfade';

function App() {
  return (
    <div>
      <Slidewithfade />
    </div>
  );
}

export default App;
```

## Code Explanation
Below is an explanation of the key parts of the `slidewithfade.js` file:

### Imports
```javascript
import React, { Component } from "react";
import { Carousel, CarouselItem, CarouselControl, CarouselIndicators } from "reactstrap";
import img1 from "../../../assets/images/small/img-1.jpg";
import img2 from "../../../assets/images/small/img-2.jpg";
import img3 from "../../../assets/images/small/img-3.jpg";
```
- The component imports necessary modules from `React` and `reactstrap`.
- It also imports images that will be displayed in the carousel.

### Component Definition
```javascript
class Slidewithfade extends Component {
  constructor(props) {
    super(props);
    this.state = { activeIndex: 0 };
    this.next = this.next.bind(this);
    this.previous = this.previous.bind(this);
    this.goToIndex = this.goToIndex.bind(this);
    this.onExiting = this.onExiting.bind(this);
    this.onExited = this.onExited.bind(this);
  }
```
- The component is defined as a class extending `Component`.
- State is initialized with an `activeIndex` to track the current slide.
- Methods for navigation (`next`, `previous`, `goToIndex`) and animation control (`onExiting`, `onExited`) are bound.

### Slide Data
```javascript
const items = [
  { src: img1, altText: "Slide 1", caption: "Slide 1" },
  { src: img2, altText: "Slide 2", caption: "Slide 2" },
  { src: img3, altText: "Slide 3", caption: "Slide 3" },
];
```
- An array of slide data is defined, with each object containing the image source, alt text, and caption.

### Render Method
```javascript
render() {
  const { activeIndex } = this.state;
  const slides = items.map(item => {
    return (
      <CarouselItem
        onExiting={this.onExiting}
        onExited={this.onExited}
        key={item.src}
      >
        <img src={item.src} className="d-block img-fluid" alt={item.altText} />
      </CarouselItem>
    );
  });

  return (
    <React.Fragment>
      <Carousel
        activeIndex={activeIndex}
        fade={true}
        next={this.next}
        previous={this.previous}
      >
        <CarouselIndicators
          items={items}
          activeIndex={activeIndex}
          onClickHandler={this.goToIndex}
        />
        {slides}
        <CarouselControl
          direction="prev"
          directionText="Previous"
          onClickHandler={this.previous}
        />
        <CarouselControl
          direction="next"
          directionText="Next"
          onClickHandler={this.next}
        />
      </Carousel>
    </React.Fragment>
  );
}
```
- The render method constructs carousel items and integrates `Carousel`, `CarouselControl`, and `CarouselIndicators`.
- The `fade` prop is set to `true` to enable fade transitions.

## Customization
- **Images:** Update the `items` array with your own images and captions.
- **Transition Duration:** Modify the transition timing by adjusting the `interval` or adding CSS transitions.
- **Styling:** Use CSS classes to style the carousel and its components to match your design needs.

## Conclusion
The `Slidewithfade` component provides a simple and effective way to implement a carousel with fade transitions in a React application. With its customizable options and responsive design, it can enhance the visual presentation of image galleries or featured content sections.

# Documentation for `slidewithindicator.js`

The `slidewithindicator.js` file is a React component that creates a carousel with slide indicators using the `reactstrap` library. This component is designed to display a series of images with the ability to navigate through them using indicators, as well as previous and next controls.

## Table of Contents

- [Overview](#overview)
- [Imports](#imports)
- [Component Structure](#component-structure)
- [State Management](#state-management)
- [Lifecycle Methods](#lifecycle-methods)
- [Carousel Functionality](#carousel-functionality)
- [Render Method](#render-method)
- [Usage](#usage)

## Overview

`Slidewithindicator` is a class-based React component that provides a carousel slider with indicators. It allows users to click on indicators to navigate directly to a specific slide and use navigation controls for sequential navigation.

## Imports

```javascript
import React, { Component } from "react";
import { Carousel, CarouselItem, CarouselControl, CarouselIndicators } from "reactstrap";
import img3 from "../../../assets/images/small/img-3.jpg";
import img4 from "../../../assets/images/small/img-4.jpg";
import img5 from "../../../assets/images/small/img-5.jpg";
```

### Description

- **React, Component**: These are imported from the `react` library. `Component` is used to create class-based components.
- **Carousel, CarouselItem, CarouselControl, CarouselIndicators**: These components are imported from the `reactstrap` library and are used to create the carousel structure.
- **img3, img4, img5**: These are image imports used as the slides in the carousel.

## Component Structure

The component is structured as a class-based component that extends `React.Component`.

```javascript
class Slidewithindicator extends Component {
  constructor(props) {
    super(props);
    this.state = { activeIndex: 0 };
    this.next = this.next.bind(this);
    this.previous = this.previous.bind(this);
    this.goToIndex = this.goToIndex.bind(this);
    this.onExiting = this.onExiting.bind(this);
    this.onExited = this.onExited.bind(this);
  }
  // ...methods
}
```

## State Management

The component maintains a single piece of state:

- **activeIndex**: Tracks the currently active slide in the carousel.

## Lifecycle Methods

- **onExiting**: Sets a flag indicating that a slide transition is currently animating.
- **onExited**: Clears the animation flag after the slide transition completes.

## Carousel Functionality

### Methods

- **next**: Advances to the next slide unless an animation is currently in progress.
- **previous**: Moves to the previous slide unless an animation is currently in progress.
- **goToIndex**: Directly navigates to a specific slide index if no animation is ongoing.

### Code Example

```javascript
next() {
  if (this.animating) return;
  const nextIndex = this.state.activeIndex === items.length - 1 ? 0 : this.state.activeIndex + 1;
  this.setState({ activeIndex: nextIndex });
}

previous() {
  if (this.animating) return;
  const nextIndex = this.state.activeIndex === 0 ? items.length - 1 : this.state.activeIndex - 1;
  this.setState({ activeIndex: nextIndex });
}

goToIndex(newIndex) {
  if (this.animating) return;
  this.setState({ activeIndex: newIndex });
}
```

## Render Method

The `render` method generates the JSX for the carousel, including the slides, controls, and indicators.

### Code Example

```javascript
render() {
  const { activeIndex } = this.state;
  const slides = items.map(item => {
    return (
      <CarouselItem onExiting={this.onExiting} onExited={this.onExited} key={item.src}>
        <img src={item.src} className="d-block img-fluid" alt={item.altText} />
      </CarouselItem>
    );
  });

  return (
    <React.Fragment>
      <Carousel activeIndex={activeIndex} next={this.next} previous={this.previous}>
        <CarouselIndicators items={items} activeIndex={activeIndex} onClickHandler={this.goToIndex} />
        {slides}
        <CarouselControl direction="prev" directionText="Previous" onClickHandler={this.previous} />
        <CarouselControl direction="next" directionText="Next" onClickHandler={this.next} />
      </Carousel>
    </React.Fragment>
  );
}
```

## Usage

To use this component, simply import and include it in your JSX as follows:

```javascript
import Slidewithindicator from 'path/to/slidewithindicator';

function App() {
  return (
    <div>
      <Slidewithindicator />
    </div>
  );
}
```

This component will render a responsive image carousel with indicators and navigation controls, perfect for showcasing images in a slideshow format.

# Slide with Caption Component Documentation

The `slidewithcaption.js` file defines a React component named `Slidewithcaption`. This component is a carousel that displays images with captions and allows navigation between the slides using controls. Below, you'll find detailed information about how this component is implemented and how it functions.

## Table of Contents

1. [Component Overview](#component-overview)
2. [Core Features](#core-features)
3. [Component Structure](#component-structure)
4. [Functionality](#functionality)
5. [How to Use](#how-to-use)
6. [Code Explanation](#code-explanation)

## Component Overview

The `Slidewithcaption` component utilizes the Reactstrap library to create a carousel with image slides. Each slide displays an image along with a caption. Users can navigate between slides using navigation controls.

## Core Features

- **Image Carousel**: Displays a series of images in a rotating carousel.
- **Captions**: Each image slide is accompanied by a caption that provides additional context or description.
- **Navigation Controls**: Users can navigate through the slides using "Previous" and "Next" controls.
- **Responsive Design**: The carousel is responsive, adapting to various screen sizes.

## Component Structure

The component imports several elements from React and Reactstrap:

- `React`, `Component`: Core React library.
- `Carousel`, `CarouselItem`, `CarouselControl`, `CarouselCaption`: Components from Reactstrap used to build the carousel.

## Functionality

### State Management

The component maintains its state with the following properties:

- `activeIndex`: Tracks the current active slide index.
- Methods to manage the state:
  - `next`: Advances to the next slide.
  - `previous`: Returns to the previous slide.
  - `goToIndex`: Jumps to a specific slide.

### Lifecycle Methods

- `onExiting`: Triggered when exiting a slide, sets an animation flag.
- `onExited`: Triggered when a slide transition completes, clears the animation flag.

### Slides Array

An array called `items` holds the details for each slide, including:

- `src`: The path to the image file.
- `altText`: Alternative text for accessibility.
- `caption`: The text that appears as the caption for each slide.

## How to Use

To use this component, ensure that you have Reactstrap installed in your project. You can then import and include the `Slidewithcaption` component within your React application.

Example:

```jsx
import React from 'react';
import Slidewithcaption from './path/to/slidewithcaption';

function App() {
  return (
    <div>
      <h1>My Carousel</h1>
      <Slidewithcaption />
    </div>
  );
}

export default App;
```

## Code Explanation

```jsx
import React, { Component } from "react";
import { Carousel, CarouselItem, CarouselControl, CarouselCaption } from "reactstrap";

// Image imports
import img3 from "../../../assets/images/small/img-3.jpg";
import img4 from "../../../assets/images/small/img-4.jpg";
import img5 from "../../../assets/images/small/img-5.jpg";

const items = [
  {
    src: img3,
    altText: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    caption: "First slide label",
  },
  {
    src: img4,
    altText: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    caption: "Second slide label",
  },
  {
    src: img5,
    altText: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    caption: "Third slide label",
  },
];

class Slidewithcaption extends Component {
  constructor(props) {
    super(props);
    this.state = { activeIndex: 0 };
    this.next = this.next.bind(this);
    this.previous = this.previous.bind(this);
    this.goToIndex = this.goToIndex.bind(this);
    this.onExiting = this.onExiting.bind(this);
    this.onExited = this.onExited.bind(this);
  }

  onExiting() {
    this.animating = true;
  }

  onExited() {
    this.animating = false;
  }

  next() {
    if (this.animating) return;
    const nextIndex = this.state.activeIndex === items.length - 1 ? 0 : this.state.activeIndex + 1;
    this.setState({ activeIndex: nextIndex });
  }

  previous() {
    if (this.animating) return;
    const nextIndex = this.state.activeIndex === 0 ? items.length - 1 : this.state.activeIndex - 1;
    this.setState({ activeIndex: nextIndex });
  }

  goToIndex(newIndex) {
    if (this.animating) return;
    this.setState({ activeIndex: newIndex });
  }

  render() {
    const { activeIndex } = this.state;
    const slides = items.map((item) => {
      return (
        <CarouselItem onExiting={this.onExiting} onExited={this.onExited} key={item.src}>
          <img src={item.src} className="d-block img-fluid" alt={item.altText} />
          <CarouselCaption className="d-none d-md-block text-white-50" captionText={item.altText} captionHeader={item.caption} />
        </CarouselItem>
      );
    });

    return (
      <React.Fragment>
        <Carousel activeIndex={activeIndex} next={this.next} previous={this.previous}>
          {slides}
          <CarouselControl direction="prev" directionText="Previous" onClickHandler={this.previous} />
          <CarouselControl direction="next" directionText="Next" onClickHandler={this.next} />
        </Carousel>
      </React.Fragment>
    );
  }
}

export default Slidewithcaption;
```

### Key Points

- The `Slidewithcaption` component is a class-based component that uses Reactstrap's Carousel components to display images with captions.
- The component manages slide navigation and transitions using React's state management and lifecycle methods.
- It's designed to be reusable and easy to integrate into any React application with the necessary image paths and imports.

This documentation should help you understand how to implement and use the `Slidewithcaption` component effectively in your projects.

# Documentation for `slidewithcontrol.js`

The `slidewithcontrol.js` file is a React component that implements a carousel with next and previous controls. This component leverages the `reactstrap` library to create a carousel that displays a series of images with the ability to navigate between them using controls.

## Overview

The `Slidewithcontrol` component is a class-based React component that provides functionality to navigate through a series of slides/images. It is designed using the `Carousel`, `CarouselItem`, and `CarouselControl` components from the `reactstrap` library.

### Import Statements

```javascript
import React, { Component } from "react";
import { Carousel, CarouselItem, CarouselControl } from "reactstrap";
import img4 from "../../../assets/images/small/img-4.jpg";
import img5 from "../../../assets/images/small/img-5.jpg";
import img6 from "../../../assets/images/small/img-6.jpg";
```

- **React and Component**: Core React library and Component class for creating React components.
- **Carousel, CarouselItem, CarouselControl**: Components from `reactstrap` used to create the structure of the carousel.
- **Images**: The images (`img4`, `img5`, `img6`) are imported from local assets, representing the slides.

### Component Structure

The component maintains the following state:
- `activeIndex`: Keeps track of the currently active slide index.
- `animating`: A flag to prevent actions while animations are in progress.

### Methods

- **constructor(props)**: Initializes the component with a default `activeIndex` of 0 and binds helper methods.

- **onExiting()**: Sets the `animating` flag to `true` when a slide transition is starting.

- **onExited()**: Sets the `animating` flag to `false` when a slide transition has ended.

- **next()**: Moves to the next slide unless an animation is in progress. If at the last slide, it wraps around to the first slide.

- **previous()**: Moves to the previous slide unless an animation is in progress. If at the first slide, it wraps around to the last slide.

- **goToIndex(newIndex)**: Sets the `activeIndex` to a specific slide index if no animation is occurring.

### Render Function

The `render` method constructs the carousel component:

- **slides**: Maps over the `items` array to create `CarouselItem` components, each containing an image and its respective alt text.
  
- **Carousel**: Contains the slides and controls. It handles the active slide index and provides navigation controls using `CarouselControl`.

### Usage

Below is an example of how you can use the `Slidewithcontrol` component in a React application:

```jsx
import React from 'react';
import Slidewithcontrol from './Slidewithcontrol';

function App() {
  return (
    <div className="App">
      <Slidewithcontrol />
    </div>
  );
}

export default App;
```

### Conclusion

The `Slidewithcontrol` component provides a simple yet effective carousel with controls for navigating through a set of images. It uses `reactstrap` for styling and behavior, ensuring responsiveness and visual appeal. By utilizing class-based React features, it manages state transitions and interactions smoothly.

# Documentation for `UiVideo.js`

## Overview

The `UiVideo.js` file is a React component designed to demonstrate the usage of responsive embedded videos within a web page. It utilizes Bootstrap's responsive embed classes to adjust the aspect ratios of embedded videos, making them adaptable to various screen sizes and orientations. This component is part of a UI elements library and provides a user-friendly interface for displaying videos in different aspect ratios.

## Index

1. [Component Structure](#component-structure)
2. [Usage](#usage)
3. [Responsive Video Embedding](#responsive-video-embedding)
4. [Customization](#customization)
5. [References](#references)

---

## Component Structure

The `UiVideo` component is structured as follows:

- **Imports**: The component imports necessary modules such as `React`, `reactstrap` components (e.g., `Card`, `CardBody`, `CardTitle`, `Col`, `Row`), and a Breadcrumbs component for navigation.
  
- **Breadcrumbs**: Displays the navigational breadcrumb, indicating the current location within the UI elements section.

- **Video Embedding**: Contains multiple cards, each demonstrating a different aspect ratio for video embedding.

```jsx
import React from "react";
import { Card, CardBody, CardTitle, Col, Row } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";

const UiVideo = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="UI Elements" breadcrumbItem="Video" />
        // Video rows and columns here
      </div>
    </React.Fragment>
  );
};

export default UiVideo;
```

## Usage

The `UiVideo` component is used to embed videos responsively within a page. It can be incorporated within any React application that utilizes `reactstrap` for UI components. The component is designed to showcase videos with different aspect ratios, making it ideal for scenarios where flexible video embedding is required.

## Responsive Video Embedding

The component illustrates how to embed videos with the following aspect ratios:

1. **16:9 Aspect Ratio**
   ```jsx
   <div className="embed-responsive embed-responsive-16by9 ratio ratio-16x9">
     <iframe title="YouTube video" className="embed-responsive-item" src="https://www.youtube.com/embed/1y_kfWUCFDQ" />
   </div>
   ```

2. **21:9 Aspect Ratio**
   ```jsx
   <div className="ratio ratio-21x9">
     <iframe title="YouTube video" allowFullScreen src="https://www.youtube.com/embed/1y_kfWUCFDQ" />
   </div>
   ```

3. **4:3 Aspect Ratio**
   ```jsx
   <div className="ratio ratio-4x3">
     <iframe title="YouTube video" allowFullScreen src="https://www.youtube.com/embed/1y_kfWUCFDQ" />
   </div>
   ```

4. **1:1 Aspect Ratio**
   ```jsx
   <div className="ratio ratio-1x1">
     <iframe title="YouTube video" allowFullScreen src="https://www.youtube.com/embed/1y_kfWUCFDQ" />
   </div>
   ```

## Customization

- **Aspect Ratio**: You can customize the aspect ratio by changing the class names to match your desired ratio (e.g., `ratio-16x9`, `ratio-4x3`).

- **Video Source**: Change the `src` attribute of the `iframe` to embed different videos.

- **Styling**: Additional CSS classes can be added to the `Card` or `CardBody` components to further style the video container.

## References

- **Reactstrap Documentation**: Learn about the `reactstrap` components used in this file [here](https://reactstrap.github.io/).
- **Bootstrap Documentation**: Explore Bootstrap's responsive embed classes [here](https://getbootstrap.com/docs/5.1/helpers/ratio/).

By utilizing these responsive video embedding techniques, developers can ensure that videos are displayed correctly across various devices and screen sizes.

# Slideindividual Component Documentation

The `slideindividual.js` file defines a **React component** named `Slideindividual` which utilizes the `reactstrap` library to create a carousel component. This carousel displays a series of images that can be navigated through by clicking on next or previous buttons.

## Table of Contents

1. [Component Overview](#component-overview)
2. [Dependencies](#dependencies)
3. [Component Details](#component-details)
    - [State Management](#state-management)
    - [Event Handlers](#event-handlers)
    - [Rendering Method](#rendering-method)
4. [How to Use](#how-to-use)
5. [Code Explanation](#code-explanation)

## Component Overview

The `Slideindividual` component is a **carousel** that displays a sequence of images. Users can move to the next or previous image using controls. The carousel is built using the following key features:
- Transition animations while changing slides.
- Controls to navigate between slides.
- A looping mechanism that resets to the start or end when the user navigates beyond the available images.

## Dependencies

This component relies on the following libraries:
- **React**: For creating and managing the component state and lifecycle.
- **reactstrap**: For utilizing pre-styled components to construct the carousel, like `Carousel`, `CarouselItem`, and `CarouselControl`.

## Component Details

### State Management

The component's state consists of:
- `activeIndex`: Tracks which slide is currently active/displayed.

### Event Handlers

1. **`next`**: Advances the carousel to the next slide. If the current slide is the last slide, it wraps around to the first slide.
2. **`previous`**: Moves the carousel to the previous slide. If the current slide is the first slide, it wraps around to the last slide.
3. **`goToIndex`**: Directly navigates to a specified slide index.
4. **`onExiting`**: Sets a flag to prevent the carousel from transitioning until the current transition is complete.
5. **`onExited`**: Resets the flag to allow new transitions.

### Rendering Method

The component renders a carousel with each image being wrapped within a `CarouselItem`. The navigation controls are rendered using `CarouselControl`.

## How to Use

1. **Import the Component**: Ensure that the `Slideindividual` component is imported into the desired file.
2. **Render the Component**: Place the `<Slideindividual />` tag within the component where the carousel should be displayed.
3. **Customize Images**: Replace `img1`, `img2`, and `img3` with your images by updating the `items` array with paths to your desired images.

## Code Explanation

Here's a breakdown of the key parts of the code:

```javascript
// Importing React and necessary components from reactstrap
import React, { Component } from "react";
import { Carousel, CarouselItem, CarouselControl } from "reactstrap";

// Image imports
import img1 from "../../../assets/images/small/img-1.jpg";
import img2 from "../../../assets/images/small/img-2.jpg";
import img3 from "../../../assets/images/small/img-3.jpg";

// Image items for the carousel
const items = [
  { src: img1, altText: "Slide 1", caption: "Slide 1" },
  { src: img2, altText: "Slide 2", caption: "Slide 2" },
  { src: img3, altText: "Slide 3", caption: "Slide 3" },
];

class Slideindividual extends Component {
  constructor(props) {
    super(props);
    this.state = { activeIndex: 0 }; // Initial state
    this.next = this.next.bind(this);
    this.previous = this.previous.bind(this);
    this.goToIndex = this.goToIndex.bind(this);
    this.onExiting = this.onExiting.bind(this);
    this.onExited = this.onExited.bind(this);
  }

  // Event handler methods

  render() {
    const { activeIndex } = this.state;
    const slides = items.map(item => {
      return (
        <CarouselItem
          onExiting={this.onExiting}
          onExited={this.onExited}
          key={item.src}
          interval={1000}
        >
          <img src={item.src} className="d-block w-100" alt={item.altText} />
        </CarouselItem>
      );
    });

    return (
      <React.Fragment>
        <div className="carousel-inner">
          <Carousel activeIndex={activeIndex} next={this.next} previous={this.previous}>
            {slides}
            <CarouselControl direction="prev" directionText="Previous" onClickHandler={this.previous} />
            <CarouselControl direction="next" directionText="Next" onClickHandler={this.next} />
          </Carousel>
        </div>
      </React.Fragment>
    );
  }
}

export default Slideindividual;
```

This documentation provides a clear understanding of how the `Slideindividual` component functions and how it can be integrated into a React application. Customize the images and controls as needed for your specific application.

# UiTabsAccordions.js Documentation

The `UiTabsAccordions.js` file is a React component that demonstrates the implementation of tabs and accordions using the `reactstrap` library. It showcases different styles and configurations of tabs and accordion panels, providing a robust interface for organizing content into collapsible and selectable sections.

## Table of Contents
1. [Component Overview](#component-overview)
2. [Features](#features)
3. [Code Explanation](#code-explanation)
4. [Usage](#usage)
5. [Styles and Classes](#styles-and-classes)

---

## Component Overview

The `UiTabsAccordions` component is designed to display navigational tabs and accordion panels. It uses React state to manage the active tab and open accordion panels. This component is ideal for creating a dynamic and interactive user interface where content can be categorized into tabs and collapsible sections.

## Features

- **Default Tabs**: Standard horizontal tabs with multiple panes.
- **Justify Tabs**: Tabs that are justified evenly across the available space.
- **Vertical Nav Tabs**: Tabs displayed vertically, ideal for side navigation.
- **Custom Tabs**: Tabs with custom styles and configurations.
- **Default Collapse**: Simple collapsible sections that can be toggled open or closed.
- **Accordion Example**: Grouped collapsible sections that function as an accordion.

## Code Explanation

### State Management

- **State Variables**: The component uses several state variables to control the active tab and the open/closed state of accordion panels. These include `activeTab`, `activeTabV`, `activeTabJustify`, `col1`, `col2`, `col3`, and `col5`.

- **State Functions**: Functions such as `toggle`, `toggleV`, `toggleCustomJustified`, and `toggleCustomJustified2` are used to change the state when a tab or accordion panel is clicked.

### Tabs

Tabs are implemented using `reactstrap`'s `Nav`, `NavItem`, `NavLink`, `TabContent`, and `TabPane` components. Each tab is associated with a `TabPane` that contains the content displayed when the tab is active.

```jsx
<Nav tabs>
  <NavItem>
    <NavLink
      style={{ cursor: "pointer" }}
      className={classnames({ active: activeTab === "1" })}
      onClick={() => { toggle("1") }}
    >
      <span className="d-block d-sm-none"><i className="fas fa-home"></i></span>
      <span className="d-none d-sm-block">Home</span>
    </NavLink>
  </NavItem>
  ...
</Nav>
<TabContent activeTab={activeTab} className="p-3 text-muted">
  <TabPane tabId="1">
    <p className="mb-0">Content for Home tab.</p>
  </TabPane>
  ...
</TabContent>
```

### Accordions

Accordions are implemented using `reactstrap`'s `Collapse` component. Each accordion item is controlled by a button that toggles the open/closed state of the `Collapse`.

```jsx
<div className="accordion" id="accordionExample">
  <div className="accordion-item">
    <h2 className="accordion-header" id="headingOne">
      <button
        className="accordion-button"
        type="button"
        onClick={() => { setcol1(!col1) }}
        style={{ cursor: "pointer" }}
      >
        Accordion Item #1
      </button>
    </h2>
    <Collapse id="collapseOne" className="accordion-collapse show" isOpen={col1}>
      <div className="accordion-body">
        <strong>This is the first item's accordion body.</strong>
      </div>
    </Collapse>
  </div>
  ...
</div>
```

## Usage

To use the `UiTabsAccordions` component, simply import it into your React application and include it in your JSX. Ensure that `reactstrap` and `classnames` packages are installed in your project.

```jsx
import UiTabsAccordions from './path/to/UiTabsAccordions';

function App() {
  return (
    <div>
      <UiTabsAccordions />
    </div>
  );
}

export default App;
```

## Styles and Classes

- **`Nav` and `TabContent`**: Used for tabs with classes like `nav-tabs`, `nav-justified`, and `text-muted`.
- **`Collapse`**: Used for collapsible sections with classes like `accordion-collapse`.
- **Icons**: Utilizes Font Awesome icons for visual representation in tabs.

This documentation provides an overview and detailed explanation of how the `UiTabsAccordions.js` component is structured and utilized. It is a comprehensive guide for developers looking to implement tabbed interfaces and accordions in their React applications using `reactstrap`.

# UiTypography.js Documentation

The `UiTypography.js` file is a React component that provides a demonstration of various typography elements using Bootstrap's styling. This component showcases different typographic elements such as headings, inline text elements, lists, blockquotes, and description lists. It is a part of a UI Elements module that helps in maintaining consistent typography throughout a web application.

## Table of Contents

1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [Typography Elements](#typography-elements)
   - [Font Family](#font-family)
   - [Headings](#headings)
   - [Font Weight](#font-weight)
   - [Display Headings](#display-headings)
   - [Inline Text Elements](#inline-text-elements)
   - [Unstyled List](#unstyled-list)
   - [Inline List](#inline-list)
   - [Blockquotes](#blockquotes)
   - [Description List Alignment](#description-list-alignment)
5. [Usage](#usage)

## Overview

The `UiTypography` component leverages Bootstrap's typography utilities to present a variety of typographic styles and elements. This is useful for developers looking to implement consistent typography across their web projects.

## Dependencies

This component relies on several external dependencies:
- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A library that provides Bootstrap 4 components as React components.
- **Breadcrumbs**: A custom component for rendering breadcrumb navigation.

## Component Structure

The component is structured into multiple sections, each demonstrating different typography features available in Bootstrap. The layout is divided into Bootstrap grid columns for a responsive design.

```jsx
const UiTypography = () => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="UI Elements" breadcrumbItem="Typography" />
        {/* Typography elements are demonstrated in the following sections */}
      </div>
    </React.Fragment>
  );
}
```

## Typography Elements

### Font Family
- Displays the default font family used in the application.
- Uses `"DM Sans", sans-serif`.

### Headings
- Demonstrates all HTML heading tags (`<h1>` through `<h6>`) with Bootstrap styling.
- Each heading is accompanied by a description of its size and weight.

### Font Weight
- Displays examples of different font weights using headings with `400` and `600` weights.

### Display Headings
- Special larger headings for highlighting important content.
- Uses Bootstrap classes `display-1` to `display-6`.

### Inline Text Elements
- Styling for common inline HTML5 elements such as `<mark>`, `<del>`, `<ins>`, `<u>`, `<small>`, `<strong>`, and `<em>`.

### Unstyled List
- Demonstrates removing default list styles using `list-unstyled`.
- Nested lists are also demonstrated.

### Inline List
- Demonstrates inline list styling using `list-inline` and `list-inline-item`.

### Blockquotes
- Provides styling for quoting blocks of content.
- Demonstrates both standard and reverse blockquote styles.

### Description List Alignment
- Shows how to align terms and descriptions horizontally using Bootstrap's grid system.
- Demonstrates the use of `.text-truncate` for truncating text with ellipsis.

## Usage

To use this component, ensure that your project has React, Reactstrap, and Bootstrap installed. Import the `UiTypography` component into your desired file and include it in your JSX as follows:

```jsx
import UiTypography from './path-to/UiTypography';

function App() {
  return (
    <div>
      <UiTypography />
    </div>
  );
}

export default App;
```

This component is ideal for projects where a consistent typography style is needed, providing a quick reference for various text styles available in Bootstrap.

# Documentation for `UiSessionTimeout.js`

## Overview

The `UiSessionTimeout.js` file implements a session timeout notification system using **React** and **react-bootstrap-sweetalert**. This component warns users when their session is about to expire and offers options to either extend the session or log out. The system manages user inactivity by monitoring idle time and displaying an alert dialog before a session expires.

## Features

- **Session Timeout Alert**: Displays an alert when the user session is about to expire.
- **Auto-Redirection**: Redirects the user to a login page after a set period of inactivity.
- **User Interaction**: Allows users to either stay connected or log out when alerted.
- **Session Management**: Monitors and updates user activity to reset session expiration.

## Components

- **Breadcrumbs**: Used to display the current UI path for better navigation awareness.
- **SweetAlert**: Utilized for displaying customizable alerts to the user.

## Code Explanation

### Imports

```javascript
import React, { Component } from "react";
import SweetAlert from "react-bootstrap-sweetalert";
import { Card, Row, Col, CardBody, CardTitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

- **React**: A JavaScript library for building user interfaces.
- **SweetAlert**: A library for creating beautiful alerts and dialog boxes.
- **Reactstrap**: Provides Bootstrap 4 components for React.
- **Breadcrumbs**: A custom component that shows the path within the application.

### Component State

```javascript
this.state = {
  timeralert: null,
  timerswitch: false,
  seconds: 0
};
```

- **timeralert**: Stores the SweetAlert component to be displayed.
- **timerswitch**: Indicates if the timer is active.
- **seconds**: Tracks the number of seconds since the last user activity.

### Key Functions

- **componentDidMount()**: Triggers the main function when the component is first rendered.

```javascript
componentDidMount() {
  this.main_function();
}
```

- **main_function()**: Initializes a timeout to check for user activity and manage session expiration.

```javascript
main_function() {
  setTimeout(
    function () {
      setTimeout(
        function () {
          this.function1();
        }.bind(this),
        6000
      );
      this.function2();
    }.bind(this),
    6000
  );
}
```

- **function1()**: Redirects the user to the login page if the session has expired.

```javascript
function1() {
  if (window.location.pathname === "/ui-session-timeout") {
    window.location = "/login";
  }
}
```

- **function2()**: Manages the alert display and session timer.

```javascript
function2() {
  this.tick();
  const nextmsg = () => (
    <SweetAlert
      showCancel
      confirmBtnText="Stay Connected"
      cancelBtnText="Logout"
      confirmBtnBsStyle="success"
      cancelBtnBsStyle="danger"
      title="Your Session is About to Expire!"
      onCancel={() => this.hideAlert()}
      onConfirm={() => this.confirmAlert()}
    >
      Redirecting in 10s seconds.<br></br>
    </SweetAlert>
  );
  this.setState({ timeralert: nextmsg() });
}
```

- **tick()**: Increments the session inactivity counter every second.

```javascript
tick() {
  this.interval = setInterval(() => {
    this.setState(prevState => ({ seconds: prevState.seconds + 1 }));
  }, 1000);
}
```

- **hideAlert()**: Redirects the user to the login page when the session expires.

```javascript
hideAlert() {
  window.location = "/login";
}
```

- **confirmAlert()**: Closes the alert and resets the session timer.

```javascript
confirmAlert() {
  this.setState({ timeralert: null });
}
```

### Render Method

Displays the session timeout alert and the main content of the page.

```javascript
render() {
  return (
    <React.Fragment>
      <div className="page-content">
        {this.state.timeralert}
        <Breadcrumbs title="UI Elements" breadcrumbItem="Session Timeout" />
        <Row>
          <Col>
            <Card>
              <CardBody>
                <CardTitle>Bootstrap-session-timeout</CardTitle>
                <p className="sub-header">
                  Session timeout and keep-alive control with a nice Bootstrap warning dialog.
                </p>
                <div>
                  <p>
                    After a set amount of idle time, a Bootstrap warning dialog is shown to the
                    user with the option to either log out, or stay connected...
                  </p>
                </div>
              </CardBody>
            </Card>
          </Col>
        </Row>
      </div>
    </React.Fragment>
  );
}
```

### Use Case

This component is suitable for enhancing the user experience in web applications by managing user sessions effectively. It ensures that users are alerted before a session timeout, allowing them to choose to remain logged in or to log out, thus protecting sensitive data and maintaining application security.

## Conclusion

The `UiSessionTimeout.js` file provides a user-friendly way to manage session timeouts in React applications. By using SweetAlert for alerts and handling user interactions, it effectively notifies users about session timeouts and implements graceful session management.

# UiSweetAlert.js Documentation

## Overview
The `UiSweetAlert.js` file is a React component that leverages the `react-bootstrap-sweetalert` library to create a variety of beautiful, responsive, and customizable alert dialogs within a UI. These dialogs are a modern alternative to traditional JavaScript alert boxes, offering more functionality and aesthetics, with zero dependencies.

---

## Features

### Key Features
- **Basic Alerts**: Simple alert dialogs with a single confirmation button.
- **Title and Text Alerts**: Alerts with a title and additional descriptive text.
- **Success and Error Alerts**: Alerts to indicate success or failure scenarios.
- **Confirm and Cancel Alerts**: Alerts that require user confirmation or cancellation.
- **Custom Alerts**: Alerts with custom content including images, HTML, and different styles.
- **Auto-Close Alerts**: Alerts that automatically close after a set duration.
- **Chained Alerts**: Sequence of alerts that appear one after the other.
- **Dynamic Alerts**: Alerts that handle dynamic content such as AJAX responses.

---

## Structure

### State Management
The component uses React's `useState` for managing the visibility of various alerts:
```javascript
const [basic, setbasic] = useState(false);
const [with_title, setwith_title] = useState(false);
// ... other state variables
```

### Functions
Several internal functions handle changes and manage the alert's lifecycle:
- **handleStep1Change**, **handleStep2Change**, **handleStep3Change**: These functions manage input changes for chained alerts.

---

## UI Elements and Interactions

### Breadcrumb
The breadcrumb component at the top indicates navigation hierarchy:
```jsx
<Breadcrumbs title="UI Elements" breadcrumbItem="SweetAlert" />
```

### Buttons and Alerts
Each alert type is triggered by a button. When a button is clicked, it updates the corresponding state to display the alert:
```jsx
<Button color="primary" onClick={() => { setbasic(true); }} id="sa-basic"> Click me </Button>
{basic ? (
  <SweetAlert title="Any fool can use a computer" onConfirm={() => { setbasic(false); }} />
) : null}
```

### Examples
- **Basic Message**: Triggered by a button, displays a simple message.
- **Title with Text**: Adds a title and explanation text.
- **Success Message**: Displays a success alert with optional cancel buttons.
- **Warning and Confirmation**: Alerts the user before performing a critical action, like deletion.
- **Custom Image Header**: Display alerts with images.
- **Auto-Close Timer**: Alerts that disappear after a specific time.
- **Chaining Modals**: Sequence of modals requiring user input.
- **Dynamic Content**: Fetch and display dynamic data, such as a public IP.

---

## Code Snippets

### Example of a Basic Alert
```jsx
{basic ? (
  <SweetAlert title="Any fool can use a computer" onConfirm={() => { setbasic(false); }} />
) : null}
```

### Example of a Success Dialog with Title and Description
```jsx
{success_dlg ? (
  <SweetAlert success title={dynamic_title} onConfirm={() => { setsuccess_dlg(false); }} >
    {dynamic_description}
  </SweetAlert>
) : null}
```

### Example of Chained Modals
```jsx
{step1 ? (
  <SweetAlert showCancel title="Question 1" cancelBtnBsStyle="danger" confirmBtnText="Next" onConfirm={() => { setstep1(false); setstep2(true); }}
  onCancel={() => { setstep1(false); }}>
    Chaining swal2 modals is easy
    <input type="text" className="form-control" onChange={(e) => { handleStep1Change(e); }} />
  </SweetAlert>
) : null}
```

---

## Conclusion
The `UiSweetAlert.js` component provides a comprehensive suite of alert dialogs that enhance user interaction with modern and stylish prompts. With its ability to handle various alert types and customization options, it significantly improves the UI experience, making it an essential element in modern web applications.

# UiRangeSlider.js Documentation 📊

## Introduction
The `UiRangeSlider.js` file is a React component that demonstrates the use of the **React Range Slider** library. It offers a responsive and customizable range slider component that can be used to select a value from a range. The component is built using the `reactstrap` library for styling and layout, and provides various configurations and customization options for the slider.

## Features
- **Default Slider**: A simple slider with default settings.
- **Min-Max Slider**: Slider with a specified minimum and maximum value.
- **Step Increment**: Slider with step increments.
- **Prefix and Postfix**: Format slider values with prefixes and postfixes.
- **Custom Values and Labels**: Slider with custom labels for each step.
- **Reverse Slider**: Slider with reversed values.
- **Floating Point Precision**: Slider with fractional steps.
- **Extra Example**: Custom formatting and additional examples.

## Usage

### Importing Required Components
```javascript
import React, { useState } from "react";
import { Row, Col, Card, CardBody, CardTitle } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import Slider from "react-rangeslider";
import "react-rangeslider/lib/index.css";
```

### Component Structure
The `UiRangeSlider` component is structured into several sections, each demonstrating a different feature of the range slider.

#### Default Slider
```jsx
<Col md={6}>
    <div className="p-3">
        <h5 className="font-size-14 mb-3 mt-0">Default</h5>
        <span className="float-start mt-4">0</span>
        <span className="float-end mt-4">100</span>
        <Slider value={def} orientation="horizontal" onChange={value => { setdef(value) }} />
    </div>
</Col>
```

#### Min-Max Slider
```jsx
<Col md={6}>
    <div className="p-3">
        <h5 className="font-size-14 mb-3 mt-0">Min-Max</h5>
        <span className="float-start mt-4">30</span>
        <span className="float-end mt-4">90</span>
        <Slider value={min_max} min={30} max={90} orientation="horizontal" onChange={value => { setmin_max(value) }} />
    </div>
</Col>
```

#### Prefix and Postfix Slider
```jsx
<Col md={6}>
    <div className="p-3">
        <h5 className="font-size-14 mb-3 mt-0">Prefix</h5>
        <span className="float-start mt-4">0</span>
        <span className="float-end mt-4">100</span>
        <Slider min={0} max={100} format={formatkg} value={prefix} onChange={value => { setprefix(value) }} />
    </div>
</Col>

<Col md={6}>
    <div className="p-3">
        <h5 className="font-size-14 mb-3 mt-0">Postfixes</h5>
        <span className="float-start mt-4">0</span>
        <span className="float-end mt-4">100</span>
        <Slider min={0} max={100} format={formatdollar} value={postfix} onChange={value => { setpostfix(value) }} />
    </div>
</Col>
```

#### Custom Values and Labels
```jsx
<Col md={6}>
    <div className="p-3">
        <h5 className="font-size-14 mb-3 mt-0"> Custom Values </h5>
        <Slider value={custom_val} min={1} max={12} labels={labels} orientation="horizontal" onChange={value => { setcustom_val(value) }} />
    </div>
</Col>
```

### Full Component Code
```jsx
const UiRangeSlider = () => {
    const formatkg = value => "$ " + value;
    const formatdollar = value => value + " kg";
    const extra_age = value => value + " Age";
    const [def, setdef] = useState(15);
    const [min_max, setmin_max] = useState(70);
    const [step, setstep] = useState(25);
    const [prefix, setprefix] = useState(50);
    const [postfix, setpostfix] = useState(85);
    const [custom_val, setcustom_val] = useState(5);
    const [float_val, setfloat_val] = useState(55.5);
    const [extra, setextra] = useState(52);
    const [hide, sethide] = useState(5);

    const labels = {
        1: "Jan", 2: "Feb", 3: "Mar", 4: "Apr",
        5: "May", 6: "Jun", 7: "Jul", 8: "Aug",
        9: "Sep", 10: "Oct", 11: "Nov", 12: "Dec"
    };

    return (
        <React.Fragment>
            <div className="page-content">
                <Breadcrumbs title="UI Elements" breadcrumbItem="Range Slider" />
                <Row>
                    <Col className="col-12">
                        <Card>
                            <CardBody>
                                <CardTitle className="h4">React Rangeslider</CardTitle>
                                <p className="card-title-desc">Cool, comfortable, responsive and easily customizable range slider</p>
                                {/* Slider Examples */}
                            </CardBody>
                        </Card>
                    </Col>
                </Row>
            </div>
        </React.Fragment>
    );
};

export default UiRangeSlider;
```

## Conclusion
The `UiRangeSlider.js` file provides a comprehensive example of using the React Range Slider to create various types of sliders with different functionalities. The sliders can be tailored with prefixes, postfixes, custom values, reversed values, and more. This component serves as a robust solution for integrating range sliders into React applications with ease and flexibility.

# UiRating.js Documentation

This documentation provides a detailed overview of the `UiRating.js` React component. This component is designed to display various types of rating systems using stars and customizable icons. It leverages the `react-rating` and `react-rating-tooltip` libraries for its functionality.

## Table of Contents

1. [Overview](#overview)
2. [Imports](#imports)
3. [State Variables](#state-variables)
4. [Rating Variants](#rating-variants)
5. [Usage](#usage)
6. [Code Explanation](#code-explanation)
7. [Conclusion](#conclusion)

## Overview

The `UiRating.js` component is a part of the UI Elements module, specifically for implementing rating systems. It provides different styles and functionalities for ratings, including default ratings, disabled ratings, customized icons, and more.

## Imports

The component imports necessary modules and components as follows:

```javascript
import React, { useState } from "react";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { Row, Col, Card, CardBody } from "reactstrap";
import Rating from "react-rating";
import RatingTooltip from "react-rating-tooltip";
```

- **React & useState**: Core React library for building UI and managing state.
- **Breadcrumbs**: A component for displaying the navigation breadcrumb.
- **reactstrap Components**: Layout and UI components from the Reactstrap library.
- **Rating & RatingTooltip**: Libraries for handling rating functionalities.

## State Variables

The component uses two state variables:

- **def**: Stores the rating value for the default rating.
- **customize**: Stores the rating value for customized ratings.

These states are managed using the `useState` hook.

## Rating Variants

Below are the different types of ratings implemented in the component:

1. **Default Rating**: Basic star rating with tooltip.
2. **Disabled Rating**: A non-interactive rating display.
3. **Readonly Rating**: Displays a static rating value.
4. **Customized Heart Rating**: Uses heart icons instead of stars.
5. **Handle Events**: Alerts the user with the selected rating.
6. **Customize Tooltips**: Uses custom tooltips for each rating point.
7. **Custom Icons**: Utilizes custom icons for ratings.
8. **Fractional Rating**: Allows fractional rating values for more precise scores.

## Usage

To use this component, it should be included within a parent component or a page where you wish to display different rating systems. Each rating system is displayed in a grid layout using Bootstrap's grid system.

## Code Explanation

The component renders a set of rating systems in a grid layout. Each rating system is wrapped in a `Col` component to maintain responsiveness. The `Rating` and `RatingTooltip` components are configured with properties such as `max`, `tooltipContent`, and custom icon components.

### Example of a Default Rating:

```jsx
<RatingTooltip
  max={5}
  onChange={rate => { setdef(rate); }}
  ActiveComponent={<i className="mdi mdi-star text-primary" />}
  InActiveComponent={<i className="mdi mdi-star-outline text-muted" />}
/>
<span>{def}</span>
```

### Explanation:

- **RatingTooltip**: Provides a rating component with tooltips for displaying hints or descriptions for each rating level.
- **max**: The maximum rating value.
- **onChange**: A callback function to update the state when a rating is selected.
- **ActiveComponent**: The icon used to represent an active (selected) rating.
- **InActiveComponent**: The icon used for inactive (unselected) ratings.

## Conclusion

The `UiRating.js` component is a versatile and interactive way to incorporate rating systems into your application. It provides a variety of styles and functionalities to meet different design requirements. This component is a great addition to any UI where user feedback or ratings are necessary.

For further customization, developers can modify the styles and behavior by adjusting properties and passing additional configuration options to the `Rating` and `RatingTooltip` components.

# 📄 UiModal.js Documentation

## Table of Contents
- [Introduction](#introduction)
- [Dependencies](#dependencies)
- [Component Description](#component-description)
- [Modal Types](#modal-types)
  - [Standard Modal](#standard-modal)
  - [Large Modal](#large-modal)
  - [Extra Large Modal](#extra-large-modal)
  - [Small Modal](#small-modal)
  - [Center Modal](#center-modal)
  - [Scrollable Modal](#scrollable-modal)
  - [Static Backdrop Modal](#static-backdrop-modal)
  - [Fullscreen Modal](#fullscreen-modal)
- [Functions](#functions)
  - [`removeBodyCss`](#removebodycss)
- [How to Use](#how-to-use)

## Introduction
The **UiModal.js** file is a React component that provides a variety of customizable modal dialog boxes using the Reactstrap library. These modals can be used for different purposes such as displaying information, alerts, or forms.

## Dependencies
The component relies on the following dependencies:
- **React**: For building the component and managing its state.
- **Reactstrap**: For UI components such as `Modal`, `Row`, `Col`, `Card`, etc.
- **Breadcrumbs**: A custom component for navigation breadcrumbs.

## Component Description
The `UiModal` component showcases different modal dialog styles, including various sizes and functionalities such as scrolling content and static backdrops. The component manages different modal states using React hooks (`useState`).

## Modal Types
The component includes several types of modals, each demonstrating different features. Below is an explanation of each modal type:

### Standard Modal
- **Description**: A basic modal with a standard size.
- **Use Case**: General purpose dialogs for information or confirmation.

### Large Modal
- **Description**: A larger modal for displaying more content.
- **Use Case**: Suitable for when you need more space for content like forms or detailed information.

### Extra Large Modal
- **Description**: An extra-large modal for extensive content.
- **Use Case**: Good for displaying comprehensive content such as large tables or complex forms.

### Small Modal
- **Description**: A smaller modal for concise information.
- **Use Case**: Ideal for quick alerts or small confirmations.

### Center Modal
- **Description**: A modal that appears centered on the screen.
- **Use Case**: Useful for drawing attention to the content without distractions.

### Scrollable Modal
- **Description**: A modal with scrolling capability.
- **Use Case**: Perfect for displaying lengthy content that doesn’t fit in the default modal size.

### Static Backdrop Modal
- **Description**: A modal that doesn't close when clicking outside of it.
- **Use Case**: Useful for critical actions where unintentional closure should be prevented.

### Fullscreen Modal
- **Description**: A modal that takes up the entire screen.
- **Use Case**: Best used for immersive content or applications.

## Functions

### `removeBodyCss`
- **Purpose**: Prevents padding issues when modals are toggled by adding a `no_padding` class to the `body`.
- **Usage**: Called in all toggle functions to ensure a consistent layout.

## How to Use
To implement the `UiModal` component in your project, follow these steps:

1. **Import the Component**:
   ```jsx
   import UiModal from './path/to/UiModal';
   ```

2. **Use the Component**:
   ```jsx
   <UiModal />
   ```

3. **Ensure Dependencies**:
   Ensure that Reactstrap is installed in your project as it is required for the UI components.

4. **Customizing Modals**:
   Each modal type can be customized by adjusting the states and the contents inside the modal bodies.

This component is a versatile tool for creating interactive and informative dialogs within a React application, leveraging the power of Reactstrap to ensure responsive and attractive UI elements.

# UiProgressbar.js Documentation 📊

This file, **UiProgressbar.js**, is a React component that provides a variety of Bootstrap-styled progress bars. These progress bars can visually indicate the status of a task or process, and come in several styles, colors, and sizes to suit different needs.

## Table of Contents
1. [Overview](#overview)
2. [Component Structure](#component-structure)
3. [Progress Bar Variants](#progress-bar-variants)
    - [Default Examples](#default-examples)
    - [Backgrounds](#backgrounds)
    - [Labels](#labels)
    - [Multiple Bars](#multiple-bars)
    - [Custom Height](#custom-height)
    - [Striped](#striped)
    - [Animated Stripes](#animated-stripes)
4. [Usage](#usage)
5. [Dependencies](#dependencies)

## Overview
The `UiProgressbar` component leverages Bootstrap's `Progress` component from "reactstrap" to create progress bars that can show various levels of progress using visual indicators. The component includes several examples to showcase different types of progress bars, with different colors, labels, and animations.

## Component Structure
The component is structured into several `Row` and `Col` elements, each containing a `Card` component. Each card showcases different styles and functionalities of progress bars.

```jsx
<Row>
    <Col lg={6}>
        <Card>
            <CardBody>
                <CardTitle className="h4">Default Examples</CardTitle>
                <Progress color="primary" value={25} />
            </CardBody>
        </Card>
    </Col>
    ...
</Row>
```

## Progress Bar Variants

### Default Examples
- **Basic Progress Bars**: Simple progress bars with different values (e.g., 25%, 50%, 75%, 100%) using a primary color.

### Backgrounds
- **Colored Progress Bars**: Demonstrates the use of different background colors such as success, info, warning, and danger.

### Labels
- **Labeled Progress Bars**: Displays text inside the progress bar to indicate the percentage complete.

### Multiple Bars
- **Stacked Bars**: Combines multiple progress bars within a single container, showing cumulative progress.

### Custom Height
- **Sized Progress Bars**: Allows customization of the height of progress bars, providing options for thin (3px) and thick (20px) bars.

### Striped
- **Striped Progress Bars**: Adds a striped pattern to the progress bar, enhancing its visual appeal.

### Animated Stripes
- **Animated Stripes**: Animates the striped pattern across the progress bar for a dynamic effect.

## Usage
To use this component, ensure your project is set up to handle React and Bootstrap components. Import the `UiProgressbar` component and include it in your JSX:

```jsx
import UiProgressbar from './path/to/UiProgressbar';

function App() {
  return (
    <div>
      <UiProgressbar />
    </div>
  );
}
```

## Dependencies
This component relies on the following:
- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: Bootstrap components built with React.
- **Bootstrap**: A CSS framework for developing responsive and mobile-first websites.

These dependencies should be included in your project's `package.json` to ensure proper functionality.

---

The `UiProgressbar.js` component is a versatile UI element for displaying task progress clearly and efficiently. With customizable options, it can easily be adapted to fit the needs of any web application.

# UiImages.js Documentation

This component in the React application demonstrates various ways to present and style images using Bootstrap's styling utilities. It includes features such as rounded images, responsive images, and thumbnails, showcasing different avatar sizes and configurations.

---

## Index

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Component Structure](#component-structure)
4. [Features](#features)
   - [Image Rounded & Circle](#image-rounded--circle)
   - [Image Thumbnails](#image-thumbnails)
   - [Responsive Images](#responsive-images)
   - [Image Sizes](#image-sizes)
5. [Code Explanation](#code-explanation)
6. [Conclusion](#conclusion)

---

## Introduction

The **UiImages** component is a part of the UI Elements suite that showcases image presentations using Bootstrap. It provides examples of how to style images in a React application with different Bootstrap classes for rounded corners, circular avatars, thumbnails, and responsive behavior.

## Imports

The component begins with several imports necessary for its functionality:

- **React**: The core library for building user interfaces.
- **Bootstrap Components**: Components from `reactstrap` for layout and styling.
- **Images**: Various images and avatars used within the component.
- **Breadcrumbs**: A breadcrumb navigation component to display the current page context.

## Component Structure

The component is structured using React functional components. It utilizes Bootstrap's grid layout with `Row` and `Col` components for organizing the visual presentation of images.

```jsx
const UiImages = () => { 
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="UI Elements" breadcrumbItem="Images" />
        // Image presentation code...
      </div>
    </React.Fragment>
  );
};
```

## Features

### Image Rounded & Circle

This section demonstrates how to use the `.rounded` and `.rounded-circle` classes to create images with rounded corners and circular shapes.

```jsx
<Row>
  <Col md={6}>
    <img className="rounded me-2" alt="" width="200" src={img4} />
  </Col>
  <Col md={6}>
    <div className="mt-4 mt-md-0">
      <img className="rounded-circle avatar-xl" alt="" src={avatar4} />
    </div>
  </Col>
</Row>
```

### Image Thumbnails

The `.img-thumbnail` class is used to add a border around the images, giving them a thumbnail appearance with a rounded border.

```jsx
<Row>
  <Col md={6}>
    <img className="img-thumbnail" alt="" width="200" src={img3} />
  </Col>
  <Col md={6}>
    <div className="mt-4 mt-md-0">
      <img className="img-thumbnail rounded-circle avatar-xl" alt="" src={avatar3} />
    </div>
  </Col>
</Row>
```

### Responsive Images

Bootstrap's `.img-fluid` class is used to ensure that images scale correctly within their parent containers, making them responsive.

```jsx
<CardImg className="img-fluid" src={img2} alt="" />
```

### Image Sizes

Demonstrates different avatar sizes using custom classes such as `.avatar-sm`, `.avatar-md`, and `.avatar-lg` for both rounded and circular images.

```jsx
<Col lg={4}>
  <div>
    <img src={avatar3} className="rounded avatar-sm" alt="" />
    <p className="mt-2 mb-lg-0"><code>.avatar-sm</code></p>
  </div>
</Col>
```

## Code Explanation

The component uses Bootstrap classes extensively to style images. Here is a brief explanation of some key parts:

- **Rounded & Circle**: Demonstrates the use of `rounded` for rounded corners and `rounded-circle` for circular images.
- **Thumbnails**: Uses the `img-thumbnail` class to give images a bordered look.
- **Responsive**: The `img-fluid` class ensures images adjust their size according to the container.
- **Avatar Sizes**: Custom classes like `avatar-sm` help define small, medium, and large avatar sizes.

## Conclusion

The **UiImages** component effectively demonstrates the use of Bootstrap's image styling capabilities within a React application. The use of rounded corners, circle shapes, responsiveness, and different sizes provides developers with a variety of options to enhance the visual presentation of images in their applications.

# 📚 UiLightbox.js Documentation

## Overview

The `UiLightbox.js` component is a React functional component designed to display images, videos, or even maps inside a Lightbox. Lightbox is a script used to overlay images on the current page. This component leverages the `react-image-lightbox` and `react-modal-video` libraries to provide a rich and interactive user experience. It offers features like image gallery display, zoom functionalities, and video popups. 

---

## Table of Contents

1. [Installation](#installation)
2. [Component Structure](#component-structure)
3. [Features](#features)
4. [Code Explanation](#code-explanation)
5. [Usage](#usage)
6. [Props](#props)
7. [Conclusion](#conclusion)

---

## Installation

To use the `UiLightbox` component, you must have the `reactstrap`, `react-image-lightbox`, and `react-modal-video` libraries installed in your project. You can install these packages using npm:

```bash
npm install reactstrap react-image-lightbox react-modal-video
```

---

## Component Structure

The component is structured using several Reactstrap elements and custom components. Here's a breakdown:

- **Breadcrumbs**: Provides navigation indicating the current page's location.
- **Card**: Used for organizing content into sections.
- **Lightbox**: Used to display images in a modal overlay.
- **ModalVideo**: Displays video content in a modal dialog.
- **Modal**: For displaying forms and extra content in a modal dialog.

---

## Features

- **Single Image Lightbox**: Displays a single image in a modal overlay with options like zoom and effects.
- **Lightbox Gallery**: Allows navigation through a series of images.
- **Zoom Gallery**: Provides zoom functionality for images.
- **Video & Map Popups**: Support for video and map display in a modal.
- **Form Popup**: Displays a form in a modal with input fields for name, email, password, and subject.

---

## Code Explanation

Below is a detailed explanation of the key code blocks in the `UiLightbox.js`:

### Image Array

```javascript
const images = [img1, img2, img3, img4, img5, img6];
```

- An array that stores the paths to the images to be displayed in the Lightbox.

### State Management

```javascript
const [photoIndex, setphotoIndex] = useState(0);
const [isFits, setisFits] = useState(false);
const [isEffects, setisEffects] = useState(false);
const [isGallery, setisGallery] = useState(false);
const [isGalleryZoom, setisGalleryZoom] = useState(false);
const [isOpen, setisOpen] = useState(false);
const [isOpen1, setisOpen1] = useState(false);
const [modal, setmodal] = useState(false);
```

- **photoIndex**: Tracks the currently displayed image index in the gallery.
- **isFits, isEffects, isGallery, isGalleryZoom**: Booleans to toggle different Lightbox modes.
- **isOpen, isOpen1**: Booleans to toggle video modals.
- **modal**: Boolean to toggle the form modal.

### Lightbox and Modal Components

- **Lightbox**: Displayed when one of the state variables (`isFits`, `isEffects`, `isGallery`, `isGalleryZoom`) is true. Each Lightbox block provides specific functionalities like zoom, navigation, etc.

- **ModalVideo**: Triggered by buttons to display YouTube or Vimeo videos.

- **Modal**: Used for displaying a form with inputs for name, email, password, and a textarea for the subject.

---

## Usage

To use the `UiLightbox` component, simply import it into your desired React file and include it within your JSX:

```jsx
import UiLightbox from './path-to/UiLightbox';

function App() {
  return (
    <div>
      <UiLightbox />
    </div>
  );
}
```

---

## Props

The `UiLightbox` component does not take any specific props as it relies on internal state management and predefined image assets. The image set can be customized by modifying the `images` array.

---

## Conclusion

The `UiLightbox.js` component is a versatile React component that provides a comprehensive Lightbox experience for images and videos. It utilizes popular libraries to offer features like image galleries, zoom functionalities, and video playback in a sleek, user-friendly interface. This component can be easily integrated into any React application requiring media display in modal overlays.

Feel free to customize the component further to fit your application's design and functionality needs! 😊

# UiGrid.js Documentation

## Overview
The `UiGrid.js` component is a React component that demonstrates the use of the Bootstrap grid system. It provides a detailed table explaining how different grid options behave across various device sizes, enabling developers to design responsive layouts effectively.

## Table of Contents
- [Import Section](#import-section)
- [Component Structure](#component-structure)
- [Grid Options Explained](#grid-options-explained)
- [Usage](#usage)

## Import Section
```javascript
import React from "react"
import Breadcrumbs from "../../components/Common/Breadcrumb"
```
- **React**: The primary library for building user interfaces.
- **Breadcrumbs**: A component used for navigation, showing the path of the current page within the UI Elements section.

## Component Structure
The `UiGrid` component is a functional component structured as follows:
- **Page Content**: Encloses the whole content of the grid page.
- **Breadcrumbs**: Displays the navigation path.
- **Grid Options Table**: Provides a detailed table showcasing the grid system features.

### JSX Structure
```jsx
<React.Fragment>
    <div className="page-content">
        <Breadcrumbs title="UI Elements" breadcrumbItem="Grid" />
        <div className="row">
            <div className="col-12">
                <div className="card">
                    <div className="card-body">
                        <h4 className="card-title">Grid options</h4>
                        <p className="card-title-desc">
                            See how aspects of the Bootstrap grid system work across multiple devices with a handy table.
                        </p>
                        <div className="table-responsive">
                            <table className="table table-bordered table-striped table-nowrap mb-0">
                                <thead>
                                    ...
                                </thead>
                                <tbody>
                                    ...
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</React.Fragment>
```

## Grid Options Explained

### **Table Headers**
The table headers define the responsive breakpoints for various device sizes:
- **Extra small**: `<576px`
- **Small**: `≥576px`
- **Medium**: `≥768px`
- **Large**: `≥992px`
- **Extra large**: `≥1200px`
- **Extra extra large**: `≥1400px`

### **Key Features**
1. **Grid Behavior**: Horizontal at all times for extra small devices, collapsible for larger.
2. **Max Container Width**: Specifies maximum width for containers at different breakpoints.
3. **Class Prefix**: Bootstrap classes used to specify column sizes.
4. **Number of Columns**: Fixed to 12 columns across all devices.
5. **Gutter Width**: Space between columns, standardized at 24px.
6. **Nestable**: Supports nested columns.
7. **Offsets**: Allows creating space around columns.
8. **Column Ordering**: Provides flexibility in ordering columns.

## Usage
This component is typically used as part of a UI elements library to educate developers on implementing responsive grid layouts using Bootstrap. It can be included in a larger UI framework as a reference or demo page.

### Example
To incorporate this component, ensure that Bootstrap styles are included in your project for the grid system to function correctly. Use the `UiGrid` component within a route or as a part of a larger layout.

```jsx
import UiGrid from './UiGrid';

// Usage in a component or route
<UiGrid />
```

This documentation provides an overview and detailed insight into the `UiGrid.js` component, making it easier for developers to understand and implement grid systems in their projects.

# Documentation for `UiGeneral.js` 🎨

The `UiGeneral.js` file is a React component that provides a user interface showcasing various general UI elements such as Badges, Popovers, Tooltips, Paginations, and Spinners. This component leverages Reactstrap, a popular library for Bootstrap components in React, to create visually appealing and interactive elements.

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Components Overview](#components-overview)
   - [Badges](#badges)
   - [Popovers](#popovers)
   - [Tooltips](#tooltips)
   - [Pagination](#pagination)
   - [Spinners](#spinners)
3. [Code Breakdown](#code-breakdown)
4. [Conclusion](#conclusion)

---

## Introduction

The `UiGeneral.js` component is designed to demonstrate the capabilities of several UI elements that can be used in web development. This component serves as a useful reference for developers looking to implement similar UI components in their projects.

## Components Overview

### Badges 🏷️

Badges are used to display small counts or labels. This component includes:

- **Default Badges**: Display badges of different colors.
- **Pill Badges**: Rounded badges created using the `.rounded-pill` class.

#### Example:

```jsx
<Badge className="bg-primary">Primary</Badge>
<Badge pill className="badge-soft-success">Success</Badge>
```

### Popovers 📌

Popovers are small overlay elements that display additional information when triggered. The component demonstrates popovers in four directions: top, right, bottom, and left. Additionally, a dismissible popover is included.

#### Example:

```jsx
<Button id="Popovertop" color="secondary">Popover on top</Button>
<Popover placement="top" isOpen={popovertop} target="Popovertop">
  <PopoverBody>Content goes here.</PopoverBody>
</Popover>
```

### Tooltips 💡

Tooltips provide contextual information about elements when hovered over. The component includes tooltips aligned in four directions.

#### Example:

```jsx
<button type="button" id="TooltipTop">Tooltip on top</button>
<Tooltip placement="top" isOpen={ttop} target="TooltipTop">Hello world!</Tooltip>
```

### Pagination 📄

Pagination components allow navigation through paginated content. The component demonstrates:

- **Default Pagination**
- **Disabled and Active States**
- **Sizing**
- **Alignment**

#### Example:

```jsx
<Pagination>
  <PaginationItem disabled><PaginationLink>Previous</PaginationLink></PaginationItem>
  <PaginationItem><PaginationLink href="#">1</PaginationLink></PaginationItem>
  <PaginationItem active><PaginationLink>2</PaginationLink></PaginationItem>
  <PaginationItem><PaginationLink href="#">Next</PaginationLink></PaginationItem>
</Pagination>
```

### Spinners 🔄

Spinners are used to indicate loading states. The component showcases:

- **Border Spinners**
- **Growing Spinners**

#### Example:

```jsx
<Spinner color="primary" />
<Spinner type="grow" color="secondary" />
```

## Code Breakdown

The component makes use of the following React hooks and Reactstrap components:

- **`useState` Hook**: Manages state for popovers and tooltips.
- **`Button`, `Popover`, `Tooltip`, `Badge`, `Pagination`, `Spinner`**: Components from Reactstrap to create interactive elements.

### State Management

The state for popovers and tooltips is managed using the `useState` hook. Each popover and tooltip has its own state to control visibility:

```jsx
const [popovertop, setpopovertop] = useState(false);
const [ttop, setttop] = useState(false);
```

### UI Elements

Each UI element is created using Reactstrap components and is styled using Bootstrap classes. The component layout is structured using `Rows` and `Cols` for responsive design.

## Conclusion

The `UiGeneral.js` component offers a comprehensive demonstration of various UI elements that can be integrated into web applications. By leveraging Reactstrap, developers can create consistent and visually appealing interfaces with ease. This component serves as a valuable resource for understanding the implementation and styling of badges, popovers, tooltips, pagination, and spinners in a React environment. 

--- 

Feel free to explore and customize the component to suit your project's needs! 💡

# Documentation for `slide.js` 📄

This documentation provides a comprehensive overview of the `slide.js` file, which is part of the broader UI component library. This particular file is responsible for implementing a simple image carousel using React and `reactstrap`. Below, you'll find details on the purpose, functionality, and usage of this component.

## Table of Contents 📚
- [Overview](#overview)
- [Component Structure](#component-structure)
- [State Management](#state-management)
- [Carousel Functionality](#carousel-functionality)
- [Usage](#usage)
- [Code Walkthrough](#code-walkthrough)
- [Dependencies](#dependencies)

## Overview 🚀

The `slide.js` file implements a basic image carousel component using React's class-based approach. It leverages the `reactstrap` library to create a carousel interface, which allows users to navigate through images with smooth transitions.

## Component Structure 🏗️

The main component in the file is `Slide`, which:

- Imports necessary modules and images.
- Initializes the carousel items (images with captions).
- Manages the current active image index.
- Provides methods to navigate between images.

## State Management 🧠

This component uses React's state to manage which image is currently being displayed in the carousel. The state variable `activeIndex` tracks the index of the image currently shown.

```javascript
this.state = { activeIndex: 0 };
```

## Carousel Functionality 🎡

The component provides functionalities to:

- **Next and Previous Controls**: Navigate through the images.
- **Indicators**: Show which image is currently active.
- **Smooth Transitions**: Handle transitions using `onExiting` and `onExited` events to ensure smooth animations.

### Key Methods

- **`next()`**: Advances to the next image.
- **`previous()`**: Goes back to the previous image.
- **`goToIndex(newIndex)`**: Jumps directly to a specified image index.
- **`onExiting()` and `onExited()`**: Manage the animation state to prevent navigation during transitions.

## Usage 🔧

To use this component in a React application, ensure you have `reactstrap` installed and import the `Slide` component wherever needed. You can then include it in your JSX as `<Slide />`.

## Code Walkthrough 🔍

Below is a walkthrough of the main sections of the `slide.js` file:

```javascript
import React, { Component } from "react";
import { Carousel, CarouselItem } from "reactstrap"; // Importing necessary components
import img1 from "../../../assets/images/small/img-1.jpg"; // Importing images
import img2 from "../../../assets/images/small/img-2.jpg";
import img3 from "../../../assets/images/small/img-3.jpg";

const items = [ // Defining the carousel items
  { src: img1, altText: "Slide 1", caption: "Slide 1" },
  { src: img2, altText: "Slide 2", caption: "Slide 2" },
  { src: img3, altText: "Slide 3", caption: "Slide 3" },
];

class Slide extends Component {
  constructor(props) {
    super(props);
    this.state = { activeIndex: 0 }; // Initializing state
    this.next = this.next.bind(this);
    this.previous = this.previous.bind(this);
    this.goToIndex = this.goToIndex.bind(this);
    this.onExiting = this.onExiting.bind(this);
    this.onExited = this.onExited.bind(this);
  }

  onExiting() { this.animating = true; } // Prevent actions during animation
  onExited() { this.animating = false; } // Reset animation state

  next() { // Navigate to the next item
    if (this.animating) return;
    const nextIndex = this.state.activeIndex === items.length - 1 ? 0 : this.state.activeIndex + 1;
    this.setState({ activeIndex: nextIndex });
  }

  previous() { // Navigate to the previous item
    if (this.animating) return;
    const nextIndex = this.state.activeIndex === 0 ? items.length - 1 : this.state.activeIndex - 1;
    this.setState({ activeIndex: nextIndex });
  }

  goToIndex(newIndex) { // Jump to a specific index
    if (this.animating) return;
    this.setState({ activeIndex: newIndex });
  }

  render() {
    const { activeIndex } = this.state;
    const slides = items.map((item) => { // Map through items to create slides
      return (
        <CarouselItem
          onExiting={this.onExiting}
          onExited={this.onExited}
          key={item.src}
        >
          <img src={item.src} className="d-block img-fluid" alt={item.altText} />
        </CarouselItem>
      );
    });

    return (
      <React.Fragment>
        <Carousel activeIndex={activeIndex} next={this.next} previous={this.previous}>
          {slides}
        </Carousel>
      </React.Fragment>
    );
  }
}

export default Slide;
```

## Dependencies 📦

- **React**: A JavaScript library for building user interfaces.
- **reactstrap**: A library that provides Bootstrap 4 components for React.

This component is part of a larger UI library and can be used in combination with other components to build rich user interfaces. Ensure that all dependencies are properly installed and configured in your project for optimal functionality.

# SlideDark.js Documentation

This documentation provides a comprehensive overview of the `SlideDark.js` component, which is a part of a carousel component suite leveraging React and Reactstrap for a dark-themed carousel presentation.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Component Features](#component-features)
3. [Code Breakdown](#code-breakdown)
   - [Imports](#imports)
   - [Carousel Items](#carousel-items)
   - [Component Structure and State](#component-structure-and-state)
   - [Methods](#methods)
   - [Render Method](#render-method)
4. [Usage](#usage)
5. [Conclusion](#conclusion)

---

## Introduction

The `SlideDark.js` file defines a React component named `SlideDark` that encapsulates the functionality for a carousel with a dark theme. This component makes use of `reactstrap` to provide a carousel interface with features like sliding effects, indicators, and controls.

## Component Features

- **Responsive Carousel**: Displays a series of images with captions.
- **Dark Theme**: Utilizes a dark background and light text for captions.
- **Controls**: Previous and next navigation controls.
- **Indicators**: Clickable indicators to navigate to specific slides.
- **Animations**: Slide transitions with exiting and exited event handlers.

## Code Breakdown

### Imports

```javascript
import React, { Component } from "react";
import { Carousel, CarouselItem, CarouselControl, CarouselIndicators } from "reactstrap";
import img3 from "../../../assets/images/small/img-3.jpg";
import img4 from "../../../assets/images/small/img-4.jpg";
import img5 from "../../../assets/images/small/img-5.jpg";
```

- **React and Component**: Core React imports for defining a class-based component.
- **Reactstrap Components**: `Carousel`, `CarouselItem`, `CarouselControl`, and `CarouselIndicators` are imported to construct the carousel.
- **Images**: Three images are imported for display in the carousel.

### Carousel Items

```javascript
const items = [
  {
    src: img3,
    altText: "Slide 1",
    caption: "Slide 1",
    title: "First slide label",
    dascription: "Nulla vitae elit libero, a pharetra augue mollis interdum.",
  },
  {
    src: img4,
    altText: "Slide 2",
    caption: "Slide 2",
    title: "Second slide label",
    dascription: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  },
  {
    src: img5,
    altText: "Slide 3",
    caption: "Slide 3",
    title: "Third slide label",
    dascription: "Praesent commodo cursus magna, vel scelerisque nisl consectetur.",
  },
];
```

- **Items Array**: Contains objects representing each slide in the carousel. Each object holds the image source, alt text, caption, title, and description.

### Component Structure and State

```javascript
class SlideDark extends Component {
  constructor(props) {
    super(props);
    this.state = {
      activeIndex: 0,
    };
    this.next = this.next.bind(this);
    this.previous = this.previous.bind(this);
    this.goToIndex = this.goToIndex.bind(this);
    this.onExiting = this.onExiting.bind(this);
    this.onExited = this.onExited.bind(this);
  }
```

- **State**: Manages the `activeIndex`, which tracks the currently visible slide.
- **Bindings**: Methods are bound to the component instance to ensure proper context.

### Methods

- **onExiting & onExited**: Manage the animation state to prevent overlapping transitions.
  
  ```javascript
  onExiting() {
    this.animating = true;
  }

  onExited() {
    this.animating = false;
  }
  ```

- **next & previous**: Navigate to the next or previous slide, respectively.
  
  ```javascript
  next() {
    if (this.animating) return;
    const nextIndex = this.state.activeIndex === items.length - 1 ? 0 : this.state.activeIndex + 1;
    this.setState({ activeIndex: nextIndex });
  }

  previous() {
    if (this.animating) return;
    const nextIndex = this.state.activeIndex === 0 ? items.length - 1 : this.state.activeIndex - 1;
    this.setState({ activeIndex: nextIndex });
  }
  ```

- **goToIndex**: Directly navigate to a specified slide index.
  
  ```javascript
  goToIndex(newIndex) {
    if (this.animating) return;
    this.setState({ activeIndex: newIndex });
  }
  ```

### Render Method

```javascript
render() {
  const { activeIndex } = this.state;
  const slides = items.map((item) => {
    return (
      <CarouselItem
        onExiting={this.onExiting}
        onExited={this.onExited}
        key={item.src}
        interval={1000}
      >
        <img src={item.src} className="d-block w-100" alt={item.altText} />
        <div className="carousel-caption d-none d-md-block">
          <h5>{item.title}</h5>
          <p>{item.dascription}</p>
        </div>
      </CarouselItem>
    );
  });
  return (
    <React.Fragment>
      <div className="carousel-inner carousel-dark">
        <Carousel activeIndex={activeIndex} next={this.next} previous={this.previous}>
          <CarouselIndicators items={items} activeIndex={activeIndex} onClickHandler={this.goToIndex} />
          {slides}
          <CarouselControl direction="prev" directionText="Previous" onClickHandler={this.previous} />
          <CarouselControl direction="next" directionText="Next" onClickHandler={this.next} />
        </Carousel>
      </div>
    </React.Fragment>
  );
}
```

- **Slides Mapping**: Each item in `items` is mapped to a `CarouselItem` component.
- **Carousel Structure**: Contains indicators, slides, and navigation controls wrapped in a `Carousel` component.

## Usage

To incorporate the `SlideDark` component into your application, ensure that React and Reactstrap are installed. Import the component and use it as a JSX tag:

```javascript
import SlideDark from './path/to/slidedark';

// Usage in JSX
<SlideDark />
```

## Conclusion

The `SlideDark.js` component is a reusable React component that provides a dark-themed carousel with sliding images, interactive controls, and captions. It is adaptable for various image carousel needs within a React application.

---

This concludes the documentation for `SlideDark.js`. For further customization, consider modifying the styles or integrating additional functionality as needed.

# Documentation for `UiCards.js`

## Overview

The `UiCards.js` file is a React component that demonstrates different styles and configurations of **Card** components using the `reactstrap` library. This component is part of a UI library for building user interfaces with pre-designed cards. Cards are flexible and extensible content containers that include various options for headers, footers, content, images, and links.

---

## Table of Contents

1. [Import Statements](#import-statements)
2. [Component Structure](#component-structure)
3. [Card Variants](#card-variants)
   - Basic Cards
   - Cards with List Groups
   - Cards with Images
   - Cards with Header and Footer
   - Card Colors
   - Outline Cards
4. [Advanced Layouts](#advanced-layouts)
   - Card Groups
   - Card Decks
   - Card Columns (Masonry Layout)
5. [Code Snippet](#code-snippet)
6. [Contributing](#contributing)
7. [License](#license)

---

## Import Statements

The component imports several modules and components from `react`, `reactstrap`, and `react-router-dom`, including:

- **React**: Core library for building user interfaces.
- **Reactstrap Components**: Components like `Card`, `CardBody`, `CardImg`, etc., that provide Bootstrap-styled components.
- **Images**: Static images used within the cards.
- **Breadcrumbs**: A component for displaying navigation context.
- **Link**: For navigation between different routes.

```javascript
import React from "react";
import { Col, Row, Card, CardBody, CardTitle, CardSubtitle, CardImg, CardText, CardHeader, CardFooter, CardDeck, CardColumns, CardGroup } from "reactstrap";
import img1 from "../../assets/images/small/img-1.jpg";
import { Link } from "react-router-dom";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

---

## Component Structure

The `UiCards` component is structured using a series of `Row` and `Col` components to layout the cards in a grid format. Each card variant is encapsulated within a `Card` component, which may include elements like `CardImg`, `CardBody`, `CardText`, etc., to showcase different styles and content arrangements.

### Main Structure

```javascript
const UiCards = props => {
  return (
    <React.Fragment>
      <div className="page-content">
        <Breadcrumbs title="UI Elements" breadcrumbItem="Cards" />
        {/* Card rows and columns go here */}
      </div>
    </React.Fragment>
  );
};

export default UiCards;
```

---

## Card Variants

### Basic Cards

These cards feature a simple image, title, and text content. They demonstrate the basic structure of a card.

```html
<Card>
  <CardImg top className="img-fluid" src={img1} alt="Card image cap" />
  <CardBody>
    <CardTitle className="h4 mt-0">Card title</CardTitle>
    <CardText>Some quick example text...</CardText>
    <Link to="#" className="btn btn-primary waves-effect waves-light">Button</Link>
  </CardBody>
</Card>
```

### Cards with List Groups

Cards can include list groups to display multiple items.

```html
<Card>
  <CardBody>
    <CardTitle className="h4 mt-0">Card title</CardTitle>
    <CardText>Some quick example text...</CardText>
  </CardBody>
  <ul className="list-group list-group-flush">
    <li className="list-group-item">Cras justo odio</li>
    <li className="list-group-item">Dapibus ac facilisis in</li>
  </ul>
</Card>
```

### Cards with Images

Cards with images can display an image along with text content, either at the top or bottom of the card.

```html
<Card>
  <CardImg className="img-fluid" src={img3} alt="Card image cap" />
  <CardBody>
    <CardText>Some quick example text...</CardText>
  </CardBody>
</Card>
```

### Cards with Header and Footer

Cards can have headers and footers for additional information or context.

```html
<Card>
  <CardHeader className="h4">Featured</CardHeader>
  <CardBody>
    <CardTitle className="h4 mt-0">Special title treatment</CardTitle>
    <CardText>With supporting text...</CardText>
    <Link to="#" className="btn btn-primary">Go somewhere</Link>
  </CardBody>
  <CardFooter className="text-muted">2 days ago</CardFooter>
</Card>
```

### Card Colors

Cards can be styled with different background colors using `reactstrap` color classes.

```html
<Card color="primary" className="text-white">
  <CardBody>
    <h5 className="mt-0 mb-4 text-white">Primary Card</h5>
    <CardText>Some quick example text...</CardText>
  </CardBody>
</Card>
```

### Outline Cards

Outline cards provide a border around the card for a distinct look.

```html
<Card outline color="primary" className="border">
  <CardHeader className="bg-transparent">Primary outline Card</CardHeader>
  <CardBody>
    <CardTitle className="h5 mt-0">card title</CardTitle>
    <CardText>Some quick example text...</CardText>
  </CardBody>
</Card>
```

---

## Advanced Layouts

### Card Groups

Card groups allow multiple cards to be displayed together with equal width and consistent height.

```html
<CardGroup>
  <Card>...</Card>
  <Card>...</Card>
  <Card>...</Card>
</CardGroup>
```

### Card Decks

Card decks align cards in a horizontal layout with equal spacing between them.

```html
<CardDeck>
  <Card>...</Card>
  <Card>...</Card>
  <Card>...</Card>
</CardDeck>
```

### Card Columns (Masonry Layout)

Card columns arrange cards in a masonry-style layout.

```html
<CardColumns>
  <Card>...</Card>
  <Card>...</Card>
  <Card>...</Card>
</CardColumns>
```

---

## Code Snippet

Here's a small snippet to showcase how cards are structured within the component:

```javascript
<Row>
  <Col mg={6} lg={3}>
    <Card>
      <CardImg top className="img-fluid" src={img1} alt="Card image cap" />
      <CardBody>
        <CardTitle className="h4 mt-0">Card title</CardTitle>
        <CardText>Some quick example text...</CardText>
        <Link to="#" className="btn btn-primary waves-effect waves-light">Button</Link>
      </CardBody>
    </Card>
  </Col>
  {/* More card components */}
</Row>
```

---

## Contributing

If you wish to contribute to this component, please fork the repository and submit a pull request. For major changes, please open an issue first to discuss what you would like to change.

---

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

---

This documentation provides an overview of how the `UiCards.js` component is structured and utilized within a React application. Each section highlights different configurations and variants of cards to help developers use and modify them according to their needs.

# UiCarousel.js Documentation

Welcome to the documentation for the **UiCarousel.js** file. This file is a component of a React application that implements various types of carousels using the `reactstrap` library. Carousels are a great way to display multiple pieces of content using a single space, making them ideal for showcasing images, testimonials, or other types of content in a rotating fashion.

## Table of Contents
- [Overview](#overview)
- [Components Breakdown](#components-breakdown)
  - [Slides Only](#slides-only)
  - [With Controls](#with-controls)
  - [With Indicators](#with-indicators)
  - [With Captions](#with-captions)
  - [Crossfade](#crossfade)
- [Dependencies](#dependencies)
- [Usage](#usage)

## Overview

The `UiCarousel` component is a part of the UI elements section of the application. It demonstrates how to use different types of carousels that are common in modern web applications. The component imports various carousel types and renders them within cards to provide distinct examples.

## Components Breakdown

### Slides Only
The **Slides Only** component is a simple carousel that consists only of slides. It does not include any controls or indicators, making it ideal for cases where users simply need to view content without interacting.

```jsx
<Slide />
```

- **Note**: Utilizes `.d-block` and `.img-fluid` classes for responsive image display.

### With Controls
The **With Controls** component adds navigation controls to the basic slides. These controls allow users to manually navigate through the carousel items.

```jsx
<Slidewithcontrol />
```

- **Benefits**: Gives users more control over the carousel navigation.

### With Indicators
The **With Indicators** component includes navigational indicators, commonly dots, at the bottom of the carousel. These indicators show which slide is currently active and allow users to click on them to jump to a particular slide.

```jsx
<Slidewithindicator />
```

- **Benefits**: Provides a visual cue of the number of slides and the current position.

### With Captions
The **With Captions** carousel introduces captions to each slide. Captions can contain text or other HTML content, providing context or additional information about the slide content.

```jsx
<Slidewithcaption />
```

- **Usage**: Use `.carousel-caption` within `.carousel-item` for captions.

### Crossfade
The **Crossfade** carousel changes the transition effect from a slide to a fade, offering a different visual experience that might be more suitable for certain types of content.

```jsx
<Slidewithfade />
```

- **Usage**: Apply `.carousel-fade` for fade transitions.

## Dependencies

The component relies on the following:
- **React**: For creating component-based architecture.
- **Reactstrap**: For Bootstrap-styled components.
- **Breadcrumbs**: Component for displaying breadcrumb navigation.

## Usage

Here’s how you can use the `UiCarousel` component in your React application:

1. **Ensure Dependencies**: Make sure `reactstrap` and `react` are installed in your project.

2. **Import and Use Component**:
   ```jsx
   import React from 'react';
   import UiCarousel from './path/to/UiCarousel';

   const App = () => (
     <div>
       <UiCarousel />
     </div>
   );

   export default App;
   ```

3. **Customization**: You can customize the carousel by editing the imported carousel components like `Slide`, `Slidewithcontrol`, etc.

This component provides a robust solution for implementing carousels in a React application, leveraging the power of Reactstrap for easy integration and customization. For more advanced features, consider exploring additional React carousel libraries or customizing the existing components further.

# UiButtons.js Documentation

Welcome to the documentation for the **UiButtons.js** file! This component provides a comprehensive guide on using various button styles and types offered by **Bootstrap** within a React application. Let’s explore the different button types and usages available in this file. 🚀

## 📑 Index

1. [Overview](#overview)
2. [Default Buttons](#default-buttons)
3. [Outline Buttons](#outline-buttons)
4. [Rounded Buttons](#rounded-buttons)
5. [Buttons with Icons](#buttons-with-icons)
6. [Button Sizes](#button-sizes)
7. [Button Widths](#button-widths)
8. [Button Tags](#button-tags)
9. [Toggle States](#toggle-states)
10. [Block Buttons](#block-buttons)
11. [Checkbox & Radio Buttons](#checkbox-radio-buttons)
12. [Button Groups](#button-groups)
13. [Button Toolbar](#button-toolbar)
14. [Sizing](#sizing)
15. [Vertical Variation](#vertical-variation)

---

## 📝 Overview

The **UiButtons.js** is a React functional component that utilizes **ReactStrap** to render various styles of buttons. These buttons can be used to enhance the user interface with different colors, sizes, icons, and functionalities. The component includes options for default styles, outlines, rounded shapes, and more. 🎨

### Dependencies:
- **React**
- **ReactStrap**
- **React Router**

### Import Statements:
```javascript
import React, { useState } from "react";
import { Link } from "react-router-dom";
import { Col, Row, Card, CardBody, CardTitle, Button, DropdownToggle, DropdownMenu, DropdownItem, ButtonDropdown } from "reactstrap";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

---

## 🖌️ Default Buttons

Default button styles provided by Bootstrap, each conveying a unique semantic purpose.

- **Primary**
- **Secondary**
- **Success**
- **Info**
- **Warning**
- **Danger**
- **Dark**
- **Link**
- **Light**

```jsx
<Button color="primary">Primary</Button>
<Button color="secondary">Secondary</Button>
// ... other buttons
```

---

## ✨ Outline Buttons

Outline buttons remove background colors and images, using a border to define the button.

```jsx
<Button color="primary" outline>Primary</Button>
<Button color="secondary" outline>Secondary</Button>
// ... other outline buttons
```

---

## 🔵 Rounded Buttons

Buttons with rounded borders for a softer look.

```jsx
<Button color="primary" className="btn-rounded">Primary</Button>
<Button color="secondary" className="btn-rounded">Secondary</Button>
// ... other rounded buttons
```

---

## 🎨 Buttons with Icons

Buttons enhanced with icons to represent actions visually.

```jsx
<button type="button" className="btn btn-primary">
    <i className="bx bx-smile"></i> Primary
</button>
// ... other buttons with icons
```

---

## 📏 Button Sizes

Available in large and small sizes by using `.btn-lg` and `.btn-sm`. 

```jsx
<Button color="primary" className="btn-lg">Large button</Button>
<Button color="secondary" className="btn-sm">Small button</Button>
```

---

## ↔️ Button Widths

Customizable button widths with classes like `.w-xs`, `.w-sm`, `.w-md`, and `.w-lg`.

```jsx
<button className="btn btn-primary width-xs">Xs</button>
<button className="btn btn-danger width-sm">Small</button>
```

---

## 🏷️ Button Tags

Buttons can be rendered using different HTML elements like `<Link>`, `<button>`, and `<input>`.

```jsx
<Link className="btn btn-primary" to="#" role="button">Link</Link>
<input className="btn btn-info" type="button" value="Input" />
```

---

## 🔄 Toggle States

Buttons can toggle their active state using `data-toggle="button"`.

```jsx
<Button color="primary" data-toggle="button">Single toggle</Button>
```

---

## 🧱 Block Buttons

Buttons that span the full width of their parent container using `.btn-block`.

```jsx
<Button color="primary" className="btn-block">Block level button</Button>
```

---

## ✔️ Checkbox & Radio Buttons

Styled as buttons rather than traditional checkboxes and radio buttons.

```jsx
<label className="btn btn-primary">
    <input type="checkbox" /> Checked-1
</label>
// ... other checkbox buttons
```

---

## 🔗 Button Groups

Group multiple buttons together for related actions.

```jsx
<div className="btn-group">
    <Button color="primary">Left</Button>
    <Button color="primary">Middle</Button>
    <Button color="primary">Right</Button>
</div>
```

---

## 🛠️ Button Toolbar

Combine multiple button groups into a toolbar for complex components.

```jsx
<div className="btn-toolbar">
    <div className="btn-group me-2">
        <Button color="secondary">1</Button>
        <Button color="secondary">2</Button>
    </div>
</div>
```

---

## 📏 Sizing

Apply size classes to button groups to ensure uniformity across a group.

```jsx
<div className="btn-group btn-group-lg">
    <Button color="primary">Left</Button>
    <Button color="primary">Middle</Button>
</div>
```

---

## 📍 Vertical Variation

Display buttons in a vertical stack rather than horizontally.

```jsx
<div className="btn-group-vertical">
    <Button color="secondary">Button</Button>
    <ButtonDropdown isOpen={drp_link} toggle={() => setdrp_link(!drp_link)}>
        <DropdownToggle caret>Dropdown</DropdownToggle>
        <DropdownMenu>
            <DropdownItem>Dropdown link</DropdownItem>
        </DropdownMenu>
    </ButtonDropdown>
</div>
```

---

This documentation provides a comprehensive view of the various button options available within the **UiButtons** component. Utilize these styles to enhance and customize your application's interface effectively! 🎉

# Documentation for `UiAlert.js` 📄

This document provides a detailed description of the `UiAlert.js` file, which is a React component used to create various types of alerts in a user interface. This component leverages the `reactstrap` library for styling and structure.

## Table of Contents

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Component Structure](#component-structure)
4. [Features](#features)
5. [Usage](#usage)
6. [Conclusion](#conclusion)

---

## Introduction

The `UiAlert` component is designed to provide alert messages with different styles and functionalities. It supports basic alerts, alerts with links, dismissible alerts, and alerts with icons, which can be used to enhance user notifications in a web application.

## Imports

The component utilizes the following imports:

| Module              | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| React               | Core library for building React components.                                 |
| reactstrap          | Provides Bootstrap components for React, such as `Alert`, `Col`, `Row`, etc.|
| react-router-dom    | Used for navigation links within the application (`Link`).                  |
| Breadcrumb          | Custom component for navigation breadcrumbs.                                |

```javascript
import React from "react";
import { Alert, Col, Row, Card, CardBody, CardTitle, UncontrolledAlert } from "reactstrap";
import { Link } from "react-router-dom";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

## Component Structure

The `UiAlert` component is structured using a combination of `Card`, `Row`, and `Col` components from `reactstrap` to organize and display the alerts. It uses `Breadcrumbs` for navigation and provides different categories of alerts.

```jsx
const UiAlert = () => {
    return (
        <React.Fragment>
            <div className="page-content">
                <Breadcrumbs title="UI Elements" breadcrumbItem="Alerts" />
                <Row>
                    {/* Default Alerts */}
                    <Col lg={6}>
                        <Card>
                            <CardBody>
                                <CardTitle className="h4">Default Alerts</CardTitle>
                                {/* Alerts without links */}
                                <div className="">
                                    <Alert color="primary"> A simple primary alert—check it out! </Alert>
                                    {/* Other alerts */}
                                </div>
                            </CardBody>
                        </Card>
                    </Col>
                    {/* Link color Alerts */}
                    <Col lg={6}>
                        <Card>
                            <CardBody>
                                <CardTitle className="h4">Link color</CardTitle>
                                {/* Alerts with links */}
                            </CardBody>
                        </Card>
                    </Col>
                </Row>
                {/* Dismissing Alerts */}
                <Row>
                    <Col lg={6}>
                        <Card>
                            <CardBody>
                                <CardTitle className="h4">Dismissing</CardTitle>
                                {/* Dismissible alerts */}
                            </CardBody>
                        </Card>
                    </Col>
                    {/* Alerts with Icons */}
                    <Col lg={6}>
                        <Card>
                            <CardBody>
                                <CardTitle className="h4 mb-4">With Icon</CardTitle>
                                {/* Alerts with icons */}
                            </CardBody>
                        </Card>
                    </Col>
                </Row>
            </div>
        </React.Fragment>
    );
}

export default UiAlert;
```

## Features

### 1. **Default Alerts**

Displays basic alerts with different color schemes. These alerts are non-dismissible and meant for simple notifications.

### 2. **Link Color Alerts**

Alerts that include a link styled according to the alert's color. This provides a consistent look and feel for links within alerts.

### 3. **Dismissing Alerts**

Alerts that can be dismissed by the user. These use the `UncontrolledAlert` component, which includes a close button.

### 4. **Alerts with Icons**

Alerts featuring icons for better visual indication of the alert type (e.g., info, warning, success).

## Usage

To utilize the `UiAlert` component, ensure that `reactstrap` and `react-router-dom` are correctly installed in your project. You can include this component in your application as follows:

```jsx
import UiAlert from "./path/to/UiAlert";

function App() {
    return (
        <div className="App">
            <UiAlert />
        </div>
    );
}

export default App;
```

## Conclusion

The `UiAlert` component is a versatile and highly customizable component designed to enhance user interaction through informative alerts. By leveraging `reactstrap`, it ensures that the alerts are responsive and consistent with the overall design of the application.

This component can be further customized or extended to add more functionalities, such as integrating additional alert types or using different animation effects.

# UiImageCropper.js Documentation 📷

## Overview
The `UiImageCropper.js` file is a React component that provides a user interface for cropping images. It leverages the `Cropper` library to allow users to easily manipulate images by adjusting crop ratios, zoom, rotation, and more. This component is part of a UI elements suite, offering various functionalities to enhance user interaction with images.

## Table of Contents
1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [State Management](#state-management)
4. [Key Methods](#key-methods)
5. [Component Rendering](#component-rendering)
6. [User Interactions](#user-interactions)
7. [Modals](#modals)
8. [Conclusion](#conclusion)

## Introduction
The `UiImageCropper` component is designed to give users the ability to crop images using different aspect ratios, adjust image zoom, drag mode, and other transformations. It is implemented as a class-based React component and utilizes various Reactstrap components for UI layout and interaction.

## Dependencies 📦
- **React** - Framework for building the component.
- **reactstrap** - For UI components like Cards, Modals, Buttons, etc.
- **Cropper** - For the image cropping functionality.
- **cropperjs** - CSS styling for the Cropper tool.
- **react-router-dom** - For routing and linking within the app.

## State Management
The component manages several state properties to control the cropping tool and modals:

| State Property | Description |
|----------------|-------------|
| `src`          | The source of the image to be cropped. |
| `cropResult`   | Stores the result of the cropped image. |
| `ratio1`, `ratio2` | Control the aspect ratio for cropping. |
| `zoom`         | Controls the zoom level of the image. |
| `dragMode`     | Determines the drag mode (`move` or `crop`). |
| `moveX`, `moveY` | Control the position of the image. |
| `rotate`       | Stores the rotation angle of the image. |
| `scaleX`, `scaleY` | Control the flip transformations. |
| `enable`, `disable` | Toggle the cropper tool's enabled state. |
| `modal_1`      | Controls the visibility of the crop result modal. |
| `imgWidth`, `imgHeight` | Dimensions of the cropped image. |
| `viewMode`     | Determines the view mode of the cropper. |

## Key Methods 🛠️
- `tog_1()`: Toggles the visibility of the crop result modal.
- `onChange(e)`: Handles file input changes to update the image source with a new image.
- `cropImage(width, height)`: Executes the cropping process and updates the `cropResult` state with the cropped image.
- `useDefaultImage()`: Resets the image source to the default image.
- `changeRatio(e, r1, r2)`: Changes the aspect ratio of the cropper based on user selection.

## Component Rendering
The component renders a comprehensive UI for image cropping:

- **Breadcrumbs**: For navigation context.
- **Cropper**: Main image cropping tool with options for zoom, aspect ratio, and more.
- **Image Previews**: Display different sizes of the cropped image.
- **Button Groups**: For various operations like zooming, moving, rotating, etc.

## User Interactions 🎨
Users can interact with the cropper through various controls:

- **Aspect Ratio Selection**: Choose from predefined aspect ratios or a freeform option.
- **Drag Mode**: Switch between moving the image or cropping it.
- **Zoom In/Out**: Adjust the zoom level of the image.
- **Move Image**: Change the position of the image within the cropper.
- **Rotate Image**: Rotate the image by 45° increments.
- **Flip**: Flip the image horizontally or vertically.
- **Enable/Disable**: Enable or disable the cropper tool.

## Modals
The component includes a modal to display the cropped image result. Users can view the cropped image and download it if needed.

- **Modal Controls**:
  - **Open/Close**: Toggle the visibility of the modal.
  - **Download Link**: Provides a link to download the cropped image.

## Conclusion
The `UiImageCropper` component is a versatile and interactive tool for image cropping, offering a rich set of features to customize and transform images. Its integration with `Cropper` empowers users with advanced image manipulation capabilities, making it an essential part of any UI suite that requires image handling.

# UiImageCropper.js Documentation 📷

## Overview
The `UiImageCropper.js` file is a React component that provides a user interface for cropping images. It leverages the `Cropper` library to allow users to easily manipulate images by adjusting crop ratios, zoom, rotation, and more. This component is part of a UI elements suite, offering various functionalities to enhance user interaction with images.

## Table of Contents
1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [State Management](#state-management)
4. [Key Methods](#key-methods)
5. [Component Rendering](#component-rendering)
6. [User Interactions](#user-interactions)
7. [Modals](#modals)
8. [Conclusion](#conclusion)

## Introduction
The `UiImageCropper` component is designed to give users the ability to crop images using different aspect ratios, adjust image zoom, drag mode, and other transformations. It is implemented as a class-based React component and utilizes various Reactstrap components for UI layout and interaction.

## Dependencies 📦
- **React** - Framework for building the component.
- **reactstrap** - For UI components like Cards, Modals, Buttons, etc.
- **Cropper** - For the image cropping functionality.
- **cropperjs** - CSS styling for the Cropper tool.
- **react-router-dom** - For routing and linking within the app.

## State Management
The component manages several state properties to control the cropping tool and modals:

| State Property | Description |
|----------------|-------------|
| `src`          | The source of the image to be cropped. |
| `cropResult`   | Stores the result of the cropped image. |
| `ratio1`, `ratio2` | Control the aspect ratio for cropping. |
| `zoom`         | Controls the zoom level of the image. |
| `dragMode`     | Determines the drag mode (`move` or `crop`). |
| `moveX`, `moveY` | Control the position of the image. |
| `rotate`       | Stores the rotation angle of the image. |
| `scaleX`, `scaleY` | Control the flip transformations. |
| `enable`, `disable` | Toggle the cropper tool's enabled state. |
| `modal_1`      | Controls the visibility of the crop result modal. |
| `imgWidth`, `imgHeight` | Dimensions of the cropped image. |
| `viewMode`     | Determines the view mode of the cropper. |

## Key Methods 🛠️
- `tog_1()`: Toggles the visibility of the crop result modal.
- `onChange(e)`: Handles file input changes to update the image source with a new image.
- `cropImage(width, height)`: Executes the cropping process and updates the `cropResult` state with the cropped image.
- `useDefaultImage()`: Resets the image source to the default image.
- `changeRatio(e, r1, r2)`: Changes the aspect ratio of the cropper based on user selection.

## Component Rendering
The component renders a comprehensive UI for image cropping:

- **Breadcrumbs**: For navigation context.
- **Cropper**: Main image cropping tool with options for zoom, aspect ratio, and more.
- **Image Previews**: Display different sizes of the cropped image.
- **Button Groups**: For various operations like zooming, moving, rotating, etc.

## User Interactions 🎨
Users can interact with the cropper through various controls:

- **Aspect Ratio Selection**: Choose from predefined aspect ratios or a freeform option.
- **Drag Mode**: Switch between moving the image or cropping it.
- **Zoom In/Out**: Adjust the zoom level of the image.
- **Move Image**: Change the position of the image within the cropper.
- **Rotate Image**: Rotate the image by 45° increments.
- **Flip**: Flip the image horizontally or vertically.
- **Enable/Disable**: Enable or disable the cropper tool.

## Modals
The component includes a modal to display the cropped image result. Users can view the cropped image and download it if needed.

- **Modal Controls**:
  - **Open/Close**: Toggle the visibility of the modal.
  - **Download Link**: Provides a link to download the cropped image.

## Conclusion
The `UiImageCropper` component is a versatile and interactive tool for image cropping, offering a rich set of features to customize and transform images. Its integration with `Cropper` empowers users with advanced image manipulation capabilities, making it an essential part of any UI suite that requires image handling.

# UI Notifications Documentation 📢

Welcome to the documentation for the **UI Notifications** component! This component is an integral part of creating dynamic and interactive notifications within a web application. Below you'll find a detailed explanation of the code, its functionality, and how you can customize it for your own use.

## Table of Contents 📚
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Component Structure](#component-structure)
4. [State Management](#state-management)
5. [Functions](#functions)
    - [showToast](#showtoast-function)
    - [clearToast](#cleartoast-function)
6. [Customization Options](#customization-options)
7. [UI Layout](#ui-layout)
8. [Usage](#usage)
9. [Dependencies](#dependencies)

---

## Introduction

The **UI Notifications** component is a React component that uses the `toastr` library to create and manage notification pop-ups. These notifications can be styled and positioned in various ways, making it a versatile tool for improving user interaction.

## Installation

Before using the UI Notifications component, ensure that you have the necessary dependencies installed:

```bash
npm install reactstrap toastr
```

Additionally, include the Toastr CSS in your project:

```javascript
import 'toastr/build/toastr.min.css';
```

## Component Structure

The component is structured using React's functional component approach. It employs hooks for state management and uses `reactstrap` components for layout and styling.

```javascript
import React, { useState } from 'react';
import { Button, Card, CardBody, Col, Label, Row } from 'reactstrap';
import toastr from 'toastr';
import 'toastr/build/toastr.min.css';
import Breadcrumbs from '../../components/Common/Breadcrumb';
```

## State Management

State management is achieved using React's `useState` hook. The component maintains several state variables to control the behavior and appearance of the notifications:

- `showEasing`, `hideEasing`: Animation easing types.
- `showMethod`, `hideMethod`: Animation methods for showing and hiding notifications.
- `showDuration`, `hideDuration`: Duration of animations.
- `timeOut`, `extendedTimeOut`: Timing for notification visibility.

## Functions

### `showToast` Function

The `showToast` function is responsible for displaying notifications based on the user-defined settings. It retrieves values from input fields and checkboxes to configure the `toastr` options.

#### Configuration Options:
- **Toast Type**: Success, Info, Warning, Error.
- **Position**: Top Right, Bottom Right, Top Left, etc.
- **Features**: Close Button, Debug Info, Progress Bar, Prevent Duplicates, etc.

```javascript
function showToast() {
  // Retrieve configuration and display notification
}
```

### `clearToast` Function

The `clearToast` function clears all active notifications.

```javascript
function clearToast() {
  toastr.clear();
}
```

## Customization Options

The UI Notifications component allows customization through various input fields and checkboxes. Users can modify:

- **Title and Message**: Customizable text for notifications.
- **Animation and Timing**: Customize the show/hide methods, durations, and easing.
- **Position and Type**: Choose where and how the notification appears.

## UI Layout

The UI is structured using a grid system provided by `reactstrap`. Elements such as input fields, checkboxes, and buttons are organized within rows and columns.

## Usage

To use the component, simply import it within your React application and render it. Customize the notification settings using the interface provided.

```jsx
<UiNotifications />
```

## Dependencies

- **React**: A JavaScript library for building user interfaces.
- **Reactstrap**: A front-end framework for building responsive UI.
- **Toastr**: A JavaScript library for non-blocking notifications.

Thank you for reviewing the UI Notifications documentation! 🎉 Feel free to experiment with the component's features to best suit your application's needs. If you have any questions or need further assistance, don't hesitate to reach out. Happy coding! 🚀