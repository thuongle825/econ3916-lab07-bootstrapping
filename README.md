# econ3916-lab07-bootstrapping
# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective
I measured how much sample estimates from the UCI Adult Census Income data vary, using both formula-based (CLT) confidence intervals and the bootstrap, and tested when each method gives honest coverage.

## Methodology
- Loaded the UCI Adult Census Income dataset (32,561 respondents).
- Separated the standard deviation of the data from the standard error of an estimate, and checked the s/√n relationship across four sample sizes.
- Built parametric confidence intervals from the Central Limit Theorem and compared how quickly the CLT takes hold for age versus capital gains.
- Ran the bootstrap by hand, then repeated it with `scipy.stats.bootstrap`.
- Bootstrapped the standard error of the median age to see how the method behaves on heavily tied, whole-number data.
- Compared percentile and BCa bootstrap intervals on a heavily skewed variable.
- Bootstrapped a two-sample difference in mean weekly hours worked.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked its output against my own intervals.
- Ran a coverage simulation on lognormal data at n = 50, recording how often nominal 95% parametric and percentile bootstrap intervals captured the true mean and the true median.

## Key Findings
- **Standard deviation is not standard error.** The spread of the data stays put as the sample grows, while the standard error of the mean shrinks in line with s/√n across all four sample sizes.
- **The CLT works at different speeds.** The sampling distribution of mean age looks normal quickly; for capital gains, which is heavily skewed, it converges slowly, so a normal-based interval is less trustworthy there at moderate sample sizes.
- **A bootstrap SE of zero can be correct.** The bootstrap standard error of the median of 32,561 whole-number ages came out to exactly 0.0000. With that many ties, every resample returns the same median, so the median is pinned. The bootstrap was reporting a real property of the data, not failing.
- **Coverage for the mean:** the nominal 95% parametric interval covered [YOUR VALUE]% and the percentile bootstrap covered [YOUR VALUE]%. The gap sits inside the Monte Carlo standard error of about 1.3 points, so the two methods are indistinguishable here, and both under-cover slightly.
- **Coverage for the median:** the mean-centred parametric interval covered only about [YOUR VALUE]%, while the bootstrap stayed near its nominal level. When there is no simple formula for an estimator's standard error, the bootstrap gives a usable interval where borrowing the mean's formula does not.
