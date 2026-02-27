---
title: Time Series Analysis - Models (Part - II)
date: 2025-01-07 20:14 +0300
categories: [Time Series Analysis]
tags: [python, time series analysis]
math: true
author: Varatharuban
description: "Predict future values"
---

### Models
Various algorithms that can be used to analyse and forecast time series data.
- ARIMA (AR, MA, ARMA, ARIMA) - Autoregressive Integrated Moving Average
- Facebook Prophet
- LSTMs
- Holt's Winter Exponential Smoothing
- GARCH
- SARIMA/SARIMAX (Variance of ARIMA)
- VAR (Vector Autoregression) 
- VARMA (Vector Autoregressive Moving Average)

### ARIMA
A popular time series analysis and forecasting technique used by data scientists and analysts world wide.
It's a powerful tool for analyzing and forecasting time series data that exhibits trend, seasonality, and auto correlation.

There are three different parameters which is called as,
- **p**: autoregressive part. its number of autoregressive terms
- **d**: moving average part. the non-seasonal differences needed for stationary.
- **q**: differencing part. the number of lagged forecast errors in the prediction equation.

Variance of ARIMA
- **AR** - use past values of the time series to predict future values, and they are particularly useful for analyzing data with trends.
		 AR = ARIMA(p, 0, 0)
- **MA** - use past forecast errors to make future predictions, and they are useful for analyzing data with periodic fluctuations.
		MA = ARIMA(0, 0, q)
- **ARMA** - which does not have the differencing factor. it's combine the concept of AR and MA models, and they are useful for analyzing more complex time series data that exhibits both trends and periodic fluctuations.
		ARMA = ARIMA(p, 0, q)
- **ARIMA** - include an additional differncing step to ensure the data is stationary, making it easier to model and analyze.
		ARIMA = ARIMA(p, d, q)

Differencing is one of the transfomation technique that can use to make a time series data stationary. In ARIMA models, we use differencing to remove trends and seasonality from the time series (to easy to analyse and model).


#### 1.1 AR Model
The future value of the time series is estimated as a linear combination of past values of the time series. The degree of past values to be considered in the linear combination is determined by the order of AR model.

Future Value ← Past Values
<br>
Predicts future values using previous values
<br>
Example, If yesterday temperature was high → today likely high

#### 1.2 MA Model
The future values of the time series are based on the average of past forecast errors. Again the degree of past forecast errors to be considered is determined by the order of the MA model.
<br><br>
Future Value ← Past Errors
<br>
Predicts future values using previous errors
<br>
Example, If prediction error was large yesterday → adjust today

#### 1.3 ARMA Model
ARMA is the combination of past values and the past forecast errors.
Better than AR or MA alone when data has mixed patterns.
<br>
Future Value ← Past Values + Past Errors

#### 1.4 ARIMA Model
Combination of ARMA with an additional dfifferencing step to ensure that the data is stationary.

Stationary is an important concept in time series analysis, because most models work on the assumption that the data is stationary.
<br>
Used when data has trend or is non-stationary.<br><br>
Step 1: Differencing → Make data stationary<br>
Step 2: Then apply ARMA<br>

Most popular classical forecasting model
<br>
Future Value ← Differencing → ARMA

![Components of Time Series Analysis (Trend)](/assets/images/ai/tsa-arima-model.png)

| Model            | Full Name                                | Idea                                                  | When to Use                                         | Equation Form                                                           | Stationary Required                          |
| ---------------- | ---------------------------------------- | ----------------------------------------------------- | --------------------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------------- |
| **AR(p)**        | Autoregressive                           | Uses **past values** to predict future values         | When data depends strongly on previous observations | $(Y_t = c + \phi_1Y_{t-1}+...+\phi_pY_{t-p}+\epsilon_t)$                  | ✅ Yes                                        |
| **MA(q)**        | Moving Average                           | Uses **past errors (noise)** to predict future values | When shocks/errors influence future values          | $(Y_t = c + \epsilon_t+\theta_1\epsilon_{t-1}+...\theta_q\epsilon_{t-q})$ | ✅ Yes                                        |
| **ARMA(p,q)**    | Autoregressive Moving Average            | Combines **AR + MA**                                  | When data has both trend memory and noise patterns  | AR + MA combined                                                        | ✅ Yes                                        |
| **ARIMA(p,d,q)** | Autoregressive Integrated Moving Average | ARMA applied after **differencing**                   | When data is **non-stationary**                     | Differencing + ARMA                                                     | ❌ No (becomes stationary after differencing) |


### ACF and PACF (Autocorrelation Function/ Partial Autocorrelation Function)
Autocorrelation analyis is one of the important step in the exploratory data analyis of time series forecasting. The autocorrelation analysis helps detect patterns and check for randomness.
It's essentially important when you intend to use an autoregressive moving average, which is a ARMA model for forecasting because it helps to determine its parameters.
The autocorrelation analysis involves looking at the autocorrelation function, which is ACF, and partial ACF.
The ACF and PACF plots are used to identify or find the order of the AR, MA and AEMA models.

Using the ACF plot, we will be able to identify the q parameter that goes into our ARIMA model.

To identify the p, we need to see the PACF plot.
To identify the q, we need to see the ACF plot.

