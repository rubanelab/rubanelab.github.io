---
title: Deep Learning (Part - III)
date: 2026-02-03 20:14 +0300
categories: [Deep Learning, Neural Network]
tags: [python, deep learning, neural network]
author: Varatharuban
description: "Mimic the human brains"
---

### Artificial Neural Network (ANN)
An Artificial Neural Network (ANN) is a machine learning model inspired by the human brain. It consists of interconnected nodes (neurons) organized into layers that work together to learn patterns from data.

**Main Components:**

- Input Layer: Receives raw data (e.g., image pixels, sensor values).
- Hidden Layers: Perform computations using weights, bias, and activation functions
- Output Layer: Produces the final prediction (e.g., class label, value).

**How ANN Works (Simple Flow):**
- Input data enters the network.
- Each neuron multiplies inputs by weights and adds bias.
- Activation function decides the neuron output.
- Output is compared with actual value.
- Weights are updated using backpropagation and gradient descent.

**Why ANN is Useful:**
- Image recognition
- Speech processing
- Medical diagnosis
- Recommendation systems

In simple terms, ANN learns from examples and improves its predictions over time.

![Basic building block in deep learning](/assets/images/ai/dl-ann-arch.png)


```python
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers

# Sample dataset
# Study hours → Pass(1) / Fail(0)
X = np.array([[1], [2], [3], [4], [5], [6]])
y = np.array([[0], [0], [0], [1], [1], [1]])

# Build ANN Model
model = keras.Sequential([
    layers.Dense(4, activation='relu', input_shape=(1,)),  # Hidden layer
    layers.Dense(1, activation='sigmoid')                  # Output layer
])

# Compile model
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)

# Train model
model.fit(X, y, epochs=100, verbose=0)

# Test prediction
test = np.array([[4.5]])
prediction = model.predict(test)

print("Prediction:", prediction)
```

**Code Explanation**
- Dense Layer → Fully connected neural layer
- ReLU Activation → Helps learn complex patterns
- Sigmoid Activation → Outputs probability (0 to 1)
- Adam Optimizer → Adjusts weights efficiently
- Binary Crossentropy → Measures prediction error