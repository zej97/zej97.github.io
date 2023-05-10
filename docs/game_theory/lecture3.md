---
layout: default
title: Lecture 3 Nash’s Theorem
parent: Game Theory
nav_order: 2
---
## Lecture 3 Nash’s Theorem

### The Brouwer Fixed Point Theorem

**Theorem(Brouwer, 1909)** Every continuous function $f: D \to D$ mapping a compact and convex, nonempty subset $D \subseteq \mathbb{R}^m$ to itself has a “fixed point”, i.e., there is $x^\ast \in D$ such that $f(x^\ast) = x^\ast$.

**Fact**: ****The set of profiles $X = X_1 \times \cdots \times X_n$ is a compact and convex subset of $\mathbb{R}^m$, where $m = \sum_{i = 1}^n m_i$, with $m_i = \lvert S_i \rvert$.

### Proof of Nash’s Theorem

**Proof**: We will define **a** continuous function $f: X \to X$, where $X = X_1 \times \cdots \times X_n$, and we will show that if $f(x^\ast) = x^\ast$ then $x^\ast = (x_1^\ast, \cdots, x_n^\ast)$ must be a Nash Equilibrium.

**Claim**: A profile $x^\ast = (x_1^\ast, \cdots, x_n^\ast) \in X$ is a Nash Equilibrium if and only if, for every Player $i$, and every pure strategy $\pi _{i, j}, j \in S_i$:

$$
U_i(x^\ast) \geq U_i(x^\ast_{-i}; \pi_{i, j})
$$

**Proof of claim**: If $x^\ast$ is a NE then, it is obvious by definition that $U_i(x^\ast) \geq U_i(x_{-i}^\ast; \pi_{i, j})$.

For the other direction: by calculation it is easy to see that for any mixed strategy $x_i \in X_i$, 

$$
U_i(x_{-i}^\ast; x_i) = \sum _{j= 1}^{m_i}x_i(j) \cdot U_i(x^\ast_{-i};\pi_{i, j}) \leq U_i(x^\ast)
$$

The inequality is true, since we assume that $U_i(x^\ast) \geq U_i(x_{-i}^\ast;\pi_{i,j})$. Therefore, each $x_i^\ast$ is a best response to strategy $x_{-i}^\ast$. In other words, $x^\ast$ is a Nash Equilibrium.

With this **Claim**, we can rephrase our goal of proving $x^\ast$ is a NE to finding $x^\ast$ such that 

$$
U_i(x_{-i}^\ast; \pi_{i, j}) \leq U_i(x^\ast)
$$

for all Player $i \in N$, and all $j \in \lbrace 1, \cdots, m_i\rbrace$. 

For a mixed profile $x = (x_1, \cdots, x_n) \in X$, let 

$$
\varphi_{i, j}(x) = \max\lbrace 0, U_i(x_{-i};\pi_{i, j}) - U_i(x)\rbrace
$$

Define $f: X \to X$ as follows: For $x = (x_1, \cdots, x_n) \in X$, let

$$
f(x) = (x_i', \cdots, x_n')
$$

where for all $i$, and $j = 1, \cdots, m_i$,

$$
x_i'(j) = \frac{x_i(j) + \varphi_{i,j}(x)}{1 + \sum_{k=1}^{m_i}\varphi_{i, k}(x)}
$$

Thus, by ***Brouwer***, there exists $x^\ast$ such that $f(x^\ast) = x^\ast$.

**Now we have to show $x^\ast$ is a NE.**

For each $i$, and for $j = 1, \cdots, m_i$,

$$
x_i^\ast(j) = \frac{x_i^\ast(j) + \varphi_{i, j}(x^\ast)}{1 + \sum_{k = 1}^{m_i}\varphi_{i, k}(x^\ast)}
$$

hence,

$$
x_i^*(j) \sum_{k = 1}^{m_i} \varphi_{i, k}(x^\ast) = \varphi_{i, j}(x^\ast)
$$

We will show that in fact this implies $\varphi_{i, j}(x^\ast)$ must be equal to $0$ for **all** $j$.

**Claim**: For any mixed profile $x$, for each Player $i$, there is some $j$ such that $x_i(j) > 0$ and $\varphi_{i, j}(x) = 0$.

**Proof of claim**: Since $U_i(x)$ is the weighted average of $U_i(x_{-i}; \pi_{i, j})$’s, based on the weights in $x_i$, there **must be** **some** $j$ used in $x_i$, i.e., with $x_i(j) > 0$, such that $U_i(x_{-i};\pi_{i, j})$ is no more than the weighted average. i.e., 

$$
U_i(x_i;\pi_{i, j}) \leq U_i(x)
$$

Therefore,

$$
\varphi_{i, j}(x) = \max\lbrace 0, U_i(x_{-i};\pi_{i, j}) - U_i(x)\rbrace = 0
$$

Thus, for such a $j$, $x^\ast_i(j) > 0$ and 

$$
x^\ast_i(j) \sum_{k = 1}^{m_i} \varphi_{i, k}(x^\ast) = \varphi_{i, j}(x^\ast) = 0
$$

But, since $\varphi_{i, k}(x^\ast)$’s are all $\geq 0$ and $x^\ast_i > 0$, this means $\varphi_{i, k}(x^\ast) = 0$ for all $k = 1, \cdots, m_i$.  Thus, for all Player $i$, and for $j = 1, \cdots, m_i$,

$$
U_i(x^\ast_{-i}; \pi_{i, j}) \leq U_i(x^\ast)
$$

**Q.D.E.**

### Useful Corollary for Nash Equilibria

$$
U_i(x^\ast) = U_i(x^\ast_{-i};\pi_{i, j})
$$

whenever $x^\ast_i(j) > 0$. i.e., each such $\pi_{i, j}$ **is itself a best response** to $x_{-i}^*$.

**Proof**: If $x^\ast$ is a NE, thus $U_i(x^\ast)$ must $\geq U_i(x^\ast_{-i}; \pi_{i, j})$, for all $j = 1, \cdots, m_i$. 

Since $U_i(x^\ast) = \sum_{j = 1}^{m_i}x^\ast_i(j) \cdot U_i(x^\ast_{-i};\pi_{i, j})$ , consider the following two cases:

1. If $U_i(x^\ast) > U(x^\ast_{-i};\pi_{i, j})$ for all $j = 1, \cdots, m_i$, then $U_i(x^\ast) > \sum_{j = 1}^{m_i}x^\ast_i(j) \cdot U_i(x^\ast_{-i};\pi_{i, j})$  which is not true;
2. If $U_i(x^\ast) > U_i(x^\ast_{-i};\pi_{i, j})$ for some $j = 1, \cdots, m_i$, then there must exist $U_i(x^\ast) < U_i(x^\ast_{-i};\pi_{i, j'})$ for some $j' = 1, \cdots, m_i$ and $j' \neq j$ when $U_i(x^\ast) = \sum_{j = 1}^{m_i}x^\ast_i(j) \cdot U_i(x^\ast_{-i};\pi_{i, j})$  holds, which is not true according to the property of NE.

In summary, $U_i(x^\ast)$ cannot be greater than $U_i(x_{-i}^\ast; \pi_{i,j})$ if $x_i^\ast(j) > 0$. Therefore, $U_i(x^\ast) = U_i(x^\ast_i; \pi_{i, j})$.

### Evolutionarily Stable Strategies