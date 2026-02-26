---
title: Time Series Analysis (Part - I)
date: 2025-01-01 20:14 +0300
categories: [Time Series Analysis]
tags: [python, time series analysis]
math: true
author: Varatharuban
description: "Predict future values"
---

### Time Series Analysis
It is a series of observations taken at specified times basically at equal intervals. 
It is used to predict future values based on past observed values.
- Stock prices
- Weather data
- Sales data

### Time Series vs Regression
- Time Series Analysis is used when we have data that are collected over time, such as sales data, stock prices, or weather data. 
With time series analysis the patterns and relationships within the data to make predictions or identify trends. 
<u>Date component will play the big role here. If the date not falls in the same intervel, then aggregate the data.</u>

- Regression analysis, on the other hand, is used to study the relationship between a dependent variable and one or more independent variables. 
It helps to predict what the outcome will be based on the values of the independent variables.

### 1. Components of Time Series
- **Trend** - Increasing or decreasing value in the series.
	![Components of Time Series Analysis (Trend)](/assets/images/ai/tsa-components-trend.png)
- **Seasonality** - A general systematic liner or (most often) non-linear component that changes over time and does repeat.
- **Irregularity** - The data in the time series follows a temporal sequences, but the measurements might not happen at a regular time interval.
- **Cyclic** - Pattern exists when data exhibit rises and falls that are not of fixed period.

#### Techniques to detech Components of Time Series
- Decomposition (Decompose) - This involves breaking down the time series into its various components, which is trend, seasonality, irregularity and cyclic.
Using some statistical methods such as moving average or exponential smoothing or faurier analysis.
- Auto Correlation - Involves analyzing the correlation between the time series and a lagged version of it.
- Fourier/Spectral Analysis - 

#### Decomposition (Decompose)
Simply time series decomposition is a technique used to break down a time series into its individual such as trend, seasonality, irregularity and cyclic behaviour.
This can be useful for understanding the underlying patterns and trends in the data and can help in making future predictions.
- **Additive**: Observed data is sum of the components. 
observed data = trend + seasonality + resid

- **Multiplicative**: Observed data is product of the components. 
observed data = trend x seasonality x resid

The choice of wheather to use additive or multiplicative decomposition depends on the characteristics of the data.
If the magnitude of seasonal component is <u>proportional</u> to the magnitude of the trend component multiplicative decomposition is prefered or more appropriate.

If the magnitude of seasonal component is <u>independent</u> to the magnitude of the trend component additive decomposition is prefered.

![Anomaly detection in Time Series Analysis](/assets/images/ai/tsa-decomposition.jpeg)

```python
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load AirLine Passangers dataset
# https://github.com/jbrownlee/Datasets/blob/master/airline-passengers.csv
df = pd.read_csv('/content/air-passenger.csv', 
		header=0, 
		index_col=0, 
		parse_dates=True)

# Perform seasonal decompose
result = seasonal_decompose(df, model='multiplicative')

# Plot the components
plt.rcParams.update({'figure.figsize': (10, 10)})
result.plot()
plt.show()
```

![Anomaly detection in Time Series Analysis](/assets/images/ai/tsa-decomposition-multiplicative.png)


### 2. Stationarity
Statistical properties of a time series remaining constant over time.
A time series is called to be stationary if its mean ($\mu$), variance, standard deviation ($\sigma$), or autocorelation remains constant over time.
Stationarity is important because many time series forecasting methods rely on the underlying statistical properties of the time series being stationary.
When a time series is not stationary, it can be difficult to make accurate predictions because statistical properties of the data are changing over time.


Once a time series has been made statinary, it can easily be applied with forecasting techniques to make accurate predictions.

![Anomaly detection in Time Series Analysis](/assets/images/ai/tsa-stationary-transfomation.png)

How to check whether a data is statinary or not?
There are some test as 
- Look at plots
- Summary statistics
- Statistical tests
	* **ADF**- The Augmented Dickey-Fuller (ADF) test aka Unit Root Test
	* **KPSS**- Kwiatkowski-Phillips-Schmidt-Shin

If data has unit root, then its not statinary.

If data doesn't have the unit root, then its statinary.

![Anomaly detection in Time Series Analysis](/assets/images/ai/tsa-stationary-test-adf-kpss.png)

#### Transformations
Various transfomation techniques to rid of the seasonal and trend components from time series data (to make the data to statinary)
- Differncing (taking the difference between the consecutive values in a time series)
	* Time - Data [Differ] - [Log if not stationary] - [Forecast] - [Bring back original scale using exponential]
- Logarithmic
- Smoothing (Moving Average or Exponential Smoothing) - involves removing the high frequence noise or variablility from the data while preserving the underlying trend and seasonality.


### 3. Pre Processing
Data pre processing is the initial phase of data preparation that involves transforming raw data into a structured and cleaned format suitable for analysis.

Common data pre-processing techniques
- Data cleaning:
	* Handling missing values
	* Remove duplicates
	* Deal with outliers
	
- Data transfomation:
	* Feature scaling
	* Encode categorical data
	* Feature engineering
	
#### Anomaly/Outlier Detection
Anomaly detection in the context of time series refers to the process of identifying data points that deviate significantly from the expected pattern or behaviour of the time series.
Time series are typically used to represent data that varies over time, such as sensor reading, stock prices, or weather data.
By detecting anomalies in time series data, we can identify unusual events or behaviours that may indicate a mulfuction or a potential problem.

![Anomaly detection in Time Series Analysis](/assets/images/ai/tsa-anomaly-detection.png)

There are multiple cases that some anomalies cannot detected by human eyes.

Outliers are the most extreams values in the data. It is an abnormal observations that deviate from the normal data. Outliers do not fit in the normal behaviour of the data.
Detect outliers using following methods,
- 3 sigma technique
- Boxplot
- Histogram
- Scatter plot
- Z-score
- Inter quartile range (values out of 1.5 time of IQR)


Handle outlier using following methods,
- Remove the outliers
- Replace Outlier with suitable values by using,
	* Quantile method
	* Inter quartile range
- Use that ML model which are not sensitive to outliers (KNN, DT, SVM, Naive Bayes, Ensemble methods)

#### Feature Scaling
Feature scaling is the method to re-scale the values present in the features. In feature scaling we convert the scale of different measurement into a single scale. It standardize the whole dataset in one range.

When we are dealing with independent variable or features that differ from each other in terms of range of values or units of the features, then we have to normalize/standardize the data so that the difference in range of values doesn't affect the outcome of the data.

The two most accepted techniques for feature scalling,
- Standard Scaler (if data normaly distributed)
Standard scaler ensures that for each feature, the mean is zero and the standard deviation is 1, bringing all feature to the same magnitude. In simple words Standardization helps you to scale down your feature based on the standard normal distrubution.
Standardization in statistics is a process of converting data to z-score values based on the mean and standard deviation of the data.
The standardize data will have mean equals to zero and the values will generally range between - 3 and +3. Almost 99.7% data will fall.

$$z = \frac{x - \mu}{\sigma}$$

- Min-Max Scaler (if data not normaly distributed)
Normalization helps you to scale down your features between a range 0 to 1.

$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}}$$

#### Feature Encoding
Transform categorical data into numeric data.
- **Label encoding**: is the technique to transform categorical variables into numerical variables by assigning a numerical value to each of the categories.
- **One-Hot encoding**: this technique is uded when independent variables are nominal. It creates k different columns each for a category and replaces one column with 1 rest of the columns is 0. Here 0, represent the absence, and 1 represents the presence of that category.
- **Dummy encoding**: one of the dummy feature can be ignored. Using drop_first or drop_last attribute can ignore the columns.
