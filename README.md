# Amsterdam Airbnb Market Performance & Revenue Intelligence Dashboard

**Data Visualization & Analytics Capstone Project**

---

![Dashboard Preview](dashboard-preview.png)

---

[![Live Dashboard](https://img.shields.io/badge/Live%20Dashboard-Google%20Sheets-34A853?style=for-the-badge)](https://docs.google.com/spreadsheets/d/1OnKfcSwHCBstFBXLfjOazdt8lVIazn-axE1gQH8vMg8/edit?usp=sharing)

---

## Project Overview

This project presents a structured, data-driven analysis of **10,361 Airbnb listings** in Amsterdam across **20+ neighbourhoods**, built as part of the Data Visualization & Analytics capstone at Newton School of Technology.

The objective was to identify:

- Key drivers of occupancy
- Revenue performance patterns
- Pricing optimisation opportunities
- Neighbourhood-level revenue concentration

The final output is an **interactive Revenue Intelligence Dashboard** built in Google Sheets using pivot tables, calculated fields, and dynamic filters.

---

## Problem Statement

Amsterdam's Airbnb market is large, fragmented, and highly competitive. Hosts and marketplace operators often lack clear, data-driven visibility into how pricing decisions affect occupancy, revenue, and overall performance. This leads to common but costly problems:

- **Mispriced listings** — hosts either price too high and sit vacant, or price too low and leave revenue on the table
- **Uneven occupancy** — no structured understanding of which price bands or room types consistently attract bookings
- **Neighbourhood blind spots** — revenue is concentrated in a few districts, yet peripheral hosts apply the same pricing strategies without accounting for local demand differences
- **No performance benchmarks** — without a KPI framework, hosts cannot measure how their listing compares to market averages

This project addresses these gaps by building a revenue intelligence framework that translates raw listing data into actionable pricing and occupancy insights — helping hosts make smarter decisions and helping marketplace operators identify structural inefficiencies across the Amsterdam market.

---

## Business Objective

To design a **KPI-driven analytical framework** that helps:

- Optimise pricing strategies
- Improve occupancy rates
- Identify high-performing neighbourhoods
- Reduce vacancy and pricing inefficiencies

---

## Dataset Information

| Attribute | Details |
|---|---|
| **Source** | [Inside Airbnb](https://insideairbnb.com/get-the-data/) |
| **Total Listings** | 10,361 |
| **Neighbourhoods** | 20+ |
| **Room Types** | 4 |
| **Currency** | EUR |

**Key Fields Used:** Listing ID · Host ID · Room Type · Neighbourhood · Price (EUR) · Days Available · Licence Status

---

## Data Cleaning & Preparation

All data cleaning was performed entirely in **Google Sheets**.

| Step | Description |
|---|---|
| ID Formatting | Converted scientific notation IDs to plain text |
| Price Cleaning | Removed EUR symbols and commas from price fields |
| Neighbourhood Standardisation | Unified inconsistent neighbourhood naming |
| Host Classification | Classified hosts as **Professional** / **Private** |
| Missing Price Imputation | Grouped median by Neighbourhood x Room Type |
| Anomaly Flagging | Flagged 0-availability records (artificial 100% occupancy) |

> **Note:** Median imputation was chosen due to right-skewed pricing distribution.

---

## Feature Engineering

Three derived metrics were created to power the dashboard:

**1. Occupancy Rate**
```
Occupancy Rate = (365 - Days Available) / 365
```

**2. Estimated Annual Revenue**
```
Estimated Annual Revenue = Price x (365 - Days Available)
```

**3. Price Band Segmentation**

| Price Range (EUR) | Segment |
|---|---|
| 0 – 100 | Budget |
| 100 – 200 | Economy |
| 200 – 300 | Mid-Range |
| 300 – 500 | Upper Mid-Range |
| 500+ | Premium |

---

## KPI Framework

The dashboard tracks the following KPIs, all generated via pivot table aggregations:

- Average Price
- Average Occupancy Rate
- Average Estimated Revenue
- Total Estimated Revenue
- Revenue per Listing
- Count of Listings

---

## Key Insights

### Price Band Performance

| Price Range (EUR) | Avg. Occupancy |
|---|---|
| 0 – 100 | 63% |
| 100 – 200 | 69% |
| **200 – 300** | **84% — Highest** |
| 300 – 500 | 67% |
| 500+ | 44% |

> The EUR 200–300 segment achieves the highest occupancy, indicating strong value-perception alignment in the market.

### Room Type Performance

- **Entire home/apartment** listings dominate revenue and occupancy (~78%)
- **Hotel rooms** show the lowest occupancy (~39%) despite commanding high prices
- **Private rooms** underperform compared to entire home listings

### Neighbourhood Revenue Concentration

- Revenue is geographically concentrated in a few high-demand districts
- Peripheral zones show lower occupancy and reduced pricing power
- Pricing strategies should vary meaningfully by neighbourhood tier

---

## Strategic Recommendations

| Finding | Recommendation | Expected Impact |
|---|---|---|
| EUR 200–300 band performs best | Encourage hosts toward this pricing zone | +10% occupancy |
| Hotel rooms underperform | Reposition or reprice inventory | +8% revenue |
| Premium EUR 500+ low demand | Implement dynamic pricing alerts | Reduced vacancy |
| Revenue concentrated in few zones | Neighbourhood-based pricing strategy | 5–12% uplift |
| 100% occupancy anomalies | Audit 0-availability listings | Data accuracy improvement |

---

## Dashboard Features

The [Google Sheets Dashboard](https://docs.google.com/spreadsheets/d/1OnKfcSwHCBstFBXLfjOazdt8lVIazn-axE1gQH8vMg8/edit?usp=sharing) includes:

- KPI summary cards
- Occupancy vs Room Type analysis
- Revenue distribution by room type
- Price band vs occupancy trends
- Revenue by neighbourhood
- Geographic revenue map
- Interactive filters (Room Type & Neighbourhood)

> **Google Sheet Name:** DVA_Capstone(G-7)

---

## Limitations

- No time-series data — this is a cross-sectional snapshot
- Revenue figures are estimated, not actual booking data
- No review rating or sentiment data available
- No external tourism demand indicators included
- Availability anomalies exist in some records

---

## Future Improvements

- Time-series demand forecasting (ARIMA / Prophet)
- Machine learning–based pricing optimisation
- Review sentiment analysis using NLP
- Dynamic demand modelling
- External tourism data integration

---

## Tech Stack

- Google Sheets
- Pivot Tables & Calculated Fields
- Dashboard Design & Layout
- Data Cleaning & Transformation

---

## Conclusion

This project delivers a **KPI-driven revenue intelligence framework** for Amsterdam's Airbnb market.

> **Strongest Insight:** Listings priced between **EUR 200–300** achieve the highest occupancy (**~84%**), making this the most strategically optimal pricing band for hosts.

The dashboard is reusable, scalable, and designed to support data-driven pricing and marketplace optimisation decisions.

---

## Quick Links

| Resource | Link |
|---|---|
| Live Dashboard | [Google Sheets – DVA_Capstone(G-7)](https://docs.google.com/spreadsheets/d/1OnKfcSwHCBstFBXLfjOazdt8lVIazn-axE1gQH8vMg8/edit?usp=sharing) |
| Dataset | [Inside Airbnb – Amsterdam](https://insideairbnb.com/get-the-data/) |

---
