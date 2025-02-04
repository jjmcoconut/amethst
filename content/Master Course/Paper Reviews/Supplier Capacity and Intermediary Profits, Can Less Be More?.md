Elodie Adida, Nitin Bakshi, Victor DeMiguel

# Introduction

__Background__
- Developed countries’ retailers often source low-cost products from international suppliers.
- Commodity products: Retailers have long-term supplier relationships.
- Specialized products (e.g., fashion, toys): High turnover requires complex, extensive networks of suppliers managed by intermediaries.
- Intermediaries maintain supplier networks due to their expertise, especially in retailer-driven supply chains where retailers monitor trends and initiate orders.

__Retailer-Driven Supply Chains__
- **Retailers as Leaders**: Retailers drive interactions, with intermediaries selecting capable suppliers.
- **Supply Chain Dynamics**: Retailer-led chains contrast with traditional supplier-led models, impacting intermediary profit and market power.

__Research Focus__
- **Objective**: Determine conditions under which intermediaries thrive in retailer-driven supply chains.
- **Model**: Uses a three-tier structure (retailer, intermediary, suppliers) to derive intermediary profit.
- **Main Finding**: Intermediary profit is unimodal relative to supplier base size—neither too large nor too small is optimal.

__Key Findings and Implications__
- **Supplier Base Size**:
	- Small supplier base → intermediary gains market power.
	- Large supplier base → retailer exerts power, reducing intermediary profits.
	- Optimal profit occurs with intermediate production capacity.
- **Extensions**:
	1. **Horizontal Competition**: Profit pattern remains unimodal with multiple retailers/intermediaries. More competition favors a less elastic supply side.
	2. **Exclusive Suppliers**: Presence reduces competition among intermediaries; increases optimal supplier base for max profit.
	3. **Direct Sourcing by Retailers**: Retailers' option to bypass intermediaries affects intermediary strategies but profit pattern holds.

__Operational Implications__
- **Portfolio Management**: Intermediaries benefit from flexible product portfolios, especially in fast-moving industries like fashion and consumer electronics.
- **Strategic Flexibility**: Intermediate capacity levels that optimize profits tend to align with product growth and decline phases.
- **Supply Chain Strategy**: Intermediaries should consider:
	- Supplier-retailer concentration.
	- Asymmetry among intermediaries.
	- Retailers' direct sourcing ability.

__Research Question:__ **Under what market conditions can intermediaries thrive in retailer-driven supply chains?**


# 3. When Do Intermediaries Thrive
## 3.1 Model Structure

**Three-Tier Supply Chain**:
- **Retailer Tier**: A single retailer, leading the chain, faces consumer demand represented by a linear demand function.
- **Intermediary Tier**: One intermediary (acting as a Stackelberg leader over suppliers) sets its order quantity to maximize profit while anticipating supplier response.
- **Supplier Tier**: Consists of $S$ capacity-constrained suppliers, each maximizing profit based on production cost and supplier price.
- **Objective**: Maximize profits through Stackelberg game hierarchy (retailer > intermediary > suppliers).

### 3.1.1 Supplier Tier

Given supplier price $p_s$, chooses $q_{s,j}$ to maximize profit $\pi_{s,j}=p_sq_{s,j}-c(q_{s,j})$
- Production cost is convex quadratic: $c(q_{s,j})=s_1q_{s,j}+(s_2/2)q_{s,j}^2$

**Aggregate Supply Function**: 
- Total quantity produced by suppliers given $p_s$
- $Q_s(p_s) = Sq_{s,j}= S (p_s - s_1)/s_2$

### 3.1.2 Intermediary Tier

Given $p_i$, Intermediary chooses quantity $q_i, p_s$ to maximize profit
- $$\begin{align}&\max_{q_i,p_s}\quad \pi_i=(p_i-p_s)q_i\\ &s.t. \quad q_i=Q_s(p_s)\end{align}$$
- $q_i(p_i)$: Intermediary equilibrium quantity for price $p_i$

### 3.1.3 Retailer Tier
__Demand__: $p_r=d_1-d_2q$
Retailer Chooses $q_r,p_i$ to maximize its proft
- $$\begin{align}&\max_{q_r,p_i}\quad \pi_r=(d_1-d_2q_r-p_i)q_r\\& s.t. \quad q_r=q_i(p_i)\end{align}$$

### 3.1.4 Discussion on Model Choices
- **Static Game**: One-shot game reflects incidental demand in industries like fashion.
- **Wholesale Price Contracts**: Model reflects industry practices.
- **Marginal Cost Assumptions**: Linearly increasing marginal cost represents realistic cost scenarios where existing supplier capacity is utilized.

## 3.2 Equilibrium and Intermediary Profit Insights
- **Theorem 1**
	- $$Q=q_r=q_i=Sq_s=\frac{S(d_1-s_1)}{2(d_2S+2s_2)}$$
	- $$p_r=d_1-d_2Q, p_i=s_1+2\frac{s_2}{S}Q,p_s=s_1+\frac{s_2}{S}Q$$
	- $$\pi_r=\frac{d_1-s_1}{2}Q,\pi_i=\frac{s_2Q^2}{S},S\pi_s=\frac{s_2Q^2}{2S}$$
- **Theorem 2 (Key Insight)**: Intermediary profit is unimodal and maximized at an intermediate number of suppliers $S = \frac{2s_2}{d_2}$.
	- **Market Power Shift**: With too many suppliers, the retailer exerts greater control, reducing intermediary margins and profits. In the limit (infinite suppliers), retailer drives price to suppliers’ marginal cost, capturing all profits.

### Implications of Intermediate Supplier Base
- Intermediaries prefer products with a balanced production capacity—sufficient suppliers for flexibility but limited enough to retain bargaining power.
- **Economic Context**: Profitability for intermediaries fluctuates with production capacity; both under- and over-capacity situations squeeze intermediary profits (e.g., shortfalls or surpluses in fashion production capacity).


# 4. The Impact of Horizontal Competition

## 4.1 Model 
![[Pasted image 20241106192922.png|400]]
Compete horizontally in quantities across a three-tier supply chain
- $R$ symmetric retailers
- $I$ symmetric intermediaries
- $S$ suppliers

__Intermediary Decision:__
- $$\begin{align}&\max_{q_{i,l},p_s}\quad \pi_i=(p_i-p_s)q_{i,l}\\& s.t. \quad q_{i,l}+Q_{i,-l}=Q_s(p_s)\end{align}$$

__Retailer Decision:__
- $$\begin{align}&\max_{q_{r,k},p_i}\quad \pi_r=(d_1-d_2(q_{r,k}+Q_{r,-k})-p_i)q_{r,k}\\ &s.t. \quad q_{r,k}+Q_{r,-k}=Q_i(p_i)\end{align}$$
- $Q_i(p_i)$: Intermediary equilibrium quantity given $p_i$


## 4.2. Equilibrium and Intermediary Profits
- **Theorem 3**: Provides closed-form solutions for equilibrium and intermediary profits.
	- $$Q=Rq_r=Iq_i=Sq_s=\frac{RSI(d_1-s_1)}{(R+1)(d_2SI+(I+1)s_2)}$$
	- $$p_r=d_1-d_2Q,p_i=s_1+\frac{s_2}{S}\frac{I+1}{I}Q,p_s=s_1+\frac{s_2}{S}Q$$
	- $$R\pi_r=\frac{d_1-s_1}{R+1}Q,I\pi_i=\frac{Is_2Q^2}{SI^2},S\pi_s=\frac{s_2Q^2}{2S}$$
- **Theorem 4**: $I\pi_i$is unimodal & achieves maximum at $S=(I+1)s_2/(d_2I)$
	- **Implication**: Competing intermediaries prefer a smaller, more inelastic supplier base than single intermediaries since competition strengthens retailer bargaining power.
- ![[Pasted image 20241106194432.png|400]]
	- **Illustration**: Graphs indicate that intermediary profits are maximized with fewer suppliers in the competitive case.

## 4.3. Size of Supply Base and Supply Chain Efficiency

- **Efficiency Definition**: Ratio of decentralized to centralized supply chain profits.
- __Theorem 5:__ Supply chain efficiency is$$\text{Efficiency}=\frac{RI[s_2R(I+2)+2(d_2SI+s_2(I+1))]}{(d_2SI+s_2(I+1))^2}\frac{2d_sS+s_2}{(R+1)^2}$$

	- Efficiency is unimodal with respect to supplier number, achieving maximum at an intermediate supply base size.
	- The supply base maximizing supply chain efficiency ($S^*$) is larger than the supply base maximizing intermediary profit ($S_{max}$) $\iff R<2+2/I$
- **Regulatory Implication**: Efficiency improvements may require tailored interventions, particularly subsidies, depending on the level of retailer concentration.

# 5. The Case with Shared and Exclusive Suppliers

1. Shared vs. Exclusive Suppliers
	- **Model Adjustment**: Unlike prior assumptions, suppliers may work with specific intermediaries, creating a mix of exclusive and shared suppliers.
	- **Finding**: Even with exclusive suppliers, intermediary profits remain unimodal in relation to the number of suppliers, though the profit-maximizing number of suppliers increases.

2. **Proposition 1**: The total equilibrium quantity where $j$th supplier works with subset of $I_j$ intermediates is the same as if all $S$ suppliers worked with a $\bar{I}\in[0,I]$ number of intermediaries, where $I$ is $$\frac{\bar{I}}{\bar{I}+1}=\frac{1}{S}\sum_{j=1}^S\frac{I_j}{I_j+1}$$
	- **Effect**: Exclusive suppliers reduce competition among intermediaries by lowering the number of effective intermediaries.

3. **Proposition 2** (All Suppliers Exclusive):
	1. Supply chain equilibrium mirrors a scenario with one intermediary working with all suppliers.
	2. Profits are unimodal, peaking at an optimal supplier count ($2s_2/d_2$), which is higher than in the shared-supplier case.
	3. Total intermediary profits exceed those in fully shared supplier scenarios.
	- **Intuition**: Intermediary profits rely on the supplier count, independent of whether suppliers work for separate or the same intermediary.

4. **Proposition 3** (Some Shared, Some Exclusive):
	- With a constant ratio of shared and exclusive suppliers, profits remain unimodal and peak at a higher supplier count than in fully shared setups.
	- **Implication**: Intermediate capacity remains optimal for profits, but exclusive suppliers lessen competition, allowing intermediaries to handle products with larger production capacity.

5. Implications
	- **Dampened Competition**: Exclusive suppliers reduce rivalry among intermediaries, enabling greater flexibility in managing products with high production capacity.
	- **Strategic Preference**: Intermediaries tend to prefer products with intermediate production levels but are more open to higher capacities in exclusive supplier contexts.

# 6. The Option to Source Directly from the Suppliers

## 6.1 Direct Sourcing
- **Cost Structure**:
	- Retailer incurs a fixed cost per supplier ($F$) and additional variable cost per unit ($v$) for direct sourcing.
	- Intermediary has established relationships with suppliers, so incurs no fixed costs but takes a margin on each unit sold to the retailer.
- **Work Flow**:
	- Retailer chooses an optimal number of suppliers $S_R$, incurring fixed cost $S_RF$
	- Retailer chooses order quantity
- $$S_R=\frac{1}{d_2}\left[\frac{(d_1-v-s_1)\sqrt{s_2}}{2\sqrt{F}}-s_2\right]^+$$
- $$\pi_R=\frac{s_2}{d_2}\left(\left[\frac{d_1-v-s_1}{2\sqrt{s_2}}-\sqrt{F}\right]^+\right)^2$$
## 6.2 Decision to Use an Intermediary
- Retailer benefits from using intermediary when $$\frac{S(d_1-s_1)^2}{4(d_2S+2s_2)}\geq \frac{s_2}{d_2}\left(\left[\frac{d_1-v-s_1}{2\sqrt{s_2}}-\sqrt{F}\right]^+\right)^2$$
	1. Fixed costs ($F$) or variable costs ($v$) for direct sourcing are high.
	2. Supplier base is large, making intermediary costs lower.
	3. Product margins($d_1-s_1$) are low, making direct sourcing less economical.
- **Impact of Retailer’s Direct Sourcing Threat**:
	- The possibility of direct sourcing pushes the intermediary to expand its supplier base beyond the profit-maximizing threshold to retain retailer business.

## 6.3 Intermediary Profits and Supplier Base Size
- **Profit Unimodality**:
	- Intermediary profit remains unimodal even with direct sourcing as an option.
- ![[Pasted image 20241106203747.png|500]]
	- Intermediary may optimally choose to carry with number of suppliers $S>S_{max}$ because of the threat that the retailer may work directly with the supplier.
