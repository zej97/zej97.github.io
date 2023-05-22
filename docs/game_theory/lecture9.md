---
layout: default
title: Lecture 9 Computing Solutions for General Strategic Games, Part II
parent: Game Theory
nav_order: 8
---

## Lecture 9 Computing Solutions for General Strategic Games: Part II: Nash Equilibria

### Computing Nash Equilibria: **a first clue**

**Proposition** In an $n$-player game, a profile $x^\ast$ is a Nash Equilibrium if and only if there exists $w_1, \cdots, w_n \in \mathbb{R}$, such that the following hold:

1. For all players $i$, and every $\pi_{i, j}\in {\rm support}(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) = w_i$, and 
2. For all players $i$, and every $\pi_{i, j} \notin {\rm support}(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) \leq w_i$.

**Note**: such $w_i$’s necessarily satisfy $w_i = U_i(x^\ast).$

### Using our first clue

- Suppose we somehow know support sets, ${\rm support}_1 \subseteq S_1, \cdots, {\rm support}_n \subseteq S_n$, for **some** Nash Equilibrium $x^\ast = (x_1^\ast, \cdots, x_n^\ast)$.
- Then, using proposition 1, to find a NE we only need to solve the following **system of constraints**:
    1. $\forall$ players $i$, and $\forall j \in {\rm support}_i$, $U_i(x_{-i};\pi_{i,j}) = w_i$,
    2. $\forall$ players $i$, and $\forall j \notin {\rm support}_i$, $U_i(x_{-i};\pi_{i,j}) \le w_i$.
    3. $\forall$ players $i = 1, \cdots,n$, $\sum_{j=1}^{m_i}x_i(j) = 1$.
    4. $\forall$ players $i = 1, \cdots,n$, and for $j \in {\rm support}_i$, $x_i(j) \ge 0$.
    5. $\forall$ players $i = 1, \cdots,n$, and for $j \notin {\rm support}_i$, $x_i(j) = 0$.
- This system has $\sum_{i = 1}^n m_i + n$ **variables**:
    
    $$
    x_1(1),\cdots, x_1(m_1), \cdots, x_n(1), \cdots, x_n(m_n), w_1, \cdots, w_n
    $$
    

How do we find ${\rm support}_1 \& {\rm support}_2$? Just **guess**!

### First algorithm to find NE's in 2-player games

$\text{Input}$: A 2-player strategic game $\Gamma$, given by rational values $u_1(s, s^\prime)$ & $u_2(s, s^\prime)$, for all $s\in S_1$ & $s^\prime \in S_2$. (I.e., the input is $2 \cdot m_1 \cdot m_2$ rational numbers.)

$\text{Alogrithm}$:

- For all possible ${\rm support}_1\subseteq S_1$ & ${\rm support}_2 \subseteq S_2$:
    - Check if  the corresponding LP has a feasible solution $x^\ast, w_1, \cdots, w_n$. (using, e.g., Simplex)
    - If so, **STOP**: the feasible solution $x^\ast$ is a Nash Equilibrium (and $w_i = U_i(x^\ast)$).

**Proposition**: Every finite 2-player game has a rational NE. (Furthermore, the rational number are not too big, i.e., are polynomial sized.)

The algorithm can easily be adapted to find not just any NE, but a good one. For example:

Finding a NE that maximizes utility social welfare:

1. For each support sets, simply solve the LP constraints while maximizing the objective
    
    $$
    f(x,w) = w_1 + \cdots + w_n
    $$
    
2. Keep track of best NE encountered, & output optimal NE after checking all support sets.