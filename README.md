# Week 6 – Integrative Capstone: Telco Customer Churn

## Project Overview

This project is the final capstone for my Data Science with Python internship. I worked on an end-to-end customer churn analysis using the IBM Telco Customer Churn dataset.

The project covers data acquisition, data cleaning, exploratory data analysis, feature engineering, supervised learning, model evaluation, cross-validation, feature importance and unsupervised customer segmentation.

## Dataset

The dataset contains customer information related to demographics, account details, services and billing.

Public dataset source:

https://github.com/IBM/telco-customer-churn-on-icp4d/blob/master/data/Telco-Customer-Churn.csv

Original dataset size: **7,043 rows × 21 columns**

After converting `TotalCharges` to numeric and removing 11 rows with invalid values, the final working dataset contained **7,032 customers**.

## Project Objectives

- Clean and prepare the customer churn dataset.
- Explore the main patterns related to customer churn.
- Build supervised machine learning models for churn prediction.
- Compare Logistic Regression and Random Forest.
- Evaluate the models using several classification metrics.
- Perform five-fold cross-validation.
- Identify important features using Random Forest.
- Use K-Means clustering to create customer segments.
- Interpret the results and provide practical recommendations.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib
- Google Colab

## Supervised Learning

Two classification models were developed:

1. Logistic Regression
2. Random Forest

### Model Results

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8053 | 0.6515 | 0.5749 | 0.6108 | 0.8361 |
| Random Forest | 0.7640 | 0.5404 | 0.7513 | 0.6286 | 0.8360 |

Logistic Regression achieved better accuracy and precision.

Random Forest achieved much higher recall for the churn class, meaning it identified a larger proportion of customers who actually churned. Its F1-score was also slightly higher.

For a retention-focused use case, Random Forest can therefore be useful when identifying more potential churners is the main priority.

## Cross-Validation

Five-fold stratified cross-validation was also performed.

| Metric | Logistic Regression | Random Forest |
|---|---:|---:|
| Accuracy | 0.8028 | 0.7776 |
| Precision | 0.6558 | 0.5636 |
| Recall | 0.5452 | 0.7244 |
| F1 Score | 0.5952 | 0.6339 |
| ROC-AUC | 0.8461 | 0.8463 |

The cross-validation results showed a similar trade-off between the two models.

## Exploratory Data Analysis

The analysis showed several noticeable differences in churn rates:

- Overall churn rate: **26.58%**
- Month-to-month contract churn: **42.71%**
- One-year contract churn: **11.28%**
- Two-year contract churn: **2.85%**
- Fiber optic internet churn: **41.89%**
- Electronic check churn: **45.29%**
- Customers without tech support churn: **41.65%**

These results were treated as associations in the dataset rather than proof of causation.

## Feature Importance

The most important Random Forest features included:

1. `tenure`
2. `TotalCharges`
3. `Contract_Two year`
4. `MonthlyCharges`
5. `InternetService_Fiber optic`
6. `PaymentMethod_Electronic check`
7. `Contract_One year`
8. `OnlineSecurity_Yes`
9. `TechSupport_Yes`
10. `PaperlessBilling_Yes`

`tenure` had the highest Random Forest feature importance.

## Customer Segmentation

K-Means clustering was also applied as an unsupervised learning step.

The clustering used:

- `tenure`
- `MonthlyCharges`
- `NumServices`

Different values of `k` from 2 to 8 were tested using silhouette scores.

The best result was:

**Number of clusters: 2**  
**Silhouette score: 0.4256**

The two groups differed mainly in customer tenure, monthly charges and number of services.

### Cluster Profiles

| Cluster | Customers | Avg Tenure | Avg Monthly Charges | Avg Services | Churn Rate |
|---|---:|---:|---:|---:|---:|
| 0 | 3,147 | 46.61 | 89.47 | 5.28 | 24.21% |
| 1 | 3,885 | 20.93 | 44.82 | 1.81 | 28.49% |

The clustering was performed without using Churn as a clustering feature. Churn rates were compared afterward to understand the segments.

## Key Recommendations

Based on the analysis:

- Pay more attention to month-to-month customers.
- Monitor customers using electronic check payments.
- Investigate the higher churn observed among fiber optic customers.
- Consider proactive support for customers without tech support.
- Use tenure as an important customer-risk indicator.
- When recall is the priority, consider the Random Forest model.
- Use customer clusters for profiling and segmentation rather than treating them as direct causes of churn.

## Repository Contents

```text
Week_6_Integrative_Capstone/
│
├── README.md
├── Week_6_Telco_Customer_Churn_Capstone.ipynb
├── Week_6_Integrative_Capstone_Telco_Customer_Churn_Report_Natural_Student_Version.docx
├── telco_customer_churn_processed.csv
├── logistic_regression_churn_model.pkl
└── random_forest_churn_model.pkl
