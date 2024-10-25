Nicos Savva, Tolga Tezcan, Özlem Yıldız

**Abstract:**
- **Yardstick Competition**: Regulatory scheme for local monopolists (e.g., hospitals) linking reimbursement to performance relative to others.
- **Traditional Focus**: Incentivizes cost reduction; basis for hospital prospective reimbursement systems.
- **Study Objective**: Use a game-theoretic queueing model to examine yardstick competition in service systems aiming to reduce both costs and waiting times.
- **Key Findings**:
  - Standard cost-based yardstick competition leads to inefficiently long waiting times.
  - Modified schemes can achieve dual goals:
    - **First-Best Efficiency**: Achieved if reimbursements depend on service rates and provider-specific tolls are charged to consumers.
    - **Second-Best Efficiency**: Without tolls, a simple scheme based on average waiting time improves efficiency; easier to implement without detailed queueing knowledge.
- **Conclusion**: Numerical analysis offers insights for practical implementation in hospital emergency departments; extensions to the model are presented.

# Introduction

- **Service Monopolies**:
	- Significant in economies (e.g., hospitals constituting 5.6% of U.S. economy in 2014).
	- Regulated entities (e.g., CMS covers ~45% of hospital reimbursements).
- **Research Gap**: Less attention on regulating service monopolies compared to production monopolies.

## What Is Yardstick Competition?

- **Traditional Regulation**: "Cost-of-service" where price equals marginal cost plus transfers to ensure breakeven.
	- **Example**: Fee-for-service model by CMS pre-1983.
	- **Advantages**: Simplicity, avoids monopoly pricing, ensures production continuation.
	- **Disadvantages**: Lacks incentives for cost containment.
- **Yardstick Competition**:
	- **Mechanism**: Uses other firms' costs as benchmarks; firms are reimbursed based on average costs of peers.
	- **Incentive Structure**: Firms compete to reduce costs; optimal cost-reduction investment achieved in equilibrium (Shleifer, 1985).
	- **Implementation**: Relies on observable accounting data; doesn't require regulator to know firms' internal cost structures.

## Yardstick Competition and Waiting Times

- **Limitations of Traditional Model**:
	- Ignores waiting times; unsuitable for services where delays are costly (e.g., EDs).
- **Proposed Model**:
	- **Game-Theoretic Queueing Framework**: Multiple identical service providers (local monopolists) with profit-maximizing behavior.
	- **Regulator's Role**: Sets customer prices and transfer payments to maximize total welfare.
	- **Customers**: Heterogeneous willingness to pay; demand decreases with price and expected waiting time.
	- **Information Asymmetry**: Regulator doesn't know providers' cost functions or demand specifics.
- **Findings on Inefficiencies**:
	- **Over-Joining**: Customers don't account for the negative externality of increased waiting times (Naor, 1969).
	- **Underinvestment in Capacity**: Providers lack incentives to reduce waiting times under standard yardstick competition.
- **Modifications for Efficiency**:
	- **First-Best Solution**:
	    - **Customer Pricing**: Introduce a "toll" reflecting the externality cost.
	    - **Provider Reimbursement**: Include components based on service rates relative to peers.
	- **Implementation**: Requires accounting data and some knowledge of the queueing system.
- **Second-Best Solution (When Tolls Are Not Feasible)**:
	- **Alternative Scheme**: Reimbursement depends on average waiting times and total costs.
	- **Advantages**: Easier to implement; doesn't need detailed queueing or cost structure information.
	- **Outcome**: Achieves efficient cost and waiting-time investments; cannot fully correct customer over-joining.

## Applications

- **Healthcare Sector**:
	- **Context**: Prospective payments and yardstick competition widely used.
	- **Issue**: Excessively long ED waiting times.
	- **Contribution**: Explains underinvestment in wait-time reduction; proposes practical reimbursement modifications.
		- **Second-Best Scheme**: Practical for EDs; requires minimal additional data (average waiting times).
- **Broader Service Systems**:
	- **Potential Uses**: Government agencies (DMVs, Social Security offices), postal services, airport security.
	- **Benefit**: Provides a framework for incentivizing better performance without detailed internal data.

## Research Questions

1. Why Does Standard Yardstick Competition Fail in Service Settings?
2. How Can Yardstick Competition Be Modified to Address Waiting Times?


# Model Description

- **Three Parties Involved**:
	- **Regulator**:
	    - Oversees $N \geq 2$ identical service providers.
	    - Sets customer price $p$ and may provide transfer payments $T$.
	- **Service Providers**:
	    - Risk-neutral local monopolists.
	    - Decide on cost reduction $c$ and capacity/wait-time reduction effort $\mu$.
	    - Aim to maximize profit given $p$ and $T$.
	- **Customers**:
	    - Observe price $p$ and decide whether to seek service.
	    - Service is provided on a first-come, first-served basis.
	    - Experience waiting time $W(\lambda, \mu)$, which incurs a cost.

## Service Environment, Customer Utility, and Equilibrium Arrival Rate

**Customer Arrival Process**:
- Large population with potential service needs; aggregate arrival rate $\Lambda$ (Poisson process).
- Each customer decides to seek service or opt for an outside option (value zero).
- In emergency care, reflects patients considering a single ED.

**Customer Utility Components**:
1. **Benefit from Service** ($r$):
	 - Heterogeneous across customers.
	 - Distribution $\Theta(x)$: proportion valuing service less than $x$.
	 - $\Theta(x)$ is increasing; density $\theta(x) > 0$ for $x \geq 0$.
2. **Price of Service** ($p$).
3. **Cost of Waiting** ($t \times W(\lambda, \mu)$):
	 - $t$: cost per unit time (homogeneous across customers).
	 - $W(\lambda, \mu)$: expected waiting time, increasing in $\lambda$, decreasing in $\mu$.
	 - Reflects opportunity cost, anxiety, pain, etc.

**Utility Function**:
- $u = r - t W(\lambda, \mu) - p$.
- Customers with $u > 0$ decide to seek service.

- **Equilibrium Arrival Rate**:
  - $\lambda(p, \mu) = \Lambda \bar{\Theta}\left( p + t W(\lambda(p, \mu), \mu) \right)$.
    - $\bar{\Theta}(x) = 1 - \Theta(x)$.
  - For M/M/1 queue, simplifies to:
    - $\lambda(p, \mu) = \Lambda \bar{\Theta}\left( p + \dfrac{t}{\mu - \lambda(p, \mu)} \right)$.

**Assumptions about Waiting Time Function $W(\lambda, \mu)$**:
- $W(\lambda, \mu)$ is increasing in $\lambda$, decreasing in $\mu$.
- $W(\lambda, \mu) > W(0, \mu)$; $\lim_{\lambda \to \mu} W(\lambda, \mu) = \infty$.

## Service Provider's Profit and Actions

**Profit Function**:
- $\Pi(c, \mu | p, T) = (p - c) \lambda(p, \mu) - R(c, \mu) + T$.
	- $c$: cost per customer.
	- $\mu$: effort to reduce waiting time (capacity).
	- $R(c, \mu)$: fixed cost of reducing $c$ and increasing $\mu$.
		- Decreasing in $c$, increasing in $\mu$, jointly convex.
		- 
**Provider's Decision Problem**:
- Maximize profit over $c$ and $\mu$:
	- $\max_{0 < c \leq c_0, \mu_0 \leq \mu} \Pi(c, \mu | p, T)$.
- Requires knowledge of $R(c, \mu)$ and demand $\lambda(p, \mu)$.

## Regulator's Welfare

**Objective**:
  - Maximize total welfare: sum of customer surplus and provider profits.

**Welfare Function**:
- $S(p, c, \mu) = \Lambda \int_{p + t W(\lambda, \mu)}^\infty [x - p - t W(\lambda, \mu)] d\Theta(x) + (p - c) \lambda(p, \mu) - R(c, \mu)$.
	- First term: total consumer surplus per unit time.
	- Second and third terms: provider's profit net of transfer payment $T$.
- Under M/M/1 assumption:
    - $S(p, c, \mu) = \Lambda \int_{p + \frac{t}{\mu - \lambda(p, \mu)}}^\infty \left[ x - p - \frac{t}{\mu - \lambda(p, \mu)} \right] d\Theta(x) + (p - c) \lambda(p, \mu) - R(c, \mu)$.

**Constraints**:
- Provider must break even: $\Pi(c, \mu | p, T) \geq 0$.

## First-Best Benchmark

**Regulator's Optimization Problem**:
- Maximize $S(p, c, \mu)$ over $p \geq 0, 0 < c \leq c_0, \mu \geq \mu_0, T$, subject to $\Pi(c, \mu | p, T) \geq 0$.

**First-Best Solution**:
- **Optimal Cost Reduction ($c^*$)**:
	- $R_c(c^*, \mu^*) = \lambda^*$.
		- Marginal cost of reducing $c$ equals marginal benefit across all customers.
- **Optimal Capacity ($\mu^*$)**:
    - $R_\mu(c^*, \mu^*) = - t \lambda^* W_\mu(\lambda^*, \mu^*)$.
		- Marginal cost of increasing $\mu$ equals marginal reduction in total waiting costs.
- **Optimal Price ($p^*$)**:
    - $p^* = c^* + t \lambda^* W_\lambda(\lambda^*, \mu^*)$.
		- Price equals cost per customer plus toll for externality of increased waiting time.
- **Transfer Payment ($T^*$)**:
    - $T^* = R(c^*, \mu^*) - t \lambda^* W_\lambda(\lambda^*, \mu^*)$.
		- Ensures provider breaks even.

- **Interpretation**:
	- **Price ($p^*$)**:
		    - Customers charged more than cost ($p^* > c^*$) to internalize waiting time externality.
		    - Additional charge incentivizes optimal customer joining behavior.
	- **Provider's Break-Even**:
	    - Transfer payment $T^*$ less than investment cost $R(c^*, \mu^*)$ due to additional revenue from toll.
	- **Comparison with Zero Waiting Cost ( $t = 0$)**:
	    - If $t = 0$, waiting times are ignored, results align with models like Shleifer (1985).
	    - With positive $t$, additional considerations for waiting costs and externalities are necessary.


# Results

**Objective**: Develop regulatory schemes that achieve welfare-maximizing outcomes without requiring the regulator to know the providers' cost functions $R(c, \mu)$ or customer arrival rates $\lambda(p, \mu)$.

**Challenge**:
- **Information Asymmetry**: Providers have more accurate cost and demand information than regulators.
- **Regulator's Available Data**:
    - Audited accounting data on cost per customer $c$.
    - Investment cost $R$.
    - Average number of customers served $\lambda$.
    - Average waiting time $W$.

**Approach**: Propose four regulatory schemes—two existing and two new—that rely on observable data rather than full knowledge of cost functions or arrival rates.

## Cost-of-Service Regulation

**Mechanism**:
- Providers set capacity $\mu$ and cost per customer $c$.
- Regulator reimburses total costs:
    - **Price**: $p = c$.
    - **Transfer Payment**: $T = R(c, \mu)$.

**Issue**:
- Providers earn zero profit regardless of investment levels.
- **Result**: No incentive to invest in cost reduction or capacity expansion.
    - Leads to suboptimal service levels and inefficiencies.

## Cost-Based Yardstick Competition (Shleifer, 1985)

**Mechanism**:
- **Reimbursement Based on Peers**:
    - **Price**: $p_i = \bar{c}_i$ (average cost of other providers).
    - **Transfer Payment**: $T_i = \bar{R}_i$ (average investment cost of others).
- **Providers Compete Indirectly**:
    - Aim to reduce costs below peers to maximize profit.

**Outcomes**:
- **Without Costly Waiting Times ($t = 0$)**:
    - Achieves first-best cost reduction.
    - Providers earn zero profit in equilibrium.

**Limitations with Costly Waiting Times ($t > 0$)**:
- **Proposition 3 Findings**:
    - **Underinvestment in Capacity**:
		- Providers have no incentive to increase capacity since reimbursement isn't tied to service rates or waiting times.
    - **Potential Underinvestment in Cost Reduction**:
		- Occurs if cost reduction becomes cheaper with higher capacity.
    - **Customer Overuse**:
		- Customers face prices that don't reflect waiting time costs, leading to excessive demand.
- **Result**: Inefficient service levels and longer waiting times.

## Cost- and Capacity-Based Yardstick Competition (First-Best Solution)

**Mechanism**:
- **Price**:
    - $p_i = c_i + t \lambda_i W_\lambda(\lambda_i, \mu_i)$.
    - Includes cost per customer and waiting time externality.
- **Transfer Payment**:
    - $T_i = (\bar{c}_i - c_i)\bar{\lambda}_i + t\bar{\lambda}_i W_{\mu}(\bar{\lambda}_i, \bar{\mu}_i)(\bar{\mu}_i - \mu_i) + \bar{R}_i - t\lambda_i W_\lambda(\lambda_i, \mu_i)$.
    - Incentivizes both cost reduction and capacity expansion.

**Outcomes**:
- **Theorem 1**:
    - Unique symmetric Nash equilibrium where all providers choose $c_i = c^*$ and $\mu_i = \mu^*$.
    - Providers earn zero profit in equilibrium.

**Challenges**:
- **Implementation Difficulties**:
    - Requires charging provider-specific prices to customers, which may not be feasible in healthcare.
    - Necessitates detailed knowledge of providers' queueing systems and service rates.
- **Practicality**:
    - Complex for regulators to implement, especially in settings like hospital emergency departments.

## Free-at-the-Point-of-Care Yardstick Competition (Second-Best Solution)

**Assumptions**:
- **Fixed Customer Price**: $p = 0$ (service is free at the point of care).
- **Regulator Focuses on Transfer Payments**.

**Mechanism**:
- **Transfer Payment**:
    - $T_i = t(\bar{W}_i - W_i)\bar{\lambda}_i + \bar{R}_i + \bar{c}_i \lambda_i$.
    - Incentivizes providers to reduce waiting times relative to peers.
    - Providers keep savings from cost reductions.

**Outcomes**:
- **Theorem 2**:
    - Unique symmetric Nash equilibrium with providers choosing $c_i = c^*_o$ and $\mu_i = \mu^*_o$ (second-best levels).
    - Providers earn zero profit in equilibrium.

**Advantages**:
- **Simpler Implementation**:
    - Does not require charging customers or knowing queueing disciplines.
    - Only needs data on average waiting times and total costs.
    - Easier for regulators to monitor and enforce.

**Limitations**:
- **Requires Knowledge of Waiting Cost ($t$)**:
    - Regulator must estimate patients' cost of waiting to set appropriate incentives.
- **Efficiency Loss**:
    - Cannot fully eliminate inefficiencies due to suboptimal customer demand (overjoining).
    - Achieves second-best, not first-best, outcomes.
