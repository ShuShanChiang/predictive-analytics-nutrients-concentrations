# Predictive Analytics for Nutrient Estimation in Potato Plants

This project develops a machine learning pipeline using **near-infrared spectroscopy (NIRS)** data to estimate multiple nutrient concentrations in potato leaves. The solution integrates **Partial Least Squares Regression (PLSR)** with **Ridge Regression** in a **stacked ensemble**, achieving strong predictive performance across seasons — particularly for macronutrients (N, P, K).

## Problem Statement

Traditional nutrient testing is destructive and labor-intensive. The goal is to:  
**Build a non-destructive, fast, and scalable nutrient estimation pipeline using spectral reflectance data.**


## Method Overview

**Data Source**  
- Potato leaf spectral reflectance data (400–2500 nm), collected across four seasons  
- Both **fresh** and **dried** samples were used to assess generalizability

**Pipeline Stages**  
1. **Data Preprocessing**
   - Missing value imputation (median for <10%, KNN for others)
   - Outlier handling (IQR method, winsorization)
   - Spectral resampling to 1nm resolution

2. **Dimensionality Reduction**
   - Partial Least Squares Regression (PLSR) with 10-fold CV

3. **Modeling**
   - Baseline models: PLS, Ridge, Lasso, SVR, Random Forest, XGBoost
   - Final: **Stacked PLS + Ridge Regression** using weighted loss

4. **Evaluation Metrics**
   - Primary: **RPD (Ratio of Prediction to Deviation)**
   - Secondary: R², RMSE


## Model Selection and Comparison

We experimented with individual and combined models.  
The best results came from a **stacked PLS + Ridge** ensemble.

| Model                     | Average RPD (All Elements) |
|---------------------------|----------------------------|
| PLS                       | 1.319                      |
| PLS + Ridge (Average)     | 1.476                      |
| Ridge                     | 1.518                      |
| **PLS + Ridge (Stacked)** | **1.610**                  |
<img width="373" height="280" alt="image" src="https://github.com/user-attachments/assets/facaa090-6027-4dc8-bfbf-03711a432731" />

**Best Performing Model:** `Stacked PLS + Ridge`  
- Extracts informative latent variables via PLS  
- Stabilizes predictions with Ridge regularization  
- Significantly improves over any individual model


## Validation Insights

- **Macronutrients** (N, P, K) consistently achieved **RPD > 2** in strong-performing seasons  
- **Micronutrients** (e.g., B, Zn, Fe) remained challenging — RPD often < 1.5  
- Performance varied by season and sample type (fresh vs dried), due to **concept drift** and **sample variability**
<img width="786" height="490" alt="image" src="https://github.com/user-attachments/assets/b8dd5303-4722-4ea8-b7ee-653a4f644e69" />
<img width="786" height="490" alt="image" src="https://github.com/user-attachments/assets/b70be928-a242-4796-9185-addb163c7186" />



## Folder Structure
```
predictive-analytics-nutrients-concentrations/
├── data/           # Raw and processed spectral data (fresh and dried leaf samples)
├── preprocessing/  # Scripts or notebooks for data cleaning and imputation
├── models/         # Model training, evaluation, and ensemble code
└── README.md       # Project overview
└── final report    # Final academic report
```
