---
layout: default
title: Lecture 18 Auctions and Mechanism Design II
parent: Game Theory
nav_order: 14
---

## Lecture 18 Auctions and Mechanism Design II: a little social choice theory, the VCG Mechanism, and Market Equilibria

### An Exchange Economy

- $n$ agents, and $m$ **divisible goods** (commodities, services, etc).
- Each agent $i$ starts with an initial endowment of goods, $w_i = (w_{i, m}, \cdots, w_{i, m}) \in \mathbb{R}^{m}_{\geq 0}$.
- Each agent $i$ has a utility function, $u_i(x)$, that defines how much it “likes” a given bundle $x \in \mathbb{R}^m_{\geq 0}$ of goods.
    
    Assume utility functions satisfy certain “reasonable” conditions:
    
    1. ***Continuity***: It means that a small change in prices should not cause a large change in demand.
    2. ***Quasi-concavity***: In other words, quasi-concavity means that if an agent likes two bundles of goods, then they will like any bundle that lies between those two bundles.
    3. ***Non-satiation***: It means that more is always better. In other words, if a bundle of goods x gives an agent $i$ a utility of $u(x)$, then any bundle $y$ that has more of at least one good and no less of any other good than $x$ should give $i$ a higher utility than $x$.
- Assume agent endowments satisfy certain “reasonable conditions”. E.g., each agent has a **positive endowment** of every good. (Much less suffices: e.g., each agent has something another agent wants, and the graph of this is strongly-connected.)
- Given a price vector, $p \in \mathbb{R}^m_{\geq 0}$, each agent $i$ has an **optimal demand** set, $D_i(p) \subseteq \mathbb{R}^m_{\geq 0}$. This is **the set of bundles of goods**, $x_i$, that **maximize** agent $i$’s utility, and which $i$ can afford to buy at prices $p$ by selling its endowment $w_i$ at prices $p$.

### Existence of market equilibrium for an exchange economy

A non-zero price vector, $p^\ast \geq 0$, together with bundles, $x_i^\ast$, of goods for each agent $i$, constitutes a **market (price) equilibrium** for an exchange economy, if at prices $p^\ast$, for every agent $i$, $x^\ast_i$ is an **optimal demand bundle**, and moreover with these demands the market clears (i.e., basically **supply = demand**). In other words:

1. For all agents $i$, $x^\ast_i\in D_i(p^\ast)$. (All agents optimize utility at price $p^\ast$)
2. $\sum_ix_i^\ast \leq \sum_i w_i$. (Demands do not exceed supply for any commodity.)
3. Furthermore, for **all goods** $j$, if $(\sum_ix^\ast_i)_j < (\sum_iw_i)_j$, then $p_j^\ast = 0$. (In other words, only free goods can have excess supply.)

**Theorem ([Arrow-Debreu, 1954])** Every exchange economy has a market (price) equilibrium.

### A side question: Do we really need money?

- Couldn’t we achieve the same “goals” of the market without money?
- In other words, couldn’t we organize a “barter economy” to conduct a simultaneous exchange of goods between all agents, in a way that achieves Pareto optimal bundles of goods for every agent?

**Note**: the **The First Fundamental Theorem of Welfare Economics** says that allocations of goods in any market equilibrium are Pareto optimal.

We shall see that some things become impossible to do without money.

### Impossibility theorems in social choice theory
The section ***Let’s bring money back into the picture & The Vickrey-Clarke-Groves (VCG) Mechanism*** really helps us to understand the concepts.

- Let $C$ be a set of **outcomes**, and let  $L$ be the set of total **orderings** ($\prec$) on $C$. A **social choice** function is a function $f: L^n\to C$. ($C = \lbrace c_1, \cdots, c_n, \cdots, c_k\rbrace$, $L^n = L_1\times \cdots \times L_n$, $L_i = \lbrace \prec_{i, 1}, \cdots, \prec_{i, m}\rbrace$)
- $f$ can be **strategically manipulated** by player (voter) $i$, if some $\prec_1,\cdots,\prec_n\in L$, we have $c\prec_i c'$, and if $c = f(\prec_1, \cdots, \prec_n)$, and there exists some other ordering $\prec_i'$ such that $c' = f(\prec_1, \cdots, \prec_i', \cdots, \prec_n)$.
    - **Note**: More intuitively, player $i$ is dominant. $L_i$ can dominant the selection of outcomes.
- $f$ is called **incentive compatible** (strategy-proof) if it can not be strategically manipulated by anyone.
- $f$ is a **dictatorship** if there is some player $i$ such that for all $\prec_1, \cdots, \prec_n$, $f(\prec_1, \cdots, \prec_n) = c_i$, where $c_i$ is the maximum outcome for player $i$, i.e. $\forall b\neq c_i,\ b\prec_i c_i$.

[**Wiki version**](https://en.wikipedia.org/wiki/Arrow%27s_impossibility_theorem#Formal_statement_of_the_theorem):

- Let $A$ be a set of outcomes, $N$ a number of voters of decision criteria. We shall denote the set of all full linear orderings of $A$ by $L(A)$.
    
    A (strict) social welfare function (preference aggregation rule) is a function:
    
    $$
    F: L(A)^N \to L(A)
    $$
    
    which aggregates **voters’ preferences** into a **single preference** order on $A$.

**Theorem [Gibbard-Satterthwaite’73,’75]**: If $\lvert C \rvert \ge 3$, and $f: L^n \mapsto C$ is an incentive compatible social choice function which is onto $C$ (i.e., all outcomes are possible), then $f$ is a dictatorship. (or, if a strict voting rule has at least 3 possible outcomes, it is non-manipulable if and only if it is dictatorial.)

**Arrow’s Impossibility Theorem**: There is no “really good” way to aggregate people’s preference orders (over $\ge 3$ alternatives) into a societal preference order.

### Let’s bring money back into the picture

- Let $V$ be the set of voters.
- Suppose that instead of a preference ordering, each voter $i\in V$ has a (**non-negative**) **monetary value function**: $v_i: C \mapsto \mathbb{R}_{\ge 0}$, where $v_i(c)$ says how much money a win by candidate $c$ is worth for voter $i$.
- Suppose we want to choose a candidate $c^\ast$ that maximizes the total value for the entire voter population, i.e., we want to choose:
    
    $$
    f(v_1, \cdots, v_n) = c^\ast \in \argmax_c\sum_{i\in V}v_i(c)
    $$
    
- But voters could be dishonest and lie about their true value function. (Voter $i$ can declare a different non-negative value functions $v_i'$.)
- Can we incentivize the voters to tell the truth?
- **Yes, if we are allowed to ask them to pay money.**    

### The Vickrey-Clarke-Groves (VCG) Mechanism

- Each voter $i\in V$ is asked to submit their nonnegative valuation function, $v_i'$. ($v_i'$ may or may not be $i$’s **actual** valuation function $v_i$.)
- The mechanism then computes an **optimal candidate**, $f(v_1', \cdots, v'_n) := c^\ast$, that maximizes total value:
    
    $$
    f(v_1',\cdots, v_n'):= c^\ast\in \argmax_c \sum_{k\in V}v_k'(c)
    $$
    
    This candidate $c^\ast$ is chosen as the **winner of the election**.
    
- Moreover, each voter $i$ has to **pay** an amount $p_i(c^\ast)$ to the mechanism, which is **independent of** $v_i'$, defined by (the marginal harm their has caused to other bidders):
    
    $$
    p_i(c^\ast) := (\max_{c'\in C} \sum_{j\in V-\lbrace i\rbrace}v'_j(c')) - \sum_{j\in V-\lbrace i\rbrace}v'_j(c^\ast)
    $$

**Key Point [1]**: This marginal harm caused to other participants (i.e. the final price paid by each individual with a successful bid) can be calculated as: **(sum of bids of the auction from the best combination of bids *excluding the participant under consideration*) − (what other *winning* bidders have bid in the current (best) combination of bids)**. If the sum of bids of the second best combination of bids is the same as that of the best combination, then the price paid by the buyers will be the same as their initial bid. In all other cases, the price paid by the buyers will be lower.

**Key Point [2]**: These payments align the incentives of all voters: each voter $i$, even knowing the valuation functions $v_j'$ declared by voters $j \neq i$, will want to declare a function $v_i'$ that yields a winner $c^\ast = f(v_1',\cdots, v_n')$ which maximizes $v_i(c^\ast) + \sum_{k\in V-\lbrace i\rbrace}v'_k(c^\ast)$. So, it should $v'_i:= v_i$. 

### Basic properties of VCG

Let $f(v_1', \cdots, v_n') = c^\ast$ be the outcome chosen as the winner by the VCG mechanism, based on their declared (non-negative) valuation functions $v_1', \cdots, v_n'$. Then for every voter $i$ both its **payment** $p_i(c^\ast)$ and its **purported utility** $u'_i(c^\ast) = v'_i(c^\ast) - p_i(c^\ast)$ are non-negative, i.e.:

$p_i(c^\ast) \ge 0$  and $u_i'(c^\ast) := v'_i(c^\ast) - p_i(c^\ast) \ge 0$.

### VCG is incentive-compatible (i.e., strategy-proof)

**Theorem ([Vickrey,1961],[Clarke,1971],[Groves,1973])** The VCG mechanism is incentive compatible (i.e., strategy proof). In other words, declaring their true valuation function $v_i$ is a (weakly) dominant strategy for all player $i$.

Proof Suppose players declare valuations $v_1', \cdots, v_n'$. Suppose player $i$’s true valuation is $v_i$. Let $c^\ast = f(v_i, v_{-i}')$, and let $c''=f(v_i', v_{-i}')$. 

Recall $c^\ast\in \argmax_c v_i(c) + \sum_{k\in V- \lbrace i\rbrace}v'_k(c^\ast)$ . In other words, for all $c\in C$, 

$$
v_i(c^\ast) + \sum_{k\in V-\lbrace i\rbrace}v_k'(c^\ast) \geq v_i(c) + \sum_{k\in V-\lbrace i\rbrace}v'_k(c)
$$

Thus, $u_i(c^\ast) =$ 

$$
\begin{align*}v_i(c^\ast) - p_i(c^\ast) &= v_i(c^\ast) + (\sum_{k\in V-\lbrace i\rbrace}v'_k(c^\ast)) - (\max_{c'\in C}\sum_{j\in V-\lbrace i\rbrace}v'_j(c')) \\&\geq v_i(c'') + (\sum_{k\in V-\lbrace i\rbrace}v_k'(c'')) - (\max_{c'\in C}\sum_{j\in V-\lbrace i\rbrace}v'_j(c')) \\ &= v_i(c'') - p_i(c'') = u_i(c'') \end{align*}
$$