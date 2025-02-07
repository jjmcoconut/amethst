Felipe Caro, Charles J. Corbett, Tarkan Tan, Rob Zuidwijk

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

---


# Script:

### Deep Dive: The Complexity of Carbon Footprinting in Supply Chains

Today, we’re tackling one of the trickiest parts of carbon footprinting—how multiple companies share responsibility for the same emissions.
How do we measure that fairly? And how do we actually encourage everyone to reduce their impact when the responsibility isn’t just one company’s burden?
This is a big deal. Companies are under increasing pressure to be sustainable. Think about major retailers like Walmart and Tesco. Walmart set a goal to cut 20 million metric tons of greenhouse gases across their entire supply chain. Tesco, on the other hand, aims to be completely carbon neutral by 2050.
Ambitious goals. But achieving them is not as simple as just measuring emissions and cutting them. That’s where today’s discussion comes in.
The Problem: Shared Responsibility and Double Counting
To guide our discussion, we’re looking at a fascinating paper called Double Counting in Supply Chain Carbon Footprinting. The researchers built a mathematical model to explore this issue. And it all comes down to a fundamental question: How do we fairly assign responsibility for shared emissions?

And once we figure that out, how do we motivate companies to actually take action, instead of just pointing fingers?
Let’s break it down.

### Joint Production of Emissions – What Does That Mean?

Think about this: multiple companies influence the emissions from a single process—even if they’re not directly involved. This happens all the time in modern supply chains.
Let me give you a real-world example.

Example 1: Construction Industry

Imagine a company that manufactures prefabricated roof trusses. They use advanced engineering to minimize wood waste, which helps the builder save money on materials and labor.
But here’s the catch:
- The supplier has to invest in higher upfront costs for better engineering.
- The builder benefits from lower waste and faster construction.
Both the supplier and the builder influence the emissions from the same process—building the roof. So, who’s responsible for those emissions?

Example 2: Paint Manufacturers

Let’s switch industries—paint manufacturing.
Many companies are moving from solvent-based paints to water-based paints to reduce emissions. Sounds great, right?
But there’s a trade-off.
- The paint supplier reduces emissions.
- The customer—the person using the paint—might have to buy all new equipment because water-based paints can be more corrosive.
Again, multiple companies are involved in the same emissions shift.

### The Scale of the Problem

Research shows that companies spend up to 68% of their budget on indirect goods and services—things like logistics, travel, and facility management. These are areas where joint production of emissions happens all the time.
We categorize emissions using three “scopes” from the Greenhouse Gas Protocol:
- Scope 1: Direct emissions from owned operations (like a factory burning fuel).
- Scope 2: Indirect emissions from purchased energy.
- Scope 3: All other indirect emissions (supply chain, travel, etc.).
Sounds simple, right? But these scopes get messy when companies are jointly responsible for emissions.

Take employee travel:
- A business trip is a Scope 3 emission for the employer.
- But for the airline? It’s Scope 1.
Same emissions, different labels.

Here’s a staggering fact:
- On average, only 14% of an industry’s emissions fall under Scope 1.
- Even when we add Scope 2, we’ve only covered 26%.
- That means 74% of emissions fall under Scope 3—where emissions responsibility is shared and complicated.
Right now, most companies avoid double counting at all costs. It makes reporting messy.
But here’s the radical idea: What if double counting could actually help us reduce emissions?
Sounds counterintuitive, right? Stick with me.

### Double Counting as a Motivational Tool

One of the key principles in economics is that people are more likely to act when they feel the full weight of their choices.
So what if, instead of dividing responsibility, we actually over-allocate responsibility in supply chains?

Think of it like a group project.
- If you and your partner know the other person will slack off, you might not put in full effort either.
- But if both of you are held fully responsible, you’re more likely to step up.

That’s the core idea behind strategic double counting. To tackle this issue, we need a structured approach. That’s where the Joint Production Model comes in. The total carbon footprint is broken down into individual components for separate processes. Each process can be influenced by multiple firms, making responsibility more complex.

To address this, researchers suggest two perspectives:
1. **Social Planner Approach**
    - The social planner assigns emissions responsibility and charges firms accordingly.
    - Firms then adjust their abatement efforts based on these allocations.
2. **Carbon Leader Approach**
    - A single firm—called the carbon leader—takes responsibility for the entire supply chain’s emissions.
    - The carbon leader offsets all emissions but recoups costs from supply chain partners.

**Key Assumptions in the Model:**
- The supply chain is already operational, meaning there’s a baseline scenario.
- Emission reduction efforts do not interfere with core business revenues.
- Companies have already implemented the most profitable abatement measures.

Now, let’s look at how we define the problem mathematically.
- We have $n$ firms and **i** processes.
- The emissions come from **joint production**, meaning multiple firms contribute to the same footprint.
Moving forward, we will analyze the **Social First-Best Solution**, which determines the **optimal effort** for emissions reduction.

The goal is to maximize total firm profit while accounting for the societal cost of carbon emissions. This is represented by the maximization problem:
$$z^S = \max_{e_1,\dots,e_N}\sum_{n=1}^N V_n(e_n) - p^S  \sum_{i=1}^I f_i(e)$$
where $e_n$ represents the carbon abatement efforts of firm $n$, and $V_n(e_n)$ is their profit function, which is concave and decreasing. The term $p^S$ represents the societal cost of carbon, and $f_i(e)$ captures the total carbon footprint from different processes. The matrix $B$ maps firms to the processes they influence.

Now, let’s move to Carbon-Based Payments. In practice, the carbon price, $p$, may differ from the social cost of carbon, $p^S$. Firms make carbon-based payments, denoted as $h_n(f)$. Two key concepts are important here: footprint balance and double counting. Footprint balance ensures that the sum of marginal payments over all firms equals the carbon price, while double counting occurs when payments exceed the correct level.

Finally, we introduce two key constraints. The first is Individual Rationality, which ensures that firms participate voluntarily:
$$V_n(e_n) - h_n(f(e)) ≥ \bar{\pi}_n$$
where $\bar{\pi}_n$ is the firm's reservation profit. The second constraint is Incentive Compatibility, which ensures that firms choose abatement levels that maximize their net profit:
$$e_n \in \arg\max\{ V_n(e_n) - h_n(f(e))\}$$
These principles help align firm incentives with societal goals in reducing carbon emissions.

### 4. The Social Planner Perspective

Now, let's shift our focus to the **Social Planner**—a central authority that allocates emissions and imposes costs while allowing voluntary internal payments between firms.
$$h_n(f) = p\hat{f}_n(f) + g_n(f)$$
Here, $p$ is the carbon price, $\hat{f}_n(f)$ is the firm’s allocated emissions, and $g_n(f)$ represents voluntary compensation.

**Key Takeaways**
1. If firms cannot **double count** emissions, achieving the optimal equilibrium is impossible.
2. **Linear payment rules** ensure that each firm internalizes the **full societal cost**.
3. If double counting is prohibited, a **higher carbon price** than $p^S$ may be necessary.

### 5. Decentralized Supply Chains and the Role of a Carbon Leader

Now, what happens when we don't have a central planner? This brings us to the concept of a **Carbon Leader**—a single firm that takes responsibility for all supply chain emissions and uses **internal payments** to incentivize other firms.

**Two Scenarios:**
-  **Contracting on Efforts (PE):** The carbon leader directly **observes and contracts** firms’ abatement efforts.
-  **Contracting on Emissions (PF):** Payments are based on **total emissions** rather than effort levels.

**Key Insights:**
- When **double counting** is permitted, the **Carbon Leader** can reach the first-best outcome.
- The leader must **lead by example**, showing commitment to emissions reduction.
- The carbon price $p$ set by the leader may differ from the societal cost $p^S$, leading to deviations in total effort levels.

### 6. Practical Illustration: Eastman Chemical

Let’s bring this theory into the real world with a case study of **Eastman Chemical**.
In 2009, Eastman’s **European division** introduced a new product transportation method, shipping products in molten instead of solid form.
**The Trade-off:**
- **Molten bulk shipping increases transport emissions.**
- **But it decreases total emissions across the supply chain.**
- Coordination was required between Eastman and customers to optimize the impact.

**Results as a Carbon Leader**
- Initial changes led to a **10% emissions reduction**.
- With better demand-sharing, reductions improved to **15%**.
- By assuming a carbon price of **€30/ton**, Eastman acted as a carbon leader, proving that leadership can drive significant impact.

**Social Planner vs. Carbon Leader**
- Without double accounting, the required price must be **higher than p^S** to correct underinvestment.
- Delegating **double counting** to a leader ensures better alignment with first-best solutions.

### Conclusion

**To wrap things up, here are our key takeaways:
2. **Carbon neutrality alone is insufficient**—it does not necessarily lead to optimal emissions abatement.
3. **Double counting is necessary** to achieve the best effort levels across firms.
4. **Optimizing the carbon price isn’t enough**—firms need to internalize their true impact.
5. **A credible Carbon Leader can bridge the gap** by assuming responsibility and delegating double counting.

Ultimately, **double accounting allows us to fairly assign responsibility and drive meaningful emissions reductions.**

Thank you for your attention. I now welcome any questions you may have.