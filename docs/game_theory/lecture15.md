---
layout: default
title: Lecture 15 A brief taster of Markov Decision Processes and Stochastic Games
parent: Game Theory
nav_order: 11
---

## Lecture 15 A brief taster of Markov Decision Processes and Stochastic Games

### Markov Decision Processes

Definition A Markov Decision Process is given by a game graph $G_{v_0} = (V, E, pl, q, v_0, u)$, where:

- $V$ is a (finite) set of vertices.
- $pl: V \to \lbrace 0, 1\rbrace$, $pl^{-1}: \lbrace 0, 1\rbrace \to V$
    - Let $V_0 = pl^{-1}(0)$, and $V_1 = pl^{-1}(1)$.
- $E: V\to 2^{V}$ (set of pairs) maps each vertex $v$ to a set $E(v)$ of “successors” (or “actions” at $v$).
- For each “nature” vertex, $v\in V_0$, a probability distribution $q_v: E(v)\to [0, 1]$, over the set of “actions” at $v$, such that $\sum _{v'\in E(v)} q_v(v') = 1$.
- A start vertex $v_0\in V$.
- A payoff function: $u: \Psi_{T_{v_0}} \to \mathbb{R}$, from plays to payoffs for player 1.
    - Player 1 want to maximize it expected payoff.

### Different payoff functions

1. Mean payoff
    
    For a play $\pi = v_0v_1v_2v_3\cdots$, the goal is to maximize the expected mean payoff
    
    $$
    E(\lim_{n\to\infty}\inf\frac{\sum_{i = 0}^{n-1}u(v_i)}{n})
    $$
    
2. Discounted total payoff
3. Probability of reaching target

### Memoryless optimal strategies

A **strategy** is again any **function** that maps each history of the game (ending in a node controlled by player 1), to an action (or a probability distribution over actions) at that node.

**Theorem** (memoryless optimal strategies) For every **finite-state** MDP, with any of the following objectives:

- Mean payoff
- Discounted total payoff
- Probability of reaching target

Player 1 has a pure memoryless optimal strategy.

In other words, player 1 has an optimal strategy where it just picks one edge (action) from $E(v)$ for each vertex $v\in V_1$.

### Bellman Optimality Equations

For the objective of maximizing probability to reach target vertex $v_t$, consider the following system of equations. Let $V = \lbrace v_1, \cdots, v_n\rbrace$ be the set of vertices of the MDP, $G$.

Consider the following system of equations, with one variable $x_i$ for every vertex $v_i$.

$$
\begin{align*}x_{T} &= 1 \\ x_i &= \max\lbrace x_j \mid v_j \in E(v_i)\rbrace \quad\text{for } v_i\in V_1 \\ x_i &= \sum_{v_j\in E(v_i)} q_{v_i}(v_j)\cdot x_j \quad\text{for } v_i\in V_0\end{align*}
$$

Theorem These max-linear Bellman equations for the MDP, have a (unique) least non-negative solution vector $x^\ast = (x_1^\ast, \cdots, x_n^\ast) \in [0, 1]^n$, in which $x_i^\ast$ is the optimal probability for player 1 to reach the target $v_{T}$ in the MDP $G_{v_i}$ starting at $v_i$.

### Computing optimal values

One way to compute the solution $x^\ast$ for the Bellman equations $x = L(x)$ is **value iteration**: consider the sequence $L(\mathbf{0}), L(L(\mathbf{0})), \cdots, L^m(\mathbf{0})$.

**Fact**: $\lim_{m\to \infty} L^{m}(\mathbf{0}) = x^\ast$.

Unfortunately, value iteration can be very slow in the worst case (requiring exponentially many iterations.) Instead, we can use LP. Let $V = \lbrace v_1, \cdots, v_n\rbrace$ be the vertices of MDP, $G$. We have one LP variable $x_i$ for each vertex $v_i \in V$.

**Minimize** $\sum_{i = 1}^n x_i$

**Subject to**:

$$
\begin{align*}x_{T} &= 1\\ x_i&\geq x_j, \text{ for each } v_i\in V_1, \text{ and } v_j \in E(v_i);\\ x_i &= \sum_{v_j\in E(v_i)}q_{v_i}(v_j) \cdot x_j, \text{ for each } v_i\in V_0; \\ x_i &\geq 0 \text{ for } i = 1, \cdots, n.\end{align*}
$$

Theorem For $(x_1^\ast, \cdots, x_n^\ast)\in \mathbb{R}^n$ an optimal solution to this LP (which must exist), each $x_i^\ast$ is the optimal value for player 1 in the game $G_{v_i}$. 

### Extracting the optimal strategy

### Stochastic Games

*What if we introduce a second player in the game against nature?*

In Shapley’s stochastic games, at each state, both player simultaneously and independently choose an action. Their joint actions yield both a 1-step reward, and a probability distribution on the next state.

**Definition** A zero-sum simple stochastic game is given by a game graph $G_{v_0} = (V, E, pl, q, v_0, u)$, where

- $V$ is a (finite) set of vertices.
- $pl: V \to \lbrace 0, 1, 2\rbrace$, 0 represents “Nature”.
    - Inverse function $pl^{-1}$ is the same with the definition above.
- $E:V\to 2^V$ maps each vertex $v$ to a set $E(V)$ of “successors” (or “actions” at $v$).
- Let $V_{dead} = \lbrace v\in V \mid E(v) = \empty\rbrace$.
- For each “nature” vertex, $v\in V_0$, a probability distribution $q_v: E(v)\to [0, 1]$, over the set of “actions” at $v$, such that $\sum_{v'\in E(v)}q_v(v') = 1$.
- A start vertex $v_0 \in V$.
- A target vertex $v_T \in V$.
- Note: a congestion game and a simple stochastic game are two different types of games and cannot be equated. (click to open.)
    
    A congestion game is a type of game in which players choose actions that contribute to a global congestion function. The payoff of each player depends on their chosen action and the congestion experienced by all players. Congestion games are typically non-cooperative and have a pure Nash equilibrium.
    On the other hand, a simple stochastic game is a dynamic game in which players take turns to choose actions, and the game transitions between states probabilistically. The payoff of each player depends on the state of the game and the actions chosen by all players. Simple stochastic games can be cooperative or non-cooperative, and the optimal strategy for each player can depend on the strategies of the other players.
    Therefore, while both congestion games and simple stochastic games involve some level of randomness, they are fundamentally different types of games with different characteristics and cannot be reduced to each other.
    

### Memoryless determinacy

**Theorem** ([Condon’92]) Every simple stochastic game is memorylessly determined.

### Computing optimal strategies

- Memoryless determinacy immediately gives us one algorithm for computing optimal strategies:
    - “Guess” the strategy for one of the two players.
    - The “residual game” is a MDP; solve corresponding LP.
- This gives a NP $\cap$ co-NP procedure for solving simple stochastic games.
- [Hoffman-Karp’66] studied a “strategy improvement algorithm” for stochastic games based on LP, which can be adapted to simple stochastic games ([Condon’92]).
- Solving parity games and mean payoff games can be reduced to solving SSGs.