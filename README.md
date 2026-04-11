# The 0.25% Problem: Cracking Rare Event Fraud Detection  

## Overview  
Fraud detection in banking is not just a machine learning problem—it’s a **rare event detection challenge**.  
In this case study, we tackle a dataset where fraud accounts for only **0.25% of transactions**, making traditional accuracy-based models unreliable.

 This project focuses on building a system that **prioritizes fraud detection (recall)** while maintaining a balance with precision.

---

##  Dataset  
- Source: Kaggle – **Credit Card Fraud Detection Dataset**  
https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud  

### Key Statistics:
- Total Transactions: **71,396**  
- Fraud Cases: **31**  
- Fraud Rate: **~0.25%**  
- Genuine Transactions: **~99.75%**  

 **Challenge:**  
A naive model predicting all transactions as genuine gives:  
-  99% Accuracy  
-  0% Fraud Detection  

 Hence, accuracy is misleading.

---

##  Problem Statement  

Binary Classification Problem:

- **0 → Legitimate Transaction**  
- **1 → Fraudulent Transaction**  

### Goals:
- Maximize fraud detection  
- Minimize false negatives  
- Maintain practical precision  

---

##  Data Processing  

### Handling Class Imbalance → SMOTE  
- Synthetic Minority Over-sampling Technique  
- Generates artificial fraud samples  
- Applied only on training data  

 Prevents bias toward majority class  

---

##  Feature Engineering  

To enhance fraud detection, new features were created:

-  **Transaction Hour** → Captures unusual timing  
-  **Night Transaction Flag (12 AM–6 AM)**  
-  **Log Amount** → Reduces skewness  
-  **High Amount Flag** → Above 95th percentile  

---

##  Descriptive Insights  

### Key Observations:
- Fraud is more frequent during **night hours**  
- Fraud occurs in:
  - Very small transactions (testing behavior)  
  - Very large transactions (high-value attacks)  

### Visualizations:
- Bar Plot (Fraud vs Time) 
- Box Plot (Amount vs Fraud)  

[View Fraud vs Time Chart](images/fraud_vs_time.png) , 
[View Fraud vs Amount Chart](images/fraud_vs_amount.png) , 
[View Fraud By Hour Chart](images/fraud_by_hour.png)

---

##  Evaluation Metrics  

### Why Not Accuracy?
Because fraud is rare, accuracy becomes misleading.

### Metrics Used:
- **Precision** → How many predicted frauds are correct  
- **Recall (MOST IMPORTANT)** → How many actual frauds are detected  
- **F1 Score** → Balance between precision & recall  

 **Critical Insight:**  
- False Negative (missed fraud) = High loss  
- False Positive = Minor inconvenience  

 Therefore, **Recall is prioritized**

---

##  Models Implemented  

### 1️. Logistic Regression  
- Simple & interpretable baseline  

| Metric | Value |
|------|------|
| Recall | 0.91 |
| Precision | 0.08 |
| Accuracy | 0.98 |
| ROC-AUC | 0.968 |

 High recall but too many false alarms  
 
###### [View Logistic Regression Confusion Matrix](images/confusion_matrix_logistic_regression.png)

---

### 2️. Support Vector Machine (SVM)  
- Effective in high-dimensional space  

| Metric | Value |
|------|------|
| Recall | 0.91 |
| Precision | 0.32 |
| Accuracy | 0.99 |
| ROC-AUC | 0.955 |

 Better balance but still moderate precision 
 
###### [View SVM Confusion Matrix](images/confusion_matrix_svm.png)

---

### 3️. Random Forest (Best Model)  

- Ensemble method  
- Handles non-linearity  
- Reduces overfitting  

| Metric | Value |
|------|------|
| Recall | 0.91 |
| Precision | 0.91 |
| Accuracy | 1.00 |
| ROC-AUC | 0.969 |

 **Best performer with balanced precision & recall**

###### [View Random Forest Confusion Matrix](images/confusion_matrix_random_forest.png)
---

##  Model Comparison  

| Model | Precision | Recall | F1 Score | Accuracy | ROC-AUC |
|------|----------|--------|----------|----------|--------|
| Logistic Regression | 0.08 | 0.91 | 0.15 | 0.98 | 0.968 |
| SVM | 0.32 | 0.91 | 0.47 | 0.99 | 0.955 |
| Random Forest | 0.91 | 0.91 | 0.91 | 1.00 | 0.969 |

##### [View Model Performance Comparison](images/model_performance_comparison.png)

---

##  Why Random Forest Wins  

Fraud patterns are:
- Complex  
- Dynamic  
- Non-linear  
- Rare  

 Random Forest advantages:
- Combines multiple decision trees  
- Captures complex patterns  
- Reduces variance  
- Handles noise effectively  

---

##  ROC Curve  

- Shows trade-off between TPR & FPR  
- AUC close to 1 indicates strong model  

##### [View ROC Curve](images/roc_curve.png)  

---

##  Key Insight  

### Why is Recall More Important Than Accuracy?

- Fraud is extremely rare (~0.25%)  
- Accuracy can be misleading  
- Recall directly measures fraud detection  

 Missing fraud leads to:
- Financial loss  
- Customer distrust  
- Legal risks  

 **Conclusion: Recall > Accuracy in fraud detection systems**

---

##  Resources  

-  [Project Report](reports/the_0.25_percent_problem_report.pdf)  
-  [Jupyter Notebook](notebooks/rare_event_fraud_detection_analysis.ipynb)
  
---

##  Disclaimer  

- This dataset is publicly available on Kaggle  
- It is used only for educational and research purposes in this project  
- Dataset is not included in this repository due to its size

---
##  Conclusion  

- Fraud detection is a **highly imbalanced problem**  
- Accuracy is not reliable  
- Recall is the most critical metric  
- **Random Forest achieved the best performance**  

---

## License

MIT License  

Copyright (c) 2026 Disha Girase  

Permission is hereby granted, free of charge, to any person obtaining a copy of this project to use, modify, and distribute it for educational purposes.

---
