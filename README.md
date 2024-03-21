# Introduction

## Background

With people depending more and more on electrical implements inside their homes, power outages become more and more costly. They hinder people who work from their computers from doing any work, limit people's ability to communicate through the internet, and overall halt the daily lives of anyone unlucky enough to get caught. In cases of severe weather or emergency, power outages can even limit access to important utilities or the ability to reach important services. An important thing to know for those affected by outages would be how long outages will last, so that they know when they can return to their normal lives or how long they should be preparing to hunker down for.

## Our Question

In our analysis, we investigated the question: **Which factors contribute the most to the severity of the power outage in terms of outage duration?**

## Our Dataset

To perform this analyis, we used the data from major power outages in the continental United States, ranging from January of 2000 to July of 2016. It contains data on the severity of outages, as well as their start and restoration dates, causes, locations, and more location-specific information. This dataset has 55 variables and 1,534 observations, where each observation corresponds to a different outage.

While there were 55 variables (columns) in the dataset, only a few were relevant to our analysis. These variables, and short descriptions, are listed below:

- `'YEAR'`: The year in which the outage happened
- `'MONTH'`: The month in which the outage happened
- `'U.S. STATE'`: The state in which the outage occured
- `'CAUSE CATEGORY'`: The category of the outage's root cause, out of 7 potential categories
- `'OUTAGE DURATION'`: The duration of the outage, in minutes
- `'CUSTOMERS AFFECTED'`: The total number of people affected by the outage
-
