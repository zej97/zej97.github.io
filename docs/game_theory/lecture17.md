---
layout: default
title: Lecture 17 A first look at Auctions and Mechanism Design
parent: Game Theory
nav_order: 13
---

## Lecture 17 A first look at Auctions and Mechanism Design: Auctions as Games, Bayesian Games, Vickrey auctions

### Auction as games

Consider one formulation of a **single-item**, **sealed-bid**, **auction** as a game:

- Each of $n$ **bidders** is a player.
- Each player $i$ has a **valuation**, $v_i \in \mathbb{R}$, for the item being auctioned.
- If the outcome is: player $i$ wins the item and pays **price** ${\rm pr}$ (not necessary be his valuation or bid, determined by strategy), then the **payoff** to player $i$, is
    
    $$
    u_i(\text{outcome}):=v_i - {\rm pr}
    $$
    
    and all other players $j \neq i$ get payoff $0$: $u_j(\text{outcome}) := 0$.
    
- Let us require that the auctioneer must set up the rules of the auction so that they satisfy the following reasonable constraints: given (sealed) bids $(b_1, \cdots, b_n)$, one of the highest bidders must win, and must pay a price ${\rm pr}$ such that $0 \leq {\rm pr} \leq \max_i b_i$.
- Question: What rule should the auctioneer employ, so that for each player $i$, bidding their “**true valuation**” $v_i$ (i.e., letting $b_i = v_i$) is a dominant strategy.
    - Note: it is the rule compels players to bid their true valuation.

### Vickrey Auctions

In a Vickery auction, a.k.a., second-price, sealed bid auction, a highest bidder, $j$, whose bid is $b_j = \max_ib_i$, gets the item, but pays the **second highest** bid price: ${\rm pr} = \max_{i\neq j}b_i$.

**Claim**: Bidding their true valuation, $v_i$, i.e., letting $b_i :=  v_i$, is a (weakly) dominant strategy in this game for all players $i$.

**Note**: there is something very fishy/unsatisfactory about our formulation so far of an auction as a complete information game: player $i$ normally does not know the valuation $v_j$ of other players $j \neq i$. But if viewed as **a complete information game**, then every player knows every one else’s valuation. This is totally unrealistic. We thus need a better game-theoretic model for settings like auctions.

### Bayesian Games (Games of Incomplete Information) [Harsanyi,’67,’68]

A [**Bayesian Game**](https://en.wikipedia.org/wiki/Bayesian_game), $$G = (N, (A_i)_{i\in N}, (T_i)_{i\in N}, (u_i)_{i\in N}, p)$$, has 

- A finite set $N = \lbrace 1, \cdots, n\rbrace$  of **players**.
- A (finite) set $A_i$ of **actions** for each player $i \in N$ (or for each type). $A_{t_i} = A_i = (A_i^1, A_i^2, \cdots, A_n^{k_i})$ for all $t_i \in T_i$ and for all $i\in N$.
- A (finite) set of **possible types (or signals)**, $T_i$, for each player $i \in N$. It represents peice of private information that player $i$ knows.
- A **payoff (utility) function**, for each player $i \in N$:

    $$
    u_i: A_1\times \cdots \times A_n \times T_1 \times \cdots \times T_n \mapsto \mathbb{R}
    $$

- A **(joint) probability distribution over types**:

    $$
    p: T_1\times \cdots \times T_n\mapsto [0, 1]
    $$

    where, letting $T = T_1 \times \cdots \times T_n$, we must have:

    $$
    \sum\limits_{(t_1,\cdots, t_n) \in T} p(t_1, \cdots, t_n) = 1
    $$

    $p$ is sometimes called a **common prior**.

[Example of Bayesian game: Wiki](https://en.wikipedia.org/wiki/Bayesian_game#Example)

[Example of Bayesian game: NYU page2](https://www.eco.uc3m.es/docencia/new_juegos/en_doc/3.3%20Bayesian.pdf)

[Example of Bayesian game: Auctions](https://zej97.github.io/docs/game_theory/lecture17.html#back-to-vickrey-auctions)

### Strategies and expected payoffs in Bayesian games

- A **pure strategy** for player $i$ is a function $s_i: T_i \mapsto A_i$.
    I.e., player $i$ knows its own type, $t_i$, and chooses action $s_i(t_i)\in A_i$. 
    
- Players’ types are chosen randomly according to (joint) distribution $p$.
- Player $i$ knows $t_i\in T_i$, but doesn’t know the type $t_j$ of player $j \neq i$.
- But every player knows the joint distribution $p$, so each player $i$ can compute the conditional probabilities, $p(t_{-i}\mid t_i)$, on other player’s types, given its own type $t_i$.
- The expected payoff to player $i$, under the pure profile $s = (s_1, \cdots, s_n)$, when player $i$ has type $t_i$ (which it knows) is:

    $$
    U_i(s, t_i) = \sum_{t_{-i}} p(t_{-i}\vert t_i)u_i(s_1(t_1), \cdots, s_n(t_n), t_i, t_{-i})
    $$

### Bayesian Nash Equilibrium

**Definition**: A strategy profile $s = (s_1, \cdots, s_n)$ is a **(pure) Bayesian Nash equilibrium (BNE)** if for all player $i$ and all types $t_i \in T_i$, and all strategies $s_i^\prime$ for player $i$, we have: 

$$
U_i(s, t_i) \geq U_i((s_i^\prime;s_{-i}), t_i).
$$

**Proposition**: Every finite **Bayesian Game has a mixed strategy BNE**.

**Proof**: Follows from Nash’s Theorem. Every finite Bayesian Games can be encoded as **a finite form game of imperfect information**: the game tree first randomly choose a subtree labeled $(t_1, \cdots, t_n)$, with probability $p(t_1, \cdots, t_n)$. All nodes belonging to player $i$ in different subtrees labeled by the same type $t_i\in T_i$ are in **the same information set**.

### Back to Vickrey auctions

Now suppose we model a **sealed-bid single-item auction** using a **Bayesian game**, with some **arbitrary** prior probability distribution $p(v_1, \cdots, v_n)$ over valuations (suppose every $v_i$ is in some finite non-negative range $[0, v_{\max}]$). The **private information** of each player $i$ is $t_i := v_i$. I.e., each player $i$ knows its own valuation $v_i$, but doesn’t know the valuations $v_j$ of other players $j \neq i$.

**Proposition**: In the Vickrey (second-price, sealed-bid) auction game, with **any** prior $p$, the **truth revealing** profile of bids $v = (v_1, \cdots, v_n)$, is a weakly dominant strategy profile.

However, in first-price, sealed-bid auctions, (maximum bidder gets the item and pays ${\rm pr} = \max_ib_i$), bidding truthfully may indeed not be a dominant strategy. E.g., if player $i$ knows (with high probability) that its valuation $v_i$ is much higher than the other players’ valuations, then it may want to bid $b_i < v_i$, since it will still win the auction and pay less.

**Proposition**: If prior $p$ is a product of i.i.d. uniform distributions over some interval $[0, v_{\max}]$, then the expected revenue of the second-price and first-price sealed-bid auctions are both **the same** in their (unique) symmetric BNEs.

This is actually a special case of a much more general result in Mechanism Design called the **Revenue Equivalence Principle**. (But anyway, note that one-shot revenue maximization is **not** always a wise goal for an auctioneer.)