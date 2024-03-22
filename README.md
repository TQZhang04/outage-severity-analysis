# Power Outages Analysis
### Note to Suraj - sorry for the boring repo name
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

## Univariate Analysis
### Qualitative Variables:
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
### Months
Plotting the distribution of months will give us an idea of when outages are most common.

<iframe
  src="Assets/univar_months.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This chart is Month distribution. As we can see, the number of outages peaks around the summer months.

### Years
Has the number of outages been on the rise? Plotting the distribution of years might give us some insights.

<iframe
  src="Assets/univar_years.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows us the distribution of years in our data. There seems to have been a peak in outage counts in 2011, with a significant jump in the number of outages. The main takeaway, however, is that not all years are represented equally in our data; If we do analysis based on time later on, we'll have to keep this in mind.

### Outage Duration
Since outage duration is what we'll ultimately be looking at, we should look at its distribution here too.
<iframe
  src="Assets/univar_durations.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

From this graph, it's pretty obvious that outage duration is severely right-skewed. This means while most outages are short, there are some lasting tens of thousands of minutes (10k minutes is about a week), with one outage lasting 108k minutes. 

## Bivariate Analysis
### Customers Affected and Duration
Does it take longer to get electrical grids back up if there are more people affected by the outage? Or maybe it's the opposite: If an outage affects less people, engineers might drag their feet fixing them. Let's plot this relationship and see if there's an correlation.
<iframe
  src="Assets/bivar_cust_vs_dur.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
There seems to be a very weak, but positive, correlation. However, it's really too weak to tell us much about actual effects.

### Cause and Duration 
Do outages caused by different things take longer to fix? Intuition tells us yes: Things that had more severe causes might take longer to repair.

<iframe
  src="Assets/bivar_cause_vs_dur.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Looking at this, it looks like fuel supply emergencies caused the longest durations, but also had the largest variance. Severe weather also caused pretty substantial outages.

## Interesting Aggregates
### Duration by Year
Let's see how durations have changed over time. To do this, we'll group by the start date and take the median duration for all the outages that occurred on that date. Then, we'll plot the change in this over time on a line plot.
We'll use the median here, since there are a lot of outliers in our data.

|   startyr |   OUTAGE DURATION |
|----------:|------------------:|
|      2000 |            1230   |
|      2001 |             278.5 |
|      2002 |            3210   |
|      2003 |            2019.5 |
|      2004 |            1950   |
|      2005 |            3060   |
|      2006 |            1793   |
|      2007 |            1003   |
|      2008 |            1092   |
|      2009 |            1204   |
|      2010 |            1683.5 |
|      2011 |             457   |
|      2012 |             255   |
|      2013 |             184.5 |
|      2014 |             235.5 |
|      2015 |             176.5 |
|      2016 |             224   |

<iframe
  src="Assets/dur_by_yr_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This seems to suggest outage duration has been on the decline since around 2004. However, keep in mind from earlier: we have a lot more data for the more recent years, meaning there is probably a higher variance in the earlier years, which could lead to the perceived decline. We could've just gotten really unlucky, and the outages that were recorded from 2002-06 happened to be really long.

### Duration by Location
Does the location have some correlation with outage severity (in terms of length and proportion of customers affected)? We can plot a choropleth map to see if there are any trends. Since we only have data for states, we'll do this on the state level.

| POSTAL CODE   |   OUTAGE DURATION |   PROP CUST AFFECTED |
|:--------------|------------------:|---------------------:|
| WV            |            5288   |            0.204557  |
| MI            |            4110   |            0.0256502 |
| NJ            |            3120.5 |            0.0346817 |
| SC            |            2947.5 |            0.0605894 |
| PA            |            2880   |            0.0209914 |

### Map of Duration by Location
<iframe
  src="Assets/folium_map.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Missingness
## two graphs for duration




