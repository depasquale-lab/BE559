# Lecture 1.3: Hypothesis Testing, P-Values, and Bayesian Inference

## Review: statistics and z-scores

- **What is a statistic?**
  - A number computed from a sample that is itself a random variable (R.V.) with its own sampling distribution.
  - Example: the sample mean.
- **Z-scoring data**

$$z = \frac{x - \mu}{\sigma}$$

  - Normalizing data so that it is easily interpretable and comparable.
  - Example: the temperature in Taipei
    - High of 90°F on May 31st ($z = 1.2$)
    - High of 70°F on Nov 31st ($z = -0.3$)

## Today: hypothesis testing

- A statistical procedure in which a choice is made between **null** and **alternative** hypotheses based on information in a sample.
- **Null hypothesis ($H_0$):** A statement about a population parameter that is assumed to be true unless there is convincing evidence to the contrary.
- **Alternative hypothesis ($H_1$ or $H_a$):** A statement about a population parameter that is contradictory to $H_0$ and accepted if evidence suggests that $H_0$ is unlikely.

## P-value

**P-value:** the probability value. The probability of observing an outcome at least as different than expected under $H_0$ as observed.

### Example from last time

A heart rate of 102 bpm was observed.

- Null hypothesis: the individual is healthy.
- Alternative: the high heart rate is the result of illness or disease.

> **Figure:** A bell curve labeled "Heart rate distribution under $H_0$". The right tail beyond the observed value is shaded red and labeled "Area = 0.0526", with the label "P-value".

There is a 5.26% chance that a healthy individual has HR $\geq 102$.

### Common misconception

~~P-value: probability that $H_0$ is true; $1 - P$: probability that $H_1$ is true.~~ **NO!**

> **Figure:** The two misconception lines are crossed out with a large red X and "NO!" written beneath.

## An illustrative example

- Suppose a particular test for whether someone has been using an illicit drug is 90% sensitive, meaning the true positive rate (TPR) = 0.90. Therefore, it leads to 90% true positive results (correct identification of drug use) for users.
- The test is 95% specific, meaning true negative rate (TNR) = 0.95. Therefore, the test correctly identifies 95% of non-use for non-users, but also generates 5% false positives, or false positive rate (FPR) = 0.05, for non-users.
- Assuming 0.005 prevalence, meaning 0.5% of people use the drug, what is the probability that a random person who tests positive is really a drug user?

$H_0$: The person is not a drug user.

Sample data: The person's drug test is positive.

**Wrong answer:**

$$\text{P-value} = P(\text{data} \mid H_0) = P(\text{positive} \mid \text{non-user}) = 0.05$$

$\Rightarrow$ 95% probability the person is a user (this is wrong).

## Bayesian inference

Bayes' theorem:

$$P(H \mid E) = \frac{P(E \mid H)\, P(H)}{P(E)}$$

- $H$: Hypothesis
- $E$: Event
- $P(H \mid E)$ = probability of $H$ being true given an observation of event $E$.

### Applying it to the drug test

- $H$: the person is a user
- $E$: the person's test is positive

From the problem statement:

- $P(E \mid H) = 0.9$
- $P(E \mid \sim H) = 0.05$
- $P(H) = 0.005$

$P(H \mid E)$ = probability that the person is a user given that their test is positive.

$$P(E) = P(E \mid H)P(H) + P(E \mid \sim H)P(\sim H) = (0.9)(0.005) + (0.05)(0.995) = 0.054$$

$$P(H \mid E) = \frac{P(E \mid H)P(H)}{P(E)} = \frac{(0.9)(0.005)}{0.054} = 0.083$$

$\Rightarrow$ Only an 8.3% chance the person is a user!

- Before test: 0.5% chance (prior probability)
- After test: 8.3% chance (posterior probability)
- Dramatically increased!

### Terms in Bayes' theorem

$$P(H \mid E) = \frac{P(E \mid H)\, P(H)}{P(E)}$$

- $P(H \mid E)$: posterior probability
- $P(E \mid H)$: likelihood
- $P(H)$: prior probability
- $P(E)$: evidence

> **Figure:** Three bell curves along a common axis. A red curve on the left is labeled "Prior belief", a blue curve overlapping it and shifted slightly right is labeled "Posterior belief", and a black curve far to the right is labeled "Evidence".

### Your Bayesian brain

- You are walking down Beacon Street.
- You see a shape out of the corner of your eye.
- It looked like a hippo! But it could also have been a shadow from a tree.
- What does your brain conclude?

> **Figure:** A horizontal axis labeled "P(seeing an exotic animal on Beacon St.)", with arrows at both ends. A narrow red curve near the left is labeled "Prior belief". A blue curve far to the right is labeled "Evidence (looked like a hippo)". A green curve, only slightly shifted from the prior toward the evidence, is labeled "updated belief (posterior)".

## P-value revisited

Misconception: probability that $H_0$ is false.

More accurately: the probability of a result as extreme or more extreme when $H_0$ is true.

$$P(\text{data} \mid H_0)$$

**Not** the probability that $H_0$ is true.

### $\alpha$: significance level

How unlikely observations have to be under $H_0$ for us to reject $H_0$.

- $P < 0.05$ or $P < 0.01$ are common.
- For example: if there is a $\leq 5\%$ chance of observing data (or more extreme data) under $H_0$, then we reject $H_0$.

$\Rightarrow$ Do **not** confuse statistical significance with **practical** significance.

A small effect can be highly significant statistically (very small p-value) if the sample size is large enough.

## Statistical power ($1 - \beta$)

**Power:** the probability of correctly rejecting a false null hypothesis.

**Example**

$H_0$: Global warming is a hoax perpetuated by self-aggrandizing scientists and George Soros.

Experiment: Measure the temperature outside right now! It's cold!

The statistical test results in $p = 0.95$.

- $\Rightarrow$ The data are very likely under $H_0$!
- $\Rightarrow$ We have failed to reject our null hypothesis.

Is our null hypothesis correct? Probably not!

Why? That was a very poorly designed experiment!
