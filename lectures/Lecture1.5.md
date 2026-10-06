# Lecture 1.5: More Statistics

## One- vs. Two-tailed tests

- **Two-tailed:** test whether $\bar{x} \neq \mu_0$ ($\mu_0$ = hypothesized mean under $H_0$)
- **One-tailed:** test whether $\bar{x} > \mu_0$ (right-tailed) or $\bar{x} < \mu_0$ (left-tailed)

> **Figure:** A bell curve centered at $\mu_0$, labeled "Expected distribution of $\bar{x}$ under $H_0$". Small red tail areas $a_2$ (left tail) and $a_1$ (right tail) are shaded, and a blue hatched region $a_3$ covers the right tail.

- Two-tailed test: $a_1 = a_2 = \dfrac{\alpha}{2}$
- One-tailed test: $a_3 = \alpha$

## Two strategies for hypothesis testing

**Fisher:**

1. Establish $H_0$
2. Do **not** establish a significance level ($\alpha$)
3. Report the p-value
4. If the p-value is large, draw no conclusion

$\Rightarrow$ Appropriate for scientific inquiry.

**Neyman-Pearson:**

1. Establish $H_0$/$H_1$, and decide about $\alpha$, $\beta$, sample size, etc.
2. If the data fall into the rejection region for $H_0$ ($p < \alpha$), accept $H_1$, otherwise accept $H_0$.

$\Rightarrow$ Accepting $H_1$ does not mean that it must be true. Just as if we are going to act as if it's true.

## Nonparametric statistics

- **Parametric tests** assume sample data follow a probability distribution that can be modeled accurately with a fixed set of parameters.
  - Examples:
    - Normal distribution (params: $\mu, \sigma^2$)
    - Poisson dist. ($\lambda$)
    - Binomial dist. ($n, p$)
    - Johnson-SU dist. ($\gamma, \delta, \xi, \lambda$)
- **Nonparametric tests** do not require that samples are normally distributed or have any other particular distribution.
  - Also called distribution-free tests.

### Advantages

1. Can be applied to a wide variety of situations.
   - Do not have the requirements of parametric tests
   - Do not require normally distributed populations
   - Insensitive to outliers
2. Can be applied to categorical data.
   - Opinion polls ("Do you approve of ...")
   - Qualitative assessments

> **Figure:** A pain scale of six faces, left to right: No Pain (dark green, smiling), Mild (light green), Moderate (yellow, neutral), Severe (orange), Very Severe (dark orange, frowning), Worst Pain Possible (red, crying).

### Disadvantages

1. Nonparametric methods tend to waste information because exact numerical data are reduced to a qualitative form.
2. As a result, they often have lower power, so they generally need stronger evidence (e.g. more samples) to be able to reject a false null hypothesis.

### Nonparametric analogs of parametric tests

| Setting | Parametric | Non-parametric |
|---|---|---|
| One sample | One-sample t-test | Sign test; Wilcoxon's signed rank test |
| Two sample | Paired t-tests | Sign test; Wilcoxon signed rank |
| Two sample | Two-sample t-test | Mann-Whitney U test; Kolmogorov-Smirnov test |
| K samples | Analysis of Variance (ANOVA); 2-way ANOVA | Kruskal-Wallis test; Friedman test; ... |

## Paired t-test

1. Collect paired data
2. Formulate $H_0$: $\mu_{i,1} = \mu_{i,2}$
3. Calculate the difference between paired values
4. Perform a 1-sample t-test on the difference values

> **Figure:** Top right: a t distribution with $\nu - 1$ d.o.f., with the observed $t$ marked on the right and the tail area shaded and labeled "Area = p-value". Middle: a strip plot of the differences in paired values ($x$-axis "Difference in paired values") with a dashed line at 0, the mean $\bar{x}_D$ and variance $s^2$ indicated, and the points labeled $X_D$. Bottom: paired values plotted on an axis "Values", with group $X_1$ (green points, labeled $i,2$) and group $X_2$ (blue points, labeled $i,1$) joined by gray lines, and one pair's difference marked $X_D$.

## The sign test for paired samples

$H_0$: For a particular animal $f(HL) = f(FL)$

| Deer | Hind leg length (cm) | Foreleg length (cm) | Difference |
|---|---|---|---|
| 1 | 142 | 138 | + |
| 2 | 140 | 136 | + |
| 3 | 144 | 147 | - |
| 4 | 144 | 139 | + |
| 5 | 142 | 143 | - |
| 6 | 146 | 141 | + |
| 7 | 149 | 143 | + |
| 8 | 150 | 145 | + |
| 9 | 142 | 136 | + |
| 10 | 148 | 146 | + |

(The "+" signs are circled in the notes: 8 of the 10 differences are positive.)

> **Figure:** A binomial CDF table for $n = 10$, with rows $c = 0, \ldots, 10$ and columns $p = 0.05, \ldots, 0.95$. The column $p = 0.50$ is boxed in red. The row for 8 is circled in blue, and the entry 0.945 (row 7, $p = 0.50$) is circled in orange with an arrow. Annotation: "CDF for the binomial dist."

- 0.945 probability of observing 7 or fewer +'s.
- $1 - 0.945 = 0.055$ probability of observing 8 or more +'s. This is the **p-value**.

### Disadvantages

- Sign tests treat these data the same way.

> **Figure:** Two strips of "Difference in paired values" with a dashed line at 0. In the left panel, 6 points lie on one side of 0 and 3 on the other side, with the mean $\bar{x}$ marked near 0. In the right panel, the counts are again 6 and 3, but a couple of points are circled in red far from zero and the mean $\bar{x}$ (orange) is shifted to the other side. The point is that the sign test gives the same result for both.

## Mann-Whitney U test (Wilcoxon rank-sum)

- Many non-parametric tests are **rank** tests.
- Testing the null hypothesis that

$$\text{Median}(x_1) = \text{Median}(x_2)$$

**Test statistic:** $U$

$$U = R_1 - \frac{N_1 (N_1 + 1)}{2}$$

What is the distribution of $U$?

$$U \sim N(\mu_U, \sigma_U^2), \quad \text{where } \mu_U = \frac{N_1 N_2}{2}, \quad \sigma_U^2 = \frac{N_1 N_2 (N_1 + N_2 + 1)}{12}$$

### Example

Consider a randomized controlled trial evaluating a new anti-retroviral therapy for HIV. A pilot trial randomly assigned participants to either the treated or untreated groups ($N = 14$). We want to assess the viral load (quantity of virus per milliliter of blood) in the treated versus the untreated groups.

- Sample 1: 4200, 960, 670, 1000, 540, 1200, 4650 ($N_1 = 7$)
- Sample 2: 7500, 6100, 900, 1300, 5000, 7400, 4500 ($N_2 = 7$)

$H_0$: drug does nothing

> **Figure:** All 14 values sorted from largest to smallest in a two-column table (Sample 1, Sample 2), with a rank column split into $S_1$ and $S_2$. Ranks assigned from the top: 7500 (1), 7400 (2), 6100 (3), 5000 (4), 4650 (5), 4500 (6), 4200 (7), 1300 (8), 1200 (9), 1000 (10), 960 (11), 900 (12), 670 (13), 540 (14). The rank sums at the bottom are 69 for $S_1$ and 36 for $S_2$.

Using the sample 2 rank sum:

$$U = R_1 - \frac{N_1(N_1+1)}{2} = 36 - 28 = 8$$

$$U \sim N(\mu_U, \sigma_U^2) \sim N(24.5,\ 7.8)$$

$$\mu_U = \frac{N_1 N_2}{2} = 24.5$$

$$\sigma_U^2 = \frac{N_1 N_2 (N_1 + N_2 + 1)}{12} = (7.8)^2, \qquad \sigma_U = 7.8$$

$$z = \frac{8 - \mu_U}{\sigma_U} = \frac{8 - 24.5}{7.8} = -2.1$$

### The z score

> **Figure:** Left: a standard normal curve with the area to the left of $z = -2.1$ shaded in blue ("Table entry"), next to a standard normal table with the $-2.1$ row circled. Center: zoomed table rows, with $-2.1$ giving .0179 (circled). Rows: $-2.3$: .0107, .0104, .0102; $-2.2$: .0139, .0136, .0132; $-2.1$: .0179, .0174, .0170; $-2.0$: .0228, .0222, .0217; $-1.9$: .0287, .0281, .0274. Right: the normal CDF $\Phi_{\mu,\sigma^2}(x)$ for $\mu = 0$, $\sigma^2 = 1.0$, an S-shaped red curve over $x \in [-5, 5]$ from 0 to 1.0, with a marker near $x = -2.1$.

Probability of observing data (or more extreme data) under the assumption that the drug does nothing is **0.0179**.
