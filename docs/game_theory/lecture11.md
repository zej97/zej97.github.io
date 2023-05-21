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

**Definition**: For a game $\mathcal{G}$ with game tree $T$, and for $w\in T$, define the subtree $T_w \subseteq T$ ($w$ is the root node of the subtree), by: 

$$
T_w=\lbrace w^{\prime} \in T \mid w^{\prime}=w w^{\prime \prime} \text { for } w^{\prime \prime} \in \Sigma^\ast \rbrace
$$

Since tree is finite, we can just associate payoffs to the leaves. Thus, the subtree $T_w$, in an obvious way, defines a “**subgame**”, $\mathcal{G}_w$, which is also a PI-game.

The **depth** of a node $w$ in $T$ is its **length** $\lvert w \rvert$  as a string. The depth of tree $T$ is the maximum depth of any node in $T$. The depth of a game $\mathcal{G}$ is the depth of its game tree.

**Proof** We prove by induction on the depth of a subgame $\mathcal G_w$ that it has a pure SPNE, $s^w = (s_1^w, \cdots, s_n^w)$. Then $s^\ast:=s^{\epsilon}$.

Base case, depth 0: In this case we are at a leaf $w$. There is nothing to show: each player $i$ gets payoff $u_i(w)$, and the strategies in the SPNE $s^\ast$ are empty.

Inductive step: Suppose depth of $$\mathcal{G}_w$$ is $$k + 1$$. Let $$Act(w) = \lbrace a^\prime_1, \cdots, a^\prime_r\rbrace$$ be the set of actions available at the root of $$\mathcal{G}_w$$. The subtrees $$T_{wa_j^\prime}$$, for $$j = 1, \cdots, r$$, each define a PI-subgame $$\mathcal{G}_{wa_j^\prime}$$, of depth $$\leq k$$.

Thus, by induction, each game $\mathcal{G}_{wa_j^\prime}$ has a pure strategy SPNE, $s^{wa^\prime_j} = (s_1^{wa_j^\prime}, \cdots, s_n^{wa_j^\prime})$.

To define $s^w = (s_1^w, \cdots, s^w_n)$, there are two cases to consider

1. $w \in Pl_0$, i.e., the root node, $w$, of $T_w$ is a chance node (belongs to “nature”).
    
    Let the strategy $s_i^w$ for player $i$ be just the obvious “union” $\bigcup_{a^\prime\in Act(w)}s_i^{wa^\prime}$, of its pure strategies in each of the subgames. (Note that $Act(w)$ denotes probability sets here.)
    
    **Claim**: $s^w = (s_1^w, \cdots, s_n^w)$ must be a pure SPNE of $\mathcal{G}_w$ (depth $k + 1$). 
    
    Suppose not. Then some player $i$ could improve its expected payoff by switching to a different pure strategy in one of the subgames. But that violates the inductive hypothesis on that subgame. 
    
2. $w \in Pl_i, i > 0$: the root, $w$, of $T_w$ belongs to player $i$. For $a \in Act(w)$, let $$h_i^{wa}(s^{wa})$$ be the expected payoff to player $i$ in the subgame $\mathcal{G}_{wa}$. Let $$a^\prime = \argmax_{a\in Act(w)}h_i^{wa}(s^{wa})$$. For player $$i^\prime \neq i$$, define $$s_{i^\prime}^w = (\bigcup_{a\in Act(w)}s_{i^\prime}^{wa})$$.
    
    For $i$, define $s_i^{w} = (\bigcup_{a\in Act(w)}s_i^{wa}) \cup \{w\to a^\prime\}$. 
    
    Claim: $s^w = (s_1^w, \cdots, s_n^w)$ is a pure SPNE of $\mathcal{G}_w$. $\quad \text{Q.E.D}$ 
    

### Algorithm for computing a SPNE in finite PI-games

The proof yields an EASY **“bottom up”** algorithm for computing a pure SPNE in a finite PI-game.

### Consequences for zero-sum finite PI-games

Recall that, by the Minimax Theorem, for every finite zero-sum game $\Gamma$, there is a value $v^\ast$ such that for any NE $(x^\ast_1, x^\ast_2)$ of $\Gamma$, $v^\ast = U(x_1^\ast, x_2^\ast)$, and 

$$
\max _{x_1 \in X_1} \min _{x_2 \in X_2} U\left(x_1, x_2\right)=v^*=\min _{x_2 \in X_2} \max _{x_1 \in X_1} U\left(x_1, x_2\right)
$$

It follows from Kuhn’s theorem that for extensive PI-games $\mathcal{G}$ there is in fact a pure NE (in fact, SPNE) $(s^\ast_1, s^\ast_2)$ such that $v^\ast = u(s^\ast_1, s^\ast_2):= h(s^\ast_1, s^\ast_2)$, and thus that in fact

$$
\max_{s_1\in S_1}\min_{s_2\in S_2}u(s_1, s_2) = v^\ast =  \min_{s_2\in S_2}\max_{s_1\in S_1}u(s_1, s_2)
$$

(P.S., unique $v^\ast$+ useful corollary for Nash Equilibria)

**Definition** A finite zero-sum game $\Gamma$ is determined, if 

$$
\max_{s_1\in S_1}\min_{s_2\in S_2}u(s_1, s_2) = \min_{s_2\in S_2}\max_{s_1\in S_1}u(s_1, s_2)
$$

(Note that $s_1$ and $s_2$ are both pure strategy.)

**Proposition** ([Zermelo’1912]) Every finite zero-sum PI-game, $\mathcal{G}$, is determined. Moreover, the value & a pure minimax profile can be computed “efficiently” from $\mathcal{G}$.

### Chess

Chess is a finite PI-game (after 50 moves with no piece taken, it ends in a draw). In fact, it’s a **win-lose-draw PI-game**: no chance nodes possible payoffs are 1, -1 and 0.

**Proposition** ([Zermelo’1912])  In Chess, either:

1. White has a winning strategy, or
2. Black has a winning strategy, or 
3. Both players have strategies to force a draw.

A **winning strategy**, e.g., for White is a pure strategy $s^\ast_1$ that guarantees value $u(s^\ast_1, s_2) = 1$, for all $s_2$.

However, the tree is too big, and that’s why we need $\alpha$-$\beta$-pruning.

### Minimax search with $\alpha$-$\beta$-pruning

Assume, for simplicity, that players alternate moves, root belongs to Player 1 (maximizer), and 

$$
-1 \leq {\rm Eval}(w) \leq +1
$$

Score $-1$ ($+1$) means player 1 definitely loses (wins). Start the search by calling: $\mathbf{MaxVal}(w, \alpha, \beta)$;

$\mathbf{MaxVal}(w, \alpha, \beta)$

1. If $\text{depth}(w) \ge \text{MaxDepth}$ then **return** $\text{Eval}(w)$.

2. Else, for each $a\in Act(w)$

    1. $\alpha:= \max\lbrace\alpha, \mathbf{MaxVal}(wa, \alpha, \beta)\rbrace$;

    2. if $\alpha \geq \beta$, then **return** $\beta$

3. **return** $\alpha$

$\mathbf{MaxVal}(w, \alpha, \beta)$

1. If $\text{depth}(w) \ge \text{MaxDepth}$ then **return** $\text{Eval}(w)$.

2. Else, for each $a\in Act(w)$

    1. $\alpha:= \max\lbrace\alpha, \mathbf{MaxVal}(wa, \alpha, \beta)\rbrace$;

    2. if $\alpha \geq \beta$, then **return** $\alpha$

3. **return** $\beta$

### Let’s generalize to infinite zero-sum PI-games

For infinite games $\max \& \min$ may not exist! Instead, we call an (infinite) zero-sum game determined if:

$$
\sup_{s_1\in S_1}\inf_{s_2\in S_2} u(s_1, s_2) = \inf_{s_2\in S_2}\sup_{s_1\in S_1} u(s_1, s_2)
$$

In the simple setting of infinite win-lose PI-games (2 players, zero-sum, no chance nodes, and only payoffs are 1 and -1), this definition says a game is determined precisely when one player or the other has a winning strategy: a strategy $s^\ast_1 \in S_1$ such that for any $s_2\in S_2$, $u(s^\ast_1, s_2) = 1$ (and vice versa for player 2).

($\sup$, i.e., supremum denotes least upper bound, and $\inf$, i.e., infimum denotes greatest lower bound.) A strategy $s^\ast_1 \in S_1$ such that for any $s_2 \in S_2$, $u(s^\ast_1, s_2) = 1$ (and vice versa for player 2). 

**Not every win-lose PI-game determined.**

### Determinacy and its boundaries

For win-lose PI-games, we can define the payoff function by providing the set $Y = u_1^{-1}(1) \subseteq \Psi_T$, of complete plays on which player 1 wins (player 2 necessarily wins on all other plays).
