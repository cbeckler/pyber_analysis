# PyBer with Matplotlib

## Overview of Project

### Purpose

The analyst was asked to perform an exploratory analysis on data for a rideshare app named PyBer, with the goal of determining if there were any differences in metrics between urban, suburban, and rural cities. Five key metrics were calculated for the overall data: Total Rides, Total Drivers, Total Fares($), Avg Fare per Ride, and Avg Fare per Driver. Addtionally, a longitudinal analysis was done to track the total fare amount by week.

The complete analysis can be found [here](https://github.com/cbeckler/pyber_analysis/blob/main/PyBer_Challenge.ipynb).

### Results

To get the overall stats, a simple aggregation was performed on the PyBer data, grouping by city type. Before the aggregation, the driver count per city was unduplicated so that the total drivers for each city would only be present in one row for each city per type. While each city should show up only in type each, counting it in each type it appears in is a good way to check for data errors, since then the overall count of unduplicated cities would be too high. After the driver count unduplication, the aggregation was performed as:

```
pyber_summary_df = pyber_data_df.groupby('type').agg({'ride_id':'count',
                                                      'driver_undup':'sum',
                                                      'fare':'sum'})
```
After that, the per ride and per driver averages were found by dividing the relevant aggregated columns to create new columns. The final results were:

![PyBer Summary Results](https://github.com/cbeckler/pyber_analysis/blob/main/Resources/summary_results.png)

From this, a few things are clear:
* The largest proportion of rides comes from urban cities, with just over 68% of the sample.
* The largest amount of fare revenue also comes from urban cities, with a similar proportion of roughly 63% of the sample.
* Likewise, most drivers operate in urban cities, with nearly 81% of the sample.
* While urban areas are the top for both number of rides and drivers, the proportion for drivers is larger than the proportion for rides, which is reflected in the average fare per driver, where urban cities are lowest by far, not even making half as much per driver as suburban areas, and less than a third of what rural drivers bring in.
* The average fare per ride follows the same trend, decreasing as area populations increase, but the trend is less dramatic.

A longitudinal analysis was then performed to see how total fare amount varied by week from January through May of 2019, based on the date the ride was taken. The results may be seen in this visualization:

![Total Fare by City Type line chart](https://github.com/cbeckler/pyber_analysis/blob/main/analysis/PyBer_fare_summary.png)

Some conclusions from this data:
* Corroborating the previous analysis, it is clear that the total fare amount is highest for urban cities, lowest for rural cities, and in between for suburban cities.
* For all three cities types, there was a peak in fares in late February. 
* Urban city fares fell sharply going into May.
* Though there was week to week change, within each month period fares stayed relatively flat, generally within the same $5k band. This indicates that while there may be some weekly volatility, fares may be relatively consistent on a montly basis.

## Summary

Based on these findings, the analyst would be make three recommendations to address disparities amoung city types:
1. Because rural drivers bring in the highest fare per driver by far, the analyst would recommend focusing driver recruitment campaigns in rural areas.
2. Because suburban fares per ride and fares per driver are generally higher than low fare ratio urban areas, while the total number of rides in the suburbs is 5 times higher than the high fare ratio rural areas, campaigns to increase both drivers and rides in suburban cities would likely yield a substantial increase in profits.
3. As urban cities are still the group with the highest number of rides and total fare amount, investigating why fares dropped in May may yield ways to minimize loss. 

Additionally, the analyst has two recommendations for further analyses:
1. Adding ride miles to the data, so that an analysis of miles per ride and fare per mile could be performed. It may be the urban cities have the lowest fare per ride ratio because rides are generally shorter, with cities generally having locations closer together.
2. Adding addtional years to the longitudinal weekly analysis of fares, to track whether the trends seen in the data persist over longer periods of time.
