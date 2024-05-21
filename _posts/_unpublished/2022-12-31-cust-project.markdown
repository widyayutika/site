---
layout: post
title:  "Revitalizing Growth: Transforming Strategies for a Leading Haircare Company - Customer Analytics"
date:   2022-04-30 08:00:00 +0800
author: WY
categories: jekyll update
---

## Overview
This page is dedicated to our Customer Analytics project, where our team of 5 experts collaborates to analyze and enhance the sales performance of a leading haircare company in the Asian market. By leveraging data-driven insights and strategic methodologies, we aim to optimize customer engagement, increase repeat purchases, and elevate revenue generation for the brand.

## Objective
Our primary objective is to revitalize the sales performance of the haircare company in the Asian market, particularly in the post-Covid-19 landscape. To achieve this, we intend to implement the RFM (Recency, Frequency, Monetary value) model to segment and target customers effectively. Our key goals include increasing customer repeat purchases, reducing repeat purchase intervals, and maximizing the sales amount of each transaction through targeted marketing strategies.

## Significance
The significance of this project lies in its potential to rejuvenate the haircare company's market presence and profitability amidst changing consumer behaviors and market dynamics. By harnessing the power of customer analytics, we seek to deliver actionable insights that drive sustainable growth, enhance customer satisfaction, and reinforce the brand's position as a leading player in the haircare industry.

## Data Source and Collection

Due to the confidential nature of the data involved, we operate under a non-disclosure agreement (NDA) to ensure the privacy and security of sensitive information.Our data derives from sales transactions, offering valuable insights into customer purchasing behaviors. These transactions are gathered through our proprietary systems and trusted partnerships with authorized data providers. Through rigorous data analysis and interpretation, we extract valuable insights to inform strategic decision-making and drive impactful business outcomes for the haircare company.


## Descriptive Statistics

Utilizing R Shiny interactive platform, we delve into the dataset to explore deeper into the data and uncover interesting patterns (i.e. Crime Occurrence, Victim Demographic, and Geospatial Mapping)

### Crime Occurrence
![Crime Occurrence]({{ site.baseurl }}/figure/ASAR_Crime_Occurrence.png)

From the heatmap above, it was revealed that noon, especially on Mondays, Wednesdays, and Fridays, sees peak crime incidents. Fridays stand out as the most common day for crimes. Crime rates slow down after midnight. Crime types show varied peak periods; for instance, theft is common during the day, burglary at night, and assaults occur throughout the day. These insights aid in deploying targeted crime prevention strategies and optimizing police resources based on peak times and specific crime types.

### Victim Demographic Distribution
Understanding the victim demographics (age, gender, and race) can help identify vulnerable communities that may require increased police protection. 

#### Age Group
![Victim Age Group]({{ site.baseurl }}/figure/ASAR_Victim_Age_Group_Distribution.png)   ![LA Population Age Group]({{ site.baseurl }}/figure/ASAR_LA_Population_Age_Group.png)

Most victims of crime in Los Angeles fall within the 20-29 and 30-39 age groups, this result is not surprising as it matches the LA census data.

#### Gender
![Victim Gender]({{ site.baseurl }}/figure/ASAR_Victim_Gender.png)  ![LA Population Gender]({{ site.baseurl }}/figure/ASAR_LA_Population_Gender.png)

There were more crimes committed against male than female or undisclosed gender. 
NOTES: Victimless crimes are excluded from the analysis.

#### Race/Descent
![Victim Descent]({{ site.baseurl }}/figure/ASAR_Victim_Descent.png)

![LA Population Descent]({{ site.baseurl }}/figure/ASAR_LA_Population_Descent.png)

Crimes against Hispanics/Latinos/Mexicans were the highest, and this is in line with the population of LA, with Hispanics being largest ethnic group (48.2%) in the city. Whereas crimes against Vietnamese and Black people was the second and third highest respectively, even though each group made up less than 12% (Vietnamese is a part of Asian) and 8% of total population in LA. This could be evidence of a community being more vulnerable to crime and warranting increased attention for police protection by the LAPD.

### Geospatial Mapping
![Geospatial Mapping]({{ site.baseurl }}/figure/ASAR_Geospatial_Mapping.png)

This serves as a tool to identify crime hot spots within the city where the users especially LAPD, can use zoom into different areas, filter by date (month, year) and also select to focus on certain crime types (eg. burglary, rape etc.).

## Inferential Statistics
This inferential statistics analysis aims to determine if there are significant differences in crime rates between 2020 and 2021, identify demographic factors associated with crime victimization, and explore relationships between crime categories and demographic variables in Los Angeles.


### Daily Crime Rate
In this section, we aim to determine whether the daily crime rate in 2020 is significantly different from that in 2021. We conducted a two-sample Z-test for two independent populations. The hypotheses are as follows:

Null hypothesis (H0): There is no significant difference in daily crime rates between 2020 and 2021.
Alternative hypothesis (H1): There is a significant difference in daily crime rates between 2020 and 2021.

![Two Samples Z Test]({{ site.baseurl }}/figure/ASAR_Two_Samples_Z_Test.png)

Based on the test results, the p-value was higher than the significance level of 5%, indicating insufficient evidence to reject the null hypothesis. Therefore, we conclude that there is no significant difference in daily crime rates between 2020 and 2021.

Our Shiny App design methodology allows users to update the reactive inputs, filter the data for hypothesis tests, and tweak test parameters such as Confidence Level, Sample Size, and Comparison Direction ('Less', 'Greater', 'two.sided').

Following the hypothesis testing, we also conducted confidence interval analysis on the daily average crime incidents in 2020 versus 2021. 

At a 95% confidence level, the confidence interval for daily average crime rates in 2020 ranged from 516 to 556, while in 2021, it increased to 542 to 568.By knowing this range, the LAPD can better predict daily crime rates and allocate resources accordingly, ensuring they have sufficient personnel and strategies in place to address the expected volume of incidents.

Our Shiny App design methodology allows users to update the reactive inputs (i.e. lower and upper bounds of confidence level and sample size parameters) as shown below.

![Confidence Interval]({{ site.baseurl }}/figure/ASAR_Confidence_Interval.png)

### Monthly Crime Rate among Different Victim Gender
We conducted an ANOVA test to compare the average monthly crime rates across different genders: male (M), female (F), and undisclosed (X). Using ten random samples and a significance level of 5%, the hypotheses were:

Null hypothesis (H0): The averages of monthly crime rates across different genders are equal.
Alternative hypothesis (H1): The averages of monthly crime rates across different genders are not equal.

![ANOVA_Tukey]({{ site.baseurl }}/figure/ASAR_ANOVA_Tukey_Test.png)

The p-value was less than 0.05, leading us to reject the null hypothesis and conclude that there is a significant difference in average monthly crime rates among the genders. Tukey’s test revealed that males have significantly higher crime rates compared to females, with an average difference of 2229.5. Similar analyses showed that males have higher crime rates than undisclosed, and females also differ significantly from undisclosed. Overall, monthly crime rates are highest for males, followed by females, and lastly, undisclosed.

![ANOVA_Shiny]({{ site.baseurl }}/figure/ASAR_ANOVA_Shiny.png)

Our Shiny app empowers users to filter data and conduct ANOVA tests on monthly crime rates across various demographic variables, including Gender, Crime Code, Race, and Area Name. Users can adjust sample sizes and observe results in real time, facilitating detailed analyses and informed decision-making for crime prevention strategies in Los Angeles.

### Association between Key Demographic Variables
We conducted a chi-squared test within Shiny Crime LA to identify potentially significant associations between the key demographic variables. Specifically, we compared Crime Code Category against three other demographic variables: Race, Area Name, and Gender. This analysis allows users to infer associations both across the entire dataset and within granular sub-categories.

At a 5% significance level, the null hypothesis (H0) stated that no association exists between crime category and demographic variable, while the alternative hypothesis (H1) posited an association between them. The app extracts key results, including the significance of the generated p-value from the chi-squared test of association. If the p-value is less than 5%, we reject the null hypothesis, indicating an association between the variables. Conversely, if the p-value is greater than 5%, we conclude that no association is found.

If an association exists, users can easily interpret the results using the cross-tab table, discerning which pairs of variables crime tends to lean towards or away from. This analysis provides valuable insights into the relationships between demographic factors and crime categories, aiding in targeted interventions and resource allocation for crime prevention efforts.

## Conclusion

In conclusion, despite limitations in scope, spanning only two years, and geographical specificity, restricted to Los Angeles, the project underscores crucial recommendations for the LAPD and City Attorney. These include addressing disproportionate impacts on victim demographics and leveraging identified crime patterns for more effective resource allocation. Looking ahead, future work could involve automating dataset updates, integrating secondary demographic data, and expanding the scope beyond Los Angeles.