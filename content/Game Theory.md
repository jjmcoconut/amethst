# 1. Static Games of Complete Information

## 1.1 Preliminaries

__Static game__
1. Each player _simultaneously and independently_ chooses an action.
2. Conditional on the players’ choices of actions, payoffs are distributed to each player.

__Games of Complete Information__
A game of __complete information__ requires that the following four components be common knowledge among all the players of the game:
1. all the possible actions of all the players,
2. all the possible outcomes,
3. how each combination of actions of all players affects which outcome will materialize, and
4. the preferences of each and every player over outcomes.

__Common Knowledge__
An event E is __common knowledge__ if
1. Everyone knows E
2. Everyone knows that everyone knows E, and so on ad infinitum.

__Pure Strategy__ 
A __pure strategy__ for player $i$ is a deterministic plan of action. The set of all __pure strategies__ for player $i$ is denoted $S_i$. A __profile of pure strategies__ $s = (s_1, s_2, . . . , s_n), s_i ∈ S_i$ for all $i= 1, 2, . . . , n$, describes a particular combination of pure strategies chosen by all n players in the game.

__Normal-form Game__
A normal-form game includes three components as follows:
1. A finite set of players, $N = \{1, 2, . . . , n\}$.
2. A collection of sets of pure strategies, ${S_1, S_2, . . . , S_n}$.
3. A set of payoff functions, ${v_1, v_2, . . . , v_n}$, each assigning a payoff value to each combination of chosen strategies, that is, a set of functions $v_i : S_1 × S_2 × . . . × S_n → R$ for each $i ∈ N$.

__Finite Game__
A **finite game** is a game with a finite number of players, in which the number of strategies in $S_i$ is finite for all players $i ∈ N$.

__Pareto Domination__
A strategy profile $s ∈ S$ __Pareto dominates__ strategy profile $s′ ∈ S$ if $v_i(s) ≥ v_i(s′)∀ i ∈ N$ and $v_i(s) > v_i(s′)$ for at least one $i ∈ N$ (in which case, we will also say that $s′$ is Pareto dominated by $s$). A strategy profile is __Pareto optimal__ if it is not Pareto dominated by any other strategy profile.

## 1.2 Rationality and Common Knowledge

__Strictly Dominated__
Let $s_i ∈ S_i$ and $s_i' ∈ S_i$ be possible strategies for player i. We say that $s_i'$ is __strictly dominated__ by $s_i$ if for any possible combination of the other players’ strategies, $s_{−i} ∈ S_{−i}$, player $i$’s payoff from $s_i'$ is strictly less than that from $s_i$. That is, $v_i(s_i, s_{−i}) > v_i(s_i', s_{−i})$ for all $s_{−i} ∈ S_{−i}$.

__Strictly Dominant Strategy__  
$s_i ∈ S_i$ is a __strictly dominant strategy__ for $i$ if every other strategy of $i$ is strictly dominated by it, that is, $$v_i(s_i, s_{−i}) > v_i(s_i', s_{−i})\text{ for all }s_i' ∈ S_i, s_i' \neq s_i,\text{ and all }s_{−i} ∈ S_{−i}$$

__Strict Dominant Strategy Equilibrium__ 
The strategy profile $s^D ∈ S$ is a __strict dominant strategy equilibrium__ if $s^D_i ∈ S_i$ is a strict dominant strategy for all $i ∈ N$.

__Proposition 4.1__
If the game $\Gamma= \langle N, \{S_i\}^n_{i=1}, \{v_i\}^n_{i=1}\rangle$ has a strictly dominant strategy equilibrium $s^D$, then $s^D$ is the unique dominant strategy equilibrium.

__Best Response__ 
Strategies $s_{-i} \in S_{-i}$ if the strategy $s_i \in S_i$ is player $i$'s __best response__ to his opponents if:  
$$ v_i(s_i, s_{-i}) \geq v_i(s'_i, s_{-i}) \quad \forall s'_i \in S_i. $$
- A rational player who believes that his opponents are playing some $s_{−i} ∈ S_{−i}$ will always choose a best response to $s_{−i}$.

__Proposition 4.3__
If $s_i$ is a strictly dominated strategy for player $i$, then it cannot be a best response to any $s_{-i} \in S_{-i}$.

**Proof:**  
If $s_i$ is strictly dominated, then there exists some $s'_i \succ_i s_i$ such that $v_i(s'_i, s_{-i}) > v_i(s_i, s_{-i})$ for all $s_{-i} \in S_{-i}$. But this in turn implies that there is no $s_{-i} \in S_{-i}$ for which $v_i(s_i, s_{-i}) \geq v_i(s'_i, s_{-i})$, and thus that $s_i$ cannot be a best response to any $s_{-i} \in S_{-i}$.

__Belief__
A **belief** of player i is a possible profile of his opponents’ strategies, $s_{-i}\in S_{-i}$

__Best-response Correspondence__
The __best-response correspondence__ of player $i$ selects for each $s_{-i} \in S_{-i}$ a subset $BR_i(s_{-i}) \subset S_i$, where each strategy $s_i \in BR_i(s_{-i})$ is a best response to $s_{-i}$.
A strategy $s_i \in S_i$ is never a best response if there are no beliefs $s_{-i} \in S_{-i}$ for player $i$ for which $s_i \in BR_i(s_{-i})$.

## 1.3 Pinning Down Beliefs: Nash Equilibrium

__Nash Equilibrium__
The pure-strategy profile $s^* = (s^*_1, s^*_2, \dots, s^*_n) \in S$ is a __Nash equilibrium__ if $s^*_i$ is a best response to $s^*_{-i}$ for all $i \in N$, that is,  
$$ v_i(s^*_i, s^*_{-i}) \geq v_i(s'_i, s^*_{-i}) \quad \text{for all } s'_i \in S_i \text{ and all } i \in N. $$

# 1.4 Mixed Strategies

__Mixed Strategy__
Let $S_i = \{s_{i1}, s_{i2}, \dots, s_{im}\}$ be player $i$'s finite set of pure strategies. Define $\Delta S_i$ as the __simplex__ of $S_i$, which is the set of all probability distributions over $S_i$. A __mixed strategy__ for player $i$ is an element $\sigma_i \in \Delta S_i$, so that $\sigma_i = \{\sigma_i(s_{i1}), \sigma_i(s_{i2}), \dots, \sigma_i(s_{im})\}$  is a probability distribution over $S_i$, where $\sigma_i(s_i)$ is the probability that player $i$ plays $s_i$.
Let $S_i$ be player $i$'s pure-strategy set, and assume that $S_i$ is an interval. A __mixed strategy__ for player $i$ is a cumulative distribution function $F_i : S_i \to [0, 1]$, where $F_i(x) = \Pr\{s_i \leq x\}$. If $F_i(\cdot)$ is differentiable with density $f_i(\cdot)$, then we say that $s_i \in S_i$ is in the support of $F_i(\cdot)$ if $f_i(s_i) > 0$.

__Support__
Given a mixed strategy $\sigma_i(\cdot)$ for player $i$, we say that a pure strategy $s_i \in S_i$ is in the __support__ of $\sigma_i(\cdot)$ if and only if it occurs with positive probability, that is, $\sigma_i(s_i) > 0$.

__Belief__
A __belief__ for player $i$ is given by a probability distribution $\pi_i \in \Delta S_{-i}$ over the strategies of his opponents. We denote by $\pi_i(s_{-i})$ the probability player $i$ assigns to his opponents playing $s_{-i} \in S_{-i}$.

__Expected Payoff__
The __expected payoff__ of player $i$ when he chooses the pure strategy $s_i \in S_i$ and his opponents play the mixed strategy $\sigma_{-i} \in S_{-i}$ is:
$$ v_i(s_i, \sigma_{-i}) = \sum_{s_{-i} \in S_{-i}} \sigma_{-i}(s_{-i}) v_i(s_i, s_{-i}). $$

**Proposition 6.1:**  
If $\sigma^*$ is a Nash equilibrium, and both $s_i$ and $s'_i$ are in the support of $\sigma^*_i$, then
$$ v_i(s_i, \sigma^*_{-i}) = v_i(s'_i, \sigma^*_{-i}) = v_i(\sigma^*_i, \sigma^*_{-i}). $$
- There can be no Nash equilibrium in which one player plays a pure strategy and the other mixes.
- There can be no Nash equilibrium in which at least one player mixes only between two pure strategies.

__Theorem (Nash’s Existence Theorem)__
Any n-player normal-form game with finite strategy sets Si for all players has a (Nash) equilibrium in mixed strategies.

__Theorem (Brouwer’s Fixed-Point Theorem)__
If f (x) is a continuous function from the domain $[0, 1]$ to itself then there exists at least one value $x^∗ ∈ [0, 1]$ for which $f (x^∗)= x^∗$.

# 2. DYNAMIC GAMES OF COMPLETE INFORMATION

## 2.1 Preliminaries

__Game Tree__
A game tree is a set of nodes $x \in X$ with a precedence relation $x > x'$, which means "x precedes $x'$." Every node in a game tree has only one predecessor. The precedence relation is:
- **Transitive:** If $x > x'$ and $x' > x''$, then $x > x''$.
- **Asymmetric:** If $x > x'$, then it is not the case that $x' > x$.
- **Incomplete:** Not every pair of nodes $x, y$ can be ordered.
There is a special node called the root of the tree, denoted by $x_0$, that precedes any other $x \in X$. Nodes that do not precede other nodes are called terminal nodes, denoted by the set $Z \subset X$. Terminal nodes denote the final outcomes of the game with which payoffs are associated. Every node $x$ that is not a terminal node is assigned either to a player, $i(x)$, with the action set $A_i(x)$, or to Nature.

__Player in Game Tree__
Every player $i$ has a collection of information sets $h_i \in H_i$ that partition the nodes of the game at which player $i$ moves, with the following properties:
1. If $h_i$ is a singleton that includes only $x$, then player $i$, who moves at $x$, knows that he is at $x$.
2. If $x \neq x'$ and both $x \in h_i$ and $x' \in h_i$, then player $i$, who moves at $x$, does not know whether he is at $x$ or $x'$.
3. If $x \neq x'$ and both $x \in h_i$ and $x' \in h_i$, then $A_i(x') = A_i(x)$.

__Perfect/Imperfect Information__
A game of complete information in which every information set is a singleton and there are no moves of Nature is called a __game of perfect information__. A game in which some information sets contain several nodes or in which there are moves of Nature is called a __game of imperfect information__.

__Pure Strategy__
A __pure strategy__ for player $i$ is a mapping $s_i : H_i \to A_i$ that assigns an action $s_i(h_i) \in A_i(h_i)$ for every information set $h_i \in H_i$. We denote by $S_i$ the set of all pure-strategy mappings $s_i \in S_i$.

__Mixed Strategy__
A **mixed strategy** for player i is a probability distribution over his pure strategies $s_i ∈ S_i$.

__Behavioral Strategy__
A __behavioral strategy__ specifies for each information set $h_i \in H_i$ an independent probability distribution over $A_i(h_i)$ and is denoted by $\sigma_i : H_i \to \Delta A_i(h_i)$, where $\sigma_i(a_i(h_i))$ is the probability that player $i$ plays action $a_i(h_i) \in A_i(h_i)$ in information set $h_i$.

__Perfect Recall__
A game of __perfect recall__ is one in which no player ever forgets information that he previously knew.

__Equilibrium Path__
Let $\sigma^* = (\sigma^*_1, \dots, \sigma^*_n)$ be a Nash equilibrium profile of behavioral strategies in an extensive-form game. We say that an information set is __on the equilibrium path__ if, given $\sigma^*$, it is reached with positive probability. We say that an information set is __off the equilibrium path__ if, given $\sigma^*$, it is never reached.

## 2.2 Credibility and Sequential Rationality

__Sequentially Rational__
Given strategies $\sigma_{-i} \in S_{-i}$ of player $i$'s opponents, we say that $\sigma_i$ is __sequentially rational__ if and only if player $i$ is playing a best response to $\sigma_{-i}$ in each of his information sets

__Proposition 8.1__
Any finite game of perfect information has a backward induction solution that is __sequentially rational__. Furthermore if no two terminal nodes prescribe the same payoffs to any player then the backward induction solution is unique.

__Proper Subgame__
A __proper subgame__ $G$ of an extensive-form $\Gamma$ game consists of only a single node and all its successors in $\Gamma$ with the property that if $x \in G$ and $x' \in h(x)$, then $x' \in G$. The subgame $G$ is itself a game tree with its information sets and payoffs inherited from $\Gamma$.

__Subgame-perfect (Nash) Equilibrium__
Let $\Gamma$ be an $n$-player extensive-form game. A behavioral strategy profile $\sigma^* = (\sigma^*_1, \sigma^*_2, \ldots, \sigma^*_n)$ is a __subgame-perfect (Nash) equilibrium__ if, for every proper subgame $G$ of $\Gamma$, the restriction of $\sigma^*$ to $G$ is a Nash equilibrium in $G$.

## 2.3 Multistage Games

**Proposition 9.1:**  
Consider a multistage game with $T$ stages, and let $\sigma^{t*}$ be a Nash equilibrium strategy profile for the $t$th stage game. There exists a subgame-perfect equilibrium in the multistage game in which the equilibrium path coincides with the path generated by $\sigma^{1*}, \sigma^{2*}, \ldots, \sigma^{T*}$.

**Proposition 9.2:**  
If $\sigma^*$ is a Nash equilibrium of the multistage game consisting of stage games $G_1, G_2, \ldots, G_T$, then the restriction of $\sigma^*$ to the stage game in period $T$ must be a Nash equilibrium of that stage game.

**Proposition 9.3:**  
If a finite multistage game consists of stage games that each have a unique Nash equilibrium, then the multistage game has a unique subgame-perfect equilibrium.

__One-stage unimprovable__
A strategy $\sigma_i$ is __one-stage unimprovable__ if there is no information set $h_i$, action $a \in A_i(h_i)$, and corresponding strategy $\sigma^{a, h_i}_i$ such that 
$$ v_i(\sigma^{a, h_i}_i, h_i) > v_i(\sigma_i, h_i). $$