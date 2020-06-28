---
layout: post
title:  "While Determining Housing Price, I Learned..."
date:   2019-09-27 20:15:32
categories: technical, data science
paginator: While Determining Housing Price I learned
---
Data Science is an art. Each decision in the process can lead to different results. A certain type of intuition can help in navigating the pathway to an appropriate model. Creativity also makes an appearance in developing features and in creating links between variables. This post's purpose is to describe the flow of the data science process from idea, to data acquisition, to learning about the data, and finally to model development.

# Obtain

In this first step, the data scientist begins to get a taste for what future work might be in store for a project. It starts with a business case, a question, a real world problem. Once the type of data to address the beginning case, question, problem is established, then it's time to acquire the dataset. For this discussion, I will be using the King's County Seattle Housing Prices dataset. It can be found [here][link1].

```import pandas as pd
df = pd.read_csv('kc_house_data.csv', index_col=0)
```


| id         | date       | price    | bedrooms | bathrooms | sqft_living | sqft_lot | floors | waterfront | view | condition | grade | sqft_above | sqft_basement | yr_built | yr_renovated | zipcode | lat     | long     | sqft_living15 | sqft_lot15 |
|------------|------------|----------|----------|-----------|-------------|----------|--------|------------|------|-----------|-------|------------|---------------|----------|--------------|---------|---------|----------|---------------|------------|
| 7129300520 | 10/13/2014 | 221900.0 | 3        | 1.00      | 1180        | 5650     | 1.0    | NaN        | 0.0  | 3         | 7     | 1180       | 0.0           | 1955     | 0.0          | 98178   | 47.5112 | -122.257 | 1340          | 5650       |
| 6414100192 | 12/9/2014  | 538000.0 | 3        | 2.25      | 2570        | 7242     | 2.0    | 0.0        | 0.0  | 3         | 7     | 2170       | 400.0         | 1951     | 1991.0       | 98125   | 47.7210 | -122.319 | 1690          | 7639       |
| 5631500400 | 2/25/2015  | 180000.0 | 2        | 1.00      | 770         | 10000    | 1.0    | 0.0        | 0.0  | 3         | 6     | 770        | 0.0           | 1933     | NaN          | 98028   | 47.7379 | -122.233 | 2720          | 8062       |
| 2487200875 | 12/9/2014  | 604000.0 | 4        | 3.00      | 1960        | 5000     | 1.0    | 0.0        | 0.0  | 5         | 7     | 1050       | 910.0         | 1965     | 0.0          | 98136   | 47.5208 | -122.393 | 1360          | 5000       |
| 1954400510 | 2/18/2015  | 510000.0 | 3        | 2.00      | 1680        | 8080     | 1.0    | 0.0        | 0.0  | 3         | 8     | 1680       | 0.0           | 1987     | 0.0          | 98074   | 47.6168 | -122.045 | 1800          | 7503       |


Initially upon first observation of the head, there are several things that begin to dictate what next steps might be. There are 'NaN's, or not a number values, in the dataset, a lot of the data even though it seems to an integer or float value is actually categorical in nature, and the years in the 'yr_renovated' and 'floor' columns have floats, but need to be integers. These three things are going to be considered throughout the course of this project, beginning with the 'NaN' values.

# Scrub

## Not a Number Data

First, let's consider 'NaN' values. To see how many values are present in the entire dataset, run the following code.
```
df.isna().sum()
```
```
date                0
price               0
bedrooms            0
bathrooms           0
sqft_living         0
sqft_lot            0
floors              0
waterfront       2376
view               63
condition           0
grade               0
sqft_above          0
sqft_basement       0
yr_built            0
yr_renovated     3842
zipcode             0
lat                 0
long                0
sqft_living15       0
sqft_lot15          0
dtype: int64
```



The three variables 'waterfront', 'view', and 'yr_renovated' have 'NaN' values. However, addressing these values can be done in various ways. While dropping the rows of data containing the 'NaN' values is an option, that means loosing potentially useful data. For this dataset, the number of 'NaN's for 'waterfront' represents 11% of the dataset, the number of 'NaN's for 'view' represents 0.29% of the dataset, and the number of 'NaN's for 'yr_renovated' represents over 17% of the dataset. This can be found with the following code:

```
print(df['waterfront'].isna().sum() / len(df['waterfront']))*100)
print(df['view'].isna().sum() / len(df['view']))*100)
print(df['yr_renovated'].isna().sum() / len(df['yr_renovated']))*100)
```

Just dropping all of those rows would cause a loss of almost a third of the original data we started with. To maintain this data without changing the overall shape and distribution of the data present, 'NaN's can be replaced with the mean, median, or mode. This is called backfilling. For this dataset, I opted to use the mode. The 'waterfront' data is either a 0 or a 1, meaning yes waterfront or no waterfront. And if the home had been renovated, the 'yr_renovated' data provides the year, if the home had not been renovated, then a zero is filled in. In selecting mode to backfill, the most common occurrence of this type of data will be used. In the case of renovations and waterfront property, I feel like the mode, which is zero for both, will most likely describe the case of the property in any case. Since the 'view' 'NaN' data is such a small amount, I opted to drop those rows, although the same argument could be made to backfill with the mode for this data type.

```
df.loc[:,'waterfront'] = df.loc[:,'waterfront'].fillna(value=df.waterfront.mode())
df.loc[:,'yr_renovated'] = df.loc[:,'yr_renovated'].fillna(value=df.yr_renovated.mode())
df = df.dropna()
# to ensure that all of the NaNs are gone
df.isna().sum()
```
Now that this big concern established from viewing the head in the obtain step is addressed, some general information about the data needs to be evaluated.

```
df.info()
```
<class 'pandas.core.frame.DataFrame'>

Int64Index: 21534 entries, 7129300520 to 1523300157

Data columns (total 20 columns):

date             21534 non-null object

price            21534 non-null float64

bedrooms         21534 non-null int64

bathrooms        21534 non-null float64

sqft_living      21534 non-null int64

sqft_lot         21534 non-null int64

floors           21534 non-null float64

waterfront       21534 non-null float64

view             21534 non-null float64

condition        21534 non-null int64

grade            21534 non-null int64

sqft_above       21534 non-null int64

sqft_basement    21534 non-null object

yr_built         21534 non-null int64

yr_renovated     21534 non-null float64

zipcode          21534 non-null int64

lat              21534 non-null float64

long             21534 non-null float64

sqft_living15    21534 non-null int64

sqft_lot15       21534 non-null int64

dtypes: float64(8), int64(10), object(2)

memory usage: 3.5+ MB


Here, what we're looking for is the data types. There are two types of data in this dataset that have object data. Object data often contains a mixture of integer and string values, and as such cannot be evaluated or interacted with by the methods for either category. Object data needs to be addressed before moving forward. Everything else is either an integer or a float, but from our initial look at the data, some of these might actually be better suited as category data.

## Object Data


# Conclusions

The biggest thing that I learned in evaulating the King County Seattle Housing Dataset is that math is art and on the meta level tells you about itself. Optimizing for linear regression is like a river that ebbs and flows where the stream is adjusted by its surroundings. Basically, observation of what is present in data can lead you to next steps. If you ever get stuck, reevaluate the data and pick at the anomalies until the path forward is clear. This results in a stronger model overall, and allows your creativity to shine.


[link1]: https://www.kaggle.com/harlfoxem/housesalesprediction
