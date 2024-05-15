---
layout: post
title:  "Statistical Insight and Analysis on Los Angeles Crimes Rates - Applied Statistics Analysis with R"
date:   2024-01-25 17:00:00 +0800
categories: jekyll update
---

## Overview

This page is dedicated to our Applied Statistics Analysis with R project, where our team of 5 members delve into the intricate patterns and trends surrounding crime rates in Los Angeles in 2021. In this data exploration,  we employ statistical methodologies to dissect the dynamics of criminal activities, aiming to provide valuable insights into the challenges faced by the city and potential avenues for improvement.

## Objective

Our primary objective is to utilize applied statistics to understand the nuances of crime rates in Los Angeles. By scrutinizing data from various sources, we aim to unravel the underlying factors contributing to the recent surge in crime, particularly in homicides and shootings, as reported by Mayor Eric Gargetti and Police Chief Michael Moore in January 2022.

## Significance:

Crime is not just a statistic; it's a multifaceted issue with profound societal implications. Through this portfolio, we aim to highlight the significance of applying statistical tools to comprehend crime rates. By doing so, we can identify patterns, correlations, and potential causative factors, ultimately contributing to informed decision-making for crime prevention strategies.


Join us on this statistical journey as we navigate through the numbers and unveil meaningful insights into the complex world of crime rates in Los Angeles.


## Data Source and Collection:

The dataset utilized for this analysis is sourced from the Los Angeles Police Department, accessible through the Los Angeles' Open Data website. It encompasses incidents of crime in Los Angeles, meticulously transcribed from original crime reports spanning the years 2020-2021. 

<p><a href="https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8/about_data">Link to the dataset</a></p>


## Descriptive Statistics
Utilizing R Shiny interactive platform, we delve into the dataset to explore deeper into the data and uncover interesting patterns (i.e. Crime Occurrence, Victim Demographic, and Geospatial Mapping)

![Widya](../figure/Photo_Widya_Tantiya_Yutika.jpg)
### Crime Occurrence
![Crime Occurrence](../figure/ASAR_Crime_Occurrence.png)
From the heatmap above, it was revealed that noon, especially on Mondays, Wednesdays, and Fridays, sees peak crime incidents. Fridays stand out as the most common day for crimes. Crime rates slow down after midnight. Crime types show varied peak periods; for instance, theft is common during the day, burglary at night, and assaults occur throughout the day. These insights aid in deploying targeted crime prevention strategies and optimizing police resources based on peak times and specific crime types.

### Victim Demographic Distribution
Understanding the victim demographics (age, gender, and race) can help identify vulnerable communities that may require increased police protection. 

#### Age Group
![Victim Age Group](figure/ASAR_Victim_Age_Group_Distribution.png)
![LA Population Age Group](figure/ASAR_LA_Population_Age_Group.png){:width="40%"}
Most victims of crime in Los Angeles fall within the 20-29 and 30-39 age groups, this result is not surprising as it matches the LA census data.

#### Gender
![Victim Gender](figure/ASAR_Victim_Gender.png){:width="40%"}
![LA Population Gender](figure/ASAR_LA_Population_Gender.png){:width="40%"}
There were more crimes committed against male than female or undisclosed gender. 
NOTES: Victimless crimes are excluded from the analysis.

#### Race/Descent
![Victim Descent](figure/ASAR_Victim_Descent.png){:width="40%"}
![LA Population Descent](figure/ASAR_LA_Population_Descent.png){:width="40%"}
Crimes against Hispanics/Latinos/Mexicans were the highest, and this is in line with the population of LA, with Hispanics being largest ethnic group (48.2%) in the city. Whereas crimes against Vietnamese and Black people was the second and third highest respectively, even though each group made up less than 12% (Vietnamese is a part of Asian) and 8% of total population in LA. This could be evidence of a community being more vulnerable to crime and warranting increased attention for police protection by the LAPD.

### Geospatial Mapping
![Geospatial Mapping](figure/ASAR_Geospatial_Mapping.png){:width="40%"}
This serves as a tool to identify crime hot spots within the city where the users especially LAPD, can use zoom into different areas, filter by date (month, year) and also select to focus on certain crime types (eg. burglary, rape etc.).


## Inferential Statistics
This inferential statistics analysis aims to determine if there are significant differences in crime rates between 2020 and 2021, identify demographic factors associated with crime victimization, and explore relationships between crime categories and demographic variables in Los Angeles.


### Daily Crime Rate
In this section, we aim to determine whether the daily crime rate in 2020 is significantly different from that in 2021. We conducted a two-sample Z-test for two independent populations. The hypotheses are as follows:

Null hypothesis (H0): There is no significant difference in daily crime rates between 2020 and 2021.
Alternative hypothesis (H1): There is a significant difference in daily crime rates between 2020 and 2021.
![Two Samples Z Test](figure/ASAR_Two_Samples_Z_Test.png){:width="40%"}

Based on the test results, the p-value was higher than the significance level of 5%, indicating insufficient evidence to reject the null hypothesis. Therefore, we conclude that there is no significant difference in daily crime rates between 2020 and 2021.

Our Shiny App design methodology allows users to update the reactive inputs, filter the data for hypothesis tests, and tweak test parameters such as Confidence Level, Sample Size, and Comparison Direction ('Less', 'Greater', 'two.sided').

Following the hypothesis testing, we also conducted confidence interval analysis on the daily average crime incidents in 2020 versus 2021. 


At a 95% confidence level, the confidence interval for daily average crime rates in 2020 ranged from 516 to 556, while in 2021, it increased to 542 to 568.By knowing this range, the LAPD can better predict daily crime rates and allocate resources accordingly, ensuring they have sufficient personnel and strategies in place to address the expected volume of incidents.

Our Shiny App design methodology allows users to update the reactive inputs (i.e. lower and upper bounds of confidence level and sample size parameters as shown below.
![Confidence Interval](figure/ASAR_Confidence_Interval.png){:width="40%"}

### Monthly Crime Rate among Different Victim Gender
We conducted an ANOVA test to compare the average monthly crime rates across different genders: male (M), female (F), and undisclosed (X). Using ten random samples and a significance level of 5%, the hypotheses were:

Null hypothesis (H0): The averages of monthly crime rates across different genders are equal.
Alternative hypothesis (H1): The averages of monthly crime rates across different genders are not equal.

![ANOVA_Tukey](figure/ASAR_ANOVA_Tukey_Test.png){:width="40%"}

The p-value was less than 0.05, leading us to reject the null hypothesis and conclude that there is a significant difference in average monthly crime rates among the genders. Tukey’s test revealed that males have significantly higher crime rates compared to females, with an average difference of 2229.5. Similar analyses showed that males have higher crime rates than undisclosed, and females also differ significantly from undisclosed. Overall, monthly crime rates are highest for males, followed by females, and lastly, undisclosed.

![ANOVA_Shiny](figure/ASAR_ANOVA_Shiny.png){:width="40%"}
Our Shiny app empowers users to filter data and conduct ANOVA tests on monthly crime rates across various demographic variables, including Gender, Crime Code, Race, and Area Name. Users can adjust sample sizes and observe results in real time, facilitating detailed analyses and informed decision-making for crime prevention strategies in Los Angeles.


### Association between Key Demographic Variables
We conducted a chi-squared test within Shiny Crime LA to identify potentially significant associations between the key demographic variables. Specifically, we compared Crime Code Category against three other demographic variables: Race, Area Name, and Gender. This analysis allows users to infer associations both across the entire dataset and within granular sub-categories.

At a 5% significance level, the null hypothesis (H0) stated that no association exists between crime category and demographic variable, while the alternative hypothesis (H1) posited an association between them. The app extracts key results, including the significance of the generated p-value from the chi-squared test of association. If the p-value is less than 5%, we reject the null hypothesis, indicating an association between the variables. Conversely, if the p-value is greater than 5%, we conclude that no association is found.

If an association exists, users can easily interpret the results using the cross-tab table, discerning which pairs of variables crime tends to lean towards or away from. This analysis provides valuable insights into the relationships between demographic factors and crime categories, aiding in targeted interventions and resource allocation for crime prevention efforts.

## Conclusion

In conclusion, despite limitations in scope, spanning only two years, and geographical specificity, restricted to Los Angeles, the project underscores crucial recommendations for the LAPD and City Attorney. These include addressing disproportionate impacts on victim demographics and leveraging identified crime patterns for more effective resource allocation. Looking ahead, future work could involve automating dataset updates, integrating secondary demographic data, and expanding the scope beyond Los Angeles.