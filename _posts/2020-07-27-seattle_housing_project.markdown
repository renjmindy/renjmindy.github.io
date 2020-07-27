---
layout: post
title:      "Mutiple Linear Regression and Model Validation: "
date:       2020-07-27 16:43:01 -0400
permalink:  seattle_housing_project
---

## Seattle Housing Project 

I would like to utilize this data to study home buyers' decision-making behaviors. That is, I try to interpret customer purchase behavior by digesting data, building model and applying model fitting with cross-validation and . 

To begin with, we ask one question prior to data exploration: What're major factors that may make impact on house buyers' behaviors? We list them as follows:

1. house location

    *  weather factor

    *  daily commute time, road condition and traffic safety

    *  neighborhood quality, e.g. ethics, religion, immigration backgrounds, political parties, education level, salary range, career/occupation and ages

    *  school district for kid education

    *  community life, convenience and entertainment, e.g. close to church, hospital, gym, national state park, fishing area, dairy food farms and so on

    *  cime rate

2. house age

   *  when it was built

   *  has it ever been renovated?

   *  house grade based on the King County grading scale system 

3. house size

  *  interior 

  *  ratio of interior to overall (exterior included)

  *  family size

4. house design

  *  floor plan

  *  with or without basement?

5. house amenities

  *  pool nearby?

6. house price

  *  home buyer's economic capability

  *  home buyer's health condition

  *  home buyer's age range or generation

  *  home buyer's intension to be a landlord of the house (monthly rental fee)

  *  annual tax payment

  *  renovation/maintenance expanses included?

  *  loan option for specific groups

  *  discount deal/offer for specific groups and seasons

[Fig1](https://github.com/renjmindy/dsc-mod-2-project-v2-1-onl01-dtsc-ft-052620/blob/master/image/mod2_motivation_final_submit_alt.png) demonstrates relations between these selected factors and house selling price. In addition to that, we could also see how likely these factors are correlated to each other. All selective factors that could help us study home buyers' purchase behaviors are expected to be as more independent to each other as possible. Otherwise, if there exists a certain level of correlation among a handful of factors that were fed into the model, varying one of them will lead to changes on other dependent ones, and the modeling fit result won't be reliable any longer, accordingly. 

Through multiple linear regression model by feeding into a bag of deliberate factors as summarized in [Fig2](http://https://github.com/renjmindy/dsc-mod-2-project-v2-1-onl01-dtsc-ft-052620/blob/master/image/mod2_model_final_submit_alt_coefs.png) with explanations in text below, we achieved a moderate fitting result as displayed in [Fig3](http://https://github.com/renjmindy/dsc-mod-2-project-v2-1-onl01-dtsc-ft-052620/blob/master/image/modelSummary_final_submit_alt_1.png). Prior to the removal of *uninfluential* factors from the model fit, [Fig4](http://https://github.com/renjmindy/dsc-mod-2-project-v2-1-onl01-dtsc-ft-052620/blob/master/image/mod2_model_final_submit_alt_All_coefs.png) shows all factors taken into consideration, whether they are influential or not.

Here, we explain each factor's definition. These factors manifests strong enough statistics significance, so that they pass the cut on p-Value, based on F-statistics, by requiring p-Value be less than 0.05, indicating a 95% confidence level of floating range around the central value for each given factor described below.

1. 'sqft_above_log' (**Top15**): house interior area

2. 'AvgAreaPerRm_log': average room size (bathrooms and bedrooms both included)

3. 'zipcode_lat_log' (**Top15**): house zipcode divided by latitudinal coordinate

4. 'zipcode_long_log': house zipcode divided by longitudinal coordinate

5. 'yrgrade_built_log': linear combination of house built year and its grade

6. 'floors' (**Top15**): house design (multiple levels above house basement)

7. 'waterfront' (**Top15**): whether there is pool outside/surrounding house or not

8. 'view' (**Top15**): frequencies of house tour

9. 'condition' (**Top15**): house maintenance and/or renovation construction

10. 'hasbasement' (**Top15**): with or without basement, i.e. ground level

11. 'hasbiggerllratio': ratio of liviing area to lot's compared to that obtained by averaging over 15 nearest neighbors'

12. 'hasreno4sale': difference in years (time length) between house sold and when the renovation took place

13. 'yrmo_sold': house sold year and month combined
 
 
To check for the normality assumption, you can obtain error terms (residuals) from the model and draw Q-Q plot against a standard normal distribution as shown in [Fig5](http://https://github.com/renjmindy/dsc-mod-2-project-v2-1-onl01-dtsc-ft-052620/blob/master/image/mod2_model_final_submit_alt_qq.png). While the residuals do not seem to match up perfectly with the red line, there seem to be no super clear deviations from the red line. So you can assume that you're OK for the normality assumption. Moreover, homoscedasticity in [Fig6](http://https://github.com/renjmindy/dsc-mod-2-project-v2-1-onl01-dtsc-ft-052620/blob/master/image/mod2_model_final_submit_alt_homo.png) indicates that a dependent variable's variability is equal across values of the independent variable. A scatter plot is good way to check whether the data are homoscedastic (meaning the residuals are equal across the regression line).

Two EDA questions are now clear to be answered. The first EDA question is "*What are influential factors on frequencies of house tour*?" **Season** matters! The second EDA question is "*What are influential factors on house buyers' decision-making behaviors*"? **House** itself! 

Prior to EDA, outliers were removed by getting rid of data points sitting outside 3 sigma regions of one normal distribution. Here, the size of 3 sigma is determined by subtracting 1.73 times IQR from first 25% of factor size and adding 1.73 times IQR to last 25%, i.e. first 75% or third 25%, of factor size. IQR stands for *interquartile range*. IQR is obtained by taking the difference between 75% and 25% of factor size. That is, IQR is the first 25% subtracted from third 25% (or first 75%). Generally speaking, we have been aware of the fact that the housing price is primarily influenced by its interior area. Therefore, we categorized data into various groups such as sold seasons and frequency of house tour. We would like to see how significantly the house selling price varies with interior area under different season and frequency tours.

In first EDA question study, we noticed that different seasons make impact on house selling price and the willingness of joining house tours as well. We also noticed the house condition, location and age (built-year/grading) also affect house buyers to participate in house tours. Three recommendations are listed as follows:

  * house condition score

  * house location

  * house age (built-year related grade scale)

  * house amenities (pool)

To quantify our observations, a list of future work are needed.

  * relate condition score to time lenth spanned from renovation to house sold year (house maintenance)

  * relate zipcode to city name (house location)

  * relate house age to grading scale released by King county house grading system

Moreover, in second EDA question study, the analysis procedure is the same as the one applied to answering first EDA question. Unlike factors used to interpret home buyers' decision-making behaviors, two additional factors play primary role. They are:

  * House design (floor plan)

  * House maintenance (additional renovation)


