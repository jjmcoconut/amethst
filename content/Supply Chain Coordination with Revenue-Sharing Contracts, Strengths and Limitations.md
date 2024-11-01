Gérard P. Cachon, Martin A. Lariviere

# Introduction

Capacity Problem in Videocassette Retail
- Issue: High initial cost per tape (~~$65) vs. low rental price (~~$3) limits retailers' ability to purchase enough tapes for peak demand.
- Solution: Revenue-sharing contracts allow retailers (e.g., Blockbuster) to pay a reduced price ($8 per tape) and share a portion of rental income (30-45%) with suppliers.
- Outcome:
    - Reduced breakeven (from 22 to ~6 rentals per tape).
    - Blockbuster’s market share rose from 24% (1997) to 40% (2002).
    - Total industry profit increased by ~7%.

Revenue-Sharing Model for Supply Chains
- Model Applicability: Relevant across various industries and supply chain links, regardless of deterministic or stochastic demand.
- Model Base: Supplier-retailer dynamic, retailer controls purchase quantity and retail price.
- Supply Chain Coordination: Revenue sharing aligns supply chain decisions on price and quantity for optimal profit allocation.

Comparative Contracts:
- Buy-back Contracts: Equivalent cash flows to revenue-sharing in fixed-price models.
- Quantity Flexibility (QF) & Sales Rebates: Not fully equivalent; ineffective in price-setting scenarios.
- Price-Discount Contracts: Effective for price-setting newsvendor models, comparable cash flows with revenue sharing.

Model Extensions:
- Quantity-Competing Retailers: Revenue sharing supports coordination and profit division among competing retailers (Cournot competitors).
- Limitations:
	- Ineffective for competing price-setting retailers influenced by mutual pricing actions.
	- High administrative burden due to revenue monitoring requirements.
	- Ineffective where retailer effort (non-contractible, costly) impacts demand.

__Research Questions__
1. How does revenue sharing influence supply chain coordination and profit allocation across deterministic, stochastic demand scenarios and fixed-price, price setting newsvendor models?
2. How does revenue sharing compare to alternative contracts such as buy-backs and price discounts in achieving supply chain coordination?
3. How does revenue sharing influence supply chain coordination with retailers competing with quantities?
4. What are the limitations of revenue sharing contracts?

# The Model

Supply Chain Structure
- Participants: Two risk-neutral firms—a supplier and a retailer.
- Retailer’s Decisions:
     - Quantity ($q \geq 0$), Price ($p$)
- Revenue: Only the retailer generates revenue over the sales period.

Revenue Function
- Retailer’s Total Revenue: $R(q, p) + vq$
     - $R(q, p)$: Revenue from purchased units $q$.
     - $vq$: Salvage revenue (may be negative); excludes long-term impact of poor availability.

Supplier & Retailer Costs
- Supplier's Cost: $c_s \cdot q$
- Retailer’s Cost (excluding supplier payment): $c_r \cdot q$
- Total Cost: $c = c_s + c_r$

Revenue-Sharing Contract
- Parameters:
     - Wholesale Price ($w$): Paid per unit by the retailer.
     - Revenue Share ($\phi$): Retailer’s share of revenue from each unit, with supplier's share $1 - \phi$.
     - Special Cases:
		- Wholesale-only contract: $\phi = 1$.
		- Uniform revenue share across all units.
- Profit Functions:
     - Retailer’s Profit: $\pi_r(q, p) = \phi R(q, p)  - (c_r + w -\phi v)q$
     - Supplier’s Profit: $\pi_s(q, p) = (1 - \phi)R(q, p) - (c_s - w - (1-\phi)v)q$
     - Total Supply Chain Profit: $\pi(q, p) = R(q, p) - (c-v) \cdot q$

Coordination and Salvage Revenue
- Fixed Retail Price: Revenue sharing coordinates the supply chain if only $R(q, p)$ is shared.
- Variable Retail Price: Sharing both $R(q, p)$ and $vq$ is needed for full coordination and arbitrary profit division.


## Revenue-Sharing Contracts

Revenue-Sharing Contracts and Supply Chain Coordination
- Concept: Contracts align retailer’s profit with overall supply chain profit by transforming the retailer’s profit function to reflect the supply chain's profit function.
- Optimal Quantity-Price Pair ($q^o$, $p^o$): This pair maximizes the combined profit function $b(q, p)$. Existence is ensured but uniqueness is not required.

Theorem 1: Revenue-Sharing Contracts Structure
- Contract Terms:
	- Wholesale price $w = \phi c − c_r$ 
- Firm Profit Functions:
	- $\pi_r(q,p)=\phi \Pi(q,p)$
	- $\pi_s(q,p)=(1-\phi)\Pi(q,p)$

Implications of Revenue-Sharing Contracts
- Coordination: A single revenue-sharing contract can coordinate actions across multiple non-competing retailers, even if they have different revenue functions, as long as their revenue is independent.
- Optimal Quantity and Price: $q^o$ and $p^o$ serve as optimal points for the retailer, effectively coordinating the supply chain.

## Other Contracts

Other Contracts
- Buy-Back Contracts: Supplier sets a wholesale price and pays retailer a buy-back rate for unsold units.
- Price-Discount Contracts: Wholesale price adjusts based on retailer’s chosen retail price.
- Quantity Flexibility (QF) Contracts: Retailer can return a portion of unsold units for a full refund.
- Sales-Rebate Contracts: Retailer receives rebates for units sold above a threshold.
- Two-Part Tariffs: Combines a per-unit wholesale price with a fixed fee.
- Franchise Contracts: Includes a fixed fee, wholesale price, and a per-transaction revenue share (royalty).
- Quantity Discount Contracts: Wholesale price decreases with quantity purchased.

Result
1. Fixed-Price Newsvendor Coordination
	- Revenue Sharing
	- Buy-Back Contracts: Equivalent to revenue sharing in generating identical profits.
	- Price-Discount Contracts: Also equivalent in profit generation to revenue sharing.
2. Price-Setting Retailer Coordination
	- Revenue Sharing
	- Equivalent Price-Discount Contract
	- Two-Part Tariffs (equivalent to franchise contracts)
		- Drawback: Two-part tariffs and quantity discounts are less advantageous than revenue sharing when applied to systems with multiple noncompeting retailers.
	- Quantity Discounts

# Competing Retailers

Market Assumptions
- Revenue Dependence: Retailer *i*’s revenue, $R_i(\bar{q})$, depends on the stocking quantities of all retailers ($\bar{q} = [q_1, q_2, \dots, q_n]$).
- Types of Competition:
	- Fixed-Price Newsvendors: Fixed retail price
	- Cournot Competition ($R_i(\bar{q}) = q_i (1 - q_i - \gamma\sum_{j \neq i} q_j$, $0\leq\gamma<1$)

Cost Structure
- Supplier’s Cost: $c_s$ per unit.
- Retailer’s Incremental Cost: $c_{ri}$.
- Total Cost for Retailer *i*: $c_i = c_s + c_{ri}$.

Supply Chain Profit
- Individual Profit: $\Pi_i(\bar{q}) = R_i(\bar{q}) - c_i q_i$.
- Total Profit: $\Pi(\bar{q}) = \sum_{i=1}^{n} \Pi_i(\bar{q})$.

System Optimization
- Optimal Quantities: $\bar{q}^o$ satisfies first-order conditions for profit maximization.
- Decentralized System: Supplier offers revenue-sharing contracts $w_i$ to each retailer, who then independently choose $q_i$ to maximize their profit.

Theorem 4: Coordination via Revenue Sharing
- Revenue-Sharing Contracts: Defined as $$w_i=\phi_i(c_i-\xi_i^o)-c_{ri}$$

     where $\xi_i^o = \xi_i(\bar{q}^o)= \sum_{j \neq i} R_j(\bar{q}^o)$.
- Outcome:
	- Achieves supply chain coordination ($\bar{q}^* = \bar{q}^o$).
	- Allows flexible profit allocation among retailers.
	- Includes wholesale price contracts as a special case.

Implications and Flexibility
- Profit Allocation: Varying parameter $\phi$ allows different splits of the supply chain profit.
- Administrative Flexibility: Different contractual terms needed for each retailer unless they are homogeneous.

Limitations of Revenue Sharing
- Heterogeneous Retailers: Single revenue-sharing contract cannot coordinate supply chains with diverse retailer costs or externalities.
- Administrative Burden: Requires monitoring of each retailer’s revenues, increasing complexity and cost.
- Competition with Pricing Decisions: Fails to coordinate in settings where retailers also set prices.

__Conclusion__
- A revenue-sharing contract enables coordination and allows flexible profit distribution among multiple competing retailers. 
- However, a separate contract is required for each retailer, and it does not achieve coordination when retailers have the ability to set prices.

# Revenue-Sharing vs. Wholesale Price Contracts

## Single retailer case


Profit Gain Depends on Marginal Revenue Curve Shape
- Convex Curve:
	- Leads to lower efficiency (<75%).
	- Decentralized system stocks less than half of the integrated system quantity.
- Concave Curve:
	- Results in higher supply chain efficiency.
	- Efficiency improves as the curve becomes more concave, approaching coordination.

Impact of Marginal Revenue Curve Curvature
- Convex Marginal Revenue Curve:
	- Results in supplier profit less than two-thirds of system profit.
	- Efficiency loss is substantial, where actual stocking quantity is far below ideal.
- Concave Marginal Revenue Curve:
	- Higher supplier profit share (more than two-thirds).
	- Higher system efficiency as stocking approaches ideal levels.
- Linear Curve: Efficiency achieves approximately 50% increase in total profit from coordination.

__Conclusion__
- Convex curves cause inefficiencies in supply chains
- Concave curves facilitate closer to optimal coordination and improve profit allocations, leading to higher overall efficiency.

## Multiple-Retailer Case

Impact of Retail Competition on Supply Chain Efficiency
- Scenario: n symmetric retailers compete under a wholesale price contract from a supplier.
- Measures of Competition:
	- Increase in parameter $\theta$ or number of retailers $n$ increases competition.
   
Equilibrium Analysis
- Equilibrium Quantity: $q^*_i = \frac{1 - w}{2 + \gamma(n - 1)}$ for each retailer $i$.
- Integrated Channel Quantity: $q^o_i = \frac{1 - c}{2 + 2\gamma(n - 1)}$.
- Coordination Condition: System coordinates if wholesale price $w^o = c + \frac{\gamma(n - 1)(1 - c)}{2 + 2\gamma(n - 1)}$.

Wholesale Price and Competition
- Optimal Wholesale Price for Supplier: Supplier prefers $w^* = \frac{1 + c}{2}$, independent of both $\gamma$ and $n$.
- Gap Between Wholesale Prices: The difference between $w^o$ and $w^*$ diminishes as $n$ grows; minimal when $\gamma$ is close to 1.

Channel Efficiency with Increasing Retailers
- Efficiency Formula: $1 - {(2 + \gamma(n - 1))^{-2}}$.
- Efficiency Improvements:
	- If $\gamma = 0$: 75% efficiency in independent markets.
	- If $\gamma > 0$: Efficiency rapidly increases with more retailers:
		- $\gamma = \frac{1}{3}$: ~85% with three retailers, ~90% with five.
		- $\gamma = \frac{2}{3}$: ~91% with three, ~95.4% with five.

Implications of Competition on Contract Preference
- __Comparison to Single-Retailer Case__: Retail competition under wholesale price contracts boosts efficiency more significantly than the revenue function.
- __Revenue Sharing__: Less appealing for suppliers with multiple retailers, especially if high administrative costs are incurred per retailer.
- __Conclusion__: Increased competition in retail markets enhances supply chain efficiency, potentially reducing the need for complex revenue-sharing models.

# Retailer Effort and Revenue Sharing

Retailer Revenue Function with Effort
- Revenue Function: $R(q, e)$
	- Variables:
		- $q$: Order quantity
		- $e$: Effort level
- Cost Function: $g(e)$
- No incremental purchase cost: $c_r=0$
- Integrated Channel Profit:
	- $\Pi(q, e) = R(q, e) - g(e) - q c$
	- Optimal Solutions: $q^o, e^o$
	- $$\frac{\partial \Pi(q^o, e^o)}{\partial e} = \frac{\partial R(q^o, e^o)}{\partial e} - g'(e^o) = 0$$
- Retailer’s Profit Function:
	- $\pi_r(q, e) = \phi R(q, e) - g(e) - q w$
	- $$\frac{\partial \pi_r(q^o, e^o)}{\partial e} =\phi \frac{\partial R(q^o, e^o)}{\partial e} - g'(e^o) < 0$$
- Coordination via Revenue Sharing:
	- Only possible if $\phi=1 \rightarrow w = c$ (supplier sells at marginal cost)

Challenges of Revenue Sharing in Effort Coordination
- Retailers bear the entire cost of effort, creating misaligned incentives.
- Alternative: suppliers could cover part of the effort cost, but this risks retailer misrepresentation of actual effort expenses.

Other Contract Methods
- Combination of sales-rebate with buy-back contract.
	- Sales-rebate contract gives incentive retailer to exert effort
	- Buy-back contract reduces effort.
	- However this contract requires 4 parameters: $w,b,t,r$
- Quantity discount contract related to revenue sharing
	- Supplier charges the retailer $w(q)=(1-\chi)R(q,e^o)/q +\chi c,\text{ } (\chi\in(0,1])$ per unit
	- Retailer retaining all revenue
		- $\{ q^o,e^o \}$ maximizes retailer's expected profit: $\pi_r(q^o,e^o)=\chi\Pi (q^o,e^o)-(1-\chi)g(e^o)$ 
	- **Effectiveness**: Retailer retains full revenue and cost responsibility, aligning effort and maximizing supply chain profits with minimal parameters.
	- **Conclusion**: While quantity discounts and variations on revenue sharing can coordinate the retailer's decisions with two parameters, they are less flexible for managing multiple retailers with different demand profiles.