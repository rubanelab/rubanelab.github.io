---
title: Deep Learning (Part - I)
date: 2026-01-15 20:14 +0300
categories: [Deep Learning, Neural Network]
tags: [python, deep learning, neural network]
author: Varatharuban
description: "Mimic the human brains"
---

### Introduction
Machine Learning is a area of research, through which you can archive AI. Deep Learning is further subfield of Machine Learning.
Innovations in fields like image identification, natural language processing, and autonomous systems have been made possible by deep learning, which has completely changed how we tackle difficult issues.

Will cover following,
- Neurons and Activation Functions
- Artificial Neural Networks (ANN): structure of ANNs, how they operate, and how to train them using backpropagation and optimization techniques.
- Convolutional Neural Networks (CNN): particularly powerful for processing grid-like data, such as images and explore how convolutional layers work, the role of pooling, and how CNNs have become the go-to model for computer vision tasks.
- Recurrent Neural Networks (RNN): designed for sequence prediction and processing temporal data and how RNNs maintain context across sequences and the challenges they address, such as handling variable-length inputs.
- Generative Adversarial Networks (GAN)
- Pre-Trained Models: explore various popular pre-trained models and frameworks that have been developed by the deep learning community. how to implement and fine-tune these models for your specific use cases, giving you a head start in developing robust applications.
- Transfer Learning: allows us to leverage pre-trained models to improve performance on new tasks with limited data. discover how to utilize existing models effectively, saving time and computational resources while achieving high accuracy.



### Neurons
Neurons is the fundamental building blocks of deep learning. It's simple computational units mimic the functioning of biological neurons and how they are activated through various activation functions like Sigmoid, ReLU, and Tanh.
Like a decision makers.

![Basic building block in deep learning](/assets/images/ai/dl-basic-building-block.png)

Weights are simply how strong the connection is.
How importance or influence of the feature.




### Activation Functions
Activation function is part of multiple layers, which decides wheather the neuron should be fired or not.
If activation function is 0, then particular node will be inactive or passive.

#### Step Function
The step function is a basic threshold activation function used in early neural networks, but it’s not suitable for training deep neural networks with backpropagation.
Modern deep learning rarely uses the step function because:
- It is not differentiable
- Gradient is zero almost everywhere
- Cannot use gradient descent effectively

![Basic building block in deep learning](/assets/images/ai/dl-activation-fn-step.png)

#### Linear Function
A linear function in deep learning is the basic transformation applied to inputs before an activation function. It performs a weighted sum of the inputs plus a bias.

It is written as:

![Basic building block in deep learning](/assets/images/ai/dl-activation-fn-linear.png)

#### Sigmoid Function
The sigmoid function is a smooth, S-shaped activation function used in neural networks.
The sigmoid function squashes input values into a probability-like range (0 to 1), making it useful for binary classification, but it’s less common in hidden layers of modern deep networks due to training inefficiencies.

![Basic building block in deep learning](/assets/images/ai/dl-activation-fn-sigmoid.png)

#### TanH Function
The TanH (Hyperbolic Tangent) function is an activation function used in neural networks.

![Basic building block in deep learning](/assets/images/ai/dl-activation-fn-tanH.png)

TanH is a zero-centered activation function that maps inputs to values between −1 and 1. It improves on sigmoid but is less commonly used in deep feedforward networks compared to ReLU.

#### ReLU Function
ReLU (Rectified Linear Unit) is one of the most widely used activation functions in modern neural networks.

![Basic building block in deep learning](/assets/images/ai/dl-activation-fn-relu.png)

ReLU is a simple, efficient activation function that outputs zero for negative values and keeps positive values unchanged. It is the default choice for hidden layers in most deep learning models today.