---
layout: default
title: Lecture 5 Introduction to Linear Programming
parent: Game Theory
nav_order: 4
---

## Lecture 5 Introduction to Linear Programming

### Definition of LR

**Definition**: A Linear Programming or Linear Optimization problem instance  $(f, {\rm Opt}, C)$, consists of:

1. A **linear objective function** $f: \mathbb{R}^n \mapsto \mathbb{R}$, given by:
    
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
4. An optimal solution, for $\text{Opt = Maximize}$, is some $x^\ast \in K(C)$ such that 
    $$
    f(x^\ast) = \max_{x\in K(C)}f(x)
    $$

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
    
    Introduce two variables $x^+_i, x_i^-$ for each variable $x_i$. Replace each occurrence of $x_i$ by $(x_i^+ - x_i^-)$, and add the constraints $x_i^+\geq 0, x_i^-\geq 0$.
    
    (N.B. can’t do both (2.) and (5.) together.)

### Fourier-Motzkin Elimination

[Wiki: Fourier-Motzkin Elimination Example](https://en.wikipedia.org/wiki/Fourier%E2%80%93Motzkin_elimination#Example)

$\mathbf{Input}$: LP instance $(x_0, \text{Opt}, C(x_0, x_1, \cdots, x_n))$.

1. $\mathbf{For}$  $i = n\text{ downto } 1$
    1. Rewrite each constraint involving $x_i$ as $\alpha \le x_i$, or as $x_i \le \beta$. (One of the two is possible.) Let these be:
        
        $$
        \alpha_1 \le x_i, \cdots, \alpha_k \le x_i; x_i \le \beta_1, \cdots, x_i \le \beta_r
        $$
        
        (Retain these constraints, $H_i$, for later.)
        
    2. Remove $H_i$, i.e., all constraints involving $x_i$. Replace with constraints:
        
        $$
        \lbrace \alpha_j \le \beta_I \mid j = 1, \cdots, k, \&\ I = 1, \cdots, r\rbrace
        $$
        
2. Only $x_0$ (or non variable) remains. All constraints have the forms $\alpha_j \le x_0, x_0 \le \beta_I$, or $\alpha_j \le \beta_I$, where $a_j$’s and $b_I$’s are constants. It’s easy to check “feasibility” & “boundedness” for such a one(or zero)-variable LP, and to find an optimal $x^\ast_0$ if one exists.
3. Once you have $x^\ast_0$, plug it into $H_1$. Solve for $x_1^\ast$. Then use $x_0^\ast, x^\ast_1$ in $H_2$ to solve for $x^\ast_2, \cdots$, use $x^\ast_0, \cdots, x^\ast_{i - 1}$ in $H_i$ to solve for $x^\ast_i, \cdots$, then $x^\ast = (x^\ast_0, \cdots, x^\ast_n)$ is an optimal feasible solution.

### Remarks

IN the worst case, if every variable $x_i$ is involved in every constraint, each iteration of the "For loop" squares the number of constraints.

**Gaussian Elimination** is much nicer and does not suffer from this explosion.

**Corollary 1**: The three possible "answers" to an LP problem do cover all possibilities.

**Corollary 2**: If an LP has an OFS, then it has a rational OFS, $x^\ast$, and $f(x^\ast)$ is also rational.

Although Fourier-Motzkin Elimination is bad in the worst case, it can still be quite useful. It can be used to remove redundant variables and constraints. And its worst-case behavior may in some cases not arise in practice.

