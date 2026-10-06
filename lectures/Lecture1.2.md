# Lecture 1.2: Statistics

## Statistics and sample statistics

- **Statistic:** any number computed from sample data.
- Since samples are random, every statistic is also a random variable.
- Every statistic therefore has its own mean, standard deviation, and probability distribution.

**Example: the sample mean**

$$\bar{X} = \frac{1}{N}\sum_{i=1}^{N} X_i$$

A very common statistic!

Questions that come down to testing sample means:

- Are individuals who received a covid vaccine less likely to contract the disease?
- How does manipulation of a gene affect the viability of cells treated with an antibiotic?
- Do patients receiving blood pressure medication display a reduction in blood pressure after six months?

$\Rightarrow$ Testing sample means

## Central Limit Theorem

- Suppose $X$ is a random variable (it could have any distribution).

  $\mu_X$ = mean of $X$, $\sigma_X$ = standard deviation of $X$.

- If we draw $N$ samples, the random variable $\bar{X}$, the mean of $N$ samples, tends towards normality as $N$ increases.

$$X \sim N(\mu_X, \sigma_X^2) \qquad\qquad \bar{X} \sim N\!\left(\mu_X, \frac{\sigma_X^2}{N}\right)$$

- $\sqrt{\sigma_X^2}$: standard deviation of $X$.
- $\sqrt{\sigma_X^2 / N}$: **standard error**.

**Standard error:** width of the distribution of the sample mean.

> **Figure:** Textbook Figure 2.6, three histograms of the mean of $N$ uniformly distributed numbers, for $N=1$, $N=2$, and $N=10$ (x-axis from 0 to 1). For $N=1$ the histogram is flat (annotated "uniform distribution"); for $N=2$ it is a triangular/bell-like shape centered near 0.5; for $N=10$ it is a narrow bell centered near 0.5. Caption: "Histogram plots of the mean of $N$ uniformly distributed numbers for various values of $N$. We observe that as $N$ increases, the distribution tends towards a Gaussian." Handwritten note: mean gets closer to normal distribution as $N$ increases.

> **Figure:** Two panels, (a) and (b), each showing the population distribution (thick green curve) and the distributions of the sample mean for $n=4$ (blue) and $n=16$ (orange). In (a) the population is symmetric and broad; in (b) the population is skewed (long right tail, marked with an arrow). In both panels the sample-mean curves get narrower and taller as $n$ increases.

- Population distribution is skewed.
- $\bar{X}$, when $N=16$, almost follows a normal distribution.

## Small samples and the sample mean

$$\bar{X} \sim N\!\left(\mu_X, \frac{\sigma_X^2}{N}\right)$$

- What happens when we don't already know the population mean and variance?
  - $\Rightarrow$ We don't know the distribution of the sample mean!
- What is our recourse? Estimate population parameters and calculate a new statistic: $t$.

## The t statistic

- Assume $\mu$, estimate $\sigma^2$:

$$s^2 = \frac{1}{N-1}\sum_{i=1}^{N}(x_i - \bar{x})^2$$

$$t = \frac{\bar{x} - \mu}{s/\sqrt{N}}$$

$t$ follows a $t$-distribution:

$$f(t) = \frac{\Gamma\!\left(\frac{\nu+1}{2}\right)}{\sqrt{\nu\pi}\,\Gamma\!\left(\frac{\nu}{2}\right)}\left(1+\frac{t^2}{\nu}\right)^{-\frac{\nu+1}{2}}$$

> **Figure:** Overlaid curves of the standard normal ($z$, black) and $t$-distributions for $n=3, 5, 20, 30$ (legend), x-axis roughly $-3$ to $3$. All are bell-shaped and centered at 0; smaller $n$ gives a lower peak and heavier tails. The tails on both the left and right are circled in red, highlighting that the $t$-distribution has heavier tails than $z$.

## Z-test (a simple statistical test)

- A comparison of one measurement against a population.
- Works when we know (or can estimate accurately) the population mean and variance.

### The Z-score

$$z = \frac{x - \mu_x}{\sigma_x}$$

$\Rightarrow$ A datapoint has a Z-score of 2 if it is $2\sigma$ above the mean.

If $x \sim N(\mu, \sigma^2)$:

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}}\exp\!\left[-\frac{1}{2}\frac{(x-\mu)^2}{\sigma^2}\right]$$

> **Figure:** A bell curve $f(x)$ with dashed vertical lines marking $\mu-2\sigma$, $\mu$ (center), and $\mu+2\sigma$ (and intermediate lines).

> **Figure:** A second bell curve $f(z)$ with x-axis ticks $-2, -1, 0, 1, 2$, labeled $\mu=0$, $\sigma^2=1$, giving $\Rightarrow Z \sim N(0,1)$.

### The Z-score (cont'd)

$$z = \frac{x-\mu}{\sigma}$$

> **Figure:** Number line (ticks $-2,-1,0,1,2$) with a green bell curve centered at $-2$ ($\mu=-2$, $\sigma^2=0.25$) and a blue bell curve centered at 0; arrows show the green curve being shifted to the right. Next to it the numerator $x-\mu$ is boxed: subtracting $\mu$ shifts the distribution to be centered at 0.

> **Figure:** A narrow blue bell curve at 0 and a wider red bell curve at 0, with red arrows showing the wide curve being squeezed inward (and a downward arrow at the peak). Next to it the denominator $\sigma$ is boxed: dividing by $\sigma$ rescales the width.

> **Figure:** Two normal curves on an x-axis from $-4$ to $4$: green with $\mu=-2$, $\sigma^2=0.5$, and red with $\mu=0$, $\sigma^2=1.0$. A point $x=-2.5$ on the green curve is mapped by an arrow to $z=-1$ on the red curve.

$$x \sim N(-2, 0.5), \qquad z = \frac{x+2}{0.5}, \qquad Z \sim N(0,1)$$

$z=-1$: 1 standard deviation below the mean.

> **Figure:** Standard normal curve with x-axis from $-3$ to $3$ marking the 68-95-99.7 rule: 68% of data within $\pm1$, 95% of data within $\pm2$, and 99.7% of data within $\pm3$ standard deviations.

### Using the Z-table

> **Figure:** Left, a standard normal curve with the area to the left of $z$ shaded and labeled "Table entry" and $F(z)$; below it a standard normal table (rows $z$ from $-3.4$ to $-0.0$, columns $.00$ to $.09$). The row $-1.0$ and column $.00$ entry (.1587) is boxed, and the entry for $z=-2.05$ (.0202) is circled, labeled $F(-2.05)$. Right, the cumulative distribution curve $\Phi_{\mu,\sigma^2}(x)$ for $\mu=0$, $\sigma^2=1.0$ (x from $-5$ to $5$, y from 0 to 1.0), labeled $F(z)$, with a vertical line at $x=-1$ dropping from the curve down to the axis and a horizontal line at about 0.16 on the y-axis.

$$x \sim N(-2, 0.5), \quad x_1 = -2.5$$

$$Z \sim N(0,1), \quad z_1 = -1$$

If $z = -1$:

$$F(z_1 = -1) = \int_{-\infty}^{-1} f(z)\,dz = 0.1587$$

## Real-world example

- An adult female measures her heart rate to be 102 bpm at rest. Should she be concerned?

Wikipedia: normal resting heart rate is 60-100 bpm.

More accurately: female HR is $79.3 \pm 14.0$ bpm at rest.

More formally: what is the probability that a healthy woman has a resting heart rate of 102 bpm or higher?

Pictorially:

> **Figure:** Probability density (y-axis) vs. heart rate (x-axis) as a bell curve centered at 79.3, labeled $HR \sim N(79.3, 14.0^2)$. The area in the right tail beyond 102 is shaded red, with the question "what is this area?"

$$z = \frac{102 - 79.3}{14.0} = 1.62$$

> **Figure:** Standard normal curve $f(z)$ with the area to the left of $z=1.62$ shaded (labeled 0.9474) and the right tail shaded red (labeled $1-0.9474$). Alongside, the standard normal table for positive $z$; the entry at row 1.6, column .02 (.9474) is circled.

Area under the curve (the standard normal pdf) to the left of $z=1.62$ is $0.9474$.

$$1 - 0.9474 = 0.0526$$

This is the **p-value** of the statistical test (Z-test).

$\Rightarrow$ There is a 5.26% chance that a healthy adult female has a resting heart rate of 102 bpm or higher.

$\Rightarrow$ This is a Z-test.
