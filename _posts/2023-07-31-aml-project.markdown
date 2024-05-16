---
layout: post
title:  "Predicting Movie Success - Applied Machine Learning"
date:   2023-07-31 08:00:00 +0800
author: WY
categories: jekyll update
---


## Overview
This page is dedicated to our Applied Machine Learning project, where our team of 5 members delves into the intricacies of predictive modeling and data analysis in the context of the film industry. With the aim of developing machine learning models tailored for predicting movie success, our project focuses on two key metrics: profitability (binary classification) and revenue (regression). As the film industry undergoes rapid evolution, influenced by factors such as the COVID-19 pandemic and shifting consumer preferences, the need for accurate predictive models has never been more pronounced. Our endeavor seeks to address this need by leveraging advanced machine learning techniques, particularly using Python programming, to provide actionable insights for movie stakeholders.

## Objective
The primary objective of this project is to create predictive models that leverage metadata available prior to production, such as storyline, production company, cast, and budget, to forecast the success of a movie. By providing insights into potential profitability and revenue, these models empower movie producers and makers to make informed decisions on investment strategies, maximizing the likelihood of a movie's financial success.

## Significance

The significance of this project lies in its potential to revolutionize decision-making processes within the movie industry. By harnessing the power of machine learning, movie stakeholders can anticipate the performance of their projects with greater accuracy, mitigating financial risks and optimizing resource allocation. Furthermore, the ability to predict both profitability and revenue offers valuable insights into the viability of movie proposals at various investment levels, facilitating data-driven decision-making and enhancing overall industry competitiveness.

## Data Source and Collection

The primary dataset used for this project is sourced from TMDB (The Movie Database) and GroupLens, obtained from Kaggle at the following link: <a href="https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset">TMDB and GroupLens Movie Dataset</a>. This dataset provides a comprehensive snapshot of movie metadata and ratings, encompassing over 45,000 movies released on or before July 2017.

Three main files were utilized from this dataset: movies_metadata, credits, and keywords. These files contain crucial information about each movie, including details on the storyline, production company, cast, and budget, among others.

Additionally, supplementary datasets were employed to supplement the main dataset for feature engineering purposes. Notably, the budget and revenue data were not adjusted for inflation initially. To ensure consistency and accuracy, global inflation rates from 1980-2021 were obtained from <a href="https://www.macrotrends.net/countries/WLD/world/inflation-rate-cpi#:~:text=World%20inflation%20rate%20for%202021,a%200.25%25%20increase%20from%202017/">Macrotrends</a>, and budget and revenue figures were adjusted to 2018 dollars accordingly.

Due to the dataset's size limitations, one-hot encoded variables for all cast and crew were not feasible. Therefore, only the <a href="https://www.imdb.com/chart/starmeter/">top 100 actors/actresses</a> and <a href="https://www.imdb.com/list/ls026411399/">top 100 directors</a> were considered in the model, based on rankings from IMDb's Starmeter and director lists.

## Data Preprocessing
The original dataset comprised over 45,000 movies, but only 5,381 movies had valid budget and revenue information. To ensure relevance, movies produced on or before 1980 were excluded, aligning with the availability of inflation rate data starting from 1980. After preprocessing, the dataset consisted of 4,835 unique movies.

Categorical and JSON variables underwent preprocessing into one-hot encoded variables, with variables featuring more than 20 unique categories simplified into the 10 most frequent categories and an "others" category. This reduction was necessary due to the dataset's limited size, which could not support numerous explanatory variables. Numerical variables with vastly different scales, such as budget and revenue, were transformed or standardized. Runtime and total cast were standard scaled to ensure consistency.

Text variables, including overview, title, and keywords, were aggregated into a single document for each movie and processed using topic modeling into 10 one-hot encoded variables. Topic modeling was essential to uncover underlying relationships among movies within a reasonable number of features. Both Latent Dirichlet Allocation (LDA) and Gibbs Sampling Dirichlet Multinomial Mixture (GSDMM) models were trained.

For LDA, a pre-determined number of topics (10) was chosen based on the Elbow method on coherence score against the number of topics. However, due to the relatively short text content, LDA yielded topics with a high degree of overlap. In contrast, GSDMM, designed for shorter texts, produced more interpretable topics with distinct, non-overlapping keywords. These GSDMM topics were utilized as features for subsequent machine learning tasks.

![GSDMM]({{ site.baseurl }}/figure/AML_GSDMM.png)


## Profitability Prediction Analysis

Profitability prediction is a critical aspect for investors and stakeholders in the film industry, influencing decisions on project viability and resource allocation. In this section, we analyze the performance and outcomes of two key predictive models: Logistic Regression and Decision Tree, focusing on their ability to predict movie profitability.

### Logistic Regression Model
The Logistic Regression model, designed to classify movies as profitable or not based on budget and revenue, yielded mixed results. While the model demonstrated overall accuracy of around 70%, it exhibited a tendency to overpredict profitable movies, which constituted 70% of the dataset. However, its performance in identifying non-profitable movies was notably poor, potentially risking financial losses for investors.

In an effort to mitigate overfitting and enhance predictive capabilities, L1 and L2 regularized models were employed. The L2 regularized model, after hyperparameter tuning, achieved the highest accuracy and an AUC of 0.72. Despite this improvement, recall for the not-profitable class remained suboptimal.

![Logistic Regression]({{ site.baseurl }}/figure/AML_Logistic_Regression.png)

Furthermore, models trained with SMOTE oversampling method showcased enhanced prediction ability for not-profitable movies, albeit at the expense of slightly reduced accuracy for profitable ones. Given the priority of identifying projects that may not break even, the SMOTE model emerges as the preferred choice despite its trade-offs.


### Decision Tree Model
The evaluation of decision tree models involved testing various hyperparameters such as split criterion (Gini, Entropy), splitter (best, random), max depth, min samples split, and min samples leaf. Ensemble techniques including Random Forest, Ada Boost, and Gradient Boosting were also employed. The performance metrics encompassed train and test accuracies, precision, recall, and F1-scores. To address the dataset's small size and class imbalance, stratified K-fold cross-validation was utilized. 

![Decision Tree]({{ site.baseurl }}/figure/AML_Decision_Tree.png)

Ada Boost emerged as the top-performing model with a test accuracy of 0.697, albeit exhibiting a slight overfitting concern. The decision tree models showcased better prediction for profitable classes compared to non-profitable ones. 

![Decision Tree AUC1]({{ site.baseurl }}/figure/AML_Decision_Tree_AUC1.png)

The Ada boost model has a Test AUC of 0.72 (on the low side compared to Train AUC of 0.82). The top important features include budget, number in series, run time, total cast, total popular cast. 

To address the class imbalance, we used SMOTE to oversample on train data set to boost performance on class [0]. We achieved higher precision and recall for class [0] at the expense of overall. However, both models had a big gap between train and test accuracy, indicating overfitting.

![Decision Tree SMOTE]({{ site.baseurl }}/figure/AML_Decision_Tree_SMOTE.png)

Despite budget being the primary feature in the optimal decision tree, its pre-production acquisition challenges prompted the development of an Ada Boost model excluding budget. Surprisingly, this model maintained the same accuracy of 0.697, with the number of movies in a series emerging as the most influential feature.

![Decision Tree AUC2]({{ site.baseurl }}/figure/AML_Decision_Tree_AUC2.png)

### Comparison between Logistic Regression and Decision Tree Model
Both the logistic regression and decision tree models had similar performance. The SMOTE logistic regression was slightly better at predicting the not-profitable class. Both models still had similar overall accuracy even after removing budget, meaning that they are somewhat robust to uncertain budget.

## Revenue Prediction Analysis
In revenue prediction, models were evaluated using mean squared error (MSE), root mean squared error (RMSE), and adjusted R2. RMSE quantifies prediction error, while adjusted R2 measures the proportion of revenue variation explained by independent variables, allowing direct model comparisons.

### Linear Regression
Linear regression models underwent feature selection via backward elimination and regularization techniques like Lasso and Ridge to prevent overfitting, revealing the significance of budget, production companies, and language. 

![Linear Regression]({{ site.baseurl }}/figure/AML_Linear_Regression.png)

Most of the models had similar performance in terms of RMSE and it is notably that the absence of the budget feature led to significantly poorer performance.Since it is essential to understand how well the independent variables collectively explain the variation in revenue, model with highest R2 is chosen as the best model (backward elimination).

![Linear Regression R2]({{ site.baseurl }}/figure/AML_Linear_Regression_R2.png)

As shown from the plot above (from best model), the model is good for predicting higher revenue movies, but performs poorly for low revenue movies. This may be because data on low revenue movies is limited.

![Linear Regression Feature]({{ site.baseurl }}/figure/AML_Linear_Regression_Feature.png)
 
The most important feature in predicting revenue is budget. The other top 10 features are mostly from production companies and language (this is also observed for model without budget). Budget, production companies and language are essential features to predict movie revenue for linear regression.

### Neural Network
Fully connected neural network can also be used for predicting continuous target variables. They have the advantage over traditional linear regression models in that they can learn non-linear relationships. They are also more robust against multicollinearity.

To test different network architectures and hyperparameters, the test dataset was further divided using random sampling to get a 70:10:20 train/validation/test ratio. Model architecture was between 2-5 layers with a decreasing number of neurons in each layer, and activation functions tried were ReLu, leaky ReLu and linear. Other hyper parameters tested were batch size and number of epochs.

Initial networks had the issue of not learning further after the first epoch regardless of architecture or hyperparameters. It was determined that this was due to incorrect specification of inputs with some of the numerical inputs being in a different scale from the others. As such, numerical variables that were not already scaled in the pre-processing step were standard scaled (budget, revenue, top100 cast).

![Neural Network]({{ site.baseurl }}/figure/AML_Neural_Network.png)

### Comparison between Linear Regression and Neural Network Models
The neural network is slightly better at predicting revenue than the linear regression (adjusted R2 of 0.558 >0.542), although both models would be considered underfitted. 

Budget was one of the most important explanatory variables in the linear regression model. While the neural network performs better when budget is included, the improvement in performance is not sizeable. If the user is unsure of the estimated budget, the neural network without budget can still provide an estimate. Nonetheless, prediction from both models would likely have a large confidence interval, especially for the neural network result which is both log transformed and standard scaled.


Please refer to the comprehensive analysis provided in the Jupyter notebook available on our GitHub repository. You can access the detailed findings and methodologies with below link. 
<p><a href="https://github.com/widyayutika/Predicting-Movie-Success">Predicting Movie Success</a></p>


## Conclusion
The team developed four predictive models for profitability and revenue prediction, but encountered challenges due to underfitting, possibly stemming from missing explanatory variables, input data quality, or dataset size limitations. Budget and revenue information, often user-submitted on platforms like TMDB, are frequently undisclosed by studios, affecting model accuracy. Notably, involvement of top production companies emerged as a significant positive variable in all models, indicating their predictive prowess, particularly for larger studios. However, the models hold potential utility for smaller producers lacking extensive resources. While budget played a crucial role in revenue prediction, its removal significantly degraded performance, highlighting the necessity of accurate budget estimation for return on investment forecasts. Despite this, profitability models exhibited robustness to budget exclusion, providing insights into breakeven potential even in budget uncertainty scenarios. Future research could focus on smaller-scale productions with less predictable outcomes, aiming to enhance model effectiveness in diverse filmmaking contexts.
