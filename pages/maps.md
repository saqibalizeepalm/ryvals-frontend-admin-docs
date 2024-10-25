# SimpleMap.js Documentation

Welcome to the documentation for the **SimpleMap.js** file! This file leverages the power of the **React** library along with **React-Leaflet** to render a simple interactive map. Below you'll find a detailed breakdown of the code components, their purpose, and how they come together to create a map interface.

## Table of Contents
- [Overview](#overview)
- [Installation](#installation)
- [Components](#components)
  - [Map Initialization](#map-initialization)
  - [Tile Layer](#tile-layer)
  - [Marker](#marker)
- [Customization](#customization)
- [Conclusion](#conclusion)

## Overview

The **SimpleMap.js** file is designed to display a straightforward map with a single marker using the **Leaflet.js** library wrapped in React components via **React-Leaflet**. The map centers on a predefined location and provides mapping via OpenStreetMap tiles.

## Installation

Make sure you have the following installed to use this component:
- React
- React-Leaflet
- Leaflet

To install these dependencies, you can use:

```shell
npm install react react-dom react-leaflet leaflet
```

## Components

### Map Initialization

The main component `SimpleMap` extends from `React.Component`, initializing the map's state with default latitude, longitude, and zoom level. This state is used to center the map.

```javascript
state = {
  lat: 51.505,
  lng: -0.09,
  zoom: 13,
}
```

- **Latitude**: `51.505`
- **Longitude**: `-0.09`
- **Zoom**: `13`

The position is derived from the state and is used to set the center of the map:

```javascript
const position = [this.state.lat, this.state.lng]
```

### Tile Layer

The `TileLayer` component is responsible for loading and displaying tile layers on the map. Here, it uses tiles from OpenStreetMap with appropriate attribution.

```javascript
<TileLayer
  attribution='&amp;copy <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
  url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
/>
```

### Marker

A `Marker` is placed at the position specified by the state. This marker does not have a popup or any additional functionality but serves as a placeholder for further enhancements.

```javascript
<Marker position={position}></Marker>
```

## Customization

To customize the map, you can:
- Change the initial `lat`, `lng`, and `zoom` in the state to different values to center the map on a different location.
- Modify the `TileLayer` URL to use different map tiles.
- Add more markers or interactive elements like `Popup` or `Tooltip` for enhanced user interaction.

## Conclusion

The **SimpleMap.js** file is an excellent starting point for anyone looking to implement basic map functionality in their React application using Leaflet. With a few lines of code, it sets up a fully functional map that can be easily expanded to include more sophisticated features.

Feel free to dive into the code, experiment with different settings, and tailor it to fit your specific needs. Happy mapping! 🌍🗺️

# MapWithPopup.js Documentation 📍

This documentation provides an overview of the `MapWithPopup.js` file, which is a component for rendering a map using the React-Leaflet library with integrated popups. This component is particularly useful for displaying maps with interactive markers that can show additional information when clicked.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [State Management](#state-management)
5. [Rendering the Map](#rendering-the-map)
6. [Customization](#customization)
7. [Code Summary](#code-summary)

---

## Introduction

The `MapWithPopup.js` file is a React component that leverages the Leaflet library to create an interactive map. It includes a single marker with a popup that displays a message when clicked. The component is built using React and React-Leaflet, and it uses default Leaflet icons for markers.

---

## Dependencies

The component relies on the following dependencies:

- **React**: A JavaScript library for building user interfaces.
- **Leaflet**: An open-source JavaScript library for mobile-friendly interactive maps.
- **React-Leaflet**: A library that provides React components for Leaflet maps.
- **Leaflet CSS**: Required styles for displaying the map and markers correctly.

```javascript
import React, { Component } from "react";
import Leaflet from "leaflet";
import { Map, TileLayer, Marker, Popup } from "react-leaflet";
import "leaflet/dist/leaflet.css";
```

---

## Component Structure

The `MapWithPopup` component is a class-based React component. Here's a breakdown of its structure:

- The component imports necessary modules from React, Leaflet, and React-Leaflet.
- It configures default Leaflet icons to ensure markers are displayed correctly.
- A `SimpleMap` class is defined, extending `Component`.

---

## State Management

The component uses React's state to manage the map's center position and zoom level. The state is initialized with the following values:

- **Latitude (`lat`)**: 51.505
- **Longitude (`lng`)**: -0.09
- **Zoom Level (`zoom`)**: 13

```javascript
state = {
  lat: 51.505,
  lng: -0.09,
  zoom: 13,
};
```

---

## Rendering the Map

The `render` method is responsible for displaying the map. It sets up the map with a center position and zoom level from the component's state. The map includes a tile layer for rendering map tiles and a marker with a popup.

```javascript
const position = [this.state.lat, this.state.lng];

return (
  <Map center={position} zoom={this.state.zoom} style={{ height: "300px" }}>
    <TileLayer
      attribution='&amp;copy <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
      url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
    />
    <Marker position={position}>
      <Popup>Hello World!</Popup>
    </Marker>
  </Map>
);
```

- **Map**: The main container for the Leaflet map.
- **TileLayer**: Provides map tiles from OpenStreetMap.
- **Marker**: Displays a marker at the specified position.
- **Popup**: Displays a text message when the marker is clicked.

---

## Customization

Developers can customize the map by adjusting the initial state values for position and zoom. Additionally, the popup message inside the `<Popup>` component can be updated to display any desired content.

---

## Code Summary

The `MapWithPopup.js` component is a straightforward implementation of a Leaflet map with a clickable marker and popup. It serves as a basic example of integrating React with Leaflet to create interactive map applications.

---

### 🎨 Conclusion

The `MapWithPopup.js` file demonstrates the power of combining React with Leaflet to create dynamic and interactive maps. This component can be expanded with additional features such as multiple markers, custom icons, and layers to build comprehensive mapping solutions.

# Documentation for `MapMarkerCustomIcons.js`

## Overview

The `MapMarkerCustomIcons.js` file is a React component built using the `react-leaflet` library. It demonstrates how to create a map with custom marker icons using the Leaflet library. The component displays a map centered at a specific latitude and longitude and includes a marker with a custom icon and a popup.

## Table of Contents

- [Imports](#imports)
- [Custom Icon Configuration](#custom-icon-configuration)
- [Component Structure](#component-structure)
  - [State Initialization](#state-initialization)
  - [Render Method](#render-method)
- [Usage](#usage)

---

## Imports

```javascript
import React, { Component } from "react";
import Leaflet from "leaflet";
import { Map, TileLayer, Marker, Popup } from "react-leaflet";
import L from "leaflet";
import "leaflet/dist/leaflet.css";
```

- **React**: Core library for building user interfaces.
- **Leaflet**: Open-source JavaScript library for interactive maps.
- **react-leaflet**: React components for Leaflet maps.
- **Leaflet CSS**: Required stylesheet for Leaflet.

## Custom Icon Configuration

The custom icon is configured using Leaflet's `L.Icon` class. This configuration specifies the icon's appearance and positioning:

```javascript
export const pointerIcon = new L.Icon({
  iconUrl: "../../../assets/images/logo.svg",
  iconRetinaUrl: "../../../assets/images/logo.svg",
  iconAnchor: [5, 55],
  popupAnchor: [10, -44],
  iconSize: [25, 55],
  shadowUrl: "../../../assets/images/logo.svg",
  shadowSize: [68, 95],
  shadowAnchor: [20, 92],
});
```

### Properties

- **iconUrl**: URL to the icon image.
- **iconRetinaUrl**: URL for the retina version of the icon.
- **iconAnchor**: Point of the icon which will correspond to marker's location.
- **popupAnchor**: Point from which the popup should open relative to the iconAnchor.
- **iconSize**: Size of the icon.
- **shadowUrl**: URL to the shadow image.
- **shadowSize**: Size of the shadow.
- **shadowAnchor**: Point of the shadow which will correspond to iconAnchor.

## Component Structure

### State Initialization

The component maintains a state to store the map's center coordinates and zoom level:

```javascript
state = {
  lat: 51.505,
  lng: -0.09,
  zoom: 13,
};
```

### Render Method

The `render` method constructs the Leaflet map with the custom marker:

```javascript
render() {
  const position = [this.state.lat, this.state.lng];
  return (
    <Map center={position} zoom={this.state.zoom} style={{ height: "300px" }}>
      <TileLayer
        attribution='&amp;copy <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      />
      <Marker position={position} icon={pointerIcon}>
        <Popup>
          A pretty CSS3 popup. <br /> Easily customizable.
        </Popup>
      </Marker>
    </Map>
  );
}
```

### Explanation

- **Map**: The main component that renders the map centered on the specified coordinates and zoom level.
- **TileLayer**: Provides the map tiles from OpenStreetMap.
- **Marker**: Positioned at the map's center, using the custom `pointerIcon`.
- **Popup**: A popup that appears when the marker is clicked, customizable with HTML content.

## Usage

This component can be used in any React application where you want to display a Leaflet map with a custom marker icon. Ensure that the icon paths are correctly set up according to your project's directory structure.

Simply import and use the `MapMarkerCustomIcons` component in your application, and it will render a map with a custom icon marker and a popup.

```javascript
import MapMarkerCustomIcons from './path/to/MapMarkerCustomIcons';

// In your JSX:
<MapMarkerCustomIcons />
```

---

This documentation provides a comprehensive guide to understanding and utilizing the `MapMarkerCustomIcons.js` component, enabling you to create interactive maps with custom markers in your React applications. 🗺️✨

# Documentation for `MapVectorLayers.js` 🌍

## Overview

The `MapVectorLayers.js` file is a React component utilizing the **React-Leaflet** library to render a map with various vector layers. This component demonstrates how to use different geometric shapes such as circles, polygons, polylines, and rectangles on a map. These features can be used for representing data, highlighting regions, or marking specific locations.

## Table of Contents

1. [Dependencies](#dependencies)
2. [Component Description](#component-description)
3. [Vector Layers Explained](#vector-layers-explained)
4. [Code Walkthrough](#code-walkthrough)
5. [Features and Interactivity](#features-and-interactivity)
6. [Usage](#usage)

## Dependencies

The `MapVectorLayers.js` file imports the following dependencies:

- **React**: JavaScript library for building user interfaces.
- **Leaflet**: A leading open-source JavaScript library for mobile-friendly interactive maps.
- **React-Leaflet**: React components for Leaflet maps.
- **Leaflet CSS**: Styles for Leaflet maps.

```javascript
import React, { Component } from "react";
import Leaflet from "leaflet";
import { Map, TileLayer, Popup, Circle, CircleMarker, Polygon, Polyline, Rectangle } from "react-leaflet";
import "leaflet/dist/leaflet.css";
```

## Component Description

The `MapVectorLayers` component is a React class component that renders a map centered on a specific set of coordinates. It includes various vector layers like circles, markers, polylines, and polygons, each demonstrating different ways to display and interact with map data.

## Vector Layers Explained

- **Circle**: Represents a circle centered around a given point with a specified radius.
- **CircleMarker**: Similar to Circle but has a fixed radius in pixels.
- **Polygon**: Represents a shape with a series of connected lines forming a closed loop.
- **Polyline**: A connected series of line segments.
- **Rectangle**: A polygon representing a rectangle with specified bounds.

## Code Walkthrough

### State Initialization

The component initializes its state to store the default latitude, longitude, and zoom level of the map.

```javascript
state = {
  lat: 51.505,
  lng: -0.09,
  zoom: 13,
};
```

### Rendering the Map

The `render()` method sets up the map using React-Leaflet's `Map` component. It includes a `TileLayer` for the base map and various vector layers.

```javascript
render() {
  const position = [this.state.lat, this.state.lng];
  return (
    <Map center={position} zoom={this.state.zoom} style={{ height: "300px" }}>
      <TileLayer
        attribution='&amp;copy <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      />
      {/* Various vector layers here */}
    </Map>
  );
}
```

### Vector Layers

The component includes several vector layers with different colors and positions:

- **Circle**: Blue circle centered at the map's initial position.
- **CircleMarker**: Red marker with a popup.
- **Polyline**: Lime-colored lines showing routes.
- **Polygon**: Purple-colored shapes representing areas.
- **Rectangle**: Black rectangle marking a specific area.

## Features and Interactivity

- **Interactive Popups**: The CircleMarker includes a popup that appears when clicked.
- **Customizable Styles**: Each vector layer can have customized colors and properties.
- **Resizable Map**: The map is responsive and adjusts to the container size.

## Usage

To use the `MapVectorLayers` component, simply import it into your React application and include it in your JSX:

```javascript
import MapVectorLayers from './MapVectorLayers';

function App() {
  return (
    <div>
      <h1>Vector Layers Map</h1>
      <MapVectorLayers />
    </div>
  );
}

export default App;
```

This component provides a robust starting point for adding interactive maps with vector layers to your web applications, making it easier to visualize geospatial data and user interactions.

# Documentation for `LayerGroup.js`

## Overview

The `LayerGroup.js` file is a React component that utilizes the `react-leaflet` library to create an interactive map with various geographical features. This map includes different layers such as circles and rectangles, showcasing how to use grouped map layers and feature groups in a Leaflet map. The map is centered on a specific latitude and longitude and is set up to render OpenStreetMap tiles.

## Components and Libraries Used

- **React**: A JavaScript library for building user interfaces.
- **Leaflet**: A popular open-source JavaScript library for interactive maps.
- **react-leaflet**: A React wrapper for Leaflet, providing React components for Leaflet elements.
- **TileLayer**: A layer that displays map tiles from a URL template.
- **Circle**: A circle overlay on the map.
- **FeatureGroup**: A group of layers that can be treated as a single layer.
- **LayerGroup**: A group of layers that can be toggled on and off.
- **Rectangle**: A rectangular overlay on the map.
- **Popup**: A popup that can be attached to markers or other map features.

## Code Explanation

```javascript
import React, { Component } from "react";
import Leaflet from "leaflet";
import { Circle, FeatureGroup, LayerGroup, Map, Popup, Rectangle, TileLayer } from "react-leaflet";
import "leaflet/dist/leaflet.css";
```

- The code begins by importing necessary modules and components from `react-leaflet` and `Leaflet`. It also imports CSS for styling the map.

### Leaflet Icon Configuration

```javascript
Leaflet.Icon.Default.imagePath = "../node_modules/leaflet";
delete Leaflet.Icon.Default.prototype._getIconUrl;
Leaflet.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});
```

- These lines configure the default icon paths for Leaflet markers. This ensures the icons are correctly displayed on the map.

### Rectangle Coordinates

```javascript
const rectangle = [
  [51.49, -0.08],
  [51.5, -0.06],
];
```

- Defines the geographical bounds for a rectangle to be displayed on the map.

### Component Definition

```javascript
export default class LayerGroupMap extends Component {
  state = {
    lat: 51.505,
    lng: -0.09,
    zoom: 13,
  };

  render() {
    const position = [this.state.lat, this.state.lng];
    return (
      <Map center={position} zoom={this.state.zoom} style={{ height: "300px" }}>
        <TileLayer
          attribution='&amp;copy <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        />
        <LayerGroup>
          <Circle center={position} fillColor="blue" radius={200} />
          <Circle center={position} fillColor="red" radius={100} stroke={false} />
          <LayerGroup>
            <Circle center={[51.51, -0.08]} color="green" fillColor="green" radius={100} />
          </LayerGroup>
        </LayerGroup>
        <FeatureGroup color="purple">
          <Popup>Popup in FeatureGroup</Popup>
          <Circle center={[51.51, -0.06]} radius={200} />
          <Rectangle bounds={rectangle} />
        </FeatureGroup>
      </Map>
    );
  }
}
```

- **State**: Manages the map's center coordinates and zoom level.
- **Map**: Main component that renders the map with specified center and zoom.
- **TileLayer**: Renders OpenStreetMap tiles.
- **LayerGroup**: Contains a group of circle layers, demonstrating how to manage multiple layers together.
- **FeatureGroup**: Another group of map features that includes a circle and a rectangle, with an attached popup.

## Usage

To use this component, simply import it into your React application and include it within your JSX. It will render a Leaflet map with multiple interactive layers.

## Conclusion

The `LayerGroup.js` file provides a comprehensive example of utilizing `react-leaflet` to create complex maps with grouped layers and feature groups. It demonstrates how to manipulate map layers for interactive web applications, making it a valuable resource for developers looking to integrate maps into their projects.

# 📜 MapLayerControl.js Documentation

The `MapLayerControl.js` file is a React component built using the `react-leaflet` library. It provides an interactive map with multiple layers and controls, allowing users to toggle between different map views and overlays. This component is particularly valuable for applications that require dynamic map interactions and visualization of geospatial data.

## 📑 Index

- [Overview](#overview)
- [Dependencies](#dependencies)
- [Component Structure](#component-structure)
- [Core Features](#core-features)
- [Code Breakdown](#code-breakdown)
- [PropTypes](#proptypes)

## 🖥️ Overview

The `MapLayerControl` component is a class-based React component that leverages Leaflet's mapping capabilities to render a map with customizable layers and control features. Users can select different base layers and overlays, enhancing the map's interactivity.

## 📦 Dependencies

This component relies on the following dependencies:

- **React**: A JavaScript library for building user interfaces.
- **react-leaflet**: A React wrapper for Leaflet, providing a set of React components for Leaflet maps.
- **Leaflet**: An open-source JavaScript library for mobile-friendly interactive maps.
- **leaflet.css**: The CSS file for styling Leaflet maps.

## 🏗️ Component Structure

```jsx
export default class MapLayerControl extends Component {
  state = {
    lat: 51.505,
    lng: -0.09,
    zoom: 13,
  };

  render() {
    const center = [this.state.lat, this.state.lng];
    return (
      <Map center={center} zoom={this.state.zoom} style={{ height: "300px" }}>
        <LayersControl position="topright">
          {/* Base Layer Options */}
          <BaseLayer checked name="OpenStreetMap.Mapnik">
            {/* TileLayer for Mapnik */}
          </BaseLayer>
          <BaseLayer name="OpenStreetMap.BlackAndWhite">
            {/* TileLayer for Black and White */}
          </BaseLayer>
          
          {/* Overlay Options */}
          <Overlay name="Marker with popup">
            {/* Marker with Popup */}
          </Overlay>
          <Overlay checked name="Layer group with circles">
            {/* LayerGroup with Circles */}
          </Overlay>
          <Overlay name="Feature group">
            {/* FeatureGroup with Circle and Rectangle */}
          </Overlay>
        </LayersControl>
      </Map>
    );
  }
}
```

## ✨ Core Features

- **Multiple Base Layers**: Allows users to toggle between different map styles (e.g., Mapnik, Black and White).
- **Interactive Overlays**: Includes markers, circles, and feature groups with popups.
- **Layer Control**: Users can easily switch between layers using the `LayersControl` component.

## 🔍 Code Breakdown

### State Management

- **State Variables**:
  - `lat`: Latitude of the map's center.
  - `lng`: Longitude of the map's center.
  - `zoom`: Zoom level of the map.

### Map Component

- **Map**: The main container for the Leaflet map, centered at the specified coordinates with a defined zoom level.

### Layers Control

- **LayersControl**: A control element that provides toggling options for base layers and overlays.

### Base Layers

- **TileLayer**: Provides selectable map styles. The example includes:
  - `OpenStreetMap.Mapnik`
  - `OpenStreetMap.BlackAndWhite`

### Overlays

- **Marker with Popup**: Displays a marker with a customizable popup.
- **LayerGroup with Circles**: Contains multiple circles with varying colors and sizes.
- **FeatureGroup**: Includes a circle and a rectangle with an embedded popup.

## 📋 PropTypes

The component doesn't use PropTypes directly. However, the presence of `Leaflet` and `react-leaflet` ensures the integration of Leaflet maps with React components.

### 📝 Note

To use this component, ensure that the required dependencies are installed and properly configured within your React application. Adjust the map's center and zoom level according to your needs for optimal visualization.

This documentation provides a detailed overview of the `MapLayerControl.js` file, highlighting its structure, features, and code implementation. Use this as a reference guide for understanding and extending the component's capabilities. 🗺️

# Vectormap.js Documentation 📜

The `Vectormap.js` file is a React component that implements a vector map using the `react-jvectormap` library. This component is styled using SCSS to provide a visually appealing and interactive map experience. Below is a detailed explanation of the component, its purpose, and how it can be utilized.

## Table of Contents 📚

1. [Overview](#overview)
2. [Key Features](#key-features)
3. [Component Breakdown](#component-breakdown)
4. [Props](#props)
5. [Styling](#styling)
6. [Usage Example](#usage-example)

## Overview

The `Vectormap` component is used to render vector maps that provide an interactive UI for geographical data visualization. This component allows developers to display different types of maps (e.g., world map, country-specific maps) with customizable regions and styles.

## Key Features

- **Interactive Maps**: The component supports interactive features like hover and selected state changes.
- **Customizable Appearance**: Easily change colors for regions and selected areas.
- **Responsive Design**: Adapts to container width for consistent display on various devices.

## Component Breakdown

```jsx
import PropTypes from 'prop-types';
import React from "react";
import { VectorMap } from "react-jvectormap";
import "./jquery-jvectormap.scss";

const map = React.createRef(null);

const Vectormap = props => {
  return (
    <div style={{ width: props.width, height: 500 }}>
      <VectorMap
        map={props.value}
        backgroundColor="transparent"
        ref={map}
        containerStyle={{
          width: "100%",
          height: "80%",
        }}
        regionStyle={{
          initial: {
            fill: props.color,
            stroke: "none",
            "stroke-width": 0,
            "stroke-opacity": 0,
          },
          hover: {
            "fill-opacity": 0.8,
            cursor: "pointer",
          },
          selected: {
            fill: "#2938bc",
          },
          selectedHover: {},
        }}
        containerClassName="map"
      />
    </div>
  );
};

Vectormap.propTypes = {
  color: PropTypes.string,
  value: PropTypes.any,
  width: PropTypes.any,
};

export default Vectormap;
```

## Props

The `Vectormap` component accepts the following props:

| Prop Name | Type          | Description                                         |
|-----------|---------------|-----------------------------------------------------|
| `color`   | `string`      | Defines the initial color of the map regions.       |
| `value`   | `any`         | Specifies the map value to be rendered (e.g., map type). |
| `width`   | `any`         | Determines the width of the map container.          |

## Styling

The component uses a SCSS file `jquery-jvectormap.scss` for styling. It defines how the map is displayed and enhances the visual appeal of the vector map. The styling involves:

- Setting the container's dimensions and background.
- Customizing region styles for various states: initial, hover, and selected.

## Usage Example

Here is a basic example of how the `Vectormap` component can be used:

```jsx
import React from 'react';
import Vectormap from './Vectormap';

const MyMapComponent = () => (
  <div>
    <h1>My Interactive Map</h1>
    <Vectormap value="world_mill" width="100%" color="#3b5de7" />
  </div>
);

export default MyMapComponent;
```

In this example, a world map is rendered with a blue color (`#3b5de7`) and adapts to the full width of its container.

## Conclusion

The `Vectormap` component is a powerful tool for integrating interactive vector maps into React applications. Its flexibility and customizable features make it suitable for various use cases, from displaying global data to focusing on specific geographical regions. 🚀

# 📜 MapsLeaflet.js Documentation

## Overview

The **MapsLeaflet.js** file is a React component that utilizes the Leaflet library to display various types of interactive maps on a webpage. It includes different map functionalities such as basic maps, maps with markers, popups, custom icons, vector layers, and layer controls, making it versatile for displaying geographical data in an engaging manner. The component is structured using Reactstrap for styling and layout.

## Table of Contents

- [Components and Imports](#components-and-imports)
- [Functionality](#functionality)
- [Structure and Layout](#structure-and-layout)
- [Usage and Integration](#usage-and-integration)

## Components and Imports

### Main React Components

- **SimpleMap**: Displays a basic Leaflet map.
- **MapWithPopup**: Integrates popups into the map.
- **MapVectorLayers**: Showcases vector layers including markers, circles, and polygons.
- **MapMarkerCustomIcons**: Allows for the use of custom icons for map markers.
- **LayerGroup**: Demonstrates the grouping of different map layers for better organization.
- **MapLayerControl**: Provides controls to manage the visibility and interaction of different layers.

### External Libraries

- **React**: The core library to build UI components.
- **Reactstrap**: Provides Bootstrap 4 components for React.
- **Breadcrumbs**: Displays breadcrumb navigation for the map page.

### File Imports
```javascript
import React from "react";
import { Row, Col, Card, CardBody } from "reactstrap";
import SimpleMap from "./LeafletMap/SimpleMap";
import MapWithPopup from "./LeafletMap/MapWithPopup";
import MapVectorLayers from "./LeafletMap/MapVectorLayers";
import MapMarkerCustomIcons from "./LeafletMap/MapMarkerCustomIcons";
import LayerGroup from "./LeafletMap/LayerGroup";
import MapLayerControl from "./LeafletMap/MapLayerControl";
import Breadcrumbs from "../../components/Common/Breadcrumb";
```

## Functionality

The **MapsLeaflet.js** component encapsulates multiple Leaflet map examples, each demonstrating different features of the Leaflet library:

- **Basic Map Display**: Introduce users to a simple map interface.
- **Interactive Popup Feature**: Engage users with interactive popups on map elements.
- **Custom Markers and Icons**: Personalize map markers with custom icons.
- **Layer and Feature Grouping**: Organize map features into logical groupings for enhanced user control.
- **Layer Control Management**: Provide UI controls for toggling map layers and features.

## Structure and Layout

### Page Layout

The component uses a grid system for layout, dividing the page into rows and columns to display the maps neatly. Each map example is contained within a Bootstrap card component, provided by Reactstrap, allowing for consistent styling and spacing.

```jsx
<Row>
  <Col lg="6">
    <Card>
      <CardBody>
        <h4 className="card-title mb-4">Example</h4>
        <div id="leaflet-map" className="leaflet-map">
          <SimpleMap />
        </div>
      </CardBody>
    </Card>
  </Col>
  ...
</Row>
```

### Breadcrumbs

Breadcrumb navigation is included at the top of the page to facilitate user navigation, indicating the current page and its hierarchy within the application.

```jsx
<Breadcrumbs title="Maps" breadcrumbItem="Leaflet" />
```

## Usage and Integration

To integrate **MapsLeaflet.js** into your application, ensure that all required Leaflet map components (e.g., SimpleMap, MapWithPopup, etc.) are correctly implemented and imported. This component is designed to be placed within a larger React application where Leaflet maps are required.

### Example Integration

```jsx
import MapsLeaflet from './path/to/MapsLeaflet';

function App() {
  return (
    <div className="App">
      <MapsLeaflet />
    </div>
  );
}

export default App;
```

## Conclusion

The **MapsLeaflet.js** component is a comprehensive solution for adding interactive and engaging maps using the Leaflet library. With its modular design and use of React and Reactstrap, it is flexible and easy to integrate into any modern web application.

# 📄 MapsVector.js Documentation

## 📚 Introduction
The `MapsVector.js` file is a React component that renders a series of vector maps using the `reactstrap` library for styling and layout. The component displays various geographical maps, such as the USA, World, Canada, and Asia maps. 

## 📜 Component Overview

### **MapsVector Component**
- This is the main component that gets exported and is responsible for rendering the vector maps.
- It utilizes the `Vector` component from the `Vectormap.js` file to display the maps.

### **Imported Libraries and Components**
- **React**: Used to create the component.
- **reactstrap**: Provides `Row`, `Col`, `Card`, `CardBody`, `CardTitle`, and `CardSubtitle` components for UI layout.
- **Vectormap**: Imported as `Vector`, used to render the vector maps.
- **Breadcrumbs**: A custom component for displaying navigation breadcrumbs at the top of the page.

## 📋 Structure and Layout

The MapsVector component is structured with a series of rows and columns to display different maps. Here's a breakdown of its structure:

### **Breadcrumbs**
- Displays the title "Maps" and a breadcrumb item "Vector Maps" at the top of the page.

### **Row and Col Layout**
- The component uses a grid system to organize maps in a responsive manner.

```jsx
<Row>
  <Col lg={6}>
    <Card>
      <CardBody>
        <CardTitle className="h4">USA Map</CardTitle>
        <CardSubtitle className="mb-3">Example of vector map.</CardSubtitle>
        <div id="usa" className="vector-map-height">
          <Vector value="us_aea" width="500" color="#3b5de7" />
        </div>
      </CardBody>
    </Card>
  </Col>

  <Col lg={6}>
    <Card>
      <CardBody>
        <CardTitle className="h4">World Map</CardTitle>
        <CardSubtitle className="mb-3">Example of vector map.</CardSubtitle>
        <div id="world-map-markers" className="vector-map-height">
          <Vector value="world_mill" width="500" color="#3b5de7" />
        </div>
      </CardBody>
    </Card>
  </Col>
</Row>
```

### **Map Details**
Each map is displayed inside a `Card` with the following attributes:
- **CardTitle**: Displays the title of the map (e.g., "USA Map").
- **CardSubtitle**: Provides a brief description (e.g., "Example of vector map").
- **Vector Component**: A map is rendered with specific properties:
  - `value`: Specifies the map type.
  - `width`: Width of the map in pixels.
  - `color`: Color theme for the map.

## 🌍 Maps Displayed
1. **USA Map**: Displayed with the `us_aea` value.
2. **World Map**: Displayed with the `world_mill` value.
3. **Canada Map**: Displayed with the `ca_lcc` value.
4. **Asia Vector Map**: Displayed with the `asia_mill` value.

## 📦 Export
The `MapsVector` component is exported as the default export, making it easily importable into other parts of the application.

## 🎨 Styles
- The `vector-map-height` class is used for setting map dimensions.
- The color `#3b5de7` is used for map styling to ensure consistency across different maps.

## Conclusion
`MapsVector.js` is a straightforward React component that efficiently organizes and displays vector maps using reusable components and a clean, responsive design. It leverages the power of React and `reactstrap` for a seamless user experience.

# 📄 LightData.js Documentation

## 🌈 Introduction
The `LightData.js` file is a simple JavaScript module that exports a `lightData` object. This object is specifically designed for styling Google Maps with a light-themed aesthetic. It defines various styling rules that modify the appearance of different map features such as roads, parks, water bodies, etc.

## 📚 Table of Contents
1. [Overview](#overview)
2. [Structure](#structure)
3. [Feature Types and Elements](#feature-types-and-elements)
4. [Usage](#usage)
5. [Conclusion](#conclusion)

## 🔍 Overview
The `lightData` object contains a property named `Data`, which is an array of style objects. Each style object specifies how a particular feature type or element on the map should appear, including its color, lightness, and visibility. This styling is intended to create a minimalist and clean look for Google Maps.

## 🏗️ Structure
Below is a simplified example of the structure of the `lightData` object:

```javascript
const lightData = {
  Data: [
    {
      featureType: "water",
      elementType: "geometry",
      stylers: [
        { color: "#e9e9e9" },
        { lightness: 17 }
      ],
    },
    // ...additional styles
  ]
}
```

## 🔧 Feature Types and Elements

The `lightData` object includes styling for various feature types and elements. Here's a breakdown of the most significant ones:

| **Feature Type**      | **Element Type**        | **Stylers**                                      |
|-----------------------|-------------------------|--------------------------------------------------|
| `water`               | `geometry`              | Color: `#e9e9e9`, Lightness: `17`                 |
| `landscape`           | `geometry`              | Color: `#f5f5f5`, Lightness: `20`                 |
| `road.highway`        | `geometry.fill`         | Color: `#ffffff`, Lightness: `17`                 |
| `road.highway`        | `geometry.stroke`       | Color: `#ffffff`, Lightness: `29`, Weight: `0.2` |
| `road.arterial`       | `geometry`              | Color: `#ffffff`, Lightness: `18`                 |
| `road.local`          | `geometry`              | Color: `#ffffff`, Lightness: `16`                 |
| `poi`                 | `geometry`              | Color: `#f5f5f5`, Lightness: `21`                 |
| `poi.park`            | `geometry`              | Color: `#dedede`, Lightness: `21`                 |
| `transit`             | `geometry`              | Color: `#f2f2f2`, Lightness: `19`                 |
| `administrative`      | `geometry.fill`         | Color: `#fefefe`, Lightness: `20`                 |
| `administrative`      | `geometry.stroke`       | Color: `#fefefe`, Lightness: `17`, Weight: `1.2` |

The `stylers` attribute of each element type influences how the map renders, including color, lightness, and visibility properties.

## 🛠️ Usage
The `lightData` object is typically imported into other files (such as `MapsGoogle.js`) to be utilized in setting the map's style. Here is an example of how it might be used:

```javascript
import { lightData } from './LightData';

// Use the styles in a Map component
<Map
  google={props.google}
  styles={lightData.Data}
  // other props
/>
```

## 🎯 Conclusion
The `LightData.js` file provides a reusable and straightforward way to apply a light theme to Google Maps. This styling is particularly useful for applications that require a clean and modern map appearance. By leveraging the different feature types and stylers, developers can create visually appealing maps that fit their application's design.

Feel free to integrate this styling configuration to bring a bright and minimalist touch to your Google Maps implementations! 🌟

# 📌 MapsGoogle.js Documentation

Welcome to the **MapsGoogle.js** documentation! This file is a React component designed to integrate and display Google Maps within a web application. It uses the `google-maps-react` package to facilitate the interaction with Google Maps API, and it offers several features including map markers, overlays, and custom styles.

## 📋 Index

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [Core Features](#core-features)
5. [Component Usage](#component-usage)
6. [Props](#props)
7. [Code Walkthrough](#code-walkthrough)

## 🌍 Introduction

The **MapsGoogle.js** component is designed to render a Google Map with various interactive elements like markers and overlays. It supports customizable styles and uses Redux for state management, making it a versatile choice for applications requiring map integration.

## 📦 Dependencies

This component relies on several third-party libraries and packages:

- **React**: For building the user interface.
- **google-maps-react**: A React wrapper for Google Maps API.
- **react-redux**: For state management.
- **reactstrap**: For UI components like Cards and Grids.
- **prop-types**: For type-checking the component's props.

## 🏗️ Component Structure

The **MapsGoogle** component is structured using React functional components and hooks. It consists of several nested elements, including:

- **Map**: The main map component from `google-maps-react`.
- **Marker**: Represents markers on the map.
- **InfoWindow**: Displays information related to a marker.
- **Cards**: Used for organizing different map examples.

## 🌟 Core Features

- **Markers**: Display markers on the map with tooltips.
- **Overlays**: Demonstrate map overlays with different styles.
- **Custom Styles**: Apply custom styles to the map using `lightData`.
- **Responsive Design**: Maps are styled to fit responsive layouts.

## 🔧 Component Usage

To use the **MapsGoogle** component, you need to import it and provide a Google Maps API key. Here's an example of how to integrate it:

```jsx
import MapsGoogle from './MapsGoogle';

function App() {
  return (
    <div>
      <MapsGoogle google={window.google} />
    </div>
  );
}

export default App;
```

## 🛠️ Props

The **MapsGoogle** component accepts the following props:

| Prop Name | Type         | Description                       |
|-----------|--------------|-----------------------------------|
| `google`  | `object`     | The Google Maps API object.       |

## 📜 Code Walkthrough

Let's break down the code to understand its functionality:

1. **Imports**: The component imports necessary libraries and components including `Map`, `Marker`, and `InfoWindow` from `google-maps-react`.

2. **LoadingContainer**: A simple functional component to display a loading message while the map data is being fetched.

    ```jsx
    const LoadingContainer = () => <div>Loading...</div>;
    ```

3. **MapsGoogle Component**: The main functional component which renders the Google Map.

    - **Breadcrumbs**: Displays navigation breadcrumbs.
    - **Map**: Renders the map with markers and info windows.
    - **Markers**: Clickable elements on the map.
    - **InfoWindow**: Shows additional information when a marker is clicked.

    ```jsx
    const MapsGoogle = props => {
      const selectedPlace = {};

      function onMarkerClick() {
        alert("You clicked in this marker");
      }

      return (
        <React.Fragment>
          <div className="page-content">
            <div className="container-fluid">
              <Breadcrumbs title="Maps" breadcrumbItem="Google Maps" />
              <Row>
                <Col lg={6}>
                  <Card>
                    <CardBody>
                      <CardTitle>Markers</CardTitle>
                      <CardSubtitle className="mb-3">
                        Example of google maps.
                      </CardSubtitle>
                      <div id="gmaps-markers" className="gmaps" style={{ position: "relative" }}>
                        <Map google={props.google} style={{ width: "100%", height: "100%" }} zoom={14}>
                          <Marker title={"The marker`s title will appear as a tooltip."} name={"SOMA"} position={{ lat: 37.778519, lng: -122.40564 }} />
                          <Marker name={"Dolores park"} />
                          <InfoWindow>
                            <div>
                              <h1>{selectedPlace.name}</h1>
                            </div>
                          </InfoWindow>
                        </Map>
                      </div>
                    </CardBody>
                  </Card>
                </Col>
                {/* Additional map examples */}
              </Row>
            </div>
          </div>
        </React.Fragment>
      );
    };
    ```

4. **PropTypes**: Validates the `google` prop to ensure it is an object.

    ```jsx
    MapsGoogle.propTypes = {
      google: PropTypes.object
    };
    ```

5. **Export**: The component is wrapped with `GoogleApiWrapper` to connect it to the Google Maps API and exported using Redux `connect`.

    ```jsx
    export default connect(
      null,
      {}
    )(GoogleApiWrapper({
      apiKey: "YOUR_GOOGLE_MAPS_API_KEY",
      LoadingContainer: LoadingContainer,
      v: "3",
    })(MapsGoogle));
    ```

## 🎉 Conclusion

The **MapsGoogle.js** component is a powerful way to integrate Google Maps into your React application. With customizable markers, overlays, and responsive design, it offers a robust solution for displaying interactive maps. By following this documentation, you can effectively utilize and extend the component's capabilities in your projects.