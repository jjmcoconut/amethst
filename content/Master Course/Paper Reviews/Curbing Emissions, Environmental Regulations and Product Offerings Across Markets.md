Zheng Han, Bin Hu, Milind Dawande

# 1. Introduction

__CAFE vs. Trump__
- **2009:**
    - President Obama proposed fuel economy regulation through the Corporate Average Fuel Economy (CAFE) program.
    - Goal: Achieve an average fuel economy of about 50 MPG by 2025.
- **2016:**
    - A midterm review found that automakers were largely on track to meet the partial targets of the Pavley/CAFE standards.
- **2018:**
    - The Trump administration announced a freeze of CAFE standards at the 2019 level.
    - Major automakers opposed this proposal, advocating for continued annual improvements and urging President Trump to reconsider.
- **July 2019:**
    - Four major automakers (Ford, Honda, Volkswagen, BMW) voluntarily agreed with California to meet CARB fuel economy targets.
    - This deal dealt a significant blow to the Trump proposal and prevented a potential split in the U.S. auto market.
- **2020:**
    - The Trump administration abandoned the plan to freeze CAFE standards.
    - A new plan was introduced, requiring a 1.5% annual improvement in fuel economy.

**Regulatory Strategy**
- U.S. auto market as a “split market”: 
	- Two regulatory bodies (CAFE and Trump) with differing standards.
- Research Questions:
	- When is market unification attainable?
	- Does unification reduce total emissions?
	- What strategies (horizontal vs. vertical negotiations) can unify a split market?
- ![[Pasted image 20250226181058.png]]

# 3. Model

![[Pasted image 20250226182508.png|500]]
__Regulator__
- Governs market by establishing minimum efficiency standard $s_i$
- $R_2$ (Trump): Sets $s_2=0$
- $R_1$: Considers marginal environmental impact $h_1$ using benchmark $b$
	- Environmental impact: $h_1(b-e)$

__Firm__
- Decides whether to
	- D(differentiation): Offering different products
	- U(unification): Offering unified products
	- S(single market): Only offering products in $M_2$
- Decides price $p_i$, product efficiency level $e_i$
- Incurs fixed setup cost $r$, per-unit variable cost $ce_i$

__Customer__
- Customer valuation $\sim U[0,\bar{u}]$
- Marginal efficiency bonus $\gamma e$
- Net utility: $u-p+\gamma e$

__Firm's Decision (given $s_1$)__

| Size           | Firm's strategy     |
| -------------- | ------------------- |
| $s_1$ small    | U (unification)     |
| $s_1$ moderate | D (differentiation) |
| $s_1$ large    | S (single market)   |

__Regulators' Decision__
$R_2$: $s_2=0$ always
$R_1$'s utility function: Consumer utility in $M_1$ + Entire environmental impact
- $$\int_0^{\bar{u}}\max(0,x-p^*+\gamma s_1)dx=\begin{cases}
  \frac{m_1}{8\bar{u}}(\bar{u}-(c-\gamma)s_1)^2 & \text{if }U,D\\
  0 & \text{if } S
  \end{cases}$$
- $$R_1\text{ env impact}=\begin{cases}
  h_1(b-s_1)\frac{m_1}{2\bar{u}}(\bar{u}-(c-\gamma)s_1) & \text{if }U,D\\
  0 & \text{if } S
  \end{cases}$$
- $$R_2\text{ env impact}=\begin{cases}
  h_1(b-s_1)\frac{m_2}{2\bar{u}}(\bar{u}-(c-\gamma)s_1) & \text{if }U\\
  -\frac{1}{2}h_1bm_2 & \text{if } D,S
  \end{cases}$$

| Strategy | Utility Function                                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------------ |
| U        | $\frac{m_1}{8\bar{u}}(\bar{u}-(c-\gamma)s_1)^2-h_1(b-s_1)\frac{m_1+m_2}{2\bar{u}}(\bar{u}-(c-\gamma)s_1)$                |
| D        | $\frac{m_1}{8\bar{u}}(\bar{u}-(c-\gamma)s_1)^2-h_1(b-s_1)\frac{m_1}{2\bar{u}}(\bar{u}-(c-\gamma)s_1)-\frac{1}{2}h_1bm_2$ |
| S        | $-\frac{1}{2}h_1bm_2$                                                                                                    |


__Neutral Arbitrator__
Maximizes: Entire consumer utility + Entire environmental impact
$$s_a^*=\arg\max_{s_1}\frac{m_1+m_2}{8\bar{u}}(\bar{u}-(c-\gamma)s_1)^2-h_1(b-s_1)\frac{m_1+m_2}{2\bar{u}}(\bar{u}-(c-\gamma)s_1)$$
- $s_a^*=s_{1,D}^*$
- U emission < A emission < D emission

# 4. Negotiation
![[Pasted image 20250227161603.png]]

__Reason of Negotiation__
- Negotiate between regulators
- Negotiation to avoid D(differentiation)

__Horizontal: Exact vs Baseline__
- $s_e$: Exact global standard, both regulators must use this value
- $s_b$: Baseline global standard, some regulators may choose higher standard
	- $s_b^*$: Effective global standard that $R_1$ will choose
- Result: $s_b^*>s_e^*$

__Vertical Negotiation__
- $s_v$: Global standard negotiated between firm and $R_1$
- $s_v^*<s_b^*<s_e^*$ & emissions are smaller than D if $h_1$ is sufficiently high
	- ![[Pasted image 20250226194012.png|500]]
	- Vertical negotiation is easier than horizontal however has higher emissions

__Result:__ If facing potential split-market try horizontal negotiation first then vertical if horizontal did not work

---
## **Slide 1: Title Slide**

**Script:**  
Good [morning/afternoon], everyone. My name is [Your Name], and I am excited to present our work on "Curbing Emissions: Environmental Regulations and Product Offerings Across Markets." 
This research, conducted by Zheng Han, Bin Hu, and Milind Dawande, explores the intersection of environmental regulations and firms’ product decisions in markets with differing regulatory standards.

The study is particularly inspired by the events surrounding the Corporate Average Fuel Economy (CAFE) standards in the United States during the Trump administration and the resulting regulatory uncertainty. 
We model these regulatory interactions to understand their implications for emissions and market behavior.

---

## **Slide 2: Introduction – CAFE vs. Trump**

To provide context, let's look at the regulatory landscape in the U.S. auto industry.

- The **California Air Resources Board (CARB)** has long implemented stricter vehicle efficiency standards compared to the **federal EPA (Environmental Protection Agency)** standards.
- The Trump administration’s **2018 proposal to freeze federal efficiency standards** widened the gap between the two, potentially splitting the U.S. market.
- Automakers, who traditionally aligned with CARB to maintain a unified market, faced a dilemma: comply with CARB’s stricter rules or take advantage of the federal rollback and offer different vehicles in different states.

This situation motivates our **three research questions:**

1. When is market unification attainable?
2. Does unification reduce total emissions?
3. What strategies—horizontal vs. vertical negotiations—can unify a split market?

Our study addresses these questions using a **game-theoretic model** involving two regulators, a firm, and consumers.

---

## **Slide 3: Regulatory Strategy**

Here’s a simplified structure of our regulatory strategy:

- We model **two regulators**:
    - **R1 (CARB-like regulator)** cares about emissions and sets efficiency standards based on environmental impact.
    - **R2 (Federal EPA under Trump)** does not regulate emissions and sets no standard ($s_2=0$).
- A firm chooses whether to:
    - Differentiate its products across markets (**D**).
    - Offer a single, unified product (**U**).
    - Exit the regulated market and only sell in the lenient one (**S**).

Our goal is to determine under what conditions unification occurs and whether it benefits overall emissions.

---

## **Slide 4: Model Overview – Regulator's Decision**

Regulator **R1** aims to curb emissions by setting a standard **$s_1$**, considering both:

- **Consumer utility** in its jurisdiction.
- **Total environmental impact** across both markets.

The model incorporates:

- A **benchmark efficiency level** ($b$) for emissions.
- **Perceived environmental impact ($h_1$)** that reflects R1’s concern for pollution.
- The firm’s decision-making process in response to regulatory conditions.

Meanwhile, **R2 always sets $s_2 = 0$**, reflecting the Trump administration’s decision to freeze standards.

---

## **Slide 5: Model Overview – Firm’s Decision**

The firm determines its strategy based on regulatory constraints and production costs.

- It **incurs a fixed setup cost ($r$)** to introduce a product and a **per-unit cost ($c e_i$)** for efficiency improvements.
- It decides between three strategies:
    1. **U (Unification):** Sell one model meeting the stricter standard.
    2. **D (Differentiation):** Sell different models with different efficiency levels.
    3. **S (Single Market):** Withdraw from the regulated market and sell only in the less-regulated one.

Consumers value efficiency, but increasing efficiency costs the firm. Thus, their choice hinges on whether unifying production is **more profitable than differentiating products**.

---

## **Slide 6: Firm’s Optimal Strategy**

The firm’s optimal response depends on **$s_1$** (set by R1).

|Size of $s_1$|Firm's Strategy|
|---|---|
|Small $s_1$|Unification (U)|
|Moderate $s_1$|Differentiation (D)|
|Large $s_1$|Single Market (S)|

- If **$s_1$ is low**, the firm unifies the market.
- If **$s_1$ is moderate**, differentiation occurs, leading to a split market.
- If **$s_1$ is too high**, the firm exits R1’s market altogether.

This highlights the tradeoff regulators face: **setting too high a standard can drive firms away**, while **too low a standard fails to curb emissions**.

---

## **Slide 7: Impact on Emissions**

We assess total emissions in different cases:

- **In a split market (D), emissions are higher** because firms sell less efficient cars in non-regulated states.
- **In a unified market (U), emissions are lower** as all cars must meet the stricter standard.
- **If the firm exits the regulated market (S), emissions depend on market size.**

This suggests that unification is environmentally beneficial **if regulators set feasible standards** that firms comply with instead of exiting.

---

## **Slide 8: Market Unification Strategies**

How can regulators **prevent a split market** and unify efficiency standards?

Two strategies exist:

1. **Horizontal Negotiation (Regulator-to-Regulator):**
    
    - R1 and R2 negotiate a **global standard** to avoid a split market.
    - This is preferred but difficult since regulators have **different incentives**.
    - **Results:** Works best when R1 offers sufficient concessions to R2.
2. **Vertical Negotiation (Regulator-to-Firm):**
    
    - R1 directly negotiates with firms to **voluntarily adopt stricter standards**.
    - This happened in reality when **California negotiated with automakers** despite federal resistance.
    - **Results:** More feasible but results in slightly higher emissions than full horizontal agreement.

---

## **Slide 9: Key Findings**

1. **Market unification is attainable** under the right conditions.
2. **Unification generally reduces emissions** compared to a split market.
3. **Horizontal negotiations (between regulators) are ideal**, but if they fail, **vertical negotiations (with firms) can work as a fallback**.
4. **Setting efficiency standards too high risks market exit**, which may increase overall emissions.

These insights are particularly relevant for policymakers designing regulatory frameworks in industries with **global supply chains**.

---

## **Slide 10: Conclusion and Takeaways**

In conclusion:

- If a **split market threatens**, policymakers should **prioritize horizontal negotiations** for a shared standard.
- If **horizontal negotiation fails**, regulators can **leverage market power** by negotiating with firms directly.
- **Unification helps curb emissions**, but **moderate efficiency targets** are crucial to keeping firms engaged.

This model applies beyond the auto industry, offering insights into global **environmental policy negotiations, trade regulations, and international market dynamics**.