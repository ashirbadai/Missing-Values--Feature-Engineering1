
# Missing Values- Feature Engineering 1

I have taken a transactional dataset that contains information about various types of fruits, including the quantity sold in kilograms, the price per kilogram in USD, the name of the farmer who sold the fruit, and the name of the customer who purchased the fruit.

In this datset there are several missing values.Missing value handling is necessary in data science because missing data can affect the accuracy and reliability of analytical models and conclusions. Ignoring missing data can lead to biased or incorrect results.

## What are the different types of Missing Data?
### MCAR, MNAR, MAR:

1. A variable is missing completely at random (MCAR) if the probability of being missing is the same for all the observations. When data is MCAR, there is absolutely no relationship between the data missing and any other values, observed or missing, within the dataset. In other words, those missing data points are a random subset of the data. There is nothing systematic going on that makes some data more likely to be missing than other.

2. Missing Data Not At Random(MNAR): Systematic missing Values. There is absolutely some relationship between the data missing and any other values, observed or missing, within the dataset.

3. Missing At Random(MAR): Here probability of being missing is not the same for all the observations

In this case the data features such as **'Quantity_kg'** & **'Price_per_kg_in_USD'** is MCAR.
## Requirements

Install pandas library in cmd

```bash
  !pip install pandas
```
## Basic Usage

```bash
  import pandas as pd
  
```
## Read csv file

```bash
   df=pd.read_csv('Fruit_Production.csv')
   df.head() 
```
### Checking null values
The code is checking for missing values (null values) in a DataFrame (df) and counting the number of missing values for each column.
```bash
  df.isnull().sum()
  
```
### Checking for any missing values in the 'Quantity_kg'
Then we checked for missing values in 'Quantity_kg' column of data frame.
```bash
  df[df['Quantity_kg'].isnull()]
  
```
### Proportion of missing values 
 Code is checking for missing values in a DataFrame (df) and calculating the mean of the missing values (i.e. the proportion of missing values in the original DataFrame). The result will be a series of mean values for each column in the DataFrame, showing the proportion of missing values for each column.




```bash
  df.isnull().mean()
  
```
### Replace null values with median
It defines a function called "impute_nan" that takes in three arguments: a DataFrame (df), a variable name (variable), and a median value (median). The function creates a new variable in the DataFrame by adding "_median" to the original variable name, and filling any missing (NaN) values in that variable with the provided median value. The last line of code assigns the median value of the "Quantity_kg" variable to the "median" variable.
```bash
  def impute_nan(df,variable,median):
    df[variable+"_median"]=df[variable].fillna(median)

  median=df.Quantity_kg.median()
  median

  impute_nan(df,'Quantity_kg',median)
  df.head()
  
```
### Checking SD of both before & after
Standard Deviation checking
```bash
  print(df['Quantity_kg'].std())
  print(df['Quantity_kg_median'].std())
  
```
### Plotting Figure using Matplotlib 

```bash
  import matplotlib.pyplot as plt
  %matplotlib inline

  fig = plt.figure()
  ax = fig.add_subplot(111)
  df['Quantity_kg'].plot(kind='kde', ax=ax)
  df.Quantity_kg_median.plot(kind='kde', ax=ax, color='red')
  lines, labels = ax.get_legend_handles_labels()
  ax.legend(lines, labels, loc='best')

  
```
**Same exercise is done for Price_per_kg_in_USD from df.**


## Mean/Median Imputation
### Advantages
1. Easy to implement(Robust to outliers)
2. Faster way to obtain the complete dataset
###  Disadvantages
1. Change or Distortion in the original variance
2. Impacts Correlation

#### Quantity_kg vs Quantity_kg_median
![FIG1](https://user-images.githubusercontent.com/122656938/213270373-2ddb7e47-2e95-4f02-a6d2-958fd4ae20cb.png)

#### Price_per_kg_in_USD  vs  Price_per_kg_in_USD_median
![FIG2](https://user-images.githubusercontent.com/122656938/213271648-453f8c0f-a460-448d-b8bf-0493c2aefaa8.png)
## Tech Stack


**Tech:** Jupyter Notebook

#python
