---
layout: default
title: Lecture 7 LP Duality
parent: Game Theory
nav_order: 6
---

## Lecture 7 LP Duality

### Solving LPs against an Adversary

Suppose you want to optimize this Primal LP:

**Maximize** $c^\top  x$

**Subject to**:

$$
\begin{align*}&Ax \leq b\\ &x_1, \cdots, x_n \geq 0 \end{align*}
$$

Suppose an “Adversary” comes along with a $m$-vector $y\in \mathbb{R}^m, y \geq 0$, such that: $c^\top  \leq y^\top  A$.

For any solution, $x$, you may have for the Primal:

$$
\begin{align*} c^\top x &\leq (y^\top A) x &\text{ (because } x \geq 0 \text{\ \& \ } c^\top  \leq y^\top  A) \\ &= y^\top (Ax) \\ &\leq y^\top b &\text{ (because } y^\top  \geq 0 \text{\ \&\ } Ax \leq b)\end{align*}
$$

So, the adversary’s goal is to minimize $y^\top b$, subject to $c^\top  \leq y^\top A$, i.e., optimize the **Dual LP**.

### The LP Duality Theorem

**Proposition**: (Weak Duality)

$$
c^\top  x^\ast \leq b^\top y^\ast
$$

**Theorem**: (Strong Duality, von Neumann’47) One of the following for situations holds:

1. Both the primal and dual LPs are feasible, and for any optimal solutions $x^\ast$ of the primal and $y^\ast$ of the dual:
    
    $$
    c^\top  x^\ast = b^\top y^\ast
    $$
    
2. The primal is infeasible and the dual is unbounded.
3. The primal is unbounded and the dual is infeasible.
4. Both LPs are infeasible.

### Useful Corollary of LP Duality

Solutions $x^\ast$ and $y^\ast$ to the primal and dual LPs, respectively, are both optimal if and only if the following hold:

1. For each primal constraint, $(Ax)_i \leq b_i$, $i = 1, \cdots, m$, either $(Ax^\ast)_i = b_i$ or $y_i^* = 0$ (or both).
2. For each dual constraint, $(A^\top y)_j \geq c_j$, $j = 1, \cdots, n$, either $(A^\top y^\ast)_j = c_j$ or $x^\ast_j = 0$ (or both).

**Proof**: By weak duality

$$
c^\top x^\ast \leq ((y^\ast)^\top A)x^\ast = (y^\ast)^\top (Ax^\ast) \leq (y^\ast)^\top b
$$

By strong duality each inequality holds with equality precisely when $x^\ast$ and $y^\ast$ are optimal. So, when optimal,

$$
(((y^\ast)^\top A - c^\top )x^\ast = 0
$$

Since both $(((y^\ast)^\top A -  c^\top ) \geq 0$ and $x^\ast \geq 0$, it must be that for each $j = 1, \cdots, n$, $(A^\top y^\ast)_j = c_j$ or $x^\ast_j = 0$.

Likewise, when optimal, $(y^\ast)^\top (b - Ax^\ast) = 0$, and thus, for each $i = 1, \cdots, m$, $(Ax^\ast)_i = b_i$ or $y_i^* = 0$.

### General Recipe for LP Duals

If the primal is:

**Maximize** $c^\top  x$

**Subject to**:

$$
\begin{align*} & (Ax)_i \leq b_i, i = 1, \cdots, d,\\& (Ax)_i = b_i, i = d + 1, \cdots, m,\\& x_1, \cdots, x_r \geq 0 \end{align*}
$$

Then the dual is:

**Minimize** $b^\top y$

**Subject to**:

$$
\begin{align*} & (A^\top y)_i \geq c_i, i = 1, \cdots, r,\\& (A^\top y)_i = c_i, i = r + 1, \cdots, n,\\& y_1, \cdots, y_d \geq 0 \end{align*}
$$

### Duality and the Minimax Theorem

Recall the LP for solving Minimax for Player 1 in a zero-sum game given by matrix $A$:

**Maximize** $v$

**Subject to**:

$$
\begin{align*} & v - (x^\top A)_j \leq 0, \text{ for } j = 1, \cdots, m_2,\\& x_1 + \cdots + x_{m_1} = 1 \\& x_1 \geq 0 \text{ for } j = 1, \cdots, m_1.\end{align*}
$$

Dual to this LP:

**Minimize** $u$

**Subject to**:

$$
\begin{align*} & u - (Ay)_i \geq 0, \text{ for } i = 1, \cdots, m_i,\\& y_1 + \cdots + y_{m_2} = 1 \\& y_j \geq 0 \text{ for } j = 1, \cdots, m_2. \end{align*}
$$

Thus, the minimax theorem follows from LP Duality: the optimal value for the two LPs is the **same**.