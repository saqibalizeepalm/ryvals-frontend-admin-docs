# ImageSliderList.js Documentation 📜

Welcome to the **ImageSliderList.js** documentation! This file is part of a React application, responsible for managing and displaying a list of image sliders (banners) in a responsive table format. This document will provide a detailed overview of the code, explaining its purpose, structure, and functionality.

## 📚 Index

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [State Management](#state-management)
4. [Functions](#functions)
   - [getList](#getlist)
   - [openModal](#openmodal)
   - [closeModal](#closemodal)
   - [deleteBanner](#deletebanner)
5. [Component Structure](#component-structure)
6. [UI Elements](#ui-elements)
7. [Conditional Rendering](#conditional-rendering)
8. [Alert and Notifications](#alert-and-notifications)
9. [Conclusion](#conclusion)

## Introduction

The **ImageSliderList.js** component is a part of a banner management system. It retrieves a list of banners from an API, displays them in a responsive table, and provides features to add, edit, or delete a banner. It uses various React and third-party libraries for UI and state management.

## Imports

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, Button } from "reactstrap";
import { Table, Thead, Tbody, Tr, Th, Td } from "react-super-responsive-table";
import "react-super-responsive-table/dist/SuperResponsiveTableStyle.css";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import { getBannerList, removeBanner } from "../../services/banner_api_helper";
import { Link } from "react-router-dom";
import SweetAlert from "react-bootstrap-sweetalert";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
```

### Explanation

- **React**: Core library for building the user interface.
- **Reactstrap**: Provides Bootstrap components as React components.
- **react-super-responsive-table**: Enables responsive table layout.
- **Breadcrumbs**: Component for displaying navigational breadcrumbs.
- **Banner API Helpers**: Functions to interact with the backend banner API.
- **SweetAlert**: Library for beautiful alerts.
- **React Toastify**: Provides notifications to the user.

## State Management

The component uses React's `useState` hook to manage the following states:

- **banners**: Stores the list of banners.
- **openDeleteModal**: Controls the visibility of the delete confirmation modal.
- **selectedBanner**: Holds the banner selected for deletion.

## Functions

### getList

```javascript
const getList = async () => {
  await getBannerList().then((res) => {
    setBanners(res);
  });
};
```

- **Purpose**: Fetches the list of banners from the backend API and updates the `banners` state.

### openModal

```javascript
const openModal = (banner) => {
  setselectedBanner(banner);
  setopenDeleteModal(true);
};
```

- **Purpose**: Opens the delete confirmation modal and stores the selected banner in the state.

### closeModal

```javascript
const closeModal = () => {
  setopenDeleteModal(false);
};
```

- **Purpose**: Closes the delete confirmation modal.

### deleteBanner

```javascript
const deleteBanner = async () => {
  await removeBanner(selectedBanner.id)
    .then(() => {
      toast.success("Banner Removed Successfully", toastrOptions);
      closeModal();
      getList();
    })
    .catch((err) => {
      toast.error(err, toastrOptions);
      closeModal();
    });
};
```

- **Purpose**: Deletes a banner from the backend API, notifies the user, and refreshes the banner list.

## Component Structure

The main component function `ImageSliderList` renders a page with a breadcrumb, an add banner button, and a table of current banners.

## UI Elements

- **Breadcrumb**: Displays the current page location as "Banners".
- **Button**: Provides an option to add a new banner, linking to the `/banner/add` route.
- **Table**: Lists banners with columns for image, description, link, and actions (edit/delete).

## Conditional Rendering

- Checks if there are banners to display; otherwise, it shows a "No Banner(s) Found" message.
- Displays a **SweetAlert** modal when attempting to delete a banner, asking for confirmation.

## Alert and Notifications

- **SweetAlert**: Provides a confirmation dialog for deleting a banner.
- **React Toastify**: Shows success or error notifications based on the result of the delete operation.

## Conclusion

The **ImageSliderList.js** component is a robust part of a banner management system, providing essential CRUD operations for image sliders. It leverages modern React features and libraries to create a responsive and user-friendly interface. This documentation should serve as a comprehensive guide to understand and extend the functionalities of this component. 🎉

Thank you for reading this documentation! If you have any questions or need further clarification, feel free to reach out. Happy coding! 🚀