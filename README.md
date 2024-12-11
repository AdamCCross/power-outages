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