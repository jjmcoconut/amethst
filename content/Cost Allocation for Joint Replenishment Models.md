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
- $$\begin{align}
 g_S(\mathbb{T}_S)&=\sum_{i=0}^s K(\{\pi_0,\dots,\pi_i\})\left(\frac{1}{T_{\pi_i}}-\frac{1}{T_{\pi_{i+1}}}\right)\\&=\sum_{i=0}^s \frac{1}{T_{\pi_i}}(K(\{\pi_0,\dots,\pi_{i-1},\pi_i\})-K(\{\pi_0,\dots,\pi_{i-1}\}))
 \end{align}$$
	- $\pi=(\pi_0,\pi_1,\dots,\pi_s)$ permutation of $S\cup\{0\}$ s.t. $T_{\pi_0}\leq T_{\pi_1}\leq\cdots\leq T_{\pi_s}$
	- Order frequency: $1/T_{\pi_i}-1/T_{\pi_{i+1}}$, $1/T_{\pi_{s+1}}=0$
- $$\begin{align} 
 \max\quad &\sum_{i=0}^s \frac{1}{T_i}k_i\\s.t.\quad &k\in\Phi_S
 \end{align}$$
	- $\Phi_S=\{k\in R^{s+1}:k\geq0\text{, and }\sum_{i\in A}k_i\leq K(A) \forall A\subseteq S \cup \{0\}\}$
- $$V_{\Gamma_\mathcal{L}}(S)=\min_{\mathbb{T}_S\in\Gamma_\mathcal{L}^{s+1}}\max_{k\in \Phi_S}\frac{k_0}{T_0}+\sum_{i\in S}\left(\frac{k_i}{T_i}+H_iT_i+H_i^w\max\{T_0-T_i,0\}\right)$$

# 3. Duality Results

1. Dual of $\max \sum k_i/T_i$ s.t. $k\in\phi_S$ is $$\begin{align}
\min_\alpha &\sum_{A \subseteq S\cup \{0\}} \alpha_KK(A)\\
s.t. &\sum_{A \subseteq S\cup \{0\}:i\in A} \alpha_A\geq \frac{1}{T_i} \quad \forall i\in S\cup \{0\}\\
&\alpha \geq0
\end{align}$$
	- $\alpha=(\alpha_A:A\subseteq S\cup\{0\})$
2. $$\begin{align}
V_{\Gamma_\mathcal{L}}(S)=\min_{\alpha,\mathbb{T}_S}&\sum_{A\subseteq S\cup\{0\}}\alpha_AK(A)+\sum_{i\in S}\left(H_iT_i+H_i^w\max\{T_0-T_i,0\}\right)\\
s.t. &\sum_{A \subseteq S\cup \{0\}:i\in A} \alpha_A\geq \frac{1}{T_i} \quad \forall i\in S\cup \{0\}\\
&\alpha \geq0\\
&\mathbb{T}_S\in \Gamma_\mathcal{L}^{s+1}
\end{align}$$
3. Relax set $\Gamma_\mathcal{L}$ into more general set $\Gamma$: $$\begin{align}
V_{\Gamma_\mathcal{L}}(S)=\min_{\alpha,z,\mathbb{T}_S}
&\sum_{A\subseteq S\cup\{0\}}\alpha_AK(A)+\sum_{i\in S}\left(H_iT_i+H_i^wz_i\right)\\
s.t. &\sum_{A \subseteq S\cup \{0\}:i\in A} \alpha_A\geq \frac{1}{T_i} \quad \forall i\in S\cup \{0\}\\
&z_i\geq T_0-T_i \quad \forall i\in S\\
&\alpha \geq0\\
& z\geq 0\\
&\mathbb{T}_S\in \Gamma_\mathcal{L}^{s+1}
\end{align}$$
	- $z=(z_i: i\in S)$
	- $\Gamma^{s+1}=\{t=(t_1,t_2,\dots,t_{s+1}):t_i\in\Gamma, i=1,2,\dots,s+1\}$
4. The Lagrangian function of above: $$\begin{align}
L(\alpha,\mathbb{T}_S,z;u,k) =
&  \sum_{A\subseteq S\cup\{0\}}\alpha_AK(A)+\sum_{i\in S}\left(H_iT_i+H_i^wz_i\right)\\ &- \sum_{i\in S\cup\{0\}} k_i\left(\sum_{A \subseteq S\cup \{0\}:i\in A} \alpha_A -\frac{1}{T_i}  \right)-\sum_{i\in S}u_i(z_i-T_0+T_i)\\
=&\sum_{A\subseteq S\cup\{0\}}\left( K(A)-\sum_{i\in A}k_i \right)\alpha_A+\frac{k_0}{T_0}+\left( \sum_{i\in S}u_i \right)T_0\\
&+\sum_{i\in S}\left( (H_i-u_i)T_i+\frac{k_i}{T_i} \right)+\sum_{i\in S} (H_i^w-u_i)z_i
\end{align}$$
	- $k\in R_+^{s+1}$, $u\in R_+^s$
5. $$\min_{\alpha\geq0,z\geq0,\mathbb{T}_S\in\Gamma^{s+1}}L(\alpha,\mathbb{T}_S,z;u,k)\\=
\begin{cases}\begin{align}\min_{\mathbb{T}_S }&\frac{k_0}{T_0}+(\sum_{i\in S}u_i)T_0+\sum_{i\in S}((H_i-u_i)T_i+\frac{k_i}{T_i})\\
&\text{if }u_i\leq H_i^w \space \forall i\in S\text{ and }K(A)\geq\sum_{i\in A} \forall A\subseteq S\cup \{0\} \end{align}\\
-\infty\quad\text{otherwise}
\end{cases}$$
6. Therefore the Lagrangian dual of (3) is $$\max_{k\in\Phi_S,0\leq u_i\leq H_i^w:i\in S}\min_{\mathbb{T}_S\in \Gamma^{s+1}}\frac{k_0}{T_0}+\left(\sum_{i\in S}u_i\right)T_0 +\sum_{i\in S}\left((H_i-u_i)T_i+\frac{k_i}{T_i}\right)$$
	- Let $f_S(\mathbb{T}_S;u,k)\equiv \frac{k_0}{T_0}+\left(\sum_{i\in S}u_i\right)T_0 +\sum_{i\in S}\left((H_i-u_i)T_i+\frac{k_i}{T_i}\right)$

**Dual Variables $(u,k)$ Interpretation:**
- $k$: Shows division of submodular joint setup cost
	- $k_i$ for retailer $i$
	- $k_0$ for warehouse
- $u_i$: Inventory holding cost saved by operating warehouse for retailer $i$
	- Retailer's modified inventory holding cost: $H_i - u_i$
	- Warehouse's modified inventory holding cost: $\sum_{i∈S} u_i$

__Lemma 1:__
- $$\forall \phi\neq S\subseteq N,\quad V_\Gamma(S)=\min_{\mathbb{T}_S\in \Gamma^{s+1}}\max_{k\in\Phi_S,0\leq u_i\leq H_i^w:i\in S} f_S(\mathbb{T}_S;u,k)$$
	- $\sum_{i\in S}(T_0-T_i)u_i$ is maximized when
		- $u_i=H_i^w$ if $T_0>T_i$
		- $u_i=0$     if $T_0<T_i$
	- $\sum_{i\in S}(T_0-T_i)u_i = H_i^w\max\{T_0-T_i,0\}$
	- $V_{\Gamma}(S)=\min_{\mathbb{T}_S\in\Gamma^{s+1}}\max_{k\in \Phi_S}\frac{k_0}{T_0}+\sum_{i\in S}\left(\frac{k_i}{T_i}+H_iT_i+H_i^w\max\{T_0-T_i,0\}\right)$
- Goal: show (6)$= V_\Gamma (S)$ when $\Gamma=\Gamma_{\mathcal{L}}$
	- (6) is $\max\min$ while this lemma is satisfied with $\min\max$ 
	- $\Gamma_\mathcal{L}$ is not convex $\rightarrow$ cannot use strong duality

__Lemma 2:__ Consider easier convex set $\Gamma=R_+$ 
- $$\forall \phi\neq S\subseteq N,\quad V_{R_+}(S)=\max_{k\in\Phi_S,0\leq u_i\leq H_i^w:i\in S}\min_{\mathbb{T}_S\in R_{+}^{s+1}} f_S(\mathbb{T}_S;u,k)$$
	- By using strong duality in Lemma 1 with $\Gamma=R_+$
	- $\sum_{A\subseteq S\cup\{0\}}\alpha_AK(A)+\sum_{i\in S}\left(H_iT_i+H_i^wz_i\right)$ is convex in $(\mathbb{T}_S,\alpha,z)$
	- $\Gamma=R_+$ is convex set

__Lemma 5 (Rockafeller [3])__:
- The followings are equivalent
	- $\min_x\max_y f(x,y)=\max_y\min_x f(x,y)$
	- $x^*\in \text{arg}\min_x\max_y f(x,y)$ and $y^*\in\text{arg}\max_y\min_x f(x,y)$ $\rightarrow$ $x^*\in\text{arg}\min_x f(x,y^*)$ and $y^*\in\text{arg}\max_y f(x^*,y)$

By Using Lemma 5:
- Let $\mathbb{T}_S^*$ be an optimal solution to $\min_{\mathbb{T}_S\in R_{+}^{s+1}}\max_{k\in\Phi_S,0\leq u_i\leq H_i^w:i\in S} f_S(\mathbb{T}_S;u,k)$
- Let $(u^*,k^*)$ be optimal solution to $\max_{k\in\Phi_S,0\leq u_i\leq H_i^w:i\in S}\min_{\mathbb{T}_S\in R_{+}^{s+1}} f_S(\mathbb{T}_S;u,k)$
- By Lemma 5:
	- $(u^*,k^*)\in\text{arg}\max_{k\in\Phi_S,0\leq u_i \leq H_i^w:i\in S} f_S(\mathbb{T}_S^*;u,k)$
	- $\mathbb{T}_S^*\in\text{arg}\min_{\mathbb{T}_S\in R_+^{s+1}} f_S(\mathbb{T}_S;u^*,k^*)$
- Resulting in:
	- $u_i^*=H_i^w$ if $T_0^*>T_i^*$
	- $u_i^*=0$ if $T_0^*<T_i^*$
	- $k^*\in\text{arg}\max_{k\in\Phi_S}\sum_{i\in S\cup\{0\}}\frac{k_i}{T_i^*}$
	- $T_0^*\in\text{arg}\min_{T_0\geq0}\frac{k_0^*}{T_0}+(\sum_{i\in S}u_i^*)T_0$
	- $T_i^* \in \text{arg}\min_{T_i\geq0}\frac{k_i^*}{T_i}+(H_i-u_i^*)T_i\quad\forall i\in S$

__Lemma 3:__
- $$\forall \phi\neq S\subseteq N,\quad V_{\Gamma_\mathcal{L}}(S)=\max_{k\in\Phi_S,0\leq u_i\leq H_i^w:i\in S}\min_{\mathbb{T}_S\in \Gamma_\mathcal{L}^{s+1}} f_S(\mathbb{T}_S;u,k)$$
	- Define $\tilde{\mathbb{T}}_S=(\tilde{T}_0,\tilde{T}_i:i\in S)$ s.t. $\tilde{T}_i=2^{m_i}\mathcal{L}$ where $2^{m_i-1/2}\mathcal{L}\leq T_i^*<2^{m_i+1/2}\mathcal{L}$
		- $\tilde{T}_0^*\in\text{arg}\min_{T_0\in \Gamma_\mathcal{L}}\frac{k_0^*}{T_0}+(\sum_{i\in S}u_i^*)T_0$
		- $\tilde{T}_i^* \in \text{arg}\min_{T_i\in \Gamma_\mathcal{L}}\frac{k_i^*}{T_i}+(H_i-u_i^*)T_i\quad\forall i\in S$
	- $u_i^*=H_i^w$ if $\tilde{T}_0>\tilde{T}_i$
	- $u_i^*=0$ if $\tilde{T}_0<\tilde{T}_i$
	- $k^*\in\text{arg}\max_{k\in\Phi_S}\sum_{i\in S\cup\{0\}}\frac{k_i}{\tilde{T}_i}$
	- Then we have:
		- $(u^*,k^*)\in\text{arg}\max_{k\in\Phi_S,0\leq u_i \leq H_i^w:i\in S} f_S(\tilde{\mathbb{T}}_S;u,k)$
		- $\tilde{\mathbb{T}}_S\in\text{arg}\min_{\mathbb{T}_S\in \Gamma_\mathcal{L}^{s+1}} f_S(\mathbb{T}_S;u^*,k^*)$
	- By applying Lemma 5:
		- $\min\max f_S=\max\min f_S$

