---
title: Investigating Socioeconomic and Climate Factors of Mental Health Outcomes with Data
excerpt: >-
  In this project, we investigate the interactions between socioeconomic and climate factors and mental health outcomes. Specifically we look at associations and causal interactions of these factors with self-reported poor mental health days and suicide rates in U.S. counties.
date: '2021-03-28'
layout: post
---
Below is an abridged version of our work intended for a more general data science audience. You can read our full work [here]({{site.baseurl}}/images/MentalHealth/final_report.pdf).

## Introduction
Mental health is a complex aspect of everybody’s well being. There are many factors involved, including socioeconomic and climate factors. In this study we investigate how these factors interact with mental health outcomes. Previous work [1] investigates a similar research question, but does so only with regression between these factors and suicide rates, an extreme manifestation of mental distress. Our contribution to the field includes extending regression analysis to also include predicting self-reported poor mental health days and introducing a causal matching analysis to draw stronger conclusions about the associations between our socioeconomic and climate features and the mental health outcomes.


## Methods
Our socioeconomic data comes from County Health Rankings [2], and the USDA [3]. Our climate data comes from NOAA [4]. Our mental health outcomes data comes from County Health Rankings [2] and CDC Wonder [5]. We gathered and filtered data for 5 years between 2011 and 2016 (excluding 2014) for U.S. counties. We split our final dataset into an 80/20 split for training our regression models.

### Regression Analysis
Our regression analysis included training 5 different models: Lasso, Ridge, LinearGAM, Random Forest, and Gradient Boosting. We trained each of these models by using 10-fold cross validation with the training set, and computing MAE, RMSE, and R^2 values for each training fold. We then averaged these metrics across all 10 folds to get the final training metrics for each model. The training metrics are presented below.

| Model Class | Avg. MAE Poor Mental Health Days| Avg. RMSE Poor Mental Health Days | Avg. R^2 Poor Mental Health Days | Avg. MAE Suicide Rate | Avg. RMSE Suicide Rate | Avg. R^2 Suicide Rate |
| ----------- | -------- | --------- | -------- | -------- | --------- | -------- |
| Lasso Regression | 0.439 | 0.575 | 0.246 | 5.118 | 7.121 | 0.108 |
| Ridge Regression | 0.402 | 0.538 | 0.339 | 4.201 | 5.731 | 0.420 |
| LinearGAM Regression | 0.376 | 0.508 | 0.411 | 3.868 | 5.287 | 0.506 |
| **Gradient Boosting Regression** | 0.370 | 0.501 | 0.426 | 3.844 | 5.220 | 0.518 |
| **Random Forest Regression** | 0.365 | 0.497 | 0.437 | 3.865 | 5.377 | 0.491 |
| Null Regression | 0.509 | 0.663 | 0 | 5.544 | 7.583 | 0 |

We found that Random Forest was the most effective model for predicting Poor Mental Health Days, and that Gradient Boosting was the most effective model for predicting Suicide Rates. We then trained these respective model classes with the entire training set and computed the same statistics using the test set for evaluation. The results from our model evaluation are presented below.

| Model Class | Outcome | Average MAE | Average RMSE | Average R^2 |
| ----------- | ------- | ----------- | ------------ | ----------- |
| Random Forest | Poor Mental Health Days | 0.359 | 0.477 | 0.437 |
| Gradient Boosting | Suicide Rate | 3.827 | 5.238 | 0.446 |



### Matching Analysis

## Results
By looking at the feature importance and partial dependence for our final models, we found the more important features for predicting each of the mental health outcomes. We found that for predicting Poor Mental Health Days, income and college education were the most significant features. For predicting Suicide Rates, the level of urbanization was the most significant feature by far.


## Discussion

## References
[1] S. Mukherjee and Z. Wei. Suicide disparities across metropolitan areas in the US: A comparativeassessment of socio-environmental factors using a data-driven predictive approach.PLOS One,16(11), Nov 2021.  
[2] County   Health   Rankings.National   Data   &   Documentation:2010-2019,    2019.  
[3] U.S. Department  of  Agriculture  (USDA)  Economic  Research  Service  (ERS).Rural-Urban Continuum Codes, Dec 2020.  
[4] National Oceanic and Atmospheric Administration (NOAA) National Centers for Environment Information. Climate at a Glance: County Time Series, Dec 2021.  
[5] Centers for Disease Control and Prevention (CDC). CDC WONDER, Dec 2021.  
