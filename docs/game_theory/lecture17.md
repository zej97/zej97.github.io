---
layout: default
title: Lecture 17 A first look at Auctions and Mechanism Design
parent: Game Theory
nav_order: 13
---

## Lecture 17 A first look at Auctions and Mechanism Design: Auctions as Games, Bayesian Games, Vickrey auctions

### Auction as games

Consider one formulation of a **single-item**, **sealed-bid**, **auction** as a game:

- Each of $n$ bidders is a player.
- Each player $i$ has a **valuation**, $v_i \in R$, for the item being auctioned.
- If the outcome is: player $i$ wins the item and pays **price** $pr$ (not necessary be his valuation or bid, determined by strategy), then the **payoff** to player $i$, is
    
    $$
    u_i(\text{outcome}):=v_i - pr
    $$
    
    and all other players $j \neq i$ get payoff $0$: $u_j(\text{outcome}) := 0$.
    
- Let us require that the auctioneer must set up the rules of the auction so that they satisfy the following reasonable constraints: given (sealed) bids $(b_1, \cdots, b_n)$, one of the highest bidders must win, and must pay a price $pr$ such that $0 \leq pr \leq \max_i b_i$.
- Question: What rule should the auctioneer employ, so that for each player $i$, bidding their “true valuation” $v_i$ (i.e., letting $b_i = v_i$) is a dominant strategy.
    - Note: it is the rule compels players to bid their true valuation.

### Vickrey Acutions

A.k.a., second-price, sealed bid auction.

### Bayesian Games

A strategy profiles $s = (s_1, \cdots, s_n)$

### Bayesian Nash Equilibrium