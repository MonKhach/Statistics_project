# Sleep, Health & Lifestyle — Statistical Analysis (OLS Regression + Hypothesis Testing)

This repository contains a statistical analysis of the **Sleep, Health, and Lifestyle** dataset.  
The goal is to study how **stress**, **physical activity**, **BMI**, and basic demographics relate to **sleep quality**, using regression and hypothesis tests.

> Note: This project reports **associations** found in the dataset. It does not prove causation.

---

## Dataset
- **Source:** Kaggle — *Sleep Health and Lifestyle Dataset*
- **How to use:** Download the dataset from Kaggle and place the CSV into `data/raw/`.

Expected path:
- `data/raw/Sleep_health_and_lifestyle_dataset.csv`

Kaggle dataset link:
```text
https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset
What I changed in the dataset
BMI Category recoding (2 groups)

Original BMI labels: Overweight, Normal, Obese, Normal Weight
I recoded them into two groups:
-Normal BMI ← (Normal, Normal Weight)
-High BMI ← (Overweight, Obese)
Counts after recoding:
-Normal BMI: 216
-High BMI: 158
Exploratory Data Analysis (EDA)
Main visualizations included:
-Scatterplot: Sleep Quality vs Stress Level
-Scatterplot: Sleep Quality vs Physical Activity Level
-Correlation heatmap for:
 -Quality of Sleep, Stress Level, Physical Activity Level
Regression Analysis (statsmodels OLS)
Regression 1 — Full model

Question: How do stress, physical activity, BMI, age, gender, and steps relate to sleep quality?
Dependent variable: Quality of Sleep
Predictors: Stress Level, Physical Activity Level, BMI_Category (Normal BMI vs High BMI), Age, Gender, Daily Steps
Result summary:
-Very strong model fit (R² ≈ 0.94)
-Stress is strongly negatively associated with sleep quality
-Physical activity, age, and Normal BMI are positively associated with sleep quality
-Daily steps effect is small compared to other predictors
Regression 2 — Without Daily Steps
Goal: Check whether results are stable without the steps variable.
Result summary:
-R² remains ≈ 0.94
-Main coefficients stay consistent
Regression 3 — Interaction model (Stress × BMI)
Question: Does the effect of stress on sleep quality differ between Normal BMI and High BMI?
Added interaction term: Stress Level × BMI_Category
Result summary:
-R² ≈ 0.944
-Interaction term is statistically significant
-The stress–sleep relationship differs by BMI group
Hypothesis Testing
Hypothesis 1
Statement: “Higher physical activity lowers stress level.”
Test: OLS regression
Dependent: Stress Level
Predictor: Physical Activity Level
Result summary:
-Not statistically significant (p ≈ 0.51)
-Very low R² (~0.001)
-Conclusion: Not supported in this dataset.
Hypothesis 2
Statement: “Higher physical activity is associated with better sleep quality.”
Test: OLS regression
Dependent: Quality of Sleep
Predictor: Physical Activity Level
Result summary:
-Positive association and statistically significant (p < 0.001)
-Conclusion: Supported (association).
t-test — Does high stress mean worse sleep?
Groups:
High stress: Stress Level ≥ 7
Low stress: Stress Level ≤ 3
Test: Welch’s t-test (unequal variances)
Observed means:
-Mean sleep quality (high stress) ≈ 5.92
-Mean sleep quality (low stress) ≈ 8.97
-p-value extremely small
Conclusion: High stress is associated with significantly worse sleep quality.
χ² test — High stress vs BMI Category
Created:
HighStress = 1 if Stress Level ≥ 7 else 0
Test:
χ² test of independence between BMI_Category and HighStress
Result:
-χ² ≈ 47.72
-p-value ≈ 4.9e-12
Conclusion: High stress and BMI category are significantly associated (not independent).
