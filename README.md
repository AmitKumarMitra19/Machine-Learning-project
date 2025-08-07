# Employee Access Approval Prediction

## Overview

This project addresses the critical business problem of automating employee access approvals within enterprise environments. Manual access control processes can be slow, inconsistent, and prone to errors, risking security breaches or operational inefficiencies. The goal is to leverage machine learning to predict whether an employee’s request for access to corporate resources should be approved or denied — enabling faster, reliable, and auditable decision-making.

## Dataset

I have used the **Amazon Employee Access** dataset, a publicly available dataset via CatBoost’s datasets module. It contains approximately 32,000 records featuring anonymized employee attributes (such as department, role, and resource requested) and a binary target indicating whether access was granted (approved) or not (denied).

- Features include both categorical and numerical data.
- The dataset reflects a real-world enterprise security problem where access management is crucial.

#  Predictive Modeling Pipeline for Classification

##  Objective

The goal of this project was to build a robust machine learning pipeline capable of accurately predicting a binary target variable in a highly **imbalanced dataset**. Key tasks included:

- Handling **class imbalance**  
- Encoding **categorical variables**  
- Treating **outliers**  
- Comparing multiple classification models  
- Hyperparameter tuning using **Optuna**  
- Model interpretability via **LIME**

---

##  Methodology

### 1. Data Preprocessing
- **Outlier Treatment**: Used a custom `Winsorizer` transformer to clip extreme values. 
- **Encoding**: Applied `OneHotEncoder` to categorical variables.  
- **Scaling**: StandardScaler applied to numerical features.

### 2. Class Imbalance Handling
- Implemented **SMOTE** to balance class distribution in the training set.

### 3. Model Pipelines
- Built pipelines with:  
  `Preprocessor ➝ SMOTE ➝ Model`  
  using `ImbPipeline` for each classifier.

### 4. Models Compared
- K-Nearest Neighbors (KNN)  
- Random Forest  
- XGBoost  
- LightGBM  
- CatBoost

### 5. Hyperparameter Tuning
- Used **Optuna** to tune model hyperparameters via 3-fold stratified cross-validation.  
- Evaluation metric: **ROC AUC**

### 6. Evaluation Metrics
- ROC AUC Score  
- Classification Report  
- ROC Curve Visualization  
- Model Leaderboard

### 7. Model Explainability
- Used **LIME** to explain individual predictions from the top model.  
- Provided insights into feature contributions at a local level.

---

## 🏆 Leaderboard (Post-Optimization)

| Model         | ROC AUC  |
|---------------|----------|
| XGBoost       | 0.842639 |
| LightGBM      | 0.835333 |
| Random Forest | 0.834310 |
| CatBoost      | 0.811128 |
| KNN           | 0.754293 |

>  **XGBoost** was selected as the best-performing model after optimization.

---

## 🔍 LIME Explainability

LIME provided feature-level explanations for specific predictions.  
Top features pushing a prediction toward **Class 1** included:

- `feature_3` (e.g., > -0.03)  
- `feature_5` (e.g., > -0.19)  
- `feature_4` (e.g., > 0.16)  
- and more...

This helps validate **why the model predicts a positive class**, essential for regulatory and business transparency.

---

##  Business Impact

- **Better Decision-Making**: Increased recall and reduced false negatives on the minority class.  
- **Regulatory Compliance**: Model explanations enhance interpretability and trust.  
- **Production Readiness**: Optimized models are scalable and deployable in real-world settings.


---

*Project by: [Amit Kumar Mitra]*  
*Date: August 2025*
