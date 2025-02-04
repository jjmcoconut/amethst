Ragavendran Gopalakrishnan, Sherwin Doroudi, Amy R. Ward, Adam Wierman

# 1. Introduction

**Traditional Approach**
- Literature on scheduling and staffing in service systems
- Servers modeled with fixed service rates
- Policies proposed and analyzed based on these rates

**Reality of Strategic Servers**
- Server work rates can be impacted by scheduling and staffing policies
- Examples:
	- Slowing down to avoid overload
	- Reducing service rates to ensure extra staff assignment
- Observed strategic behaviors:
	- Call center agents hanging up on customers
	- Academics delaying paper reviews

**Impact of Strategic Behavior**
- Can significantly affect service system performance
- Optimal policies under non-strategic models may lead to suboptimal results

**Approaches to Create Proper Incentives**
1. Performance-based payments (bonuses)
2. Incentive-aware scheduling and staffing
	- Incentives in how scheduling and staffing are performed that reward good job performance

**Importance of Incentive-Aware Scheduling and Staffing**
- Crucial in systems where bonuses are not possible (e.g., volunteered academic reviewing)
- Many service systems don't use performance-based compensation (fixed salaryman)
- Can be less expensive than monetary bonuses
- Eliminates concerns about unfairness from differential payments

**Research Goal**
- Initiate study of incentive-aware scheduling and staffing policies

**Key Questions**
- Can scheduling and staffing incentives significantly impact server behavior?
- How can these incentives be leveraged to improve system performance?

# 2. A Model for Strategic Servers

**Objective**
- Investigate effects of strategic servers on service system management decisions


**Utility Function Formula**`
$$ U_i(\mu) = I_i(\mu) - c(\mu_i), i \in \{1, ..., N\} $$
- Fixed wage service system
- Parameters:
	- $\mu$: Vector of work rates chosen by each server
	- $I_i(\mu)$: Time-average idle time for server i
	- $c(\mu_i)$: Effort cost for server i
		- $c$: Increasing, convex function (same for all servers)
- Key Trade-off: Balance between idleness and effort

**Challenges for Staffing and Routing**
- Routing to fastest servers decreases their utility
- Makes maintaining fast service rates less desirable 

**Example: M/M/1 Queue with Strategic Server**
- Server chooses service rate $\mu > \lambda$ to maximize utility
- Fraction of idle time: $1-\lambda/\mu$
- $U(\mu)=1-\frac{\lambda}{\mu}-c(\mu)$
	1. $c'(\lambda) < 1/\lambda$: Unique optimal operating point exists
	2. $c'(\lambda) \geq 1/\lambda$: No maximum in $(\lambda, \infty)$

# 3. The M/M/N Queue with Strategic Servers

## 3.1 Model and Notation

**System Overview**
- M/M/N queue with Poisson arrivals (rate $\lambda$)
- N servers, each capable of handling any customer
- FIFO discipline for delayed customers
- Service times are independent and exponential

**Strategic Server Behavior**
- Servers choose their service rate to maximize utility
- Utility function for server $i$: $U_i(\mu; λ, N, R) = I_i(\mu; λ, N, R) - c(\mu_i)$
	- $\mu$: vector of service rates
	- $I_i$: steady-state fraction of idle time for server i
	- $c(\mu_i)$: effort cost (increasing, convex function)
	- $R$: routing policy
		- Random
		- LISF/SISF
		- FSF/SSF

**Game-Theoretic Model**
- Servers compete for system idle time
- Operating point modeled as Nash equilibrium
- Nash equilibrium condition: $U_i(\mu_i^*, \mu_{-i}^*; R) = \max_{\mu_i > λ/N} U_i(\mu_i, \mu_{-i}^*; R)$

**Focus on Symmetric Nash Equilibria**
- All servers choose the same service rate $\mu^*$
- Reasons:
	1. Fair outcome (servers have same skill level)
	2. Technical challenges in analyzing asymmetric equilibria

**Constraints**
- Each server must work at rate $> \lambda/N$ for system stability
- Possibility of quality standards imposing higher lower bounds

**Note**: Asymmetric equilibria may exist but are not studied in this paper


## 3.2 M/M/N Queue with Strategic Servers and Random Routing

### 3.2.1 Idle Time Analysis

__Goal:__
- Understand idle time of heterogeneous M/M/N queues
- Only focusing on symmetric equilibria $\rightarrow$ Understand best response for a deviating server when others have same service rate

**Key Results:**
1. Theorem 1: Idle time probability for a tagged server $\mu_1>(\lambda-(N-1)\mu)^+$
	- $$\begin{align} I(\mu_1,\mu;\lambda,N)=\left(1-\frac{\rho}{N}\right)\left( 1-\frac{\rho}{N}\left( 1-\frac{\mu}{\mu_1} \right) \right)\left(1+\frac{\text{ErlC}(N,\rho)}{N-(\rho+1-\mu_1/\mu)}\right)^{-1} \end{align}$$
		- $\rho=\lambda/\mu$
2. Theorem 2: First two derivatives of idle time w.r.t. $μ_1$
	- First derivative always positive (idle time increases with service rate)
	- Second derivative more complex
3. Theorem 3: Properties of second derivative
	- Threshold $μ_1^+$: Idle time convex below, concave above

### 3.2.2 Symmetric Equilibrium Analysis

**Key Results:**
- $U_i(\mu; λ, N, R) = I_i(\mu; λ, N, R) - c(\mu_i)$
	- First order condition: $$\frac{\partial U}{\partial \mu_1}=0 \iff \frac{\partial I}{\partial \mu_1}=c'(\mu_1)$$
	- Needs to be obtained by $\mu_1=\mu$: $$\frac{\lambda}{N^2\mu^2}\left( N-\frac{\lambda}{\mu}+\text{ErlC}\left( N,\frac{\lambda}{\mu} \right) \right)=c'(\mu)$$
	- Also equilibrium needs to satisfy: $U(\mu,\mu)\geq U(\lambda/N,\mu)$
1. Theorem 5: Existence and uniqueness of equilibrium
	- Sufficient condition for at least one solution: $c'(λ/N) < 1/λ$
	- Sufficient condition for unique solution: $2(λ/N)c'(λ/N) + (λ/N)²c''(λ/N) ≥ 1$
2. Theorem 6: Multiple equilibria comparison
	- If two equilibria exist, the one with larger service rate is preferred by servers

## 3.3 Numerical Examples

![[Pasted image 20241127132504.png|500]]

__Key Observations__
1. **Number of Equilibria**
	- At most two equilibria
	- No equilibrium for large minimum service rate $λ/N$
	- Unique equilibrium for small enough $λ/N$
	- Two equilibria possible for intermediate $λ/N$
2. **Behavior of Equilibria**
	- Larger equilibrium:
		- Service rate: Increases then decreases with $λ$
		- Mean waiting time: Steadily increases
	- Smaller equilibrium:
		- Service rate: Increases with $λ$
		- Mean waiting time: Decreases
3. **Inconsistent Relationship**
	- Equilibrium service rates and waiting times show inconsistent relationships
	- Differs from classical, nonstrategic models

## 4. Staffing Strategic Servers

__Staffing__: How many servers should be used for a given arrival rate?
- As number of server increases, the incentive to work harder decreases
- Staffing level creates incentives for the servers to speed up or slow down
- Find staffing level that minimizes costs

### 4.1 Preliminaries

**Cost Structure**
- Linear staffing and waiting costs
- Total system cost: $C^*(N, λ) = c_S N + \bar{w} λ\bar{W}^*$
	- $c_S$: per-unit staffing cost
	- $\bar{w}$: per-unit waiting cost
	- $\bar{W}^*$: mean steady state waiting time

**Admissible Staffing Policy**
A staffing policy $N^λ$ is admissible if:
1. Stable symmetric equilibrium exists for large λ
2. Sequence of symmetric equilibria has bounded service rates

**Asymptotic Optimality**
A staffing policy $N^λ$ is asymptotically optimal if:
- It is admissible
- $\lim_{λ→∞} C^{*,λ}(N^\lambda) / C^{*,\lambda}(N^{opt,λ}) = 1$
	- $N^{opt,\lambda}=\text{arg}\min_{N:\text{admissable}}C^*(N,\lambda)$
	- $C^{*,\lambda}(N^\lambda)=c_SN^\lambda+\bar{w}\lambda\bar{W}^{*,\lambda}$
	- $\mu^{*,\lambda}$: Equilibrium service rate with arrival rate $\lambda$
	- $\bar{W}^{*,\lambda}$: Mean steady state waiting time in $M/M/N^\lambda$

## 4.2 An Asymptotically Optimal Staffing Policy


Asymptotically optimal policies must be asymptotically linear in $λ$
- $N_λ = (1/a)λ + o(λ)$, for $a ∈ (0, ∞)$
	- $\lim_{\lambda \rightarrow \infty} N^\lambda/\lambda=0$: Severe understaffing leading to service rates increasing without limit.
	- $\lim_{\lambda \rightarrow \infty} N^\lambda/\lambda=\infty$: Severe overstaffing is too expensive for the system manager.

Equilibrium Characterization:
- $a(μ - a) = μ³c'(μ)$
	- $\partial U/\partial \mu =0$
	- $N_λ = (1/a)λ + o(λ)$
	- $\lambda \rightarrow \infty$

Existence of Symmetric Equilibria:
- Depends on value of a in staffing policy
- Theorem 7 provides conditions for existence

Optimal Staffing:
- $$\frac{C^{*,\lambda}(N^\lambda)}{\lambda}\rightarrow\frac{1}{a}c_S,\quad\text{as }\lambda\rightarrow\infty$$
	- $C^{*,\lambda}(N^\lambda)=c_SN^\lambda+\bar{w}\lambda\bar{W}^{*,\lambda}$
	- $N_λ = (1/a)λ + o(λ)$
- $a^* = \sup\{a > 0 :$ there exists at least one solution $μ > 0$ to $a(μ - a) = μ³c'(μ)\}$
- $N^{ao,λ} = (1/a*)λ + o(λ)$ is asymptotically optimal if it satisfies $a(μ - a) = μ³c'(μ)$

Specific Case: $c(μ) = c_E μ^p$
- a* and μ* both increasing in p
- Higher $c_E$ requires more staffing
- More convex cost functions allow for lower staffing levels ($p \uparrow \rightarrow a^*\uparrow$)
## 4.3 Contrasting Staffing Policies for Strategic and Nonstrategic Servers

Key Observation
- Strategic server behavior leads to quality-driven regime

### 4.3.1 Nonstrategic Servers 

Square-root staffing minimizes costs as λ increases(Borst et al. 2004)
- Asymptotically optimal staffing rule: $$N^{BMR,λ}_μ = \frac{\lambda}{\mu} + y^*\sqrt{\frac{\lambda}{\mu}}$$
	- $y^* = \text{arg}\min_{y>0}{c_Sy + w\alpha(y)/y}$
	- $\alpha(y)=(1+y/h(-y))^{-1}$
	- $h(y)=\phi(y)/(1-\Phi(y))$

### 4.3.2. Contrasting Strategic and Nonstrategic Servers


__Staffing Levels:__
- $N^{ao,λ}$ staffs order λ more servers than $N^{BMR,λ}_{\mu^*}$
	- Solution of $a(μ - a) = μ³c'(μ)$ implies $a>\mu$
- If $c(\mu)=c_E\mu^p$
	- $N^{ao,λ} - N^{BMR,λ}_{\mu^*} = λ/α^*(p+2) + o(λ)$
- Difference decreases as cost function becomes more convex($p$)
- Convexity is helpful to the system manager

Nonstrategic Server Staffing Policy:
- Can system manager force nonstrategic servers to work harder?
- $N^{*,BMR,λ} = λ/μ^{*,λ} + y^*\sqrt{λ/μ^{*,λ}}$
- Equilibrium service rate $μ_λ → 0$ as $λ → ∞$
- Cannot be a symmetric equilibrium service rate
- Staffing policy based on nonstrategic servers may not be practical


## 4.4. Numerical Examples

![[Pasted image 20241127142548.png|500]]

Observations:
- Jagged curves due to discrete staffing levels
- Quick convergence of $N^{ao,λ}$ to $N^{opt,λ}$
- Complex prelimit behavior necessitates asymptotic analysis
- Asymptotic results predictive for realistically sized systems

# 5. Routing to Strategic Servers

### Two Classes of Routing Policies:
1. Idle-time-order-based policies
2. Rate-based policies

## 5.1 Idle-Time-Order-Based Policies

__Definition:__
- Use rank ordering of when servers last became idle
	1. Random
	2. Weighted Random
	3. Longest Idle Server First (LISF)
	4. Shortest Idle Server First (SISF)

### 5.1.1 Policy-Space Collapse
- All idle-time-order-based policies are "equivalent"
	1. When all servers are busy, the system behaves like an M/M/1 queue regardless of the routing policy, as there's no choice in routing.
	2. The steady-state probabilities for states where servers are idle depend only on the arrival rate and individual server service rates, not on the specific order in which idle servers are chosen.

__Implications for Server Game:__
- All idle-time-order-based policies have same equilibrium behavior as Random
- Cannot achieve better performance than Random using any idle-time-order-based policy

## 5.2 Rate-Based Policies

__Definition:__
- Makes routing decisions based on server rates
- $r$-routing policies: Jobs assigned to idle server $i$ with probability $p_i = μ_i^r / \sum μ_j^r$

__Special Cases:__
- $r = 0$: Random
- $r → ∞$: Fastest Server First (FSF)
- $r → -∞$: Slowest Server First (SSF)

__Equilibrium Analysis (M/M/2 system):__
2. FSF and SSF do not admit symmetric equilibria
3. Any $r$-routing policy that admits symmetric equilibrium admits unique symmetric equilibrium: $μ^*$
	- $μ^*$ decreases with $r$
	- Mean response time($E[T]$) increases with r
4. Theorem 12:
	- Equilibrium service rate has an upper limit
	- $r$ that makes symmetric equilibrium has a lower limit
5. Theorem 13:
	- Symmetric equilibrium exists for r ∈ {-2, -1, 0, 1}

__Implications for System Manager:__
- Choose smallest r admitting symmetric equilibrium
	- $\because$ $μ^*$ decreases with $r$
- If cost function unknown, set $r = -2$ for better performance than Random
- If cost function known, may use lower $r$ for even better performance
