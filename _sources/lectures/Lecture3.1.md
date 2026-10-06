# Lecture 3.1: Classification and Discriminant Functions

## Module 3: Classification and clustering

> **Figure:** Two side-by-side scatter plots, both with axes gene 1 (x) and gene 2 (y). Left, "Classification": a cluster of red points labeled "cancerous" (upper right) and a cluster of blue points labeled "normal" (lower left), separated by a diagonal line. Right, "Clustering": two groups of unlabeled points (black), one circled in red (lower left) and one circled in blue (upper right).

**Classification** ⇒ "supervised learning"
- Determine a *rule* to assign labels to new data based on previous observations.

**Clustering** ⇒ "unsupervised learning"
- Groups points based on similarity.
- Discover structure in data.

**First: classification.** Three approaches:

1. Discriminant function: $\text{Class} = G(x)$
2. Conditional probability models: $P(\text{class} \mid x)$
3. Generative models: $P(x, \text{class}) \Rightarrow P(\text{class} \mid x)$

## Discriminant functions

$$\text{Class} = G(x)$$

How do we choose $G$? It depends on your goals.

Common goals:

1. Minimize misclassification
2. Minimize loss

> **Figure:** Two overlapping bell curves along one axis, "normal" (red, left) and "cancer" (blue, right). Two candidate thresholds are drawn: a dotted/purple vertical line placed further left (marked with a purple arrow, associated with minimizing loss) and a solid purple/green vertical line at the curves' crossing point (marked with a green arrow, associated with minimizing misclassification).

### 1-D classification

> **Figure:** Two overlapping bell curves on a horizontal axis: "Negative" (red, left) and "Positive" (blue, right). A dotted vertical line marks the "threshold". Regions are shaded: green under the negative curve left of the threshold, blue under the positive curve right of the threshold, a red-shaded sliver of the negative curve's tail to the right of the threshold, and a purple-shaded sliver of the positive curve's tail to the left of the threshold.

- True positives (TP) (blue)
- False positives (FP) (purple)
- True negatives (TN) (green)
- False negatives (FN) (red)

> **Figure:** The same two curves with the threshold, now with the positive curve labeled "P" and the TP region marked. A purple arrow below the axis points to the left (low sensitivity-end region) and a green arrow points to the right of the positive peak.

**Sensitivity** (or true positive rate):

$$\text{Sensitivity} = \frac{TP}{P}$$

**Specificity** (or true negative rate):

$$\text{Specificity} = \frac{TN}{N}$$

**Accuracy:**

$$\text{Accuracy} = \frac{TP + TN}{TP + FP + TN + FN}$$

**High sensitivity** ⇒ cancer screening

**High specificity** ⇒ nuclear retaliation

⇒ All of this describes how two groups are classified based on a 1-D threshold.

## Threshold agnostic measures

$d'$ = "d prime" = discriminability index (also: detectability, sensitivity)

$$d' = \frac{|\mu_2 - \mu_1|}{\sigma}$$

> **Figure:** Top: two overlapping bell curves, blue with mean $\mu_1$ (left) and red with mean $\mu_2$ (right), with a dotted vertical threshold between them; double-headed arrows beneath each curve are labeled $\sigma$. Bottom: two narrower, well-separated bell curves (blue left, red right) with a dotted threshold between them and almost no overlap.

⇒ "Mahalanobis distance" in higher-D

## ROC curves (receiver operating characteristic)

- ⇒ threshold agnostic
- ⇒ 1-D data
- ⇒ AUC: how separable are classes

> **Figure:** Left: the 1-D classification plot (negative red curve, positive blue curve, dotted threshold, shaded TP/FP/TN/FN regions) with a purple arrow below it. Right: an ROC plot with $\text{TPR} = TP/P$ on the y-axis and $\text{FPR} = FP/N$ on the x-axis, both running from 0 to 1. A diagonal line runs from (0,0) to (1,1); a concave curve bows above it through the upper left, with a few points marked along it. The area under the curve is shaded pink and labeled "AUROC".

AUROC: how separable.
- 1: perfectly separable
- 0.5: not distinguishable

## Discriminant functions and higher-D classification

$$\text{Class} = G(x)$$

Simple case: linear discriminants.

Let $x = [x_1, x_2, \ldots, x_D]$ in $D$-dimensional space.

> **Figure:** In 2-D (axes $x_1$ horizontal, $x_2$ vertical), a red cluster (lower left) and a blue cluster (upper right) separated by a diagonal line labeled "boundary". An arrow perpendicular to the boundary is labeled "discriminant vector". Marginal 1-D distributions (red and blue bell curves) are drawn along each axis, and blue/red arrows show points projected onto the discriminant vector.

**Boundary:**

| Data | Boundary |
|---|---|
| 1-D data | point (0D) |
| 2-D data | line (1D) |
| 3-D data | plane (2D) |
| ... | ... |
| $n$-D data | $D-1$ dimensional hyperplane |

**Discriminant:** vector orthogonal to boundary.

### Linear discriminant

$$y = G(x) = W x^T, \qquad x = [x_1, x_2], \quad W = [w_1, w_2]$$

$$W x^T = x_1 w_1 + x_2 w_2$$

= distance from origin to projection of $x$ onto vector $W$.

> **Figure:** The 2-D plot again with classes 1 (red) and 2 (blue), the boundary, and the discriminant vector. Several parallel purple lines are drawn perpendicular to the discriminant vector, showing points projected onto it. A green segment labeled $w_0$ runs from the origin along the discriminant vector to the boundary. Class 1 and class 2 marginal distributions are drawn along the projection direction.

- ⇒ Right back to 1-D data.
- ⇒ Just like before, now we need a threshold.
- ⇒ How to choose $w_0$?

$$G(x) = \begin{cases} 1, & W x^T < w_0 \\ 2, & W x^T \geq w_0 \end{cases}$$

### Choosing $w_0$ and $W$

> **Figure:** A 2-D plot with a red cluster (mean $\mu_1$) and a blue cluster (mean $\mu_2$). The discriminant vector is parallel to the line joining the two means; the boundary passes through the midpoint between them, perpendicular to that line.

Discriminant vector: parallel to $\mu_2 - \mu_1$.

$$W = (\mu_2 - \mu_1), \qquad w_0 = \frac{\mu_1 + \mu_2}{2}\ \text{(the threshold point, midway between the means)}$$

$$y(x) = W x^T - w_0$$

$$G(x) = \begin{cases} 1, & W x^T - w_0 < 0 \\ 2, & W x^T - w_0 \geq 0 \end{cases}$$

$y(x) = 0$ when $W x^T = W\left(\frac{\mu_1 + \mu_2}{2}\right)^T = w_0$

$$w_0 = (\mu_2 - \mu_1)\left(\frac{\mu_1 + \mu_2}{2}\right)^T$$

## What if data look like this?

> **Figure:** A 2-D scatter of red and blue points forming elongated, tilted, overlapping clouds, with means $\mu_1$ (red) and $\mu_2$ (blue) marked. A vertical line through the midpoint, perpendicular to the line joining the means, is drawn as the boundary and clearly cuts through both clouds.

Clearly not the best boundary. Why? $x_1$ and $x_2$ covary:

$$\text{Cov}(x_1, x_2) = \begin{bmatrix} \text{Var}(x_1) & a \\ a & \text{Var}(x_2) \end{bmatrix}, \qquad a \neq 0$$

## Fisher's linear discriminant

Linear discriminant analysis (LDA).

Fisher's criterion: maximize

$$J(W) = \frac{(m_1 - m_2)^2}{s_1^2 + s_2^2}, \qquad m_i = W \mu_i^T$$

- Numerator: separation between class means along discriminant vector.
- Denominator: within-class variances along decision vector.

> **Figure:** Two small pairs of bell curves (red and blue): one pair overlapping heavily, one pair more separated, illustrating the criterion.

⇒ Essentially the vector along which $d'$ is maximized.

### Finding $W$

How to find $W$ that maximizes $J(W)$?
- Take $\frac{dJ}{dW}$, use gradient descent...

$J(W)$ is maximized when

$$W \propto \Sigma_w^{-1} (\mu_2 - \mu_1)$$

where $\Sigma = \text{Cov}(x_1, x_2)$ is the within-class covariance.

> **Figure:** The 2-D plot with red and blue clusters, a tilted discriminant vector, and the boundary perpendicular to it. Points from each cluster are projected onto the discriminant vector, with the class means marked by black dots.

For now:

$$w_0 = W\left(\frac{\mu_2 + \mu_1}{2}\right)^T$$

Remember: choice of threshold depends on goals.

⇒ LDA assumes within-class covariance is the same for both classes.
