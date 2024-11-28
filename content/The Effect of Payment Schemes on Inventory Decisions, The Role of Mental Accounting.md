Li Chen, A. Gürhan Kök, Jordan D. Tong

# 1. Introduction

**Overview:**
- Newsvendor problem: Decision maker chooses inventory order quantity to meet random future demand
- Goal: Maximize expected profit from selling the product
- Common in short selling seasons with limited replenishment (e.g., fashion, high-tech)
- Human decisions often deviate from optimal solutions

**Payment Schemes:**
- Definition: Amounts and times of payment transactions for order quantity, realized sales, and leftover units
- Three payment schemes studied:
	1. O (Own financing): Pay at order time, receive revenue after demand realization
	2. S (Supplier financing): Delayed payment until after demand realization
	3. C (Customer financing): Receive advanced revenue at order time, refund for leftovers after demand

**Mental Accounting Theory:**
- Individuals mentally segregate transactions into "order-time payments" and "demand-time payments"
- Altering transactions before/after demand realization may lead to different order decisions

**Descriptive Models:**
1. Expected profit maximization
2. Loss aversion for separate order-time and demand-time payments
3. Time-discounting of demand-time payments
4. Prospective accounting: Underweighting order-time payments

**Experimental Studies:**
1. Study 1:
	- Equal overage and underage costs
	- Results: Decreasing order quantities in O, S, C order
	- Consistent with prospective accounting model
2. Study 2:
	- Mental accounting at all physical payments after demand realization
	- Results: Same ordering pattern as Study 1
	- Framing of payment scheme sufficient to induce prospective accounting behavior
3. Study 3:
	- Prospective accounting behavior is robust under high or low profit
	- Magnitudes are influenced by profit condition

**Key Findings:**
- Behavioral effect of payment scheme opposes time discounting
- Loans based on purchase cost (S) or projected revenue (C) may lower order quantity compared to no loan (O)
- Provides explanation for asymmetry of pull-to-center effect in previous studies
- Direction of pull-to-center asymmetry depends on payment scheme framing

**Implications:**
- Careful evaluation needed when designing payment schemes for supply chain financing and contracting
- Consider relative magnitude of behavioral and time-discounting effects
- Payment scheme framing influences decision-making in newsvendor problems

# 3. Models of Newsvendor Decision Making

**Problem Setup:**
- Decision maker chooses order quantity $q$ to meet future random demand $D$
- $F(·)$: cumulative distribution function for random demand
- No backlogs allowed, leftover inventory has zero salvage value
- c: Unit cost
- $p$: Selling price (p > c)

**Payment Schemes:**
- ![[Pasted image 20241127171011.png|500]]
1. O (Own financing):
	- Pay c per unit at order time
	- Receive p per unit sold after demand realization
2. S (Supplier financing):
	- Pay nothing at order time
	- After demand realization:
		* Receive p - c per unit sold
		* Pay c per unit leftover to external financing party
3. C (Customer financing):
	- Receive p - c per unit ordered at order time
	- Refund p per unit leftover to external financing party after demand realization

## 3.1 Expected-Profit-Maximizing Model

**Reward Function:**
- $R^i(q,D) =$ net profit for payment scheme $i ∈ {O, S, C}$
- $$R^i(q,D)=\begin{cases}-cq + p \min(q,D) &\text{if }i=O\\(p-c)\min(q,D) - c \max(q-D,0)&\text{if }i=S\\(p-c)q - p \max(q-D,0)&\text{if }i=C\end{cases}$$

**Optimal Order Quantity:**
- $q^i = \text{arg} \max_q E_D[R^i(q,D)]$
- $q^O = q^S = q^C = q^* = F^{-1}((p-c)/p)$

## 3.2 Loss Aversion Model

**Assumptions:**
- Individuals are loss averse with respect to order-time and demand-time payments
- Reference wealth updated after order-time payments

**Utility Function:**
- $U^l(x) = \{x \text{ if } x \geq 0; λx \text{ if } x < 0\}$ for $\lambda>1$
	- Increase the magnitude of the profit if it is negative.

**Reward Function:**
- $R^i(q) = U^l(\pi^i_1(q)) + U^l(\pi^i_2(q,D))$
- $$R^i(q,D)=\begin{cases}-\lambda cq + p \min(q,D) &\text{if }i=O\\0+U^l[(p-c)\min(q,D) - c \max(q-D,0)]&\text{if }i=S\\(p-c)q - \lambda p \max(q-D,0)&\text{if }i=C\end{cases}$$

**Optimal Order Quantities:**
- Optimal quantities under all three payments are less than the expected-profit maximizing solution
	- $q^O < q^*, q^S < q^*, q^C < q^*$

## 3.3 Time-Discounting Model

**Assumptions:**
- Decision maker prefers to receive benefits earlier and delay costs
- Demand-time payments are discounted
- Discount Factor: $\delta (0 < \delta < 1)$

**Reward Function:**
- $$R^i(q,D)=\begin{cases}-cq + \delta p \min(q,D) &\text{if }i=O\\\delta[(p-c)\min(q,D) - c \max(q-D,0)]&\text{if }i=S\\(p-c)q - \delta p \max(q-D,0)&\text{if }i=C\end{cases}$$

**Optimal Order Quantities:**
- $q^O < q^S = q* < q^C$

## 3.4 Prospective Accounting Model

**Key Concepts:**
- Mental "coupling" of payment and consumption
- Stronger coupling when looking forward, weaker when looking backward
- Underweighting of whichever occurs first (payment or consumption)

**Application to Newsvendor Problem:**
- Payments segregated into two time buckets: before and after demand realization
- Order-time payments coupled with demand-time payments

**Underweighting Factors:**
- $\gamma (0 < \gamma < 1)$ for scheme O (order cost)
- $\alpha (0 < \alpha < 1)$ for scheme C (net profit from quantity ordered)
- No underweighting for scheme S

**Reward Function:**
- $$R^i(q,D)=\begin{cases}-\beta cq + p \min(q,D) &\text{if }i=O\\(p-c)\min(q,D) - c \max(q-D,0)&\text{if }i=S\\\alpha (p-c)q - p \max(q-D,0)&\text{if }i=C\end{cases}$$

**Optimal Order Quantities:**
- $q^O > q^S = q* > q^C$

## 3.5 Summary

**Model Predictions:**

| Model                      | Predicted Order Pattern |
| -------------------------- | ----------------------- |
| Expected-Profit-Maximizing | $q^O = q^S = q^C = q^*$ |
| Loss Aversion              | $q^O , q^S , q^C < q^*$ |
| Time-Discounting           | $q^O < q^S = q^* < q^C$ |
| Prospective Accounting     | $q^O > q^S = q^* > q^C$ |

**Key Points:**
- Four behavioral models predict various ordering patterns under payment schemes O, S, and C
- Effects in each model are not mutually exclusive
- Time discounting and prospective accounting may coexist, biasing orders in opposite directions
	- Resulting order would depend on which effect dominates

# 4. Newsvendor Experiments

## 4.1 Study 1: Simple Payment Scheme Experiment

**Experimental Design:**
- 3 payment schemes: O, S, C
- Parameters: c = $1, p = $2
- Demand: Sum of 3 dice (min 3, max 18, mean 10.5)
- 25 rounds
- 99 student participants

**Methods:**
- Participants given instructions for assigned payment scheme
- Interacted with research assistant
- Used poker chips and play money
- Follow-up question and comprehension check

**Results:**
- Payment scheme significantly affected ordering behavior (p < 0.0001)
- Order pattern: O > S > C
- Average orders:
	* O: Significantly higher than mean demand
	* S: Not significantly different from mean demand
	* C: Significantly lower than mean demand
- No significant difference in ordering levels over time
- No significant interaction between payment scheme and experience

**Structural Parameter Estimates:**
- Used 3 estimation techniques: N1, N2, NH
- Estimated $\gamma$ (O scheme) ≈ 0.7
- Estimated $\alpha$ (C scheme) ≈ 0.8

**Expected Profits:**
- Significantly affected by payment scheme (p = 0.005)
- Highest under S scheme
- Differences in supplier revenue and customer service levels noted

**Key Findings:**
- Payment schemes have significant effect on ordering behavior
- Results consistent with prospective accounting model
- Inconsistent with expected-profit-maximizing, loss aversion, and time-discounting models
- Effect robust over 25 rounds

## 4.2 Study 2: Payment Scheme Experiment with Same Payment Timing

**Purpose:**
- Test if framing alone can produce similar results to Study 1
- Eliminate differences in actual payment timing

**Experimental Design:**
- Similar to Study 1, with key difference:
  * All payments postponed until after demand realization
- Three payment frames: Ō, S̄, C̄

**Methods:**
- 57 student participants
- Slight wording changes in payment scheme descriptions
- Additional comprehension question on long-run average demand

**Results:**
- Payment frame significantly affected ordering behavior (p < 0.0001)
- Order pattern: Ō > S̄ > C̄
- Average orders:
  * Ō: Significantly higher than mean demand
  * S̄: Not significantly different from mean demand
  * C̄: Significantly lower than mean demand
- No significant change in orders over time
- No significant interaction between payment frame and round

**Comparison to Study 1:**
- Similar overall ordering behavior
- Slightly less significant contrasts in Study 2
- No significant differences in round 1 order quantities

**Structural Parameter Estimates:**
- Almost identical to Study 1
- Confirms framing is sufficient to induce underweighting

**Expected Profits:**
- Significantly affected by payment frame (p = 0.016)
- Similar pattern to Study 1

**Key Findings:**
- Framing of payment scheme can significantly affect order decisions
- Mental accounting effect observed: participants mentally set aside payments
- Results provide further evidence for prospective accounting model

## 4.3 Study 3: Payment Scheme Experiments with High- and Low-Profit Conditions

**Experimental Design:**
- High-profit: c = $1, p = $4 (critical fractile 75%)
- Low-profit: c = $3, p = $4 (critical fractile 25%)
- Payment schemes O, S, C tested for each condition
- 20 rounds per participant

**Participants:**
- 130 students (70 high-profit, 60 low-profit)

**Results - High-Profit Condition:**
- Payment scheme significantly affected ordering (p < 0.0001)
- Order pattern: O > S > C
- Significant differences: S > C, O > C
- No significant difference: O > S

**Results - Low-Profit Condition:**
- Payment scheme significantly affected ordering (p = 0.0017)
- Order pattern: O > S > C
- Significant differences: O > S, O > C
- No significant difference: S > C

**Key Findings:**
- Payment scheme effect robust across profit conditions
- Supports prospective accounting model
- Differences in significance patterns explained by varying magnitudes of order-time payments

**Structural Parameter Estimates:**
- Controlled for pull-to-center effect
- Confirmed observations from order quantity comparisons

**Expected Profits:**
- High-profit: O ≈ S > C
- Low-profit: C ≈ S > O

**Asymmetry of Pull-to-Center Effect:**
- Scheme O: Stronger in low-profit condition
- Scheme S: No significant asymmetry
- Scheme C: Stronger in high-profit condition

**Implications:**
- Payment scheme interacts with pull-to-center effect
- Direction of pull-to-center asymmetry depends on payment scheme