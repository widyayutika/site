---
layout: post
title:  "Recommendation System for Retail Product - Data Science for Business"
date:   2023-04-30 08:00:00 +0800
author: WY
categories: jekyll update
---

## Overview

This page is dedicated to our Data Science for Business project, where our team of 5 members delve into addressing the challenges faced by H&M, a leading fashion retailer. One of the main challenges we aim to tackle is increasing sales and driving growth in an extremely competitive market.

## Objective

Our primary objective is to leverage data science methodologies to help H&M overcome challenges in the competitive retail industry. Specifically, we aim to conduct RFM analysis, market basket analysis, and develop a personalized product recommendation system to improve customer targeting, boost sales, and drive growth for H&M.

## Significance

The significance of this project lies in its potential to empower H&M with actionable insights derived from data science techniques. By understanding customer behavior patterns and preferences, H&M can enhance customer engagement, loyalty, and ultimately achieve sales growth in a highly competitive market.

## Data Source and Collection

We obtained the H&M purchase history of customers across time dataset from Kaggle.

<p><a href="https://www.kaggle.com/competitions/h-and-m-personalized-fashion-recommendations/data ">Link to the dataset</a></p>

The dataset consists of three main components:

A. Articles: This dataset contains information about items available for purchase at H&M, including details such as product name, product group, pattern, color, and index group.

B. Customer: This dataset includes detailed information about H&M customers, including their membership status, fashion newsletter subscription frequency, and age (with missing values).

C. Transactions Train: This dataset comprises purchases made by customers over time, including transaction dates, customer IDs, article IDs, prices, and sales channel IDs.

## Data Preparation

In the data preparation phase, we cleaned the datasets by addressing missing values, removing duplicates, and reformatting the data. Specifically:

For the Articles dataset, missing values were handled, and unnecessary fields such as detailed description were removed. No duplicated rows were found.
The Customer dataset underwent similar cleaning processes, with no missing values or duplicated rows detected.
In the Transactions Train dataset, missing values and duplicated rows were addressed, ensuring data integrity for further analysis.

The cleaned datasets are now ready for further processing and analysis.

## Analysis and Discussion

In this section, we elaborate on our analytical methodologies and findings.

### RFM (Recency, Frequency, and Monetary) Analysis
RFM analysis is pivotal in understanding and serving H&M's customer base effectively. By segmenting customers based on their Recency, Frequency, and Monetary metrics, we can high-value customers for targeted marketing and retention efforts.

#### RFM Calculation
The calculation involves determining the snapshot date (i.e. the day after the latest transaction date in the dataset), grouping the dataset by customer_id, and computing the RFM values for each customer as follows:
- Recency: the difference between the snapshot date and the most recent transaction date for each customer
- Frequency: the number of transactions for each customer
- Monetary: the total amount spent by each customer

![DSB_RFM_Distribution]({{ site.baseurl }}/figure/DSB_RFM_Distribution.png)

In RFM analysis, we observe a recency range of 0 to 700 days, with most customers falling below 250 transactions in frequency and total monetary spend typically less than $10,000,000.


#### Quantile Segmentation
After calculating the RFM values, we determine quantiles for each metric. These quantiles allow us to assign R, F, and M scores to each customer based on their respective RFM values. Customers with lower Recency values receive higher R scores, while those with higher Frequency and Monetary values receive higher F and M scores, respectively.

We then combine the R, F, and M scores to calculate the total RFM score for each customer. Based on these scores, we define customer segments as below: 
-	Low Spender: total RFM score <= 6
-	Promising: total RFM score <= 9
-	High Spender: total RFM score <= 11 
-	Champion: total RFM score > 11 

Customers are then assigned to a segment according to their total RFM score.

![DSB_Customer_Groups]({{ site.baseurl }}/figure/DSB_Customer_Groups.png)

The analysis indicates that there are fewer high spenders compared to low spenders,  signifying a potential focus area for targeted strategies aimed at elevating spending levels among this segment.

### MBA (Market Basket Analysis)
Market Basket Analysis (MBA) is a statistical technique utilized by retailers to glean insights into customers' purchasing behavior, aiding in informed decisions regarding product placement and marketing strategies. Implemented through the Apriori algorithm, MBA identifies frequent itemsets within transactional data and generates association rules to capture item co-occurrence patterns. By converting transactional data into a one-hot encoded format, we identified frequent itemsets with support greater than a specified threshold of 0.03 to ensure a balance between capturing general trends (by including itemsets with relatively low support) and identifying specific patterns (by excluding itemsets with very low support). Furthermore, with the large size of our datasets, a lower support (i.e 0.03) is more appropriater to capture customer behaviour

Association rules were then generated based on these itemsets, utilizing the lift metric to measure association strength. Filtering based on support and lift thresholds yielded actionable rules. Visualized through a heatmap, confidence levels revealed strong associations between items for different customer segments, such as a 0.71 confidence level for low spenders, indicating a 71% chance of purchasing consequent items given antecedent items. Similarly, for the Promising segment, a confidence of 0.53 meant that given a transaction containing the antecedent items, there is a 53% chance that the same customer will also buy the consequent items. Conversely for the High Spenders and Champions, there was a confidence of 0.34 and 0.28 instead, suggesting that High Spenders or Champions usually had more diverse shopping habits.
 
![DSB_AR_Low_Spender]({{ site.baseurl }}/figure/DSB_AR_Low_Spender.jpg)     ![DSB_AR_Champion]({{ site.baseurl }}/figure/DSB_AR_Champion.jpg)

### Recommendation System
Expanding upon the RFM and Market Basket Analysis groundwork, we endeavored to develop a recommendation system tailored to customers with prior transactions, segmented accordingly. To achieve this, we devised two distinct functions: one for initial item recommendations and another for subsequent item suggestions.

The first_item() function offers guidance on the first item a customer might consider, leveraging their past purchases and the association rules derived from market basket analysis. By examining the antecedents of these rules, the function identifies relevant product groups, removes duplicates, and recommends the top articles associated with those groups.

Similarly, the second_item() function proposes subsequent items based on a customer's existing cart contents and past purchasing behavior. It cross-references the cart's product groups with the association rules, retrieves consequents where applicable, and suggests top articles associated with those groups. If the cart is empty, the function defaults to the first_item() recommendation. Moreover, if only one item is in the cart, it suggests top articles aligned with that item's product group.

Additionally, we introduced a recommender function aimed at enhancing the customer experience. Upon inputting their customer ID, the method determines the user's customer group based on their transaction history. If the user lacks prior purchases, the program notifies them that no recommendations are available. However, for returning customers, the system utilizes market basket analysis to propose items for their cart. By generating potential item combinations and aligning with the customer group's purchasing tendencies, we optimize the cart's contents while introducing additional items tailored to their preferences.

Please refer to the comprehensive analysis provided in the Jupyter notebook available on our GitHub repository. You can access the detailed findings and methodologies with below link. 
<p><a href="https://github.com/widyayutika/Recommendation-System-for-Retail-Product/blob/main/Project_Group8_final.ipynb">Project Analysis - Jupyter Notebook</a></p>

## Limitation and Data Governance
Bias must be addressed to ensure the accuracy and fairness of recommendations, as content, algorithmic, and user biases can impact user trust and engagement, potentially reducing revenue.

Data governance is crucial to ensure accurate, reliable, and transparent data usage while protecting customer privacy. Privacy, data quality, accessibility, and compliance with relevant laws like PDPA must be carefully managed.

## Data Provenance

Documenting data management processes improves accountability, trustworthiness, and customer loyalty by ensuring traceability and transparency in decision-making. This includes documenting data sources, processing steps, feature selection, model training, evaluation, and ethical considerations.

## Closed Loop Analysis

Collecting customer feedback and analyzing new data is essential for continuously improving the recommendation system's effectiveness. Monitoring performance metrics like click-through rates and revenue enables adjustments to optimize the system over time.

## Conclusion

In conclusion, our implemented project analyzes H&M's customer buying patterns through RFM analysis and utilizes association rule mining to create a personalized product recommendation system. This data-driven approach enhances sales, customer loyalty, transaction quantity, and revenue for H&M. Continuous evaluation and refinement ensure adaptation to evolving customer preferences, maintaining competitiveness in the market.