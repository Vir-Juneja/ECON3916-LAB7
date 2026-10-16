# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective

I explored how to measure uncertainty in statistical estimates using the Central Limit Theorem (CLT), confidence intervals, and bootstrapping, and compared how these methods perform with different sample sizes and data distributions.

## Methodology

- **Data Exploration:** I loaded the UCI Adult Census Income dataset containing 32,561 respondents and examined variables including age, capital gains, and weekly hours worked.
- **Standard Deviation vs. Standard Error:** I compared the standard deviation of the data with the standard error of an estimate. I tested the relationship SE = s/√n across four sample sizes to see how sample size affects uncertainty.
- **Central Limit Theorem:** I constructed parametric confidence intervals using the CLT and examined how quickly the sampling distributions of age and capital gains approached normality.
- **Manual Bootstrapping:** I implemented bootstrap resampling manually by repeatedly sampling observations with replacement and calculating statistics from each sample.
- **SciPy Bootstrapping:** I used `scipy.stats.bootstrap` to calculate confidence intervals and compared the results with my manual implementation.
- **Degenerate Bootstrap Case:** I investigated why bootstrapping the median of 32,561 whole-number ages produced a standard error of exactly 0.0000.
- **Confidence Interval Methods:** I compared percentile and bias-corrected and accelerated (BCa) bootstrap intervals for a heavily skewed variable.
- **Two-Sample Bootstrapping:** I estimated uncertainty in the difference between mean weekly hours worked across two groups.
- **AI-Assisted Coding:** I asked an AI tool to write a bootstrap confidence interval function, revised my prompt once, and checked the generated function against my own results.
- **Coverage Simulation:** I simulated lognormal data with a sample size of n = 50 to compare how often parametric and bootstrap confidence intervals captured the true population mean and median.

## Key Findings

- **Standard Error and Sample Size:** I confirmed that standard error decreases approximately with 1/√n. Larger samples produced more precise estimates, even though the underlying variability in the data did not necessarily change.

- **Central Limit Theorem:** I found that the CLT worked quickly for age but converged more slowly for capital gains because of the highly skewed distribution. This showed me that the shape of the data affects how well normal approximations work.

- **Bootstrap vs. Parametric Methods:** I learned that bootstrapping estimates uncertainty directly from resampled data without requiring a formula for the standard error. I also compared percentile and BCa intervals to see how different methods handle skewed distributions.

- **Zero Bootstrap Standard Error:** The bootstrap standard error of the median age was exactly **0.0000**. Because the dataset contained 32,561 whole-number ages with many repeated values, every bootstrap resample returned the same median. I learned that this was a real property of the data rather than a failure of the bootstrap method.

- **Two-Sample Comparison:** I used bootstrapping to estimate uncertainty in the difference between mean weekly hours worked across groups, showing how resampling can be applied to comparisons between populations.

- **AI-Generated Function:** After revising my prompt once, I checked the AI-generated bootstrap function against my own confidence intervals. This helped me understand the importance of verifying AI-generated statistical code rather than assuming it is correct.

### Coverage Simulation Results

I tested how accurately different confidence interval methods estimated the population mean and median using lognormal data with n = 50.

| Statistic | Method | Nominal Coverage | Observed Coverage |
|---|---|---|---|
| Mean | Parametric CLT | 95% | 92.5% |
| Mean | Percentile Bootstrap | 95% | 91.5% |
| Median | Mean-centred Parametric | 95% | ~66.8% |
| Median | Bootstrap | 95% | Near 95% |

**For the mean:** The parametric interval covered the true value 92.5% of the time, while the percentile bootstrap covered it 91.5% of the time. The difference was within the Monte Carlo standard error of approximately 1.3 percentage points, so I could not conclude that one method performed better. Both methods slightly under-covered relative to the nominal 95% level.

**For the median:** The mean-centred parametric interval covered the true median only about 66.8% of the time, while the bootstrap interval stayed near the expected 95% coverage. This showed how using a confidence interval designed for the mean can produce misleading results when estimating a different statistic.

## Conclusion

The main lesson I learned from this lab is that **the best way to estimate uncertainty depends on the statistic being measured and the distribution of the data**.

I found that the CLT works well in some situations but can be less accurate with highly skewed data. Bootstrapping provides another way to estimate uncertainty by resampling observations instead of relying on a theoretical formula.

The coverage simulation showed me that bootstrapping is not automatically better than parametric methods. Both approaches slightly under-covered the mean, while the bootstrap performed much better for the median than an incorrectly applied mean-centred interval.

Overall, I learned why it is important to check assumptions, understand what a confidence interval is estimating, and test whether a statistical method actually achieves its intended coverage.
