## Note to Suraje- 
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

# Data Cleaning and Exploratory Data Analysis

## Data Cleaning
First some preliminary cleaning: we'll replace all the values that should be missing with NaN. Then, we'll convert all numerical values to floats to have consistency across our dataframe. Finally, we'll make sure all the values make sense, and correct them if not.
The column names currently have periods and underscores instead of spaces. Let's replace these with spaces just to make things look a little prettier.

Here is the head of our dataframe (Only included a few columns):
```py
print(df.head().to_markdown(index=False))
```
|   YEAR | U S STATE   | CLIMATE REGION     |   OUTAGE DURATION | CAUSE CATEGORY     |   CUSTOMERS AFFECTED |
|-------:|:------------|:-------------------|------------------:|:-------------------|---------------------:|
|   2011 | Minnesota   | East North Central |              3060 | severe weather     |                70000 |
|   2014 | Minnesota   | East North Central |                 1 | intentional attack |                  nan |
|   2010 | Minnesota   | East North Central |              3000 | severe weather     |                70000 |
|   2012 | Minnesota   | East North Central |              2550 | severe weather     |                68200 |
|   2015 | Minnesota   | East North Central |              1740 | severe weather     |               250000 |

# Univariate Analysis
## Qualitative Variables:
### Climate Region
Which regions are most represented in our dataset? This could affect how we analyze our data, if certain regions are overrepresented.

<iframe
  src="Assets/univar_ClimateRegion.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This chart shows the distribution for the Climate Region. The trend for this chart seems to be that the Northeast region has the most outages recorded in the dataset. We'll have to keep this in mind for later: The dataset might be biased towards this region.

### States
<iframe
  src="Assets/univar_PostalCode.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Taking this at face value, this tells us that CA (California) had the most power outages out of all these states from 2000 to 2016. However, this could also have to do with how the data was collected. Either way, California seems very overrepresented in our dataset- we might have to control for this later on.

## Quantitative Variables:

### Outage Duration


### Months

### Years

# Bivariate Analysis
## Customers Affected and Duration

## Cause and Duration 

## Interseting Aggregates
### dur_by_yr
### Severity by Location
### Map of Duration by Location


