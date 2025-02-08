---
title: Common Loss Functions for Pose Estimation
layout: tutorial
subtitle: "Key Loss Functions for Training Accurate Pose Models"
description: "Understand essential loss functions, such as MSE, L1, and heatmap-based losses, used to optimize pose estimation networks."
parent: Basic Concepts
order: 4
---

Understand essential loss functions, such as MSE, L1, and heatmap-based losses, used to optimize pose estimation networks.


This page contains a list of loss functions commonly used for human pose estimation.

## Mean Squared Error (MSE)

Human Pose Estimation is a regression problem where the model tries to regress to the the correct coordinates, i.e., move to the ground truth coordinates in small increments. The most common loss function used to train the model to output these continuous coordinates is the Mean Squared Error (MSE). The MSE is calculated as the average of the squared difference between the predicted and ground truth coordinates.

$$
\begin{align}
MSE = \frac{1}{N}\sum_{i=1}^{N} (y_i - \hat{y}_i)^2
\end{align}
$$

where $N$ is the number of samples, $y_i$ is the ground truth coordinate and $\hat{y}_i$ is the predicted coordinate.
