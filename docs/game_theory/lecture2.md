---
layout: default
title: Lecture 2 Mixed Strategies, Expected Payoffs, and Nash Equilibrium
parent: Game Theory
nav_order: 1
---
## Lecture 2 Mixed Strategies, Expected Payoffs, and Nash Equilibrium

### Pure Strategy

For Player $i$, a **finite** set $S_i = \lbrace 1, \cdots, m_i\rbrace$ of (pure) strategies.

### Mixed Strategy

A mixed strategy for Player $i$ is a vector $x_i = (x_i(1), \cdots, x_i(m_i))$, these probabilities sums up to $1$. Let $X_i$ be **the set of mixed strategies** for Player $i$. 

For an $n$-player game, let 

$$X = X_1 \times \cdots \times X_n$$ 

denote the set of all possible combinations, or “**profiles**”, of mixed strategies.

### Expected Payoffs

Let $x = (x_1, \cdots, x_n) \in X$ be a profile of mixed strategies. For $s = (s_1, \cdots, s_n) \in S$ a combination of pure strategies ($s_i$ is one elements in $S_i = \lbrace 1, \cdots, {m_i}\rbrace$), let

$$
x(s) := \prod_{j = 1}^{n}x_j(s_j)
$$

be the probability of combination $s$ under mixed profile $x$. Clearly, $x_j(s_j)$ is the probability of Player $j$ choosing the pure strategy $s_j$.

**Definition:** The expected payoff of Player $i$ under a mixed strategy profile $x = (x_1, \cdots, x_n) \in X$, is:

$$
U_i(x) = \sum_{s\in S} x(s)\cdot u_i(s)
$$

### Best Response

**Definition**: A (mixed) strategy $z_i \in X_i$ is a **best response** for Player $i$ to $x_{-i}$ if for all $y_i \in X_i$,

$$
U_i(x_{-i};z_i) \geq U_i(x_{-i};y_i)
$$

### Nash Equilibrium

**Definition**: ****For a strategic game $\Gamma$, a strategy profile $x = (x_1, \cdots, x_n) \in X$ is a mixed Nash Equilibrium if for every Player $i$, $x_i$ is a best response to $x_{- i}$.

In other words, for every Player $i = 1, \cdots, n$, and for every mixed strategy $y_i \in X_i$,

$$
U_i(x_{-i};x_i)\geq U_i(x_{-i};y_i)
$$

In other words, no player can improve its own payoff by ***unilaterally*** deviating from the mixed strategy profile $x = (x_1, \cdots, x_n)$.

$x$ is called a pure Nash Equilibrium if in addition every $x_i$ is a pure strategy $\pi_{i, j}$, for some $j \in S_j$.