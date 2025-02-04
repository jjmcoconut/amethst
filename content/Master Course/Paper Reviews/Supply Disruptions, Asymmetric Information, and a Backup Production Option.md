Zhibin (Ben) Yang, Göker Aydın, Volodymyr Babich, Damian R. Beil

# Introduction
## Supply Chain Disruption Risks

- Example: Menu Foods Corp. pet food recall (March 2007)
	- 60+ million cans/pouches recalled
	- Deaths linked to melamine in wheat gluten
	- Supply chain: Menu Foods (Canada) -> ChemNutra (US) -> Xuzhou Anying (China)

- Consequences of supply disruptions:
	- Menu Foods: Market cap dropped by ~50% to $70 million
	- Generally: Negative 40% abnormal stock return over 3 years

## Risk Management Strategies

- Supplier qualification screening
- Multisourcing
- Flexibility
- Penalties for nonperformance

## Information Asymmetry

- Suppliers often have better info about disruption likelihood
- Most research assumes equal knowledge between manufacturer and supplier
- Difference: Supply disruptions affect both cost and risk profile

## Research Questions

1. How do risk management strategies change with asymmetric information?
2. Value of eliminating information asymmetry?
3. Are risk management tools more/less valuable with information asymmetry?
4. Impact of business environment changes?

## Focus of the Study

- Penalties for nondelivery
- Manufacturer's ability to offer contract alternatives
- Supplier's backup production option

## Model Overview

- Single-period, single-supplier, single-manufacturer
- Two supplier types: high and low reliability
- Supplier choices on disruption: backup production or pay penalty

## Key Findings

1. Less reliable suppliers may be forced to pay penalties, while more reliable ones use backup production
2. Value of perfect information highest for moderately costly backup production
3. Value of information increases with:
	- Larger reliability gap between supplier types
	- Uniformly higher supplier reliability
1. Backup production option may become less valuable with better supplier information

# Model
### Model Overview
- Manufacturer purchases from unreliable supplier
- Two supplier types: high reliability ($H$) and low reliability ($L$)
- Fraction of high-reliability suppliers: $\theta ∈ [0, 1]$

### Supplier Characteristics
- Random yield: Bernoulli random variable ($\rho$)
	- Success probability: $H = h, L = l (1 > h > l > 0)$
- Regular production cost: $c_i$ per unit
- Assumption 1: $c_L/l > c_H/h$ (high type more cost-efficient)
- Backup production: perfectly reliable, cost $b$ per unit
- Assumption 2: $b > c_H/h$

### Manufacturer Characteristics
- Deterministic demand ($D$), normalized to 1
- Revenue per unit sold: $r$
- Assumption 3: $r > c_H/h$

### Information Asymmetry
- Supplier type is private information
- All other information is common knowledge

### Contract Design
- Mechanism design approach
- Two contracts: one for each supplier type
- Contract terms: 
	1. Upfront transfer payment ($X_i ≥ 0$)
	2. Order quantity ($q_i ≥ 0$)
	3. Unit penalty for delivery shortfall ($p_i ≥ 0$)

### Timing of Events
1. Nature reveals supplier type to supplier
2. Manufacturer designs contract menu
3. Supplier selects contract
4. Supplier receives transfer payment
5. Supplier runs regular and/or backup production
6. Supplier makes delivery and pays penalty if necessary


## 3.1 Supplier's Production Decisions

### Optimization Problem
- Supplier chooses regular production size ($z$) and delivery quantity ($y$)
- Maximize expected profit: $\pi_S(X,q,p|\theta) = \max_{x\geq0}[X - cz - E(\min_{y\geq0}\{b(y-\rho z)^+ + p(q-y)^+\})]$

![[Pasted image 20241113214029.png|500]]
### Optimal Decisions (Proposition 1)
Four cases based on $p, b$, and $c/θ$:
1. $p > b, b < c/θ: z^* = 0, y^* = q$
2. $p > b, b ≥ c/θ: z^* = q, y^* = q$
3. $b ≥ p, p < c/θ: z^* = 0, y^* = 0$
4. $b ≥ p, p ≥ c/θ: z^* = q, y^* = \rho q$

### Supplier Profit Difference ($\Gamma$)
- $\Gamma(q,p) = π_S(X,q,p|h) - π_S(X,q,p|l)$
- Always non-negative
- Increases with $b, p, q, h$; decreases with $l$

## 3.2 Manufacturer's Contract Design Problem

### Optimization Program
Objective: Maximize expected profit from high and low supplier types
$$\max \{\alpha [rE\min(y_H^*,D)-X_H+p_HE(q_H-y_H^*)^+]+(1-\alpha)[rEmin(y_L^*,D)-X_L+p_LE(q_L-y_L^*)^+]\}$$

### Assumptions
- Reservation profit for both supplier types is zero
- Focus on incentive-compatible, direct revelation contracts (Revelation Principle)


# 4. Optimal Contracts Under Symmetric Information

### Key Points:
- Benchmark case: manufacturer knows supplier's reliability type
- Incentive compatibility constraints not required
- Individual rationality constraints binding at optimality

### Proposition 2: Optimal Contract
![[Pasted image 20241113214424.png|500]]

### Results:
- Supplier's profit is zero ($π̌^*_H = π̌^*_L = 0$)
- Manufacturer extracts entire channel profit

### Channel Loss Definition:
$Δ(X,q,p) = π^*_{C|L} - π_{C|L}(X,q,p)$
- Measures profit loss when contract differs from optimal

### Notes:
- $π̌_{M|i}$: Manufacturer's profit with supplier type i
- $π̌_i$: Supplier's profit of type i
- $π_{C|i}$: Channel's profit with supplier type i
- $π^*_{C|i}$: Channel's optimal profit with supplier type i


# 5. Optimal Contracts Under Asymmetric Information

## 5.1 Fundamental Trade-Off
- Manufacturer's objective: Maximize profit
- High-type supplier's incentive compatibility constraint binding
- Low-type supplier's individual rationality constraint binding
- Trade-off: Incentive payment vs. channel loss

## 5.2 Optimal Contracts (Proposition 3)
![[Pasted image 20241113214945.png|500]]
## 5.3 Effect of Asymmetric Information
- Counterintuitive risk management in Region II
- No orders from low-type in Regions IV and V
- Quantity received stochastically smaller under asymmetric information

## 5.4 Informational Rent and Channel Loss
- Informational rent ($Δ$): Incentive payment to high-type supplier
- Channel loss ($Γ$): Loss from deviating from symmetric information optimal contract
- Trade-off between $Δ$ and $Γ$ in different regions
- Region II: Mix of informational rent and channel loss
- Other regions: Either informational rent or channel loss, not both


# 6. Values of Information and Backup Production

### Value of Information Definition
- Difference between optimal expected profits under symmetric and asymmetric information

### Value of Information for Different Entities
1. Manufacturer: $\alpha\gamma + (1-\alpha)\delta$
2. Low-type supplier: 0
3. High-type supplier: $-\gamma$
4. Channel: $(1-\alpha)\delta$

## 6.1 Value of Information and Backup Production Cost ($b$)
- Most pronounced for moderate $b$ values
- Extreme $b$ values: manufacturer offers same contract to both types

## 6.2 Value of Information and Unit Revenue ($r$)
- Nonmonotone for channel and high-type supplier
- Increasing for manufacturer
- Jumps at $r̄$ and $r̂$

## 6.3 Value of Backup Production
- Manufacturer and channel: decreasing in b, increasing in r, nonnegative
- High-type supplier: nonmonotone in b, can be negative

## 6.4 Effect of Information on Value of Backup Production
- Can be larger or smaller under symmetric information
- Small b: greater value under asymmetric information
- Moderate b: diminished value under asymmetric information


# 7. Sensitivity Analysis

## 7.1 Sensitivity to Supplier Reliabilities
- Increasing both θh and θl (constant gap):
	- Value of information increases in regions I, IV, V
	- Value of information decreases in regions II, III
	- Value of backup production for manufacturer decreases

## 7.2 Sensitivity to Reliability Gap
- Increasing θh (fixed θl):
	- Value of information for manufacturer increases
	- Value of backup production for manufacturer decreases
	- Absolute value of backup production for high-type supplier increases

## 7.3 Sensitivity to Fraction of High-Type Suppliers (γ)
- Value of information:
	- Increases in regions I, III
	- Decreases in regions IV, V
	- Can increase or decrease in region II
- Value of backup production:
	- Decreases in region I
	- Increases in regions II, IV

## 7.4 Sensitivity to Manufacturer's Contracting Flexibility
Three manufacturer types:
1. Informed manufacturer
2. Partially informed and discriminating manufacturer
3. Partially informed and nondiscriminating manufacturer
