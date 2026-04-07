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
A narrative summary page for stakeholder presentation, covering the full 19-month dataset (April 2023 – October 2024) across 9,216 unique patients.

#### Patient Wait Time & Satisfaction
- Average wait time: **35.3 minutes** — flagged in the dashboard as needing improvement for better patient flow.
- Average satisfaction score: **4.99 / 10** — moderate, indicating meaningful room for improvement in patient experience.

#### Departmental Referrals
- **5,400 patients** required no referral and were handled directly by the ER.
- Top referral destinations among the remaining patients:
  - **General Practice** — 1,840 cases
  - **Orthopedics** — 995 cases
  - Physiotherapy — 276 cases
  - Cardiology — 248 cases

#### Peak Busy Periods
- Busiest days: **Monday (1,377)**, Saturday (1,322), Tuesday (1,318)
- Busiest hours: **11 AM, 7 PM, 1 PM, and 11 PM** — spanning both daytime peaks and late-night surges.

#### Patient Demographics
- **Age:** Adults aged 30–39 were the largest group (1,200 patients), followed closely by 20–29 year-olds (1,188). Middle-aged patients (40–50) were also a notable segment.
- **Gender:** Near-even split (tracked via donut chart across all pages).
- **Race:** White (2,571) · African American (1,951) · Multi-racial (1,557) · Asian (1,060) · Declined to identify (1,030).

#### Admission Patterns
- Nearly a 50/50 split: **4,612 admitted**, **4,604 treated and released** — indicating the ER is handling a very high proportion of cases that require inpatient care.

---

## Recommendations

Based on the Key Takeaways, the following improvements are worth highlighting to stakeholders:

**1. Reduce wait times below 30 minutes**
The 35.3-minute average is above the commonly cited 30-minute benchmark for ER triage. Consider triaging fast-track patients (non-urgent cases) into a separate queue to free up capacity for critical cases.

**2. Staff to peak hours, not just peak days**
The busiest hours — 11 AM, 7 PM, 1 PM, and 11 PM — straddle shift changes and late-night periods. Scheduling overlapping shifts or flex staff during these windows could directly cut wait times.

**3. Prioritise Monday and weekend readiness**
Mondays and Saturdays are consistently the busiest days. Pre-positioning additional staff and resources before these days (rather than reacting in real time) would reduce bottlenecks.

**4. Expand General Practice and Orthopedics capacity**
With General Practice (1,840) and Orthopedics (995) absorbing the bulk of referrals, ensuring those departments have adequate intake capacity will reduce downstream delays for ER patients waiting on referral disposition.

**5. Investigate the satisfaction score gap**
A 4.99/10 satisfaction average is a significant flag. Cross-referencing satisfaction scores with wait time intervals in the heatmap (Waittime Interval × Day Name) could identify whether the dissatisfaction is concentrated in specific time windows or demographics.

**6. Address the 50% admission rate**
An admission rate close to 50% is unusually high and suggests either a high-acuity patient population or potential over-admission. A clinical audit comparing admitted vs. released patients by age group and referral department could surface opportunities to improve triage decision-making.

**7. Improve race/ethnicity data completeness**
Over 1,000 patients (roughly 11%) declined to identify their race. Improving voluntary self-identification rates would give a more accurate picture for equity-focused care analysis.

---

## Navigation

All four pages share a **page navigator** menu (labelled "Menu") and three branding images in the header, providing consistent navigation across the report.

---

## How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
2. Open `HR_Operational_Insights_Dashboard.pbix`.
3. If prompted about a live connection, sign in with a Power BI account that has access to the source dataset, or import the data locally if the dataset has been exported separately.

> **Note:** Because this report references a remote Power BI Service dataset, visuals will not populate without an active connection to that dataset or a locally loaded data model.

