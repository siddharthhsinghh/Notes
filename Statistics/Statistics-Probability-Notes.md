# Statistics & Probability Notes

Beginner-friendly notes for Data Analytics, Data Science, and Machine Learning. Includes definitions, formulas, Python examples, interview questions, and practice.

## 1. What is Statistics?

**Statistics** is the branch of mathematics concerned with collecting, organizing, analyzing, interpreting, and presenting data.

Two main branches:
- **Descriptive statistics:** Summarizes the data you have.
- **Inferential statistics:** Uses sample data to draw conclusions about a larger population while accounting for uncertainty.

## 2. Population and sample

- **Population:** Complete group being studied.
- **Sample:** Subset selected from the population.
- **Parameter:** Numerical characteristic of a population, such as population mean μ.
- **Statistic:** Numerical characteristic calculated from a sample, such as sample mean x̄.

Example: All students in a university form a population; 200 selected students form a sample.

A biased sample can produce misleading conclusions.

## 3. Types of data

**Qualitative (categorical):**
- Nominal: categories without a natural order, e.g. city.
- Ordinal: ordered categories, e.g. low, medium, high.

**Quantitative (numerical):**
- Discrete: countable values, e.g. number of orders.
- Continuous: measurements over an interval, e.g. height or time.

## 4. Measures of central tendency

### Mean
Arithmetic average:

\[
\bar{x} = \frac{\sum_{i=1}^{n}x_i}{n}
\]

Example: mean of 10, 20, 30 is 20.

```python
import numpy as np
data = [10, 20, 30]
np.mean(data)
```

The mean is sensitive to extreme values.

### Median
Middle value after sorting. For an even number of observations, average the two middle values.

```python
np.median([10, 20, 30, 40])
```

The median is more resistant to extreme values than the mean.

### Mode
Most frequently occurring value.

```python
from statistics import mode
mode([10, 20, 20, 30])
```

A dataset may have one mode, multiple modes, or no useful unique mode.

### When to use each?
- Mean: numerical data without severe skew or influential outliers.
- Median: skewed data or data with extreme values.
- Mode: most frequent value; also useful for categorical data.

## 5. Measures of dispersion

Dispersion describes how spread out data is.

### Range

\[
\text{Range}=\text{Maximum}-\text{Minimum}
\]

```python
max(data) - min(data)
```

### Variance

Population variance:

\[
\sigma^2=\frac{\sum_{i=1}^{N}(x_i-\mu)^2}{N}
\]

Sample variance:

\[
s^2=\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}
\]

```python
np.var(data)          # Population variance by default
np.var(data, ddof=1)  # Sample variance
```

### Standard deviation

Square root of variance; measures spread in the original units.

\[
\sigma=\sqrt{\sigma^2}
\]

```python
np.std(data)          # Population standard deviation
np.std(data, ddof=1)  # Sample standard deviation
```

### Interquartile range (IQR)

\[
IQR=Q_3-Q_1
\]

Measures the spread of the middle 50% and is less affected by extreme values than the range.

```python
q1 = np.percentile(data, 25)
q3 = np.percentile(data, 75)
iqr = q3 - q1
```

## 6. Percentiles and quartiles

- **Percentile:** Value at or below which a given percentage of observations falls, according to the chosen percentile convention.
- Q1: 25th percentile.
- Q2: 50th percentile (median).
- Q3: 75th percentile.

```python
np.percentile(data, [25, 50, 75])
```

Different software can use slightly different quantile interpolation conventions, especially for small datasets.

## 7. Shape of a distribution

- **Symmetric:** Left and right sides are approximately mirror images.
- **Right-skewed (positive):** Longer tail on the right; large values can pull mean above median.
- **Left-skewed (negative):** Longer tail on the left; small values can pull mean below median.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(data, kde=True)
plt.show()
```

## 8. Probability basics

**Probability** measures how likely an event is, from 0 to 1.

- 0: impossible.
- 1: certain.
- 0.5: 50% chance.

For equally likely outcomes:

\[
P(A)=\frac{\text{Favourable outcomes}}{\text{Total outcomes}}
\]

Example: probability of an even number on a fair six-sided die is 3/6 = 1/2.

Terms:
- Experiment: process producing an outcome.
- Outcome: one possible result.
- Sample space: set of all possible outcomes.
- Event: a set of outcomes.

## 9. Probability rules

Complement:

\[
P(A^c)=1-P(A)
\]

Addition:

\[
P(A\cup B)=P(A)+P(B)-P(A\cap B)
\]

For mutually exclusive events:

\[
P(A\cup B)=P(A)+P(B)
\]

Multiplication:

\[
P(A\cap B)=P(A)P(B\mid A)
\]

For independent events:

\[
P(A\cap B)=P(A)P(B)
\]

Do not confuse mutually exclusive with independent. Two mutually exclusive events with positive probabilities are not independent.

## 10. Conditional probability

Probability of A occurring given that B has occurred:

\[
P(A\mid B)=\frac{P(A\cap B)}{P(B)},\quad P(B)>0
\]

Example: Given that a randomly drawn card is a heart, the probability it is a king is 1/13.

## 11. Bayes' theorem

Updates the probability of a hypothesis after observing evidence:

\[
P(A\mid B)=\frac{P(B\mid A)P(A)}{P(B)}
\]

- P(A): prior probability.
- P(B|A): likelihood.
- P(B): evidence probability.
- P(A|B): posterior probability.

Applications include medical testing, spam filtering, and probabilistic machine learning.

## 12. Random variables and expected value

A **random variable** assigns a numerical value to each outcome.

- Discrete: countable possible values.
- Continuous: values over a continuous interval.

For a discrete random variable:

\[
E[X]=\sum_x xP(X=x)
\]

Variance:

\[
Var(X)=E[(X-E[X])^2]=E[X^2]-(E[X])^2
\]

Expected value is the long-run average across repeated trials under the model.

## 13. Common probability distributions

### Bernoulli
One trial with two outcomes, often success and failure:

\[
P(X=x)=p^x(1-p)^{1-x},\quad x\in\{0,1\}
\]

Example: one coin toss coded as heads = 1, tails = 0.

### Binomial
Counts successes in a fixed number of independent Bernoulli trials with the same success probability:

\[
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}
\]

Example: number of heads in 10 independent fair coin tosses.

### Poisson
Models event counts in a fixed interval under assumptions such as a constant average rate and independent occurrences:

\[
P(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}
\]

λ is the expected count in the interval.

### Uniform
All values in a specified range have equal density for a continuous uniform distribution.

### Normal
A symmetric, bell-shaped continuous distribution described by mean μ and standard deviation σ:

\[
f(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
\]

Empirical rule for normal data:
- About 68% within 1 standard deviation.
- About 95% within 2.
- About 99.7% within 3.

These percentages are approximate and apply to normally distributed data.

## 14. Z-score

A z-score tells how many standard deviations a value is from the mean:

\[
z=\frac{x-\mu}{\sigma}
\]

```python
from scipy.stats import zscore
values = [10, 12, 14, 16, 18]
zscore(values)
```

A z-score of 2 means two standard deviations above the mean under the selected standardization.

## 15. Sampling methods

**Sampling** selects a subset of a population.

- Simple random: each member has an equal chance.
- Systematic: select every kth member after a random start.
- Stratified: divide into strata and sample from each.
- Cluster: divide into clusters and select clusters.
- Convenience: select readily available participants; can create substantial bias.

A representative sample and suitable sample size both matter.

## 16. Sampling distribution and Central Limit Theorem

A **sampling distribution** is the probability distribution of a statistic across repeated samples of the same size.

**Central Limit Theorem (CLT):** Under suitable conditions, the sampling distribution of the sample mean becomes approximately normal as sample size increases, even if the population distribution is not normal.

For independent observations with finite mean and variance:

\[
E[\bar{X}]=\mu,\qquad SE(\bar{X})=\frac{\sigma}{\sqrt{n}}
\]

Standard error describes variability of a statistic across samples. It is not the standard deviation of individual observations.

## 17. Confidence intervals

A **confidence interval** is a range calculated using a method with a stated long-run coverage rate.

For a large-sample mean interval when population standard deviation is known:

\[
\bar{x}\pm1.96\frac{\sigma}{\sqrt{n}}
\]

When population standard deviation is unknown, a t-based interval is commonly used:

\[
\bar{x}\pm t^*\frac{s}{\sqrt{n}}
\]

A 95% confidence procedure produces intervals containing the true parameter in about 95% of repeated samples under its assumptions. It does not mean a fixed computed interval has a 95% probability of containing the fixed parameter.

## 18. Hypothesis testing basics

Hypothesis testing uses sample data to assess a claim about a population.

- **Null hypothesis (H0):** baseline claim, often no effect or no difference.
- **Alternative hypothesis (H1/Ha):** competing claim.
- **Significance level (α):** preselected threshold, often 0.05.
- **Test statistic:** value calculated from sample data.
- **p-value:** probability, assuming H0 and the test assumptions, of observing a result at least as extreme as the one obtained.

A p-value is not the probability that H0 is true.

Steps:
1. State H0 and H1.
2. Choose α.
3. Select an appropriate test and check assumptions.
4. Calculate test statistic and p-value.
5. Compare p-value with α.
6. Report the conclusion in context.

If p-value < α, reject H0. Otherwise, fail to reject H0. Failing to reject does not prove H0 true.

## 19. Type I and Type II errors

- **Type I error:** Rejecting a true null hypothesis. Its long-run probability is controlled by α under test assumptions.
- **Type II error:** Failing to reject a false null hypothesis.
- **Power:** Probability of correctly rejecting a false null hypothesis; for a specified alternative, power = 1 − β.

Increasing sample size can improve power when other conditions are held appropriately.

## 20. Covariance and correlation

**Covariance** measures how two variables vary together; its magnitude depends on their units.

**Correlation** is a standardized measure of linear association, usually between −1 and +1:
- +1: perfect positive linear association.
- 0: no linear association.
- −1: perfect negative linear association.

```python
import pandas as pd

df = pd.DataFrame({
    "hours": [1, 2, 3, 4, 5],
    "marks": [40, 45, 55, 65, 75]
})
df["hours"].corr(df["marks"])
```

A correlation near zero does not rule out a non-linear relationship. Correlation does not establish causation.

## 21. Python libraries

```python
import numpy as np
import pandas as pd
from scipy import stats

np.mean(data)
np.median(data)
np.var(data)
np.std(data)
np.percentile(data, 25)

pd.Series(data).describe()
pd.Series(data).value_counts()

stats.mode(data, keepdims=False)
stats.skew(data)
stats.kurtosis(data)
stats.zscore(data)
stats.norm.cdf(0)
```

SciPy function arguments and return types can vary by version; consult documentation for the installed version.

## 22. Interview questions

**Descriptive vs inferential statistics?** Descriptive statistics summarize observed data; inferential statistics use sample data to draw conclusions about a population.

**Population vs sample?** Population is the complete group; sample is a subset.

**Mean vs median?** Mean is the arithmetic average and is sensitive to extremes; median is the middle value and is more resistant.

**Variance vs standard deviation?** Variance is average squared deviation; standard deviation is its square root.

**What is conditional probability?** Probability of an event given that another event has occurred.

**What is Bayes' theorem?** A formula for updating a hypothesis probability using evidence.

**What is CLT?** Under suitable conditions, the sampling distribution of the sample mean becomes approximately normal as sample size increases.

**What is a p-value?** Probability, assuming H0 and test assumptions, of a result at least as extreme as the observed result.

**What is a confidence interval?** An interval produced by a method designed to capture a population parameter at a stated long-run rate.

**Correlation vs causation?** Correlation is association; causation means a change in one variable produces a change in another. Correlation alone cannot establish causation.

**Type I vs Type II error?** Type I rejects a true H0; Type II fails to reject a false H0.

## 23. Practice questions

Conceptual:
1. Explain population, sample, parameter, and statistic.
2. When is median preferable to mean?
3. Explain discrete and continuous data.
4. What does standard deviation of zero mean?
5. Explain independent and mutually exclusive events.
6. State Bayes' theorem and one application.
7. Explain the CLT in your own words.
8. What does a 95% confidence interval mean?
9. Explain p-value, significance level, and power.
10. Why does correlation not prove causation?

Numerical:
1. Find mean, median, and mode of [2, 3, 3, 5, 7].
2. Find range and IQR for a sorted dataset.
3. A fair die is rolled. Find the probability of a number greater than 4.
4. Two fair coins are tossed. Find the probability of exactly one head.
5. A fair coin is tossed 5 times. Identify binomial parameters for number of heads.
6. If mean = 50 and standard deviation = 10, calculate z-score for 70.
7. If population standard deviation = 12 and sample size = 36, calculate standard error of the sample mean.

## 24. Quick formula reference

| Concept | Formula |
|---|---|
| Mean | x̄ = Σxᵢ / n |
| Range | Maximum − Minimum |
| Population variance | σ² = Σ(xᵢ − μ)² / N |
| Sample variance | s² = Σ(xᵢ − x̄)² / (n − 1) |
| Standard deviation | Square root of variance |
| IQR | Q3 − Q1 |
| Complement | P(Aᶜ) = 1 − P(A) |
| Addition | P(A∪B) = P(A)+P(B)−P(A∩B) |
| Conditional | P(A\|B) = P(A∩B)/P(B) |
| Independent | P(A∩B) = P(A)P(B) |
| Bayes | P(A\|B) = P(B\|A)P(A)/P(B) |
| Z-score | z = (x − μ)/σ |
| Standard error of mean | SE = σ/√n |
| IQR fences | Q1 − 1.5 IQR, Q3 + 1.5 IQR |

---
**Learning tip:** Learn the meaning and assumptions behind each formula. Choosing the right method matters more than memorizing formulas.
