---
layout: page
title: Housing Price Prediction
description: Prediction of housing prices using various ML algorithms including MLP, Random Forests, and XGBoost
img: 
importance: 1
category: Stats & ML
related_publications: false
---

#### Overview
This project aimed to predict house prices using multiple regression models, including XGBoost, AdaBoost, Random Forest, Ridge Regression, and a Multi-Layer Perceptron (MLP) regressor. Extensive preprocessing was performed, handling missing data, correcting errors, and encoding categorical variables. We also created composite features and addressed skewness using log and Box-Cox transformations. Ensemble methods combining models like XGBoost and Ridge Regression delivered the best results.

#### Results
The models were evaluated using 4-fold cross-validation (RMSE):

| **Model**                  | **RMSE** |
|----------------------------|----------|
| XGBoost                    | 0.118    |
| Ridge Regression           | 0.123    |
| Random Forest              | 0.137    |
| Neural Network (MLP)       | 0.148    |
| AdaBoost                   | 0.162    |
| Ridge-XGB Ensemble         | 0.116    |
| Ridge-RF Ensemble          | 0.121    |
| XGB-RF Ensemble            | 0.122    |


The XGBoost/Ridge Regression ensemble model performed the best with an RMSE of 0.116.

#### Conclusions
* Feature Interactions: Interactions between features were crucial for improving model accuracy, not just high correlation to sale price.
* Data Scaling: Standardization and normalization had varying effects across models. Correcting skewness improved performance.
* Ensemble Methods: Hybrid models like XGBoost/Ridge Regression outperformed individual models, likely due to reduced overfitting and better handling of outliers.

The project highlights the importance of feature engineering and ensemble learning for improving predictive accuracy in regression tasks.

<a href="https://github.com/guswns3396/CSCI567-Project/">Github</a>

Collaborators: Nathaniel Sands, Chenyu Wang