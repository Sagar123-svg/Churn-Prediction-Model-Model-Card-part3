# Model Card Report: Random Forest Churn Intelligence Engine

## 1. Intended Use
* **Primary Objective:** Real-time prediction of a consumer's likelihood to churn within the next 60 days.
* **Target Audience:** Marketing Ops, CRM Managers, and Customer Experience teams.
* **Out-of-Scope Applications:** Do not use this model to evaluate wholesale accounts, external distributor performance, or long-term trends past the 60-day window.

## 2. Sourcing & Data Split Matrix
* **Data Context:** Modeled using customer behavior history cut off on **September 30, 2025**.
* **Splits:** 80% Training ($N=1,911$), 20% Out-of-Sample Test Validation ($N=511$).
* **Anti-Leakage Guardrails:** Derived features are strictly locked to pre-snapshot timestamps. Post-snapshot data fields are used only to build the final target verification markers.

## 3. Modeling Framework & Architecture
* **Baseline Approach:** Stratified Logistic Regression with $L_2$ Regularization.
* **Final Chosen Architecture:** Random Forest Classifier (`n_estimators=200`, `max_depth=10`, `min_samples_leaf=4`).
* **Decision Optimization Threshold:** Shifted from 0.50 down to **0.42** to balance precision and recall, optimizing the cost of retention campaigns.

## 4. Performance Validation Overview
* **ROC-AUC:** 0.9124
* **Precision (Class 1):** 0.7622
* **Recall (Class 1):** 0.8148
* **F1-Score:** 0.7876

## 5. Limitations & Ethical Risks
* **Data Bias:** Heavily reliant on recent digital engagement metrics. Customers who primarily purchase offline or don't interact with emails may be incorrectly flagged as high risk.
* **Ethical Risk Profile:** Price discrimination. Over-relying on risk scores can lead to automated systems that only offer discounts to churning users, penalizing loyal, full-price buyers.

## 6. Production Monitoring Strategy
* **Drift Tracking:** Measure the Population Stability Index (PSI) monthly for key inputs like `Recency` and `ticket_count`.
* **Retraining Triggers:** Automatically retrain the model if performance drops ($\text{ROC-AUC} < 0.82$) or if customer response behaviors shift by more than 15%.
