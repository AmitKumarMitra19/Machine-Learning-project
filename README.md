# Employee Access Approval Prediction

## Overview

This project addresses the critical business problem of automating employee access approvals within enterprise environments. Manual access control processes can be slow, inconsistent, and prone to errors, risking security breaches or operational inefficiencies. The goal is to leverage machine learning to predict whether an employee’s request for access to corporate resources should be approved or denied — enabling faster, reliable, and auditable decision-making.

## Dataset

I have used the **Amazon Employee Access** dataset, a publicly available dataset via CatBoost’s datasets module. It contains approximately 32,000 records featuring anonymized employee attributes (such as department, role, and resource requested) and a binary target indicating whether access was granted (approved) or not (denied).

- Features include both categorical and numerical data.
- The dataset reflects a real-world enterprise security problem where access management is crucial.

## Methodology

My approach follows a systematic machine learning pipeline with attention to data preprocessing, exploratory data analysis, model selection, evaluation and  explainability.

### Data Preprocessing & EDA

- Handled categorical variables through label encoding, suitable for tree ensemble models.
- Scaled numeric features for distance-based models like KNN.
- Performed correlation analysis and feature exploration to understand data distributions and relationships.
- Checked for class imbalances and outliers.

### Model Training & Evaluation

I trained and compared multiple classifiers well-suited for tabular data, including:

- K-Nearest Neighbors (KNN)  
- Random Forest  
- XGBoost  
- LightGBM   

For fair comparison, each model was evaluated on a hold-out validation set using these metrics:

- **Accuracy:** Proportion of correct predictions.  
- **ROC AUC:** Measure of model discrimination between classes.  
- **F1 Score:** Harmonic mean of precision and recall, robust under class imbalance.

### Dimensionality Reduction

- Applied Principal Component Analysis (PCA) for KNN to reduce dimensionality and improve performance.
- Determined PCA was not required for tree-based models due to their native handling of high-dimensional data.

### Explainability

- Used **LIME** for local interpretability, focusing on explaining model predictions at an individual employee request level.
- These explainability tool helps building trust and auditability critical for security-focused applications.


## Key Findings

| Model          | Train Accuracy | Validation Accuracy | Train ROC AUC | Validation ROC AUC | Validation F1 Score |
|----------------|----------------|---------------------|---------------|--------------------|---------------------|
| KNN            | 0.9490         | 0.9382              | 0.9485        | 0.7006             | 0.9679              |
| Random Forest  | 0.9421         | 0.9442              | 0.7665        | 0.7234             | 0.9713              |
| XGBoost        | **0.9660**     | 0.9513              | **0.9824**    | 0.8415             | **0.9747**          |
| LightGBM       | 0.9540         | **0.9493**          | 0.9563        | **0.8483**         | 0.9738              |

- **XGBoost** and **LightGBM** outperformed other models, achieving the best balance of accuracy, ROC AUC, and F1 score on validation data.
- **KNN** had a noticeable drop in ROC AUC on validation, indicating less robust generalization.
- Tree ensemble model demonstrated superior ability to capture nonlinear relationships and complex patterns.

## Business Impact

The deployment of this machine learning pipeline will enable:

- **Automated and consistent employee access approval decisions.**  
- **Increased operational efficiency** by reducing manual review overhead.  
- **Improved security posture** through data-driven, auditable access control.  
- **Explainable AI compliance** via LIME ,essential for trusted enterprise adoption.


---

*Project developed by [Amit Kumar Mitra]*  

