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

### First algorithm to find NE's in 2-player games

$\text{Input}$: A 2-player strategic game $\Gamma$, given by rational values $u_1(s, s')$ & $u_2(s, s')$, for all $s\in S_1$ & $s' \in S_2$. (I.e., the input is $2 \cdot m_1 \cdot m_2$ rational numbers.)

$\text{Alogrithm}$:

- For all possible ${\rm support}_1\subseteq S_1$ & ${\rm support}_2 \subseteq S_2$:
    - Check if  the corresponding LP has a feasible solution $x^\ast, w_1, \cdots, w_n$. (using, e.g., Simplex)
    - If so, STOP: the feasible solution $x^\ast$ is a Nash Equilibrium (and $w_i = U_i(x^\ast)$).

Proposition: Every finite 2-player game has a rational NE.