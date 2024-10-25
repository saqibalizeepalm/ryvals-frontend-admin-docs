# PaymentConstantTypes.js Documentation 📄

Welcome to the documentation for the **PaymentConstantTypes.js** file! This document will guide you through the purpose and structure of this file. Let's dive right in! 🏊‍♂️

## Overview 📚

The **PaymentConstantTypes.js** file is a JavaScript module that exports an array of objects. Each object represents a type of payment-related action or transaction, with a `label` and a corresponding `value`. This can be useful in applications that handle financial transactions, allowing developers to easily reference and utilize different payment types throughout their codebase.

## Table of Contents 📑

1. [File Structure](#file-structure)
2. [Detailed Explanation](#detailed-explanation)
3. [Usage](#usage)
4. [Conclusion](#conclusion)

## File Structure 🏗️

Below is a breakdown of the file structure:

```javascript
const PaymentConstantTypes = [
  { label: "ADD TO WALLET", value: 1 },
  { label: "REDEEM BALANCE", value: 2 },
  { label: "PAY ENTRY FEE", value: 3 },
  { label: "RECEIVE WINNINGS", value: 4 },
  { label: "WINNINGS SEIZED", value: 5 },
  { label: "WALLET BALANCE SEIZED", value: 6 },
  { label: "REFUND", value: 7 },
  { label: "ON HOLD", value: 8 },
  { label: "RECEIVE REFERRAL", value: 9 },
  { label: "RECEIVE BONUS", value: 10 },
  { label: "VOLUNTEER", value: 11 },
  { label: "INACTIVITY CHARGES", value: 12 },
];

export default PaymentConstantTypes;
```

## Detailed Explanation 🔍

Here's a detailed look at each payment type:

| **Label**               | **Value** | **Description**                                                                            |
|-------------------------|-----------|--------------------------------------------------------------------------------------------|
| **ADD TO WALLET**       | 1         | Represents the action of adding funds to a user's wallet.                                  |
| **REDEEM BALANCE**      | 2         | Indicates redeeming or utilizing available balance for a service or product.               |
| **PAY ENTRY FEE**       | 3         | Used for transactions involving payment of an entry fee to participate in an event or game.|
| **RECEIVE WINNINGS**    | 4         | Represents receiving money as winnings, typically from a competition or game.              |
| **WINNINGS SEIZED**     | 5         | Indicates that previously earned winnings have been taken away or confiscated.             |
| **WALLET BALANCE SEIZED**| 6        | Represents the action of seizing funds directly from a user's wallet balance.              |
| **REFUND**              | 7         | Used when a user is refunded money for a previous transaction.                             |
| **ON HOLD**             | 8         | Denotes transactions that are temporarily on hold and not yet finalized.                   |
| **RECEIVE REFERRAL**    | 9         | Indicates receiving a monetary reward for referring new users to a service.                |
| **RECEIVE BONUS**       | 10        | Represents receiving a bonus, often as a reward or incentive.                              |
| **VOLUNTEER**           | 11        | Used for classifications involving volunteer actions, possibly involving voluntary payments.|
| **INACTIVITY CHARGES**  | 12        | Represents charges applied to a user due to inactivity over a period of time.              |

## Usage 🛠️

To use the **PaymentConstantTypes** in your application, you can import it as follows:

```javascript
import PaymentConstantTypes from './paymentConstantTypes';

// Example of accessing a specific payment type
const addToWallet = PaymentConstantTypes.find(type => type.label === "ADD TO WALLET");
console.log(addToWallet); // { label: "ADD TO WALLET", value: 1 }
```

This array can be iterated over or accessed directly to implement logic related to different types of payment transactions within your application.

## Conclusion 🏁

The **PaymentConstantTypes.js** file provides a centralized and easily maintainable list of payment transaction types used in an application. By using this module, developers can ensure consistent references across their codebase, simplifying the management of transaction-related logic.

Feel free to explore and utilize this module in your financial or transaction-based applications. Happy coding! 😃✨

---

This concludes the documentation for the **PaymentConstantTypes.js** file. For more information on how this file connects with other parts of your application, please refer to the related documentation or codebase.

# Documentation for `paymentConstantTypes.js` 📜

Welcome to the comprehensive documentation for `paymentConstantTypes.js`. This file is crucial for managing various types of payment-related constants in your application. Below, we will explore the structure, purpose, and usage of the constants defined in this file.

---

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Constant Definition](#constant-definition)
3. [Constant Details](#constant-details)
4. [Usage](#usage)
5. [Conclusion](#conclusion)

---

## Introduction 🌟

The **`paymentConstantTypes.js`** file provides a set of constants that represent various payment actions or events. These constants are essential for ensuring consistency and clarity across the application when handling payment-related functionalities.

---

## Constant Definition 📝

The file defines an array of objects, each containing a `label` and a `value` that represent different types of payment actions.

```javascript
const PaymentConstantTypes = [
  { label: "ADD TO WALLET", value: 1 },
  { label: "REDEEM BALANCE", value: 2 },
  { label: "PAY ENTRY FEE", value: 3 },
  { label: "RECEIVE WINNINGS", value: 4 },
  { label: "WINNINGS SEIZED", value: 5 },
  { label: "WALLET BALANCE SEIZED", value: 6 },
  { label: "REFUND", value: 7 },
  { label: "ON HOLD", value: 8 },
  { label: "RECEIVE REFERRAL", value: 9 },
  { label: "RECEIVE BONUS", value: 10 },
  { label: "VOLUNTEER", value: 11 },
  { label: "INACTIVITY CHARGES", value: 12 },
];

export default PaymentConstantTypes;
```

---

## Constant Details 📊

Each object in the `PaymentConstantTypes` array represents a specific payment action or event. Here's a detailed look at each one:

| **Label**                 | **Value** | **Description**                                    |
|---------------------------|-----------|----------------------------------------------------|
| **ADD TO WALLET**         | 1         | 📥 Adding funds to the wallet.                     |
| **REDEEM BALANCE**        | 2         | 💳 Redeeming an available balance.                 |
| **PAY ENTRY FEE**         | 3         | 💸 Paying an entry fee for an event or service.    |
| **RECEIVE WINNINGS**      | 4         | 🎉 Receiving winnings from a competition or event. |
| **WINNINGS SEIZED**       | 5         | 🚫 Winnings being seized due to some conditions.   |
| **WALLET BALANCE SEIZED** | 6         | 🚫 Wallet balance being seized.                    |
| **REFUND**                | 7         | 🔄 Issuing a refund.                               |
| **ON HOLD**               | 8         | ⏳ Payment is on hold pending further action.      |
| **RECEIVE REFERRAL**      | 9         | 🤝 Receiving a referral bonus.                     |
| **RECEIVE BONUS**         | 10        | 🎁 Receiving a bonus.                              |
| **VOLUNTEER**             | 11        | 🙋 Volunteering without monetary compensation.     |
| **INACTIVITY CHARGES**    | 12        | 💤 Charges due to account inactivity.              |

---

## Usage 🚀

To use these constants in your application, simply import the `PaymentConstantTypes` array where needed. This can help streamline handling different payment-related processes by referring to these predefined labels and values.

```javascript
import PaymentConstantTypes from './paymentConstantTypes';

// Example: Use a payment type
const paymentAction = PaymentConstantTypes.find(type => type.label === "ADD TO WALLET");
console.log(paymentAction.value); // Output: 1
```

This allows you to manage and reference payment actions programmatically with consistent, readable terms.

---

## Conclusion 🎯

The `paymentConstantTypes.js` file serves as an organized and efficient way to manage various payment-related constants in your application. By using these predefined labels and values, developers can ensure clarity and consistency across different components and modules that deal with payments.

For further details or to contribute, please refer to the main project repository. Happy coding! 🚀

---

By understanding and utilizing the `paymentConstantTypes.js` file effectively, you can maintain a clean, organized approach to managing payment actions within your application.

# 📊 Reports Table Constant Documentation

This documentation provides a comprehensive overview of the `reportsTableConstant.js` file, which is a critical part of managing and displaying report data in a tabular format. The file defines the structure and headers for multiple types of reports such as transactions, users, lobbies, and complaints. Each report type is tailored with specific fields to meet the requirements of different data analyses.

---

## 📑 Index

1. [Overview](#overview)
2. [Report Types](#report-types)
   - [Transactions History](#transactions-history)
   - [Users](#users)
   - [Lobbies](#lobbies)
   - [Complaints](#complaints)
3. [Table Header Descriptions](#table-header-descriptions)

---

## Overview

The `reportsTableConstant.js` file is primarily used to define the structure and headers of various tabular reports. It exports a constant array, `reportsTableConstant`, where each object represents a different report type. Each report type contains metadata about the report's structure, including:

- **Type**: A numerical identifier for the report type.
- **Heading**: A descriptive title for the report.
- **Table Headers**: An array of objects that define the columns of the table. Each object contains:
  - **Label**: The display name of the column.
  - **Key**: The key used to access the data for this column.
  - **Type**: (Optional) The data type of the column (e.g., date).
  - **Units**: (Optional) The unit of measure for numerical data (e.g., $, %).

---

## Report Types

### 1. Transactions History

**Type**: `1`

**Heading**: "Transactions History"

**Description**: This report provides detailed information on all financial transactions. It includes columns for dates, amounts, transaction types, fees, and payment methods.

**Table Headers**:
- Date
- Transaction ID
- Transaction Type
- Transaction Amount
- Transaction Fee
- Payment Method
- Lobby Name
- Name Of The Game
- Email
- Ryvals Share

---

### 2. Users

**Type**: `2`

**Heading**: "Users"

**Description**: This report focuses on user data, particularly their registration and referral information.

**Table Headers**:
- Players' Email
- Referred By Email
- Referral Code
- Registered On

---

### 3. Lobbies

**Type**: `3`

**Heading**: "Lobbies"

**Description**: Provides information about game lobbies, including their creation and start dates, entry fees, and player statistics.

**Table Headers**:
- Lobby Name
- Game Name
- Lobby Created Date
- Lobby Start Date
- Entry Fee
- Enrolled Players
- Total Enrollment Money
- Players' Played Game
- Total Kills
- Total Winning Amount

---

### 4. Complaints

**Type**: `4`

**Heading**: "Complaints"

**Description**: This report details user complaints, including information about the complainant and the subject of the complaint.

**Table Headers**:
- Lobby Name
- Game
- Complaint By
- Complaint By Email
- Complaint Against
- Complaint Against Email
- Date of Match

---

## Table Header Descriptions

Below is a detailed description of some of the key attributes found in the table headers:

| **Attribute**      | **Description**                                           |
|--------------------|-----------------------------------------------------------|
| **Label**          | The name displayed in the table header.                   |
| **Key**            | The data key used to retrieve corresponding data.         |
| **Type**           | Specifies the data type like "date" for date formatting.  |
| **Units**          | Specifies the unit for numerical data, e.g. "$" for money.|

---

This comprehensive setup allows for a systematic and organized approach to handling various report types, ensuring that the data is presented in a clear and structured format for analysis and decision-making.

# Documentation for `reportCardsConstant.js`

## 📜 Overview

The `reportCardsConstant.js` file is designed to define constants for generating report cards for a system that tracks various financial and user metrics related to players, lobbies, and complaints. This data is crucial for presenting management and stakeholders with clear insights into different operational aspects, including financial transactions, user engagement, and complaint resolutions.

### 🗂️ Index

1. [Structure of `reportCardsConstant`](#structure-of-reportcardsconstant)
2. [Detailed Explanation](#detailed-explanation)
   - [Type 1: Financial Metrics](#type-1-financial-metrics)
   - [Type 2: User Metrics](#type-2-user-metrics)
   - [Type 3: Lobby Metrics](#type-3-lobby-metrics)
   - [Type 4: Complaint Metrics](#type-4-complaint-metrics)
3. [Code Example](#code-example)

---

## Structure of `reportCardsConstant`

The `reportCardsConstant` is an array of objects where each object contains:

- **type**: A number representing the category of the report card.
- **cardLabels**: An array of objects, each representing a specific metric with the following properties:
  - **units** (optional): The unit of measurement, e.g., `$`.
  - **label**: A descriptive name for the metric.
  - **key**: A unique identifier key used to retrieve the corresponding data.
  - **tileKey**: A unique identifier for the tile position in the UI.

---

## Detailed Explanation

### Type 1: Financial Metrics

This category covers financial transactions and balances related to players' activity on the platform.

| Label                                | Description                                      | Key                                | Units |
|--------------------------------------|--------------------------------------------------|------------------------------------|-------|
| Players' Deposit Amount              | Total money deposited by players.                | `money_deposit_to_walltes`         | $     |
| Players' Withdrawn Amount            | Total money withdrawn by players.                | `money_transferred_from_walltes`   | $     |
| Amount Distributed in Players' Wallet| Total distributed money to players' wallets.     | `total_distributed_money`          | $     |
| Ryvals Fee paid by Players'          | Fees collected by the platform from players.     | `fees_paid_to_ryvals`              | $     |
| Seized Wallet Amount                 | Money seized from players' wallets.              | `seized_wallet_money`              | $     |
| Winning Amount Distributed           | Total winnings distributed to players.           | `winning_amount_distributed`       | $     |
| Referral Amount Distributed          | Money distributed through referral programs.     | `referral_amount_distributed`      | $     |
| Unclaimed Money                      | Money that has not been claimed by players.      | `unclaimed_money`                  | $     |
| Seized Winning Money                 | Winnings seized by the platform.                 | `seized_winning_money`             | $     |
| Dormant Money                        | Money from inactive players.                     | `dormant_money`                    | $     |
| Inactivity Charges                   | Fees charged for player inactivity.              | `inactivity_charges`               | $     |

### Type 2: User Metrics

This category tracks user engagement and acquisition metrics.

| Label                                    | Description                                      | Key                 |
|------------------------------------------|--------------------------------------------------|---------------------|
| Total Users                              | Total number of registered users.                | `total_users`       |
| New users signed up on website           | New users who signed up on the website.          | `recent_user`       |
| Users signed up through referrals        | New users who signed up via referral links.      | `referrals`         |

### Type 3: Lobby Metrics

This category monitors the various states and activities related to lobbies.

| Label                        | Description                                            | Key                        |
|------------------------------|--------------------------------------------------------|----------------------------|
| Total Created lobbies        | Total number of created lobbies.                       | `total_created_lobbies_count` |
| Played lobbies               | Number of lobbies where games have been played.        | `played_lobbies_count`     |
| Cancelled lobbies            | Number of lobbies that were cancelled.                 | `cancelled_lobbies_count`  |
| Refunded lobbies             | Number of lobbies that were refunded.                  | `refunded_lobbies_count`   |
| Upcoming lobbies             | Lobbies scheduled to start in the future.              | `upcoming_lobbies_count`   |
| Running lobbies              | Currently active lobbies.                              | `active_lobbies_count`     |
| Paid lobbies                 | Lobbies that require payment to enter.                 | `paid_lobbies_count`       |
| Free lobbies                 | Lobbies that are free to enter.                        | `free_lobbies_count`       |

### Type 4: Complaint Metrics

This category evaluates the handling and resolution of user complaints.

| Label                     | Description                                      | Key                |
|---------------------------|--------------------------------------------------|--------------------|
| Total complaints received | Total number of complaints received.             | `total_cmp`        |
| Resolved complaints       | Number of complaints that have been resolved.    | `resolved_cmp`     |
| Unresolved complaints     | Number of complaints that are still unresolved.  | `unresolved_cmp`   |

---

## Code Example

Here is a snippet of the code defining `reportCardsConstant`:

```javascript
export const reportCardsConstant = [
  {
    type: 1,
    cardLabels: [
      { units: "$", label: "Players' Deposit Amount", key: "money_deposit_to_walltes", tileKey: 1 },
      { units: "$", label: "Players' Withdrawn Amount", key: "money_transferred_from_walltes", tileKey: 2 },
      { units: "$", label: "Amount Distributed in Players' Wallet", key: "total_distributed_money", tileKey: 3 },
      { units: "$", label: "Ryvals Fee paid by Players'", key: "fees_paid_to_ryvals", tileKey: 4 },
      { units: "$", label: "Seized Wallet Amount", key: "seized_wallet_money", tileKey: 5 },
      { units: "$", label: "Winning Amount Distributed", key: "winning_amount_distributed", tileKey: 6 },
      { units: "$", label: "Referral Amount Distributed", key: "referral_amount_distributed", tileKey: 7 },
      { units: "$", label: "Unclaimed Money", key: "unclaimed_money", tileKey: 8 },
      { units: "$", label: "Seized Winning Money", key: "seized_winning_money", tileKey: 10 },
      { units: "$", label: "Dormant Money", key: "dormant_money", tileKey: 11 },
      { units: "$", label: "Inactivity Charges", key: "inactivity_charges", tileKey: 12 },
    ],
  },
  {
    type: 2,
    cardLabels: [
      { label: "Total Users", key: "total_users", tileKey: 1 },
      { label: "New users signed up on website ", key: "recent_user", tileKey: 2 },
      { label: "Users signed up through referrals", key: "referrals", tileKey: 3 },
    ],
  },
  {
    type: 3,
    cardLabels: [
      { label: "Total Created lobbies", key: "total_created_lobbies_count", tileKey: 1 },
      { label: "Played lobbies", key: "played_lobbies_count", tileKey: 2 },
      { label: "Cancelled lobbies", key: "cancelled_lobbies_count", tileKey: 3 },
      { label: "Refunded lobbies ", key: "refunded_lobbies_count", tileKey: 4 },
      { label: "Upcoming lobbies", key: "upcoming_lobbies_count", tileKey: 5 },
      { label: "Running lobbies", key: "active_lobbies_count", tileKey: 6 },
      { label: "Paid lobbies", key: "paid_lobbies_count", tileKey: 8 },
      { label: "Free lobbies", key: "free_lobbies_count", tileKey: 7 },
    ],
  },
  {
    type: 4,
    cardLabels: [
      { label: "Total complaints received", key: "total_cmp", tileKey: 1 },
      { label: "Resolved complaints", key: "resolved_cmp", tileKey: 2 },
      { label: "Unresolved complaints", key: "unresolved_cmp", tileKey: 3 },
    ],
  },
];
```

---

By using this file, the system can dynamically generate metrics and insights across various aspects of the platform, ensuring a comprehensive overview for stakeholders.