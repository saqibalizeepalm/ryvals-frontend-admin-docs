
# Documentation for TopicsDropDown.js 📄

## Overview
The `TopicsDropDown.js` file defines a React component named `TopicsDropDown`. This component uses `react-select` to render a dropdown menu that allows users to select an existing topic or create a new one. It's a part of a larger system, likely a CMS (Content Management System), that deals with managing topics, possibly for FAQ or PPK content.

## Key Features
- **Topic Selection**: Users can select an existing topic from a list.
- **Topic Creation**: Users have the ability to create new topics directly from the dropdown.
- **Editable and Clearable**: The dropdown supports clearing the selection and is editable if permissions (`data.change`) allow.

## Dependencies
- **React**: A JavaScript library for building user interfaces.
- **react-select**: A flexible, customizable select input control for React.
- **react-select/creatable**: Allows users to create new options in a dropdown.

## Component Details

### Props
The `TopicsDropDown` component accepts the following props:

| Prop Name | Type | Description |
|-----------|------|-------------|
| `setTopic` | Function | Callback function to set the current topic. |
| `topic` | Object | The currently selected topic. |
| `options` | Array | Array of available topic options. |
| `data` | Object | Contains permissions and other state information. |

### Functions

#### `formatCreateLabel`
Formats the label when creating a new topic, displaying "Create new topic.." followed by the input value.

```javascript
const formatCreateLabel = (inputValue) => `Create new topic.. ${inputValue}`;
```

#### `handleChange`
Handles the change event for the dropdown and updates the selected topic using the `setTopic` callback.

```javascript
const handleChange = (topicChange) => {
    setTopic(topicChange);
};
```

#### `Input`
A custom input component that limits the maximum length of the input field. It uses the `maxLength` prop to enforce this restriction.

```javascript
const Input = (props) => {
    const { maxLength } = props.selectProps;
    return <components.Input {...props} maxLength={maxLength} />;
};
```

### Component Usage

Below is how the component is structured and rendered:

```jsx
return (
    <CreatableSelect
        components={{ Input }}
        isClearable
        isDisabled={!data.change}
        options={options}
        key={topic?.value}
        defaultValue={topic}
        formatCreateLabel={formatCreateLabel}
        placeholder="Select or create new topic"
        onChange={handleChange}
        value={topic}
        maxLength={50}
    />
);
```

- **CreatableSelect**: This component is used to render the dropdown. It is clearable and can be disabled based on the `data.change` property.
- **Input Component**: A customized input component to enforce the `maxLength` attribute.
- **Placeholder**: "Select or create new topic" is used as the placeholder text.

## Conclusion
The `TopicsDropDown` component provides a user-friendly interface for managing topics within a CMS. It supports both selection from existing topics and the creation of new topics, with clear permissions handling for enabling or disabling editing capabilities. This component leverages the power of `react-select` to provide a flexible and extensible dropdown interface.
# Documentation for the `TestCms.js` File

Welcome to the detailed documentation for the `TestCms.js` file. This file is a part of a React application and is responsible for managing a simple content management system (CMS) interface, specifically handling "Terms and Conditions" and "Privacy Policy" sections.

## Table of Contents
1. [Introduction](#introduction)
2. [Imports and Dependencies](#imports-and-dependencies)
3. [Component Overview](#component-overview)
4. [State Management](#state-management)
5. [Functions and Methods](#functions-and-methods)
6. [Render Method](#render-method)
7. [Usage](#usage)
8. [Conclusion](#conclusion)

---

## Introduction

The `TestCMS` component is a React functional component that serves as a basic CMS interface. It allows administrators to view and edit the contents of "Terms and Conditions" and "Privacy Policy". The component uses the ReactQuill text editor to provide rich text editing capabilities.

## Imports and Dependencies

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, CardTitle, Nav, NavItem, NavLink, TabContent, TabPane, Button } from "reactstrap";
import classnames from "classnames";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import ReactQuill from "react-quill";
import "react-quill/dist/quill.snow.css";
import Loader from "../../components/Common/Loader";
import { getTermsAndCondition, addTermsCMS, editTermsCMS, getPrivacyPolicy, addPrivacyCMS, editPrivacyCMS } from "../../services/cms_api_helper";
```

### Key Dependencies:
- **React and Reactstrap**: For building UI components and layout.
- **classnames**: For conditional CSS class names.
- **ReactQuill**: A rich text editor component for writing and editing text content.
- **Custom Services**: Functions imported from `cms_api_helper` for API interactions.

## Component Overview

### `TestCMS` Component

This component provides a tabbed interface for editing "Terms and Conditions" and "Privacy Policy". It uses two main tabs to switch between these sections, utilizing React's state and effect hooks for managing data and lifecycle events.

## State Management

The component uses several pieces of state, managed by the `useState` hook:

- **isLoading**: Indicates whether data is currently being loaded.
- **activeTab**: Determines which tab is currently active.
- **termsNdCondition**: Stores the current text for "Terms and Conditions" being edited.
- **terms**: Stores the saved version of "Terms and Conditions".
- **policy**: Stores the saved version of "Privacy Policy".
- **privacyPolicy**: Stores the current text for "Privacy Policy" being edited.

## Functions and Methods

### `useEffect`

- **callTermsAndCondition**: Fetches "Terms and Conditions" content when the component mounts.

### API Interaction Functions

- **callTermsAndCondition**: Fetches terms and conditions from the server.
- **callPrivacyPolicy**: Fetches privacy policy from the server.

### Content Management Functions

- **setTermsData**: Updates the state with the edited content from the Quill editor for "Terms and Conditions".
- **addTermsNdCondition**: Handles form submission to save or update "Terms and Conditions".
- **setPrivacyPolicyData**: Updates the state with the edited content from the Quill editor for "Privacy Policy".
- **addPrivacyPolicyData**: Handles form submission to save or update "Privacy Policy".

## Render Method

The render method returns a fragment containing the following main components:

- **Loader**: Displays a loading indicator when data is being fetched.
- **Breadcrumbs**: Shows the navigation path within the application.
- **Tabs and Tab Content**: Managed by `reactstrap` components to allow switching between editing "Terms and Conditions" and "Privacy Policy".
- **ReactQuill Editor**: Used for rich text editing of the content.
- **Submit Buttons**: For saving the changes made in the editors.

## Usage

To utilize the `TestCMS` component, it should be included in a React application where the requisite services (`cms_api_helper`) are available for API interaction. The component is designed to handle both viewing and editing of text content, providing a straightforward interface for non-technical users to manage legal and informational documents.

## Conclusion

The `TestCMS.js` file is a well-structured React component that integrates a rich text editor with state management and API calls to provide a simple yet effective CMS interface. It leverages React's hooks for state and lifecycle management and utilizes third-party UI components from Reactstrap and ReactQuill to enhance the user experience.

# Documentation for `quill-utils.js` 📜

Welcome to the documentation for the `quill-utils.js` file! This file is designed to configure and export utility settings for the Quill Rich Text Editor. Quill is a powerful, modern WYSIWYG editor built for the web. This utility file focuses on defining the toolbar options and formats available in the editor.

## Table of Contents 📑

- [Introduction](#introduction)
- [Modules Configuration](#modules-configuration)
  - [Toolbar](#toolbar)
  - [Clipboard](#clipboard)
- [Formats](#formats)
- [Conclusion](#conclusion)

## Introduction

The `quill-utils.js` file exports two main configurations for Quill:
1. **`modules`**: Defines the modules used by Quill, specifically the toolbar layout and clipboard behavior.
2. **`formats`**: Lists the formats that the Quill editor supports.

These configurations allow developers to easily customize the Quill editor's functionality and appearance in their applications.

## Modules Configuration

### Toolbar

The `toolbar` configuration specifies the tools available to the user in the Quill editor's toolbar. It is an array of arrays, where each inner array represents a group of tools. Below is the breakdown of the toolbar configuration:

- **Header Levels**: Allows users to set text as either Header 1 or Header 2.
- **Font Selection**: Provides a dropdown for selecting different fonts.
- **Text Size**: Offers a dropdown to choose the size of the text.
- **Text Formatting**: Includes options for bold, italic, underline, strike-through, and blockquote.
- **Lists and Indents**: Features ordered and unordered lists, and indent controls.
- **Image**: Supports image insertion.
- **Clean**: Provides a tool to remove formatting from selected text.

Here's a code snippet illustrating the toolbar configuration:

```javascript
toolbar: [
  [{ header: "1" }, { header: "2" }, { font: [] }],
  [{ size: [] }],
  ["bold", "italic", "underline", "strike", "blockquote"],
  [
    { list: "ordered" },
    { list: "bullet" },
    { indent: "-1" },
    { indent: "+1" },
  ],
  ["image"],
  ["clean"],
],
```

### Clipboard

The `clipboard` module configuration controls how pasted content is handled. The `matchVisual` property is set to `false`, ensuring extra line breaks are not added when pasting HTML content.

```javascript
clipboard: {
  matchVisual: false,
},
```

## Formats

The `formats` array defines which formatting options are allowed by the Quill editor. This configuration ensures that only specified formats can be applied to the text. Here are the supported formats:

- `header`
- `font`
- `size`
- `bold`
- `italic`
- `underline`
- `strike`
- `blockquote`
- `list`
- `bullet`
- `indent`
- `image`

### Code Example

Here's how the `formats` array is structured:

```javascript
export const formats = [
  "header",
  "font",
  "size",
  "bold",
  "italic",
  "underline",
  "strike",
  "blockquote",
  "list",
  "bullet",
  "indent",
  "image",
];
```

## Conclusion

The `quill-utils.js` file is a crucial setup for integrating the Quill text editor. By defining the toolbar and format options, it provides a versatile and user-friendly editing experience. You can modify these settings as needed to fit the specific requirements of your application.

Thank you for reading this documentation! 🙌 If you have any questions or need further assistance, feel free to reach out.
# Documentation for `QuestionList.js`

---

## Overview

The `QuestionList.js` component serves as a wrapper for displaying a list of questions using a drag-and-drop interface. It utilizes the `PPKDranNDrop` component to provide sorting and interaction capabilities for the questions within a list, allowing users to edit, delete, or reorder questions easily.

## Components and Props

### `QuestionList`

- **Props:**
  - **`enableAddQuestionView`**: A function that toggles the view for adding a new question.
  - **`questions`**: An array of question objects to be displayed in the list. Defaults to an empty array.
  - **`enableEditView`**: A function that switches the interface to edit mode for a specific question.
  - **`deleteQuestion`**: A function that handles the deletion of a question.
  - **`onDragEnd`**: A callback function triggered when a drag-and-drop operation ends.
  - **`isFaq`**: A boolean indicating if the list belongs to a FAQ section. Defaults to `false`.
  - **`subQuestionid`**: A unique identifier for sub-questions, used when questions are nested.
  - **`questionNum`**: A numeric identifier for the question list, used for tracking order.
  - **`data`**: An object containing additional data for permissions or configuration.

### Structure

The `QuestionList` component is structured as follows:

```jsx
import React from "react";
import PPKDranNDrop from "./PPKDranNDrop";

const QuestionList = ({
  enableAddQuestionView,
  questions = [],
  enableEditView,
  deleteQuestion,
  onDragEnd,
  isFaq = false,
  subQuestionid,
  questionNum,
  data,
}) => {
  return (
    <>
      <PPKDranNDrop
        questions={questions}
        deleteQuestion={deleteQuestion}
        enableEditView={enableEditView}
        onDragEnd={onDragEnd}
        isFaq={isFaq}
        subQuestionid={subQuestionid}
        questionNum={questionNum}
        data={data}
      />
    </>
  );
};

export default QuestionList;
```

## Key Features ✨

- **Drag-and-Drop Interface**: Utilizes the `PPKDranNDrop` component to allow users to reorder questions visually. This enhances user experience by providing intuitive interaction with list items.
- **Question Management**: Integrates functions for adding, editing, and deleting questions, making it a versatile component for managing question lists.
- **Conditional Rendering**: Supports FAQ and non-FAQ sections through the `isFaq` prop to adjust functionality and appearance as needed.

## Usage Example

Here's a basic example of how the `QuestionList` component could be used in a parent component:

```jsx
import React from "react";
import QuestionList from "./QuestionList";

const ExampleComponent = () => {
  const questions = [
    { id: 1, text: "What is the meaning of life?" },
    { id: 2, text: "How does the internet work?" },
  ];

  const handleEditView = (question) => {
    console.log("Edit question:", question);
  };

  const handleDeleteQuestion = (questionId) => {
    console.log("Delete question with ID:", questionId);
  };

  const handleDragEnd = (result) => {
    console.log("Drag ended:", result);
  };

  return (
    <QuestionList
      questions={questions}
      enableEditView={handleEditView}
      deleteQuestion={handleDeleteQuestion}
      onDragEnd={handleDragEnd}
      isFaq={true}
    />
  );
};

export default ExampleComponent;
```

## Conclusion

The `QuestionList.js` component is a fundamental part of the CMS interface, allowing for interactive and flexible management of question items within a list. With its integration of drag-and-drop functionality and support for various operations, it provides a robust solution for handling dynamic content in web applications.

# 📄 PPK.js Documentation

This document provides a detailed explanation of the `PPK.js` file, which is part of a content management system (CMS) for managing "What’s PPK" questions. This file facilitates the creation, editing, deletion, and reordering of questions related to the PPK topic using React components and a drag-and-drop interface.

## 📑 Table of Contents

1. [Introduction](#introduction)
2. [Imports](#imports)
3. [State Variables](#state-variables)
4. [Key Functions](#key-functions)
   - [Fetching Questions](#fetching-questions)
   - [Adding a Question](#adding-a-question)
   - [Editing a Question](#editing-a-question)
   - [Deleting a Question](#deleting-a-question)
   - [Reordering Questions](#reordering-questions)
5. [Event Handlers](#event-handlers)
6. [Rendering Logic](#rendering-logic)
7. [Component Structure](#component-structure)

## 🔍 Introduction

The `PPK.js` file defines the `PPK` component which manages a list of questions related to a topic called "What’s PPK". It uses a drag-and-drop interface to facilitate the reordering of questions and supports CRUD (Create, Read, Update, Delete) operations for individual questions.

## 📥 Imports

```javascript
import React, { useEffect, useRef, useState } from "react";
import { deleteQuestion, editQuestion, getQuestions, postQuestion } from "../../services/cms_api_helper";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import Loader from "../../components/Common/Loader";
import AddQuestion from "./AddQuestion";
import QuestionList from "./QuestionList";
import { Button, CardTitle } from "reactstrap";
import { DragDropContext } from "react-beautiful-dnd";
```

- **React**: Used for building user interface components.
- **Reactstrap**: Provides Bootstrap 4 components for React.
- **React Beautiful DnD**: Offers drag-and-drop functionality for reordering questions.
- **React Toastify**: Used for displaying success and error notifications.
- **Loader**: A common component for displaying a loading spinner.
- **CMS API Helper**: Contains functions for API operations.

## 🗂️ State Variables

- **`listView`**: Determines whether the list of questions is being viewed.
- **`isEdit`**: Indicates if a question is in edit mode.
- **`topicId`**: Stores the ID of the current topic.
- **`isLoading`**: Shows a loading indicator during API calls.
- **`questions`**: Holds the list of questions fetched from the API.
- **`editQuestionData`**: Stores data for the question that is being edited.

## 🔧 Key Functions

### Fetching Questions

```javascript
const getPPKQuestions = async () => {
  try {
    setIsLoading(true);
    const filter = { filter: "PPK" };
    const res = await getQuestions(filter);
    setIsLoading(false);
    topicId.current = res?.results?.[0]?.id;
    setQuestions(res?.results?.[0]?.category?.questions);
  } catch (error) {
    setIsLoading(false);
    toast.error(error, toastrOptions);
  }
};
```
- Fetches questions under the "PPK" topic from the server and updates the component state.

### Adding a Question

```javascript
const postQuestionPPK = async ({ filter, callback }) => {
  try {
    setIsLoading(true);
    await postQuestion(filter);
    callback();
    setIsLoading(false);
    toast.success("Question Added Successfully", toastrOptions);
    getPPKQuestions();
  } catch (error) {
    setIsLoading(false);
    toast.error(error, toastrOptions);
  }
};
```
- Posts a new question to the server and refreshes the question list.

### Editing a Question

```javascript
const editQuestionPPK = async ({ payload, questionId }) => {
  try {
    setIsLoading(true);
    await editQuestion({ payload, questionId });
    disableEditView();
    toast.success("Question Edited Successfully", toastrOptions);
    getPPKQuestions();
  } catch (error) {
    disableEditView();
    setIsLoading(false);
    toast.error(error, toastrOptions);
  }
};
```
- Updates an existing question on the server and refreshes the list.

### Deleting a Question

```javascript
const deleteQuestionPPK = async ({ questionId, callback }) => {
  try {
    setIsLoading(true);
    await deleteQuestion({ questionId });
    toast.success("Question Deleted Successfully", toastrOptions);
    getPPKQuestions();
  } catch (error) {
    callback();
    setIsLoading(false);
    toast.error(error, toastrOptions);
  }
};
```
- Removes a question from the server and updates the list.

### Reordering Questions

```javascript
const reorderQuestionPPK = async ({ payload, questionId }) => {
  try {
    await editQuestion({ payload, questionId });
    const filter = { filter: "PPK" };
    setIsLoading(true);
    const res = await getQuestions(filter);
    topicId.current = res?.results?.[0]?.id;
    setQuestions(res?.results?.[0]?.category?.questions);
    setIsLoading(false);
    toast.success("Question Reorder Successfully", toastrOptions);
  } catch (error) {
    toast.error(error, toastrOptions);
    setIsLoading(false);
  }
};
```
- Changes the order of questions and updates the server.

## ⚡️ Event Handlers

- **`enableEditView`**: Sets the state to edit mode for a specific question.
- **`disableEditView`**: Disables edit mode and returns to view mode.
- **`enableListView`**: Switches to the list view mode.

## 🖼️ Rendering Logic

- **Loader**: Displays a loading spinner while API calls are in progress.
- **Conditionally Renders**: 
  - The question list view.
  - The `AddQuestion` component when adding or editing a question.
  - Drag-and-drop functionality for reordering questions.

## 🏗️ Component Structure

The `PPK` component renders based on the state variables, providing a dynamic user interface for managing questions. It handles different views (list and edit) and manages the interaction with the server for fetching, updating, and deleting questions.

## 🖨️ Example Usage

```jsx
<PPK data={{ view: true, add: true }} />
```
- This component can be used within a larger application to manage a list of questions related to the "What’s PPK" topic, providing the necessary permissions to view and add questions.

This documentation provides comprehensive insights into how the `PPK.js` file operates within a CMS, detailing its various functionalities and interactions with the server.

# 📄 Documentation for `PPKDranNDrop.js`

## Overview
The `PPKDranNDrop.js` file is a React component that provides a drag-and-drop interface for managing a list of questions. It leverages the `react-beautiful-dnd` library to allow users to reorder questions dynamically. This component is highly reusable and can be used in different contexts where a list configuration is needed.

## Components and Libraries Used
- **React**: A JavaScript library for building user interfaces.
- **Droppable & Draggable**: Components from `react-beautiful-dnd` that enable drag-and-drop functionality.
- **CMSRow**: A custom component used for rendering individual question rows.

## Component Structure

### Props
The component accepts several props to manage its behavior and rendering:

| Prop Name        | Type     | Description                                                                 |
|------------------|----------|-----------------------------------------------------------------------------|
| `questions`      | Array    | An array of question objects to be displayed and managed.                   |
| `enableEditView` | Function | Callback function to switch to an edit view for a specific question.        |
| `deleteQuestion` | Function | Callback function to handle the deletion of a question.                     |
| `droppableId`    | String   | A unique identifier for the droppable area. Defaults to `"droppable"`.      |
| `isFaq`          | Boolean  | Indicates if the context is FAQ. Modifies behavior if true.                 |
| `subQuestionid`  | String   | An identifier to distinguish different sets of questions.                   |
| `questionNum`    | String   | A unique identifier for each question for drag-and-drop operations.         |
| `data`           | Object   | Contains permission and configuration data, affecting interactivity.        |

### Component Functionality
- **Droppable Component**: Acts as a container for draggable items. It uses a unique `droppableId` to manage drag-and-drop interactions.
- **Draggable Component**: Wraps individual question items, allowing them to be dragged within the `Droppable` container.

### Render Logic
The component maps over the `questions` array, rendering each question as a `Draggable` component. Each question:
- Is associated with a unique key derived from `questionNum` and `question.id`.
- Is rendered using the `CMSRow` component, which handles display and actions for each question.

### Example Usage
```javascript
<PPKDranNDrop 
  questions={questionsArray}
  enableEditView={handleEditView}
  deleteQuestion={handleDeleteQuestion}
  droppableId="myDroppableId"
  isFaq={true}
  subQuestionid="sub-1"
  questionNum="1"
  data={permissionsData}
/>
```

## Key Features
- **Drag-and-Drop**: Uses `react-beautiful-dnd` for intuitive reordering of questions.
- **Conditional Rendering**: Only renders questions if they exist in the provided array.
- **Interactivity**: Based on the `data` prop, the component can be configured to allow or disable dragging.

## Conclusion
The `PPKDranNDrop` component is a flexible and powerful tool for managing lists of questions within a drag-and-drop interface. It's especially useful in content management systems where user interactions with question lists are frequent and need to be user-friendly and efficient.

# FAQ.js Documentation

## Introduction
The `FAQ.js` file is a React component responsible for managing the FAQ section within a CMS (Content Management System). It handles the display, addition, editing, deletion, and reordering of FAQ topics and questions. This component leverages various libraries and components to provide a dynamic and interactive FAQ management interface.

## Table of Contents
- [Key Imports](#key-imports)
- [Component Overview](#component-overview)
- [State Variables](#state-variables)
- [Key Functions](#key-functions)
- [Component Methods](#component-methods)
- [Render Logic](#render-logic)

## Key Imports
```javascript
import React, { useEffect, useState } from "react";
import { Button, CardTitle } from "reactstrap";
import CMSRow from "./CMSRow";
import { deleteQuestion, deleteTopic, editQuestion, editTopic, getQuestions, postQuestion } from "../../services/cms_api_helper";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import Loader from "../../components/Common/Loader";
import { DragDropContext, Droppable, Draggable } from "react-beautiful-dnd";
import AddQuestion from "./AddQuestion";
import QuestionList from "./QuestionList";
import { Accordion, AccordionItem, AccordionItemButton, AccordionItemHeading, AccordionItemPanel } from "react-accessible-accordion";
import "./accordian.scss";
import EditTopic from "./EditTopic";
```

## Component Overview
The `FAQ` component is designed to manage FAQs effectively by utilizing several other components and libraries:
- **CMSRow**: Displays each FAQ question/topic.
- **AddQuestion**: Form for adding new questions.
- **EditTopic**: Form for editing existing topics.
- **QuestionList**: Displays a list of questions under a topic.
- **React Beautiful DnD**: Enables drag-and-drop functionality for reordering topics/questions.
- **React Accessible Accordion**: Provides accordion functionality for listing FAQs.

## State Variables
The component maintains several state variables to manage its operations:
- **listView**: Boolean to toggle between list and form views.
- **isEdit**: Boolean to check if in edit mode.
- **topic**: Boolean to determine if editing a topic.
- **isLoading**: Boolean to show loading state.
- **questions**: Array to store the list of questions and topics.
- **editQuestionData**: Object to hold data for the question being edited.

## Key Functions

### Data Fetching and Management
- **getFAQQuestions**: Fetches the list of FAQ questions from the server.
- **postQuestionFAQ**: Submits a new FAQ question to the server.
- **deleteQuestionFAQ**: Deletes a specific FAQ question.
- **deleteTopicFAQ**: Deletes an entire FAQ topic.
- **editQuestionFAQ**: Edits an existing FAQ question.
- **editTopicFAQ**: Edits an entire FAQ topic.

### View Management
- **enableEditView**: Switches to the edit view for a question.
- **enableEditViewFAQ**: Switches to the edit view for a topic.
- **disableEditView**: Resets to the list view from edit view.
- **enableListView**: Enables the list view.
- **enableAddQuestionView**: Switches to the add question view.

### Drag-and-Drop
- **reorder**: Helper function to reorder items in a list.
- **onDragEnd**: Handles the logic when a drag-and-drop operation ends, updating the order of questions/topics.

## Component Methods

### useEffect
- **getFAQQuestions** is called when the component mounts or when the `props.data.view` changes.

### Accordion and Drag-and-Drop
- The component utilizes an accordion to display topics, with drag-and-drop functionality to reorder them. It uses the `react-beautiful-dnd` library to handle the drag-and-drop logic.

## Render Logic
- **Loader**: Displays a loading spinner when data is being fetched or modified.
- **CardTitle**: Displays the title and the "Add New" button, if adding is permitted.
- **Accordion**: Displays the FAQs as expandable sections. Each section can contain multiple questions.
- **DragDropContext**: Handles the drag-and-drop operations for reordering topics and questions.
- **Conditional Rendering**: The component conditionally renders forms for adding or editing based on the current state (`listView`, `isEdit`, `topic`).

The `FAQ.js` component provides a robust interface for managing FAQs in a CMS, allowing for dynamic content updates and order management with a user-friendly UI.

# JoditEditorForm.js Documentation

Welcome to the documentation for `JoditEditorForm.js`. This file is a React component that integrates the Jodit WYSIWYG (What You See Is What You Get) editor and provides a form to submit edited content to a server. Below is a detailed guide to understand its implementation and usage.

## Table of Contents
1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Component Structure](#component-structure)
4. [Props](#props)
5. [State Variables](#state-variables)
6. [Configuration](#configuration)
7. [Effects and Handlers](#effects-and-handlers)
8. [Rendering](#rendering)
9. [Export](#export)

## Overview

The `JoditEditorForm` component is designed to:
- Display a rich text editor using the Jodit library.
- Allow editing of content depending on user permissions.
- Submit the edited content back to the server.

## Dependencies

This component uses the following libraries:
- **React** - For creating the component.
- **reactstrap** - For UI components such as `Button`.
- **jodit-react** - For the Jodit Editor integration.

## Component Structure

```jsx
function JoditEditorForm({ dataFromAPI = () => {}, postDataToServer = () => {}, changePermission, }) { ... }
```

## Props

The component accepts the following props:

| Prop Name       | Type     | Description                                                                 |
|-----------------|----------|-----------------------------------------------------------------------------|
| `dataFromAPI`   | Function | Callback to fetch data from an API and set it as the editor's initial content. |
| `postDataToServer` | Function | Callback to handle form submission and post edited data to a server.       |
| `changePermission` | Boolean | Determines if the editor should be in read-only mode or editable.           |

## State Variables

- **`content`**: Stores the current content of the editor.
- **`apiData`**: Holds data fetched from the API, initially set as the editor's content.

## Configuration

A memoized configuration object for the Jodit Editor is created using `useMemo` to enhance performance by avoiding unnecessary recalculations.

```javascript
const config = useMemo(() => ({
  readonly: !changePermission,
  showBrowserColorPicker: false,
  removeButtons: ["brush"],
}), [changePermission]);
```

## Effects and Handlers

- **`useEffect`**: Fetches initial data from the API to set the editor's content when the component mounts.
  
  ```jsx
  useEffect(() => {
    dataFromAPI({ setContent });
  }, []);
  ```

- **`handleSetContext`**: Updates the `content` and `apiData` state whenever changes are made in the editor.
  
  ```jsx
  const handleSetContext = (value) => {
    setContent(value);
    setApiData(value);
  };
  ```

## Rendering

The component renders a form containing:

- **JoditEditor**: Uses the configured settings and updates the content state on changes.
  
  ```jsx
  <JoditEditor
    value={content}
    config={config}
    tabIndex={1}
    onBlur={handleSetContext}
    onChange={handleSetContext}
  />
  ```

- **Submit Button**: Triggers form submission and is disabled when `changePermission` is `false`.

  ```jsx
  <Button
    type="submit"
    color="primary"
    className="ms-1 cms-button privacy-policy-submit-btn"
    style={{ marginTop: "60px" }}
    disabled={!changePermission}
  >
    Submit
  </Button>
  ```

## Export

The component is exported as default.

```javascript
export default JoditEditorForm;
```

---

This documentation provides a comprehensive understanding of the `JoditEditorForm.js` file, detailing its components, props, and functionality. The integration of Jodit Editor with controlled access based on permissions makes this component versatile for various content management scenarios.

# Documentation for `EditorToolbar.js`

The `EditorToolbar.js` file is a React component that provides a customizable toolbar for the Quill rich text editor. This toolbar allows users to format text and manipulate content with various editing tools. Below is a detailed documentation for understanding the structure and functionality of this component.

---

## Index

1. [Introduction](#introduction)
2. [Formats](#formats)
3. [Custom Buttons](#custom-buttons)
4. [QuillToolbar Component](#quilltoolbar-component)
5. [Usage Example](#usage-example)

---

## Introduction

The `EditorToolbar.js` file defines a set of tools that can be incorporated into a Quill editor instance to enhance text editing capabilities. It allows users to apply various styles and effects to their text content.

## Formats

The `formats` array specifies the various text formats that the Quill editor can support. These formats determine which buttons and options appear in the toolbar.

```javascript
export const formats = [
  "header", "font", "size", "bold", "italic", "underline", "align",
  "strike", "script", "blockquote", "background", "list", "bullet",
  "indent", "link", "image", "color", "code-block"
];
```

### Format Descriptions

- **header**: Text header (heading levels)
- **font**: Font family
- **size**: Text size
- **bold**, **italic**, **underline**, **strike**: Text styling
- **align**: Text alignment
- **script**: Superscript/subscript
- **blockquote**: Quote styling
- **background**: Background color
- **list**: Ordered and unordered lists
- **indent**: Text indentation
- **link**, **image**, **video**: Media embedding
- **color**: Text color
- **code-block**: Code block styling

## Custom Buttons

The file defines two simple custom button components. While they are currently placeholders (as seen with the `octicon-star`), they can be extended to introduce additional functionality.

```javascript
const CustomButton = () => <span className="octicon octicon-star" />;
const CustomButtonRaw = () => <span className="octicon octicon-star" />;
```

## QuillToolbar Component

The main exported component `QuillToolbar` is responsible for rendering the toolbar interface. It accepts two props: `toolbarId` to uniquely identify the toolbar and `onClickRaw` to handle raw mode toggling.

```javascript
export const QuillToolbar = ({ toolbarId, onClickRaw }) => {
  return (
    <div id={toolbarId}>
      <span className="ql-formats">
        <select className="ql-font" defaultValue="arial">
          <option value="arial">Arial</option>
          <option value="comic-sans">Comic Sans</option>
          <option value="courier-new">Courier New</option>
          <option value="georgia">Georgia</option>
          <option value="helvetica">Helvetica</option>
          <option value="lucida">Lucida</option>
        </select>
        <select className="ql-size" defaultValue="medium">
          <option value="extra-small">Size 1</option>
          <option value="small">Size 2</option>
          <option value="medium">Size 3</option>
          <option value="large">Size 4</option>
        </select>
        <select className="ql-header" defaultValue="3">
          <option value="1">Heading</option>
          <option value="2">Subheading</option>
          <option value="3">Normal</option>
        </select>
      </span>
      <span className="ql-formats">
        <button className="ql-bold" />
        <button className="ql-italic" />
        <button className="ql-underline" />
        <button className="ql-strike" />
      </span>
      <span className="ql-formats">
        <button className="ql-list" value="ordered" />
        <button className="ql-list" value="bullet" />
        <button className="ql-indent" value="-1" />
        <button className="ql-indent" value="+1" />
      </span>
      <span className="ql-formats">
        <button className="ql-script" value="super" />
        <button className="ql-script" value="sub" />
        <button className="ql-blockquote" />
        <button className="ql-direction" />
      </span>
      <span className="ql-formats">
        <select className="ql-align" />
        <select className="ql-color">
          <option value="#00cdff" />
          <option value="#FFFFFF" />
          <!-- Additional color options omitted for brevity -->
        </select>
      </span>
      <span className="ql-formats">
        <button className="ql-link" />
        <button className="ql-image" />
        <button className="ql-video" />
      </span>
      <span className="ql-formats">
        <button className="ql-formula" />
        <button className="ql-code-block" />
        <button className="ql-clean" />
      </span>
      <button type="button" onClick={onClickRaw}> Raw </button>
    </div>
  );
};
```

### Props

- `toolbarId`: A unique identifier for the toolbar.
- `onClickRaw`: A function to toggle raw HTML view.

## Usage Example

To use the `QuillToolbar`, import the component and include it in your editor setup:

```javascript
import React from 'react';
import { QuillToolbar } from './EditorToolbar';

const MyQuillEditor = () => {
  return (
    <div>
      <QuillToolbar toolbarId="my-toolbar" onClickRaw={() => console.log('Raw mode toggled')} />
      {/* Include Quill editor here */}
    </div>
  );
};
```

---

This component effectively modularizes the toolbar functionality for a Quill editor, allowing developers to easily customize and extend text editing features in their React applications.

# Documentation for `EditTopic.js`

## Overview
The `EditTopic.js` file is a React component designed to facilitate editing a topic within a content management system (CMS). It uses the `availity-reactstrap-validation` package for form validation and `reactstrap` for UI components. This component allows users to edit the name of a topic and submit the changes.

## Table of Contents
- [Component Props](#component-props)
- [Structure and Functionality](#structure-and-functionality)
- [Key Features](#key-features)
- [Usage](#usage)
- [Code Explanation](#code-explanation)

## Component Props

| Prop Name         | Type     | Description                                                                 |
|-------------------|----------|-----------------------------------------------------------------------------|
| `enableListView`  | function | Callback function to enable the list view after editing is completed.        |
| `editQuestionData`| object   | Contains the current data of the topic to be edited, including its slug.     |
| `editTopicFAQ`    | function | Function to be called when the form is submitted, used to update the topic.  |
| `data`            | object   | Contains permissions data, used to determine if editing is allowed.          |

## Structure and Functionality

### Import Statements
- **React**: Essential for creating React components.
- **AvField, AvForm**: For form and input validation.
- **reactstrap Components**: `Button`, `CardTitle`, and `FormGroup` are used for UI elements.
- **Assets**: Imports a back icon image for navigation.

### Component Structure
The `EditTopic` component consists of:
- A **back button** that allows users to return to the list view.
- A **form** containing a single input field for editing the topic name.
- **Submit and Cancel buttons** for form actions.

### Form Validation
- Validation is provided by the `AvField` component, ensuring the topic name is required and does not exceed 50 characters.

## Key Features
- **Form Validation**: Ensures user input meets specified criteria.
- **Edit Functionality**: Allows users to modify the name of a topic.
- **Responsive UI**: Utilizes `reactstrap` for consistent styling and component behavior.
- **Permission Control**: Respects `data.change` to enable or disable editing based on user permissions.

## Usage
This component is meant to be part of a larger CMS where users can manage topics. It is particularly useful in scenarios where topics need to be frequently updated or corrected.

## Code Explanation

```jsx
const EditTopic = ({ enableListView, editQuestionData = {}, editTopicFAQ, data, }) => {
    const resetForm = () => {
        enableListView();
    };

    return (
        <>
            <CardTitle>
                <div style={{ cursor: "pointer" }} onClick={enableListView}>
                    <img alt="back-icon" src={backIcon} />
                    <span style={{ display: "inline-block", marginLeft: "4px", color: "black", }}> back </span>
                </div>
            </CardTitle>
            <div className="faq-box d-flex flex-column align-items-start mb-4 pl-3">
                <div>
                    <AvForm onValidSubmit={(e, v) => {
                        editTopicFAQ({
                            payload: { name: v.topic },
                            topicSlug: editQuestionData.topic.slug,
                            callback: resetForm,
                        });
                    }}>
                        <div className="mb-3">
                            <AvField
                                key={editQuestionData.topic.id}
                                name="topic"
                                label="Topic"
                                placeholder="Enter topic here"
                                type="text"
                                value={editQuestionData?.topic.name}
                                validate={{
                                    required: { value: true, errorMessage: "Topic is required" },
                                    maxLength: { value: 50, errorMessage: "Topic can have 50 characters max" }
                                }}
                                disabled={!data.change}
                            />
                        </div>
                        {data.change ? (
                            <FormGroup style={{ marginTop: "20px" }}>
                                <div>
                                    <Button type="submit" color="primary" className="ms-1 mr-2"> Submit </Button>
                                    <Button onClick={resetForm} type="reset" color="secondary" outline className="ms-1"> Cancel </Button>
                                </div>
                            </FormGroup>
                        ) : null}
                    </AvForm>
                </div>
            </div>
        </>
    );
};
```

- **Reset Function**: `resetForm` is a helper function to invoke `enableListView`, likely to navigate back to the list view.
- **Form Submission**: On form submission, `editTopicFAQ` is called with the new topic name, using the existing topic's slug for identification, and `resetForm` is called to clear the form.
- **Conditional Rendering**: The `Submit` and `Cancel` buttons are only rendered if `data.change` is true, ensuring users without edit permissions cannot make changes.

---

With this documentation, you should have a comprehensive understanding of the `EditTopic.js` component, its features, and how it integrates within a larger CMS.

# Documentation for CMS.js

## Overview 🌟

The `CMS.js` file is a React component that serves as a Content Management System (CMS) interface. It manages and displays various content sections such as PPK, FAQ, Terms and Conditions, Privacy Policy, and California Policy. The component provides functionalities to view, add, edit, and manage permissions for these sections.

## Features 🎯

- **Tab Navigation:** Allows users to switch between different content sections.
- **Permission Management:** Controls user access for viewing and editing content based on permissions.
- **Content Editing:** Integrates rich text editors for editing content.
- **API Integration:** Fetches and updates content via API calls.
- **Feedback Mechanism:** Provides user notifications for actions like adding or editing content.

## Table of Contents 📑

1. [Imports and Dependencies](#imports-and-dependencies)
2. [State Management](#state-management)
3. [Effect Hooks](#effect-hooks)
4. [Helper Functions](#helper-functions)
5. [Render Method](#render-method)
6. [Export Statement](#export-statement)

## Imports and Dependencies 📚

```javascript
import React, { useEffect, useState } from "react";
import { Row, Col, Card, CardBody, CardTitle, Nav, NavItem, NavLink, TabContent, TabPane, Button } from "reactstrap";
import classnames from "classnames";
import Breadcrumbs from "../../components/Common/Breadcrumb";
import ReactQuill from "react-quill";
import "react-quill/dist/quill.snow.css";
import Loader from "../../components/Common/Loader";
import { getTermsAndCondition, addTermsCMS, editTermsCMS, getPrivacyPolicy, addPrivacyCMS, editPrivacyCMS, addCaliforniaPrivacyCMS, editCaliforniaPrivacyCMS, getCaliforniaPrivacyPolicy } from "../../services/cms_api_helper";
import { toast } from "react-toastify";
import toastrOptions from "../../helpers/toastr-options/toastr-options";
import PPK from "./PPK";
import FAQ from "./FAQ";
import FilterPermission from "../../helpers/FilterPermission";
import { filterOutPermissionToShowHide } from "../../helpers/PermissionUtils";
import EditorToolbar, { formats } from "./EditorToolbar";
import JoditEditorForm from "./JoditEditorForm";
import { CONSTANT_STRINGS, permissionsStrings, SUCCESS_MESSAGES } from "../../helpers/StringConstant";
import { isEmpty } from "lodash";
```

### Key Libraries:

- **React**: Core library for building the UI.
- **Reactstrap**: Provides Bootstrap 4 components for React.
- **React Quill**: Rich text editor for editing content.
- **Toastify**: For displaying toast notifications.
- **classnames**: Utility for conditionally joining classNames together.
- **lodash**: Utility library with various helpers.

## State Management 🧠

The component maintains several pieces of state to manage permissions, active tabs, and content data.

```javascript
const [permissionPPKFAQ, setPermissionPPKFAQ] = useState([]);
const [changePermission, setChange] = useState(false);
const [viewPermission, setView] = useState(false);
const [changePermissionPPKFAQ, setChangePPKFAQ] = useState(false);
const [viewPermissionPPKFAQ, setViewPPKFAQ] = useState(false);
const [deletePermissionPPKFAQ, setDeletePPKFAQ] = useState(false);
const [addPermissionPPKFAQ, setAddPPKFAQ] = useState(false);
const [isLoading, setisLoading] = useState(null);
const [activeTab, setactiveTab] = useState("1");
const [termsNdCondition, setTermsNdCondition] = useState("");
const [terms, setTerms] = useState("");
const [policy, setPolicy] = useState("");
const [privacyPolicy, setPrivacyPolicy] = useState("");
const [raw_html, setRawHTML] = useState("");
const [show_raw, setShowRaw] = useState(false);
```

## Effect Hooks 🔄

### Initial Permission Setup

On component mount, the `useEffect` hook is used to initialize permissions and fetch initial data.

```javascript
useEffect(() => {
    if (isEmpty(props.permission)) {
        setChange(true);
        setView(true);
    } else {
        callSetPermission();
    }
}, []);
```

## Helper Functions 🔧

### Permission Management

Sets permissions based on the provided props and manages which sections are accessible.

```javascript
const callSetPermission = () => {
    const type = permissionsStrings.staticPage;
    const typePPKFAQ = permissionsStrings.PPKFAQ;
    const filteredPermission = FilterPermission(props.permission, type);
    const filteredPermissionPPKFAQ = FilterPermission(props.permission, typePPKFAQ);

    if (filteredPermission.length !== 0) {
        const setchange = filterOutPermissionToShowHide(filteredPermission[0].permissions, permissionsStrings.typeStaticPageChange);
        const setview = filterOutPermissionToShowHide(filteredPermission[0].permissions, permissionsStrings.typeStaticPageView);
        setChange(setchange);
        setView(setview);
        callTermsAndCondition();
    }

    if (filteredPermissionPPKFAQ.length !== 0) {
        const setchangePPKFAQ = filterOutPermissionToShowHide(filteredPermissionPPKFAQ[0]?.permissions, permissionsStrings.typePPKFAQChange);
        const setviewPPKFAQ = filterOutPermissionToShowHide(filteredPermissionPPKFAQ[0]?.permissions, permissionsStrings.typePPKFAQView);
        const setdeletePPKFAQ = filterOutPermissionToShowHide(filteredPermissionPPKFAQ[0]?.permissions, permissionsStrings.typePPKFAQDelete);
        const setaddPPKFAQ = filterOutPermissionToShowHide(filteredPermissionPPKFAQ[0]?.permissions, permissionsStrings.typePPKFAQAdd);
        setChangePPKFAQ(setchangePPKFAQ);
        setViewPPKFAQ(setviewPPKFAQ);
        setDeletePPKFAQ(setdeletePPKFAQ);
        setAddPPKFAQ(setaddPPKFAQ);
        setPermissionPPKFAQ(filteredPermissionPPKFAQ[0].permissions);
    }

    setactiveTab(filteredPermissionPPKFAQ.length !== 0 ? "1" : "3");
};
```

### API Calls

Functions like `callTermsAndCondition`, `callPrivacyPolicy`, and `addTermsNdCondition` are defined to interact with the backend services.

```javascript
async function callTermsAndCondition() {
    showLoader(true);
    await getTermsAndCondition()
        .then((res) => {
            setTerms(res.content);
            showLoader(false);
        })
        .catch(() => showLoader(false));
}
```

## Render Method 🖥️

Renders the UI components, including breadcrumbs, tabs, content sections, and editors.

```javascript
return (
    <React.Fragment>
        <Loader showLoader={isLoading} />
        <div className="page-content">
            <Breadcrumbs title="Pages" breadcrumbItem="CMS" />
            <div className="checkout-tabs">
                <Row>
                    <Col lg="2">
                        <Nav className="flex-column" pills>
                            {permissionPPKFAQ.length === 0 ? null : (
                                <>
                                    <NavItem>
                                        <NavLink
                                            className={classnames({ active: activeTab === "1" })}
                                            onClick={() => { setactiveTab("1"); }}
                                        >
                                            <i className="bx bx-question-mark d-block check-nav-icon mt-4 mb-2" />
                                            <p className="fw-bold mb-4">What’s PPK?</p>
                                        </NavLink>
                                    </NavItem>
                                    <NavItem>
                                        <NavLink
                                            className={classnames({ active: activeTab === "2" })}
                                            onClick={() => { setactiveTab("2"); }}
                                        >
                                            <i className="bx bx-question-mark d-block check-nav-icon mt-4 mb-2" />
                                            <p className="fw-bold mb-4">FAQ</p>
                                        </NavLink>
                                    </NavItem>
                                </>
                            )}
                            {viewPermission ? (
                                <>
                                    <NavItem>
                                        <NavLink
                                            className={classnames({ active: activeTab === "3" })}
                                            onClick={() => { setactiveTab("3"); setShowRaw(false); }}
                                        >
                                            <i className="bx bx-question-mark d-block check-nav-icon mt-4 mb-2" />
                                            <p className="fw-bold mb-4">Terms and Conditions</p>
                                        </NavLink>
                                    </NavItem>
                                    <NavItem>
                                        <NavLink
                                            className={classnames({ active: activeTab === "4" })}
                                            onClick={() => { callPrivacyPolicy(); setactiveTab("4"); setShowRaw(false); }}
                                        >
                                            <i className="bx bx-check-shield d-block check-nav-icon mt-4 mb-2" />
                                            <p className="fw-bold mb-4">Privacy Policy</p>
                                        </NavLink>
                                    </NavItem>
                                    <NavItem>
                                        <NavLink
                                            className={classnames({ active: activeTab === "5" })}
                                            onClick={() => { setactiveTab("5"); }}
                                        >
                                            <i className="bx bx-check-shield d-block check-nav-icon mt-4 mb-2" />
                                            <p className="fw-bold mb-4">California Policy</p>
                                        </NavLink>
                                    </NavItem>
                                </>
                            ) : null}
                        </Nav>
                    </Col>
                    <Col lg="10">
                        <Card>
                            <CardBody>
                                <TabContent activeTab={activeTab}>
                                    {viewPermission || viewPermissionPPKFAQ ? (
                                        <>
                                            <TabPane tabId="1">
                                                <PPK data={{
                                                    change: changePermissionPPKFAQ,
                                                    add: addPermissionPPKFAQ,
                                                    delete: deletePermissionPPKFAQ,
                                                    view: viewPermissionPPKFAQ,
                                                }} />
                                            </TabPane>
                                            <TabPane tabId="2">
                                                <FAQ data={{
                                                    change: changePermissionPPKFAQ,
                                                    add: addPermissionPPKFAQ,
                                                    delete: deletePermissionPPKFAQ,
                                                    view: viewPermissionPPKFAQ,
                                                }} />
                                            </TabPane>
                                            <TabPane tabId="3">
                                                <CardTitle className="h4 mb-5"> Terms and Conditions </CardTitle>
                                                <div className={show_raw ? "faq-box d-flex align-items-start mb-4 showRaw" : "faq-box d-flex align-items-start mb-4"}>
                                                    <div className="flex-1">
                                                        <EditorToolbar toolbarId="toolbar-1" onClickRaw={handleClickShowRaw} />
                                                        <form onSubmit={addTermsNdCondition}>
                                                            <ReactQuill theme="snow" modules={{
                                                                toolbar: { container: `#toolbar-1`, },
                                                                clipboard: { matchVisual: false, },
                                                            }} formats={formats} onChange={setTermsData} value={termsNdCondition ? termsNdCondition : terms} placeholder="Write something" readOnly={!changePermission} />
                                                            <textarea className={"raw-editor"} onChange={(e) => handleChangeRaw(e.target.value)} value={raw_html} disabled={!changePermission} />
                                                            <Button type="submit" color="primary" className="ms-1 cms-button terms-conditions-submit-btn" style={{ marginTop: "60px" }} disabled={!changePermission}>
                                                                Submit
                                                            </Button>
                                                        </form>
                                                    </div>
                                                </div>
                                            </TabPane>
                                            <TabPane tabId="4">
                                                <CardTitle className="h4 mb-5"> Privacy Policy </CardTitle>
                                                <div className={show_raw ? "faq-box d-flex align-items-start mb-4 showRaw" : "faq-box d-flex align-items-start mb-4"}>
                                                    <div className="flex-1 privacy-policy-box">
                                                        <EditorToolbar toolbarId="toolbar-2" onClickRaw={handleClickShowRaw} />
                                                        <form onSubmit={addPrivacyPolicyData}>
                                                            <ReactQuill theme="snow" modules={{
                                                                toolbar: { container: `#toolbar-2`, },
                                                                clipboard: { matchVisual: false, },
                                                            }} formats={formats} onChange={setPrivacyPolicyData} value={privacyPolicy ? privacyPolicy : policy} placeholder="Write something" readOnly={!changePermission} />
                                                            <textarea className={"raw-editor"} onChange={(e) => handleChangeRaw(e.target.value)} value={raw_html} disabled={!changePermission} />
                                                            <Button type="submit" color="primary" className="ms-1 cms-button privacy-policy-submit-btn" style={{ marginTop: "60px" }} disabled={!changePermission}>
                                                                Submit
                                                            </Button>
                                                        </form>
                                                    </div>
                                                </div>
                                            </TabPane>
                                            <TabPane tabId="5">
                                                <CardTitle className="h4 mb-5"> California Policy </CardTitle>
                                                <div className="faq-box d-flex align-items-start mb-4">
                                                    <div className="flex-1 privacy-policy-box">
                                                        <JoditEditorForm dataFromAPI={callCaliforniaPrivacyPolicy} postDataToServer={addTermsNdConditionCalifornia} changePermission={changePermission} />
                                                    </div>
                                                </div>
                                            </TabPane>
                                        </>
                                    ) : null}
                                </TabContent>
                            </CardBody>
                        </Card>
                    </Col>
                </Row>
            </div>
        </div>
    </React.Fragment>
);
```

## Export Statement 📤

The component is exported as the default export of the module.

```javascript
export default CMS;
```

## Conclusion 🏁

The `CMS.js` component is a powerful interface for managing various content sections within an application. It integrates rich text editors, handles permissions, and provides a responsive UI for managing content. With its structured codebase, it ensures the content is easily editable and manageable, providing a seamless user experience.

# CMSRow.js Documentation

This documentation provides a detailed overview of the `CMSRow.js` component, which is an integral part of a content management system (CMS) designed to handle questions and topics. The component is built using React and various third-party packages to manage state and UI interactions seamlessly.

## Table of Contents
- [Overview](#overview)
- [Dependencies](#dependencies)
- [Component Props](#component-props)
- [State Management](#state-management)
- [Functions](#functions)
- [UI Structure](#ui-structure)
- [Modals and Alerts](#modals-and-alerts)
- [Code Snippet](#code-snippet)

## Overview
The **CMSRow** component is responsible for displaying a row of data, which could be either a FAQ question or a topic, within the CMS interface. It provides functionalities for editing and deleting these entries, offering a confirmation modal before any destructive action.

## Dependencies

The component uses several libraries and assets, including:

- **React**: To manage component lifecycle and state.
- **reactstrap**: For UI components like `Button`.
- **SweetAlert**: To display a modal alert for delete confirmations.
- **IconsToolTip**: A custom component for displaying tooltips with icons.
- **Icons**: Imported as `editIcon` and `deleteIcon` for edit and delete actions respectively.

```javascript
import { Button } from "reactstrap";
import React, { useState } from "react";
import editIcon from "../../assets/images/edit.svg";
import deleteIcon from "../../assets/images/bin.svg";
import SweetAlert from "react-bootstrap-sweetalert";
import IconsToolTip from "../../components/IconsToolTip";
```

## Component Props

The **CMSRow** component takes several props which dictate its behavior and content:

| Prop Name          | Type     | Description                                                                          |
|--------------------|----------|--------------------------------------------------------------------------------------|
| `questionData`     | Object   | The data for the question or topic to be displayed in this row.                      |
| `editCallBack`     | Function | Callback function to be called when editing is triggered.                             |
| `deleteCallback`   | Function | Callback function to be called when deleting a question is confirmed.                 |
| `enableEditView`   | Function | Function to switch to the edit view mode.                                             |
| `deleteTopic`      | Function | Function to delete a topic when confirmed.                                            |
| `editTopic`        | Function | Function to edit a topic.                                                             |
| `isFaq`            | Boolean  | Determines if the row is for a FAQ item.                                              |
| `isFaqHeading`     | Boolean  | Determines if the row is for a FAQ heading.                                           |
| `disableDeleteTopic` | Boolean | Disables the delete button for a topic.                                             |
| `data`             | Object   | Contains permissions like view, change, and delete to control button visibility.      |

## State Management

The component manages the state of its UI using `useState`:

- **showDeleteModal**: A boolean state to toggle the visibility of the delete confirmation modal.

## Functions

- **showAlert**: Stops event propagation and sets `showDeleteModal` to `true` to display the delete confirmation modal.
- **closeAlert**: Resets `showDeleteModal` to `false` to hide the modal.
- **questionStyle**: Determines the styling class for the row based on whether it is a FAQ item.

## UI Structure

The component renders a div that consists of:

1. **Question Text**: Displayed as a span with conditional styling.
2. **Edit Button**: Triggers the edit callback if the user has permission.
3. **Delete Button**: Opens the delete confirmation modal if the user has permission.

### Buttons

- **Edit Button**: Displays an icon with a tooltip. It calls `enableEditView` with the current question data.
- **Delete Button**: Similar to the edit button but triggers the delete confirmation modal.

## Modals and Alerts

The component uses **SweetAlert** to present a modal for confirming delete actions. Depending on whether it's a question or topic, the modal's title and confirm actions differ:

- **Question**: Triggers `deleteCallback`.
- **Topic**: Triggers `deleteTopic`.

## Code Snippet

Here's a small snippet highlighting the core part of the component:

```javascript
<Button type="submit" color="primary" className="edit-icon cmsEdit info-icon" onClick={showAlert} disabled={disableDeleteTopic}>
  <IconsToolTip image={deleteIcon} altImageText="delete-icon" text="Delete" />
</Button>

{showDeleteModal ? (
  <SweetAlert
    title={isFaqHeading ? "Delete Topic" : "Delete Question"}
    warning
    showCancel
    confirmButtonText="Yes"
    confirmBtnBsStyle="success"
    cancelButtonText="No"
    cancelBtnBsStyle="danger"
    onConfirm={() => {
      if (isFaqHeading) {
        deleteTopic({ topicSlug: questionData.topicData?.category?.slug, callback: closeAlert });
      } else {
        deleteCallback({ questionId: questionData?.id, callback: closeAlert });
      }
    }}
    onCancel={() => closeAlert()}
  >
    Are you sure you want to delete this {isFaqHeading ? "topic" : "question"}?
  </SweetAlert>
) : null}
```

## Conclusion

The `CMSRow` component is a versatile part of the CMS, providing essential functionalities for managing questions and topics. Its integration with SweetAlert and Reactstrap ensures a smooth and user-friendly experience. The component handles both display and confirmation of critical actions, making it an invaluable part of the CMS infrastructure.

# 📄 AddQuestion.js Documentation

Welcome to the **AddQuestion.js** file documentation. This file is a React component that provides a user interface for adding and editing questions within a FAQ or PPK system. It encompasses functionality for form validation, question input, and topic selection using a rich text editor.

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Imports](#imports)
3. [Component Props](#component-props)
4. [State and Refs](#state-and-refs)
5. [Functions](#functions)
6. [UI and JSX Rendering](#ui-and-jsx-rendering)
7. [Usage](#usage)

---

## 🧐 Overview

The **AddQuestion** component is designed to handle the addition and modification of questions. It integrates with a backend service to fetch topics and submit or update question data. It leverages several third-party libraries to enhance the user interface and provide a more interactive experience:

- **ReactQuill** for rich text editing.
- **Availity Reactstrap Validation** for form handling.
- **Reactstrap** for UI components like buttons and card titles.

---

## 📦 Imports

Here's a breakdown of the primary imports used in this component:

```javascript
import { AvField, AvForm } from "availity-reactstrap-validation"; // For form and field validation
import React, { useEffect, useRef, useState } from "react"; // React hooks
import ReactQuill from "react-quill"; // Rich text editor
import { Button, CardTitle, FormGroup } from "reactstrap"; // UI components
import { getTopics } from "../../services/cms_api_helper"; // API service for fetching topics
import { formats } from "./EditorToolbar"; // Predefined formats for the editor
import TopicsDropDown from "./TopicsDropDown"; // Component for topic selection
import backIcon from "../../assets/images/arrow-left.svg"; // Back navigation icon
```

---

## ⚙️ Component Props

The component accepts several props to customize its behavior:

| Prop               | Type     | Description                                                                 |
|--------------------|----------|-----------------------------------------------------------------------------|
| `enableListView`   | Function | Function to switch back to list view.                                       |
| `isEdit`           | Boolean  | Determines if the component is in edit mode.                                |
| `editQuestionData` | Object   | Contains data of the question being edited (if in edit mode).               |
| `topicId`          | Number   | ID of the topic when adding a question.                                      |
| `postQuestion`     | Function | Callback to post a new question.                                            |
| `editQuestion`     | Function | Callback to edit an existing question.                                      |
| `isFaq`            | Boolean  | Determines if the question relates to a FAQ.                                |
| `data`             | Object   | Additional data for the component to determine changes.                     |

---

## 🏗️ State and Refs

The component uses several state variables and refs to manage its internal state:

- **State Variables:**
  - `editorValue`: Holds the content of the rich text editor.
  - `options`: Stores the available topics.
  - `topic`: Represents the selected topic.
  - `topicError`: Flags if there's an error with the topic selection.
  - `editorError`: Flags if there's an error with the editor content.

- **Refs:**
  - `formRef`: References the form element for programmatic access.
  - `quillRef`: References the Quill editor instance.
  - `formSubmitRef`: Tracks if the form is being submitted.

---

## 🔧 Functions

### `isQuillEmpty`

Checks if the Quill editor is empty.

```javascript
const isQuillEmpty = (quill) => {
  if ((quill?.getContents()?.["ops"] || [])?.length !== 1) {
    return false;
  }
  return quill.getText()?.trim()?.length === 0;
};
```

### `UpdateEditorValue`

Updates the editor's value and checks for errors.

```javascript
const UpdateEditorValue = (content, delta, source, editor) => {
  let updatedTermsNdCondition = editor.getHTML();
  setEditorValue(updatedTermsNdCondition + "");
  setEditorError(isQuillEmpty(editor));
};
```

### `getFAQTopics`

Fetches FAQ topics from the API.

```javascript
const getFAQTopics = async () => {
  try {
    const res = await getTopics({ topicType: "FAQ" });
    setOptions(res?.results.map((category) => ({
      ...category,
      label: category.name,
      value: category.id,
    })));
  } catch (error) {}
};
```

### `resetForm`

Resets the form and states to their initial values.

```javascript
const resetForm = () => {
  formRef?.current?.reset();
  setEditorValue("");
  setTopic(null);
  formSubmitRef.current = false;
  setTopicError(false);
  setEditorError(false);
  enableListView();
};
```

---

## 🖼️ UI and JSX Rendering

The **AddQuestion** component returns a JSX structure comprising various UI elements including a form, a rich text editor, and buttons for submitting or canceling the form. It dynamically renders topics dropdown and handles validation feedback.

---

## 🔍 Usage

This component is typically used within a content management system where users can manage FAQs or PPK questions. It provides a user-friendly interface for entering questions and answers with rich text support.

---

By utilizing this documentation, developers can gain a comprehensive understanding of the **AddQuestion.js** component, its functionality, and how it integrates into a broader application. Enjoy developing with this component! 😊

# Accordion.scss Documentation 📚

Welcome to the **Accordion.scss** documentation! This detailed guide provides an overview of the styling for an accordion component using SCSS. The purpose of this file is to define the styling rules for accordion elements, commonly used in FAQs, CMS pages, or any UI that requires collapsible content sections.

## 📑 Table of Contents
1. [Introduction](#introduction)
2. [Accordion Button Styles](#accordion-button-styles)
3. [Accordion Panel Styles](#accordion-panel-styles)
4. [Animations](#animations)
5. [FAQ Specific Styles](#faq-specific-styles)
6. [Code Summary](#code-summary)

## Introduction

The **Accordion.scss** file contains SCSS styles specifically for creating an accordion component. This component allows users to toggle the visibility of content sections, enhancing the user experience by decluttering the interface.

## Accordion Button Styles 🎛️

The accordion button is a crucial part of the accordion component, as it is the interactive element users click to expand or collapse content.

### Styles:

- **Default Styles**:
  ```scss
  .accordion__button {
    color: black;
    cursor: pointer;
    border: none;
    display: inline-block;
    display: flex;
    align-items: center;
  }
  ```

  **Explanation**:
  - `color: black;`: Sets the text color to black.
  - `cursor: pointer;`: Changes the cursor to a pointer, indicating it's clickable.
  - `border: none;`: Removes any default border.
  - `display: flex;`: Utilizes flexbox for alignment.
  - `align-items: center;`: Vertically centers the content.

- **Arrow Indicator**:
  ```scss
  .accordion__button::after {
    display: inline-block;
    content: '';
    height: 10px;
    width: 10px;
    margin-right: 12px;
    border-bottom: 2px solid currentColor;
    border-right: 2px solid currentColor;
    transform: rotate(45deg);
  }
  ```

  **Explanation**:
  - Creates an arrow using borders, which rotates to indicate the accordion's state.

- **Expanded State**:
  ```scss
  .accordion__button[aria-expanded='true']::after,
  .accordion__button[aria-selected='true']::after {
    transform: rotate(-140deg);
  }
  ```

  **Explanation**:
  - Rotates the arrow to show when the panel is expanded.

## Accordion Panel Styles 🗂️

The panel is the content area that gets revealed when the accordion button is clicked.

### Styles:

```scss
.accordion__panel {
  padding: 20px;
  animation: fadein 0.35s ease-in;
}
```

- **Padding**: Adds space around the content.
- **Animation**: Applies a fade-in effect when the panel is revealed.

## Animations 🎨

Animations improve the visual feedback of the accordion component.

### Fade-in Animation:

```scss
@keyframes fadein {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
```

- **Opacity Transition**: Smoothly transitions the panel from invisible to visible.

## FAQ Specific Styles ❓

These styles are tailored for accordion components used in FAQ sections.

### Styles:

```scss
.faq-cms-page {
  .accordion__button {
    background-color: unset;
    padding: 0;
    color: #000;
    &:before {
      display: none;
    }
  }
}
```

- **Background**: Removes any background color for a cleaner look.
- **Padding**: Removes extra padding.
- **Color**: Ensures text remains black.
- **Icon Removal**: Removes any additional icons before the button text.

## Code Summary 📜

The **Accordion.scss** file is meticulously crafted to style interactive accordion components. From defining button styles to adding animations, this file ensures a seamless and visually appealing user experience. Whether used in a CMS or FAQ page, the accordion styles are flexible and easy to customize.

---

🎨 **Note**: SCSS allows for nested rules and variables, enhancing maintainability and scalability. This file leverages these features to create a robust styling foundation for accordion components.