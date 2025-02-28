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

