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

Machine Learning is a subset of AI, that provides computers with the ability to learn without being explicitly programed. ML focuses on the development of computer programs that can teach themselves to grow and change when exposed to new data.
- Automatically learn
- Improve performance from past experience
- Make predictions

![Components of Time Series Analysis (Trend)](/assets/images/ai/ml-ai-subsets.png)

### Types of Machine Learning
Based on the methods and way of learning, majorly divided into following categories,
- **Supervised learning** (labeled data - some of the data already mapped with the output)
	* Classifification - spam detection, fraud detection, churn analysis, disease prediction
	  KNN, Decision Tree, Random Forest, Logistic Regression, Naive Bayse, 
	* Regression - another type of supervised learning. there is a relationship between input and output, and based on that you use to predict the continuous out variable.
		House price prediction
	* Forecasting (date time plays vital role)
- **Unsupervised learning** (unlabeled data: news -> sports, politics, cinema, if new news comes should predict)
- **Reinforcement learning**



Diving the data into a proper training and test data is very important. Sometimes your predictions may go wrong.
Draw a line that should closest to all data points (best fit line).

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

### Train-Test Split
If you pass all the records to train the model, how can we test it perform correctly or not?

![Components of Time Series Analysis (Trend)](/assets/images/ai/ml-train-test-flow.png)

### Feature scaling (data cleaning process)
Feature scaling is the method to re-scale the values present in the features. In feature scaling we convert the scale of different measurement into a single scale. It standardize the whole dataset in one range.
<br>
When we are dealing with independent variable or feautures that differ from each other in terms of range of values or unit of the features, then we have to normalize/standardize the data so that the difference in range of values doesn't affect the outcome of the data.
- Standardization (Standard Scaler)
	Standardization in statistics is a process of converting data to z-score values based on the mean and standard deviation of the data.
	Standard Scaler ensures that for each feature, the mean is zero and the sta
- Normalization (Min-Max Scaler)
	Normalization helps you to scale down features between a range of 1 to 1.
