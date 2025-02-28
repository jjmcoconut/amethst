Karthik Murali, Michael K. Lim, Nicholas C. Petruzzi

__정부의 개입은 기업의 신뢰도가 충분히 높고 소비자가 환경 보호를 중요하게 생각하는 경우 자발적인 외부 인증을 장려해야 한다__

# 1. Introduction

**Ecolabel Strategies**  
- Self-Labels (Type 2)
	- Examples: Whole Foods' "Responsibly Grown," Walmart's "Natural" line  
	- Challenges: Consumer skepticism without third-party verification  
- External Certifications (Type 1)
	- Trusted authorities: USDA Organic, Marine Stewardship Council  
	- Advantages: Higher consumer willingness to pay  

**Credibility Dynamics**  
- Reputation dictates label effectiveness (e.g., Whole Foods vs. Walmart perception gap)  
- Low-credibility firms benefit more from external certifications  
- High-credibility firms may avoid certification costs  

**Policy Landscape**  
- Voluntary Approaches
	- Self-labeling vs certification decisions tied to brand credibility  
- Government Regulation
	- Examples: California's Green Chemistry Law (chemical restrictions)  
	- Pros: Standardizes environmental baselines  
	- Cons: May limit innovation and market differentiation  

**Strategic Implications**  
1. Credible brands can leverage reputation for premium pricing  
2. Certification costs create market entry barriers for smaller firms  
3. Regulations reduce greenwashing but risk "lowest common denominator" outcomes  

**Research Objectives**  
- Analyze credibility's role in competitive strategies  
- Compare effectiveness of voluntary vs mandatory approaches  
- Develop policy frameworks balancing innovation and environmental goals


# 3. Base Model

**Key Components**  
- **Firms**: High-credibility (H: $\mu_H$) vs low-credibility (L: $\mu_L$)  
- **Environmental Quality ($g_i$)**: Chosen from (0,1) interval  
- **Cost Structure**: Quadratic investment ($g_i^2$)  
- **Consumer Perception**: 
	- $q_H=\frac{1}{2}-p_H+(p_L-p_H)+\beta(\mu_Hg_H-\mu_Lg_L)$
	- $q_L=\frac{1}{2}-p_L+(p_H-p_L)+\beta(\mu_Lg_L-\mu_Hg_H)$
		-   $\beta$: Consumers’ relative valuation of perceived environmental quality

**Two-Stage Game**  
1. **Quality Choice**: Simultaneous $g_i$ selection  
2. **Pricing**: Simultaneous price setting post-quality announcement  

**Equilibrium Insights**  
- High-credibility firms choose higher $g_i$ (e.g., $g_H > g_L$)  
- Profit advantage for credible firms ($π_H > π_L$)  
- Credibility gaps widen environmental quality differences  

**3BL Metrics**  

| Aspects                             | Impact of Credibility Increase |
| ----------------------------------- | ------------------------------ |
| __Consumer Surplus__                | Increases with H's credibility |
| __Pollution Reduction ($1 - g_i$)__ | Directly proportional to $g_i$ |
| __Firm Profits ($\Pi_i$)__          | H gains disproportionately     |

# 4. External Certification

**Key Features of External Certification**  
- **Credibility Advantage**: Removes credibility discount; perceived quality equals actual quality.  
- **Certification Process**:  
	1. NGO announces quality target ($g^G$) and fee ($\tau^G$).  
	2. Firms decide to adopt certification (G) or self-label (S).  
	3. Firms choose quality levels and set prices.  
- **Zero Fee Insight**: NGO sets $\tau^{G*}=0$ to maximize environmental quality improvement.  

**Equilibrium Outcomes**

| **Credibility Thresholds ($\mu_H$)** | Environmental Quality ($g^G$) | **Firm Behavior**                                                                             |
| ------------------------------------ | ----------------------------- | --------------------------------------------------------------------------------------------- |
| $\mu_H < \bar{\mu}^G(\mu_L)$         | Moderate ($g^G_I$)            | Both firms meet $g^G_I$ exactly ($g_L^G = g_H^G = g^G_I$); no differentiation; equal profits. |
| $\mu_H \geq \bar{\mu}^G(\mu_L)$      | High ($g^G_{II}$)             | Firm L adopts $g^G_{II}$; Firm H self-labels ($g_H^G < g^G_{II}$)                             |


**Broader Impacts**  

| Metric                   | Impact of Certification                                                                                                                        |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **Profits**              | Firm L profits increase ($\Pi^G_L > \Pi^S_L$); Firm H profits decrease ($\Pi^G_H < \Pi^S_H$). Partial adoption makes Firm L the profit leader. |
| **Environmental Damage** | Certification reduces overall damage ($E^G < E^S$).                                                                                            |
| **Consumer Surplus**     | Mixed effects: Higher surplus under certification if Firm H has high credibility; lower surplus if both firms certify.                         |


**Key Takeaways**  
- Certification eliminates credibility discounts, enhancing perceived environmental quality.  
- Market dynamics shift based on firm credibility: Firm L benefits most from certification, while Firm H may strategically avoid it.  
- Environmental outcomes improve under certification, but economic and social impacts vary, with trade-offs between firm profits and consumer surplus.  


# 5. Government Regulation

**Key Features of Regulation**  
- **Mandatory Standards**: Minimum environmental quality ($g^R$) applied to all firms.  
- **Objective**: Maximize societal welfare ($W_j = \Pi_L + \Pi_H + CS - \theta E$), balancing:  
	- **Economic Gains**: Firm profits ($\Pi_L, \Pi_H$)  
	- **Social Benefits**: Consumer surplus ($CS$)  
	- **Environmental Outcomes**: Reduced damage ($E$, weighted by $\theta$)  

**How Regulation Works**  
1. **Regulator Sets Standard** ($g^R$): Firms must meet or exceed $g^R$.  
2. **Firm Responses**: Firms self-label with $g_i^R \geq g^R$.  
3. **Pricing Stage**: Prices reflect environmental quality above $g^R$.  

**Equilibrium Outcomes**

| **Credibility Thresholds ($\mu_H$)** | **Regulatory Standard ($g^R$)** | **Firm Behavior**                                                                                 |
| ------------------------------------ | ------------------------------- | ------------------------------------------------------------------------------------------------- |
| $\mu_H \leq \mu^R$                   | High ($g^R_I$)                  | Both firms meet $g^R_I$ exactly ($g_L^R = g_H^R = g^R_I$); no differentiation; equal profits.     |
| $\mu^R < \mu_H < \bar{\mu}^R$        | Moderate ($g^R_{II}$)           | Firm L meets $g^R_{II}$; Firm H overcomplies ($g^R_H > g^R_{II}$), differentiating at extra cost. |
| $\mu_H \geq \bar{\mu}^R$             | Low ($g^R_{III}$)               | Regulation does not bind; firms revert to self-labeling choices ($g^R_L = g^S_L, g^R_H = g^S_H$). |


**Broader Impacts (Proposition 6)**  

| Metric                     | Impact of Regulation                                                                                     |
| -------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Economic Outcomes**      | Firm L profits may increase if $\mu_H$ is low; Firm H profits decrease due to reduced differentiation. |
| **Social Outcomes**        | Consumer surplus generally decreases under regulation due to reduced product differentiation.            |
| **Environmental Outcomes** | Regulation consistently reduces environmental damage, achieving its primary goal.                        |

**Key Takeaways on Regulation**  
- Enforces baseline environmental performance, benefiting the environment.  
- Limits firms’ ability to differentiate based on environmental quality, impacting profitability and consumer surplus.  
- Firm H face reduced profits, while less credible firms Firm L may benefit.  


# 6. The Role of Government

**Key Question**: How should the government act when external certification exists?  

**Framework Overview**  
1. **Regulatory Decision**:  
	- Regulator sets a mandatory minimum environmental standard ($\tilde{g}^R$).  
	- Goal: Maximize societal welfare (firm profits, consumer surplus, reduced environmental damage).  
2. **Certification Response**:  
	- NGO adjusts its certification scheme based on the regulatory standard.  
	- Certified claims are fully credible to consumers.  

**Equilibrium Outcomes**  

- Moderate $\mu_H$ 

| NGO\Government                              | Government Out                                 | Government In                                                                                                                   |
| ------------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **No Certification Adoption<br>(NGO Out)**  | self-labeling<br>$g_L = g^S_L, g_H = g^S_H$    | Strict $\tilde{g}^R$ imposed<br>Both firms meet $\tilde{g}^R$ exactly ($g_L = g_H = \tilde{g}^R$).<br>No differentiation.       |
| **Full Certification Adoption<br>(NGO In)** | Both firms meet $g^G_I$<br>$g_L = g_H = g^G_I$ | Strict $\tilde{g}^R>g^G_I$ imposed<br>Both firms meet $\tilde{g}^R$ exactly ($g_L = g_H = \tilde{g}^R$).<br>No differentiation. |
- High $\mu_H$ 

| NGO\Government                                 | Government Out                                                                      | Government In                                                                                                                         |
| ---------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **No Certification Adoption<br>(NGO Out)**     | self-labeling<br>$g_L = g^S_L, g_H = g^S_H$                                         | Equilibrium Outcomes of 5                                                                                                             |
| **Partial Certification Adoption<br>(NGO In)** | Firm L adopts certification<br>Firm H self-labels with lower quality ($g_H < g_L$). | No regulatory intervention ($\tilde{g}^R = 0$)<br>Firm L adopts certification<br>Firm H self-labels with lower quality ($g_H < g_L$). |
- Compare social welfare of outcome of equilibrium outcomes of 5 and $\tilde{g}^R=0$ with partial adaption
	- $\beta$ (Consumers’ valuation of perceived environmental quality) large $\iff$ NGO In SW > NGO Out SW

**When Should the Government Intervene?**
- **Non-Intervention Preferred If**:  
	- Firms (especially Firm H) are highly credible.  
	- Consumers place high value on environmental quality → differentiation enhances welfare.  
- **Intervention Necessary If**:  
	- Firms lack credibility or consumers undervalue environmental attributes → ensures minimum standards are met.  

