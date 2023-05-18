---
layout: default
title: Lecture 6 The Simplex Algorithm
parent: Game Theory
nav_order: 5
---

## Lecture 6 The Simplex Algorithm

“We don’t seem to get stuck in any locally optimal vertex. That’s the geometric idea of simplex.

### Geometric idea of simplex

$\text{Input}$: Given $(f, {\rm Opt}, C)$ and a start “vertex” $x\in K(C) \subseteq \mathbb{R}^n$.

$\text{While}$ ($x$ has a “neighbor vertex”, $x^\prime$, with $f(x^\prime) > f(x)$)

- Pick such a neighbor $x^\prime$. Let $x := x^\prime$.
- (If the “neighbor” is at “infinity”, $\text{Output}$: “unbounded”.)

$\text{Output}$: $x^\ast := x$ is optimal solution, with optimal value $f(x^\ast)$.

But why should this work? Why don’t we get stuck in some local optimum?

**Key reason**: The region $K(C)$ is **convex**. ($x, y\in K,\  \lambda x + (1 - \lambda)y \in K,\ \text{for all }\lambda\in [0, 1]$ .)

**Fact**: On a convex region, a local optimum of a linear objective is always a global optimum.

### LP’s in Primal Form

Using the simplification rules from the last lecture, we can convert any LP into the following form:

**Maximize** $c_1 x_1+c_2 x_2+\ldots+c_n x_n+d$

**Subject to**:

$$
\begin{array}{ll}a_{1,1} x_1+a_{1,2} x_2+\ldots+a_{1, n} x_n & \leq b_1 \\a_{2,1} x_1+a_{2,2} x_2+\ldots+a_{2, n} x_n & \leq b_2 \\\ldots & \cdots \\\ldots & \cdots \\a_{m, 1} x_1+a_{m, 2} x_2+\ldots+a_{m, n} x_n & \leq b_m \\x_1, \ldots, x_n \geq 0\end{array}
$$

### Slack variables

By adding a slack variable $y_i$ to each inequality, we get an equivalent LP explain, with only equalities (& non-neg):

**Maximize** $c_1 x_1+c_2 x_2+\ldots+c_n x_n+d$

**Subject to**:

$$
\begin{array}{ll}a_{1,1} x_1+a_{1,2} x_2+\ldots+a_{1, n} x_n+y_1 & =b_1 \\a_{2,1} x_1+a_{2,2} x_2+\ldots+a_{2, n} x_n+y_2 & =b_2 \\\ldots & \ldots \\a_{m, 1} x_1+a_{m, 2} x_2+\ldots+a_{m, n} x_n+y_m & =b_m \\x_1, \ldots, x_n \geq 0 ; \quad y_1, \ldots, y_m \geq 0\end{array}
$$

The new LP has some **particularly nice properties**:

1. Every equality constraint has at least one variable with coefficient $1$ that doesn’t appear in any other equality.
2. Picking one such variable, $y_i$, for each equality, we obtain a set of $m$ variables $B = \lbrace y_1, \cdots, y_m\rbrace$ called a **Basis**.
3. Objective $f(x)$ involves only non-Basis variables.

Let’s call an LP in this form a “dictionary”.

### Basic Feasible Solutions

Rewrite our dictionary as:

**Maximize** $c_1 x_1+c_2 x_2+\ldots+c_n x_n+d$

**Subject to**:

$$
\begin{aligned}& x_{n+1}=b_1-a_{1,1} x_1-a_{1,2} x_2-\ldots-a_{1, n} x_n \\& x_{n+2}=b_2-a_{2,1} x_1-a_{2,2} x_2-\ldots-a_{2, n} x_n \\&\ldots \quad \quad \ldots \\& x_{n+m}=b_m-a_{m, 1} x_1-a_{m, 2} x_2-\ldots-a_{m, n} x_n \\& x_1, \ldots, x_{n+m} \geq 0 \end{aligned}
$$

Suppose, somehow, $b_i \geq 0$ for all $i = 1, \cdots, m$. Then we have a feasible dictionary and a feasible solution for it, namely, let $x_{n + i} := b_i$, for $i = 1, \cdots, m$, and let $x_j := 0$, for $j = 1, \cdots, n$. The objective value is then $f(0) = d$.

Call this a **basic feasible solution (BFS)**, with basis $B$.

**Geometry**: A **BFS** corresponds to a vertex. (But different Bases $B$ may yield the same BFS.)

**Questions**: How do we move from one BFS with basis $B$ to neighboring BFS with basis $B’$? **Answers**: Pivoting.

### Pivoting

Suppose our current dictionary basis (the variables on the left) is $B = \lbrace x_{i_1}, \cdots, x_{i_m} \rbrace$, with $x_{i_r}$ the variable on the left of constraint $C_r$.

The following pivoting procedure moves us from basis $B$ to basis $B^\prime:= (B\backslash\lbrace x_{i_r}\rbrace) \bigcup \lbrace x_j \rbrace$.

Pivoting to add $x_j$ and remove $x_{i_r}$ from basis $B$:

1. Assume $C_r$ involves $x_j$, rewrite $C_r$ as $x_j = \alpha$. (Tightest)
2. Substitute $\alpha$ for $x_j$ in other constraints $C_I$, obtaining $C_I^\prime.$
3. The new constraints $C^\prime$, have a new basis: $B^\prime:= (B\backslash\lbrace x_{i_r}\rbrace) \bigcup \lbrace x_j \rbrace$.
4. Also substitute $\alpha$ for $x_j$ in $f(x)$, so that $f(x)$ again only depends on variables not in the new basis $B^\prime$.

The new basis $B^\prime$ is a **possible neighbor** of $B$. However, not every such basis $B^\prime$ is eligible.

### Sanity checks for pivoting

To check eligibility of a pivot, we have to make sure:

1. The new constants $b_i^\prime$ remain $\geq 0$, so we retain a “**feasible dictionary**”, and thus $B^\prime$ yields a BFS.
2. The new BFS must improve, or at least must not decrease, the value $d^\prime = f(0)$ of the new objective function. 
3. We should also check for the following situations 
    1. Suppose all variables in $f(x)$ have **negative coefficients**. Then any increase from $0$ in these variables will decrease the objective. We are thus at an optimal BFS $x^\ast$. $\text{Output: Opt-BFS}: x^\ast \& f(x^\ast) = f(0) = d^\prime$
    2. Suppose a variable $x_j$ in $f(x)$ has coefficient $c_j > 0$, and the coefficient of $x_j$ in every constraint $C_r$ is $\geq 0$. Then we can increase $x_j$, and objective, to “infinity” without violating constraints. So, $\text{Output:}$ **Feasible but Unbounded**.

### Example of a simplex piovting step

It is really necessary to have an example that helps us understand pivoting.

**Maximize** $2x_1 + 3x_2 + 4x_3 + 8$

**Subject to**:

$$
\begin{aligned}& x_4=3-x_1-3 x_2-x_3 \\& x_5=4-2 x_1+x_2-2 x_3 \\& x_6=2-2 x_1-4 x_2+x_3 \\&x_1, \cdots, x_6\geq 0;\end{aligned}
$$

**The initial BFS** is $(0, 0, 0, 3, 4, 2)$. Suppose we next choose to move $x_2$ into the basis.

1. The tightest constraints is $x_6 = 2 - \ldots - 4x_2 + \ldots$, which means we can at most increase $x_2$ to $\frac{1}{2}$.
2. Rewrite the constraint $x_6=2-2 x_1-4 x_2+x_3$ as: $(\ast\ast)\ x_2 = \frac{1}{2} - \frac{1}{2}x_1 + \frac{1}{4}x_3 - \frac{1}{4}x_6$, and rewrite the objective and other constraints, by replacing $x_2$ with RHS of $(\ast\ast)$.

### Further Reading

1. [**Simplex Algorithm - oi-wiki**](https://oi-wiki.org/math/simplex/)