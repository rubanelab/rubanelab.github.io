---
title: Machine Learning - Introduction (Part - I)
date: 2024-11-01 20:14 +0300
categories: [Machine Learning]
tags: [python, machine learning]
math: true
author: Varatharuban
description: "Predict future values"
---

### Machine Learning

Machine Learning is a subset of AI, that provides computers with the ability to learn without being explicitly programed. Machine Learning focuses on the development of computer programs that can teach themselves to grow and change when exposed to new data.
- Automatically learn
- Improve performance from past experience
- Make predictions

![Components of Time Series Analysis (Trend)](/assets/images/ai/ml-ai-subsets.png)

### Types of Machine Learning
Based on the methods and way of learning, majorly divided into following categories,
- **Supervised learning** (LABELED data - some of the data already mapped with the output)
	* Regression - Type of supervised learning. Investigate the relationship between input and output, and based on that you use to predict the continuous out variable.
	  eg. House price prediction
	* Classifification - Spam detection, Fraud detection, Churn analysis, Disease prediction<br>
	  KNN, Decision Tree, Random Forest, Logistic Regression, Naive Bayse
	* Forecasting (date time plays vital role)
- **Unsupervised learning** (UNLABELED data: News → Sports, Politics, Science, if new news comes should predict)
- **Reinforcement learning**



Dividing the data into a proper training and test data is very important. Sometimes your predictions may go wrong.<br>
Best Fit Line - Draw a line that should closest to all data points.

### Features
The features, aka independent variables or predators, are the input variables used to make predictions or classify data in a machine learning model.
These features can be numerical or categorical and represent different aspects or characteristics of the data.
For ex, in a model predicting house prices, features could include the number of bedrooms, square footage, location and age of the house.
(simply called those columns which helps in model buildings)

| X-Variables           | Y-Variables         |
|-----------------------|---------------------|
| Features              | Target variables    |
| Independent variables | Dependent variables |
| Predators             |                     |
| Input variables       | Output variables    |

The columns which will help in the model building process are called x-variables, predators or features.
<br>
The column that you are going to predict is y-variable or dependent variable or target.

### Train-Test Split
If you pass all the records to train the model, then cannot test it perform correctly or not.<br>
You can decide the training/testing data portion with train_size or test_size attributes. No need to pass both to avoid the redundant information.
If test_size=0.2 then the train_size will be 0.8

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(x, y, test_size=0.2)
```

![Components of Time Series Analysis (Trend)](/assets/images/ai/ml-train-test-flow.png)

### Feature Scaling (data cleaning process)
Feature scaling is the method to re-scale the values present in the features. In feature scaling we convert the scale of different measurement into a single scale. It standardize the whole dataset in one range.
<br>
When we are dealing with independent variable or feautures that differ from each other in terms of range of values or unit of the features, then we have to normalize/standardize the data so that the difference in range of values doesn't affect the outcome of the data.
Simply neutralize the data (bring all data into same magnitude).

Following two are the most accepted scaling techniques,

- Standardization (Standard Scaler)
	Standardization in statistics is a process of converting data to z-score values based on the mean and standard deviation of the data.
	Standard scaler ensures that for each feature, the mean is zero and the standard deviation is 1, bringing all feature to the same magnitude. In simple words Standardization helps you to scale down your feature based on the standard normal distrubution.
	The standardize data will have mean equals to zero and the values will generally range between - 3 and +3. Almost 99.7% data will fall.

	
	$$z = \frac{x - \mu}{\sigma}$$
	
- Normalization (Min-Max Scaler) - Normalization helps you to scale down features between a range of 1 to 1.
	
	$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}}$$

```python
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import MinMaxScaler

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

scaler = MinMaxScaler(feature_range=(0, 1))
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

### Feature Encoding
Feature encoding is the process of converting __categorical data__ into numerical format so machine learning models can understand it.

Most ML algorithms (Linear Regression, Logistic Regression, SVM, Neural Networks, etc.) cannot work directly with text values like "Red", "Male", "Singapore".

#### Label Encoding
Education Level → High School < Bachelor < Master < PhD
```python
from sklearn.preprocessing import LabelEncoder
import pandas as pd

data = pd.DataFrame({
    'Education': ['High School', 'Bachelor', 'Master', 'PhD']
})

encoder = LabelEncoder()
data['Education_encoded'] = encoder.fit_transform(data['Education'])

print(data)

#Education      Education_encoded
#High School    1
#Bachelor       0
#Master         2
#PhD            3
```

#### One-Hot Encoding
Color → Red, Blue, Green
```python
import pandas as pd

data = pd.DataFrame({
    'Color': ['Red', 'Blue', 'Green']
})

encoded = pd.get_dummies(data, columns=['Color'])
print(encoded)
```

```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import Pipeline
import pandas as pd

# Sample dataset
data = pd.DataFrame({
    'Gender': ['Male', 'Female', 'Female', 'Male'],
    'Age': [25, 30, 22, 35],
    'Purchased': [0, 1, 0, 1]
})

X = data[['Gender', 'Age']]
y = data['Purchased']

# Column transformer
preprocessor = ColumnTransformer(
    transformers=[
        ('cat', OneHotEncoder(), ['Gender'])
    ],
    remainder='passthrough'
)

pipeline = Pipeline([
    ('preprocessing', preprocessor),
    ('model', LogisticRegression())
])

pipeline.fit(X, y)
```

### Regression
Regression analysis is a form of predictive modeling technique which investigate the relationship between target and features.

This technique is used for forecasting, time series modeling and finding the casual effect relationship between the variables.<br>
Variaous regression alrorithsms.
- Linear Regression/Multiple Linear Regression
- Polynomial Regression
- Lasso Regression (L1)
- Ridge Regression (L2)
- Stepwise Regression

#### Model building steps
1. Data cleaning (fillna, dropna)
1. Split data into training and test data
1. Feature scaling (Standard/Min-Max scaler)
1. Feature encoding (if categorical data available)
1. Feature engineering (feature selection)
1. Create/Train model
1. Evaluvate the model

#### Regression Metrics
These are common evaluation metrics for regression models. They measure how well a model predicts continuous values. <br>
Here’s a clear explanation of each one:
1. **Mean Absolute Error (MAE)** - Average of the absolute differences between predicted and actual values.<br>
   $$MAE=\frac{1}{n}∑∣yi​−\hat{yi}∣$$
1. **Mean Squared Error (MSE)** - Average of the squared differences between predicted and actual values.<br>
   $$MSE=\frac{1}{n}∑(yi​−\hat{yi}​)^2$$
1. **Root Mean Squared Error (RMSE)** - Square root of MSE.<br>
   $$RMSE=\sqrt{MSE}$$  
1. **R² Score (Coefficient of Determination)** - Measures how much variance in the target variable is explained by the model.<br>
   $$R^2 = 1 - \frac{SSR_{reg}}{SSM_{mean}}$$
1. **Adjusted R²** - Modified R² that penalizes adding unnecessary features. Adding relevant featuers, score will increase and if adding irrelevant features score will decrease<br>
   $$\text{Adjusted } R^2 = 1 - \left(\frac{(1 - R^2)(n - 1)}{n - k - 1}\right)$$

| Metric      | Measures                | Sensitive to Outliers |
| ----------- | ----------------------- | --------------------- |
| MAE         | Average absolute error  | ❌ No                  |
| MSE         | Average squared error   | ✅ Yes                 |
| RMSE        | Root of squared error   | ✅ Yes                 |
| R²          | Variance explained      | ❌                     |
| Adjusted R² | R² with feature penalty | ❌                     |


#### Single Linear Regression

```python
# Import libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.linear_model import LinearRegression
from sklearn.pipeline import Pipeline

from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

# --------------------------------------------------
# 1. Load dataset (download CSV from data.gov.sg)
# --------------------------------------------------
url = "https://data.gov.sg/api/action/datastore_search?resource_id=f1765b54-a209-4718-8d38-a39237f502b3&limit=5000"

data = pd.read_json(url)
records = data['result']['records']

df = pd.DataFrame(records)

print(df.head())

# --------------------------------------------------
# 2. Select features and target
# --------------------------------------------------
# Example features
X = df[['town', 'flat_type', 'floor_area_sqm', 'lease_commence_date']]
y = df['resale_price']

# --------------------------------------------------
# 3. Feature Encoding & Scaling
# --------------------------------------------------
categorical_features = ['town', 'flat_type']
numerical_features = ['floor_area_sqm', 'lease_commence_date']

preprocessor = ColumnTransformer(
    transformers=[
        ('num', StandardScaler(), numerical_features),  # Feature scaling
        ('cat', OneHotEncoder(handle_unknown='ignore'), categorical_features)  # Encoding
    ]
)

# --------------------------------------------------
# 4. Train Test Split
# --------------------------------------------------
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# --------------------------------------------------
# 5. Create Pipeline with Linear Regression
# --------------------------------------------------
model = Pipeline(steps=[
    ('preprocessor', preprocessor),
    ('regressor', LinearRegression())
])

# Train model
model.fit(X_train, y_train)

# --------------------------------------------------
# 6. Predictions
# --------------------------------------------------
y_pred = model.predict(X_test)

# --------------------------------------------------
# 7. Evaluation Metrics
# --------------------------------------------------
mae = mean_absolute_error(y_test, y_pred)
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
r2 = r2_score(y_test, y_pred)

print("Evaluation Metrics")
print("-------------------")
print("MAE :", mae)
print("MSE :", mse)
print("RMSE:", rmse)
print("R2 Score:", r2)

#Evaluation Metrics
#-------------------
#MAE : 42000.52
#MSE : 3.2e+09
#RMSE: 56568.4
#R2 Score: 0.71
```
