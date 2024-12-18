# Introduction

In this project, I examin a dataset of all major power outages in the United States
from January 2000 to July 2016. These Outages are determined as major by the U.S.
Department of Energy for having impacted at least 50,000 customers or having caused
an unplanned loss of at least 300 MegaWatts. This data was sourced from Purdue
University and be accessed using the following link: https://engineering.purdue.edu/LASCI/research-data/outages

The goal of this poject will be to develope a greater understanding of power 
outages and the factors most pertient to their duration. If these factors can 
be identified then they can be used to more accurately predict the duration of 
a power outage and potentialy be focused on by utility companies seeking to 
migigate the greatest risk factors to customers access to electricity. 

The rest of this website will detail my exploration of power outage data and
and explain the conclusions I can draw from avaible information.

## Dataset

The Dataset of power outages contains 1,534 different observed power outages
with 57 characteristics recorded for each. Of these 57 characteristics the
following are of particular realvance and will be focused on for the remanider
the project.

| Column  | Description |
|---|---|---|---|
| YEAR | Indicates the year when the outage event occurred | 
| NERC.REGION | The North American Electric Reliability Corporation (NERC) regions involved in the outage event |
| CLIMATE.REGION | U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.) |
| ANOMALY.LEVEL | This represents the oceanic El Niño/La Niña (ONI) index referring to the cold and warm episodes by season. It is estimated as a 3-month running mean of ERSST.v4 SST anomalies in the Niño 3.4 region (5°N to 5°S, 120–170°W) |
| OUTAGE.START.DATE | This variable indicates the day of the year when the outage event started (as reported by the corresponding Utility in the region) |
| OUTAGE.START.TIME | This variable indicates the time of the day when the outage event started (as reported by the corresponding Utility in the region) |
| OUTAGE.RESTORATION.DATE | This variable indicates the day of the year when power was restored to all the customers (as reported by the corresponding Utility in the region) |
| OUTAGE.RESTORATION.TIME | This variable indicates the time of the day when power was restored to all the customers (as reported by the corresponding Utility in the region) |
| CAUSE.CATEGORY | Categories of all the events causing the major power outages |
| CAUSE.CATEGORY.DETAIL | Detailed description of the event categories causing the major power outages |
| OUTAGE.DURATION | Duration of outage events (in minutes) |
| RES.PERCEN | Percentage of residential electricity consumption compared to the total electricity consumption in the state (in %) |


# Data Cleaning and Exploratory Data Anaylsis

Before proceding with more advance anaylsis it is important to understand the 
data and how I have cleaned it.

## Data Cleaning

1. The first cleaning step is deciding which columns in the dataset to keep. The
following columns were those kept for this project: YEAR, NERC.REGION, 
CLIMATE.REGION, ANOMALY.LEVEL, OUTAGE.START.DATE, OUTAGE.START.TIME, OUTAGE.RESTORATION.DATE, OUTAGE.RESTORATION.TIME, CAUSE.CATEGORY, CAUSE.CATEGORY.DETAIL,
OUTAGE.DURATION, RES.PERCEN
2. The second cleaning step is combining columns with complimentary data. The columns OUTAGE.START.DATE and OUTAGE.START.TIME are combined into a singlur new 
OUTAGE.START column that records the day and time an outage begins at. The columns OUTAGE.RESTORATION.DATE and OUTAGE.RESTORATION.TIME are combined into a singlur new 
OUTAGE.RESTORATION column that records the day and time an outage ends at.
3. The third cleaning step is replacing the 0 values in OUTAGE.DURATION with
np.nan as these values are likely indicative of missingness.

Dataset Head:

<div style="overflow-x: auto;">
<pre>
|   OUTAGE.DURATION | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL |   YEAR |   RES.PERCEN | OUTAGE.START        | OUTAGE.RESTORATION   |
|------------------:|:-------------------|:------------------------|:--------------|:-------------------|----------------:|-------:|-------------:|:--------------------|:---------------------|
|              3060 | severe weather     | nan                     | MRO           | East North Central |            -0.3 |   2011 |      35.5491 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|                 1 | intentional attack | vandalism               | MRO           | East North Central |            -0.1 |   2014 |      30.0325 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|              3000 | severe weather     | heavy wind              | MRO           | East North Central |            -1.5 |   2010 |      28.0977 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|              2550 | severe weather     | thunderstorm            | MRO           | East North Central |            -0.1 |   2012 |      31.9941 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|              1740 | severe weather     | nan                     | MRO           | East North Central |             1.2 |   2015 |      33.9826 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |
</pre>
</div>

## Exploratory Data Anaylsis

### Univariate Analysis

This section begins Exploratory Data Anaylsis with the examination of single variable distributions.

It is first important to see how major power outages have been trending in the dataset over time.
<iframe
  src="assets/outages_yearly.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

Another variable of intrest is outage duration
<iframe
  src="assets/outage_duration_dist.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

This section contains the most significant relationships between outage duration and other variables.

The average power outage duration can be seen as trending down over time.
<iframe
  src="assets/outage_duration_time_change.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

The duration of a power outage appears connected to the cuase of the outage. Severe weather has the highest median duration.
<iframe
  src="assets/outage_duration_cuase_category.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

The duration of a power outage also appears associated with the day of the week the outage begins on. Days on the weekend seems to have a longer outage duration.
<iframe
  src="assets/outage_duration_weekday.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

### Grouping and Aggregate

The pivot table below shows the average anomaly level and outage duration for each of the climate regions present in the data. This aggragate grouping reveals how climate region may be an important factor of outage duration.

| CLIMATE.REGION     |   ANOMALY.LEVEL |   OUTAGE.DURATION |
|:-------------------|----------------:|------------------:|
| West North Central |     -0.2375     |           796.071 |
| Northwest          |     -0.00681818 |          1536.36  |
| Southwest          |     -0.0467391  |          1621.41  |
| West               |     -0.0285714  |          1636.31  |
| Southeast          |     -0.135333   |          2247.66  |
| South              |      0.0180617  |          2872.45  |
| Central            |     -0.166332   |          2882.21  |
| Northeast          |     -0.176218   |          3330.52  |
| East North Central |     -0.15942    |          5391.4   |


# Assessment of Missingness

## Not Missing at Random Analysis

Many of the columns in the dataset contain missing columns. One of these columns whose missingness could be interpreted as not missing at Random (NMAR) would be DEMAND.LOSS.MW. This column records the amount of peak demand lost during an outage event (in Megawatt), but in many observations it is actually the total demand lost reported. It is likely MNAR because the value in this column, including whether it is missing, is likely dependent on data itself and where it came from. This data could be beter explained and potionally identified as missing at random (MAR) through the included provision of which utility is reporting each outage in the dataset.

## Missingness Dependency

To test missing dependency I will examin the distribution of OUTAGE.START Day of Week and NERC.REGION against OUTAGE.DURATION missingness.

### Day of Week

Examine the distribution of OUTAGE.START Day of Week when OUTAGE.DURATION is missing vs. not missing.

<b>Null Hypothesis</b>: The distribution of Day of Week is the same when Duration is missing vs. not missing

<b>Alternate Hypothesis</b>: The distribution of Day of Week is different when Duration is mising vs. not missing

<iframe
  src="assets/weekday_missingness_dep.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

An observed TVD value of 0.08 was found with a p-value of 0.64. The empirical distribution fo the TVDs is shown below. At the given p-value, I fail to reject the null hypothesis that distribution of Day of Week is the same when Duration is missing vs. not missing. This indicates the missingness of OUTAGE.DURATION is not dependent on the day of the week for OUTAGE.START.

<iframe
  src="assets/weekday_missingness_TVD_dist.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

### NERC Region

Examine teh disribution of NERC.REGION when OUTAGE.DURATION is missing vs. not missing.

<b>Null Hypothesis</b>: The distribution of NERC.REGION is the same when OUTAGE.DURATION is missing vs. not missing

<b>Alternate Hypothesis</b>: The distribution of NERC.REGION is different when OUTAGE.DURATION is mising vs. not missing

<iframe
  src="assets/NERC_missingness_duration_dep.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

An observed TVD value of 0.14 was found with a p-value of 0.04. The empirical distribution fo the TVDs is shown below. At the given p-value, I reject the null hypothesis in favor of the alternate hypothesis. This indicates the missingness of OUTAGE.DURATION is dependent on the NERC Region in NERC.REGION.

<iframe
  src="assets/NERC_missingness_TVD_dist.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>

# Hypothesis Testing

I tested whether there is a significant difference between outage durations for outages that start at different hours of the day. The relevant columns for this test were OUTAGE.DURATION and OUTAGE.START. This test is used to confirm if the outage start hour will be potenitally useful in predicting OUTAGE.DURATION in the future. 

<b>Null Hypothesis</b>: The median duration of outages in OUTAGE.DURATION is the same for all hours of the day in OUTAGE.START.

<b>Alternate Hypothesis</b>: The median duration of outages in OUTAGE.DURATION differs across hours of the day in OUTAGE.START.

<b>Test Statistic</b>: Mood's Median Test

After conducting this hypothesis test a p-value of 0.00 was found. With a p-value at this level I reject the null hypothesis that the median duration of outages in OUTAGE.DURATION is the same for all hours of the day in OUTAGE.START when using the standard p-value of 0.05 to determine significance. These results indicate the hour an outage begins at could be useful in analysing differences in outage duration across power outages.

# Framing a Prediction Problem

The model in this project will attempt to predict the duration of a power outage (OUTAGE.DURATION). It will be a regression model as its focus will be on predicting a continous variable.

The metric the model will be evaluated on is Root Mean Squared Error (RMSE). This metric was choosen becuase of how it can be used to indicate how far off a prediction is using a unit denominated number. 

At the time of prediction the OUTAGE.START, OUTAGE.CAUSE, OUTAGE.CAUSE.DETIAL, NERC.REGION, and CLIMATE.REGION are some of the known variables.

# Baseline Model

The Baseline Model is a DecisionTreeRegressor built to predict an outage's OUTAGE.DURATION using the hour the outage began in as stored in OUTAGE.START along with CAUSE.CATEGORY and CAUSE.CATEGORY.DETAIL.

Features Used: 

> <b>CAUSE_COMBINED</b>: The combined string values stored in CAUSE.CATEGORY and CAUSE.CATEGORY.DETAIL so that an outage's cuase is treated as one unique feature. It is One-Hot-Encoded as a nominal categorical variable.
>
> <b>HOUR</b>: The hour of the day an outage started at as stored in OUTAGE.START. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's start hour and duration.

The predicted column OUTAGE.DURATION was normalized to mitigate the effects of an extreme right skew. The graph below showcases this transformation's effects on the disribution of OUTAGE.DURATION. 

<iframe
  src="assets/duration_transformation.png"
  width="700"
  height="600"
  frameborder="0"
></iframe>


The performace of this model was not great. It achieved an R<sup>2</sup> of 0.34 and an RMSE value of 4.54. This shows the model fails to capture much of the variance expressed in OUTAGE.DURATION.

# Final Model

The Final Model is a GradientBoostingRegressor built to predict an outage's OUTAGE.DURATION using the hour, day of week, month, and year the outage began in as stored in OUTAGE.START along with CAUSE.CATEGORY, CAUSE.CATEGORY.DETAIL, NERC.REGION, and CLIMATE REGION.

Features Used: 

> <b>CAUSE_COMBINED</b>: The combined string values stored in CAUSE.CATEGORY and CAUSE.CATEGORY.DETAIL so that an outage's cuase is treated as one unique feature. It is One-Hot-Encoded as a nominal categorical variable.
>
> <b>HOUR</b>: The hour of the day an outage started at as stored in OUTAGE.START. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's start hour and duration.
>
> <b>WEEKDAY</b>: The day of week an outage started at as stored in OUTAGE.START. This varible was added becuase the day of week can be indicative of how fast a utility can address an outage. Outages on the weekend tend to take longer. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's start day of week and duration.
>
> <b>MONTH</b>: The month an outage started at as stored in OUTAGE.START. This varible was added becuase the month can be indicative of season and if seanonal factors affect a utilities ability to address an outage. Outages in winter months tend to take longer. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's start month and duration.
>
> <b>YEAR</b>: The year an outage started at as stored in OUTAGE.START. This varible was added becuase the year can account for the slow (on average) trend down in outage durations. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's start year and duration (some years still have higher outage durations, though the trend is down).
>
> <b>NERC.REGION</b>: The NERC region an outage occurs in. This variable was added because the regulatory body in charge of a utility can have an impact on how severe/long an outage can be. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's NERC region and duration.
>
> <b>CLIMATE.REGION</b>: The Climate region an outage occurs in. This variable was added because the climate an outage occurs in can affect how easy it is to address an outage and how extreme tempetures may be. It is One-Hot-Encoded as a nominal categorical variable. This is because a nonlinear relationship exists between an outage's climate region and duration.

The predicted column OUTAGE.DURATION was normalized to mitigate the effects of an extreme right skew. The graph below showcases this transformation's effects on the distribution of OUTAGE.DURATION. 

<iframe
  src="assets/duration_transformation.png"
  width="700"
  height="600"
  frameborder="0"
></iframe>


GridSearchCV was used to find the best hyperparameters for the GradientBoostingRegressor. The best hyperparameters identified were:

- ccp_alpha: 0.01
- max_depth: 5
- min_samples_leaf: 2
- min_samples_split: 10
- n_estimators: 500

The graph of below shows a relatively random distribution of residuals for the prediction model.

<iframe
  src="assets/prediction_residuals.png"
  width="700"
  height="600"
  frameborder="0"
></iframe>

The performace of this model was an improvement upon the base model. It achieved an R<sup>2</sup> of 0.52 and an RMSE value of 3.89. However, this perfomance shows the model fails to capture much of the variance expressed in OUTAGE.DURATION, like the baseline model, with approximately only half of the OUTAGE.DURATION variance accounted for. Further refinements will need to be explored in the future. 

# Fairness Analysis

I tested whether there is a significant difference between outage duration predictions for outages that occur in areas with residential percentages above the median vs. outages that occur in areas with residentail percentages at or below the median. The relevant columns for this test were OUTAGE.DURATION and RES.PERCEN. The evaluation metric is RMSE. This test is used to confirm if the model is fair for areas that all less residential. 

<b>Null Hypothesis</b>: The model's RMSE is the same for areas with residential percentages above the median and for those with residencial percentages below the median.

<b>Alternate Hypothesis</b>: The model's RMSE for areas with residential percentages above the median is significantly different from the RMSE for areas with residencial percentages at or below the median

<b>Test Statistic</b>: Difference in RMSE

After conducting a permutaion test with 10,000 permutations a p-value of 0.69 was found. With a p-value at this level I fail to reject the null hypothesis that the model's RMSE is the same for areas with residential percentages above the median and for those with residencial percentages below the median, when using the standard p-value of 0.05 to determine significance. These results indicate the model is fair for areas regardless of a higher or lower residential percentage.

<iframe
  src="assets/fairness_RMSE_diff.html"
  width="700"
  height="600"
  frameborder="0"
></iframe>