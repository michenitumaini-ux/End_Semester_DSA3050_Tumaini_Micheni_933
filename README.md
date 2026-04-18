# DSA 3050A End Semester Exam

## Student Information
- **Name:** Tumaini Micheni
- **Admission Number:** 668933
- **Course Code:** DSA 3050A

## Project Overview
A comprehensive Power BI healthcare analytics solution built to analyze 
patient admissions, billing trends, medical conditions, and provider 
performance across a hospital network.

## Problem Statement
Hospital administrators lack real-time visibility into patient flow, 
billing performance, and medical condition trends. This solution provides 
an interactive dashboard to support data-driven decisions.

## Dataset Description
- Source: Kaggle (prasad22/healthcare-dataset)
- Size: 55,500+ rows
- Fields: 15 columns including patient demographics, admission details, 
  billing, and medical information

## Tools Used
- Power BI Desktop
- Power Query (M Language)
- DAX (Data Analysis Expressions)
- GitHub

## Steps Followed
1. Data acquisition from Kaggle
2. Data loading and transformation in Power Query
3. Star schema data modeling
4. DAX measure creation
5. Dashboard design (3 pages)
6. Insight generation and recommendations

## Dashboard Features
- Executive Summary with KPI cards and trend analysis
- Detailed Analysis with drill-down and matrix views
- Performance Monitoring with time intelligence and rankings

## Key DAX Measures
- Total Billing, Avg Billing, Total Patients
- YTD Billing, PY Billing, Billing Growth %
- Avg Length of Stay, Condition Rank

## Key Insights
1. Billing concentrated in high-cost conditions
2. Emergency admissions drive higher costs
3. Seasonal admission peaks in mid-year
4. Seniors form largest patient segment
5. Weak correlation between length of stay and billing

## Challenges Encountered
- Splitting a flat CSV into a relational star schema
- Creating time intelligence with a custom Date table
- Designing cross-filtering interactions across 3 report pages

## Conclusion
This solution demonstrates an end-to-end Power BI analytics workflow 
from raw data to actionable business insights in the healthcare domain.
