---
layout: default
title: Lecture 16 Selfish Network Routing, Congestion Games, and the Price of Anarchy
parent: Game Theory
nav_order: 12
---

## Lecture 16 Selfish Network Routing, Congestion Games, and the Price of Anarchy

### (Selfish) Network Routing as a Game

### Congestion Games

A Congestion Game, 

$$G = (N, R, (Z_i)_{i\in N}, (d_r)_{r\in R})$$

 has: 

- A finite set $N = \lbrace 1, \cdots, n\rbrace $ of **players**.
- A finite set of $R = \lbrace 1, \cdots, m\rbrace $ of **resources**, (could be **edges**).
- For each player, $i$, a set $Z_i \subseteq 2^{R}$, of admissible strategies for player $i$. So a pure strategy $s_i\in Z_i$ is **a set of resources (edges)**.
- Each resource $r \in R$ has a **cost function**: $d_r: \mathbb{N} \to \mathbb{Z}$. Intuitively, $d_r(j)$ is the cost of using resource $r$ if there are $j$ agents simultaneously using $r$.
- For a pure strategy profile $s = (s_1, \cdots, s_n) \in Z_1 \times \cdots \times Z_n$, the **congestion** (how many agents) on resource $r$ is: $n_r(s) = \lvert\lbrace i\mid r\in s_i\rbrace \rvert$. I.e., if agent $i$ has resource $r$, then $n_r(s_i) = \lvert \lbrace i\rbrace  \rvert = 1$.
- Under strategy profiles $s = (s_1, \cdots, s_n)$, the **total cost** to player $i$ is
    
    $$
    C_i(s) \doteq \sum_{r\in s_i}d_r(n_r(s))
    $$
    
    Every player $i$ wants to **minimize** its own (expected) cost.
    

### Best response dynamics and pure Nash Equilibria

In a **congestion game** $G$, for any pure strategy profile $$s = (s_1, \cdots, s_n)$$, suppose that some player $i$ has a better alternative strategy, $$s'_i\in Z_i$$, such that $$C_i(s_{-i}; s_i') < C_i(s)$$.

Player $i$ can switch (unilaterally) from $s_i$ to $s_i'$. This takes us from profile perform a sequence of such **(strict) improvement steps**.

**Theorem**: ([Rosenthal’73]) In any congestion game, every sequence of strict improvement steps is necessarily finite, and terminates in a **pure NE**. 

Thus, in particular, every congestion game has a pure strategy NE.

**Proof**: Consider the following **potential function** (from potential energy):

$$
\varphi(s) \doteq \sum_{r\in R}\sum_{j=1}^{n_r(s)}d_r(j)
$$

This function computes the **total cost or benefit of the players' choices in the game**. Sometimes called the **social cost function**. the Let $s' := (s_{-i}; s_i')$.

**Claim**: $\varphi(s) - \varphi(s') = C_i(s) - C_i(s')$. 

For $i'\in \lbrace 1, \cdots, n \rbrace$, define

$$
n_r^{(i')}(s) = \lvert \lbrace i \mid r\in  s_i \wedge  i \in \lbrace 1, \cdots, i'\rbrace  \rbrace  \rvert
$$

By exchanging the order of summation in equation $(1)$ for 

$$
\varphi(s) = \sum_{i=1}^n\sum_{r\in s_i} d_r(n^{(i)}_r(s))
$$. 

Now note that $n^{(n)}_r(s) = n_r(s)$. Thus

$$
\sum_{r\in s_n}d_r(n^{(n)}_r(s)) = \sum_{r\in s_n}d_r(n_r(s)) = C_n(s)
$$

So, if player $n$ switches from strategy $s_n$ to $s_n'$, leading us from profile $s$ to $s'$, then $\varphi(s) - \varphi(s') = C_i(s) - C_i(s')$. 

$n_r(s)$ is the total congestion on resource $r$. The formula $\sum_{j=1}^{n_r(s)}$ doesn’t need have a intuitively explanation. This constructed formula represents a sense of potential which is quite like the gravitational potential energy.

The claim shows that $\varphi$ is a so-called **exact potential**, i.e., if a single player decreases its latency by a value of $\Delta > 0$, then $\varphi$ decreases by exactly the same amount.

**Continue to proof**: Observe that every strict improvement step must decreases the value of the potential function $\varphi(s)$ by at least $1$ (the costs $d_r(s)$ are all integers). Furthermore, there are only finitely many pure strategies $s$, so there are finite integers:

$a = \min_s\varphi(s)$ and $b = \max_s\varphi(s)$. Thus, every improvement sequence is finite.

Finally, note that the last profile $s$ in any improvement sequence which can not be further improved is, by definition, a pure Nash equilibrium.

### A flow network game

### Braess’s paradox

Add one more road, but it will cause a 15-minute delay.

### Social welfare and the price of anarchy

[Price of anarchy in auctions](https://en.wikipedia.org/wiki/Price_of_anarchy_in_auctions): The Price of Anarchy (PoA) measures how the social welfare of a system **degrades** due to selfish behavior of its agents. 

Recall that in a strategic game $\Gamma$, “utilitarian social welfare”, ${\rm welfare}(x)$, under a particular profile of mixed strategies $x\in X$, is defined as ${\rm welfare(x)}:= \sum_{i=1}^n U_i(x)$. For a game $\Gamma$, let ${\rm NE}(\Gamma)$ be the set of NE’s of $\Gamma$.

For our next definition suppose ${\rm welfare}(x) > 0$ for all $x\in X$. 

One approach to maximizing the social welfare is designing a truthful mechanism. In such a mechanism, each agent is incentivized to report his true valuations to the items. Then, the auctioneer can calculate and implement an allocation that maximizes the sum of values. An example to such a mechanism is the VCG auctions.

A version of “the price of anarchy” can be defined as **the ratio between the optimal social welfare and the social welfare in the worst equilibrium (where does the social welfare degrade to)**: ([Koutsoupias-Papadimitriou98])

$$
{\rm PoA}(\Gamma) := \frac{\max_{x\in X}{\rm welfare}(x)}{\min_{x\in {\rm NE}(\Gamma)}{\rm welfare}(x)}
$$

**Note**: this ratio is $\geq 1$ and larger means “worse”.

### Pure price of anarchy

In some settings, such as congestion games, where we know that a pure equilibrium exists, it is sometimes more sensible to compare the best overall outcome to the worst pure-NE outcome.

Let pure-${\rm NE}(\Gamma)$ denote the set of pure NEs in the game $\Gamma$. For settings (such as congestion games) where we know pure-${\rm NE}(\Gamma)$ is non-empty, we define “the pure price of anarchy” as:

$$
\text{pure-PoA}(\Gamma) := \frac{\max_{s\in S}{\rm welfare}(s)}{\min_{s\in\text{pure-}{\rm NE}(\Gamma)(\Gamma)}{\rm welfare}(s)}
$$