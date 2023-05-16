---
layout: default
title: Lecture 12 Games on Graphs
parent: Game Theory
nav_order: 11
---
## Lecture 12 Games on Graphs

The same “position or configuration” might recur in the game, but the (infinite) game tree does not reflect this.

### Game graphs and their trees

A 2-player **game graph**, $G = (V, E, pl)$ consists of:

- A (finite) set $V$ of vertices.
- A set $E \subseteq V\times V$ of edges.
- A partition $(V_1, V_2)$ of the vertices $V = V_1 \cup V_2$ into two disjoint sets belonging to players 1 and 2, respectively.

A game graph $G$ together with a start vertex $v_0 \in V$, defines a game tree $T_{v_0}$ given by:

- Action alphabet $\Sigma = V$. Thus $T_{v_0} \subseteq V^*$.
- $\epsilon \in T_{v_0}$, and $wv'' \in T_{v_0}$, for $v'' \in V$, if and only if
    - $w = \epsilon$ and $(v_0, v'') \in E$, or
    - $w = w'v'$, for some $v'\in V$, and $(v', v'')\in E$.
    
    **(If last vertex of any node $w$ is $v'$, it have action $v''$ if and only if $(v', v'')\in E$.)**
    

### Games on graphs

A **game on graph**, $\mathcal{G}_{v_0}$, is given by:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A finite game graph $G$, vertex $v_0\in V$, and payoff function $u: \Psi_{T_{v_0}} \mapsto \mathbb{R}$.

These together define a 2-player zero-sum PI-game with game tree $T_{v_0}$.

**Note**: Finite graphs are not in general determined.

### History oblivious payoff

Suppose $\exist$ vertex $v'$ of graph $G$ that is a “dead end”. E.g., in chess this could be “checkmate for Player I”.

There may be many ways to get to $v'$, but the winner is the same for any finite play $wv' \in V^\ast$. I.e., $u(wv') = u(w'v')$, for all $wv', w'v' \in V^\ast$. So, the pay off is “**history oblivious**”.

What about for infinite plays $\pi$? We can think of $\pi$ as an infinite sequence $v_0v_1v_2\cdots$, where each $v_i \in V$. We use the notation $\pi \in V^\omega$.

For $\pi = v_0v_1v_2\cdots$, let

$$
\inf(\pi) = \lbrace v\in V \mid \text{ for }\infty\text{-many } i \in \mathbb{N}, v_i = v\rbrace 
$$

I.e., the entry of the cycle in the infinite play $\pi$.

Let’s call payoff function $u()$ history oblivious (**h.o.**), if for all infinite plays $\pi\ \&\ \pi'$, if $\inf(\pi) = \inf(\pi')$, then $u(\pi) = u(\pi')$, and for all finite complete plays $wv$ and $w'v$, 

$$
u(wv) = u(w'v)
$$

**Call a graph game h.o. if its payoffs are h.o.. $w$ and $w'$ represent histories here.**

### Finitistic payoffs

Note that in chess, if the play $\pi$ is infinite, then the play is always a draw, i.e., $u(\pi) = 0$.

Let’s call an h.o. payoff function **finitistic** if for **ALL infinite plays** $\pi$ and $\pi'$, $u(\pi) = u(\pi')$. Let’s call game on a graph $\mathcal{G}_{v_0}$ finitistic if its payoff function is. 

**So, in win-lose-draw finitistic games, infinite plays are either all wins, all losses, or all draws, for player 1.**

**Therefore, all finitistic games on graphs determined.** In fact, more it true, for finitistic games there is always a memorylessly strategy for each player that achieves the value of the game, and we can efficiently compute these strategies.

### Memoryless strategies and determinacy

**Definition**: For a game $\mathcal{G}_{v_0}$, a strategy $s_i$ for player $i$ is **memoryless strategy** if for all $wv, w'v \in Pl'_i$, $s_i(wv) = s_i(w'v)$, and if $wv_0\in Pl_i'$ then $s_i(wv_0) = s_i(\epsilon)$. 

**I.e., the strategy always makes the same move from vertex, regardless of the history of how it got there.**

Let ${\rm MLS}_i$ denote the set of memoryless strategies for player $i$. ${\rm MLS}_i$ is a finite set, even if $S_i$ is not. In particular, if $m = \lvert Pl_i\rvert$ is the number of vertices belonging to player $i$, then $\lvert {\rm MLS}_i \rvert \leq \lvert \Sigma \rvert ^m$.

**Definition**: $\mathcal{G}_{v_0}$ is **memorylessly determined** if both players have memoryless strategies that achieve “the value”. I.e.,

$$
\max_{s_1\in {\rm MLS}_1}\inf_{s_2\in S_2} u(s_1, s_2) = \min_{s_2\in {\rm MLS}_2}\sup_{s_1\in S_1} u(s_1, s_2)
$$

**Theorem A** Finitistic games on finite graphs are memorylessly determined. Moreover, there is an efficient (P-time) algorithm to compute memoryless value-achieving strategies in such game.