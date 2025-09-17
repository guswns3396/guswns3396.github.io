---
layout: page
title: Image Registration
description: Basic concepts for optimization in image registration from transformations to gradient descent as part of a take-home technical challenge
img: 
importance: 3
category: Stats & ML
related_publications: false
---
#### Method 1: Brute force alignment
This brute force method should iterate through all angles and computes the mean squared error between the transformed source image and the target image. We simply pick the angle with the minimum mean-squared error.

##### MSE
Mean-squared error is given by the following equation
$$\text{MSE} = \frac{1}{n}\sum_{i=0}^{n}{(\hat{Y_i} - Y_i)^{2}}$$

We can find the optimal angle $\theta^*$ by
$$ \theta^{*} = \underset{\theta}{\operatorname{\arg \min}}{\text{MSE}(Y, \text{rotate}(X, \theta))}$$
where $Y$ is the target image, $X$ is the source image, and $\theta$ is the angle of rotation.

#### Method 2: Least squares

Although the brute force approach works, it is obviously not the optimal approach, especially if the images are more deformed/translated/scaled than this toy example. Instead, if we manually define a few pairs of points that match between the two images, we can use a least squares approach to compute a linear transformation matrix that transforms points from the source to the target image. **Make the solutions generalizable to any transformation (scaling,rotation,translation). Print out your tranformation matrix. Display an image subtraction between target and source.**

##### Estimating transformation parameters
Transformation from source coordinate $i$ to target coordinate $x$ is done by:
$$x = Mi$$
where $M$ is the transformation matrix.

When coordinates are known but the parameters $p$ of the transformation matrix $M$ are unknown, we can convert the form
$$x = Mi$$
$$ \begin{bmatrix}x \\ y\end{bmatrix} = \begin{bmatrix}p_1 & p_2 & p_3 \\ p_4 & p_5 & p_6\end{bmatrix}\begin{bmatrix}i \\ j \\ 1\end{bmatrix} $$
to
$$b = Ap$$
$$ \begin{bmatrix}x_1 \\ y_1 \\ \vdots \\ x_n \\ y_n \end{bmatrix} = \begin{bmatrix}i_1 & j_1 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & i_1 & j_1 & 1 \\ \vdots & & & & & \vdots \\i_n & j_n & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & i_n & j_n & 1 \end{bmatrix}\begin{bmatrix}p_1 \\ p_2 \\ p_3 \\ p_4 \\ p_5 \\ p_6\end{bmatrix} $$

where $b$ is the vectorized target coordinates, $A$ is the matrix of source coordinates, and $p$ is the vectorized parameters of the transformation matrix.

From here we can use linear least squares to find $p$:
$$ \min \| Ap-b \| ^2$$
$$ p = (A^TA)^{-1}A^Tb $$

The transformation matrix $M$ is then:
$$ M = \begin{bmatrix}p_1 & p_2 & p_3 \\ p_4 & p_5 & p_6 \\ 0 & 0 & 1\end{bmatrix} $$

#### Method 3: Optimization

If we don't have a list of points but still want a transformation matrix, an alternative is an optimization approach, such as gradient descent.
We need to first define a similarity metric to minimize between the two images (for example: mean-squared error), and then we compute the gradient of this metric with respect to each of our transformation matrix elements. In each iteration of this algorithm, we apply an update to each matrix element based on the gradient value. **Make the solutions generalizable to any transformation (scaling,rotation,translation). Print out your tranformation matrix. Display an image subtraction between target and source.**

You can read more about SciPy's built-in optimizers here
https://docs.scipy.org/doc/scipy/tutorial/optimize.html

##### Gradient descent
In order to perform gradient descent, the gradient of the cost function with respect to the transformation matrix parameters is required.

The cost function can be written as the following:
$$ C = \frac{1}{n}\sum_{i,j}[I(x(i,j;\Theta), y(i,j;\Theta)) - I_R(i,j)]^2 = \frac{1}{n}\sum_{i,j}e_{ij}^2$$
where $i,j$ are coordinates of the target image, $x, y$ are functions that transform the coordinates in the target image to the coordinates of the source image using the parameters of the transformation matrix $\Theta$, and $I, I_R$ are functions that get the pixel value at the given coordinates.

The gradient of the cost function with respect to transformation matrix $\Theta$ with $K=6$ parameters is :
$$\nabla_{\Theta}{C} = \begin{bmatrix}\frac{\partial C}{\partial\Theta_1} \\ \vdots \\ \frac{\partial C}{\partial\Theta_6}\end{bmatrix}$$
where
$$ \frac{\partial C}{\partial\Theta_k} = \frac{1}{n}\sum_{i,j}{\frac{\partial C}{\partial e_{ij}}\frac{\partial e_{ij}}{\partial \Theta_k}}$$
according to the chain rule.

Here,
$$ \frac{\partial C}{\partial e_{ij}} = 2e_{ij} = 2(I(x(i,j;\Theta), y(i,j;\Theta))-I_R(i,j))$$

a.k.a. the influence function and
$$\frac{\partial e_{ij}}{\partial \Theta_k} = \frac{\partial}{\partial \Theta_k}(I(x(i,j;\Theta), y(i,j;\Theta))-I_R(i,j))$$
$$ = \begin{bmatrix}\frac{\partial x(i,j)}{\partial \Theta_k} & \frac{\partial y(i,j)}{\partial \Theta_k} \end{bmatrix}
\begin{bmatrix}\frac{\partial I(x(i,j;\Theta), y(i,j;\Theta))}{\partial x} \\ \frac{\partial I(x(i,j;\Theta), y(i,j;\Theta))}{\partial y} \end{bmatrix}$$

where the first matrix, coordinate matrix model, is a $6 \times 2$ matrix and the second matrix is the image gradient.

Since the affine transformation is given by:
$$\begin{bmatrix}x \\ y \\ 1\end{bmatrix} = \begin{bmatrix}\Theta_1 & \Theta_2 & \Theta_3 \\ \Theta_4 & \Theta_5 & \Theta_6 \\ 0 & 0 & 1\end{bmatrix} \begin{bmatrix}i \\ j \\ 1\end{bmatrix}$$
coordinate matrix model can be rewritten as:
$$ \begin{bmatrix}\frac{\partial x(i,j)}{\partial \Theta_k} & \frac{\partial y(i,j)}{\partial \Theta_k} \end{bmatrix} =
\begin{bmatrix}i & 0 \\ j & 0 \\ 1 & 0 \\ 0 & i \\ 0 & j \\ 0 & 1\end{bmatrix}$$

As for the image gradient, it can be obtained with a filter. In this example, we choose the Sobel filter.

<a href="https://github.com/guswns3396-personal/image-registration">Github</a>