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
Summed all discretionary activity hours per student to measure overall daily 
engagement:
