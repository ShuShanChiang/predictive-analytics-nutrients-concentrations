# Predictive Analytics for Nutrient Concentration Estimation

This project explores the use of near-infrared spectroscopy (NIRS) and machine learning to estimate nutrient concentrations in potato leaves. By leveraging a stacked Partial Least Squares (PLS) and Ridge Regression model, we aim to improve predictive performance and interpretability—supporting more efficient, non-destructive nutrient monitoring in agriculture.

## Project Highlights

- Predicts multiple nutrient concentrations (e.g., N, P, K) from hyperspectral reflectance data
- Implements a scalable pipeline with:
  - Hybrid imputation for missing data
  - Spectral resampling and z-score normalization
  - PLSR for dimensionality reduction
  - Stacked ensemble learning (PLS + Ridge)
- Focus on macronutrient prediction and seasonal generalization
- Evaluation using RPD, RMSE, and R² metrics

## Methodology

1. **Preprocessing**: Data cleaning, IQR-based outlier removal, and Winsorization
2. **Dimensionality Reduction**: Supervised PLS regression
3. **Modeling**: Ridge Regression and stacking with weighted loss
4. **Evaluation**: Cross-validation and seasonal testing on fresh vs. dried datasets

## Results

- Best RPD > 4.5 for nitrogen in optimal seasons
- PLS–Ridge stacking achieved highest mean RPD (1.61)
- Generalization limited by seasonal variability (concept drift)
- Strongest performance on dried-season2 samples

## Tech Stack

- Python (NumPy, Pandas, Scikit-learn, Seaborn)
- Jupyter Notebook / VSCode
- Fixed random seed for reproducibility

## Folder Structure
project-root/
┣ data/ # Raw and processed datasets
┣ notebooks/ # Exploratory and training notebooks
┣ models/ # Saved models or output
┗ README.md
