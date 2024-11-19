Serguei Netessine, Fuqiang Zhang

# 1. Introduction
1. **Introduction to Retailer Stocking Decisions and Externalities**  
	- Retailers' stocking decisions interdepend when products are related.
	- **Externalities** impact demand and supply:  
		- **Demand-side**: Prices influence demand across products.  
		- **Supply-side**: Product availability affects supply chain performance (focus of this paper).
	- Retailers (either centralized or competitive) face inefficiencies due to:  
		- **Double Marginalization**: Wholesaler sets prices above marginal cost, leading to understocking.
		- **Supply-side Externalities**: Impact varies by externality type (positive or negative) and competition level.

2. **Negative externalities (substitutability)**
    - One retailer’s inventory affects others negatively (e.g., stock-out substitution).
	- Result: Competition in substitutes can lead to overstocking, mitigating understocking caused by double marginalization.

3. **Positive Externalities (Complementarity)**  
	- **Complementarity in Practice**: Stocking of one product boosts demand for others (e.g., complementary goods like game consoles and cartridges).
	- Real-world examples: Video game market (Nintendo), compatible media formats (VHS vs. Betamax).

4. **Research Objectives and Key Contributions**  
	- Compare **centralized** vs. **competitive inventory management** for complements vs. substitutes.
	- Discover that **competition on complements** consistently leads to understocking, unlike overstocking with substitutes.

5. **Framework and Findings**  
	- Introduced models for externalities through **inventory and sales** with parameter **$b$** for externality type:
		- $b = -1$: Strong substitutes.
		- $b = 0$: Independent.
		- $b = 1$: Strong complements.
	- **Inventory Trends**:  
		- Total inventory is monotone increasing in $b$.
		- **Substitutes**: Lowest inventory.  
		- **Complements**: Highest inventory but severe understocking under competition.
	- **Supply Chain Insights**:  
		- **Competition with Complements**: Aggravates understocking and double-marginalization.
		- **Competition with Substitutes**: Offsets understocking, improves supply chain efficiency.

6. **Managerial Implications**  
	- **Supply Chain Coordination**: Essential under competition with complements.
	- Wholesalers benefit differently by externality type:  
		- **Substitutability**: Prefers competition to boost demand.
		- **Complementarity**: Prefers centralized control to reduce understocking.

# 3. Complementarity

**Retail Decision-Making Framework**
- Retailers $i$ indexed by $i = 1, 2, ... N$, set initial inventory $Q_i$ at season start.
- Retailer buys at wholesale cost $w_i$, sells at retail price $r_i$, and faces fixed prices due to price maintenance.
- **Effective Demand ($D_i^e$)**: Depends on other retailers’ stocking levels, $Q_{-i}$, and varies stochastically.
   
**Complementarity and Substitutability Defined**
- $X\geq_s Y \equiv \Phi_Y(x)\geq \Phi_X(x)$
- **Complementarity**: If higher inventory levels at other retailers ($Q_{-i}$) increase retailer $i$’s demand ($D_i^e$).
	- $Q'_{-i}\geq Q_{-i}\rightarrow D_i^e(Q'_{-i})\geq_s D_i^e(Q_{-i})$
- **Substitutability**: If higher inventory levels at other retailers decrease $D_i^e$.
	- $Q'_{-i}\geq Q_{-i}\rightarrow D_i^e(Q'_{-i})\leq_s D_i^e(Q_{-i})$
- Effective demand models that show complementarity:
	- **Externality Through Sales**: Demand depends on both local stock and other retailers' stock.
		- $D_i^e=D_i+\sum_{j\neq i}a_{ji}\min (D_j,Q_j)$
	- **Additive Demand**: Demand increases with other retailers’ stocking levels.
		- $D_i^e=A_i+g_i(Q_{-i})+\epsilon_i$
	- **Multiplicative Demand**: Proportional increase with higher stocking levels.
		- $D_i^e=\epsilon_i g_i(Q_{-i})$
	- **Perfect Complements**: Minimum stock across components determines demand.
		- $D_i^e=\min(Q_1,Q_2,\cdots,Q_{i-1},Q_{i+1},\cdots,Q_n,D)$

## 3.1. Competition at the Retail Level

**Decentralized Inventory Management (Competition)**
- **Non-Cooperative Game**: Each retailer decides stocking levels independently in a static game with complete information.
	- Game: $(A_i,\pi_i^d:i\in N)$
	- Action space: $A_i=[0,M]$
	- Expected profit: $\pi_i^d(Q)=E[r_i\min(Q_i,D_i^e)-w_iQ_i]$
- **Proposition 1**: Complementarity ensures
	- Game is supermodular
	- The game has at least one Nash equilibrium.
	- Largest and smallest equilibrium inventory levels exist.
	- Equilibrium inventory levels exceed the newsvendor quantity (standard inventory level).

## 3.2. Centralization at the Retail Level
- **Joint Profit Maximization**: A central planner optimizes total inventory for all locations.
	- $$\pi(Q)=\sum_i \pi_i(Q)=\sum_iE[r_i\min(Q_i,D_i^e)-w_iQ_i]$$
- **Concavity Condition**: Ensures a unique solution for total profit maximization.
	- **Proposition 2**: When demand functions are concave, unique inventory policies exist under centralization.

## 3.3. Comparison of Centralized and Decentralized Inventory Management
- **Key Insight**: Decentralized management leads to **understocking** under complementarity.
- **Proposition 3**:
	- $Q_i^c\geq Q_i^d$: All retailers stock less than the centralized optimal levels.
	- $\pi_i(Q^d)\leq\pi_i(Q^c)$: Centralized management yields higher profits for each retailer.
- **Intuition**:
	- **Complementarity Effect**: If one retailer stocks more, it boosts demand for others, promoting higher stock levels in a centralized system.
	- **Substitutability Effect**: An increase in one retailer’s stock reduces demand for others, leading to complex stocking behavior with some retailers over- and others under-stocking.

**Managerial Implications**
- **Complementarity**: Retailers prefer centralized inventory control because of predictability in inventory outcomes.
- **Substitutability**: Leads to mixed stocking strategies, where centralization benefits may not be uniformly beneficial for all retailers.

# 4. Complements vs. Substitutes and Competition vs. Centralized Control: A Duopoly Analysis

__Types of Externalities__
1. **Externality through Sales**:
	- Sales of one product affect demand for others (e.g., TVs & VCRs).
2. **Externality through Stocking Quantity**:
	- Inventory presence influences demand for related products.
- $\Pi$: Wholesaler profit

__Models Analyzed__
1. **Supply Chain Optimal Model**: Centralized control by retailers and wholesaler with optimal order quantities $Q^o_i$.
2. **Decentralized Model**: Competing retailers; each retailer's stock decision ($Q^d_i,\pi_i^d,\Pi^d$) is made independently.
3. **Centralized Retail Model**: Retailers centrally controlled; wholesaler remains a separate entity ($Q^c_i,\pi_i^c,\Pi^c$).
- Two retailers with demand model $D_i^e(Q_j)=A_i+g_i(bQ_j)+\epsilon_i$(Additive demand model)

__Key Propositions__
__When wholesale price is fixed:__
1. **Proposition 4**: Decentralized Inventory Management
	- **Supermodular (b > 0)** / **Submodular (b < 0)** game.
	- Unique **Nash equilibrium** exists.
	- **Total inventory** and wholesaler profit increase with $b$.

2. **Proposition 5**: Centralized Inventory Management
	- Optimality conditions ensure inventory levels are **monotonically increasing** with $b$.
	- Objective is **supermodular (b > 0)**, **submodular (b < 0)**.

- Supply Chain Optimal model
	- Centralized retailer model with $w_i=c$
	- $Q_i^o\geq Q_i^c$: Due to double marginalization

3. **Proposition 6**: Under additive demand model
	- $b > 0$: $Q^c_i \geq Q^d_i, \Pi^c\geq\Pi^d$, $\exists w_i\in[c.r_i]$ that achieves coordination (compensate double marginalization)
	- $b < 0$: $Q^c_i \leq Q^d_i, \Pi^c\leq \Pi^d$, never achieves coordination (intensify double marginalization)
	- ![[Pasted image 20241107134638.png|400]]

__Wholesale price can change:__
- The wholesaler may raise the wholesale price as $b$ increases due to higher demand.
- **Proposition 7**: Price-Setting Wholesaler with Vertical Competition
	- Unique **stock quantities and wholesale prices** $Q_d$, $Q_c$; both increase with $b$.
	- Results align with fixed wholesale price outcomes under mild assumptions.

# 5. Managerial Implications for Supply Chain Design
 
**Complements vs. Substitutes**
- **Complements**
	- Competition 
		- Leads to severe understocking, worsening the double-marginalization effect.
		- Complex contracts are useful
	- All parties (retailers and wholesaler) benefit from centralizing retail operations, as it mitigates understocking, though not fully optimal.
- **Substitutes** 
	- Competition 
		- Results in overstocking (mitigates understocking from double marginalization).
		- Wholesale price contracts performs well
	- Wholesalers prefer retail competition since it boosts demand without coordination.
- **Highest Inefficiency**: Competition with complements.
- **Lowest Inefficiency**: Competition with substitutes.


