---
title: Game Theory
layout: default
nav_order: 2
has_children: true
---
# Game Theory

<!-- ***[Notes on Notion.so: Algorithm Game Theory and its Applications](https://zej.notion.site/Algorithm-Game-Theory-and-its-Applications-6ffba454613c41fa9b9d090b16cf66b0)*** -->

The following are notes from the lecture: [CS4 Algorithmic Game Theory and Applications](https://www.inf.ed.ac.uk/teaching/courses/agta/) in UoE.

## Key Notes

### Nash's Theorem

**Theorem(Nash 1950)** Every finite $n$-person strategic game has a mixed Nash Equilibrium.

### Useful Corollary for Nash Equilibria

$$
U_i(x^\ast) = U_i(x^\ast_{-i};\pi_{i, j})
$$

whenever $x^\ast_i(j) > 0$. i.e., each such $\pi_{i, j}$ is itself a best response to $x_{-i}^\ast$.

### The Minimax Theorem

**Theorem(von Neumann)** Let a 2p-zs game $\Gamma$ be given by an $(m_1 \times m_2)$-matrix $A$ of real numbers. There exists a **unique** value $v^\ast \in \mathbb{R}$, such that there exists $x^\ast = (x_1^\ast, x_2^\ast)\in X$ such that

1. $((x_1^\ast)^\top )_j \geq v^\ast$, for $j = 1, \cdots, m_2$.
2. $(Ax_2^\ast)_j \leq v^\ast$, for $j = 1, \cdots, m_1$.
3. And (thus) $v^\ast = (x_1^\ast)^\top Ax_2^\ast$ and 
    
    $$
    \min_{x_2 \in X_2}(x_1^\ast)^\top Ax_2 = (x_1^\ast)^\top Ax_2^\ast = \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast
    $$
    
4. In fact, the above conditions all hold precisely when $x^\ast = (x_1^\ast, x_2^\ast)$ is any **Nash Equilibrium**. Equivalently, they hold precisely when $x_1^\ast$ is any minmaximizer and $x_2^\ast$ is any maxminimizer.

### Useful Corollary for Minimax

In a minimax profile $x^\ast = (x_1^\ast, x_2^\ast)$,

1. if $x_2^\ast(j) > 0$, then $((x^\ast_1)^\top A)_j = (x^\ast_1)^\top A x_2^\ast = v^\ast$.
2. if $x_1^\ast(j) > 0$, then $(Ax^\ast_2)_j = (x_1^\ast)^\top A x_2^\ast = v^\ast$.

### Useful Corollary of LP Duality

Solutions $x^*$ and $y^*$ to the primal and dual LPs, respectively, are both optimal if and only if the following hold:

1. For each primal constraint, $(Ax)_i \leq b_i$, $i = 1, \cdots, m$, either $(Ax^*)_i = b_i$ or $y_i^* = 0$ (or both).
2. For each dual constraint, $(A^{\rm T}y)_j \geq c_j$, $j = 1, \cdots, n$, either $(A^{\rm T}y^*) = c_j$ or $x^*_j = 0$ (or both).

### Dominance
Only a pure strategy can be strictly dominant.

### Computing Nash Equilibria: **a first clue**

**Proposition** In an $n$-player game, a profile $x^\ast$ is a Nash Equilibrium if and only if there exists $w_1, \cdots, w_n \in \mathbb{R}$, such that the following hold:

1. For all players $i$, and every $\pi_{i, j}\in {\rm support}(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) = w_i$, and 
2. For all players $i$, and every $\pi_{i, j} \notin {\rm support}(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) \leq w_i$.

**Note**: such $w_i$’s necessarily satisfy $w_i = U_i(x^\ast).$