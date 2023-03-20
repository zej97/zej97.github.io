---
title: Formula Test
layout: default
nav_order: 2
math: katex
markdown: kramdown
---

# Algorithm Game Theory and its Applications

> **Claim Definition Theorem Proof Fact Note Statement**
> 

## Reference

[Course Website: CS4 Algorithmic Game Theory and Applications](https://www.inf.ed.ac.uk/teaching/courses/agta/)

## Lecture 2 Mixed Strategies, Expected Payoffs, and Nash Equilibrium

### Pure Strategy

For Player $i$, a **finite** set $S_i = \{1, \cdots, m_i\}$ of (pure) strategies.

### Mixed Strategy

A mixed strategy for Player $i$ is a vector $x_i = (x_i(1), \cdots, x_i(m_i))$, these probabilities sums up to $1$.

Let $X_i$ be **the set of mixed strategies** for Player $i$. 

For an $n$-player game, let

$X = X_1 \times \cdots \times X_n$

denotes the set of all possible combinations, or “**profiles**”, of mixed strategies.

### Expected Payoffs

Let $x = (x_1, \cdots, x_n) \in X$ be a profile of mixed strategies. For $s = (s_1, \cdots, s_n) \in S$ a combination of pure strategies ($s_i$ is one elements in $S_i = \{1, \cdots, {m_i}\}$), let

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

### Nash’s Theorem

*The Fundamental Theorem of Game Theory*

**Theorem(Nash 1950)** Every time $n$-person strategic game has a mixed Nash Equilibrium.

## Lecture 3 Nash’s Theorem

### The Brouwer Fixed Point Theorem

**Theorem(Brouwer, 1909)** Every continuous function $f: D \to D$ mapping a compact and convex, nonempty subset $D \subseteq \mathbb{R}^m$ to itself has a “fixed point”, i.e., there is $x^{\ast} \in D$ such that $f(x^{\ast}) = x^{\ast}$.

**Fact**: The set of profiles $X = X_1 \times \cdots \times X_n$ is a compact and convex subset of $\mathbb{R}^m$, where $m = \sum_{i = 1}^n m_i$, with $m_i = \lvert S_i \rvert$.

### Proof of Nash’s Theorem

**Proof**: We will define **a** continuous function $f: X \to X$, where $X = X_1 \times \cdots \times X_n$, and we will show that if $f(x^{\ast}) = x^{\ast}$ then $x^{\ast} = (x_1^{\ast}, \cdots, x_n^{\ast})$ must be a Nash Equilibrium.

**Claim**: A profile $x^{\ast} = (x_1^{\ast}, \cdots, x_n^{\ast}) \in X$ is a Nash Equilibrium if and only if, for every Player $i$, and every pure strategy $\pi _{i, j}, j \in S_i$:

$$
U_i(x^{\ast}) \geq U_i(x^{\ast}_{-i}; \pi_{i, j})
$$

**Proof of claim**: If $x^{\ast}$ is a NE then, it is obvious by definition that $U_i(x^{\ast}) \geq U_i(x_{-i}^{\ast}; \pi_{i, j})$.

For the other direction: by calculation it is easy to see that for any mixed strategy $x_i \in X_i$, 

$$
U_i(x_{-i}^{\ast}; x_i) = \sum _{j= 1}^{m_i}x_i(j) \cdot U_i(x^{\ast}_{-i};\pi_{i, j}) \leq U_i(x^{\ast})
$$

The inequality is true, since we assume that $U_i(x^{\ast}) \geq U_i(x_{-i}^{\ast};\pi_{i,j})$. Therefore, each $x_i^{\ast}$ is a best response to strategy $x_{-i}^{\ast}$. In other words, $x^{\ast}$ is a Nash Equilibrium.

With this **Claim**, we can rephrase our goal of proving $x^{\ast}$ is a NE to finding $x^{\ast}$ such that 

$$
U_i(x_{-i}^{\ast}; \pi_{i, j}) \leq U_i(x^{\ast})
$$

for all Player $i \in N$, and all $j \in \{1, \cdots, m_i\}$. 

For a mixed profile $x = (x_1, \cdots, x_n) \in X$, let 

$$
\varphi_{i, j}(x) = \max\{0, U_i(x_{-i};\pi_{i, j}) - U_i(x)\}
$$

Define $f: X \to X$ as follows: For $x = (x_1, \cdots, x_n) \in X$, let

$$
f(x) = (x_i', \cdots, x_n')
$$

where for all $i$, and $j = 1, \cdots, m_i$,

$$
x_i'(j) = \frac{x_i(j) + \varphi_{i,j}(x)}{1 + \sum_{k=1}^{m_i}\varphi_{i, k}(x)}
$$

Thus, by ***Brouwer***, there exists $x^{\ast}$ such that $f(x^{\ast}) = x^{\ast}$.

**Now we have to show $x^{\ast}$ is a NE.**

For each $i$, and for $j = 1, \cdots, m_i$,

$$
x_i^{\ast}(j) = \frac{x_i^{\ast}(j) + \varphi_{i, j}(x^{\ast})}{1 + \sum_{k = 1}^{m_i}\varphi_{i, k}(x^{\ast})}
$$

hence,

$$
x_i^{\ast}(j) \sum_{k = 1}^{m_i} \varphi_{i, k}(x^{\ast}) = \varphi_{i, j}(x^{\ast})
$$

We will show that in fact this implies $\varphi_{i, j}(x^{\ast})$ must be equal to $0$ for **all** $j$.

**Claim**: For any mixed profile $x$, for each Player $i$, there is some $j$ such that $x_i(j) > 0$ and $\varphi_{i, j}(x) = 0$.

**Proof of claim**: Since $U_i(x)$ is the weighted average of $U_i(x_{-i}; \pi_{i, j})$’s, based on the weights in $x_i$, there **must be** **some** $j$ used in $x_i$, i.e., with $x_i(j) > 0$, such that $U_i(x_{-i};\pi_{i, j})$ is no more than the weighted average. i.e., 

$$
U_i(x_i;\pi_{i, j}) \leq U_i(x)
$$

Therefore,

$$
\varphi_{i, j}(x) = \max\{0, U_i(x_{-i};\pi_{i, j}) - U_i(x)\} = 0
$$

Thus, for such a $j$, $x^{\ast}_i(j) > 0$ and 

$$
x^{\ast}_i(j) \sum_{k = 1}^{m_i} \varphi_{i, k}(x^{\ast}) = \varphi_{i, j}(x^{\ast}) = 0
$$

But, since $\varphi_{i, k}(x^{\ast})$’s are all $\geq 0$ and $x^{\ast}_i > 0$, this means $\varphi_{i, k}(x^{\ast}) = 0$ for all $k = 1, \cdots, m_i$.  Thus, for all Player $i$, and for $j = 1, \cdots, m_i$,

$$
U_i(x^{\ast}_{-i}; \pi_{i, j}) \leq U_i(x^{\ast})
$$

**Q.D.E.**

### Useful Corollary for Nash Equilibria

$$
U_i(x^{\ast}) = U_i(x^{\ast}_{-i};\pi_{i, j})
$$

whenever $x^{\ast}_i(j) > 0$. i.e., each such $\pi_{i, j}$ **is itself a best response** to $x_{-i}^{\ast}$.

**Proof**: If $x^{\ast}$ is a NE, thus $U_i(x^{\ast})$ must $\geq U_i(x^{\ast}_{-i}; \pi_{i, j})$, for all $j = 1, \cdots, m_i$. 

Since $U_i(x^{\ast}) = \sum_{j = 1}^{m_i}x^{\ast}_i(j) \cdot U_i(x^{\ast}_{-i};\pi_{i, j})$ , consider the following two cases:

1. If $U_i(x^{\ast}) > U(x^{\ast}_{-i};\pi_{i, j})$ for all $j = 1, \cdots, m_i$, then $U_i(x^{\ast}) > \sum_{j = 1}^{m_i}x^{\ast}_i(j) \cdot U_i(x^{\ast}_{-i};\pi_{i, j})$  which is not true;
2. If $U_i(x^{\ast}) > U_i(x^{\ast}_{-i};\pi_{i, j})$ for some $j = 1, \cdots, m_i$, then there must exist $U_i(x^{\ast}) < U_i(x^{\ast}_{-i};\pi_{i, j'})$ for some $j' = 1, \cdots, m_i$ and $j' \neq j$ when $U_i(x^{\ast}) = \sum_{j = 1}^{m_i}x^{\ast}_i(j) \cdot U_i(x^{\ast}_{-i};\pi_{i, j})$  holds, which is not true according to the property of NE.

In summary, $U_i(x^{\ast})$ cannot be greater than $U_i(x_{-i}^{\ast}; \pi_{i,j})$ if $x_i^{\ast}(j) > 0$. Therefore, $U_i(x^{\ast}) = U_i(x^{\ast}_i; \pi_{i, j})$.

## Lecture 4 Zero-sum games, and the Minimax Theorem

### Min-maximizing strategies

Suppose Player 1 chooses a mixed strategy $x_1^{\ast} \in X_1$, by trying to maximum the “worst that can happen would be for Player 2 to choose $x_2$ which minimizes $(x_1^{\ast})^{\rm T}Ax_2$”.

**Definition**: $x_1^{\ast} \in X_1$ is a ***minmaximizer*** for Player 1 if 

$$
\min_{x_2\in X_2}(x_1^{\ast})Ax_2 = \max_{x_1\in X_1}\min_{x_2\in X_2}(x_1)^{\rm T}Ax_2
$$

Similarly, $x_2^{\ast} \in X_2$ is a ***maxminimizer*** for Player 2 if 

$$
\max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast} = \min_{x_2\in X_2}\max_{x_1 \in X_1}(x_1)^{\rm T}A{x_2}
$$

Note that (obviously)

$$
\min_{x_2 \in X_2}(x_1^{\ast})^{\rm T}Ax_2 \leq (x_1^{\ast})^{\rm T}Ax_2^{\ast} \leq \max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast}
$$

### The Minimax Theorem

**Theorem(von Neumann)** Let a 2p-zs game $\Gamma$ be given by an $(m_1 \times m_2)$-matrix $A$ of real numbers. There exists a unique value $v^{\ast} \in \mathbb{R}$, such that there exists $x^{\ast} = (x_1^{\ast}, x_2^{\ast})\in X$ such that

1. $((x_1^{\ast})^{\rm T})_j \geq v^{\ast}$, for $j = 1, \cdots, m_2$.
2. $(Ax_2^{\ast})_j \leq v^{\ast}$, for $j = 1, \cdots, m_1$.
3. And (thus) $v^{\ast} = (x_1^{\ast})^{\rm T}Ax_2^{\ast}$ and 
   
    $$
    \min_{x_2 \in X_2}(x_1^{\ast})^{\rm T}Ax_2 = (x_1^{\ast})^{\rm T}Ax_2^{\ast} = \max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast}
    $$
    
4. In fact, the above conditions all hold precisely when $x^{\ast} = (x_1^{\ast}, x_2^{\ast})$ is any **Nash Equilibrium**. Equivalently, they hold precisely when $x_1^{\ast}$ is any minmaximizer and $x_2^{\ast}$ is any maxminimizer.

**Note**:

1. (1.)  says $x_1^{\ast}$ guarantees Player 1 at least expected profit $v^{\ast}$ and (2.) says $x_2^{\ast}$ guarantees Player 2 at most expected loss $v^{\ast}$.
2. We call the unique $v^{\ast}$ the **minimax value** of game $\Gamma$, and call any such $x^{\ast} = (x_1^{\ast}, x_2^{\ast})$ a **minimax profile**.
3. It is obvious that the maximum profit that Player 1 can guarantee for itself should be $\leq$ the minimum loss that Player 2 can guarantee for itself, i.e., that 
   
    $$
    \max_{x_1\in X_1}\min_{x_2\in X_2}(x_1)^{\rm T}Ax_2 \leq \min_{x_2\in X_2}\max_{x_1\in X_1}(x_1)^{\rm T}Ax_2
    $$
    
    (Look back the whole definition.)
    

**Proof**: Let $x^{\ast} = (x_1^{\ast}, x_2^{\ast}) \in X$ be a NE of the 2-player zero-sum game $\Gamma$, with matrix $A$.

Let $v^{\ast} := (x_1^{\ast})^{\rm T}Ax_2^{\ast} = U_1(x^{\ast}) = - U_2(x^{\ast})$.

Since $x_1^{\ast}$ and $x_2^{\ast}$ are “best responses” to each other, we know that for $i \in \{1, 2\}$

$$
U_i(x_{-i}^{\ast}; \pi_{i,j}) \leq U_i(x^{\ast})
$$

Then we have

1. $U_1(x_{-1}^{\ast}; \pi_{1, j}) = (Ax_2^{\ast})_j$, thus,
   
    $$
    (Ax_2^{\ast})_j \leq U_1(x^{\ast}) = v^{\ast}
    $$
    
    The (1.) Q.E.D.
    
2. $U_2(x_{-2}^{\ast}; \pi_{2, j}) = -((x_1^{\ast})^{\rm T}A)_j$, thus
   
    $$
    - ((x_1^{\ast})^{\rm T}A)_j \leq U_2(x^{\ast}) = - v^{\ast} \\ s.t.\  ((x_1^{\ast})^{\rm T}A)_j \geq v^{\ast}
    $$
    
    The (2.) Q.E.D.
    
3. Since 1.  and $(x_1)^{\rm T}Ax_2^{\ast}$ is a weighted average of $(Ax_2^{\ast})_j$, thus
   
    $$
    \max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast} \leq v^{\ast}
    $$
    
    Similarly, since 2. and $(x_1^{\ast})^{\rm T}Ax_2$ is a weighted average of $((x_1^{\ast})^{\rm T}A)_j$, thus
    
    $$
    \min_{x_2\in X_2}(x_1^{\ast})^{\rm T}Ax_2 \geq v^{\ast}
    $$
    
    So we finally have
    
    $$
    \max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast} \leq v^{\ast} = (x_1^{\ast})^{\rm T}Ax_2^{\ast} \leq \min_{x_2\in X_2}(x_1^{\ast})^{\rm T}Ax_2
    $$
    
    which is entirely the opposite inequality we earlier noted
    
    $$
    \min_{x_2 \in X_2}(x_1^{\ast})^{\rm T}Ax_2 \leq (x_1^{\ast})^{\rm T}Ax_2^{\ast} \leq \max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast}
    $$
    
    Therefore, 
    
    $$
    \min_{x_2 \in X_2}(x_1^{\ast})^{\rm T}Ax_2 = (x_1^{\ast})^{\rm T}Ax_2^{\ast} = \max_{x_1\in X_1}(x_1)^{\rm T}Ax_2^{\ast}
    $$
    
4. We didn’t assume anything about the particular NE we chose. So, for ever NE, $x^{\ast}$, letting $v' = (x^{\ast})^{\rm T}Ax_2^{\ast}$,
   
    $$
    \max_{x_1\in X_1}\min_{x_2 \in X_2}(x_1)^{\rm T}Ax_2 = v' = v^{\ast} = (x_1^{\ast})^{\rm T}Ax_2^{\ast} = \min_{x_2\in X_2}\max_{x_1\in X_1}(x_1)^{\rm T}Ax_2
    $$
    
    Moreover, if $x^{\ast} = (x_1^{\ast}, x_2^{\ast})$ satisfies conditions (1.) and (2.) for some $v^{\ast}$, then $x^{\ast}$ must be a NE.
    

## Lecture 5 Introduction to Linear Programming

### Definition of LR

**Definition**: A Linear Programming or Linear Optimization problem instance  $(f, {\rm Opt}, C)$, consists of:

1. A **linear objective function** $f: \mathbb{R}^n \to \mathbb{R}$, given by:
   
    $$
    f(x_1, \cdots, x_n) = c_1x_1 + c_2x_2 + \cdots + c_nx_n + d
    $$
    
    where we assume the coefficients $c_i$ and constant $d$ are rational numbers.
    
2. An **optimization criterion**: ${\rm Opt} \in \text{\{Maximize, Minimize\}}$.
3. A set (or system) $C(x_1, \cdots, x_n)$ of $m$ **linear constraints**, or **linear inequalities/equalities**, $C_i(x_1, \cdots, x_n), i = 1, \cdots, m$, where $C_i(x)$ has form:
   
    $$
    a_{i, 1} x_1 + a_{i, 2} x_2 + \cdots + a_{i, n} x_n\ \Delta\ b_i
    $$
    
    where $\Delta \in \{\leq, \geq, =\}$, and where $a_{i, j}$’s and $b_i$’s are rational numbers.
    

**Note**:

1. $v = (v_1, \cdots, v_n) \in \mathbb{R}^n$ **satisfies** $C_i(x)$ if plugging in $v$ for the variables $x = (x_1, \cdots, x_n)$, the constraint $C_i(v)$ holds true.
2. $v\in \mathbb{R}^n$ is called a solution to a system $C(x)$, if $v$ satisfies every constraint $C_i \in C$.
3. Let $K(C) \subseteq \mathbb{R}^n$ denote the set of all solutions to the system $C(x)$. We say $C$ is **feasible** if $K(C)$ is not empty.

**Statement**:

The following three possible “answers” to an LP problem do cover all possibilities.

1. The problem is Infeasible.
2. The problem is Feasible but Unbounded.
3. An Optimal Feasible Solution (OFS) exists.
    1. One such optimal solution is $x^{\ast} \in \mathbb{R}^n$
    2. The optimal objective values if $f(x^{\ast}) \in \mathbb{R}$.

### Simplified forms for LP problems

1. In principle, we need only consider Maximization, because:
   
    $$
    \min_{x\in K}f(x) = -\max_{x\in K} -f(x)
    $$
    
    (either side is unbounded if and only if both are.)
    
2. We only need an objective function $f(x_1, \cdots, x_n) = x_i$, for some $x_i$, because we can:
   
    Introduce new variable $x_0$. Add new constraint $f(x) = x_0$ to constraints $C$. Make the new objective “Optimize $x_0$”.
    
3. Don’t need “$=$” constraints: $\alpha = \beta \Leftrightarrow (\alpha \leq \beta \wedge \alpha \geq \beta)$.
4. Don’t need “$\alpha \geq \beta$”, where $\beta \in \mathbb{R}: \alpha \geq \beta \Leftrightarrow -\alpha \leq - \beta$.
5. We can constrain every variable $x_i$ to be $x_i \geq 0$:
   
    Introduce two variables $x^+_i, x_i^-$ for each variable $x_i$. Replace each occurence of $x_i$ by $(x_i^+, x_i^-)$, and add the constraints $x_i^+\geq 0, x_i^-\geq 0$.
    
    (N.B. can’t do both (2.) and (5.) together.)
    

## Lecture 6 The Simplex Algorithm

[***Simplex Algorithm - oi-wiki***](https://oi-wiki.org/math/simplex/)

## Lecture 7 LP Duality

### Solving LPs against an Adversary

Suppose you want to optimize this Primal LP:

**Maximize** $c^{\rm T} x$

**Subject to**:

$$
\begin{align*}&Ax \leq b\\ &x_1, \cdots, x_n \geq 0 \end{align*}
$$

Suppose an “Adversary” comes along with a $m$-vector $y\in \mathbb{R}^m, y \geq 0$, such that: $c^{\rm T} \leq y^{\rm T} A$.

For any solution, $x$, you may have for the Primal:

$$
\begin{align*} c^{\rm T}x &\leq (y^{\rm T}A) x &\text{ (because } x \geq 0 \text{\ \& \ } c^{\rm T} \leq y^{\rm T} A) \\ &= y^{\rm T}(Ax) \\ &\leq y^{\rm T}b &\text{ (because } y^{\rm T} \geq 0 \text{\ \&\ } Ax \leq b)\end{align*}
$$

So, the adversary’s goal is to minimize $y^{\rm T}b$, subject to $c^{\rm T} \leq y^{\rm T}A$, i.e., optimize the **Dual LP**.

### The LP Duality Theorem

**Proposition**: (Weak Duality)

$$
c^{\rm T} x^{\ast} \leq b^{\rm T}y^{\ast}
$$

**Theorem**: (Strong Duality, von Neumann’47) One of the following for situations holds:

1. Both the primal and dual LPs are feasible, and for any optimal solutions $x^{\ast}$ of the primal and $y^{\ast}$ of the dual:
   
    $$
    c^{\rm T} x^{\ast} = b^{\rm T}y^{\ast}
    $$
    
2. The primal is infeasible and the dual is unbounded.
3. The primal is unbounded and the dual is infeasible.
4. Both LPs are infeasible.

### Useful Corollary of LP Duality

Solutions $x^{\ast}$ and $y^{\ast}$ to the primal and dual LPs, respectively, are both optimal if and only if the following hold:

1. For each primal constraint, $(Ax)_i \leq b_i$, $i = 1, \cdots, m$, either $(Ax^{\ast})_i = b_i$ or $y_i^{\ast} = 0$ (or both).
2. For each dual constraint, $(A^{\rm T}y)_j \geq c_j$, $j = 1, \cdots, n$, either $(A^{\rm T}y^{\ast}) = c_j$ or $x^{\ast}_j = 0$ (or both).

**Proof**: By weak duality

$$
c^{\rm T}x^{\ast} \leq ((y^{\ast})^{\rm T}A)x^{\ast} = (y^{\ast})^{\rm T}(Ax^{\ast}) \leq (y^{\ast})^{\rm T}b
$$

By strong duality each inequality holds with equality precisely when $x^{\ast}$ and $y^{\ast}$ are optimal. So, when optimal,

$$
(((y^{\ast})^{\rm T}A - c^{\rm T})x^{\ast} = 0
$$

Since both $(((y^{\ast})^{\rm T}A -  c^{\rm T}) \geq 0$ and $x^{\ast} \geq 0$, it must be that for each $j = 1, \cdots, n$, $(A^{\rm T}y^{\ast})_j = c_j$ or $x^{\ast}_j = 0$.

Likewise, when optimal, $(y^{\ast})^{\rm T}(b - Ax^{\ast}) = 0$, and thus, for each $i = 1, \cdots, m$, $(Ax^{\ast})_i = b_i$ or $y_i^{\ast} = 0$.

### General Recipe for LP Duals

If the primal is:

**Maximize** $c^{\rm T} x$

**Subject to**:

$$
\begin{align*} & (Ax)_i \leq b_i, i = 1, \cdots, d,\\& (Ax)_i = b_i, i = d + 1, \cdots, m,\\& x_1, \cdots, x_r \geq 0 \end{align*}
$$

Then the dual is:

**Minimize** $b^{\rm T}y$

**Subject to**:

$$
\begin{align*} & (A^{\rm T}y)_i \geq c_i, i = 1, \cdots, r,\\& (A^{\rm T}y)_i = c_i, i = r + 1, \cdots, n,\\& y_1, \cdots, y_d \geq 0 \end{align*}
$$

### Duality and the Minimax Theorem

Recall the LP for solving Minimax for Player 1 in a zero-sum game given by matrix $A$:

**Maximize** $v$

**Subject to**:

$$
\begin{align*} & v - (x^{\rm T}A)_j \leq 0, \text{ for } j = 1, \cdots, m_2,\\& x_1 + \cdots + x_{m_1} = 1 \\& x_1 \geq 0 \text{ for } j = 1, \cdots, m_1.\end{align*}
$$

Dual to this LP:

**Minimize** $u$

**Subject to**:

$$
\begin{align*} & u - (Ay)_i \geq 0, \text{ for } i = 1, \cdots, m_i,\\& y_1 + \cdots + y_{m_2} = 1 \\& y_j \geq 0 \text{ for } j = 1, \cdots, m_2. \end{align*}
$$

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

**Proposition** In an $n$-player game, a profile $x^{\ast}$ is a Nash Equilibrium if and only if there exists $w_1, \cdots, w_n \in \mathbb{R}$, such that the following hold:

1. For all players $i$, and every $\pi_{i, j}\in support(x_i^{\ast})$, $U_i(x_{-i}^{\ast}; \pi_{i, j}) = w_i$, and 
2. For all players $i$, and every $\pi_{i, j} \notin support(x_i^{\ast})$, $U_i(x_{-i}^{\ast}; \pi_{i, j}) \leq w_i$.

**Note**: such $w_i$’ necessarily satisfy $w_i = U_i(x^{\ast}).$

## Lecture 9 Computing Solutions for General Strategic Games: Part II: Nash Equilibria

## Lecture 10 Games in Extensive Form

Players making “moves” to which other players react with “moves”.

### Tree: a formal definition

Actually, the tree here can be regarded as a **state-transformation machine**.

1. Let $\Sigma = \{a_1, a_2, \cdots, a_k\}$ be an **alphabet**. A **tree** over $\Sigma$ is a set $T \subseteq \Sigma^{\ast}$ of nodes $w \in \Sigma^{\ast}$ such that: if $w = w'a \in T$, then $w'\in T$. (i.e. it is a prefix closed subset of $\Sigma^{\ast}$.)
2. For a node $w \in T$, the **children** of $w$ are $ch(w) = \{w'\in T | w' = wa, \text{for some } a\in \Sigma\}$. For $w \in T$, let $Act(w) = \{a\in \Sigma | wa\in T\}$ be “**actions**” available at $w$.
3. A leaf (or terminal) node $w \in T$ is one where $ch(w) = \empty$. Let $L_T = \{w\in T| w \text{ a leaf} \}$.
4. A (finite or infinite) path $\pi$ in $T$ is sequence $\pi = w_0, w_1, w_2, \cdots$ of nodes $w_i\in T$, where if $w_{i + 1} \in T$ then $w_{i + 1} = w_ia$, for some $a \in \Sigma$. It is a **complete path (or play)** if $w_0 = \epsilon$ and every non-leaf node in $\pi$ has a child in $\pi$. Let $\Psi_{T}$ denote the **set of** **plays** of $T$.

### Game in Extensive form

A game in extensive form $\mathcal{G}$ consists of:

1. A set $N = \{1, \cdots, n\}$ of players.
2. A tree $T$, called the game tree, over some $\Sigma$.
3. A partition of the tree nodes $T$ into disjoint sets $Pl_0, Pl_1, \cdots, Pl_n$, such that $T = \bigcup_{i = 0}^n Pl_i$. Where $Pl_i,i\geq 1$, **denotes the nodes of player $i$, where it is player $i$’s turn to move.** (And $Pl_0$ denotes the “chance” / “nature” nodes.)
4. For each “**nature**” node, $w \in Pl_0$, a probability distribution $q_w: Act(w) \to \mathbb{R}$ over its actions: $q_w(a) \geq 0, \sum_{a\in Act(w)}q_w(a) = 1$. (That is $Act(w)$ denotes a probability.)
5. For each player $i \geq 1$, a partition of $Pl_i$ into disjoint non-empty **information sets** $\textit{Info}_{i, 1}, \cdots, \textit{Info}_{i, r_i}$, such that $Pl_i = \bigcup_{j = 0}^{r_i} \it{Info}_{i, j}$. Moreover, for any $i, j,$ and & all nodes $w, w' \in \it Info_{i, j}$, $Act(w) = Act(w')$. (i.e., **the set of possible “actions” from all nodes in one information set is the same.**) (Normal node with only one element can also make up a information set.)
6. For each player $i$, a function $u_i: \Psi_T \to \mathbb{R}$, from (complete) plays to the payoff for player $i$. (p.s. it is for infinite. for finite game it can be $u_i: L_t \to \mathbb{R}$).

**Definition** An extensive form game $\mathcal{G}$ is called a game of **perfect information**, if every information set $\it Info_{i, j}$ contains only 1 node.

### Pure Strategies

A pure strategy $s_i$ for player $i$ in an extensive game $\mathcal G$ is a function $s_i: Pl_i \to \Sigma$ (i.e., $s_i$ is a letter in the alphabet.) that assigns actions to each of player $i$’s nodes,  such that $s_i(w) \in Act(w), w\in Pl_i$, and such that if $w, w' \in \it Info_{i, j}$, then $s_i(w) = s_i(w')$.

Let $S_i$ be the set of pure strategies for player $i$.

1. No Chance: Given pure profiles $s = (s_1, \cdots, s_n)\in S_1\times\cdots\times S_n$, if there are no chance nodes (i.e., $Pl_0 = \empty$) then $s$ uniquely determines a play $\pi_s$ of the game: players move according their strategies:
    1. $\text {Initialize}$ $j:= 0$, $\text {and}$ $w_0 := \epsilon$;
    2. $\text{While}$ ($w_j$ $\text {is not at a terminal node}$)
       
        $\quad \quad \text{If } w_j \in Pl_i$, $\text{then } w_{j + 1}:= w_js_i(w_j)$;
        
        $\quad \quad j:= j + 1$
        
    3. $\pi_s = w_0, w_1, \cdots$
2. With Chance: If there are chance nodes, then $s\in S$ determines a probability distribution over plays $\pi$ of the game.
   
    For finite extensive games, where $T$ is finite, we can calculate the probability $p_s(\pi)$ of play $\pi$, using probabilities $q_w(a)$:
    
    Suppose $\pi = w_0, \cdots, w_m$, is a play of $T$. Suppose further that for each $j < m$, if $w_j \in Pl_i$, then $w_{j + 1} = w_js_i(w_j)$. Otherwise, let $p_s(\pi) = 0$.
    
    Let $w_{j_1} \cdots, w_{j_r}$ be the chance nodes in $\pi$, and suppose, for each $k = 1, \cdots, r, w_{j_k + 1} = w_{j_k} a_{j_k}$, i.e., the required action to get from node $w_{j_k}$ to $w_{j_k + 1}$ is $a_{j_k}$. Then
    
    $$
    p_s(\pi) := \prod_{k = 1}^r q_{w_{j_k}}(a_{j_k})
    $$
    

### Chance and Expected Payoffs

Expected payoff for player $i$ under $s$ as:

$$
h_i(s):= \sum_{\pi\in \Psi_T}p_s(\pi)\cdot u_i(\pi)
$$

### Imperfect Information & Perfect Recall

1. An extensive form game (EFG) is a game of imperfect information if it has non-trivial (size > 1) information sets. **Players don’t have full knowledge of the current “state” (current node of the game tree).**
2. Informally, an imperfect information EFG has perfect recall if each player $i$ never forgets its own sequence of prior actions and information sets. I.e., a EFG has perfect recall if whenever $w, w' \in \it Info_{i, j}$ belong to the same information set, then the “visible history” for player $i$ (sequence of information sets and actions of player $i$ during the play) prior to hitting node $w$ and $w'$ must be exactly the same.

### Subgames and (Subgame) Perfection

A **subgame** of an extensive form game is any subtree of the game tree which has self-contained information sets. (i.e., **every node in that subtree must be contained in an information sets that itself entirely contained in that subtree. Moreover, subtree $\neq$ subgame.**)

For an extensive form game $\mathcal G$, a profile of **behavior** strategies $b = (b_1, \cdots, b_n)$ for the players is called a **subgame perfect equilibrium (SGPE)** if it **defines a NE** **for every subgame** of $\mathcal G$.

## Lecture 11 Games of Perfect Information

### Finite games of perfect information

A perfect information (PI) game: 1 node per information set.

**Theorem ([Kuhn’53])** Every **finite $n$-person extensive PI-game**, $\mathcal{G}$, has a NE, in fact, a subgame-perfect NE (SPNE), in pure strategies. I.e., some pure profile, $s^{\ast} = (s_1^{\ast}, \cdots, s^{\ast}_n)$, is a SPNE.

**Proof** We prove by induction on the depth of a subgame $\mathcal G_w$ that it has a pure SPNE, $s^w = (s_1^w, \cdots, s_n^w)$. Then $s^{\ast}:=s^{\epsilon}$.

Base case, depth 0: In this case we are at a leaf $w$. There is nothing to show: each player $i$ gets payoff $u_i(w)$, and the strategies in the SPNE $s^{\ast}$ are empty.

Inductive step: Suppose depth of $\mathcal{G}_w$ is $k + 1$. Let $Act(w) = \{a'_1, \cdots, a'_r\}$ be the set of actions available at the root of $\mathcal{G}_w$. The subtrees $T_{wa_j'}$, for $j = 1, \cdots, r$, each define a PI-subgame $\mathcal{G}_{wa_j'}$, of depth $\leq k$.

Thus, by induction, each game $\mathcal{G}_{wa_j'}$ has a pure strategy SPNE, $s^{wa'_j} = (s_1^{wa_j'}, \cdots, s_n^{wa_j'})$.

To define $s^w = (s_1^w, \cdots, s^w_n)$, there are two cases to consider

1. $w \in Pl_0$, i.e., the root node, $w$, of $T_w$ is a chance node (belongs to “nature”).
   
    Let the strategy $s_i^w$ for player $i$ be just the obvious “union” $\bigcup_{a'\in Act(w)}s_i^{wa'}$, of its pure strategies in each of the subgames. (Note that $Act(w)$ denotes probability sets here.)
    
    Claim: $s^w = (s_1^w, \cdots, s_n^w)$ must be a pure SPNE of $\mathcal{G}_w$ (depth $k + 1$). 
    
    Suppose not. Then some player $i$ could improve its expected payoff by switching to a different pure strategy in one of the subgames. But that violates the inductive hypothesis on that subgame. 
    
2. $w \in Pl_i, i > 0$: the root, $w$, of $T_w$ belongs to player $i$. For $a \in Act(w)$, let $h_i^{wa}(s^{wa})$ be the expected payoff to player $i$ in the subgame $\mathcal{G}_{wa}$. Let $a' = \argmax_{a\in Act(w)}h_i^{wa}(s^{wa})$. For player $i' \neq i$, define $s_{i'}^w = (\bigcup_{a\in Act(w)}s_{i'}^{wa})$.
   
    For $i$, define $s_i^{w} = (\bigcup_{a\in Act(w)}s_i^{wa}) \cup \{w\to a'\}$. 
    
    Claim: $s^w = (s_1^w, \cdots, s_n^w)$ is a pure SPNE of $\mathcal{G}_w$. $\quad \text{Q.E.D}$ 
    

### Algorithm for computing a SPNE in finite PI-games

The proof yields an EASY “bottom up” algorithm for computing a pure SPNE in a finite PI-game.

### Consequences for zero-sum finite PI-games

**Definition** A finite zero-sum game $\Gamma$ is determined, if 

$$
\max_{s_1\in S_1}\min_{s_2\in S_2}u(s_1, s_2) = \min_{s_2\in S_2}\max_{s_1\in S_1}u(s_1, s_2)
$$

(Note that $s_1$ and $s_2$ are both pure strategy.)

**Proposition** ([Zermelo’1912]) Every finite zero-sum PI-game, $\mathcal{G}$, is determined. Moreover, the value & a pure minimax profile can be computed “efficiently” from $\mathcal{G}$.

### Minimax search with $\alpha$-$\beta$-pruning

### Let’s generalize to infinite zero-sum PI-games

For infinite games $\max \& \min$ may not exist! Instead, we call an (infinite) zero-sum game determined if:

$$
\sup_{s_1\in S_1}\inf_{s_2\in S_2} u(s_1, s_2) = \inf_{s_2\in S_2}\sup_{s_1\in S_1} u(s_1, s_2)
$$

($\sup$, i.e., supremum denotes least upper bound, and $\inf$, i.e., infimum denotes greatest lower bound.) A strategy $s^{\ast}_1 \in S_1$ such that for any $s_2 \in S_2$, $u(s^{\ast}_1, s_2) = 1$ (and vice versa for player 2). 

**Not every win-lose PI-game determined.**

### Determinacy and its boundaries

For win-lose PI-games, we can define the payoff function by providing the set $Y = u_1^{-1}(1) \subseteq \Psi_T$, of complete plays on which player 1 wins (player 2 necessarily wins on all other plays).

## Lecture 12 Games on Graphs

### Game graphs and their trees

A 2-player game graph, $G = (V, E, pl)$ consists of:

- A (finite) set $V$ of vertices.
- A set $E \subseteq V\times V$ of edges.
- A partition $(V_1, V_2)$ of the vertices $V = V_1 \cup V_2$ into two disjoint sets belonging to players 1 and 2, respectively.

A game graph $G$ together with a start vertex $v_0 \in V$, defines a game tree $T_{v_0}$ given by:

- Action alphabet $\Sigma = V$. Thus $T_{v_0} \subseteq V^{\ast}$.
- $\epsilon \in T_{v_0}$, and $wv'' \in T_{v_0}$, for $v'' \in V$, if and only if
    - $w = \epsilon$ and $(v_0, v'') \in E$, or
    - $w = w'v'$, for some $v'\in V$, and $(v', v'')\in E$.
    
    **(If last vertex of any node $w$ is $v'$, it have action $v''$ if and only if $(v', v'')\in E$.)**
    

### Games on graphs

A game on graph, $\mathcal{G}_{v_0}$, is given by:

A finite game graph $G$, vertex $v_0\in V$, and payoff function $u: \Psi_{T_{v_0}} \to \mathbb{R}$.

### History Oblivious Payoff

Let’s call payoff function $u()$ history oblivious (h.o.), if for all infinite plays $\pi\ \&\ \pi'$, if $\inf(\pi) = \inf(\pi')$, then $u(\pi) = u(\pi')$, and for all finite complete plays $wv$ and $w'v$, 

$$
u(wv) = u(w'v)
$$

Call a graph game h.o. if its payoffs are h.o. . $**w$ and $w'$ represent histories here.**

### Finitistic payoffs

Let’s call an h.o. payoff function finitistic if for **all infinite plays** $\pi$ and $\pi'$, $u(\pi) = u(\pi')$. Let’s call game on a graph $\mathcal{G}_{v_0}$ finitistic if its payoff function is. 

So, in win-lose-draw finitistic games, infinite plays are either all wins, all losses, or all draws, for player 1.

Therefore, all finitistic games on graphs determined.

### Memoryless strategies and determinacy

Definition For a game $\mathcal{G}_{v_0}$, a strategy $s_i$ for player $i$ is memoryless strategy if for all $wv, w'v \in Pl'_i$, $s_i(wv) = s_i(w'v)$, and if $wv_0\in Pl_i'$ then $s_i(wv_0) = s_i(\epsilon)$. I.e., the strategy always makes the same move from vertex, regardless of the history of how it got there.

Let $MLS_i$ denote the set of memoryless strategies for player $i$. $MLS_i$ is a finite set, even if $S_i$ is not.

**Definition** $\mathcal{G}_{v_0}$ is memorylessly determined if both players have memoryless strategies that achieve “the value”. I.e.,

$$
\max_{s_1\in MSL_1}\inf_{s_2\in S_2} u(s_1, s_2) = \min_{s_2\in MLS_2}\sup_{s_1\in S_1} u(s_1, s_2)
$$

**Theorem A** Finitistic games on finite graphs are memorylessly determined. Moreover, there is an efficient (P-time) algorithm to compute memoryless value-achieving strategies in such game.

## Lecture 15 A brief taster of Markov Decision Processes and Stochastic Games

## Lecture 16 Selfish Network Routing, Congestion Games, and the Price of Anarchy

## Lecture 17 A first look at Auctions and Mechanism Design:
Auctions as Games, Bayesian Games, Vickrey auctions

### Auction as games

### Vickrey Acutions

### Bayesian Games

## Lecture 18 Auctions and Mechanism Design II: a little social choice theory, the VCG Mechanism, and Market Equilibria
