Woonam Hwang, Nitin Bakshi, Victor DeMiguel

# 1. Introduction



__Supply Uncertainty__
- Labor strikes
- Manufacturing defects

__GM labor strike (2019) - Random Capacity__
- ![[GM_strike.jpeg|300]]
- Estimated lost $1.75 billion (New York Times)

__Samsung Exynos - Random Yield__
- ![[samsung_exynos.png|300]]
- Yield rate for 3nm GAA $\leq 20\%$ (TAdviser)

**Supplier Effort**
- Suppliers can invest in improving reliability
- Effort is costly and not contractible
- Moral hazard problem 
	- Due to suppliers not fully internalizing consequences

**Coordinating Penalty Contracts:**
- Can resolve moral hazard problem
- Difficult to implement due to:
	1. Supplier's limited liability
	2. Perceived unfairness by suppliers

**Wholesale Price Contracts:**
- Often preferred in practice
- Easier to implement 

__Research Questions__
1. Who's bargaining power improves coordination?

|                     | Control | Delegation |
| ------------------- | ------- | ---------- |
| __Random Capacity__ | ?       | ?          |
| __Random Yield__    | ?       | ?          |

2. Wholesale price contracts vs. Coordinating penalty contracts

# 3. Model

__Sequence of Events__
![[Pasted image 20250108102614.png|500]]
1. Demand $D$ observed (deterministic)
2. Buyer and supplier bargain over wholesale price $w$
3. Buyer orders quantity $q$
4. Supplier exerts unverifiable effort $e$ to improve reliability
5. Supplier chooses production quantity $x$
6. Supplier delivers $\tilde{q} \leq q$ units
7. Buyer fulfills demand at unit price $p$

__Profit Functions__
- Buyer's expected profit: $\pi_b(q, e, w) = pS(q, e) - wy(q, e)$
- Supplier's expected profit: $\pi_s(q, e, w) = wy(q, e) - c(q, e)$
- Centralized supply chain profit: $\pi (q, e) = pS(q, e) - c(q, e)$

__Bargaining Process__
- Wholesale price w determined by maximizing: $\pi_s^*(w)^\alpha \pi_b^*(w)^{1-\alpha}$
	- $\alpha \in (0, 1)$ represents supplier's relative bargaining power

__Buyer's Decision Problem__
$$\begin{align*}
\max_q\quad &\pi_b(q,e,w)\\
s.t.\quad &e=\arg\max_{e\geq 0}\\
&\pi_s(q,e,w)\geq0
\end{align*}$$

__Key Findings__
1. Wholesale price w can represent supplier's relative bargaining power
2. Higher w implies greater supplier bargaining power
3. Analysis focuses on buyer's decision problem

__Assumptions__
1. Profitable to produce positive amount even without supplier effort
2. Buyer chooses largest quantity when indifferent among order quantities

[[Topic Research - Excalidraw#^0uzl04VmjnkInYyMEsYxr]]
# 4. Random Capacity

__Key Components__
- Disruptions destroy part or all of supplier's capacity
- Capacity loss independent of production quantity
- Examples: labor strikes, machine breakdowns, fire

__Model Specifics__
- Delivered quantity: $\tilde{q} = \min\{q, K - \zeta\}$
	- $q$: order quantity
	- $K$: nominal capacity
	- $\zeta$: random capacity loss
- Random loss: $\zeta = \psi/(e + 1)$
	- $\psi$: uniformly distributed in $[0, K]$
- Expected delivered quantity: $y(q, e) = E[\tilde{q}]$
- Expected sales: $S(q, e) = E[\min\{\tilde{q}, D\}]$
- Cost Structure: $c(q, e) = cy(q, e) + v(e)$
	- $c$: unit production cost
	- $v(e)$: cost of effort to improve reliability

__Centralized Supply Chain__
- Optimal order quantity ($q^o$) equals demand ($D$)
- Unique optimal decisions ($q^o, e^o$) exist
	- Producing more than $D$ does not increase sales
	- Increasing effort is the only way to mitigate risk

__Wholesale Price Contract Performance__
- Efficiency generally increasing with wholesale price ($w$)
- Efficiency trend monotonically increasing if $p < 3c$
	- High efficiency achievable with powerful supplier
	- $\because$ More powerful supplier has bigger margin $\rightarrow$ incentive to put effort

__Unit Penalty Contract__
- Coordinates supply chain (when buyer has more power)
- Buyer imposes penalty $z$ for each unit of shortage
- Coordinating contracts: $w^* = p - \chi$ and $z^* = \chi$ for $\chi \in [0, \bar{\chi})$
	- Buyer's expected profit: $\pi_b = \chi D$
	- Imposing a penalty supplier has more motivation to put effort

__Transaction Costs__
![[Pasted image 20250108111147.png|500]]
- $T$: transaction cost as percentage of centralized supply chain profit
- Wholesale price contract preferred when efficiency $> (100 - T)\%$
- Pareto improvement possible with wholesale price contract when $T$ is high

__Key Insights__
1. Wholesale price contracts perform well with powerful suppliers
2. Unit penalty contracts coordinate but have implementation complexities
3. Transaction costs may make wholesale price contracts preferable
4. Wholesale price contracts can offer Pareto improvement with high transaction costs

# 5. Random Yield

__Key Components__
- Random loss stochastically proportional to production quantity
	- Supply risk can be also mitigated by increasing production
- Applies to semiconductor, biotech manufacturing

## 5.1. Control Scenario

__Supplier Production Quantity__ ($x=q$)
- __Control__: Supplier's production quantity equals buyer's order quantity
- Common when supplier cannot test product quality on-site

### 5.1.1. Model and Centralized Supply Chain
- Delivered quantity: $\tilde{q} = (1 - \zeta)q$
	- Optimal order quantity ($q^o$) strictly greater than demand ($D$)
	- Both optimal order quantity and effort level exist
- Leftovers are same
	- Random loss: $\zeta = \psi/(e + 1)$, $\psi$ uniformly distributed in $[0, 1]$
	- Expected delivered quantity: $y(q, e) = E[\tilde{q}]$
	- Expected sales: $S(q, e) = E[\min\{\tilde{q}, D\}]$
	- Cost: $c(q, e) = cq + v(e)$

### 5.1.2. Wholesale Price Contract Performance

__Wholesale Contract Performance__
- Efficiency generally decreases with supplier's bargaining power (Preferred when buyer is powerful) 
- Powerful buyer (high $w$)
	- Deters supplier's effort investment
	- Incentivizes larger order quantity - Dual role
		- Able to order near coordinated optimum quantity
		- Supplier order quantity increases (more profit) $\rightarrow$ incentivizes effort
- ![[Pasted image 20250108125533.png|400]]
	- Robust decreasing trend in efficiency observed in numerical experiments


__Alternative Contracts__
- Unit penalty contract no longer coordinates (supplier shares none of the overage risk)
- Unit-penalty with buy-back contract coordinates and allows arbitrary profit allocation


## 5.2. Delegation Scenario

__Key Components__
- Buyer delegates production quantity decision to supplier
- Supplier determines production quantity x after receiving buyer's order q

### 5.2.1. Model and Centralized Supply Chain
- Delivered quantity: $\tilde{q} = \min\{q, (1 - \zeta)x\}$
- Expected delivered quantity: $y(q, x, e) = E[\tilde{q}]$
- Expected sales: $S(q, x, e) = E[\min\{\tilde{q}, D\}]$
- Cost: $c(x, e) = cx + v(e)$

### 5.2.2. Wholesale Price Contract Performance

__Wholesale Contract Performance__
- Efficiency exhibits V-shaped pattern as wholesale price (supplier's bargaining power) increases
	- Increasing part of wholesale price efficiency can be proved (proposition 8)
	- Other parts are from numerical observation
- Preferred when either party has most bargaining power
- ![[Pasted image 20250108131655.png|400]]
	- Numerical analysis shows clear V-shaped pattern


__Coordinating Contract__
- Unit-penalty contract coordinates supply chain




# 6. Conclusion

**Efficiency of Wholesale Price Contracts:**

|                     | Control    | Delegation |
| ------------------- | ---------- | ---------- |
| __Random Capacity__ | Increasing | Increasing |
| __Random Yield__    | Decreasing | V-shaped   |

__Wholesale price contracts may be preferred when__
  1. Random capacity: Supplier is powerful 
  2. Random yield with control: Buyer is powerful
  3. Random yield with delegation: Either party is powerful

