# Pivot Table Calculations — Method & Working

This document explains how calculations were performed using Pivot Tables and how each metric shown in the dashboard is derived from the cleaned Amsterdam Airbnb dataset.

---

## 1. Source Data (Input Fields)

The pivot tables use the following prepared columns from the cleaned dataset:

- **ID**: Unique listing identifier (used for counting listings)
- **Price**: Nightly price (cleaned and standardized)
- **Room Type**: Listing room category
- **Neighbourhood**: Area in which the listing is located
- **Occupancy Rate**: Calculated field  
  \[
  \text{Occupancy Rate} = \frac{365 - \text{Days Available Per Year}}{365}
  \]
- **Estimated Revenue**: Calculated field  
  \[
  \text{Estimated Revenue} = \text{Price} \times (365 - \text{Days Available Per Year})
  \]
- **Price Range**: Helper category created from `Price` (e.g. `€0–€100`, `€100–€200`, …)

These fields come directly from the **Cleaned Dataset** after all data quality checks and feature engineering.

---

## 2. Pivot Table Aggregation Logic

Pivot Tables summarize the dataset using standard aggregation functions.

### 2.1 COUNT

**Purpose**: Measure supply (number of listings).

- **COUNT of ID**

Used in:
- **Total Listings** KPI
- **Listings by Room Type**
- **Listings by Neighbourhood**
- **Listings by Price Range**

### 2.2 AVERAGE

**Purpose**: Understand typical (average) performance.

- **AVERAGE of Price**
- **AVERAGE of Occupancy Rate**
- **AVERAGE of Estimated Revenue**

Used in:
- Average price comparisons across neighbourhoods and room types
- Occupancy rate comparisons
- Revenue performance analysis

### 2.3 SUM

**Purpose**: Calculate total market revenue.

- **SUM of Estimated Revenue**

Used in:
- Total revenue by neighbourhood
- Overall revenue contribution by segment

---

## 3. Pivot Table Structures

### 3.1 Neighbourhood Performance Pivot

- **Rows**
  - Neighbourhood
- **Values**
  - AVERAGE of Price
  - COUNT of ID
  - AVERAGE of Estimated Revenue
  - AVERAGE of Occupancy Rate

**Purpose**:
- Compare pricing, occupancy, and revenue performance across neighbourhoods.
- Identify high-demand and high-revenue areas.

---

### 3.2 Room Type Performance Pivot

- **Rows**
  - Room Type
- **Values**
  - AVERAGE of Price
  - COUNT of ID
  - AVERAGE of Occupancy Rate
  - AVERAGE of Estimated Revenue

**Purpose**:
- Compare performance between different room categories (e.g. Entire home, Private room).
- Understand how room type impacts price, occupancy, and revenue.

---

### 3.3 Price vs Occupancy Pivot

- **Rows**
  - Price Range
- **Values**
  - COUNT of ID
  - AVERAGE of Occupancy Rate

**Purpose**:
- Analyze how different price bands affect occupancy.
- Check whether lower-priced listings actually achieve higher occupancy and how demand changes by price segment.

---

### 3.4 Revenue by Neighbourhood Pivot

- **Rows**
  - Neighbourhood
- **Values**
  - AVERAGE of Estimated Revenue
  - SUM of Estimated Revenue
  - COUNT of ID

**Purpose**:
- Identify which neighbourhoods generate the highest **average** and **total** revenue.
- Combine supply (COUNT of ID) with revenue metrics to understand contribution by area.

---

## 4. KPI Card Calculations (Pivot-Based)

KPI cards in the dashboard are directly linked to Pivot Table outputs.

Examples:

- **Total Listings**  
  - Based on: `COUNT of ID (Grand Total)`
- **Average Price**  
  - Based on: `AVERAGE of Price`
- **Average Occupancy Rate**  
  - Based on: `AVERAGE of Occupancy Rate`
- **Average / Total Estimated Revenue**  
  - Based on: `AVERAGE of Estimated Revenue` or `SUM of Estimated Revenue` depending on the KPI

Because KPI cards reference Pivot values:

- They automatically update when filters or slicers are changed.
- They always stay synchronized with the underlying dataset and Pivot logic.

---

## 5. Filtering and Dynamic Updates

Slicers are connected to the Pivot Tables to allow interactive filtering:

- **Room Type**
- **Neighbourhood**
- (Optionally) **Price Range** or other categorical dimensions

When a slicer is applied:

- Pivot Table values recalculate automatically.
- All connected charts and KPI cards refresh based on the filtered subset.

This makes the dashboard fully dynamic and suitable for exploring:

- Performance by specific neighbourhood
- Differences between room types
- Behaviour of different price segments

---

## Summary

- All Pivot Table metrics are built on top of the **cleaned and engineered dataset**.
- Standard aggregation functions (**COUNT**, **AVERAGE**, **SUM**) are used consistently.
- Separate Pivot structures are designed for **Neighbourhood**, **Room Type**, **Price Range**, and **Revenue** analysis.
- KPI cards read directly from Pivot outputs, ensuring accurate and always up-to-date indicators for decision-making.

