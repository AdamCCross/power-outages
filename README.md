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
  width="800"
  height="600"
  frameborder="0"
></iframe>

Another variable of intrest is outage duration
<iframe
  src="assets/outage_duration_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis

This section contains the most significant relationships between outage duration and other variables.

The average power outage duration can be seen as trending down over time.
<iframe
  src="assets/outage_duration_time_change.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The duration of a power outage appears connected to the cuase of the outage. Severe weather has the highest median duration.
<iframe
  src="assets/outage_duration_cuase_category.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The duration of a power outage also appears associated with the day of the week the outage begins on. Days on the weekend seems to have a longer outage duration.
<iframe
  src="assets/outage_duration_weekday.html"
  width="800"
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


## Assessment of Missingness

### Not Missing at Random Analysis

Many of the columns in the dataset contain missing columns. One of these columns whose missingness could be interpreted as not missing at Random (NMAR) would be DEMAND.LOSS.MW. This column records the amount of peak demand lost during an outage event (in Megawatt), but in many observations it is actually the total demand lost reported. It is likely MNAR because the value in this column, including wiether it is missing, is likely dependent on data itself and where it came from. This data could be beter explained and potionally identified as missing at random (MAR) through the included provision of which utility is reporting each outage in the dataset.

### Missingness Dependency

To test missing dependency I will examin the distribution of OUTAGE.START Day of Week and NERC.REGION against OUTAGE.DURATION missingness.

#### Day of Week

Examine the distribution of OUTAGE.START Day of Week when OUTAGE.DURATION is missing vs. not missing.

<b>Null Hypothesis</b>: The distribution of Day of Week is the same when Duration is missing vs. not missing

<b>Alternate Hypothesis</b>: The distribution of Day of Week is different when Duration is mising vs. not missing

<iframe
  src="assets/weekday_missingness_dep.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

An observed TVD value of 0.08 was found with a p-value of 0.64. The empirical distribution fo the TVDs is shown below. At the given p-value, I fail to reject the null hypothesis that distribution of Day of Week is the same when Duration is missing vs. not missing. This indicates the missingness of OUTAGE.DURATION is not dependent on the day of the week for OUTAGE.START.

<iframe
  src="assets/weekday_missingness_TVD_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### NERC Region

Examine teh disribution of NERC.REGION when OUTAGE.DURATION is missing vs. not missing.

<b>Null Hypothesis</b>: The distribution of NERC.REGION is the same when OUTAGE.DURATION is missing vs. not missing

<b>Alternate Hypothesis</b>: The distribution of NERC.REGION is different when OUTAGE.DURATION is mising vs. not missing

<iframe
  src="assets/NERC_missingness_duration_dep.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

An observed TVD value of 0.14 was found with a p-value of 0.04. The empirical distribution fo the TVDs is shown below. At the given p-value, I reject the null hypothesis in favor of the alternate hypothesis. This indicates the missingness of OUTAGE.DURATION is dependent on the NERC Region in NERC.REGION.

<iframe
  src="assets/NERC_missingness_TVD_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>