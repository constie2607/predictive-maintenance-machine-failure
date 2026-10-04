# Predictive Maintenance: Machine Failure Prediction

## Project Overview

Unexpected machine failures can lead to costly downtime, disrupted production and increased maintenance costs. This project analyses machine operating data and applies machine learning to predict equipment failure.

The project combines exploratory data analysis (EDA), feature engineering and classification modelling to identify patterns associated with machine failure and assess how effectively failures can be predicted.

Two machine-learning models were developed and compared:

- Logistic Regression
- Random Forest

Particular attention was given to class imbalance and the trade-off between identifying as many failures as possible and avoiding unnecessary maintenance alerts.

---

## Dataset

The dataset contains **10,000 machine observations** with information about operating conditions and recorded machine failures.

Key variables used for modelling include:

- Machine type
- Air temperature
- Process temperature
- Rotational speed
- Torque
- Tool wear
- Temperature difference

The target variable is:

`machine_failure`

Only **339 of the 10,000 observations (3.39%)** represent machine failures, creating a significant class imbalance.

---

## Project Objectives

The project aims to:

- Explore the frequency and characteristics of machine failures
- Investigate relationships between operating conditions and failure
- Analyse different machine failure mechanisms
- Engineer relevant features for predictive modelling
- Build machine-learning models to predict machine failure
- Compare Logistic Regression and Random Forest performance
- Identify the most influential features used by the Random Forest model
- Evaluate the business trade-off between missed failures and false maintenance alerts

---

## Exploratory Data Analysis

Exploratory analysis identified several patterns in machine operating conditions.

Machine failures were highly imbalanced, accounting for only **3.39%** of observations.

Different failure mechanisms were also explored, including:

- Heat Dissipation Failure (HDF)
- Power Failure (PWF)
- Overstrain Failure (OSF)
- Tool Wear Failure (TWF)
- Random Failure (RNF)

Heat Dissipation Failure was the most frequently recorded failure type in the dataset.

Analysis of HDF showed differences in temperature conditions, rotational speed and torque compared with observations without HDF.

Correlation analysis also identified a strong negative relationship between rotational speed and torque, while torque showed the strongest positive correlation with overall machine failure among the individual operating variables analysed.

---

## Machine Learning

The data was split into:

- **80% training data**
- **20% testing data**

A stratified split was used to preserve the proportion of machine failures in both datasets.

Two classification models were evaluated.

### Logistic Regression

The Logistic Regression model used class weighting to account for the highly imbalanced target variable.

Results:

| Metric | Score |
|---|---:|
| ROC-AUC | 0.907 |
| Failure Precision | 0.14 |
| Failure Recall | 0.82 |
| Failure F1-Score | 0.25 |

The model detected **82% of actual machine failures**, but its low precision resulted in a large number of false-positive maintenance alerts.

### Random Forest

A Random Forest classifier was also trained using balanced class weights.

Results:

| Metric | Score |
|---|---:|
| ROC-AUC | 0.968 |
| Failure Precision | 0.96 |
| Failure Recall | 0.63 |
| Failure F1-Score | 0.76 |

The Random Forest correctly identified **43 of the 68 failures** in the test set while producing only **2 false-positive failure predictions**.

---

## Model Comparison

The two models demonstrate an important predictive-maintenance trade-off.

**Logistic Regression** achieved higher failure recall, identifying more of the machines that actually failed. However, it generated substantially more false-positive alerts.

**Random Forest** achieved substantially higher precision and F1-score, producing far fewer false alarms while still identifying 63% of failures.

Overall, Random Forest provided the strongest performance across ROC-AUC, precision and F1-score.

---

## Feature Importance

Random Forest feature importance identified the strongest predictive features as:

| Feature | Importance |
|---|---:|
| Torque | 32.2% |
| Rotational Speed | 24.5% |
| Tool Wear | 19.9% |
| Temperature Difference | 10.1% |

Torque, rotational speed and tool wear together accounted for approximately **77% of the model's total feature importance**.

These results suggest that information relating to mechanical load, machine speed and accumulated wear is particularly useful for predicting machine failure.

Feature importance represents how useful each variable was to the Random Forest model and should not be interpreted as evidence that these variables directly cause machine failure.

---

## Business Insights

In a real predictive-maintenance environment, the optimal model depends on the relative cost of different prediction errors.

A **false negative** could result in an unexpected machine breakdown, production downtime or equipment damage.

A **false positive** could trigger an unnecessary inspection or maintenance intervention.

The Logistic Regression model may therefore be useful where detecting as many potential failures as possible is the priority.

The Random Forest model may be more suitable where maintenance teams require more precise alerts and want to minimise unnecessary interventions.

The prediction threshold could also be adjusted depending on the organisation's tolerance for missed failures versus false maintenance alerts.

---

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Google Colab

---

## Repository Structure

```text
predictive-maintenance-machine-failure/
│
├── ai4i2020.csv
├── predictive_maintenance_machine_failure.ipynb
└── README.md
