---
layout: default
title: Lecture 5 Introduction to Linear Programming
parent: Game Theory
nav_order: 4
---

## Lecture 5 Introduction to Linear Programming

### Definition of LR

**Definition**: A Linear Programming or Linear Optimization problem instance  $(f, {\rm Opt}, C)$, consists of:

1. A **linear objective function** $f: \mathbb{R}^n \to \mathbb{R}$, given by:
    
    $$
    f(x_1, \cdots, x_n) = c_1x_1 + c_2x_2 + \cdots + c_nx_n + d
    $$
    
    where we assume the coefficients $c_i$ and constant $d$ are rational numbers.
    
2. An **optimization criterion**: ${\rm Opt} \in \lbrace \text{Maximize, Minimize}\rbrace$.
3. A set (or system) $C(x_1, \cdots, x_n)$ of $m$ **linear constraints**, or **linear inequalities/equalities**, $C_i(x_1, \cdots, x_n), i = 1, \cdots, m$, where $C_i(x)$ has form:
    
    $$
    a_{i, 1} x_1 + a_{i, 2} x_2 + \cdots + a_{i, n} x_n\ \Delta\ b_i
    $$
    
    where $\Delta \in \lbrace \leq, \geq, =\rbrace$, and where $a_{i, j}$’s and $b_i$’s are rational numbers.
    

**Note**:

1. $v = (v_1, \cdots, v_n) \in \mathbb{R}^n$ **satisfies** $C_i(x)$ if plugging in $v$ for the variables $x = (x_1, \cdots, x_n)$, the constraint $C_i(v)$ holds true.
2. $v\in \mathbb{R}^n$ is called a solution to a system $C(x)$, if $v$ satisfies every constraint $C_i \in C$.
3. Let $K(C) \subseteq \mathbb{R}^n$ denote the set of all solutions to the system $C(x)$. We say $C$ is **feasible** if $K(C)$ is not empty.

**Statement**:

The following three possible “answers” to an LP problem do cover all possibilities.

1. The problem is Infeasible.
2. The problem is Feasible but Unbounded.
3. An Optimal Feasible Solution (OFS) exists.
    1. One such optimal solution is $x^\ast \in \mathbb{R}^n$
    2. The optimal objective values if $f(x^\ast) \in \mathbb{R}$.

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