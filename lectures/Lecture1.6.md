# Lecture 1.6: Sampling-based Methods

## Monte Carlo methods

> **Figure:** Photograph of an ornate casino hall (Monte Carlo) with chandeliers, a domed stained-glass ceiling, and gaming tables.

**Sampling (Monte Carlo) methods**

- Use **computational simulation** and **random sampling** to make conceptually hard problems easy to solve.
- Originally developed as part of the effort to develop a hydrogen bomb.

> **Figure:** Quote slide: "After spending a lot of time trying to estimate success by combinatorial calculations, I wondered whether a more practical method...might be to lay it out say one hundred times and simply observe and count the number of successful plays" -- S. Ulam. Shown with a photo of early room-sized computing machinery operated by two women, and portraits labeled "Stan Ulam" and "John Von Neumann".

**Problem:** Need to understand neutron transport.

**At the time:** massive groups of people doing calculations ("computers") to investigate the distance that neutrons would travel through various materials.

### Example: calculate the value of $\pi$

$\Rightarrow$ Use computational simulation and random sampling.

> **Figure:** A square centered at the origin $(0,0)$ with an inscribed circle of radius 1. Axes are drawn through the center. A single point $(x_i, y_i)$ is marked inside the circle in the upper right quadrant.

- Area of square: $2 \times 2 = 4$
- Area of circle: $\pi$
- Ratio $= \pi/4$

Procedure:

1. Pick 2 random numbers between $-1$ and $1$ $\Rightarrow$ coordinates of a point inside the square.
2. Is it inside the circle?
3. $P(\text{point in circle}) = \pi/4$

Repeat lots of times!

$$\pi = 4 \cdot \frac{\#\text{ points in circle}}{\#\text{ points}}$$

> **Figure:** A square filled with many random points: red points fall inside the inscribed circle, blue points outside it. Annotations: "Area of square = 4" (pointing to the square) and "Area circle = $\pi$" (pointing to the circle).

> **Figure:** Line plot of the estimate of $\pi$ (y-axis, 2.8 to 3.4) versus number of random samples (x-axis, log scale, $10^1$ to $10^6$). The blue curve fluctuates widely at small sample counts (between about 2.9 and 3.38) and converges to a dotted horizontal line at $\pi \approx 3.14$ as the number of samples grows.

Code shown (MATLAB):

```matlab
tic
iterations = 10000000;

r = rand(iterations, 2);
d = sqrt(r(:,1).^2 + r(:,2).^2);
in = d<=1;
pi_est = 4*sum(in)./iterations
toc

pi_est =
   3.141557200000000
Elapsed time is 0.183833 seconds.
```

### Example: probability of 3-of-a-kind in 5-card poker

What is the probability of getting a hand of 3-of-a-kind in 5-card poker?

> **Figure:** Photo of five playing cards fanned out: K of spades, K of hearts, K of clubs, 5 of spades, 8 of diamonds.

**Solution using probability theory** (slide shown): for three of a kind, the hand looks like $\{x, x, x, y, z\}$ for some distinct values $x, y, z \in \{A, 2, 3, \dots, K\}$. There are $\binom{13}{1}$ ways to choose $x$. There are 12 remaining values available to $y$ and $z$, so there are $\binom{12}{2}$ ways to choose these singletons. For the suits, there are $\binom{4}{3}$ ways to choose the three suits for $x$, and $\binom{4}{1}$ ways for each of $y$ and $z$. There are $\binom{52}{5}$ possible five-card hands. So the probability of three of a kind is:

$$\frac{\binom{13}{1}\binom{12}{2}\binom{4}{3}\binom{4}{1}\binom{4}{1}}{\binom{52}{5}} = \frac{54912}{2598960} = 0.0211$$

**Alternative:** use computational methods to simulate many poker hands.

```matlab
iterations = 1e6;
deck = 1:52;

hits = zeros(iterations, 1);
for i = 1:iterations
    hand = randsample(deck, 5);
    nums = mod(hand, 13);
    N = histc(nums, 0:13);
    if ismember(3, N) && ismember(1, N)
        hits(i)=1;
    end
end

disp(['Probabiliity of three-of-a-kind = ' num2str(sum(hits)/iterations)]);
Probabiliity of three-of-a-kind = 0.021184
```

The simulated value (0.021184) agrees with the analytic value (0.0211).

## In assignment 1

- Calculate sample means ($n=3$)
- Repeat 5000 times
- Plot a histogram

> **Figure:** Histogram (light blue bars) of z-scored height (x-axis, about 60 to 75; y-axis Density, 0 to about 0.35) with an orange normal curve overlaid, centered near 68. The histogram is annotated: "Monte Carlo simulation of distribution of sample means with $n=3$".

- Here, we had access to the population.
- We want to determine the distribution of a sample statistic.
- Used simulation and random sampling to find the distribution of the statistic of interest.

**What happens if the full population is not observable/known?** $\Rightarrow$ Resampling / shuffling

### Example: two-sample t test

Statistic $\propto \bar{X}_2 - \bar{X}_1 = \bar{X}_D$

What is the probability of observing this $\bar{X}_D$ by chance under $H_0$: $X_1$ and $X_2$ are drawn from the same distribution?

> **Figure:** Strip plot along a "Value" axis with two clouds of dots: green dots (group 1, mean $\bar{X}_1$ marked by an arrow from below) and blue dots (group 2, mean $\bar{X}_2$ marked by an arrow from above). Red up/down arrows between the groups indicate points being exchanged between the two groups.

**Shuffle the data between $X_1$ and $X_2$ many times.**

> **Figure:** Stacked strip plots, each a reshuffled version of the data with its own group means and difference, labeled $\bar{X}_{D,1}$, $\bar{X}_{D,2}$, $\bar{X}_{D,3}$, ..., $\bar{X}_{D,N}$ (each with green group-1 and blue group-2 dots, means $\bar{X}_1$ and $\bar{X}_2$ marked).

> **Figure:** A bell-shaped curve labeled "Null distribution" / "shuffled dist" (and "Simulated distrib. of $\bar{X}_D$ under $H_0$"). The observed $\bar{X}_D$ is marked as a point on the left tail, with the area in the tail beyond it shaded and labeled "Probability of observing data [under] $H_0$".

### A more complex example

> **Figure:** Slide from the Cell article "The Striatum Organizes 3D Behavior via Moment-to-Moment Action Selection" (Markowitz et al.). Left: a mouse in an arena under a depth sensor (MoSeq), yielding behavioral syllables (a colored sequence bar, 500 ms scale; example syllables "Reared pause", "Dive", "Locomotion"; outputs listed: syllable number, syllable identity, transition statistics, frame label). Right: plot of z-scored $\Delta F/F_0$ (y-axis, $-20$ to $20$) around an event for dSPN (red), iSPN (green), and a "Time shuffle" control (gray), which is circled by the instructor; the shuffle control stays flat near 0 while dSPN/iSPN traces deviate.

## The bootstrap

*To succeed only by one's own efforts.*

> **Figure:** Photo of a cowboy boot with a spur.

- How can we use sampling and simulation when we have finite data?
  $\Rightarrow$ we know about our sample, but not the population.

**IDEA:** resample data to create virtual populations to make inferences about actual populations.

### Basic bootstrap procedure

- Suppose we have some statistic, $s$, calculated from a random sample of size $N$: $(x_1, x_2, x_3, \dots, x_N)$.

**Step 1:** Re-sample data $\Rightarrow$ draw a random sample of size $N$ from $x$, by sampling **with replacement**.

**Step 2:** Calculate the statistic of interest from each re-sample.

**Step 3:** Repeat many times (10,000, for example).

**Example:** sample data $(x)$: 8, 9, 6, 13, 8, 15, 10

Statistic: $s = f(x) = \dfrac{\mathrm{Var}(x)}{\mathrm{Mean}(x)} = 0.9952$

**Question:** what is the 5-95% confidence interval for $s$?

Perform lots of virtual experiments:

| Resample | Data | Statistic |
|---|---|---|
| 1 | 6, 13, 6, 9, 15, 6, 8 | $s_1 = 1.4815$ |
| 2 | 8, 8, 6, 8, 6, 10, 9 | $s_2 = 0.273$ |
| 3 | 8, 13, 6, 8, 6, 10, 15 | $s_3 = 1.267$ |
| ... | | |

What is the 5-95% CI for $s$?

$\Rightarrow$ 90% of bootstrapped statistics lie in this interval: $[0.2278,\ 1.4256]$

> **Figure:** Histogram of the bootstrapped statistic std(X)/mean(X) (x-axis 0 to 2.5; y-axis Count 0 to 800), roughly unimodal with a peak around 0.8 to 1 and a right tail. Two red vertical lines mark the 5th percentile (0.2278) and the 95th percentile (1.4256).

### Advantages of bootstrapping

- Simplicity! Even when considering complex statistics.
- Applied to nested data.
- Can be used when nothing is known about the underlying distribution of the data.

### Disadvantages

- Accuracy is contingent upon the sample data being **representative** of the population from which the sample is drawn.
  - This is often unknown!

## Multiple comparisons

> **Figure:** xkcd comic "Significant". Panel 1: "Jelly beans cause acne!" "Scientists! Investigate!" Panel 2: "We found no link between jelly beans and acne (P > 0.05)." Panel 3: "That settles that." "I hear it's only a certain color that causes it." "Scientists!"

> **Figure:** The full comic: after the first three panels, a grid of about 20 further panels, one per jelly bean color (salmon, red, turquoise, magenta, yellow, grey, tan, cyan, green, mauve, purple, brown, pink, blue, teal, beige, lilac, black, peach, orange), each reporting "We found no link between [color] jelly beans and acne (P > 0.05)", except the green panel, circled in red: "We found a link between green jelly beans and acne (P < 0.05)." "Whoa!"

> **Figure:** Newspaper front page from the comic: "News: Green jelly beans linked to acne! 95% confidence. Only 5% chance of coincidence!" with a picture of green jelly beans.

> **Figure:** Title block of the paper "Neural correlates of interspecies perspective taking in the post-mortem Atlantic Salmon: An argument for multiple comparisons correction" (Bennett, Baird, Miller, Wolford). Text describes a dead salmon shown photographs of humans in social situations during fMRI. Two brain-scan images (sagittal and axial slices of the salmon) show a small region of apparent activation, circled in red, with a t-value color scale from about 2.5 to 4.5.

> **Figure:** Spurious-correlation chart: "Divorce rate in Maine correlates with Per capita consumption of margarine", correlation 99.26% ($r = 0.992558$), years 2000 to 2009. Two curves (divorce rate per 1,000 and pounds of margarine consumed) both decline together.

> **Figure:** Spurious-correlation chart: "Age of Miss America correlates with Murders by steam, hot vapours and hot objects", correlation 87.01% ($r = 0.870127$), years 1999 to 2009. Two curves rise and fall together.

> **Figure:** Table 4 from a paper listing statistically significant DWT EEG features of AD subjects (Wilcoxon rank-sum test, p-values). Rows are features (MP, Min, Max, Std, Skw, Kurt at several decomposition levels $D_2$ to $D_5$); columns are EEG channels/subject groups (EC1 ... EO8). Most cells are "-" with a scattering of p-values below 0.05. The rows and columns are circled in red, with annotations: "408 comparisons", "43 with $p<0.05$", "$H_0$: would predict 20 comparisons with $p<0.05$".

**Which significant results do you believe?**

(With 408 comparisons at $\alpha = 0.05$, about $0.05 \times 408 \approx 20$ false positives are expected under $H_0$, versus 43 observed.)

### Dealing with multiple comparisons

**Family-wise error rate**

- Probability of making one or more false discoveries when performing multiple hypothesis tests.

**Simplest approach: Bonferroni correction**

$\Rightarrow$ Replace $\alpha$ with $\dfrac{\alpha}{N}$, where $N$ is the number of comparisons.

**Example:** if you perform 10 tests, and desire a false positive rate ($\alpha$) of 5%, then the criterion should be $p < \dfrac{\alpha}{10}$ to reject the null.

**Pro:** corrects for large false positive rates stemming from multiple comparisons.

**Con:** reduces statistical power (increases false negative rate), particularly when the number of comparisons is large.
