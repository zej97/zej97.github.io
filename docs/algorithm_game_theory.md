---
title: Game Theory
layout: default
nav_order: 2
has_children: true
---
# Game Theory

<!-- ***[Notes on Notion.so: Algorithm Game Theory and its Applications](https://zej.notion.site/Algorithm-Game-Theory-and-its-Applications-6ffba454613c41fa9b9d090b16cf66b0)*** -->

The following are notes from the lecture: [CS4 Algorithmic Game Theory and Applications](https://www.inf.ed.ac.uk/teaching/courses/agta/) in UoE.

## Key Notes

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

### Useful Corollary of LP Duality

Solutions $x^*$ and $y^*$ to the primal and dual LPs, respectively, are both optimal if and only if the following hold:

1. For each primal constraint, $(Ax)_i \leq b_i$, $i = 1, \cdots, m$, either $(Ax^*)_i = b_i$ or $y_i^* = 0$ (or both).
2. For each dual constraint, $(A^{\rm T}y)_j \geq c_j$, $j = 1, \cdots, n$, either $(A^{\rm T}y^*) = c_j$ or $x^*_j = 0$ (or both).

### Dominance
Only a pure strategy can be strictly dominant.

### Computing Nash Equilibria: **a first clue**

**Proposition** In an $n$-player game, a profile $x^\ast$ is a Nash Equilibrium if and only if there exists $w_1, \cdots, w_n \in \mathbb{R}$, such that the following hold:

1. For all players $i$, and every $\pi_{i, j}\in {\rm support}(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) = w_i$, and 
2. For all players $i$, and every $\pi_{i, j} \notin {\rm support}(x_i^\ast)$, $U_i(x_{-i}^*; \pi_{i, j}) \leq w_i$.

**Note**: such $w_i$’s necessarily satisfy $w_i = U_i(x^\ast).$

### Kuhn's Theorem
**Theorem ([Kuhn’53])** Every finite $n$-person extensive PI-game, $\mathcal{G}$, has a NE, in fact, a subgame-perfect NE (SPNE), in pure strategies. I.e., some pure profile, $s^* = (s_1^*, \cdots, s^*_n)$, is a SPNE.

### History oblivious payoff

Let’s call payoff function $u()$ history oblivious (**h.o.**), if for all infinite plays $\pi\ \&\ \pi'$, if $\inf(\pi) = \inf(\pi')$, then $u(\pi) = u(\pi')$, and for all finite complete plays $wv$ and $w'v$, 

$$
u(wv) = u(w'v)
$$

Call a graph game h.o. if its payoffs are h.o.. $**w$ and $w'$ represent histories here.**

### Finitistic payoff

Let’s call an h.o. payoff function finitistic if for all infinite plays $\pi$ and $\pi'$, $u(\pi) = u(\pi')$. Let’s call game on a graph $\mathcal{G}_{v_0}$ finitistic if its payoff function is. 

### Memoryless strategies and determainacy

**Definition**: For a game $\mathcal{G}_{v_0}$, a pure strategy $s_i$ for player $i$ is **memoryless strategy** if for all $wv, w'v \in Pl'_i$, $s_i(wv) = s_i(w'v)$, and if $wv_0\in Pl_i'$ then $s_i(wv_0) = s_i(\epsilon)$. 

I.e., the strategy always makes the same move from vertex, regardless of the history of how it got there.

**Theorem A** Finitistic games on finite graphs are memorylessly determined. Moreover, there is an efficient (P-time) algorithm to compute memoryless value-achieving strategies in such game.

### The win-lose case: easy “fixed point” algorithm

We first prove the **theorem** for finitistic win-lose games via an easy bottom up fixed point algorithm.

$\text{Input}$: Game graph $G = (V, E, pl, v_0)$.

Assume w.l.o.g. all infinite plays are win for player 2 (other case is symmetric). “Dead end”: vertex with no outgoing edge.

- $\text{Good} := \lbrace v\in V \mid v \text{ a dead end that wins for player 1}\rbrace$.
- $\text{Bad}:= \lbrace v\in V \mid v \text{ a dead end that wins for player 2} \rbrace$
1. $\mathbf{Initialize}$:  $\text{Win}_1 := \text{Good}; St_1 := \emptyset$;
2. $\mathbf{Repeat}$
    1. $\text{Foreach } v\notin \text{Win}_1$:
        1. $\text{If } (pl(v) = 1 \ \&\ \exist (v, v')\in E: v'\in \text{Win}_1)$:
            
            $\text{Win}_1 := \text{Win}_1 \cup \lbrace v\rbrace; St_1 := St_1 \cup \lbrace v\mapsto v'\rbrace$;
            
        2. $\text{If } (pl(v) = 2 \ \&\ \forall (v, v')\in E: v'\in \text{Win}_1)$:
            
            $\text{Win}_1 := \text{Win}_1 \cup \lbrace v\rbrace$;
            
    
    $\mathbf{Until} \text{ The set Win}_1 \text{ does not change}$;
    

Player 1 has a winning strategy iff $v_0 \in \text{Win}_1$. If so, $St_1$ is a **memoryless winning strategy** for player 1.

### Memoryless determinacy

**Theorem** ([Condon’92]) Every simple stochastic game is memorylessly determined.

### Best response dynamics and pure NE

**Theorem**: ([Rosenthal’73]) In any congestion game, every sequence of strict improvement steps is necessarily finite, and terminates in a pure NE. 

### VCG is incentive-compatible (i.e., strategy-proof)

**Theorem ([Vickrey,1961],[Clarke,1971],[Groves,1973])** The VCG mechanism is incentive compatible (i.e., strategy proof). In other words, declaring their true valuation function $v_i$ is a (weakly) dominant strategy for all player $i$.

Proof Suppose players declare valuations $v_1', \cdots, v_n'$. Suppose player $i$’s true valuation is $v_i$. Let $c^\ast = f(v_i, v_{-i}^\ast)$, and let $c''=f(v_i', v_{-i}')$. Recall $c^\ast\in \argmax_c v_i(c) + \sum_{k\in V- \lbrace i\rbrace}v'_k(c^\ast)$ . In other words, for all $c\in C$, 

$$
v_i^\ast(c^\ast) + \sum_{k\in V-\lbrace i\rbrace}v_k'(c^\ast) \geq v_i(c) + \sum_{k\in V-\lbrace i\rbrace}v'_k(c)
$$

Thus, $u_i(c^\ast) =$ 

$$
\begin{align*}v_i(c^\ast) - p_i(c^\ast) &= v_i(c^\ast) + (\sum_{k\in V-\lbrace i\rbrace}v'_k(c^\ast)) - (\max_{c'\in C}\sum_{j\in V-\lbrace i\rbrace}v'_j(c')) \\&\geq v_i'(c'') + (\sum_{k\in V-\lbrace i\rbrace}v_k'(c'')) - (\max_{c'\in C}\sum_{j\in V-\lbrace i\rbrace}v'_j(c')) \\ &= v_i(c'') - p_i(c'') = u_i(c'') \end{align*}
$$