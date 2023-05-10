---
layout: default
title: Lecture 8 Computing Solutions for General Finite Strategic Games, Part I
parent: Game Theory
nav_order: 7
---
## Lecture 8 Computing Solutions for General Finite Strategic Games, Part I: Dominance and iterated strategy elimination

### Obviously good strategies: dominant strategies

**Definition**: A mixed strategy $x_i \in X_i$ is **dominant** if for all $x_i' \in X_i, x_i \succeq x_i'$. $x_i$ is **strictly dominant** if for all $x_i' \in X_i$ such that $x_i \neq x_i', x_i \succ x_i'$.

**Definition**: For a mixed strategy $x_i$, its **support**, $support(x_i)$, is the set of pure strategies $\pi_{i, j}$, such that $x_i(j) > 0$.

**Proposition**: Every dominant strategy $x_i$ is in fact a “weighted average” of pure dominant strategies, i.e., each $\pi_{i, j} \in support(x_i)$ is also dominant.

*Moreover, only a pure strategy can be **strictly** dominant.*

**Proof**: weighted average of pure strategies

$$
U_i(x_{-i}; x_i) = \sum_{j = 1}^{m_i} x_i(j)\cdot U_i(x_{-i}; \pi_{i, j})
$$

If $x_i$ is dominant, then for any $x_{-i}$, $U_i(x_{-i}; x_i) \geq U_i(x_{-i}; \pi_{i, j})$, for all $j$. But then if $x_i(j) > 0$, $U_i(x_{-i};x_i) = U_i(x_{-i}; \pi_{i, j})$. (Useful Corollary.) 

If $x_i$ is strictly dominant, it must clearly be equal to the unique pure strategy in its support. (Otherwise, $U_i(x_{-i}; x_i) > U_i(x_{-i}; \pi_{i, j})$ will not hold.)

### Obviously bad: strictly dominated strategies

**Definition**: We say a strategy $x_i \in X_i$ is **strictly dominated** if there ***exists*** another strategy $x_i'$ such that $x_i' \succ x_i$. We say $x_i$ is **weakly dominated** if there ***exists*** $x_i'$ such that $x_i' \succeq x_i$ and for some $x_{-i} \in X_i$, $U_i(x_{-i}; x_i') > U_i(x_{-i}; x_i)$.

Weakly dominated strategies aren’t necessarily as “bad”. It depends on what you think others will play. In particular, there can be Nash Equilibria where everybody is playing a weakly dominated strategy: 

$$
\begin{bmatrix} (0, 0) & (0, 0) \\ (0, 0) & (1, 1)\end{bmatrix}
$$

Example Is the last row strictly dominated?

$$
\begin{bmatrix} 30 & 0 & 0 \\ 0 & 30 & 0 \\ 0 & 0 & 30 \\ 5 & 5 & 5 \end{bmatrix}
$$

No matter how to choose, there always exists a strategy whose expected payoff is larger than the lest row’s.

### Iterated SDS elimination algorithm

### Computing Nash Equilibria: **a first clue**

**Proposition** In an $n$-player game, a profile $x^\ast$ is a Nash Equilibrium if and only if there exists $w_1, \cdots, w_n \in \mathbb{R}$, such that the following hold:

1. For all players $i$, and every $\pi_{i, j}\in support(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) = w_i$, and 
2. For all players $i$, and every $\pi_{i, j} \notin support(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) \leq w_i$.

**Note**: such $w_i$’ necessarily satisfy $w_i = U_i(x^\ast).$