# Customer Churn & Retention Analytics

An end-to-end customer churn and retention analytics project built with **PostgreSQL, Python, machine learning, and Power BI**.

The project combines customer demographics, subscription behavior, product usage, payments, support interactions, churn outcomes, and machine-learning predictions to identify churn drivers, prioritize at-risk customers, and quantify revenue exposure.

> **Note:** This is a portfolio project built using synthetically generated data. All customers, transactions, support interactions, financial values, and business records are fictional.

---

## Dashboard Preview

![Executive Overview](https://github.com/maurynbotha/customer-churn-retention-analytics/blob/main/screenshots/customer_churn_dashboard_screenshots/01_executive_overview.png)

---

## Project Objectives

The project was designed to answer five key business questions:

- How many customers are currently churning, and which segments are most affected?
- What behavioral and service patterns are associated with churn?
- Which active customers are most at risk of leaving?
- How much recurring revenue is exposed to elevated churn risk?
- How accurately can machine learning identify customers likely to churn?

---

## Technology Stack

- **PostgreSQL** — relational database design, feature engineering, data validation, and analytical views
- **Python** — data preparation and machine-learning workflow
- **Pandas / NumPy** — data manipulation
- **Scikit-learn** — preprocessing, modelling, calibration, and evaluation
- **SQLAlchemy / psycopg2** — PostgreSQL connectivity from Python
- **Power BI** — data modelling, DAX, visualization, and interactive reporting
- **Jupyter Notebook / VS Code** — model development

---

## Dataset

The synthetic environment contains **50,000 customers** and supporting operational datasets covering:

- Customer demographics
- Subscription plans
- Subscription status and churn reasons
- Product usage and login activity
- Payment behavior
- Support tickets
- Customer satisfaction
- Machine-learning churn predictions

The final customer-level modelling dataset contains **50,000 observations and 36 source features/fields**, with additional transformations performed in Python.

### Customer Status

| Status | Customers | Share |
|---|---:|---:|
| Active | 39,858 | 79.72% |
| Churned | 10,142 | 20.28% |
| **Total** | **50,000** | **100%** |

---

## Machine Learning Workflow

The modelling workflow included:

1. PostgreSQL feature engineering
2. Missing-value assessment
3. Behavioral feature preparation
4. Categorical encoding
5. Numerical scaling
6. Stratified train/test split
7. Logistic Regression baseline
8. Random Forest modelling
9. Probability calibration
10. Model evaluation
11. Customer risk scoring
12. Prediction write-back to PostgreSQL
13. Power BI reporting

The dataset was split into:

- **40,000 training customers**
- **10,000 test customers**

The original churn distribution was preserved using stratified sampling.

---

## Model Comparison

Three modelling approaches were evaluated.

| Model | Accuracy | Precision | Recall | F1 Score | ROC AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 94.48% | 90.77% | 81.02% | 85.62% | 96.37% |
| Random Forest | 94.29% | 82.60% | **91.03%** | 86.61% | **97.99%** |
| Calibrated Random Forest | **95.45%** | 89.70% | 87.62% | **88.65%** | 97.96% |

The **Calibrated Random Forest** was selected for final churn-risk scoring because it provided the strongest overall balance between accuracy, precision, recall, F1 score, and probability quality.

Additional final-model metric:

- **Brier Score:** 0.0348

### Final Model Confusion Matrix

On the 10,000-customer test set:

| Actual / Predicted | Active | Churned |
|---|---:|---:|
| Active | 7,768 | 204 |
| Churned | 251 | 1,777 |

The final model correctly identified **1,777 of 2,028 actual churners** in the test dataset.

---

## Churn Risk Segmentation

The calibrated model was used to score currently active customers.

| Risk Band | Customers | Average Churn Probability |
|---|---:|---:|
| Critical | 745 | 69.12% |
| High | 1,368 | 32.40% |
| Medium | 3,341 | 10.01% |
| Low | 34,404 | 0.96% |

This resulted in **2,113 High/Critical-risk active customers** requiring elevated retention attention.

---

## Key Model Predictors

The Random Forest feature-importance analysis identified support experience and declining engagement as major predictive signals.

Top predictors included:

1. Recent 90-Day Average Resolution Hours
2. Recent 90-Day Average Satisfaction
3. Recent 90-Day Support Tickets
4. Recent 90-Day High-Priority Tickets
5. Recent 90-Day Repeat Contacts
6. Recent 3-Month Average Logins
7. Recent 3-Month Average Active Days
8. Customer Tenure
9. Login Decline %
10. Recent 3-Month Average Session Minutes

The strongest individual predictor was **Recent 90-Day Average Resolution Hours**, contributing approximately **23.42%** of Random Forest feature importance.

> Feature importance represents predictive contribution within this synthetic dataset and should not be interpreted as proof of causation.

---

## Business Insights

### Churn

Overall customer churn is **20.28%**.

Among acquisition channels:

- Campaign: 23.7%
- Agent: 22.4%
- Referral: 19.7%
- Web: 19.3%
- Mobile App: 19.3%

Individual customers show higher churn than Corporate customers.

Churned customers also exhibit substantially greater deterioration in engagement:

- Average login decline: **11.7%**
- Average usage decline: **10.6%**

---

### Customer Experience

Customer-support behavior shows a strong relationship with modelled churn risk.

Average support resolution time increases from:

- **23.9 hours** for Low-risk customers
- to **33.1 hours** for Critical-risk customers

Average satisfaction falls from:

- **4.0** for Low-risk customers
- to **3.0** for Critical-risk customers

Repeat-contact rate increases from:

- **13.4%** for Low risk
- to **33.7%** for Critical risk

---

### Revenue Exposure

Current active monthly recurring revenue is approximately:

**₦573.11M**

Revenue associated with High/Critical-risk active customers:

**₦28.51M**

Revenue at risk is split approximately into:

- High risk: **₦18.8M**
- Critical risk: **₦9.7M**

Monthly revenue associated with already churned customers is approximately:

**₦136.55M**

The largest churn-related revenue-loss categories are:

- Price Too High
- Service Quality
- Competitor Offer
- Billing Issues
- Poor Customer Support

---

## Power BI Dashboard

The Power BI report contains six pages.

### 1. Executive Overview

![Executive Overview](./screenshots/01_executive_overview.png)

Provides an executive summary of customer volume, churn, retention, revenue, churn reasons, subscription-plan performance, and active-customer risk distribution.

### 2. Churn Drivers & Segmentation

![Churn Drivers & Segmentation](./screenshots/02_churn_drivers_segmentation.png)

Examines churn across acquisition channels, customer segments, contract types, payment behavior, and changes in customer engagement.

### 3. Predictive Churn & Risk

![Predictive Churn & Risk](./screenshots/03_predictive_churn_risk.png)

Uses calibrated machine-learning probabilities to segment active customers into Low, Medium, High, and Critical churn-risk groups and creates a prioritized retention list.

### 4. Customer Experience & Support

![Customer Experience & Support](./screenshots/04_customer_experience_support.png)

Analyzes support volume, high-priority cases, unresolved tickets, resolution time, satisfaction, and repeat contacts across churn-risk bands.

### 5. Revenue & Retention Value

![Revenue & Retention Value](./screenshots/05_revenue_retention_value.png)

Quantifies current monthly revenue, churn-related revenue loss, revenue at risk, customer value, and financial exposure across subscription plans and customer segments.

### 6. Model Performance & Explainability

![Model Performance & Explainability](./screenshots/06_model_performance_explainability.png)

Compares machine-learning models, presents final-model evaluation metrics and confusion matrix results, and identifies the strongest predictive features.

---

## Project Architecture

```text
PostgreSQL
    │
    ├── Customers
    ├── Subscriptions
    ├── Subscription Plans
    ├── Usage Activity
    ├── Payments
    └── Support Tickets
           │
           ▼
SQL Feature Engineering
           │
           ▼
Python / Scikit-learn
           │
           ├── Logistic Regression
           ├── Random Forest
           └── Calibrated Random Forest
           │
           ▼
Churn Predictions
           │
           ▼
PostgreSQL
           │
           ▼
Power BI
```

---

## Repository Structure

```text
customer-churn-retention-analytics/
│
├── README.md
├── .gitignore
│
├── customer_retention_snapshot.pbix
├── customer_retention_snapshot.pdf
│
├── python/
│   └── customer_churn_model.ipynb
│
├── sql/
│   └── customer_churn_schema.sql
│
└── screenshots/
    ├── 01_executive_overview.png
    ├── 02_churn_drivers_segmentation.png
    ├── 03_predictive_churn_risk.png
    ├── 04_customer_experience_support.png
    ├── 05_revenue_retention_value.png
    └── 06_model_performance_explainability.png
```

---

## Project Files

- **Power BI report:** `customer_retention_snapshot.pbix`
- **PDF dashboard:** `customer_retention_snapshot.pdf`
- **Machine-learning notebook:** `python/customer_churn_model.ipynb`
- **PostgreSQL schema:** `sql/customer_churn_schema.sql`

---

## Data Privacy & Disclaimer

This project uses **synthetically generated data** created solely for portfolio and educational purposes.

No real customer records, organizations, financial transactions, support interactions, personal information, or confidential business data are included.

Model performance therefore reflects the relationships intentionally represented in the synthetic dataset and should not be interpreted as expected production performance on real-world customer data.

---

## Skills Demonstrated

**SQL & Data Engineering**
- Relational database design
- PostgreSQL
- Feature engineering
- Analytical views
- Data validation
- Data-quality checks

**Python & Machine Learning**
- Pandas
- NumPy
- Scikit-learn
- Logistic Regression
- Random Forest
- Probability calibration
- Classification evaluation
- Feature importance
- Risk segmentation

**Business Intelligence**
- Power BI
- DAX
- KPI design
- Interactive filtering
- Customer segmentation
- Revenue-at-risk analysis
- ML explainability
- Executive dashboard design

---

## Author

**Maureen Oyibotha**

Data Analytics | Business Intelligence | SQL | Python | Power BI | Machine Learning
