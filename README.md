# Predicting Covid Case Counts per Ward in Washington, DC
​
### Background and Problem Statement
> COVID-19 is the most devastating pandemic to emerge in the past century, causing millions of human deaths worldwide, as well as lasting economic and psychological damage for countless more. As of January 22, the U.S. Government has begun distributing a promising vaccine to the American public, but Coronavirus cases are still spiking -- this is especially true in the Washington, DC area, where ICU beds were over 75% full at the beginning of 2021. Focusing on DC, if healthcare administrators could better predict which areas of the city were going to receive more positive cases, they could better allot resources to provide infected patients the attention they need.

> To tackle this issue, I extracted data on reported daily positive cases in DC for each of its eight Wards, as well as daily average temperatures over that same time span. I then fitted a variety of Auto Regressive Integrated Moving Average models with temperature as an exogenous variable (ARIMAX) as well as a Vector Auto Regressive model (VAR) on the data to forecast the count of daily cases per Ward.

---

### Contents
| Notebook | File Name | Description |
|----|----|----|
|**1**|[1_EDA_DC_Covid.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/1_EDA_DC_Covid.ipynb)|Data collection using Petfinder API and Petpy wrapper. Data cleaning and feature engineering. EDA, exploratory LogReg and TFIDF model|
|**2**|[2_Feature_Engineering.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/2_Feature_Engineering.ipynb)|LogReg, Bagging Classifier, Random Forest, AdaBoost and XGBoost Models|
|**3**|[3_Baseline_Modeling.ipynb](https://github.com/jessicabow/Capstone/blob/main/3-FeatureUnion.ipynb)| TFIDF (ordinal) and LogReg (numerical) Feature Union Model + Misclassification DataFrame Creation|
|**4**|[4_ARIMAX_Modeling.ipynb](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/4_Baseline_Modeling.ipynb)|Post Modeling + Misclassification EDA (in support of Tableau visuals)|
|**5**|[5_VAR_Modeling.ipynb](https://github.com/jessicabow/Capstone/blob/main/4-Inference.ipynb)|Post Modeling + Misclassification EDA (in support of Tableau visuals)|
|**6**|[6_Predicting_Covid_Cases_DC.pdf](https://github.com/gabecano4308/Predicting-Covid-Case-Counts-in-Washington-DC/blob/main/7_Predicting_Covid_Cases_DC.pdf)|Post Modeling + Misclassification EDA (in support of Tableau visuals)|

---

### Analysis and Summary​

Ward 3 has the most days in the lower 0-5 reported cases range, while other Wards have more varied distributions. In Ward 4 for instance, about 30-41 cases were reported in one day on almost 20 occasions.

We know Winter months lead to increased cases since more people are going indoors. Indoor crowds make spreading easier.

---
### Datasets
* [dc_covid_cases_by_ward.csv](link to GitHub)
* [tot_cases_per_ward_df.csv](link to GitHub)
* [net_new_daily_cases.csv](link to GitHub)
* [temp_stats.csv](link to GitHub)
* [engineered_df.csv](link to GitHub)
* [model_df.csv](link to GitHub)
* [model_df_sc.csv](link to GitHub)
* [model_df_sc_diff.csv](link to GitHub)
​
---

<!-- ### Data Dictionary
|Features|Type|Description|
|---|---|---|
|Ward_1_Cases, Ward_2_Cases, etc. up to 8|Float|Daily number of new COVID cases per Ward of DC.|
|Ward_1_Cases_1M_Avg, Ward_2_Cases_1M_Avg, etc. up to 8|Float|One month rolling average for the daily number of new COVID cases per Ward of DC (first 30 values are NA).|
|Ward_1_Cases_2M_Avg, Ward_2_Cases_2M_Avg, etc. up to 8|Float|Two month rolling average for the daily number of new COVID cases per Ward of DC (first 60 values are NA).|
|Ward_1_Cases_Shift_M, Ward_2_Cases_Shift_M, etc. up to 8|Float|Daily number of new COVID cases per Ward of DC, shifted backward one month (first 30 values are NA).|
|Ward_1_Cases_Shift_2W, Ward_2_Cases_Shift_2W, etc. up to 8|Float|Daily number of new COVID cases per Ward of DC, shifted backward two weeks (first 14 values are NA).|
|Avg_Temp|Float|Average daily temperatures in the DC area from April 1 to January 18.|

<!-- --- -->

---

### Conclusions & Considerations
​
​Given Covid case counts and average temperature as variables, the rolling ARIMAX model gives lower prediction errors than the VAR model.

Health administrators in DC should leverage the ARIMAX model to identify which Wards are more likely to have spikes in new cases, in order to more efficiently allocate the healthcare resources at hand.

---

### Further Research and Data to Gather

- Including average income per Ward as an exogenous variable, since there appears to be a negative correlation between socioeconomic status and COVID cases.
- Creating a Tableau dashboard to interactively analyze current data and make predictions.

---
### Data Sources:

* Data on DC COVID-19 Cases by Ward was taken from [Open Data DC's website](https://opendata.dc.gov/datasets/dc-covid-19-cases-by-ward/data).
* Data tables on daily average temperatures in the DC area were copied from [Weather Underground's website](https://www.wunderground.com/history/daily/us/va/arlington-county/KDCA).

#### Other Sources Cited:

* [KHN - Critical Bed Shortages in US Hospitals](https://khn.org/morning-breakout/critical-bed-shortages-in-u-s-hospitals/)
* [NBC Washington - DMV COVID Updates](https://www.nbcwashington.com/news/local/coronavirus-in-dc-maryland-virginia-what-to-know-on-dec-22/2517745/)
