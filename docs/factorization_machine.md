---
layout: default
title: Factorization Machine
parent: Recommendation System
nav_order: 1
---
# Factorization Machine

## Backgorund
Polynomial model is the most intuitive model that includes feature combinations. The combination of features $x_i$ and $x_j$ is represented by $x_ix_j$, and the combination feature is only meaningful when both are nonzero. From a comparative perspective, this article only discusses the second-order polynomial model. The expression of the model obtained by adding second-order feature combinations to the traditional linear model is as follows:

$$
y({\rm \bf x}) = w_0 + \sum_{i = 1}^nw_ix_i + \sum_{i = 1}^n\sum_{j=i+1}^nw_{ij}x_ix_j
$$

