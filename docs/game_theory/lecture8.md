---
layout: default
title: Lecture 8 Computing Solutions for General Finite Strategic Games, Part I
parent: Game Theory
nav_order: 7
---
## Lecture 8 Computing Solutions for General Finite Strategic Games, Part I: Dominance and iterated strategy elimination
### A partial-order on strategies: dominance

**Definition**: For $x_i, x_i^\prime \in X_i$, we say $x_i$ dominates $x^\prime_i$, denoted $x_i \succeq x^\prime_i$, if for all $x_{-i} \in X_{-i}$,

$$
U_i(x_{-i};x_i) \geq U_i(x_{-i};x_i^\prime)
$$

We say $x_i$ strictly dominates $x_i^\prime$, denoted $x_i \succ x_i^\prime$, if for all $x_{-i}\in X_{-i}$

$$
U_i(x_{-i};x_i) > U_i(x_{-i};x_i^\prime)
$$

Proposition: $x_i$ dominates $x_i^\prime$ if and only if for all pure counter profiles $\pi_{-i}\in X_{-i}$.

$$
U_i(\pi_{-i};x_i) \geq U_i(\pi_{-i};x_i^\prime)
$$

Likewise, $x_i$ strictly dominates $x_i^\prime$ iff for all $\pi_{-i}$

$$
U_i(\pi_{-i};x_i) > U_i(\pi_{-i};x_i^\prime)
$$

### Obviously good strategies: dominant strategies

**Definition**: A mixed strategy $x_i \in X_i$ is **dominant** if for all $x_i^\prime \in X_i, x_i \succeq x_i^\prime$. $x_i$ is **strictly dominant** if for all $x_i^\prime \in X_i$ such that $x_i \neq x_i^\prime, x_i \succ x_i^\prime$.

**Definition**: For a mixed strategy $x_i$, its **support**, ${\rm support}(x_i)$, is the set of pure strategies $\pi_{i, j}$, such that $x_i(j) > 0$.

**Proposition**: Every dominant strategy $x_i$ is in fact a “weighted average” of pure dominant strategies, i.e., each $\pi_{i, j} \in {\rm support}(x_i)$ is also dominant.

**Moreover, only a pure strategy can be strictly dominant.**

**Proof**: weighted average of pure strategies

$$
U_i(x_{-i}; x_i) = \sum_{j = 1}^{m_i} x_i(j)\cdot U_i(x_{-i}; \pi_{i, j})
$$

If $x_i$ is dominant, then for any $x_{-i}$, $U_i(x_{-i}; x_i) \geq U_i(x_{-i}; \pi_{i, j})$ (NE), for all $j$. But then if $x_i(j) > 0$, $U_i(x_{-i};x_i) = U_i(x_{-i}; \pi_{i, j})$. (Useful Corollary.) 

If $x_i$ is strictly dominant, it must clearly be equal to the unique pure strategy in its support. (Otherwise, $U_i(x_{-i}; x_i) > U_i(x_{-i}; \pi_{i, j})$ will not hold.)

### Algorithm to find dominant strategies

- For each player $i$ and each pure strategy $s_j \in S_i$,
    1. Check if, for all pure combinations $s\in S = S_1 \times \cdots \times S_n, u_i(s_{-i};s_j) \geq u_i(s)$.
    2. If this is so for all $s$, output $s_j$ is a dominant strategy for player $i$.
- If no such pure strategy found, then there are no dominant strategies.

### Obviously bad: strictly dominated strategies

**Definition**: We say a strategy $x_i \in X_i$ is **strictly dominated** if there ***exists*** another strategy $x_i^\prime$ such that $x_i^\prime \succ x_i$. We say $x_i$ is **weakly dominated** if there ***exists*** $x_i^\prime$ such that $x_i^\prime \succeq x_i$ and for some $x_{-i} \in X_i$, $U_i(x_{-i}; x_i^\prime) > U_i(x_{-i}; x_i)$.

Weakly dominated strategies aren’t necessarily as “bad”. It depends on what you think others will play. In particular, there can be Nash Equilibria where everybody is playing a weakly dominated strategy: 

$$
\begin{bmatrix} (0, 0) & (0, 0) \\ (0, 0) & (1, 1)\end{bmatrix}
$$

**Example**: Is the last row strictly dominated?

$$
\begin{bmatrix} 30 & 0 & 0 \\ 0 & 30 & 0 \\ 0 & 0 & 30 \\ 5 & 5 & 5 \end{bmatrix}
$$

No matter how to choose, there always exists a strategy whose expected payoff is larger than the lest row’s.

### Common knowledge and strategy elimination

Definition: A fact $P$ is common knowledge among all $n$ players if:

- For every player $i$, “Player $i$ knows $P$”: call this fact $P_{\langle i \rangle}$.
- And, inductively, for $k \geq 1$, for all players $i$, and all sequences $s = i_1 \cdots i_k\in \lbrace 1, \cdots, n\rbrace^k$, “Player $i$ knows $P_{\langle s \rangle}$”: call this fact $P_{\langle i, s \rangle}$.

**RNK hypothesis**: every player’s rationality is common knowledge among all players.

### Iterated SDS elimination algorithm

Assuming the RNK, we can safely conduct the following strategy elimination algorithm:

- ${\rm While}$ (some pure strategy $\pi_{i,j}$ is **strictly** dominated)
    - eliminate $\pi_{i,j}$ from the game,
    - obtaining a new residual game;
