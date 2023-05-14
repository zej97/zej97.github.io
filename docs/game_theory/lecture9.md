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