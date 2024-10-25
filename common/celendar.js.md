# 📅 Calendar.js Documentation

Welcome to the **Calendar.js** documentation! This file is part of a larger project and is responsible for managing and defining events within a calendar system. Let's dive deeper into the structure and functionality of this file. 🌟

## 📜 Table of Contents

- [Overview](#overview)
- [Date Handling](#date-handling)
- [Event Details](#event-details)
- [Default Categories](#default-categories)
- [Exported Modules](#exported-modules)

---

## 🎯 Overview

The `calendar.js` file is designed to handle events and categories within a calendar application. It defines a set of events with various attributes such as title, start date, end date, and style classes. Additionally, it categorizes these events into default categories.

## 📅 Date Handling

The file begins by creating a new `Date` object to fetch the current date, month, and year. This data is utilized to set the start and end dates for the events.

```javascript
const date = new Date();
const d = date.getDate();
const m = date.getMonth();
const y = date.getFullYear();
```

- `d`: Day of the month
- `m`: Month of the year (zero-indexed)
- `y`: Current year

## 📌 Event Details

The `events` array contains a list of event objects, each with specific details:

- **id**: Unique identifier for the event
- **title**: Name of the event
- **start**: Start date and time of the event
- **end**: (Optional) End date and time of the event
- **allDay**: Boolean indicating if the event lasts all day
- **className**: CSS class for styling the event
- **url**: (Optional) External link associated with the event

Here's a breakdown of some of the events:

| ID | Title              | Start Date                   | End Date                     | Class Name            | All Day | URL                |
|----|--------------------|------------------------------|------------------------------|-----------------------|---------|--------------------|
| 1  | All Day Event      | Start of the current month   | -                            | `bg-primary text-white` | true    | -                  |
| 2  | Long Event         | 5 days ago                   | 2 days ago                   | `bg-warning text-white` | false   | -                  |
| 5  | Meeting            | Today at 10:30 AM            | -                            | `bg-success text-white` | false   | -                  |
| 8  | Click for Google   | 28th of current month        | 29th of current month        | `bg-dark text-white`   | false   | http://google.com/ |

## 🎨 Default Categories

The `calenderDefaultCategories` array defines default categories for organizing events. Each category contains:

- **id**: Unique identifier
- **title**: Name of the category
- **type**: CSS class for the category

Here's a look at the default categories:

| ID | Title             | Type          |
|----|-------------------|---------------|
| 1  | New Theme Release | `bg-success`  |
| 2  | My Event          | `bg-info`     |
| 3  | Meet Manager      | `bg-warning`  |
| 4  | Report Error      | `bg-danger`   |

## 📦 Exported Modules

The file exports two key modules:

- **calenderDefaultCategories**: An array of default event categories
- **events**: An array of defined events

```javascript
export { calenderDefaultCategories, events }
```

These exports allow other parts of the application to import and utilize the events and categories defined in this file.

---

Thank you for exploring the **Calendar.js** documentation! 🎉 This file is integral to managing events and categories within your calendar application, making it easier to organize and display important dates and activities. 📆✨