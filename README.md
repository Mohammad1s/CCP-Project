# Telecom Customer Churn Prediction

## Business Problem

Customer churn reduces recurring revenue and increases the cost of acquiring replacement customers. This project uses customer account, service, and billing information to predict whether a customer is likely to leave, so the telecom company can prioritize retention outreach.

The business objective is to identify as many likely churners as practical. Accordingly, model tuning prioritizes **recall for the churn class**: missing a customer who leaves can mean a lost retention opportunity. Precision is also important because false alarms can lead to unnecessary outreach or discounts.

## Findings

Exploratory analysis of the 7,043-customer dataset found that:

- About **26.5%** of customers churned (1,869 customers), while 73.5% stayed. Because churn is the minority class, accuracy alone can hide poor identification of churners.
- Churn was highest among **month-to-month customers** (about 43%), compared with about 11% for one-year contracts and 3% for two-year contracts.
- Customers who churned had shorter tenure (median about **10 months**, versus 38 months for customers who stayed), indicating that early-tenure engagement may be important.
- Churners had higher median monthly charges (about **$80**, compared with $64 among customers who stayed).
- Newer, higher-paying, month-to-month customers are a useful group to prioritize for further risk assessment. These are observed associations, not proof that any one factor causes churn.

## Results

The data was split into stratified training and test sets. Preprocessing was fitted within model pipelines to avoid leakage. Logistic Regression and Random Forest were tuned on the training set with stratified 5-fold cross-validation, using churn recall as the selection metric. The selected tuned Logistic Regression was then evaluated once on the held-out test set.

| Model | Test recall | Test precision | Test F1-score |
|---|---:|---:|---:|
| Logistic Regression baseline | 0.5588 | 0.6572 | 0.6040 |
| Random Forest baseline | 0.4893 | 0.6310 | 0.5512 |
| **Tuned Logistic Regression (selected)** | **0.7834** | 0.5043 | 0.6136 |
| Tuned Random Forest | 0.7487 | 0.5364 | 0.6250 |

The tuned Logistic Regression was selected because it achieved the highest cross-validated churn recall. Its test recall increased by **22.46 percentage points** over the untuned Logistic Regression baseline—a substantial gain in the share of churners identified. The trade-off is lower precision: about half of customers flagged by the tuned model did not churn in the test set. These holdout results are useful for comparison, but do not establish statistical significance or guarantee future performance.

## Recommendation

The company should focus retention efforts on customers most likely to leave, especially newer customers on month-to-month plans and those facing higher monthly bills. Offer practical help first—such as a check-in about service quality, a review of whether the plan fits their needs, or clear lower-cost plan options. Use discounts selectively where they are likely to keep a valuable customer, rather than giving incentives to every at-risk customer.

Start with a limited retention campaign and compare its results with a similar group of customers who receive the usual service. Track how many customers stay, the cost of outreach and offers, and the revenue retained. Expand the campaign when it produces enough additional retained-customer value to justify its cost.
