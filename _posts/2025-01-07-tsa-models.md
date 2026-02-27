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

