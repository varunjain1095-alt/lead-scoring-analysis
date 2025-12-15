# Lead Scoring Analysis

## Overview
This project focuses on predicting whether a website visitor is likely to purchase a certification course. Using user interaction data captured through website metrics and optional surveys, multiple machine learning models were evaluated to identify the most suitable model for lead conversion prediction.

The primary objective of this analysis is **model selection based on comparative performance**, rather than deep error diagnostics or post-hoc model explainability.

---

## Business Objective
The analysis supports customer acquisition efforts by helping marketing and sales teams prioritise high-potential leads. By identifying users with a higher likelihood of conversion, the model enables more targeted outreach and efficient allocation of sales and marketing resources.

---

## Dataset Summary
- **Rows:** 9,240  
- **Columns:** 37  
- **Target Variable:** `Converted` (binary: conversion vs non-conversion)

### Data Sources
- Website interaction metrics (e.g., time spent on website, page views per visit)
- Optional survey responses (e.g., city, specialisation, referral source)
- Outreach indicators (e.g., do not email, do not call)

The target variable exhibits class imbalance, with non-converted users forming the majority of observations.

---

## Methodology

### Data Cleaning
- Missing values were present primarily in categorical features and were assumed to be **missing completely at random (MCAR)** or **missing at random (MAR)**.
- Columns with excessive missingness were dropped, while remaining features were treated using category consolidation and imputation.
- Duplicate rows were identified and removed to prevent bias in model training.

### Exploratory Data Analysis (EDA)
- Numeric features were analysed using summary statistics and distributions to identify outliers.
- Categorical features were reviewed for balance across categories.
- Correlation analysis and variance inflation factor (VIF) indicated no strong multicollinearity among numeric features.

### Feature Engineering
- Label encoding was applied to selected binary categorical features.
- One-hot encoding was applied to remaining categorical variables, resulting in feature expansion.
- Feature selection was performed using a combination of Chi-square tests, ANOVA, mutual information, and random forest–based feature importance.
- Irrelevant and weak features were removed to improve model stability and reduce noise.

---

## Modeling Strategy
The following models were evaluated:
- **XGBoost**
- **CatBoost**
- **Stacked Ensemble (XGBoost + CatBoost)**

Gradient boosting models were chosen due to their suitability for high-dimensional tabular data and their ability to capture complex, non-linear relationships. Cross-validation was used to assess model stability, and a stacking approach was explored to evaluate potential performance gains.

The focus of this project is **comparative model performance and selection**, rather than detailed error analysis or explainability.

---

## Evaluation Framework
Models were evaluated using consistent metrics:
- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Given the class imbalance, accuracy alone was not considered sufficient. Precision and recall were balanced based on business needs, and ROC-AUC was used to assess class separation performance.

---

## Results
- All models achieved similar accuracy.
- **CatBoost** achieved the highest precision.
- **XGBoost** achieved the highest recall and ROC-AUC (0.888).
- The stacked model performed comparably but did not outperform XGBoost.

**Final Model Selected:** **XGBoost**, based on its superior ability to separate purchasers from non-purchasers while maintaining a balanced precision–recall trade-off.

---

## Business Impact
- A limited set of features was sufficient to achieve strong predictive performance, reducing the need for additional data collection.
- Incomplete information was found to impact model performance more than the absence of additional features.
- The existing feature set effectively captures key web usage and behavioural signals relevant to purchase decisions.

---

## Limitations and Future Work
- Missing demographic and survey information limits model performance.
- Timestamp-level data could enable deeper behavioural analysis, such as visit sequencing and research intensity.
- Additional cost, pricing, and payment-related features could further improve predictive accuracy.

---

## Tech Stack
- Python
- Pandas, NumPy
- Scikit-learn
- XGBoost
- CatBoost
