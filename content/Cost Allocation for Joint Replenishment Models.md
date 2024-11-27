Jiawei Zhang

# Abstract
## One-Warehouse Multiple Retailer Inventory Model

**Model Overview:**
- Objective: Minimize long-run average system cost
- Time horizon: Infinite
- Setup cost function: Submodular joint

**Key Points:**
- Optimal policy: Unknown
- Power-of-two policies:
  - Easy to implement
  - 98% effective

**Research Focus:**
- Cost allocation to retailers under optimal power-of-two policy

**Game Theory Aspect:**
- Generates a cooperative game
- Proven: Game has a nonempty core

**Theoretical Foundation:**
- Strong duality theorem for one-warehouse multiple retailer problem under power-of-two policies

# 1. Introduction

**System Overview:**
- Retailers: Multiple, belonging to different firms
- Time horizon: Infinite
- Customer demand: Constant at each retailer
- Warehouse: Holds inventory, replenished by external supplier
- Lead times: Zero (instantaneous delivery)

**Cost Components:**
- Holding cost: Per unit of inventory per unit time at each facility
- Setup cost: Submodular function of facilities placing joint orders

**Cooperation Aspect:**
- Retailers share warehouse and place joint orders to reduce holding and setup costs

**Cost Allocation Challenge:**
- How to allocate optimal system-wide cost among retailers
- Aim: Ensure benefit for all retailers and subsets

**Research Question:**
- Find inventory replenishment policy that minimizes long-run average cost over infinite time horizon

**Game Theory Approach:**
- Model: Cooperative game
- Key concept: Core (related to coalition stability)
- Research focus: Conditions for nonempty core in the game

# 2. The Model and the Game

**Model Components:**
- Retailers: Set $N = \{1, 2, ..., n\}$
- Warehouse: Denoted as $0$
- Demand: Continuous, deterministic rate $d_i > 0$ for retailer $i$
- Lead time: Zero (instantaneous delivery)

**Cost Structure:**
- Holding cost: $h_i$ per unit per time at facility $i$
- Setup cost: $K(S)$ for subset $S$ of facilities placing joint order
	- Submodular function with economies of scale

**Inventory Policy:**
- Stationary, characterized by $(T_0, T_i, i \in N)$
- Power-of-two policy: $T_i = 2^{m_i} * \mathcal{L}$
	- $\mathcal{L}$: Base planning period
	- $m_i\in \mathbb{Z}$: Integer (can be negative)

**Policy Effectiveness:**
- 94% effective for arbitrary $\mathcal{L}$
- 98% effective for optimal $\mathcal{L}$

**Cooperative Game Model:**
- Game: $(N, V_\Gamma)$
- $N$: Grand coalition of retailers
- $V_\Gamma$: Cost characteristic function
- $\Gamma$: Set of permissible policies
	- $\Gamma_\mathcal{L}=\{t:t>0,t=2^m\mathcal{L}\text{ for some }m\in Z\}$

**Core Concept:**
- Allocation $l = (l_1, l_2, ..., l_N)$
- Allocation $l$ is in the core of the game if:
	1. $\sum_{j\in N} l_j = V_\Gamma(N)$
	2. $\sum_{j\in S} l_j \leq V_\Gamma(S)$ for all $S \subseteq N$

**Cost Function Characterization:**
- $V_{\Gamma_\mathcal{L}}(S) = \min{g_S(\mathbb{T}_S) + h_S(\mathbb{T}_S)}$, $(\mathbb{T}_S\in \Gamma_\mathcal{L}^{s+1})$
	- $g_S$: Setup cost
	- $h_S$: Inventory holding cost
	- $\mathbb{T}_S=(T_0,T_i,i\in S)$

__Inventory Holding Cost__:
- $h_S(\mathbb{T}_S)=\sum_{i\in S}(H_iT_i+H_i^w\max\{T_0-T_i,0\})$
- by Roundy (1985)

__Setup Cost:__
- $$\begin{align}g_S(\mathbb{T}_S)&=\sum_{i=0}^s K(\{\pi_0,\dots,\pi_i\})\left(\frac{1}{T_{\pi_i}}-\frac{1}{T_{\pi_{i+1}}}\right)\\&=\sum_{i=0}^s \frac{1}{T_{\pi_i}}(K(\{\pi_0,\dots,\pi_{i-1},\pi_i\})-K(\{\pi_0,\dots,\pi_{i-1}\}))\end{align}$$
	- $\pi=(\pi_0,\pi_1,\dots,\pi_s)$ permutation of $S\cup\{0\}$ s.t. $T_{\pi_0}\leq T_{\pi_1}\leq\cdots\leq T_{\pi_s}$
	- Order frequency: $1/T_{\pi_i}-1/T_{\pi_{i+1}}$, $1/T_{\pi_{s+1}}=0$
- $$\begin{align} \max\quad &\sum_{i=0}^s \frac{1}{T_i}k_i\\s.t.\quad &k\in\Phi_S\end{align}$$
	- $\Phi_S=\{k\in R^{s+1}:k\geq0\text{, and }\sum_{i\in A}k_i\leq K(A) \forall A\subseteq S \cup \{0\}\}$
- $$V_{\Gamma_\mathcal{L}}(S)=\min_{\mathbb{T}_S\in\Gamma_\mathcal{L}^{s+1}}\max_{k\in \Phi_S}\frac{k_0}{T_0}+\sum_{i\in S}\left(\frac{k_i}{T_i}+H_iT_i+H_i^w\max\{T_0-T_i,0\}\right)$$


