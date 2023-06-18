<!-- ---
layout: default
title: Feature Engineering
parent: Recommendation System
nav_order: 5
--- -->
# Feature Engineering

## Numerical Feature Processing

### Missing value

If a certain real number feature $x_i$ of a sample $\mathbf{x}$ is missing, we can use the following methods to fill in the missing value:

1. **Mean value**: replace the missing value with the mean value of the feature $x_i$ of all samples.
2. **Median value**: replace the missing value with the median value of the feature $x_i$ of all samples.

These two methods are simple but too rough. If the missing value is caused by the abnormality of the sample itself, the above two methods will cause the feature to deviate from the true distribution. Therefore, we can train a simple model to predict the missing value of the feature $x_i$ based on other features of the sample. 

On the other side, if the real number feature $x_i$ will be discretized (bucketized) later, we can treat the missing value as a special category that is for the missing value.

### Normalization

Normalization is to map the original value of the feature to a new value in a certain range. The purpose of normalization is to make the feature value have the same order of magnitude, so that the feature value is not too large or too small, and the model can converge faster. 

One of the most common normalization methods is z-score normalization, which maps the feature value to a standard normal distribution with a mean of 0 and a variance of 1. The formula is as follows:

$$
x' = \frac{x - \mu}{\sigma}
$$

where $\mu$ is the mean of the feature value, and $\sigma$ is the standard deviation of the feature value.
