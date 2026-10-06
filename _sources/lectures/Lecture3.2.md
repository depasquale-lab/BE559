# Lecture 3.2: From LDA to Probabilistic Classifiers and Naive Bayes

## Review: 3 approaches

1. Discriminant functions: $G(x) = \text{class}$
2. Probabilistic discriminative models: $P(\text{class}\mid x) \Rightarrow \text{class}$
3. Generative models: $P(x, \text{classes}) \Rightarrow P(\text{class}\mid x) \Rightarrow \text{class}$

### LDA

$$G(x) = \begin{cases} 1, & y(x) < 0 \\ 2, & y(x) > 0 \end{cases}$$

$$y(x) = W x^T - W_0$$

Maximize $J(W) \Rightarrow$ maximize $d'$ along the discriminant vector $\Rightarrow$ find the vector such that the projections of $x$ onto the vector are most discriminable.

$$W = \Sigma_W^{-1}(\mu_2 - \mu_1)^T \qquad (\Sigma_W:\ \text{within-class covariance})$$

$$W_0 = W\left(\frac{\mu_2 + \mu_1}{2}\right)^T$$

> **Figure:** Scatter plot with axes $x_1$ (horizontal) and $x_2$ (vertical). Class 1 (red dots) lies in the lower left and Class 2 (blue dots) in the upper right. A diagonal line labeled "boundary" separates them, and an arrow perpendicular to it is labeled "discrim. vector". Along the discriminant vector, a red and a blue bell-shaped curve (the projected class distributions) are drawn overlapping.

## Probabilistic discriminative model

$P(\text{class}\mid x) \Rightarrow$ choose class.

> **Figure:** The same two-class scatter plot as above (axes $x_1$, $x_2$; Class 1 red, Class 2 blue; boundary line; discrim. vector arrow with red and blue projected curves), with a green outline drawn around the points and curves.

> **Figure:** Two overlapping bell curves, red (class 1) on the left and blue (class 2) on the right, drawn on an axis labeled "Proj onto discr. vector ($y(x)$)".

> **Figure:** Plot of class label (vertical axis, values 1 and 2) versus $y(x)$ (horizontal axis). Red circles (class 1) lie along the bottom line at 1 and blue circles (class 2) along the top line at 2, with a few overlapping near the middle. An S-shaped curve rises from 1 to 2, labeled "looks like $P(\text{class } 2 \mid y(x))$".

$\Rightarrow$ Reminiscent of logistic regression!

## Deriving $P(C_1\mid x)$ from a generative model

Want

$$P(C_1\mid x) = \frac{P(x\mid C_1)P(C_1)}{P(x)} = \frac{P(x\mid C_1)P(C_1)}{P(x\mid C_1)P(C_1) + P(x\mid C_2)P(C_2)}$$

$$= \frac{1}{1 + \dfrac{P(x\mid C_2)P(C_2)}{P(x\mid C_1)P(C_1)}}$$

$$= \frac{1}{1 + \exp\left(\ln\left(\dfrac{P(x\mid C_2)P(C_2)}{P(x\mid C_1)P(C_1)}\right)\right)}$$

$$= \frac{1}{1 + \exp\left(-\ln\left(\dfrac{P(x\mid C_1)P(C_1)}{P(x\mid C_2)P(C_2)}\right)\right)}$$

$$P(C_1\mid x) = \frac{1}{1 + \exp(-a)} \qquad \text{where } a = \ln\left(\frac{P(x\mid C_1)P(C_1)}{P(x\mid C_2)P(C_2)}\right)$$

This is the **logistic function**.

### Gaussian class-conditional densities with shared covariance

$$a = \ln\left(\frac{P(x\mid C_1)P(C_1)}{P(x\mid C_2)P(C_2)}\right)$$

$$P(x\mid C_k) = \frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}}\exp\left(-\frac{1}{2}(x-\mu_k)^T\Sigma^{-1}(x-\mu_k)\right)$$

$$a = \ln\left(\frac{P(C_1)}{P(C_2)}\right) + \ln\left(\frac{\frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}}\exp\left(-\frac{1}{2}(x-\mu_1)^T\Sigma^{-1}(x-\mu_1)\right)}{\frac{1}{(2\pi)^{D/2}|\Sigma|^{1/2}}\exp\left(-\frac{1}{2}(x-\mu_2)^T\Sigma^{-1}(x-\mu_2)\right)}\right)$$

The normalization constants cancel, and the $\ln$ and $\exp$ cancel:

$$= \ln\left(\frac{P(C_1)}{P(C_2)}\right) + \left[-\frac{1}{2}(x-\mu_1)^T\Sigma^{-1}(x-\mu_1) + \frac{1}{2}(x-\mu_2)^T\Sigma^{-1}(x-\mu_2)\right]$$

$$= \ln\left(\frac{P(C_1)}{P(C_2)}\right) - \frac{1}{2}\left(x^T\Sigma^{-1}x - \mu_1^T\Sigma^{-1}x - x^T\Sigma^{-1}\mu_1 + \mu_1^T\Sigma^{-1}\mu_1\right) + \frac{1}{2}\left(x^T\Sigma^{-1}x - \mu_2^T\Sigma^{-1}x - x^T\Sigma^{-1}\mu_2 + \mu_2^T\Sigma^{-1}\mu_2\right)$$

The $x^T\Sigma^{-1}x$ terms cancel. Collecting the remaining terms:

$$= \underbrace{\ln\left(\frac{P(C_1)}{P(C_2)}\right) - \frac{1}{2}\mu_1^T\Sigma^{-1}\mu_1 + \frac{1}{2}\mu_2^T\Sigma^{-1}\mu_2}_{\text{independent of } x\ (\text{constant})} + \mu_1^T\Sigma^{-1}x - \mu_2^T\Sigma^{-1}x$$

$$\Rightarrow (\mu_1^T - \mu_2^T)\Sigma^{-1}x$$

The vector $(\mu_1 - \mu_2)^T\Sigma^{-1}$ is $W$ in LDA.

$$P(C_1\mid x) = \sigma(-a)$$

$$a = \underbrace{\ln\left(\frac{P(C_1)}{P(C_2)}\right) - \frac{1}{2}\mu_1^T\Sigma^{-1}\mu_1 + \frac{1}{2}\mu_2^T\Sigma^{-1}\mu_2}_{W_0} + \underbrace{(\mu_1 - \mu_2)^T\Sigma^{-1}x}_{W^Tx}$$

So

$$a = y(x) = W^Tx + W_0$$

$$P(C_1\mid x) = \sigma(-y(x))$$

This is Fisher's linear discriminant with a particular choice of threshold.

- This insight takes us from a discriminant function to a probabilistic classifier.
- Prior probabilities ($P(C_1)$, $P(C_2)$) only affect $W_0$.

## What assumptions have we made?

1. Within-class covariances are identical.
2. $P(x\mid C_k)$ are normally distributed.

Also, one limitation:

3. Not clear how to scale this to multi-class problems.

## Another approach: Naive Bayes classifier

- Central assumption: no covariance between features.

In 2-D:

$$\Sigma = \begin{bmatrix} \mathrm{Var}(x_1) & 0 \\ 0 & \mathrm{Var}(x_2)\end{bmatrix}$$

> **Figure:** Two-dimensional plot with concentric red circular contours around a cluster of red points near the origin, plus a small cluster of blue points up and to the right, outside the contours. Small tick marks along the horizontal axis mark positions at increasing distance from the red cluster. This illustrates uncorrelated (circular) feature distributions.

> **Figure:** Labeled "Not This". A scatter plot of red and blue points where the features are correlated, so each cloud is a diagonal, downward-sloping elongated shape.

$\Rightarrow$ But it often doesn't matter too much if they are weakly correlated.

## Naive Bayes

Still want $P(C_k\mid x)$.

$$G(x) = \begin{cases} 1, & P(C_1\mid x) > P(C_2\mid x) \\ 2, & P(C_1\mid x) < P(C_2\mid x)\end{cases}$$

$$P(C_k\mid x) = \frac{P(C_k)P(x\mid C_k)}{P(x)} \qquad \text{(Bayes' rule)}$$

$P(x)$ is the same for all classes (i.e. a constant), so

$$P(C_k\mid x) \sim P(C_k)P(x\mid C_k)$$

$\Rightarrow$ easily extends to multi-class problems.

**Chain rule / conditional probability**

$$P(A,B) = P(A)P(B\mid A)$$

$$P(A,B,C) = P(A)P(B\mid A)P(C\mid B,A)$$

**Independence of random variables**

$$P(A,B) = P(A)P(B)$$

### Derivation

$$P(C_k\mid x) \sim P(C_k)P(x\mid C_k)$$

$$P(C_k)P(x\mid C_k) = P(x, C_k) = P(x_1, x_2, \ldots, x_n, C_k)$$

$$= P(x_1\mid x_2, x_3, \ldots, x_n, C_k)\,P(x_2, x_3, \ldots, x_n, C_k)$$

$$= P(x_1\mid x_2, x_3, \ldots, x_n, C_k)\,P(x_2\mid x_3, \ldots, x_n, C_k)\,P(x_3, \ldots, x_n, C_k)$$

$$= P(x_1\mid x_2, x_3, \ldots, x_n, C_k)\cdot P(x_2\mid x_3, \ldots, x_n, C_k)\cdots P(x_n\mid C_k)P(C_k)$$

$\Rightarrow$ Now our assumption: $x_1, x_2, x_3, \ldots, x_n$ are independent (given the class).

$$= P(x_1\mid C_k)P(x_2\mid C_k)\cdots P(x_n\mid C_k)\cdot P(C_k)$$

$$= P(C_k)\prod_{i=1}^{n}P(x_i\mid C_k)$$

$$P(C_k\mid x) \propto P(C_k)\prod_{i=1}^{n}P(x_i\mid C_k)$$

- $P(C_k)$: relative frequency of each class.
- $P(x_i\mid C_k)$: estimate a parametric model, e.g. $\mu_k$, $\sigma_k$ of a normal distribution, OR estimate the probability density using a nonparametric method, e.g. histogram $\Rightarrow$ "kernel density estimation".

For a normal distribution:

$$P(x_i = a\mid C_k) = \frac{1}{\sqrt{2\pi\sigma_k^2}}\exp\left(-\frac{(a-\mu_k)^2}{2\sigma_k^2}\right)$$
