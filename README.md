# Predictive Analytics for Nutrient Estimation in Potato Plants

This project develops a machine learning pipeline using **near-infrared spectroscopy (NIRS)** data to estimate multiple nutrient concentrations in potato leaves. The solution integrates **Partial Least Squares Regression (PLSR)** with **Ridge Regression** in a **stacked ensemble**, achieving strong predictive performance across seasons — particularly for macronutrients (N, P, K).

## Problem Statement

Traditional nutrient testing is destructive and labor-intensive. Our goal:  
**Build a non-destructive, fast, and scalable nutrient estimation pipeline using spectral reflectance data.**

---

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

---

## Model Selection and Comparison

We experimented with individual and combined models.  
The best results came from a **stacked PLS + Ridge** ensemble.

| Model                     | Average RPD (All Elements) |
|---------------------------|----------------------------|
| PLS                       | 1.319                      |
| PLS + Ridge (Average)     | 1.476                      |
| Ridge                     | 1.518                      |
| **PLS + Ridge (Stacked)** | **1.610**                  |

**Best Performing Model:** `Stacked PLS + Ridge`  
- Extracts informative latent variables via PLS  
- Stabilizes predictions with Ridge regularization  
- Significantly improves over any individual model

---

## Validation Insights

- **Macronutrients** (N, P, K) consistently achieved **RPD > 2** in strong-performing seasons  
- **Micronutrients** (e.g., B, Zn, Fe) remained challenging — RPD often < 1.5  
- Performance varied by season and sample type (fresh vs dried), due to **concept drift** and **sample variability**

---

## Cross-Season Generalization

- Low model transferability between seasons  
- Performance drops notably when training on one season and testing on another  
- Indicates the need for **season-aware models** or **transfer learning techniques**

---

## Future Work

- Cross-season training and transfer learning  
- Physically realistic data augmentation (e.g., Gaussian noise instead of Mixup)  
- Explore non-linear models (e.g., tuned Random Forests with cloud resources)

---

## Real-World Impact

This workflow shows potential for:
- Smart fertilization recommendations  
- Real-time crop monitoring  
- Sustainable precision agriculture

---


## Folder Structure
```
predictive-analytics-nutrients-concentrations/
├── data/           # Raw and processed spectral data (fresh and dried leaf samples)
├── preprocessing/  # Scripts or notebooks for data cleaning and imputation
├── models/         # Model training, evaluation, and ensemble code
└── README.md       # Project overview
```
