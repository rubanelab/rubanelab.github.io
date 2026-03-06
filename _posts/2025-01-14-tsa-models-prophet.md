---
title: Time Series Analysis - Prophet (Part - III)
date: 2025-01-07 20:14 +0300
categories: [Time Series Analysis]
tags: [python, time series analysis]
math: true
author: Varatharuban
description: "Predict future values"
---

### Facebook Prophet
Facebook Prophet (now called Meta Prophet) is a time series forecasting library designed to make forecasting easy even for people without deep statistical knowledge. It works very well for daily, weekly, and yearly seasonality data such as sales, traffic, weather, etc.

<br>
Prophet automatically learns:
- Trend
- Seasonality
- Holiday effects (optional)


```bash
pip install prophet
```

```python
# Import libraries
import pandas as pd

from prophet import Prophet

# --------------------------------------------------
# 1. Load dataset (download CSV from data.gov.sg)
# --------------------------------------------------
df = pd.read_csv("rainfall_singapore.csv")
df = df.rename(columns={"date": "ds", "rainfall": "y"})
print(df.head())

# --------------------------------------------------
# 2. Train Prophet Model
# --------------------------------------------------
model = Prophet()
model.fit(df)

# --------------------------------------------------
# 3. Create Future Dates
# --------------------------------------------------
future = model.make_future_dataframe(periods=30)
print(future.tail())

# --------------------------------------------------
# 4. Forecast
# --------------------------------------------------
forecast = model.predict(future)

print(forecast[['ds','yhat','yhat_lower','yhat_upper']].tail())
# yhat → predicted rainfall
# yhat_lower / upper → confidence interval

# --------------------------------------------------
# 5. Plot Forecast
# --------------------------------------------------
model.plot(forecast)

# --------------------------------------------------
# 6. Plot Components
# --------------------------------------------------
model.plot_components(forecast)
```

### Prophet vs ARIMA

| Feature      | Prophet      | ARIMA     |
| ------------ | ------------ | --------- |
| Seasonality  | Automatic    | Manual    |
| Missing Data | Handles well | Not good  |
| Trend change | Handles      | Difficult |
| Ease of use  | Very easy    | Moderate  |
