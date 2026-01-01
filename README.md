# Heart Disease Prediction & Risk Modeling 🫀

**Course:** BIOS5801 - Final Project  
**Date:** December 2025  
**Language:** R

## 📖 Project Overview
This project applies statistical modeling and machine learning techniques to a clinical dataset to predict the presence of heart disease. The analysis focuses not only on predictive accuracy but also on **model interpretability** and **clinical risk assessment**.

The workflow includes extensive Exploratory Data Analysis (EDA), advanced missing value imputation, and a comparison of three distinct modeling approaches: **Naive Bayes**, **XGBoost**, and **Lasso Regression**.


## 📊 Dataset
The analysis uses the `heart.csv` dataset, which includes the following clinical features:
* **Numerical:** Age, RestingBP, Cholesterol, MaxHR, Oldpeak.
* **Categorical:** Sex, ChestPainType, FastingBS, RestingECG, ExerciseAngina, ST_Slope.
* **Target:** HeartDisease (Binary: 0/1).

## 🛠️ Methodology

### 1. Data Cleaning & Preprocessing
* **Handling Zero Values:** Biologically impossible zeros in `RestingBP` and `Cholesterol` were converted to `NA`.
* **Imputation:** Utilized **k-Nearest Neighbors (kNN)** imputation (k=5) via the `VIM` package to handle missing data.
* **Encoding:** Applied One-Hot Encoding using `fastDummies` for categorical variables.
* **Splitting:** Data partitioned into 80% Training and 20% Testing sets using `caret`.

### 2. Exploratory Data Analysis (EDA)
* **Distributions:** Histograms and Density plots for numerical features.
* **Outlier Detection:** Violin and Boxplots.
* **Correlations:** Spearman correlation heatmaps and Chi-square tests for categorical variables.
* **Multivariate Analysis:** Scatter plot matrices grouped by disease status.

### 3. Modeling Approaches
The project evaluates three models with hyperparameter tuning:

1.  **Naive Bayes:**
    * Tuned with Kernel density estimation and Laplace smoothing.
2.  **XGBoost (eXtreme Gradient Boosting):**
    * Tuned `nrounds`, `max_depth`, `eta`, `gamma`, and `subsample` using Cross-Validation.
    * Includes **SHAP (SHapley Additive exPlanations)** analysis to visualize feature impact.
3.  **Lasso Logistic Regression (GLMNet):**
    * Used for feature selection and regularization.
    * Converted coefficients into **Odds Ratios** for clinical interpretation.

## 💡 Key Features & Insights

### 🔍 Interpretability & Risk Scoring
Unlike "black box" predictions, this project generates actionable insights:
* **SHAP Summary Plots:** Identifies which features (e.g., ST Slope, Chest Pain Type) drive the XGBoost predictions.
* **Clinical Scorecard:** Derived from Lasso coefficients, creating a point-based system where users can calculate a "Risk Score" and convert it to a probability of heart disease.

### 📈 Advanced Evaluation
* **Threshold Tuning:** Analyzed how moving the classification threshold impacts Precision, Recall, and F1 scores.
* **Age Stratification:** Evaluated model performance across specific age groups (<45, 45-60, >60) to ensure fairness and reliability.
* **Calibration Plots:** Verified if predicted probabilities match observed event rates.

## 📦 Dependencies
To run this project, you will need the following R libraries:

```r
install.packages(c(
  "ggplot2", "gridExtra", "VIM", "GGally", "dplyr", "corrplot", 
  "fastDummies", "pheatmap", "caret", "naivebayes", "MLmetrics", 
  "SHAPforxgboost", "glmnet", "broom", "pROC", "ROCR"
))
