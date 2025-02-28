Felipe Caro, Charles J. Corbett, Tarkan Tan, Rob Zuidwijk

<span style="color:rgb(0, 176, 80)">Review:</span> [[2025-02-07 Meeting]]

# 1. Introduction

- __Main Challenge__: Multiple companies share responsibility for the same emissions.
- __Key Question__: How do we fairly assign responsibility and encourage reductions?
- Examples of Corporate Goals:
	- Walmart → Reduce 20M metric tons of GHG emissions.
	- Tesco → Carbon neutral by 2050.

__The Problem: Shared Responsibility & Double Counting__
- Core Issue: Multiple firms influence emissions from the same process.
- Examples:
	- Construction Industry → Roof truss manufacturer vs. builder (shared impact).
	- Paint Manufacturing → Supplier (reduces emissions) vs. customer (faces equipment costs).

__Measuring Carbon Emissions (Scopes)__
- Scope 1 → Direct emissions (e.g., factory burning fuel).
- Scope 2 → Indirect emissions from purchased energy.
- Scope 3 → Other indirect emissions (e.g., supply chain, travel).
- Scope 3 Problem → 74% of emissions fall here, making responsibility unclear.

__Double Counting: Problem or Opportunity?__
- Traditional view: Double counting makes reporting difficult.
- New Perspective: Strategic double counting can motivate companies to act.
- Economic Principle: Over-allocating responsibility encourages greater effort (like a group project).

__Key Question__: How do we fairly assign responsibility and encourage reductions?

# 3. Model

**Joint Production Model**
- Total footprint decomposed into separate components for individual processes
- Each process can be influenced by any combination of firms

**Two Perspectives**
1. Social Planner:
	- Allocates emissions to individual firms
	- Charges for those emissions
2. Carbon Leader:
	- Offsets all supply chain emissions
	- Recoups costs from supply chain partners

__Assumptions__
- Supply chain already operating (baseline scenario)
- Abatement efforts don't affect core business revenues
- Firms have exhausted profitable abatement initiatives

__Key Components__
- $n$ firms $(n ∈ N = \{1,...,N\})$
- $i$ processes $(i ∈ I = \{1,...,I\})$
- Joint production of emissions across firms and processes

__Social First-Best Solution__
- $z^S = \max_{e_1,\dots,e_N}\sum_{n=1}^N V_n(e_n) - p^S  \sum_{i=1}^I f_i(e)$
	- $p^S$: Societal cost of carbon
	- $e_n$: Carbon abatement efforts by firm $n$
	- $V_n(e_n)$: Firm $n$'s profit (concave, decreasing)
	- $f_i(e)$: Total footprint of process $i$
		- $B: N \times I$ matrix mapping firms to processes they influence

__Carbon-Based Payments__
- $p$: Carbon price (may differ from $p^S$)
- $h_n(f)$: Carbon-based payment by firm $n$
- Key Concepts
	1. Footprint balance: $\sum_{n=1}^N \partial h_n/\partial f_i = p$ for all $i$
	2. Double counting: $\sum_{n=1}^N \partial h_n/\partial f_i > p$ for some $i$

__Constraints__
1. Individual rationality: $V_n(e_n) - h_n(f(e)) ≥ \bar{\pi}_n$
2. Incentive compatibility: $e_n \in \arg\max\{ V_n(e_n) - h_n(f(e))\}$

# 4. The Social Planner Perspective

- Social planner allocates emissions and imposes costs on firms
- Firms choose efforts simultaneously
- Voluntary internal payments between firms allowed $(g_n(f))$

__Carbon-Based Payments__
$$h_n(f) = p\hat{f}_n(f) + g_n(f)$$
- $p$: Carbon price
- $\hat{f}_n(f)$: Emissions allocated to firm n
- $g_n(f)$: Aggregate voluntary payment by firm n

__Key Findings__
1. Without double accounting, it is impossible to find carbon price $p\leq p^S$, voluntary payment $g$ such that social first-best efforts yield a Nash equilibrium
	- To achieve first-best, each firm needs to internalize the full benefits of effort, but without double accounting theses benefits must be split.
2. Linear payment rules (Payment is linear to emission)
	- Charging the full societal cost to each firm that can influence a process is the only way to achieve first-best with a linear increasing payment rule. (Double counting)
3. If double counting is not allowed:
	- Tries to compensate by charging a carbon price higher than $p^S$
	- Needs to solve a system with
		- $1+N\times I$ unknowns: price $p$, derivatives of allocation rule
		- $1+\sum_{n=1}^N m_n$ equations: footprint balance, first-order conditions 
	- May not have solution $\rightarrow$ Unable to achieve first-best

# 5. Decentralized Supply Chains with a Carbon Leader

- Single firm (carbon leader) pays for all supply chain emissions at price $p$
- Carbon leader moves first as Stackelberg leader
- Internal payments to incentivize other firms

__Two Cases__
1. Contracting on Efforts (PE)
	- Carbon leader can observe and contract on other firms' efforts
	- $$\begin{align}
		\max_{g_1,\dots,g_{N-1},e_N}&V_N(e_N)-p\sum_{i=1}^I f_i(e)+\sum_{n\neq N}g_n(e_n)\\
		s.t.\quad &V_n(e_n)-g_n(e_n)\geq \bar{\pi}_n,\quad \forall n\neq N\\
		&e_n\in\arg\max \{V_n(e_n)-g_n(e_n)\}, \quad \forall n \neq N
		\end{align}$$
	- $$\begin{align}
		\max_{g_1,\dots,g_{N-1},e_N}&\sum_{n=1}^N V_n(e_n)-p\sum_{i=1}^I f_i(e)-\sum_{n\neq N}\bar{\pi}_n
		\end{align}$$ 
	- Equivalent to social planner's first-best problem with price $p$
2. Contracting on Emissions (PF)
	- Efforts not verifiable, payments contingent on emissions
	- $$\begin{align}
		\max_{g_1,\dots,g_{N-1},e_N}&V_N(e_N)-p\sum_{i=1}^I f_i(e)+\sum_{n\neq N}g_n(f(e))\\
		s.t.\quad &V_n(e_n)-g_n(e_n)\geq \bar{\pi}_n,\quad \forall n\neq N\\
		&e_n\in\arg\max \{V_n(e_n)-g_n(e_n)\}, \quad \forall n \neq N
		\end{align}$$

__Key Findings__
1. If double counting is allowed, carbon leader can achieve same outcome in both cases
	- Each firm is compensated for the costs of exerting $e_n^E$
	- Charged the carbon price $p$ per unit by which the footprints it influences deviate from the optimum
2. Carbon leader must "lead by example"
	- Exert effort to incentivize other firms

__Comparison to Social Planner Case__
1. Carbon leader pays a carbon price $p$ that is different from the societal cost $p^S$
	- If $p < p^S$, exerts less effort than first-best
2. Credible commitment
	- Social planner can achieve first-best by appointing a firm that can commit as carbon leader
	- Delegating double counting to the appointed carbon leader

# 6. Practical Illustration: Eastman Chemical

__Background__
- European division started selling products in solid and molten states in 2009
- Molten bulk shipping increases transportation emissions but decreases total emissions
- Requires significant coordination between Eastman and customers

__Assumptions__
- Eastman is carbon leader, offsetting Scope 3 emissions
- Joint effort required for emissions reduction

__Results (Carbon Leader)__
1. Initial scenario:
	- ![[Pasted image 20250204160147.png|400]]
2. With process improvements (sharing demand information):
	- ![[Pasted image 20250204160251.png|400]]
- With 4 customers and p = €30/ton:
	- Initial: ~10% reduction
	- With improvements: 15% reduction

__Social Planner Scenario__
- If double accounting is unavailable: 
	- $p = 2(1 - 1/N)p^S$ to correct underinvestment



# Conclusion

**Key Findings**
1. Carbon neutrality doesn't usually lead to optimal emissions abatement efforts
2. Double counting of emissions is usually necessary for optimal abatement efforts
3. Optimizing carbon price doesn't fully compensate for not double counting
4. With a credible leader, optimal abatement efforts can be achieved by delegating double counting to the leader

__By using double accounting we can fairly assign responsibility__
