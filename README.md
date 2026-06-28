# Student Lifestyle & Academic Performance Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset Description](#dataset-description)
- [Data Preparation & Engineered Columns](#data-preparation--engineered-columns)
- [Analysis Questions](#analysis-questions)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [Tools Used](#tools-used)
- [Analytical Skills Demonstrated](#analytical-skills-demonstrated)

---

## Project Overview

 <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/11717e24-9461-4602-9351-c7a3f8875301" />



This project explores the relationship between student lifestyle habits and 
academic performance using a synthetic dataset of 2,000 students. 
The central question driving the analysis is: **what lifestyle factors actually 
influence GPA, and by how much?**

The analysis challenges several common assumptions — that social activity 
destroys grades, that physical activity helps academic performance, and that 
balanced students are the highest achievers. The findings tell a more nuanced, 
and in several cases counterintuitive, story.

The dashboard was built entirely in Microsoft Excel using Power Query for data 
transformation, Pivot Tables for aggregation, and a fully interactive dashboard 
with slicers for dynamic filtering.

---

## Dataset Description

| Property | Detail |
|---|---|
| Source | Synthetic academic lifestyle dataset |
| Rows | 2,000 students |
| Original Columns | 8 |
| Missing Values | None |
| GPA Scale | 0.0 – 4.0 |

**Original Columns:**
- `Student_ID` — Unique identifier per student
- `Study_Hours_Per_Day` — Daily hours spent studying
- `Extracurricular_Hours_Per_Day` — Daily hours in extracurricular activities
- `Sleep_Hours_Per_Day` — Daily hours of sleep
- `Social_Hours_Per_Day` — Daily hours spent socialising
- `Physical_Activity_Hours_Per_Day` — Daily hours of physical exercise
- `GPA` — Grade Point Average (0.0 – 4.0 scale)
- `Stress_Level` — Categorical: High, Moderate, or Low

---

## Data Preparation & Engineered Columns

All data transformation was performed inside Power Query before loading to 
Excel. Four new columns were engineered from existing data to support deeper 
analysis:

### 1. `GPA_Category`
Bucketed the continuous GPA decimal into four performance tiers for 
categorical analysis:

| GPA Range | Category |
|---|---|
| 3.5 – 4.0 | High Performer |
| 3.0 – 3.49 | Above Average |
| 2.5 – 2.99 | Average |
| Below 2.5 | Below Average |

### 2. `Total_Productive_Hours`
Summed all activity hours per student to measure overall daily 
engagement:
`= Study_Hours + Extracurricular_Hours + Social_Hours + Physical_Activity_Hours`

### 3. `Activity_StdDev`
Calculated the standard deviation across each student's four lifestyle activity 
columns (Study, Social, Physical Activity, Extracurricular) using Power Query's 
`List.StandardDeviation()` function. This measures how evenly a student 
distributes their time — a low value indicates a balanced schedule, a high 
value indicates concentration in one activity.

### 4. `Balance_Profile`
Classified each student as `Balanced` or `Concentrated` based on their 
`Activity_StdDev` value against a threshold of 1.5 — representing students 
whose four activity hours typically vary by no more than 1.5 hours from their 
own personal average: `If Activity_StdDev ≤ 1.5 → Balanced
Otherwise → Concentrated`.

The threshold of 1.5 was chosen after validating the 25th percentile method 
(≤ 2.46) against actual row data and finding it produced distributions that 
were not genuinely even. A stricter absolute threshold of 1.5 was adopted to 
ensure "Balanced" described students with a truly fair spread of hours across 
activities.

### 5. `Study_Share_Pct`
Expressed study hours as a proportion of total productive hours per student:
`= Study_Hours / (Study + Social + Physical_Activity + Extracurricular)`.
This metric was used to quantify how dominant study is in the daily schedule 
of each stress group, directly testing whether high stress is caused by study 
intensity alone or by juggling multiple commitments simultaneously.

---

## Analysis Questions

This dashboard was built to answer these questions:

1. Which lifestyle factor has the strongest relationship with GPA?
2. Do students who study more actually get better GPAs?
3. Does physical activity help or hurt academic performance?
4. What is the stress profile of high-performing students?
5. Do socially active students sacrifice GPA?
6. Does the "balanced student" exist?
7. Study Hours as Share of Productive and its stress distribution. 


---

## Key Findings

### 1. Study Hours Is the Only Lifestyle Factor That Positively Drives GPA
Across all five lifestyle activities measured, only Study Hours produced a 
positive GPA impact. The GPA difference between the lowest and highest study 
hour bands was **+0.61 points** — by far the largest swing of any activity. 
Every other activity produced either a negative or negligible relationship 
with GPA.

<img width="576" height="244" alt="image" src="https://github.com/user-attachments/assets/f05354a1-5e46-4cce-866e-bced5c462dc7" />



### 2. The Study-GPA Relationship Is Consistent and Linear
GPA rose with every additional hour of study across the full range (5–10 hours 
per day), with no plateau, no threshold effect, and no band where additional 
study failed to add value. Average GPA climbed from **2.81 at 5–6 hrs** to 
**3.42 at 9–10 hrs** — a clean, unbroken progression.

### 3. Physical Activity Produces a Gradual, Marginal GPA Decline
More physical activity is associated with lower GPA, but the decline is slow 
and modest — a total drop of **−0.29 GPA points** across the full activity 
range. Critically, the decline flattens at higher activity levels (4–5 hrs and 
5–6 hrs produce almost identical GPAs), suggesting diminishing negative impact 
rather than a compounding penalty.

The most likely explanation is a time trade-off: every hour spent on physical 
activity is an hour not spent studying, and study hours are the primary GPA 
driver. Physical activity itself is not academically harmful — it competes 
for finite time.

### 4. High Stress Is a Feature of Top Academic Performance, Not a Barrier
**96.8% of High Performers (GPA ≥ 3.5) experience High Stress** — compared 
to 51.5% of all students. High Stress students also carry the highest average 
GPA across the entire dataset (3.26), while Low Stress students average just 
2.82.

Further analysis of the `Study_Share_Pct` column reveals why: High Stress 
students dedicate **50.2% of their total productive hours to study alone**, 
compared to 43.6% for Moderate Stress and 34.6% for Low Stress students. 
The stress is not caused by juggling multiple commitments — total productive 
hours are nearly equal across all three groups (~16 hours). It is caused by 
the concentrated allocation of those hours into one dominant activity.

### 5. Social Activity Has a Negligible Effect on GPA
The total GPA decline from the lowest to the highest social hours band is just 
**0.07 GPA points** — the smallest relationship of any activity measured. 
Importantly, every social hours band, including students with the highest 
social engagement (5–6 hrs/day), maintained a GPA above 3.0. Socially active 
students remain above-average performers regardless of how much time they 
spend socialising.

### 6. True Lifestyle Balance Is Effectively Absent Among Top Performers
Using a standard deviation threshold of ≤ 1.5 across four lifestyle activities 
(Study, Social, Physical Activity, Extracurricular) to define genuine balance, 
**zero High Performers qualify as Balanced**. Only **1.2% of Above Average 
students** achieve a truly even distribution of time — making balanced high 
achievers an extremely rare profile in this dataset.

The inverse pattern is equally notable: Below Average students show the 
highest proportion of balanced schedules (6.5%), suggesting that spreading 
time evenly across activities, while appealing in theory, does not translate 
into top academic outcomes.

### 7. High Stress Students Study More and Move Less in Equal Measure
High Stress students average **8.39 study hours per day** versus 5.47 for 
Low Stress students — a difference of nearly 3 hours. The time for that extra 
study is drawn primarily from Physical Activity, where High Stress students 
average 3.96 hrs/day compared to 5.58 hrs/day for Low Stress students. Sleep 
and social hours remain relatively stable across all three stress groups, 
confirming that the High Stress lifestyle is defined by a specific study-versus-
movement trade-off rather than a general compression of all other activities.

---

## Recommendations

**For students aiming to improve GPA:**
Study hours is the single most reliable lever available. The data shows 
consistent, linear returns — every additional hour of study adds measurable 
GPA value with no point of diminishing returns observed within the 5–10 hour 
range.

**For students concerned about social life:**
The data does not support the belief that socialising damages academic 
performance. A 0.07 GPA difference across the full social hours spectrum is 
statistically negligible. Students can maintain an active social life without 
meaningfully sacrificing grades.

**For students and educators regarding stress:**
High stress and high performance are closely linked in this dataset, but the 
mechanism matters. The stress appears to stem from study concentration, not 
from overwhelming workload across many commitments. Interventions focused on 
time allocation awareness — rather than blanket stress reduction — may be more 
effective for this student profile.

**For the pursuit of "balance":**
The data suggests that true lifestyle balance, as defined by an even 
distribution of time across all activities, is incompatible with top-tier 
academic performance in this dataset. Students and advisors should reframe 
"balance" as intentional prioritisation rather than equal time distribution.

---

## Analytical Skills Demonstrated

| Skill | Application |
|---|---|
| Data transformation | Power Query: data loading, type setting, column engineering |
| Feature engineering | Derived five meaningful columns from raw data |
| Statistical reasoning | Applied standard deviation as a balance metric; selected and defended threshold choice after validating against raw data |
| Pivot Table design | Seven structured pivot tables with custom aggregations, grouped bands, and filtered views |
| Chart selection | Matched chart types to data structure and analytical question — diverging bar, line, 100% stacked bar, clustered bar |
| Insight-led titling | All chart titles state findings directly, following the established standard: specific subject, specific finding, no topic labels |
| Dashboard design | Single-screen interactive dashboard with three slicers, five KPI cards, static and dynamic chart architecture |
| Analytical thinking | Independently identified misleading axis scaling (Q5), flawed threshold definition (Q6), and chart type mismatch (Q7b) during the build process |
| Portfolio documentation | Structured GitHub README with full methodology transparency including threshold justification and engineered column rationale |
