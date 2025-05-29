# 📊 ToppersNotes Audit Session Analysis Dashboard

This Power BI dashboard is designed to monitor and audit stock management activity related to **ToppersNotes** products. It provides real-time insights into stock adjustments, user operations, and anomalies in inventory sessions.

---

## 📌 Purpose

The dashboard helps:
- Track day-wise stock changes and trends
- Identify discrepancies between original and final stock
- Audit entries made by users
- Analyze specific book activity (e.g., Reasoning, English, etc.)
- Detect anomalies or suspicious stock modifications

---

## 📂 Data Sources

Assumes a dataset with the following fields (example):

- `Book`: Title of the book
- `Barcode`: Unique identifier
- `User`: Who made the stock entry
- `Date`: Timestamp of entry
- `Stock`: Final stock value
- `OriginalStock`: Expected or initial stock value
- `Difference`: Calculated field (Stock - OriginalStock)

---

## 📈 Key Features

### 📊 KPI Cards
- **Sum of Difference**: Total stock deviation
- **Sum of Stock**: Final stock count
- **Number of Entries by Users**: Total logs submitted
- **Number of Entries of Particular Book**: Activity level of selected book

### 📋 Visuals
- **Pie Chart**: Distribution of stock by book category
- **Time-Series Charts**:
  - Sum of Stock by Day
  - Sum of Original Stock by Day
  - Sum of Difference by Day

### 🧰 Slicers / Filters
- `Date`
- `User`
- `Barcode`
- `Book`

---

## ⚙️ DAX Measures

```dax
Difference = [Stock] - [OriginalStock]

Number of Entries by Users = COUNTROWS('TableName')

Number of Entries of Particular Book = 
CALCULATE(
    COUNTROWS('TableName'),
    ALLEXCEPT('TableName', 'TableName'[Book])
)
