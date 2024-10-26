---
title: Loss Functions
layout: tutorial
description: Learn about the different loss functions used in Human Pose Estimation.
parent: Advanced Topics
order: 2
---

This page contains a list of loss functions commonly used for human pose estimation.

## Mean Squared Error (MSE)

Human Pose Estimation is a regression problem where the model tries to regress to the the correct coordinates, i.e., move to the ground truth coordinates in small increments. The most common loss function used to train the model to output these continuous coordinates is the Mean Squared Error (MSE). The MSE is calculated as the average of the squared difference between the predicted and ground truth coordinates.

$$
\begin{align}
MSE = \frac{1}{N}\sum_{i=1}^{N} (y_i - \hat{y}_i)^2
\end{align}
$$

where $N$ is the number of samples, $y_i$ is the ground truth coordinate and $\hat{y}_i$ is the predicted coordinate.

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
