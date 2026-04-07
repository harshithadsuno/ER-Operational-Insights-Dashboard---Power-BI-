# ER Operational Insights Dashboard

**File:** `ER_Operational_Insights_Dashboard.pbix`  
**Tool:** Microsoft Power BI Desktop (version 2.152.856.0 or later)   

---

## Overview

This Power BI report provides operational analytics for a hospital emergency room (ER). It tracks patient volume, wait times, satisfaction scores, referral patterns, and demographic breakdowns. The data is structured to support both granular month-level analysis and high-level consolidated views across a date range.

This dashboard focuses on **hospital ER operational metrics** — patient flow, admission status, staffing patterns by day/hour, and departmental referrals.

---

## Data Sources

The report is built on two tables:

| Table | Description |
|---|---|
| `Hospital ER_Data` | Core fact table containing one row per patient visit, with fields for demographics, wait time, satisfaction score, admission status, and referral |
| `Date Table` | Calendar/time dimension with date, day name, month, month & year, and year fields for time-intelligence filtering |

The report connects to a remote Power BI dataset (`DatasetId: d1aa60f8-f46b-4d03-b437-db9b1a6654b4`) hosted in the Power BI service.

### Key Fields in `Hospital ER_Data`

| Field | Type | Description |
|---|---|---|
| `Patient Id` | Text | Unique patient identifier |
| `Patient Full Name` | Text | Patient name |
| `Patient Gender` | Text | Gender |
| `Patient Age` | Numeric | Age in years |
| `Patient Race` | Text | Race/ethnicity |
| `Patient Waittime` | Numeric | Wait time in minutes |
| `Patient Satisfaction Score` | Numeric | Satisfaction rating |
| `Admission Status` | Text | Admitted vs. not admitted |
| `Department Referral` | Text | Department the patient was referred to |
| `Waittime Status` | Text | Categorical bucket (e.g., seen within 30 mins or not) |
| `Waittime Interval` | Text | Finer interval grouping for heatmap |
| `Age Group` | Text | Age bracket (calculated) |
| `No of Patients` | Measure | Count of patients |
| `No of Patients Referred` | Measure | Count of referred patients |
| `Avg Wait Time` | Measure | Average wait time |

---

## Report Pages

### 1. Monthly View
Drill into a single selected month and year. Slicers let the user filter by **Year** and **Month**, with all visuals updating to reflect the chosen period.

**KPI Cards:**
- Total number of patients
- Average wait time
- Average patient satisfaction score
- Number of patients referred

**Trend Charts (area charts by day of month):**
- Daily patient volume
- Daily satisfaction score trend
- Daily referral count
- Daily total wait time

**Breakdown Charts:**
- Patient admission status (pivot table + bar chart)
- Patients by age group (clustered column chart)
- Patients by department referral (clustered bar chart)
- % of patients seen within 30 minutes (donut chart)
- Patients by gender (donut chart)
- Patients by race (clustered bar chart)
- Patient count by day and hour — heatmap-style pivot table and column chart

---

### 2. Consolidated View
A full date-range view with a **date range slicer** spanning the entire dataset. All the same breakdown charts as the Monthly View are present, but trend charts are aggregated by **month** rather than by day, enabling multi-month comparison.

**Trend Charts (column charts by month):**
- Monthly patient volume
- Monthly average satisfaction score
- Monthly referral count
- Monthly average wait time

All other demographic and operational breakdowns mirror the Monthly View.

---

### 3. Patient Details
A record-level drill-through page. Filtered by a date range slicer, it presents a table showing:

- Patient ID
- Full Name
- Gender
- Age
- Race
- Wait Time (minutes)

Useful for audits, individual case review, or data validation.

---

### 4. Key Takeaways
A text-based summary/narrative page intended for stakeholder presentation. Contains contextual callouts and observations derived from the data (no interactive visuals).

---

## Navigation

All four pages share a **page navigator** menu (labelled "Menu") and three branding images in the header, providing consistent navigation across the report.

---

## How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
2. Open `HR_Operational_Insights_Dashboard.pbix`.
3. If prompted about a live connection, sign in with a Power BI account that has access to the source dataset, or import the data locally if the dataset has been exported separately.

> **Note:** Because this report references a remote Power BI Service dataset, visuals will not populate without an active connection to that dataset or a locally loaded data model.

---

## File Contents (internal structure)

| Component | Description |
|---|---|
| `Report/Layout` | All page layouts, visuals, and configurations |
| `DataModel` | Embedded data model (~600 KB) |
| `Report/StaticResources/` | Theme JSON and branding images (logo, GitHub icon) |
| `Connections` | Reference to remote Power BI dataset |
| `Settings` | Report-level query and relationship settings |
| `Metadata` | Authoring version and creation metadata |
