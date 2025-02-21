Gérard P. Cachon, Robert Swinney

# Introduction

**Overview**
- **Topic:** Fast Fashion: Quick Response, Enhanced Design, and Strategic Consumer Behavior
- **Focus:** How fast fashion (e.g., Zara, H&M, Benetton) transforms production and influences consumer purchasing decisions
- **Key Question:** Why is fast fashion so successful?

**Fast Fashion Basics**
- **Definition:**
    - Business model capturing latest trends and delivering them quickly and cheaply.
- **Core Components:**
    - **Quick Response:** Dramatically shorten the design-to-retail lead time.
    - **Enhanced Design:** Invest in trendy, high-value products to boost consumer willingness to pay.

 **Quick Response Strategies**
- **Method:**
    - Place small initial orders; use real-time data to replenish inventory.
- **Example:**
    - Zara manufactures locally (Europe/North Africa) → higher costs but rapid turnover.
    - New styles every 2 weeks.
- **Benefits:**
    - Reduced unsold inventory risk.
    - Minimizes markdowns (clearance sales).
    - Consumers less likely to wait for discounts.

**Enhanced Design Strategies**
- **Method:**
    - Create “hot” garments that reflect current trends.
- **Impact:**
    - Increases immediate consumer utility.
    - Higher perceived value → less incentive to delay purchase.
    - Creates urgency (“buy now” effect).

**Overview of the Four Operational Systems**

|                     | **Normal Design**  | **Enhanced Design** |
| ------------------- | ------------------ | ------------------- |
| **Slow Production** | Traditional (T)    | Enhanced Design (D) |
| **Quick Response**  | Quick Response (R) | Fast Fashion (F)    |

- **Traditional System (T):**
    - Long production lead times, standard design.
    - Resembles a classic newsvendor model.
- **Quick Response System (Q):**
    - Standard design but with significantly reduced lead times.
- **Enhanced Design System (D):**
    - Superior design capabilities, higher consumer value; long lead times.
- **Fast Fashion System (F):**
    - Combines quick response and enhanced design (like Zara/H&M).

# Traditional System
- **Model Setting:**
    - **Firm:** Sells one product over a finite season.
    - **Demand:** Uncertain, modeled as a continuous random variable $N$ with distribution $F$ and mean $\mu$.
    - **Consumer Valuation:** Homogeneous value $v$.
- **Firm’s Decisions:**
    - Procure inventory level $q$ at cost $c$ before the season starts.
    - Set a selling price $p$ to maximize expected profit.
    - Unsold inventory is cleared at salvage price $s$ (where $s<c$).
- **Consumer Behavior:**
    - **Strategic Consumers:** Know prices will drop at clearance.
    - **Immediate Purchase:** Surplus = $v−p$.
    - **Delayed Purchase:** Expected surplus = $\delta \phi(v−s)$
        - $\delta$: Discount factor (loss of future utility)
        - $\phi$: Perceived probability of obtaining the product at clearance.
    - **Equilibrium Condition:** Consumers purchase early if $v−p>\delta \phi(v−s)$
- **Equilibrium Concept:**  
	-  Simultaneous game:
	    - Firm: Chooses $q$ and $p$ to maximize expected profit.
	    - Consumers form rational expectations about the likelihood of a clearance sale.
	- Homogeneous customers
		- All customers buys at full cost $p$ or waits for clearance $s$
		- $s<c$ & Clearance: firms orders 0 inventory
		- Only option: All customers purchasing full cost

# Operational Systems Comparison

| System                  | Key Features                      | Profit Equation                           | Price Outcome                                                |
| ----------------------- | --------------------------------- | ----------------------------------------- | ------------------------------------------------------------ |
| **Traditional (T)**     | Long lead times, standard designs | $\pi_T=(p−s)S(q)−(c−s)q$                  | $p_T^*$                                                      |
| **Quick Response (Q)**  | Fast replenishment, cost $c_Q$    | $\pi_Q=(p−c)\mu−c_QL(q)−(c−s)I(q)$        | $p_Q^*>p_T^*  ⟺  p_T^*>c+c_Q$                                |
| **Enhanced Design (D)** | $+m$  value, $+c_D$  cost         | $\pi_D=(p−s)S(q)−(c+c_D−s)q$              | $p_D^*>p_T^*$                                                |
| **Fast Fashion (F)**    | Combines $Q$ and $D$              | $\pi_F=(p−c−c_D)\mu−c_QL(q)−(c+cD−s)I(q)$ | $p_D^*>c+c_D+c_Q$$\Rightarrow p_F^*>max⁡(p_D^*,p_Q^*,p_T^*)$ |


# The Interaction of Enhanced Design and Quick Response

__Key Question__
Are enhanced design and quick response complements  or substitutes?

**Complementarity Condition**
$$\pi_F − \pi_T ≥ (\pi_Q − \pi_T) + (\pi_D − \pi_T) \iff \pi_F − \pi_Q ≥ \pi_D − \pi_T$$

 **Key Findings**
- No cost of enhanced design: $c_D=0$
	- Nonstrategic consumers $\delta=0$
		- Everyone buys at full cost
			- Increase in profit per unit increases with enhanced design
			- Quick response eliminates stockouts -> Able to sell more
		- Complementary
	- Strategic customers $\delta>0$:
		- Adding enhanced design on traditional system generates smaller increase in price
			- Firms need to lower price if customers have higher motivation to wait clearance
			- Quick response lowers probability of leftovers (clearance)
		- Complementary
- Costly enhanced design: $c_D = m$
	- Firms gain nothing from adding enhanced design to quick response
	- Adding enhanced design to traditional system benefits
		- Selling fewer units at a higher price
	- Substitutes
- Substitution effect increases as $c_D$ increases
	- ![[Pasted image 20250219173304.png|400]]

# Numerical Study

 **Key Findings (12,150 Simulations)**
- **Complementarity Prevalence**:
    - 93.9% of cases: Are complements 
    - Substitution cases (6.1%): Occurred with high $c_D$ + low $c_Q$ 
- **System Performance**:
    - Fast fashion was optimal in 74.5% of cases.
    - Even with $c_D ≥ m$ (ED seemingly unprofitable), fast fashion was optimal in 41% of such cases.
- **Complementarity Drivers**:
    - Low ED cost ($c_D$)
    - High strategic customers $\gamma$
    - Moderate QR Cost ($c_Q$)

**Design-Dependent Clearance Prices**
- **Model Change**: Clearance price in ED/fast fashion systems = $s + \gamma m$ 
- **Conflicting Effects**:
    - Higher clearance price → ↑ inventory → ↑ clearance risk → ↓ early purchases.
- **Key Results**:
    - Fast fashion value ↓ as $\gamma$ ↑ 


---

Good morning. 
This paper explains how fast fashion systems-like those employed by brands such as Zara and H&M-are not only transforming production but also influencing the way consumers make purchasing decisions.

In the traditional retail environment, companies planned months in advance. 
However, the fast fashion model has upended this approach. 
By combining rapid production cycles with a keen sense of emerging trends, fast fashion brands can get new, “hot” products to market in a matter of weeks. 
So the main point is "Why is fast fashion so successful?" and that's what we'll be covering.

**What is Fast Fashion? (Approx. 3 minutes)**

Let’s begin by defining fast fashion. 
At its core, fast fashion is a business model designed to capture the latest trends and deliver them to consumers as quickly and inexpensively as possible. 
Two critical components enable this model. 
The first is **quick response**-the ability to dramatically shorten the time between design and retail. 
The second is **enhanced design**, where companies invest in developing products that are not only trendy but also hold a higher perceived value for consumers. 
Together, these elements form the backbone of fast fashion systems.

**Quick Response: Reducing Lead Times (Approx. 4 minutes)**

Quick response strategies, however, allow retailers to place initial orders for a smaller quantity and then use real-time sales data to replenish inventory as needed.
For example, Zara is well known for its quick response system. 
Zara manufactures a significant portion of its products in Europe or North Africa rather than outsourcing entirely to Asia. 
This decision increases production costs, but it dramatically reduces lead times. 
As a result, Zara can introduce new styles every two weeks. 
This not only reduces the risk of unsold inventory but also minimizes the chance that items will go on clearance. 
Consumers are less inclined to wait for a markdown because they know that products may quickly sell out.

**Enhanced Design: Creating Value and Urgency (Approx. 4 minutes)**

Enhanced design involves creating garments that capture current trends and resonate with consumer tastes. 
When a garment is designed to be “hot” and exclusive, consumers derive a higher immediate utility from buying it at full price. 
They perceive a higher value, and this reduces the risk of missing out on a product they truly desire.
Consequently, they are less willing to postpone their purchase in anticipation of a later discount. 
The higher perceived value essentially creates an “incentive to buy now.” 

**Overview of the Four Operational Systems**

To analyze fast fashion’s benefits, the paper considers four different operational systems:
- **Traditional System (T):** 
	It resembles the classic newsvendor model.
- **Quick Response System (Q):**  
    Here, the firm still uses standard designs but significantly reduces production lead times.
- **Enhanced Design System (D):**  
    In this system, the firm invests in superior design capabilities.
- **Fast Fashion System (F):**  
    This combines both quick response and enhanced design capabilities, mimicking the strategies used by retailers like Zara, Benetton, and H&M.

**Traditional System**

Let’s focus on the traditional system to understand the model’s structure.
3. **Model Setting:**  
	- We consider a single firm that sells one product over a finite season.
	- Market demand is uncertain, represented by a continuous random variable $N$ with distribution $F$ and mean $\mu$. 
	- All consumers have a homogeneous valuation $v$ for the product.
4. **Firm’s Decision:**  
	- Before the season begins—and without knowing the actual market size—the firm makes two key decisions:
	    - It procures an inventory level $q$ at a unit cost $c$.
	    - It sets a selling price $p$ aimed at maximizing its expected profit. 
	    - At the end of the season, any unsold inventory is cleared at a salvage price $s$ (with $s<c$).
5. **Consumer Behavior:**  
	- Consumers are forward-looking or “strategic.” 
	  They know that the price will eventually be lowered at the clearance sale, so each consumer must decide whether to purchase immediately at the full price $p$ or wait for the discounted clearance price $s$.
	    - The surplus from buying immediately is $v−p$.
	    - The expected surplus from waiting is $\delta\phi(v−s)$, where $\delta$ is the discount factor and $\phi$ is the perceived probability of obtaining the product at clearance.
	- In equilibrium, all consumers purchase early if $v−p>\delta \phi(v-s)$ 
6. **Equilibrium Concept:**  
	-   The interaction between the firm and its consumers is modeled as a simultaneous game:
	    - The firm chooses $q$ and $p$ to maximize expected profit.
	    - Consumers cannot not observe the exact inventory level, form rational expectations about the likelihood of a clearance sale.
	- The equilibrium is defined such that consumer beliefs about the clearance probability are correct, and all consumers purchase early at the full price.
7. **Profit Expression:**  
	- Given homogeneous customers, either all customers buys at full cost $p$ or waits for clearance $s$
		- Given $s<c$, firms orders 0 inventory, leaving all customers purchasing early as the only option
	- Under these conditions, the firm’s expected profit in the traditional system can be expressed as: $$\Pi_T(q,p)=(p−s) S(q)−(c−s) q$$where $S(q)=E[\min(q,N)]$ is the expected sales

__Quick Response__

Assumptions
- Firm can procure inventory both before and after receiving a forecast update prior to the start of the selling season. 
- The forecast update is perfectly informative and production is fast enough that all units arrive before the start of the selling season
	- Additional inventory procured after learning the realized value of market size incurs an additional cost $c_Q\geq 0$

Results
- By the same logic from the traditional system, the only possible candidate equilibrium is one in which all consumers attempt to purchase at the full price
- $$\pi_Q(q,p)=(p-c)\mu -c_QL(q)-(c-s)I(q)$$
- Because of the option to procure additional inventory at a later date, the firm procures less inventory in the initial buy than in the traditional system
- Equilibrium price is greater in the quick response system than in the traditional system ($p_Q^*>p_T^*$) if and only if $p_T^*>c+c_Q$. Otherwise, $p_Q^*=p_T^*$

__Enhanced design__

Assumptions
- Enhanced design results in a marginal increase of $m \geq 0$ to consumer value
- Every unit produced incurs an additional cost $c_D\geq 0$
- clearance price $s$ is assumed to be identical

Result
- $$\pi_D(q,p)=(p-s)S(q)-(c+c_D-s)q$$
- In equilibrium, all consumers purchase early
- Equilibrium price is greater in the enhanced design system than in the traditional system $p_D^*>p_T^*$

__Fast Fashion__

Result
- $$\pi_F(q,p)=(p-c-c_D)\mu-c_QL(q)-(c+c_D-s)I(q)$$
- In equilibrium, all consumers purchase early
- If $p_D^*>c+c_D+c_Q$, equilibrium price is greater in the fast fashion system than in all of the other systems $p_F^*>\max(p_D^*,p_Q^*,p_T^*)$



__Numerical Results__

__Complementarity Prevalence__
In **93.9% of cases**, ED and QR are **complements**—their joint adoption boosts profits beyond individual benefits.
Substitution occurred in just **6.1% of cases**, driven by **high ED costs** and **low QR costs** . 

__System Performance__
Fast fashion was optimal in 74.5% of cases—demonstrating its dominance when ED and QR synergize.
Even when ED seemed unprofitable, fast fashion was optimal in 41% of such cases. 
Why? The behavioral effect of ED enabled price increases exceeding m, offsetting costs.

