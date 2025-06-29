# Assignment 15: Loan Default Prediction

## Overview

This assignment applies machine learning to a real-world financial problem: predicting loan defaults. It involves data preprocessing, model training, performance evaluation, and fairness/explainability analysis. The goal is to identify high-risk borrowers and provide actionable insights that can reduce default rates while maintaining transparency and fairness.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Dataset and Cleaning](#dataset-and-cleaning)
3. [Feature Engineering](#feature-engineering)
4. [Model Building and Evaluation](#model-building-and-evaluation)
5. [Explainability and Fairness](#explainability-and-fairness)
6. [Ethical Considerations](#ethical-considerations)
7. [Conclusion](#conclusion)
8. [Technologies Used](#technologies-used)

---

## Introduction

Loan defaults pose a significant risk to financial institutions. Predictive models can assist in identifying likely defaulters early in the loan approval process. However, such models must be built carefully to avoid reinforcing existing biases or violating ethical standards. This project explores how we can develop a responsible and effective machine learning solution.

---

## Dataset and Cleaning

- **Dataset**: UCI "German Credit Data" – a commonly used dataset for credit risk modeling.
- **Preprocessing Steps**:
  - Handled missing values.
  - Encoded categorical variables using one-hot and label encoding.
  - Normalized numerical features for consistent model input.
  - Defined the `default` column as the target variable.

### Exploratory Data Analysis
- Visualized distributions of key features.
- Checked class imbalance and correlations.

---

## Feature Engineering

- Created additional binary or ratio-based features from existing columns (e.g., loan-to-income ratio).
- Applied `StandardScaler` for numeric feature scaling.
- Ensured all features were ready for tree-based modeling.

---

## Model Building and Evaluation

- **Model Used**: Random Forest Classifier (due to its robustness and interpretability).
- **Split**: 80% training, 20% testing.
- **Evaluation Metrics**:
  - Accuracy
  - Confusion Matrix
  - Precision, Recall, F1-score

### Results:
```

Test Accuracy: \~0.76
Precision, Recall, F1-scores all indicate good performance with balanced class handling.

```

- **Feature Importance** was visualized to highlight critical attributes like `credit_duration`, `checking_status`, and `credit_amount`.

---

## Explainability and Fairness

### Explainability with SHAP
- **Global Explainability**: SHAP summary plot showed most influential features across the dataset.
- **Local Explainability**: SHAP waterfall plot explained individual predictions for high-risk users.

###  Fairness with Fairlearn
- Evaluated performance across different `checking_status` groups.
- Metrics: accuracy, selection rate, false positive rate (FPR), and true positive rate (TPR).

#### Fairness Metrics Snapshot:

| Checking Status | Accuracy | Selection Rate | FPR  | TPR  |
|-----------------|----------|----------------|------|------|
| 0               | 0.676    | 0.721          | 0.56 | 0.81 |
| 1               | 0.673    | 0.694          | 0.52 | 0.88 |
| 2               | 0.750    | 0.917          | 1.00 | 0.90 |
| 3               | 0.873    | 0.986          | 1.00 | 0.98 |

### Interpretation
- Groups with `checking_status` 2 and 3 had **perfect FPR** — indicating potential over-approval bias.
- Selection rate and model accuracy also varied significantly between groups.
- Actionable insight: fairness-aware training may be needed to balance outcomes.

---

## Ethical Considerations

### Key Focus Areas:
- **Bias**: Sensitive attributes like financial background may introduce unintended discrimination.
- **Privacy**: Only publicly available, non-identifiable data was used.
- **Transparency**: Explainability methods like SHAP ensure interpretability.

### Recommendations:
- Apply **fairness-aware algorithms** (e.g., reweighting, adversarial debiasing).
- Continuously **monitor** fairness metrics post-deployment.
- Use **model cards** for clear documentation of model behavior.

---

## Conclusion

This project shows that:
- Machine learning can effectively predict loan defaults.
- However, **fairness and transparency** must be actively addressed.
- Tools like SHAP and Fairlearn are essential for **responsible AI development** in high-stakes domains.

---

## Technologies Used

- Python 3.x
- scikit-learn
- pandas, numpy
- SHAP
- Fairlearn
- Matplotlib / Seaborn
