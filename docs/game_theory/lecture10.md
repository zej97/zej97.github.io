---
layout: default
title: Lecture 10 Games in Extensive Form
parent: Game Theory
nav_order: 9
---

## Lecture 10 Games in Extensive Form

Players making “moves” to which other players react with “moves”.

### Tree: a formal definition

Actually, the tree here can be regarded as a **state-transformation machine**.

1. Let $\Sigma = \lbrace  a_1, a_2, \cdots, a_k \rbrace$ be an **alphabet**. A **tree** over $\Sigma$ is a set $T \subseteq \Sigma^\ast$ of nodes $w \in \Sigma^\ast$ such that: if $w = w'a \in T$, then $w'\in T$. (i.e. it is a prefix closed subset of $\Sigma^\ast$.)
2. For a node $w \in T$, the **children** of $w$ are $ch(w) = \lbrace w'\in T \vert w' = wa, \text{for some } a\in \Sigma\rbrace$. For $w \in T$, let $Act(w) = \lbrace a\in \Sigma \vert wa\in T\rbrace$ be “**actions**” available at $w$.
3. A leaf (or terminal) node $w \in T$ is one where $ch(w) = \empty$. Let $L_T = \lbrace w\in T \vert w \text{ a leaf} \rbrace$.
4. A (finite or infinite) path $\pi$ in $T$ is sequence $\pi = w_0, w_1, w_2, \cdots$ of nodes $w_i\in T$, where if $w_{i + 1} \in T$ then $w_{i + 1} = w_ia$, for some $a \in \Sigma$. It is a **complete path (or play)** if $w_0 = \epsilon$ and every non-leaf node in $\pi$ has a child in $\pi$. Let $\Psi_{T}$ denote the **set of** **plays** of $T$.

### Game in Extensive form

A game in extensive form $\mathcal{G}$ consists of:

1. A set $N = \lbrace 1, \cdots, n\rbrace$ of players.
2. A tree $T$, called the game tree, over some $\Sigma$.
3. A partition of the tree nodes $T$ into disjoint sets $Pl_0, Pl_1, \cdots, Pl_n$, such that $T = \bigcup_{i = 0}^n Pl_i$. Where $Pl_i,i\geq 1$, **denotes the nodes of player $i$, where it is player $i$’s turn to move.** (And $Pl_0$ denotes the “chance” / “nature” nodes.)
4. For each “**nature**” node, $w \in Pl_0$, a probability distribution $q_w: Act(w) \to \mathbb{R}$ over its actions: $q_w(a) \geq 0, \sum_{a\in Act(w)}q_w(a) = 1$. (That is $Act(w)$ denotes a probability.)
5. For each player $i \geq 1$, a partition of $Pl_i$ into disjoint non-empty **information sets** $$\textit{Info}_{i, 1}, \cdots, \textit{Info}_{i, r_i}$$, such that $$Pl_i = \bigcup_{j = 0}^{r_i} \it{Info}_{i, j}$$. Moreover, for any $i, j,$ and & all nodes $w, w' \in \it Info_{i, j}$, $Act(w) = Act(w')$. (i.e., **the set of possible “actions” from all nodes in one information set is the same.**) (Normal node with only one element can also make up a information set.)
6. For each player $i$, a function $u_i: \Psi_T \to \mathbb{R}$, from (complete) plays to the payoff for player $i$. (p.s. it is for infinite. for finite game it can be $u_i: L_t \to \mathbb{R}$).

**Definition** An extensive form game $\mathcal{G}$ is called a game of **perfect information**, if every information set $\it Info_{i, j}$ contains only 1 node.

### Pure Strategies

A pure strategy $s_i$ for player $i$ in an extensive game $\mathcal G$ is a function $s_i: Pl_i \to \Sigma$ (i.e., $s_i$ is a letter in the alphabet.) that assigns actions to each of player $i$’s nodes,  such that $s_i(w) \in Act(w), w\in Pl_i$, and such that if $w, w' \in \it Info_{i, j}$, then $s_i(w) = s_i(w')$.

Let $S_i$ be the set of pure strategies for player $i$.

1. **No Chance**: Given pure profiles $s = (s_1, \cdots, s_n)\in S_1\times\cdots\times S_n$, if there are no chance nodes (i.e., $Pl_0 = \empty$) then $s$ uniquely determines a play $\pi_s$ of the game: players move according their strategies:
    1. $\text {Initialize}$ $j:= 0$, $\text {and}$ $w_0 := \epsilon$;
    2. $\text{While}$ ($w_j$ $\text {is not at a terminal node}$)
        
        $\quad \quad \text{If } w_j \in Pl_i$, $\text{then } w_{j + 1}:= w_js_i(w_j)$;
        
        $\quad \quad j:= j + 1$
        
    3. $\pi_s = w_0, w_1, \cdots$
2. **With Chance**: If there are chance nodes, then $s\in S$ determines a probability distribution over plays $\pi$ of the game.
    
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

For an extensive form game $\mathcal G$, a profile of **behavior** strategies $b = (b_1, \cdots, b_n)$ for the players is called a **subgame perfect equilibrium (SGPE)** if it **defines a NE** **for *EVERY* subgame** of $\mathcal G$.
