---
title: Game Theory
layout: default
nav_order: 2
has_children: true
---
# Game Theory

<!-- ***[Notes on Notion.so: Algorithm Game Theory and its Applications](https://zej.notion.site/Algorithm-Game-Theory-and-its-Applications-6ffba454613c41fa9b9d090b16cf66b0)*** -->

The following are notes from the lecture: [CS4 Algorithmic Game Theory and Applications](https://www.inf.ed.ac.uk/teaching/courses/agta/) in UoE.

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