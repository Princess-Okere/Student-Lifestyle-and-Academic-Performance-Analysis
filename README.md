# Student Lifestyle & Academic Performance Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset Description](#dataset-description)
- [Data Preparation & Engineered Columns](#data-preparation--engineered-columns)
- [Analysis Questions](#analysis-questions)
- [Key Findings](#key-findings)
- [Key Takeaways](#key-takeaways)
- [Analytical Skills Demonstrated](#analytical-skills-demonstrated)
- [Tools Used](#tools-used)
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

<img width="593" height="243" alt="image" src="https://github.com/user-attachments/assets/8c95954d-4d21-4cd2-bc09-03efa7f40fd3" />


### 3. Physical Activity Produces a Gradual, Marginal GPA Decline
More physical activity is associated with lower GPA, but the decline is slow 
and modest — a total drop of **−0.29 GPA points** across the full activity 
range.
 The pattern reflects a steady, gradual decrease rather than a sharp drop.
This suggests that higher physical activity hours are associated with slightly lower academic performance, but the effect is modest. Overall, the trend indicates a small trade-off in time allocation rather than a strong impact of physical activity on GPA.

<img width="411" height="279" alt="image" src="https://github.com/user-attachments/assets/c82b8cb8-dee3-4e50-a7f0-7faf36cb8eaf" />

### 4. High Stress Is a Feature of Top Academic Performance
**96.8% of High Performers (GPA ≥ 3.5) experience High Stress** — compared 
to 51.5% of all students. High Stress students also carry the highest average 
GPA across the entire dataset (3.26), while Low Stress students average just 
2.82.

<img width="616" height="267" alt="image" src="https://github.com/user-attachments/assets/6fbf728e-6c30-4944-a299-e2a2bf511dbc" />

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

<img width="414" height="277" alt="GPA vs Social_Hour" src="https://github.com/user-attachments/assets/696d3f85-53cf-4a75-8681-78f81f222359" />


### 6. True Lifestyle Balance Is Effectively Absent Among Top Performers
Using a standard deviation threshold of ≤ 1.5 across four lifestyle activities 
(Study, Social, Physical Activity, Extracurricular) to define genuine balance, 
**zero High Performers qualify as Balanced**. Only **1.2% of Above Average 
students** achieve a truly even distribution of time — making balanced high 
achievers an extremely rare profile in this dataset.

The inverse pattern is equally notable: Average students show the 
highest proportion of balanced schedules (9.8%), suggesting that spreading 
time evenly across activities, while appealing in theory, does not translate 
into top academic outcomes.

<img width="585" height="268" alt="Student Balance Profile" src="https://github.com/user-attachments/assets/da5a832b-030e-44fa-bbbc-e6c3e489c35c" />


### 7. Increased studying hour is responsible for stress
Studying Contributes to 50.2% of High Stress Levels Among Students.

After identifying that high-performing students overwhelmingly belonged to the high-stress category, a follow-up question emerged: What is driving this stress? Is it the challenge of balancing time across multiple activities, or is it linked to a specific activity?

The analysis points clearly to studying as the primary source of stress. Among high-performing students, study hours account for 57% of reported high stress levels, making it the largest contributor by a considerable margin. This suggests that the elevated stress observed among top-performing students is not primarily the result of trying to maintain a balanced lifestyle. Instead, it appears to be closely associated with the increased study commitment required to achieve strong academic outcomes.

Taken together, these findings indicate that academic success in this dataset is strongly linked to intensive study habits, and that the stress experienced by high performers is largely a by-product of the effort invested in maintaining high grades.


<img width="375" height="278" alt="Study_Hr Stress Distribution" src="https://github.com/user-attachments/assets/73f2a69d-df0f-4ae5-825e-21750fdf16b3" />



---

## Key Takeaways

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

**For the pursuit of "balance":**
The data suggests that true lifestyle balance, as defined by an even 
distribution of time across all activities, is incompatible with top-tier 
academic performance in this dataset. Students and advisors should reframe 
"balance" as intentional prioritisation rather than equal time distribution.

---

## Analytical Skills Demonstrated

* **Data Cleaning & Transformation** – Used Power Query for data loading, type correction, and column preparation.
* **Feature Engineering** – Created five derived columns to support stress, performance, and balance analysis.
* **Statistical Analysis** – Applied standard deviation to measure activity balance and validated the threshold against the underlying data.
* **Pivot Table Analysis** – Built multiple pivot tables with custom aggregations, grouped bands, and slicer-driven views.
* **Data Visualization** – Selected and designed appropriate chart types, including line charts, diverging bars, and 100% stacked bars.
* **Interactive Dashboard Development** – Built a single-page dashboard with slicers, KPI cards and dynamic charts.
* **Excel Automation** – Recorded and implemented a VBA macro to clear dashboard filters, improving usability and enabling a cleaner slicer design without visible headers.
* **Data Storytelling** – Converted analytical findings into concise insight-driven chart titles and dashboard narratives.
* **Documentation & Reporting** – Produced a structured GitHub README covering methodology, assumptions, calculations, findings, and analytical decisions.


## Tools Used

* Microsoft Excel (Pivot Tables, Power Query, GETPIVOTDATA).
* Dynamic KPI cards with GETPIVOTDATA formulas.
* Slicer-driven filtering with Report Connections.
* VBA macro for filter clearing.

[View Interactive Dashboard](https://github.com/Princess-Okere/Student-Lifestyle-and-Academic-Performance-Analysis/blob/0c5399114de3ffbac4662b9062157d06fa2add71/Student%20lifestyle%20project.xlsm)

[View Presentation(PDF)](https://github.com/user-attachments/files/29464972/Student_Lifestyle_Analysis.pdf)

[View Presentation(pptx)](https://github.com/user-attachments/files/29465020/Student_Lifestyle_Analysis.pptx)



*Dataset: Student Lifestyle | Source: Kaggle | Tool: Microsoft Excel*
