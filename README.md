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
| OUTAGE.DURATION | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL | NERC.REGION | CLIMATE.REGION     | ANOMALY.LEVEL | YEAR | RES.PERCEN | OUTAGE.START        | OUTAGE.RESTORATION   |
|------------------|--------------------|-----------------------|-------------|--------------------|---------------|------|------------|---------------------|----------------------|
|             3060 | severe weather     | nan                   | MRO         | East North Central |          -0.3 | 2011 |     35.5491 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00 |
|                1 | intentional attack | vandalism             | MRO         | East North Central |          -0.1 | 2014 |     30.0325 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00 |
|             3000 | severe weather     | heavy wind            | MRO         | East North Central |          -1.5 | 2010 |     28.0977 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00 |
|             2550 | severe weather     | thunderstorm          | MRO         | East North Central |          -0.1 | 2012 |     31.9941 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00 |
|             1740 | severe weather     | nan                   | MRO         | East North Central |           1.2 | 2015 |     33.9826 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00 |

## Exploratory Data Anaylsis

