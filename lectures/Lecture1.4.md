# Lecture 1.4: T-tests

## Review: Central limit theorem

$$\bar{X} \sim N\left(\mu_X, \frac{\sigma_X^2}{N}\right) \quad \text{when } N \text{ is large}$$

- $\bar{X}$ is the sample mean.
- $\mu_X$ is the mean of $X$.
- $\sigma_X^2$ is the variance of $X$.
- $\mu_X$ and $\sigma_X^2$ are population parameters, not sample statistics.

The sample mean is a statistic with its own sampling distribution. When $N$ is large, that distribution is a Normal distribution with the same mean as the distribution of $X$ and variance equal to the original variance divided by $N$.

## Distribution of the sample mean

The distribution of the sample mean "tends" to Normality as $N$ increases.

> **Figure:** Textbook Figure 2.6, three histograms of the mean of $N$ uniformly distributed numbers (x-axis from 0 to 1, with 0.5 marked). For $N=1$ the histogram is flat (annotated "Uniform distribution"). For $N=2$ it is triangular/bell-shaped. For $N=10$ it is a narrow bell curve centered at 0.5. Annotation: "mean gets closer to Normal dist." Caption: "Histogram plots of the mean of $N$ uniformly distributed numbers for various values of $N$. We observe that as $N$ increases, the distribution tends towards a Gaussian."

For the uniform example:

$$\mu_X = \tfrac{1}{2}(\max + \min) = 0.5$$

$$\sigma_X^2 = \tfrac{1}{12}(\max - \min)^2 = \tfrac{1}{12}$$

If $N = 10$, $\bar{X} \sim N\left(0.5, \frac{1/12}{10}\right)$ (annotated $\frac{1}{120}$).

$\Rightarrow$ We can easily predict the distribution of $\bar{X}$.

## What if we don't know the population parameters?

**Q:** What happens if we don't know the population parameters?

**A:** Calculate the statistic, $t$.

$$t = \frac{\bar{x} - \mu}{s/\sqrt{N}}, \qquad s = \sqrt{\frac{1}{N-1}\sum_{i=1}^{N}(x_i - \bar{x})^2}$$

- $\mu$ is the hypothesized mean under $H_0$.
- $s$ is the sample standard deviation.

### t-distribution

$$f(t) = \frac{\Gamma\left(\frac{\nu+1}{2}\right)}{\sqrt{\nu\pi}\,\Gamma(\nu/2)}\left(1 + \frac{t^2}{\nu}\right)^{-\frac{\nu+1}{2}}$$

- The $t$ distribution has only a single parameter, $\nu$, the degrees of freedom.

$$t = \frac{\sqrt{N}\,(\bar{x} - \mu)}{\sqrt{\sum (x_i - \bar{x})^2 / (N-1)}}$$

Because we estimated $\bar{x}$, the $x_i$ have $N-1$ degrees of freedom.

## Example: degrees of freedom

A class has three students. Their test scores are:

- $x_1 = 86$
- $x_2 = 74$
- $x_3 = 92$

This is a unique point in 3D space.

> **Figure:** 3D plot with axes Student 1, Student 2, Student 3 (each roughly 60 to 100). A single red point marks the data point (86, 74, 92), with lines dropping to the axes.

Suppose the instructor tells you $\bar{x} = 84$. Now the data has $N - 1 = 3 - 1 = 2$ degrees of freedom.

> **Figure:** Same 3D axes, now with a colored (blue-green) tilted plane outlined in red, containing the red data point. The plane represents all score triples consistent with the mean of 84.

If $x_1 = 86$, $x_2 = 74$:

$$\bar{x} = (86 + 74 + x_3)\tfrac{1}{3} = 84$$

then $x_3 = 92$. This is now constrained.

## t statistic

$$\sigma^2 = \frac{1}{N}\sum (x_i - \mu)^2$$

$$s^2 = \frac{1}{N-1}\sum (x_i - \bar{x})^2$$

- The squared deviation of the data from the sample mean will always be less than (or equal to) the squared deviation from the population mean.
- $\frac{1}{N}\sum (x_i - \bar{x})^2$ is then less than $\sigma^2$.
- $\frac{1}{N-1}\sum (x_i - \bar{x})^2$ is an unbiased estimate of $\sigma^2$.

## The t distribution

- $t$ follows a $t$ distribution.
- The $t$ distribution converges to the standard normal distribution as dof (number of data points) increases.

**Rule of thumb:** $\bar{X}$ follows a normal distribution when $N \ge 30$.

> **Figure:** Images of William Sealy Gosset: the first page of "The Probable Error of a Mean" by "Student" (Biometrika, Vol. VI, March 1908, No. 1; "By Student" underlined in red), a plaque reading "William Sealy Gosset 1876-1937 Chief Brewer" ("Student's t-test"), and a black-and-white portrait photograph of Gosset.

## The one-sample t-test

1. Collect data.
2. Formulate a null hypothesis ($H_0$): $\mu = \mu_0$.
3. Estimate parameters.
4. Compute test statistic.
5. Determine distribution of test statistic under $H_0$.
6. Compute probability of observing outcome under $H_0$.

$$t = \frac{\bar{x} - \mu_0}{s/\sqrt{N}}, \qquad s = \sqrt{\frac{1}{N-1}\sum (x_i - \bar{x})^2}$$

> **Figure:** Left: green dots scattered along a horizontal "Value" axis, with $\bar{x}$ marked by an arrow at the center of the cloud, a double arrow labeled $s$ showing the spread, and a dotted red vertical line at $\mu_0$ to the right. Right: a green bell-shaped $t$ distribution, labeled "$t$ distribution, $\nu = N-1$", with the observed $t$ marked as a blue dot in the left tail and the tail area shaded red, labeled "Area = p-value".

## Variation: two-sample t-test (equal variances)

1. Collect data.
2. Formulate $H_0$ ($\mu_1 = \mu_2$).
3. Estimate population parameters.
4. Calculate test statistic.
5. Determine distribution of test statistic under $H_0$.
6. Compute probability of observing outcome under $H_0$.

$$t = \frac{\bar{x}_1 - \bar{x}_2}{s_p\sqrt{\frac{1}{N_1} + \frac{1}{N_2}}}$$

$$s_p = \sqrt{\frac{(N_1 - 1)s_{x_1}^2 + (N_2 - 1)s_{x_2}^2}{N_1 + N_2 - 2}}$$

> **Figure:** Left: two clouds of dots along a "Value" axis, green (group 1) lower with mean $\bar{x}_1$ and spread $s_{x_1}$ marked, and blue (group 2) higher with mean $\bar{x}_2$ and spread $s_{x_2}$ marked. Right: a red $t$-distribution curve labeled "$t$-distribution with $N_1 + N_2 - 2$ d.o.f.", with a blue dot in the left tail and the tail shaded, labeled "Area = p-value".

### Unequal variances

$$t = \frac{\bar{x}_1 - \bar{x}_2}{s}, \qquad s = \sqrt{\frac{s_1^2}{N_1} + \frac{s_2^2}{N_2}}$$

## Paired t-test (repeated measures)

1. Collect paired data.
2. Formulate $H_0$: $\mu_{i,1} = \mu_{i,2}$.
3. Calculate difference in paired values: $x_{i,D} = x_{i,1} - x_{i,2}$.
4. Perform 1-sample t-test on difference values ($x_D$).

> **Figure:** Left: two rows of dots along a "Values" axis, $X_2$ (blue, upper) and $X_1$ (green, lower), with gray lines connecting each pair; one pair's horizontal separation is marked $x_{i,D}$. Right: gray dots along a "Difference in paired values" axis showing $X_D$, with a dashed vertical line at 0 and a blue brace under the dots.

## A common misconception

$\Rightarrow$ It is incorrect to use a t-test when data are not normally distributed.

What assumptions do t-tests make?

1. $\frac{s^2(N-1)}{\sigma^2}$ follows a $\chi^2$ distribution with $N-1$ d.o.f.
2. Sample mean and variance are independent.

> **Figure:** Three panels of person icons. "One sample t-test": a globe linked to a group of people, "Is there a difference between a group and the population". "Independent samples t-test": two groups of people linked, "Is there a difference between two groups". "Paired samples t-test": a clock above two columns of people with each person linked to their counterpart, "Is there a difference in a group between two points in time".
