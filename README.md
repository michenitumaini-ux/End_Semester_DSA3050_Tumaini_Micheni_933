# DSA 3050A — Advanced Power BI Examination
## Healthcare Analytics Power BI Solution

**Student Name:** Tumaini Micheni
**Admission Number:** 668933
**Course Code:** DSA 3050A


## Project Overview

This project presents a complete end-to-end Business Intelligence solution built in Microsoft Power BI for the Healthcare Analytics domain. The solution transforms a raw flat-file dataset of 55,500+ hospital patient records into a structured, interactive, and insightful analytical dashboard designed to support executive decision-making in a hospital environment.

The project covers every stage of the BI development lifecycle — from raw data acquisition and cleaning, through relational data modeling and DAX measure creation, to a professionally designed three-page interactive dashboard. The solution gives hospital administrators visibility into patient admissions, billing performance, medical condition trends, and provider efficiency.

---

## Problem Statement

Hospital administrators and healthcare executives face persistent challenges in monitoring the operational and financial performance of their institutions. Key questions that often go unanswered without proper BI tooling include:

- Which medical conditions generate the highest billing burden on patients and the institution?
- How does admission volume fluctuate across months and years — are there predictable seasonal peaks?
- Which insurance providers account for the most and least revenue?
- Are there differences in billing and length of stay across admission types (Emergency, Elective, Urgent)?
- Which doctors and hospitals are carrying the highest patient loads?
- How do this year's billing figures compare to the previous year?

This Power BI solution addresses all of these questions through a structured star schema data model, calculated DAX measures, and an interactive three-page dashboard — enabling stakeholders to explore data dynamically and derive actionable business insights.

---

## Dataset Description

| Field | Details |
|---|---|
| **Source** | Kaggle — [prasad22/healthcare-dataset](https://www.kaggle.com/datasets/prasad22/healthcare-dataset) |
| **Nature** | Synthetic dataset simulating real-world hospital patient records |
| **Format** | Single CSV file — `healthcare_dataset.csv` |
| **Size** | 55,500+ rows, 15 columns |

### Fields

| Field | Data Type | Description |
|---|---|---|
| Name | Text | Patient full name |
| Age | Whole Number | Patient age at time of admission |
| Gender | Text | Male or Female |
| Blood Type | Text | e.g. A+, O-, B+ |
| Medical Condition | Text | Primary diagnosis (e.g. Diabetes, Cancer, Asthma) |
| Date of Admission | Date | Date the patient was admitted |
| Doctor | Text | Name of attending doctor |
| Hospital | Text | Hospital where patient was admitted |
| Insurance Provider | Text | e.g. Aetna, Medicare, Blue Cross, Cigna, UnitedHealthcare |
| Billing Amount | Decimal | Amount billed in USD for the admission |
| Room Number | Whole Number | Room assigned to the patient |
| Admission Type | Text | Emergency, Elective, or Urgent |
| Discharge Date | Date | Date the patient was discharged |
| Medication | Text | Medication prescribed during admission |
| Test Results | Text | Normal, Abnormal, or Inconclusive |

### Why This Dataset Was Chosen

- **Volume:** 55,500+ rows far exceeds the minimum 9,000-row requirement, ensuring statistically meaningful aggregations
- **Date fields:** Two date columns (Date of Admission and Discharge Date) support advanced time intelligence — YTD billing, period-over-period comparisons, and length-of-stay calculation
- **Relational potential:** The flat file is split into five logical tables (one fact table and four dimension tables) forming a proper star schema
- **Mixed variable types:** Both categorical (Gender, Admission Type, Medical Condition) and numerical variables (Age, Billing Amount) are present
- **Business richness:** Supports diverse KPIs including Total Billing, Avg Length of Stay, Patient Volume, Top Conditions by Cost, and Insurance Provider comparisons

---

## Tools Used

| Tool | Purpose |
|---|---|
| Microsoft Power BI Desktop | Data modeling, DAX calculations, dashboard design |
| Power Query (M Language) | Data cleaning, transformation, and star schema creation |
| DAX (Data Analysis Expressions) | Calculated measures and columns for analytical KPIs |
| Microsoft Excel | Initial data inspection of the raw CSV file |
| GitHub | Version control, file hosting, and project documentation |

---

## Steps Followed

### Step 1 — Data Acquisition
The dataset was downloaded from Kaggle in CSV format. It was first opened in Microsoft Excel to inspect the raw structure, confirm column headers, and understand data types before import into Power BI.

### Step 2 — Data Loading into Power BI
The CSV file was imported via **Home → Get Data → Text/CSV**. The **Transform Data** option was selected to open Power Query Editor before loading data into the model.

### Step 3 — Data Cleaning and Transformation in Power Query
The following transformation steps were applied:

1. **Changed data types** — Date of Admission and Discharge Date set to Date; Age and Room Number to Whole Number; Billing Amount to Decimal Number
2. **Removed duplicate rows** — to ensure data integrity across the main table
3. **Renamed columns** — for consistency and clarity across all queries
4. **Added Length of Stay column** — custom column using `Duration.Days([Discharge Date] - [Admission Date])`
5. **Added Age Group conditional column** — categorising patients as Paediatric, Young Adult, Middle Aged, or Senior
6. **Extracted Month Name and Year** — from the Admission Date column for time-based analysis
7. **Added Billing Category conditional column** — grouping billing amounts as Low (<10,000), Medium (10,000–30,000), or High (>30,000)
8. **Split into dimension tables** — Dim_Patients, Dim_Doctors, Dim_Medical, and Dim_Insurance — each with a unique ID index column and duplicates removed

### Step 4 — Data Modeling
A star schema was constructed in Model View with the following tables:

- **Fact_Admissions** — Central fact table containing all transactional records
- **Dim_Patients** — Patient demographics (Name, Age, Gender, Blood Type, Age Group)
- **Dim_Doctors** — Doctor and hospital information
- **Dim_Medical** — Medical condition, medication, and test results
- **Dim_Insurance** — Insurance provider dimension
- **Dim_Date** — Custom date table created via DAX `CALENDAR()` function with Year, Month, Quarter, and Day of Week columns

All relationships use **Many-to-One** cardinality from the fact table to each dimension.

### Step 5 — DAX Measures and Calculated Columns
A dedicated **Measures Table** was created to organise all DAX measures. Ten measures and two calculated columns were written covering total billing, averages, YTD calculations, period-over-period comparison, growth percentages, and rankings.

### Step 6 — Dashboard Design
Three report pages were designed: **Executive Summary**, **Detailed Analysis**, and **Performance Monitoring**. Each page features KPI cards, charts, slicers, and cross-filtering interactions with a consistent dark green and purple theme.

### Step 7 — Insight Generation
The completed dashboard was used to derive five analytical insights and three actionable business recommendations, documented in the accompanying PDF report.

---
All dimension tables connect to **Fact_Admissions** via Many-to-One relationships on their respective key fields. Cross-filter direction is set to Single on all relationships.

---

## Dashboard Features

### Page 1 — Executive Summary
- **KPI Cards:** Total Billing (1.40bn), Total Patients (55K), Average Billing (25.54K)
- **Donut Chart:** Total Patients by Admission Type (Elective / Emergency / Urgent)
- **Bar Chart:** Total Billing by Medical Condition
- **Slicers:** Admission Type, Year, Gender

### Page 2 — Detailed Analysis
- **Matrix Table:** Hospital vs Medical Condition with Total Billing values
- **Bar Chart:** Total Patients by Year (2019–2024)
- **Stacked Bar Chart:** Total Billing by Insurance Provider broken down by Billing Category
- **Slicers:** Insurance Provider, Test Results

### Page 3 — Performance Monitoring
- **Bar Chart:** Total Billing by Doctor — top performers ranked
- **Area Chart:** Billing Growth % by Year — period-over-period comparison
- **Bar Chart:** Total Patients by Medical Condition
- **100% Stacked Bar Chart:** Count of Medical Condition by Test Results
- **Slicers:** Month Name, Year range slider

---

## Key DAX Measures

```dax
-- 1. Total Billing
Total Billing = SUM(Fact_Admissions[Billing Amount])

-- 2. Average Billing
Avg Billing = AVERAGE(Fact_Admissions[Billing Amount])

-- 3. Total Patients
Total Patients = COUNTROWS(Fact_Admissions)

-- 4. Distinct Patients
Distinct Patients = DISTINCTCOUNT(Fact_Admissions[Name])

-- 5. Average Length of Stay
Avg Length of Stay = AVERAGE(Fact_Admissions[Length of Stay])

-- 6. Year-to-Date Billing
YTD Billing = TOTALYTD(SUM(Fact_Admissions[Billing Amount]), Dim_Date[Date])

-- 7. Previous Year Billing
PY Billing = CALCULATE(SUM(Fact_Admissions[Billing Amount]), SAMEPERIODLASTYEAR(Dim_Date[Date]))

-- 8. Billing Growth %
Billing Growth % = DIVIDE([Total Billing] - [PY Billing], [PY Billing], 0)

-- 9. Billing % by Condition
Billing % by Condition =
DIVIDE(
    SUM(Fact_Admissions[Billing Amount]),
    CALCULATE(SUM(Fact_Admissions[Billing Amount]), ALL(Fact_Admissions[Medical Condition])),
    0
)

-- 10. Condition Rank
Condition Rank =
RANKX(
    ALL(Fact_Admissions[Medical Condition]),
    [Total Billing],
    ,
    DESC,
    DENSE
)
```

### Calculated Columns

```dax
-- 1. Length of Stay (DAX version)
LOS Days = DATEDIFF(Fact_Admissions[Admission Date], Fact_Admissions[Discharge Date], DAY)

-- 2. Billing Category
Billing Category =
IF(Fact_Admissions[Billing Amount] < 10000, "Low",
IF(Fact_Admissions[Billing Amount] < 30000, "Medium", "High"))
```

---

## Key Insights

1. **Billing is concentrated in a small number of conditions** — Diabetes, Obesity, and Cancer consistently rank as the highest billing conditions, collectively accounting for the majority of total revenue across the hospital network.

2. **Emergency admissions incur higher average billing** — Patients admitted as emergencies generate higher average billing amounts than those admitted electively, reflecting the unplanned and resource-intensive nature of emergency care.

3. **Billing growth has turned negative** — The Billing Growth % measure shows -0.30 for the most recent period, indicating a year-over-year decline in total billing that warrants management investigation.

4. **Seasonal peaks in patient admissions** — Admission volumes show a notable increase during mid-year months, particularly between 2020 and 2022, suggesting seasonal demand patterns that hospitals should factor into staffing and resource planning.

5. **Senior patients form the largest age segment** — The Age Group breakdown shows that Senior patients (65+) represent approximately one-third of all admissions, creating sustained demand for geriatric care capabilities and longer average lengths of stay.

---

## Actionable Recommendations

1. **Invest in chronic disease management programs** — Since conditions like Diabetes, Hypertension, and Obesity drive the highest billing and admission volumes, proactive outpatient management could reduce costly emergency admissions and improve patient outcomes.

2. **Investigate and address the billing decline** — The negative billing growth trend should be examined urgently. Management should determine whether declining admissions, shorter stays, or billing inefficiencies are responsible and develop a corrective action plan.

3. **Develop dedicated geriatric care pathways** — With seniors forming a major and growing patient segment, establishing dedicated geriatric wards, streamlined discharge planning, and community support linkages would improve outcomes and reduce unnecessary length of stay.

---

## Challenges Encountered

- Splitting a single flat CSV file into a relational star schema required careful planning of which fields belonged to each dimension table while preserving join keys without data loss
- Creating time intelligence DAX measures (YTD, SAMEPERIODLASTYEAR) required a properly configured Dim_Date table with a continuous date range — this needed to be set up correctly before the measures would function
- Managing cross-filtering interactions across three report pages with multiple slicers required careful attention to filter context to avoid unexpected data exclusions
- Some column name conventions in the original dataset used inconsistent casing which required renaming steps in Power Query for clean, professional output

---

---

## Conclusion

This project demonstrates a complete and professional Power BI healthcare analytics solution — from raw CSV ingestion through to an interactive three-page dashboard delivering actionable business insights. The solution applies industry-standard data modeling practices (star schema), advanced DAX calculations including time intelligence, and structured dashboard design principles.

The findings reveal significant patterns in billing concentration, admission seasonality, and patient demographics that can directly inform hospital management decisions around resource allocation, financial planning, and quality of care. This solution is fully reproducible, professionally documented, and hosted on GitHub for transparency and academic integrity.

---
