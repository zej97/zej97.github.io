---
layout: default
title: Lecture 11 Games of Perfect Information
parent: Game Theory
nav_order: 10
---

## Lecture 11 Games of Perfect Information

### Finite games of perfect information

A perfect information (PI) game: 1 node per information set.

**Theorem ([Kuhn’53])** Every **finite $n$-person extensive PI-game**, $\mathcal{G}$, has a NE, in fact, a subgame-perfect NE (SPNE), in pure strategies. I.e., some **pure** profile, $s^\ast = (s_1^\ast, \cdots, s^\ast_n)$, is a SPNE.

**Proof** We prove by induction on the depth of a subgame $\mathcal G_w$ that it has a pure SPNE, $s^w = (s_1^w, \cdots, s_n^w)$. Then $s^\ast:=s^{\epsilon}$.

Base case, depth 0: In this case we are at a leaf $w$. There is nothing to show: each player $i$ gets payoff $u_i(w)$, and the strategies in the SPNE $s^\ast$ are empty.

Inductive step: Suppose depth of $$\mathcal{G}_w$$ is $$k + 1$$. Let $$Act(w) = \lbrace a'_1, \cdots, a'_r\rbrace$$ be the set of actions available at the root of $$\mathcal{G}_w$$. The subtrees $$T_{wa_j'}$$, for $$j = 1, \cdots, r$$, each define a PI-subgame $$\mathcal{G}_{wa_j'}$$, of depth $$\leq k$$.

Thus, by induction, each game $\mathcal{G}_{wa_j'}$ has a pure strategy SPNE, $s^{wa'_j} = (s_1^{wa_j'}, \cdots, s_n^{wa_j'})$.

To define $s^w = (s_1^w, \cdots, s^w_n)$, there are two cases to consider

1. $w \in Pl_0$, i.e., the root node, $w$, of $T_w$ is a chance node (belongs to “nature”).
    
    Let the strategy $s_i^w$ for player $i$ be just the obvious “union” $\bigcup_{a'\in Act(w)}s_i^{wa'}$, of its pure strategies in each of the subgames. (Note that $Act(w)$ denotes probability sets here.)
    
    Claim: $s^w = (s_1^w, \cdots, s_n^w)$ must be a pure SPNE of $\mathcal{G}_w$ (depth $k + 1$). 
    
    Suppose not. Then some player $i$ could improve its expected payoff by switching to a different pure strategy in one of the subgames. But that violates the inductive hypothesis on that subgame. 
    
2. $w \in Pl_i, i > 0$: the root, $w$, of $T_w$ belongs to player $i$. For $a \in Act(w)$, let $$h_i^{wa}(s^{wa})$$ be the expected payoff to player $i$ in the subgame $\mathcal{G}_{wa}$. Let $$a' = \argmax_{a\in Act(w)}h_i^{wa}(s^{wa})$$. For player $$i' \neq i$$, define $$s_{i'}^w = (\bigcup_{a\in Act(w)}s_{i'}^{wa})$$.
    
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

($\sup$, i.e., supremum denotes least upper bound, and $\inf$, i.e., infimum denotes greatest lower bound.) A strategy $s^\ast_1 \in S_1$ such that for any $s_2 \in S_2$, $u(s^\ast_1, s_2) = 1$ (and vice versa for player 2). 

**Not every win-lose PI-game determined.**

### Determinacy and its boundaries

For win-lose PI-games, we can define the payoff function by providing the set $Y = u_1^{-1}(1) \subseteq \Psi_T$, of complete plays on which player 1 wins (player 2 necessarily wins on all other plays).
