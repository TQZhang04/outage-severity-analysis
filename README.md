# Investigating Which Factors Affect Outage Duration
### Name(s): (Natasha Lie, TQ Zhang)
# Introduction

## Background

With people depending more and more on electrical implements inside their homes, power outages become more and more costly. They hinder the productivity of all computer users, limit people's ability to communicate through the internet, and overall halt the daily lives of anyone unlucky enough to get caught. In cases of severe weather or emergency, power outages can even limit access to important utilities or the ability to reach emergency services. An crucial thing to know for those affected by outages would be how long outages will last, so that they know when they can return to their normal lives or how long they should be preparing to hunker down for.

## Our Question

In our analysis, we investigated the question: **Which factors contribute the most to the severity of the power outage in terms of outage duration?**

## Our Dataset

To perform this analysis, we used the data from major power outages in the continental United States, ranging from January of 2000 to July of 2016. Our dataset contains data on the severity of outages, as well as their start and restoration dates, causes, locations, and more location-specific information. **This dataset has 55 variables (columns) and 1,534 observations (rows), where each observation corresponds to a different outage.**

While there were 55 variables (columns) in the dataset, only a few were relevant to our analysis. These variables, and short descriptions, are listed below:

- `'YEAR'`: The year in which the outage happened
- `'MONTH'`: The month in which the outage happened
- `'U.S. STATE'`: The state in which the outage occurred
- `'CAUSE CATEGORY'`: The category of the outage's root cause, out of 7 potential categories
- `'OUTAGE DURATION'`: The duration of the outage, in minutes
- `'CUSTOMERS AFFECTED'`: The total number of people affected by the outage
- `'TOTAL CUSTOMERS'`: Annual number of total customers served in the state in which the outage occurred
- `'DEMAND LOSS MW'`: The amount of peak demand lost during the outage in Megawatts

# Data Cleaning and Exploratory Data Analysis

## Data Cleaning
First some preliminary cleaning: we replaced all the values that contained "NA" with actual NaN values. Then, we converted all numerical values to floats to have consistency across our dataframe. Finally, we made sure all the values make sense, and corrected them if not. This included removing outages with extreme durations (over a week) and reducing the `'CUSTOMERS AFFECTED'` column to contain values less than or equal to the `'TOTAL CUSTOMERS'` column. 
The column names had periods and underscores instead of spaces. We replaced these with spaces just to make things look a little prettier and standardize formatting.

Here is the head of our dataframe after cleaning (Only included a few relevant columns):


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

This chart shows the distribution for the Climate Region. The trend for this chart seems to be that the Northeast region has the most outages recorded in the dataset. This could be because the Northeast Region is more prone to outages due to severe weather/climate. We'll have to keep this in mind for later: The dataset might be biased towards this region.

### States
<iframe
  src="Assets/univar_PostalCode.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This shows the distribution of the number of recorded power outages for each State. Taking this at face value, this tells us that CA (California) had the most power outages out of all these states from 2000 to 2016. However, this could also have to do with how the data was collected - maybe more California simply had more records of their outages. Either way, California seems very overrepresented in our dataset.

### Quantitative Variables:
### Months
Plotting the distribution of months will give us an idea of when outages are most common.

<iframe
  src="Assets/univar_months.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This chart shows the distribution for the number of outages for each month. As we can see, the number of outages peaks around the summer months.

### Years
Has the number of outages been on the rise? Plotting the distribution of years might give us some insights.

<iframe
  src="Assets/univar_years.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows us the distribution of years in our data. There seems to have been a peak in outage counts in 2011, with a significant jump in the number of outages. The main takeaway, however, is that not all years are represented equally in our data.

### Outage Duration
Since outage duration is what we'll ultimately be looking at, we should look at its distribution here too.
<iframe
  src="Assets/univar_durations.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows the distribution of outage durations. From this graph, it's pretty obvious that outage duration is severely right-skewed. This means while most outages are short, there are some lasting tens of thousands of minutes (10k minutes is about a week), with one outage lasting 108k minutes. 

## Bivariate Analysis
### Customers Affected and Duration
Does it take longer to get electrical grids back up if there are more people affected by the outage? Or maybe it's the opposite: If an outage affects less people, engineers might drag their feet fixing them. Let's plot this relationship and see if there's an correlation.
<iframe
  src="Assets/bivar_cust_vs_dur.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
There seems to be a very weak, but positive, correlation. This could mean that, as we expected, the more people are affected, the longer it takes the outage to get fixed.

### Cause and Duration 
Do outages caused by different things take longer to fix? Intuition tells us yes: Things that had more severe causes might take longer to repair.

<iframe
  src="Assets/bivar_cause_vs_dur.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows the distribution of outage duration for each cause category. Looking at this, it looks like fuel supply emergencies caused the longest durations, but also had the largest variance. Severe weather also caused pretty substantial outages.

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

This table was grouped by US State and aggregated by median. We can see that Eastern States seem to have longer median outage durations.

### Map of Duration by Location
<iframe
  src="Assets/folium_map.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The States in black are States with no recorded Outage Duration.

# Missingness
## NMAR Analysis
One column that could be NMAR, meaning the missingness of the data depends on some property of the missing data itself, is `'OUTAGE RESTORATION DATE'`. This is because restoration dates could have started being recorded after a certain date. Restoration dates before that date would be missing. The additional data we would want to obtain would be when they started recording restoration dates, and the dates for outage restorations before they started recording restorations.
## Missingness Dependency
In our dataset, the `'OUTAGE DURATION'` column, which we are interested in as a measure of outage severity, is missing some of its values. This is problematic, and we want to know which missingness mechanism it follows so that we can impute values and closely replicate the missing data.

One way to check this is to look at the difference in the distributions of a column between rows where duration is missing and rows where it's present. This is demonstrated for `'CAUSE CATEGORY'` below.

<iframe
  src="Assets/missing_diff_cause.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The rows of "severe weather" seem to be missing duration less, while "fuel supply emergency" seems to be missing it more. Based on this difference in distributions, we believe that the 'OUTAGE DURATION' Column is Missing at Random (MAR) depending on the 'CAUSE CATEGORY' column. To test this theory, we'll run a permutation test on these two columns.

H0: The distribution of Cause Category is the same for rows that are missing Outage Duration and rows that are not missing Outage Duration.

Ha: The distribution of Cause Category is different for rows that are missing Outage Duration and rows that are not missing Outage Duration.

Test Statistic: The Total Variation Distance between the distributions of Cause Category for rows missing Outage Duration and rows not missing Outage Duration.
Significance level:  𝛼=0.05

Our results:
P-value: 0.0

Based on the results of our permutation test, we reject the null hypothesis. We rarely see TVD's as high as our observed. This tells us that the missingness of `'Outage Duration'` does depend on `'Cause Category'`, making it NMAR. To replace these values, we should employ probabilistic imputation, replacing each missing duration value with a randomly sampled value from the durations with the same cause category.

Let's run the same test on some other columns, to see if the missingness in Duration is dependent on anything else.

<iframe
  src="Assets/missing_diff_month.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We can see that the distribution of month looks about the same regardless of the missingness of Duration. Let's see if that tiny difference is significant.

H0: The distribution of Month is the same for rows that are missing Outage Duration and rows that are not missing Outage Duration.

Ha: The distribution of Month is different for rows that are missing Outage Duration and rows that are not missing Outage Duration.

Test Statistic: The Total Variation Distance between the distributions of Month for rows missing Outage Duration and rows not missing Outage Duration.
Significance level:  𝛼=0.05

Our results: 
P-value: 0.858

As expected, the p-value is high, beyond the chosen significance threshold of 0.05. This means that Outage Duration is Not Missing at Random (NMAR) in relation to Month.

# Hypothesis Testing

Question 1: Are the durations of outages in the East North Central region significantly longer than the overall population?
Since we're interested in predicting Outage Duration as one metric for severity, it'd be helpful to know what factors affect this. In our EDA, we saw that the East North Central region had a higher median outage duration than other regions. This was backed up in our aggregate analysis. Is this a significant difference?

Before running our hypothesis test, let's take a look at the data and see how different they really are.

<iframe
  src="Assets/hypothesis_region.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


Observed Difference: 3005.622585762335

So in our observed data, there's a 3005 minute difference between the mean durations for ENC and other regions. Let's see if this difference is significant using a permutation test.

H0: The mean duration of outages in the East North Central region is the same as the mean duration of outages in other regions.

Ha: The mean duration of outages in the East North Central region longer than the mean duration of outages in other regions.
Test statistic: Absolute Difference in Mean Duration between the ENC region and other regions.
Significance level:  𝛼=0.05
 
To do this we'll have to create a dataframe where one of the columns is binary, which takes on one value for "ENC" and another value for "not ENC".

| CLIMATE REGION     |   OUTAGE DURATION | Region Binarized   |
|:-------------------|------------------:|:-------------------|
| East North Central |              3060 | East North Central |
| East North Central |                 1 | East North Central |
| East North Central |              3000 | East North Central |
| East North Central |              2550 | East North Central |
| East North Central |              1740 | East North Central |
| West North Central |               720 | Other              |
| West North Central |               nan | Other              |
| West North Central |                59 | Other              |
| West North Central |               181 | Other              |

Our Results:

P-value: 0.0

From the results of our permutation test, we can conclude that we reject the null hypothesis. There is significant evidence that the mean duration in the East North Central region is higher than the mean duration in other regions.

# Framing a Prediction Problem
**Our prediction problem: Predict the severity (measured in Outage Duration) of an outage by looking at data from any of the cause columns.** To solve this problem, we will be using regression, since we want to predict the duration, not classify the data. The response variable is Outage Duration. To evaluate our model, we will be using  R², since it is more straightforward metric, where higher values are better (as opposed to RMSE, where lower error is better). At the time of prediction, we would know the year and month of the outage as well as have a general idea of how many customers were affected. We would also know where the outage happened, cause of outage, and the amount of demand lost. This is because the electric company would likely have records of how many customers they serve under each grid as well as how much demand is usually generated.

# Baseline Model
For our baseline model, we’ll train a Linear Regression model to predict outage duration. This model will only have 2 features, and we’ll use it so we have something to which we can compare to compare future models. 

The two features we’ve chosen for our baseline model were `’PCT LAND’`, which is the proportion of the land area of the entire continental US made up by the state the outage occurred in, and `’CUSTOMERS AFFECTED’`, the number of customers affected by the outage. We chose `’PCT LAND’` because when looking at the Pearson’s correlation of each numerical column with the `’OUTAGE DURATION’` column, `’PCT LAND’` had the highest absolute value (as shown below). `’CUSTOMERS AFFECTED’` was chosen also for its high correlation, and because, intuitively, it makes sense for outages that affected more customers to take longer to restore, an intuition that’s backed up by our analysis of the two variables in our EDA. **Both of these features are quantitative, and while Pct. Land is continuous, Customers is discrete.** No encodings were necessary, since both these features are numerical.

We scored this model using the R² value, which measures how much of the variance in the observed data the model is able to capture in its predictions. We chose this metric because out of the two evaluation metrics for linear regression models, it is the more intuitive and easier to understand at a glance (higher means better). 

| COLUMNS            | CORRELATION TO OUTAGE DURATION |
|:-------------------|------------------:|
| OUTAGE DURATION    |          1        |
| PCT LAND           |          0.250879 |
| PCT WATER TOT      |          0.250865 |
| YEAR               |          0.240186 |
| CUSTOMERS AFFECTED |          0.21734  |
| PROP CUST AFFECTED |          0.196802 |
| UTIL CONTRI        |          0.141612 |
| PC REALGSP USA     |          0.138206 |
| RES CUST PCT       |          0.130159 |
| POPDEN RURAL       |          0.129671 |
| POPPCT UC          |          0.127768 |

The baseline model had an R² of 0.11 on the training set, and about 0.09 for the unseen data in the test set. Considering this metrics ranges between 0 and 1, this is extremely low performance. This is likely because although the features we selected had *relatively* high correlation coefficients when comparing to other variables, they were still only weakly correlated to the Outage Duration (both with Pearson’s r values of about 0.2). 

Seeing as how this metric is low on both training and testing, this model is *underfit* to the data. This means to improve performance, we have to make our model more complex.

# Final Model
We first tried to maximize the performance using a Linear Regression model. We noticed that many of our variables were severely skewed, so we applied various linearization transformations in order to account for this skew. We also tried binarizing the skewed variables in case the real distinction only lied in “high” or “low” values, rather than the exact values.

An interesting finding was that after adding `’U S STATE’` as a feature, adding more variables that were state-specific, such as the `’PCT LAND’` variable used in the base model, ceased to help the model’s performance. This is likely because the values of these variables were unique to each state, not each outage. Every outage that occurred in the same state would share a value for these variables. Therefore, each of the vectors of these variables would simply be a linear combination of the one-hot-encoded state vectors.

After some testing and iteration, the model that reached the highest performance was actually a Random Forest Regressor, which achieved an R² of 0.72 on the training set and 0.44 on the test set. We believe this is due to the Random Forest model’s ability to ignore the skewness of data and not require linearization to complete its task. Below, we outline the features used in this model and why we believe they improved our model’s performance.

- `’CUSTOMERS AFFECTED’`: As stated before, Customers Affected had a relatively high correlation with Outage Duration. We believe this is because outages that affected more customers likely happened to a larger power grid or had more severe causes, both of which would make it harder to restore power. Also, duration was recorded as the time it took to restore power to *all customers*- naturally, if more customers were affected, it would take longer for this to be true.
- `’DEMAND LOSS MW’`: This variable measured the amount of peak demand lost in an outage. Similarly to customers, if this number was higher, it would likely point to either a larger outage overall or a more severe cause, lengthening the time it takes to restore power.
- `’YEAR’`: In our EDA, we found that the duration of outages seemed to decrease overall as years went on. This is likely due to newer, more modern electrical infrastructure making outages less severe, and allowing engineers to restore power quicker. Thus, knowing in which year an outage happened would help our model predict how long it lasted.
- `’MONTH’`: We saw that more outages occurred in the summer months. This could be due to the fact that more people are home in summer, thus making there be more energy demand and more strain on electrical grids. Either way, knowing in which month the outage happened likely helps our model because outages were more common and lasted longer during the summer.
- `’U S STATE’`: As seen in our EDA process, certain states had much longer median outage durations than other states. This is likely due to differences in electrical infrastructure, exposure to more extreme weather conditions, or differing protocols for resolving outages. For this reason, knowing which state an outage occurred in would have helped our model predict its duration.
- `’CAUSE CATEGORY’`: Finally, the cause of an outage had a rather large impact on the outage’s duration. Outages in the “severe weather” category, for example, had a far longer median duration than outages caused by an “intentional attack”. This is likely due to differences in the severity of the cause: A hurricane that wipes out entire power grids or fuel supply emergencies that take months to resolve would cause far longer outages than things like small equipment failures, which likely have protocols in place for speedy resolution and restoration. Thus, knowing the broader cause category helped our model determine the duration.

*Note that our two categorical features (State and Cause Category) were one-hot-encoded in our final pipeline to turn them into numerical data, since neither of them had any inherent order significant enough to make the decision to ordinally encode them.*

For the final model, we chose the following hyper-parameters:
- `max_depth` = 10
- `n_estimators` = 100

We chose a max depth of 10 to prevent overfitting, and n_estimators of 100 was the default value. While we did use GridSearchCV to find the best hyperparameters, the parameters it chose seemed to lower the performance of the model overall, so the default values were kept for our final model.

As mentioned, the R² of the final model reached 0.72 on the training set and 0.44 on the test set. This was an improvement of about 0.35 on the test set when compared to the baseline model, meaning its predictions captured about 35% more of the variance of Outage Durations.

# Fairness Analysis
In 2003, various geopolitical events, an increase in demand, and natural disasters caused the price for a barrel of crude oil in the US to rise to above $30, from its previous price of under $25. Under pressure from things like tensions in the Middle East and Hurricane Katrina, this price continued to skyrocket up until around 2008, causing a national [energy crisis](https://en.wikipedia.org/wiki/2000s_energy_crisis) (this was actually one of the many factors of the great recession, in 2007).

The changes in the `'TOTAL PRICE'` column, which measures the average price of energy per month in each state, reflect this change (as seen above). We want to know if our model is equally successful for outages that occured before this crisis (before 2003) and after (during or after 2003). 


#### **Fairness Analysis:** Is Our Model Fair for Outages Before and After the 2003 Energy Crisis?
**Group X:** Outages occurring before 2003

**Group Y:** Outages occurring during or after 2003

**Evaluation metric:** R²

**H0:** Our model is fair. Its R² for power outages before 2003 and outages during or after 2003 are roughly the same, and any differences are due to random chance.

**Ha:** Our model is unfair. Its R² for outages before 2003 is different from its R² for outages during or after 2003.

**Test Statistic:** The absolute difference in R² of the model between observations in group X and observations in group Y.

**Significance level:** 𝛼 = 0.05


<iframe
  src="Assets/perm_plot2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Observed Test Statistic:** 0.5

After performing the permutation test, our p-value was around 0.3. Because the p-value is high, we fail to reject the null hypothesis and conclude that our model is fair. There is no sufficient evidence to prove that its performance for power outages before 2003 and those after 2003 are significantly different.



