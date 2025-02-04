Lu Huang, Jing-Sheng Song, Robert Swinney

# Introduction

Multitier supply chain's responsibility violation has 3 features
1. Violations occur in tiers 2+ 
2. Violations can result in direct and indirect losses for all tiers
3. Tiers 0 and 1 work together to assist tier 2

__Goal: Understand the unique implications of a multitier structure of social responsibility__
1. How should a tier 0 manage social responsibility in tier 2
2. How can external forces best exert pressure to improve responsibility in the supply chain?
3. How does tier 2+ suppliers differ from tier 0, 1?

# Model

__Variables__
$x_i$: Responsibility effort in tier $i$
$b$: Baseline return on tier 2 effort
- $b>0$
- Tier 2 can exert effort on improving responsibility w/o help from tier 0/1
$x=(x_0+x_1+b)x_2$: Total supply chain effort
- Tier 0/1 is fully responsible, Tier 2 is risky
- Efforts from tier 0/1 are substitutes
	- Does not matter for tier 2 whether tier 0 or tier 1 provides financial support
	- Total support from tier 0 & 1: $x_0+x_1$
- Effort from tier 2 and tiers 0/1 are complements
$\lambda(x)=e^{-x}$: Probability of violation
- Decreasing and convex in $x$
$\beta$: Conditional probability of detecting a violation
- Probability violation is detected given violation had occured
$\alpha(x)=\beta\lambda(x)$: Probability of detecting a violation
$d$: Total consumer demand
$m_i$: unit profit margin in tier $i$
- $m_i \geq 0$: profitable for each tier(motivation)
$k_i$: Marginal cost of effort in tier $i$
- $k_i>0$ constant
- Financial costs are usually linear
$\gamma$: Fraction of demand lost due to a violation
- $\gamma \in (0,1)$, demand loss: $\gamma d$
- Affects all tiers
$a_i$: Indirect loss from a violation in tier $i$
$\ell_i=\gamma m_id+a_i$: Total loss from a violation in tier $i$
$\tau_i = k_i/\ell_i$: Loss-adjusted effort cost in tier $i$

__Sequence of Events__
Buyer is assumed to be powerful(e.g. GM)
1. Effort stage
	- Tier 0 first optimizes $x_0$ by maximizing its profit
	- Tier 1 optimizes $x_1$ by maximizing its profit based on $x_0$
	- Tier 2 optimizes $x_2$ by maximizing its profit based on $x_0, x_1$
2. Production stage
	- Responsibility violations randomly occur with probability $\alpha (x)$
	- Impact of violation($\gamma, a_i$)
3. Selling stage
	- After observing violations tier 0 finalizes its order quantity
	- All tiers are affected by $\gamma$

__Profit Models__
Expected profit function of tier i
$$\Pi_i(x_0,x_1,x_2)=m_id-k_ix_i-\ell_i\alpha(x)$$
where $\ell_i=\gamma m_id+a_i,\alpha(x)=\beta e^{-x_2(x_0+x_1+b)}$

# Result

## Buyer's Optimal Strategy

Lemma 1. Given fixed efforts from tiers 0 and 1, the tier 2 supplier’s profit is concave in x2. Furthermore,
1. Tier 2’s best response effort is $x^∗_2(x_0, x_1)= ln β(x_0+x_1 + b)/τ_2]/(x_0 + x_1 + b)$.
2. The chance of a violation is $λ^∗(x_0, x_1)=τ_2/(β(x_0 + x_1 + b))$.
3. The chance of a detected violation is $α^∗(x_0, x_1) =τ_2/(x_0 + x_1 + b)$.

Lemma 1(1) is the result of $\frac{\partial \Pi_2}{\partial x_2} = \frac{\partial}{\partial x_2} (m_2d-k_2x_2-\ell_2\beta e^{-x_2(x_0+x_1+b)})=0$ .
(2),(3) are just the results from (1)
By looking at result (3) we can see that $\alpha$ is only a function of $\tau_2, x_0, x_1, b$
Also the expected profit function of tier i is $\Pi_i(x_0,x_1,x_2)=m_id-k_ix_i-\ell_i\tau_2/(x_0+x_1+b)$

Again by calculating $\frac{\partial \Pi_1}{\partial x_1} = \frac{\partial}{\partial x_1} (m_1d-k_1x_1-\ell_1\tau_2/(x_0+x_1+b))=0$ we get 
$$x_1^*(x_0)=(\sqrt{\tau_2/\tau_1}-b-x_0)^+$$
-  If $x_0 > \sqrt{\tau_2/\tau_1}-b$ then $x_1=0$
	- From $\frac{\partial \Pi_0}{\partial x_0} = \frac{\partial}{\partial x_0} (m_0d-k_0x_0-\ell_0\tau_2/(x_0+b))=0$ we get $x_0^*=(\sqrt{\tau_2/\tau_0}-b)^+$
	- If $\sqrt{\tau_2/\tau_0}\leq b$ then $x_0,x_1=0$
-  If $x_0 \leq \sqrt{\tau_2/\tau_1}-b$ then $x_1=\sqrt{\tau_2/\tau_1}-b-x_0 \geq 0$
	- $\Pi_0=m_0d-k_0x_0-\ell_0\tau_2/(x_0+(\sqrt{\tau_2/\tau_1}-b-x_0)+b)=m_0d-k_0x_0-\ell_0\tau_2/\sqrt{\tau_2/\tau_1}$
	- $\partial \Pi_0/\partial x_0 =-k_0$: Tier 0 wants to minimize $x_0$ -> $x_0=0$

Therefore there is only 3 cases
1. $x_0=\sqrt{\tau_2/\tau_0}-b \geq 0,x_1=0$: Control strategy
2. $x_0 = 0,x_1=\sqrt{\tau_2/\tau_1}-b-x_0\geq 0$: Delegation strategy
3. $x_0=x_1=0$: No effort strategy

## External Stakeholder Pressure

From $x_i$,$b$,$x$,$\lambda(x)$,$\beta$,$\alpha(x)$,$d$,$m_i$,$k_i$,$\gamma$,$a_i$,$\ell_i$,$\tau_i$ the variables that can be changed by an external factor is $\gamma,\beta,a_i,b$. Consider how $\gamma,\beta,a_i,b$ can affect $\lambda$

For fixed responsibility management strategy, chance of violation is decreasing in all sources of external stakeholder pressure

Boundary between control and delegation strategy, control results in strictly lower violation risk
- When the strategy changes from control to delegation violation risk increases
	- Buyer is willing to pay $k_0x_0$ iff it results in significant reduction in risk
	- Because tier 1's effort under delegation strategy is free to the buyer
- $\beta,a_0,a_1,b$ does not move strategy from control to delegation
	- These variables always decrease riskiness
- Increase of $\gamma, a_1$ is possible to move the optimal strategy from control to delegation
	- These variables can increase violation probability

## Comparison with a Two-Tier Supply Chain

Multitier supply chains better represent the structure of the real world examples
Comparison 2-tier supply chain is made by merging tier 0 and tier 1.
- $m'_0=m_0+m_1$
- $a'_0=a_0+a_1$

In this supply chain there are only 2 optimal strategies
- Control strategy
- No effort strategy

Delegate strategy is not an option for 2-tier supply chain implies that external pressure cannot reduce responsibility. However chance of violation($\lambda$) can be smaller for the 3-tier supply chain in some conditions ($\tau'_0>\tau_1,\tau_2>b^2\tau_1$).

# Conclusion

- For a 3-tier supplier chain the optimal strategy for the buyer is one of control, delegation, no-effort strategy
- From external pressures($\gamma,\beta,a_i,b$)
	- $\beta,a_0,a_1,b$ always reduces tier 2's violation probability($\lambda$)
		- $\lambda$ is inversely proportional to $\beta$ which makes $\alpha$ independent with $\beta$
	- Increase of $\gamma, a_1$ may lead to increase in violation
- Increase of external factors do not backfire in 2-tier supply chains, but 3-tier suppliers take advantage in certain conditions having a lower violation rate

__Helps buyers make better decisions about managing responsibility in multitier supply chain.__