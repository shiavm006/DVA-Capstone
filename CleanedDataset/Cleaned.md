# Amsterdam Airbnb – Data Cleaning & Transformation Report

This document outlines the systematic data cleaning, transformation, and feature engineering performed on the Amsterdam Airbnb dataset.

The objective of this process was to:

- Ensure data integrity
- Standardize categorical values
- Handle missing values appropriately
- Create performance-driven calculated metrics
- Prepare structured aggregations for dashboard development

## 1. Data Cleaning Log

| Column Name | Status | Cleaning Reason & Action Taken |
|-------------|--------|--------------------------------|
| ID / Host ID | Cleaned | Converted from scientific notation to plain text to prevent Google Sheets rounding 18-digit IDs and maintain uniqueness. |
| Listing Title | Cleaned | Standardized casing to Proper Case. Replaced abbreviations (e.g., "Ap.", "Apt") with "Apartment". Removed slashes and emojis for better readability. |
| Host Name | Cleaned | Standardized separators for multi-host listings ("And", "En", "/") → "&". Categorized hosts as Professional or Private based on business-related keywords. |
| Neighbourhood | Cleaned | Split compound names (e.g., "Centrum-West") into Primary Area and Sub-Area. Filled missing values using geographic inference from listing titles. |
| Price | Cleaned | Removed currency symbols (€) and commas. Standardized #N/A values to 0 using IFNA. |
| Price (Missing Values) | Imputed | Missing prices replaced using Median Price based on Neighbourhood + Room Type to maintain pricing realism and reduce skewness impact. |
| License | Cleaned | Removed extra spaces for deduplication. Standardized entries like "Exempt" and "Not Provided". Filtered invalid placeholders (e.g., "ABCD 1234..."). |
| Listing Name | Cleaned | Fixed spacing between numbers and text ("50M2" → "50 M2"). Replaced "M2" with proper square meter symbol (M²). |

## 2. Data Quality Checks: Duplicates, Blanks, and Null Values

A comprehensive data quality audit was performed across all columns to identify and correct duplicates, blank cells, and null values.

### Duplicate Detection and Removal

**Process:**
- Checked all columns for duplicate records based on unique identifiers (ID, Host ID)
- Identified duplicate entries across multiple columns
- Removed exact duplicate rows to maintain data integrity
- Preserved the most complete record when partial duplicates were found

**Actions Taken:**
- Scanned entire dataset for duplicate IDs
- Removed complete duplicate rows
- Verified uniqueness of primary keys after cleaning

### Blank and Null Value Detection

**Process:**
- Systematically checked every cell in all columns for blank values
- Identified null values represented in various formats (empty cells, "NULL", "N/A", "#N/A")
- Categorized missing values by column type (numeric, text, categorical)

**Columns Checked:**
- ID / Host ID
- Listing Title
- Host Name
- Neighbourhood
- Price
- License
- Room Type
- Days Available Per Year
- All other dataset columns

**Correction Strategy:**
- **Numeric Columns:** Missing values replaced using median imputation (as detailed in Section 2)
- **Categorical Columns:** Missing values filled using mode or logical inference
- **Text Columns:** Blank values standardized to "Not Provided" or inferred from related columns
- **Geographic Data:** Missing neighbourhood values inferred from listing titles and descriptions

**Outcome:**
- All blank cells identified and addressed
- Null values standardized and corrected
- Data completeness improved across all columns
- No critical columns left with missing values that would impact analysis

### Data Completeness Summary

After cleaning:
- Duplicate records removed
- Blank cells filled or standardized
- Null values handled appropriately
- All columns validated for data quality
- Dataset ready for analysis and visualization

## 3. Handling Missing Values Strategy

### Why Median?

Instead of using mean:

- Median reduces impact of extreme luxury listings.
- More robust for skewed Airbnb pricing distributions.
- Calculated within each Neighbourhood and Room Type for realistic replacement.

Example grouping:

```
Median Price
→ Grouped by:
   - Neighbourhood
   - Room Type
```

This ensures:

- Budget areas stay budget
- Premium zones retain premium pricing behavior

## 4. Engineered Features (Calculated Columns)

To analyze commercial performance, the following features were created:

### A. Occupancy Rate

**Definition**

Occupancy Rate represents the percentage of days a listing is occupied in a year.

**Formula**

```
Occupancy Rate = (365 - Days Available Per Year) / 365
```

**Explanation**

- Days Available Per Year → Number of days listing is available
- 365 - Available Days → Occupied Days
- Output formatted as percentage (%)

**Purpose**

- Measures property demand
- Evaluates utilization efficiency
- Helps compare pricing vs popularity

### B. Estimated Yearly Revenue

**Definition**

Estimated yearly revenue is calculated based on nightly price and occupied days.

**Formula**

```
Estimated Revenue = Price × (365 - Days Available Per Year)
```

**Explanation**

- Price → Nightly listing price
- Occupied Days → 365 - Available Days
- Output formatted as € (Currency)

**Purpose**

- Financial benchmarking
- Identifies high-performing listings
- Determines profitable neighborhoods

### C. Price Range (Helper Column)

A helper column was created to group listings into pricing segments.

**Formula Used (Google Sheets)**

```
=IF(G2<100,"€0 - €100",
IF(G2<200,"€100 - €200",
IF(G2<300,"€200 - €300",
IF(G2<500,"€300 - €500","€500+"))))
```

**Output Categories**

- €0 – €100
- €100 – €200
- €200 – €300
- €300 – €500
- €500+

**Purpose**

Used to analyze:

- Occupancy Rate vs Pricing Strategy
- Demand elasticity across price segments
- Revenue distribution by category

## 5. Data Aggregations for Dashboard

After feature engineering, Pivot Tables were used to generate Key Performance Indicators (KPIs).

### Aggregations Used

| Metric | Aggregation Type | Business Insight |
|--------|------------------|------------------|
| Average Price | Average | District-level cost comparison |
| Count of Listings (ID) | Count | Supply density by area |
| Average Occupancy Rate | Average | Popularity vs pricing efficiency |
| Average Estimated Revenue | Average | Average earning per listing |
| Total Estimated Revenue | Sum | Total revenue contribution by zone |

## 6. Dashboard Impact

These transformations power:

- KPI Cards
- Revenue Distribution Charts
- Price vs Occupancy Comparisons
- Neighborhood Performance Heatmaps
- Profitability Ranking Tables

## Final Outcome

- Cleaned and standardized dataset
- Missing values handled using statistically sound approach
- Performance-driven calculated metrics created
- Dashboard-ready aggregated data
- Business insights aligned with strategic pricing decisions

## Project Objective Achieved

The Amsterdam Airbnb dataset is now:

- Reliable
- Structured
- Financially analyzable
- Ready for visualization
- Suitable for business decision-making
