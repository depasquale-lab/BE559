# Lecture 3.4: Clustering

> **Figure:** Two side-by-side scatter plots. Left, "classification": axes $x_1$ (horizontal) and $x_2$ (vertical), red points in the lower left and blue points in the upper right, separated by a diagonal line. Labeled "supervised learning". Right, "clustering": axes $x_1$ and $x_2$, two groups of black points, one circled in red (lower left) and one circled in blue (upper right). Labeled "unsupervised learning".

Clustering:

- Group based on similarity
- Discover structure in data

## 2 Approaches to clustering

1. **Partitioning** $\rightarrow$ divides observations into non-overlapping classes
2. **Hierarchical clustering** $\rightarrow$ builds a hierarchy of classes (e.g. tree of life)

Example (red): Humans $\rightarrow$ primates $\rightarrow$ mammals $\rightarrow$ vertebrates $\rightarrow$ animals $\rightarrow$ Eukaryotes

## K-means clustering (partitioning)

**IDEA:** Assume there are $K$ clusters

- Create groupings that are as compact as possible

$\Rightarrow$ Central to all clustering techniques is the choice of distance measure between points/clusters.

**Distance metric:** Euclidean distance

**Formally:** Minimize

$$J = \sum_{n=1}^{N} \sum_{k=1}^{K} r_{n,k} \, \lVert x_n - \mu_k \rVert^2$$

- $J$: objective function
- $N$: data points
- $K$: clusters
- $\lVert x_n - \mu_k \rVert^2$: squared Euclidean distance from points ($x_n$) to cluster centroids ($\mu_k$)
- $r_{n,k}$: cluster assignments

$$r_{n,k} = \begin{cases} 1, & \text{if } x_n \text{ in cluster } k \\ 0, & \text{if } x_n \text{ not in cluster } k \end{cases}$$

## How to minimize $J$?

Gradient descent? $\Rightarrow$ Unfortunately, this will not work.

Why?

- $r_{n,k}$ (cluster assignments) depend on $\mu_k$
- $\mu_k$ (cluster centroids) depend on $r_{n,k}$

$\Rightarrow$ We call $r_{n,k}$ a **latent** (or hidden) **variable**.

**Example: Baby's mood**

- Can't measure it directly
- Can't ask about it
- Can only build a model to try and infer it
  - $\Rightarrow$ facial expressions, noises, activity level, etc.

(Annotation in red: mood controls all of those things.)

## What is our recourse?

$\Rightarrow$ Local minima of $J(\mathcal{X} \mid r_{n,k}, \mu_k)$ can be found with an iterative algorithm.

## The K-means algorithm

1. Guess $\mu_k$ (even randomly)
2. Determine $r_{n,k}$ based on $\mu_k$ (annotation: if $\mu_k$ is the closest cluster centroid to $x$)
3. Recompute $\mu_k$ based on $r_{n,k}$
4. Repeat steps 2, 3 until $\mu_k$, $r_{n,k}$ stop changing (convergence)

**Determining $r_{n,k}$:**

$$r_{n,k} = \begin{cases} 1, & \text{if } k = \arg\min_j \lVert x_n - \mu_j \rVert^2 \\ 0, & \text{otherwise} \end{cases}$$

**Determining $\mu_k$:**

$$\frac{d}{d\mu_k} \sum_{n=1}^{N} r_{n,k} \lVert x_n - \mu_k \rVert^2 = 2 \sum_{n=1}^{N} r_{n,k} (x_n - \mu_k) = 0$$

(Sign slip in the notes fixed: the derivative of $\lVert x_n - \mu_k \rVert^2$ with respect to $\mu_k$ carries a factor of $-1$, which does not affect setting it to zero.)

$$2 \sum_{n=1}^{N} r_{n,k} x_n - 2 \sum_{n=1}^{N} r_{n,k} \mu_k = 0$$

$$\mu_k = \frac{\sum_{n=1}^{N} r_{n,k} x_n}{\sum_{n=1}^{N} r_{n,k}}$$

- Numerator $\Rightarrow$ sum of all points in cluster $k$
- Denominator $\Rightarrow$ number of points in cluster $k$

$\Rightarrow$ $\mu_k$ is the mean of all data points in cluster $k$.

## K-means algorithm: worked example

1. Guess at $\mu_k$ (even randomly)
2. Determine $r_{n,k}$ based on $\mu_k$
3. Recompute $\mu_k$ based on $r_{n,k}$
4. Repeat 2, 3

> **Figure:** A 3x3 grid of small scatter plots (panels a to i), axes roughly from $-2$ to $2$, showing two elongated blobs of data. Panel (a), circled 1: all points green, with a blue $\times$ and a red $\times$ marking the initial centroids. Panel (b), circled 2: points colored red or blue by nearest centroid, with a magenta line (the decision boundary between the two centroids) and an arrow pointing to it. Panel (c), circled 3: centroids recomputed and drawn as large black dots. Panels (d) to (i) alternate circled 2 and 3 (assign, then recompute): the magenta boundary line shifts and the $\times$ centroids move toward the centers of the blue (lower left) and red (upper right) groups. By the last panel the assignments no longer change, annotated "$\Rightarrow$ Done".
