# Heart Disease Prediction & Clinical Risk Scoring 🫀

**Course:** BIOS5801 - Final Project  
**Date:** December 2025  
**Language:** R

## 📖 Project Overview
This project applies statistical modeling and machine learning techniques to a clinical dataset to predict the presence of heart disease. Beyond standard prediction, the analysis focuses heavily on **model interpretability** and **clinical risk assessment**, culminating in a patient-facing "Risk Scorecard."

## 📊 Dataset
The analysis uses the `heart.csv` dataset ($N=918$), featuring:
* **Numerical:** Age, RestingBP, Cholesterol, MaxHR, Oldpeak.
* **Categorical:** Sex, ChestPainType, FastingBS, RestingECG, ExerciseAngina, ST_Slope.
* **Target:** HeartDisease (Binary: 0/1).

## 🛠️ Methodology

### 1. Preprocessing & EDA
* **Imputation:** Biological zeros in `Cholesterol` and `RestingBP` were treated as missing and imputed using **k-Nearest Neighbors (k=5)**.
* **Outlier Detection:** Violin plots identified significant outliers in `Cholesterol` (up to 603) and `RestingBP` (up to 200).
* **Correlation:** A Spearman correlation heatmap revealed that `MaxHR` (-0.40) and `Oldpeak` (0.40) have the strongest linear relationships with Heart Disease among numerical variables.

### 2. Modeling Pipeline
Three models were trained and tuned using 5-fold Cross-Validation:
1.  **Naive Bayes:** Tuned with Kernel estimation and Laplace smoothing.
2.  **XGBoost:** Gradient boosting with SHAP interpretability.
3.  **Lasso Logistic Regression:** Regularized regression for feature selection and scorecard creation.

## 🏆 Model Results



**XGBoost** achieved the highest performance across all metrics. Below is the performance on the held-out test set (20% split):

| Model | Accuracy | ROC AUC | Precision | Recall | Brier Score |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **XGBoost** | **87.43%** | **0.939** | **0.882** | **0.891** | **0.092** |
| Naive Bayes | 86.89% | 0.926 | 0.889 | 0.871 | 0.120 |
| Lasso GLM | 86.34% | 0.929 | 0.864 | 0.891 | 0.099 |

*Metrics derived from model output logs.*

## 💡 Key Clinical Insights

### 1. Top Risk Factors (SHAP Analysis)
Using SHAP (SHapley Additive exPlanations) on the XGBoost model, the most dominant predictors of heart disease were:
1.  **ST Slope (Up vs. Flat/Down):** The single most critical feature.
2.  **Exercise Angina:** Presence of angina during exercise significantly increases risk.
3.  **Chest Pain Type:** Specifically `ASY` (Asymptomatic) and `NAP` (Non-Anginal Pain).
4.  **Sex:** Being Male is associated with higher risk.



### 2. Age Stratification Analysis
The model's performance varies significantly by patient age, performing best on elderly patients:
* **< 45 years:** 90.0% Accuracy (Sample size small)
* **45 - 60 years:** 83.0% Accuracy (Lowest performance)
* **> 60 years:** 94.3% Accuracy (Highest reliability)
*Source: Age group performance table.*

### 3. Patient Risk Scorecard
A logistic scorecard was derived from Lasso coefficients to translate complex model outputs into a simple "Risk Score."
* **The Curve:** The relationship follows a sigmoid curve where a score of **0** represents a 50% probability.
* **Risk Zones:**
    * **Low Risk:** Score < 0 (Green Zone)
    * **High Risk:** Score > 0 (Red Zone)
* **Example Calculation:** A patient with a calculated score of `914` has a **71.38%** probability of heart disease.



## 📦 Dependencies
```r
install.packages(c(
  "ggplot2", "gridExtra", "VIM", "GGally", "dplyr", "corrplot", 
  "fastDummies", "pheatmap", "caret", "naivebayes", "MLmetrics", 
  "SHAPforxgboost", "glmnet", "broom", "pROC", "ROCR"
))
