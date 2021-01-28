# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project : Capstone
​
### Problem Statement
> Over the last 30 years, diabetes prevalence and incidence in the United States have been rising steadily, which has put the American people in an ever-worsening public health crisis. Combining California diabetes prevalence data from 2012-2018, alongside state-level diabetes indicator survey data, I plan to conduct a time series analysis and train models to predict future California diabetes prevalence rates. These predictions should inform policy on how to best allocate funds for diabetes prevention/awareness.
​

---
### Loaded Datasets (Plan to Use)
* [ca-diabetes-per-100.csv](https://github.com/gabecano4308/Capstone-Project/blob/main/Data/ca-diabetes-per-100.csv)
* [diabetes_indicators.csv (the csv on GitHub is too big to display right now, will eventually narrow down the data)](https://chronicdata.cdc.gov/Chronic-Disease-Indicators/U-S-Chronic-Disease-Indicators-Diabetes/f8ti-h92k/data)
* [diabetes_prevalence.csv](https://github.com/gabecano4308/Capstone-Project/blob/main/Data/diabetes_prevalence.csv)
​
---
### Other Sources That Could Be Useful​
* [Diabetes Prevalence (pdfs and tables)](https://www.cdc.gov/nchs/hus/contents2018.htm?search=Diabetes,)
* [Diabetes Prevalence csv (only up to 2006)](https://catalog.data.gov/dataset/selected-trend-table-from-health-united-states-2011-diabetes-prevalence-and-glycemic-contr)
* [2020 National Diabetes Statistics Report](https://www.cdc.gov/diabetes/pdfs/data/statistics/national-diabetes-statistics-report.pdf)
* [Diabetes 2030](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5278808/)


​
​
---
​
<!-- ### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
​
​
---
​
### Analysis Summary
​
​
​
---
​
### Conclusions & Considerations
​
​Given Covid case counts and average temperature as variables, the rolling ARIMAX model gives lower prediction errors than the VAR model

Health administrators in DC should leverage the ARIMAX model to identify which Wards are more likely to have spikes in new cases, in order to more efficiently allocate the healthcare resources at hand.


---

### Further Research and Data to Gather

* Looking forward, some potentially valuable additions I'd like to make to this project include:
- Adding average income per Ward as a variable
- Spending more time tinkering with hyperparameters
- Making a Tableau dashboard

---
​
### Sources Cited:

* https://opendata.dc.gov/datasets/dc-covid-19-cases-by-ward/data
* https://khn.org/morning-breakout/critical-bed-shortages-in-u-s-hospitals/

* https://www.nbcwashington.com/news/local/coronavirus-in-dc-maryland-virginia-what-to-know-on-dec-22/2517745/
