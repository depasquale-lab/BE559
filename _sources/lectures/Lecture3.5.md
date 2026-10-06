# Lecture 3.5: Gaussian Mixture Models and Expectation-Maximization

- Gaussian Mixture Models (GMMs): the next step up from K-means
- Expectation Maximization (EM): a common algorithm used in statistical modelling

## First: K-means Review

- Assume data can be grouped into $K$ clusters
- Create groupings that are as compact as possible
- Minimize

$$J = \sum_{n=1}^{N}\sum_{k=1}^{K} r_{n,k}\,\lVert x_n - \mu_k \rVert^2$$

  - $r_{n,k} \in \{0,1\}$: cluster assignments
  - $\lVert x_n - \mu_k \rVert$: Euclidean distance from points to cluster centroids

Algorithm:

1. Initialize $\mu_k$
2. Determine $r_{n,k}$ based on $\mu_k$
3. Recompute $\mu_k$ based on $r_{n,k}$
4. Repeat 2, 3 until convergence

## Limitations of K-means

- Assumes all clusters are the same size (in terms of $\sigma^2$ and number of points)
- Assumes no covariance between features
- Hard assignments of each point to a cluster
  - Better if we knew $P(\text{cluster}=k \mid x)$

> **Figure:** Three scatter plots of K-means results, points colored by assigned cluster (teal, yellow, purple). Left, "Anisotropically Distributed Blobs": elongated diagonal streaks split incorrectly. Middle, "Unevenly Sized Blobs": a small group circled in purple at upper right, and a green circle around a large yellow cluster and the adjacent purple cluster, marking the poor split. Right, "Unequal Variance": a large diffuse yellow cluster, a teal cluster, and a tight purple cluster, with boundaries that do not follow the true clusters.

## More Flexible: Gaussian Mixture Models (GMMs)

- Explicitly model data as composed of several multivariate Gaussian distributions, each with their own $\mu_k$, $\Sigma_k$.

$\Rightarrow$ Addresses the three weaknesses of K-means above.

## Mixture of Gaussians

Assume data are drawn from a **mixture of Gaussians** distribution:

$$P(x) = \sum_{k=1}^{K} \pi_k\, \mathcal{N}(x \mid \mu_k, \Sigma_k), \qquad \sum_{k=1}^{K}\pi_k = 1$$

- $\mathcal{N}(x\mid\mu_k,\Sigma_k)$: normal distribution
- $\pi_k$: **mixing coefficients** = how much each Gaussian contributes to the overall density

$K$ Gaussians mixed together.

> **Figure:** Left, "1-D": $P(x)$ versus $x$ with three component Gaussians labeled $K=1$ (red, medium bump on the left), $K=2$ (green, low and broad), and $K=3$ (blue, tall bump on the right). A purple curve, the mixture of $K=3$ Gaussians, is their sum and shows two humps.
>
> **Figure:** Right, "2-D": nested contour ellipses in purple, green and red. The wide outer contours are annotated "$\pi$ small" and the tight red contours "$\pi$ large (lots of points)".

$\Rightarrow$ Each Gaussian represents a cluster.

## K-means vs. GMMs

- **K-Means:** Model data as belonging to one of $K$ clusters with centroids $\mu_k$.
- **GMMs:** Model data as drawn from a mixture of Gaussians distribution parameterized by centroids $\mu_k$, covariances $\Sigma_k$, and mixing coefficients $\pi_k$.

Want to find:

1. $\mu$'s, $\Sigma$'s, $\pi$'s that maximize $P(X \mid \mu, \Sigma, \pi)$ $\Rightarrow$ maximum likelihood solution
2. $P(\text{cluster} \mid x)$
   - = probabilistic cluster assignment
   - = probability of a point belonging to each cluster
   - = a **latent** variable
   - = "responsibilities"

## Strategy

Maximize the likelihood, $P(X \mid \mu, \Sigma, \pi)$, with respect to $\mu, \Sigma, \pi$.

A helpful variable:

$$N_k = \sum_{n=1}^{N} P(\text{cluster}=k \mid x_n)$$

This is the "effective" number of points belonging to each cluster.

When we maximize $P(X\mid\mu,\Sigma,\pi)$ with respect to $\mu$, we get

$$\mu_k = \frac{1}{N_k}\sum_{n=1}^{N} P(\text{cluster}=k\mid x_n)\, x_n$$

$\Rightarrow$ weighted centroid.

Now maximize $P(X\mid\mu,\Sigma,\pi)$ with respect to $\Sigma$:

$$\Sigma_k = \frac{1}{N_k}\sum_{n=1}^{N} P(\text{cluster}=k\mid x_n)\,(x_n-\mu_k)(x_n-\mu_k)^T$$

And with respect to $\pi$:

$$\pi_k = \frac{N_k}{N}$$

## Summary of the Updates

$$\mu_k = \frac{1}{N_k}\sum_{n=1}^{N} P(\text{cluster}=k\mid x_n)\, x_n$$

$$\Sigma_k = \frac{1}{N_k}\sum_{n=1}^{N} P(\text{cluster}=k\mid x_n)\,(x_n-\mu_k)(x_n-\mu_k)^T$$

$$\pi_k = \frac{N_k}{N} = \frac{1}{N}\sum_{n=1}^{N} P(\text{cluster}=k\mid x_n)$$

- Optimal $\mu_k, \Sigma_k, \pi_k$ depend on $P(\text{cluster}=k\mid x_n)$ (the cluster assignments)
- $P(\text{cluster}=k\mid x_n) = \mathcal{N}(\mu_k,\Sigma_k,\pi_k)$ $\Rightarrow$ depends on $\mu_k, \Sigma_k, \pi_k$

Just like K-means except:

1. $P(\text{cluster}\mid x)$ instead of $r_{n,k}$
2. $\mu_k, \Sigma_k, \pi_k$ instead of only $\mu_k$

## The Expectation-Maximization (EM) Algorithm

> "an elegant and powerful method for finding maximum likelihood solutions for models with latent variables" (Bishop)

- Iterate between Expectation and Maximization steps

**Expectation:** Use the current value of parameters ($\mu_k, \Sigma_k, \pi_k$) to evaluate responsibilities, $P(\text{cluster}=k\mid x)$.

$$P(\text{cluster}=k\mid x_n) = \frac{\pi_k\,\mathcal{N}(x_n\mid\mu_k,\Sigma_k)}{\sum_{j=1}^{K}\pi_j\,\mathcal{N}(x_n\mid\mu_j,\Sigma_j)}$$

- Numerator: density at $x_n$ of cluster $k$
- Denominator: sum of densities across clusters

> **Figure:** A 1-D mixture of three Gaussians with components labeled 1 (red, left), 2 (green, broad and low) and 3 (blue, right). Two points are marked on the axis: one $x_n$ (purple dashed line) falling where only component 2 has density, annotated $P(\text{cluster}=2\mid x_n)=1$; and a second $x_n$ (orange dashed line) where components 2 and 3 overlap, annotated $P(\text{cluster}=3\mid x_n)=0.5$.

**Maximization:** Re-estimate parameters ($\mu_k, \Sigma_k, \pi_k$) using the responsibilities (equations from the previous slide).

$\Rightarrow$ Repeat E and M steps until convergence

$\Rightarrow$ Each EM iteration is guaranteed to increase $P(X\mid\mu,\Sigma,\pi)$, unless at a maximum

> **Figure:** Left, a 2x2 panel of GMM clustering results ("Ground truth clusters"): "Mixture of Gaussian Blobs", "Anisotropically Distributed Blobs", "Unequal Variance", and "Unevenly Sized Blobs", with points colored by cluster (purple, teal, yellow), each correctly recovered.
>
> **Figure:** Right, three scatter plots (a), (b), (c) of the same 2-D data, with axes from 0 to 1. (a) shows red, green and blue clusters; (b) shows all points in one color (magenta); (c) shows a soft, color-blended assignment of red, green and blue. The result is annotated "Much better".

## GMM Clustering in Action

- Converges more slowly than K-means
- K-means clustering can be used to initialize GMM parameters

> **Figure:** Six scatter plots (a) to (f) of 2-D data on axes from -2 to 2, showing EM on two clusters. (a) Initialization: green points with a blue circle and a red circle as initial Gaussians. (b) Expectation: points colored on a blue-to-red gradient by responsibility, same initial circles. (c) Maximization (parameters), $L=1$: the Gaussians are re-fit as elongated diagonal ellipses. (d) $L=2$, (e) $L=5$, (f) $L=20$: the ellipses tighten around the two clusters, and by $L=20$ points are clearly split into blue and red.

## Other Stuff

1. Hierarchical clustering
2. Many advanced clustering methods!

> **Figure:** A grid comparing clustering methods (columns: MiniBatch KMeans, Affinity Propagation, MeanShift, Spectral Clustering, Ward, Agglomerative Clustering, DBSCAN, OPTICS, BIRCH, Gaussian Mixture) on six toy datasets (rows: concentric circles, two moons, overlapping blobs, anisotropic streaks, well-separated blobs, uniform noise), with run time under each panel. MiniBatch KMeans, DBSCAN, and Gaussian Mixture column headers are circled. In the moons row, the MiniBatch KMeans and Gaussian Mixture panels are marked.
