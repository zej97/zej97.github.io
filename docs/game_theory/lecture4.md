---
layout: default
title: Lecture 4 Zero-sum games, and the Minimax Theorem
parent: Game Theory
nav_order: 3
---
## Lecture 4 Zero-sum games, and the Minimax Theorem

### Min-maximizing strategies

Suppose Player 1 chooses a mixed strategy $x_1^\ast \in X_1$, by trying to maximum the “worst that can happen would be for Player 2 to choose $x_2$ which minimizes $(x_1^\ast)^\top Ax_2$”, where $A$ is the payoff matrix $[u(i,j)]_{m_1\times m_2}$.

**Definition**: $x_1^\ast \in X_1$ is a **minmaximizer** for Player 1 if 

$$
\min_{x_2\in X_2}(x_1^\ast)^\top Ax_2 = \max_{x_1\in X_1}\min_{x_2\in X_2}(x_1)^\top Ax_2
$$

Similarly, $x_2^\ast \in X_2$ is a **maxminimizer** for Player 2 if 

$$
\max_{x_1\in X_1}(x_1)^\top Ax_2^\ast = \min_{x_2\in X_2}\max_{x_1 \in X_1}(x_1)^\top A{x_2}
$$

Note that (obviously)

$$
\min_{x_2 \in X_2}(x_1^\ast)^\top Ax_2 \leq (x_1^\ast)^\top Ax_2^\ast \leq \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast
$$

### The Minimax Theorem

**Theorem(von Neumann)** Let a 2p-zs game $\Gamma$ be given by an $(m_1 \times m_2)$-matrix $A$ of real numbers. There exists a unique value $v^* \in \mathbb{R}$, such that there exists $x^\ast = (x_1^\ast, x_2^\ast)\in X$ such that

1. $((x_1^\ast)^\top A)_j \geq v^*$, for $j = 1, \cdots, m_2$.
2. $(Ax_2^\ast)_j \leq v^*$, for $j = 1, \cdots, m_1$.
3. And (thus) $v^* = (x_1^\ast)^\top Ax_2^\ast$ and 
    
    $$
    \min_{x_2 \in X_2}(x_1^\ast)^\top Ax_2 = (x_1^\ast)^\top Ax_2^\ast = \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast
    $$
    
4. In fact, the above conditions all hold precisely when $x^\ast = (x_1^\ast, x_2^\ast)$ is any **Nash Equilibrium**. Equivalently, they hold precisely when $x_1^\ast$ is any minmaximizer and $x_2^\ast$ is any maxminimizer.

**Note**:

1. (1.)  says $x_1^\ast$ guarantees Player 1 at least expected profit $v^*$ and (2.) says $x_2^\ast$ guarantees Player 2 at most expected loss $v^*$.
2. We call the unique $v^*$ the **minimax value** of game $\Gamma$, and call any such $x^\ast = (x_1^\ast, x_2^\ast)$ a **minimax profile**.
3. It is obvious that the maximum profit that Player 1 can guarantee for itself should be $\leq$ the minimum loss that Player 2 can guarantee for itself, i.e., that 
    
    $$
    \max_{x_1\in X_1}\min_{x_2\in X_2}(x_1)^\top Ax_2 \leq \min_{x_2\in X_2}\max_{x_1\in X_1}(x_1)^\top Ax_2
    $$
    
    (Look back the whole definition.)
    

**Proof**: Let $x^\ast = (x_1^\ast, x_2^\ast) \in X$ be a NE of the 2-player zero-sum game $\Gamma$, with matrix $A$.

Let $v^* := (x_1^\ast)^\top Ax_2^\ast = U_1(x^\ast) = - U_2(x^\ast)$.

Since $x_1^\ast$ and $x_2^\ast$ are “best responses” to each other, we know that for $i \in \lbrace 1, 2\rbrace$

$$
U_i(x_{-i}^*; \pi_{i,j}) \leq U_i(x^\ast)
$$

Then we have

1. $U_1(x_{-1}^*; \pi_{1, j}) = (Ax_2^\ast)_j$, thus,
    
    $$
    (Ax_2^\ast)_j \leq U_1(x^\ast) = v^*
    $$
    
    The (2.) Q.E.D.
    
2. $U_2(x_{-2}^*; \pi_{2, j}) = -((x_1^\ast)^\top A)_j$, thus
    
    $$
    - ((x_1^\ast)^\top A)_j \leq U_2(x^\ast) = - v^* \\ s.t.\  ((x_1^\ast)^\top A)_j \geq v^*
    $$
    
    The (1.) Q.E.D.
    
3. Since 1.  and $(x_1)^\top Ax_2^\ast$ is a weighted average of $(Ax_2^\ast)_j$, thus
    
    $$
    \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast \leq v^*
    $$
    
    Similarly, since 2. and $(x_1^\ast)^\top Ax_2$ is a weighted average of $((x_1^\ast)^\top A)_j$, thus
    
    $$
    \min_{x_2\in X_2}(x_1^\ast)^\top Ax_2 \geq v^*
    $$
    
    So we finally have
    
    $$
    \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast \leq v^* = (x_1^\ast)^\top Ax_2^\ast \leq \min_{x_2\in X_2}(x_1^\ast)^\top Ax_2
    $$
    
    which is entirely the opposite inequality we earlier noted
    
    $$
    \min_{x_2 \in X_2}(x_1^\ast)^\top Ax_2 \leq (x_1^\ast)^\top Ax_2^\ast \leq \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast
    $$
    
    Therefore, 
    
    $$
    \min_{x_2 \in X_2}(x_1^\ast)^\top Ax_2 = (x_1^\ast)^\top Ax_2^\ast = \max_{x_1\in X_1}(x_1)^\top Ax_2^\ast
    $$
    
4. We didn’t assume anything about the particular NE we chose. So, for ever NE, $x^\ast$, letting $v' = (x^\ast)^\top Ax_2^\ast$,
    
    $$
    \max_{x_1\in X_1}\min_{x_2 \in X_2}(x_1)^\top Ax_2 = v' = v^* = (x_1^\ast)^\top Ax_2^\ast = \min_{x_2\in X_2}\max_{x_1\in X_1}(x_1)^\top Ax_2
    $$
    
    Moreover, if $x^\ast = (x_1^\ast, x_2^\ast)$ satisfies conditions (1.) and (2.) for some $v^*$, then $x^\ast$ must be a NE.

### Useful Corollary for Minimax

In a minimax profile $x^\ast = (x_1^\ast, x_2^\ast)$,

1. if $x_2^\ast(j) > 0$, then $((x^\ast_1)^\top A)_j = (x^\ast_1)^\top A x_2^\ast = v^\ast$.
2. if $x_1^\ast(j) > 0$, then $(Ax^\ast_2)_j = (x_1^\ast)^\top A x_2^\ast = v^\ast$.

### Minimax as an optimization problem

**Maximize** $v$

**Subject to**:

$$
\begin{align*}&(x_1^\top A)_j \geq v \quad \text{for }j =1, \cdots, m_2, \\&x_1(1) + \cdots + x_1(m_1) = 1, \\&x_1(j) \geq 0 \quad \text{for }j = 1, \cdots, m_1 \end{align*}
$$