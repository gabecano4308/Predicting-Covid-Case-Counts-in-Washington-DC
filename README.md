# Predicting COVID-19 Case Counts per Ward in Washington, DC

### Background and Problem Statement
> COVID-19 is the most devastating pandemic to emerge in the past century, causing millions of human deaths worldwide, as well as lasting economic and psychological damage for countless more. As of January 22, the U.S. Government has begun distributing a promising vaccine to the American public, but Coronavirus cases are still spiking -- this is especially true in the Washington, DC area, where ICU beds were over 75% full at the beginning of 2021. Focusing on DC, if healthcare administrators could better predict which areas of the city were going to receive more positive cases, they could better allot resources to provide infected patients the medical attention they need.

> To tackle this issue, I extracted data on reported daily positive cases in DC for each of its eight Wards, as well as daily average temperatures over that same time span. I then fitted a variety of Auto Regressive Integrated Moving Average models with temperature as an exogenous variable (ARIMAX) as well as a Vector Auto Regressive model (VAR) on the data to forecast the count of daily cases per Ward.



---

### Contents
| Notebook | File Name | Description |
|----|----|----|
|**1**|[1_EDA_DC_Covid.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/1_EDA_DC_Covid.ipynb)|COVID-19-related data collection, cleaning, and visual analysis.|
|**2**|[2_Feature_Engineering.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/2_Feature_Engineering.ipynb)|Temperature-related data collection, checking for shifted time and rolling average trends, and standardizing the scale of the variables.|
|**3**|[3_Baseline_Modeling.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/3_Baseline_Modeling.ipynb)|Baseline model creation to compare score efficacy against ARIMAX and VAR models.|
|**4**|[4_ARIMAX_Modeling.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/4_ARIMAX_Modeling.ipynb)|Standard and rolling prediction ARIMAX modeling -- Augmented Dickey Fuller testing to determine stationarity, grid searching for optimal p and q values per Ward.|
|**5**|[5_VAR_Modeling.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/5_VAR_Modeling.ipynb)|Rolling prediction VAR model including all 8 Wards and temperature variables.|
|**6**|[6_Presentation.pdf](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/6_Presentation.pdf)|Google Slides pdf for presenting key findings to stakeholders.|

---

### Analysis and Summary​

The below graph shows the cumulative number of reported positive COVID-19 cases in each Ward of Washington, DC. The graph shows an initial spike in reported cases from March to May (the early months of the pandemic), followed by a gradual flattening through the Summer months, and finishing with a more prolonged spike during the last three Winter months. Seeing a pattern of increased cases during colder months, I decided to add daily average temperature to the dataset and use it as an exogenous variable in the time series models.

![Aggregated](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/Images/1_EDA_DC_Covid_cell_32_output_0.png)

I wanted the time series models to predict net-new reported daily cases as opposed to the cumulative total, so I differenced the dataset to obtain that information. The below graph shows the differenced data for Ward 7 along with its one-month average and average regional temperatures. Similarly to the aggregated plot, one can see increased daily cases during the first few and last few months, as well as a decrease through the Summer. The temperature tends to rise as the case rate drops, as confirmed with a moderately negative correlation between temperature and all Ward case rates, displayed in the below correlation Heatmap.

![Net New Daily and Temp](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/Images/2_Feature_Engineering_cell_24_output_0.png)


![Heatmap](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/Images/2_Feature_Engineering_cell_19_output_0.png)


To construct a baseline time series model, I used the Persistence Algorithm, which simply uses the previous value from the day before to predict the following day, as described in Jason Brownlee's blog post on [Machine Learning Mastery](https://machinelearningmastery.com/persistence-time-series-forecasting-with-python/#:~:text=Persistence%20Algorithm%20(the%20%E2%80%9Cnaive%E2%80%9D%20forecast)&text=The%20equivalent%20technique%20for%20use,step%20(t%2B1).). Using this baseline, I calculated RMSE for each DC Ward in order to compare against the other time series models' RMSEs.   

After conducting an Augmented Dickey Fuller test to determine the stationarity of all data at d = 2, I grid searched for the p and q values that would provide the lowest Akaike Information Criterion (a commonly used estimator of prediction error), per Ward. I then ran the ARIMAX models with these p, q, and d values fitted with the corresponding training set of the Ward data. THE 'X' in ARIMAX stands for the model's exogenous variable, which in this case is daily average temperature.

For each Ward, I first used ARIMAX to forecast the test set values in one run. Then, I created 'Rolling' ARIMAX models, which forecast the test set values through the iterative process of 1) predicting the following observation, 2) adding the observation to the training set, 3) running the model with the updated training set, and 4) adding the new observation to training, repeating the process until all test set values are forecasted. Below are two subplots showing the train and test data for Ward 4, along with the forecasted values in green, for the one-time predictions and the rolling predictions.

#### ARIMAX Model Prediction Results (One-Time and Rolling)
![ARIMAX](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/Images/4_ARIMAX_Modeling_cell_49_output_0.png)

In addition to creating multiple ARIMAX models for each Ward in DC, I was interested in using a single Vector Autoregression model (VAR). VAR is a multivariate time series model that can take the changes of all included endogenous variables into account. Similarly to the ARIMAX modeling process, ran the Augmented Dickey Fuller test and differenced the data once. I employed a rolling prediction method, iteratively fitting a VAR model with training data updated with each one-step forecast. Below is a plot showing the train and test data for Ward 5, along with the rolling forecasted values in green.

#### VAR Model Prediction Results
![VAR](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/Images/5_VAR_Modeling_cell_24_output_0.png)

RMSE scores for each model type are laid out below. Overall, every model performed better than the baseline, with the exception of the ARIMAX (One-Time) models for Wards 5 and 7. Overall, the rolling ARIMAX RMSE models gave the lowest errors.

#### RMSE Results per Model Type
| DC Ward | Baseline RMSE | ARIMAX RMSE (One-Time) | ARIMAX RMSE (Rolling) | VAR RMSE |
|----|----|----|----|----|
|Ward 1|17.0|16.6|12.6|13.2|
|Ward 2|19.4|14.0|12.3|13.7|
|Ward 3|9.1|7.1|6.7|7.0|
|Ward 4|23.9|19.9|16.3|18.7|
|Ward 5|24.4|25.4|18.4|18.0|
|Ward 6|22.1|19.1|16.4|17.3|
|Ward 7|23.1|24.1|15.7|17.0|
|Ward 8|20.8|16.1|15.4|17.4|

---

### Conclusions & Considerations
​
​Given reported COVID-19 case counts and average temperature as variables, the rolling ARIMAX model gives the lowest prediction errors out of all other created models, beating out the baseline when forecasting errors in every Ward.

Health administrators in DC should leverage the rolling ARIMAX model to identify which Wards are more likely to have spikes in new cases, in order to more efficiently allocate the healthcare resources at hand.

#### Further Research and Data to Gather

- Including average income per Ward as an exogenous variable, since there appears to be a negative correlation between socioeconomic status and COVID-19 cases.
_ Including data on COVID-19 vaccine turnout rates per DC Ward.
- Creating a Tableau dashboard to interactively analyze current data and make predictions.

---
### Data Sources:

* Data on DC COVID-19 Cases by Ward was taken from [Open Data DC's website](https://opendata.dc.gov/datasets/dc-covid-19-cases-by-ward/data).
* Data tables on daily average temperatures in the DC area were copied from [Weather Underground's website](https://www.wunderground.com/history/daily/us/va/arlington-county/KDCA).

#### Other Sources Cited:

* [KHN - Critical Bed Shortages in US Hospitals](https://khn.org/morning-breakout/critical-bed-shortages-in-u-s-hospitals/)
* [NBC Washington - DMV COVID Updates](https://www.nbcwashington.com/news/local/coronavirus-in-dc-maryland-virginia-what-to-know-on-dec-22/2517745/)
* [Machine Learning Mastery - Making Baseline Predictions for Time Series](https://machinelearningmastery.com/persistence-time-series-forecasting-with-python/#:~:text=Persistence%20Algorithm%20(the%20%E2%80%9Cnaive%E2%80%9D%20forecast)&text=The%20equivalent%20technique%20for%20use,step%20(t%2B1).)
* [Machine Learning Plus -- Vector Autoregression (VAR) Comprehensive Guide](https://www.machinelearningplus.com/time-series/vector-autoregression-examples-python/)
