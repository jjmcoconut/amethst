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


---


Good morning, everyone. Thank you for joining me today as we explore the fascinating world of green product development and the strategic role of ecolabels and environmental regulation. Today’s presentation is based on insights from the paper **“The Effects of Ecolabels and Environmental Regulation on Green Product Development,”** published in the _Manufacturing and Service Operations Management_ journal by INFORMS.

#### Ecolabels: Communicating the Unobservable

Unlike many product attributes—such as taste, texture, or design—that consumers can directly experience, environmental quality is inherently unobservable. This is where ecolabels come in. They serve as a critical communication tool that allows companies to convey their environmental efforts to the marketplace.

There are two main types of ecolabels:
4. **Self-Labels (Type 2 Ecolabels):**
    - Many retailers use self-labels to brand their products. For example, Whole Foods Market labels its 365 line as “Responsibly Grown,” while Walmart uses “Natural” on its Great Value cleaning products.
    - However, a drawback of self-labels is that they are sometimes met with skepticism. Without third-party verification, consumers may undervalue these claims, leading to a decreased willingness to pay.
5. **External Certifications (Type 1 Ecolabels):**
    - External certifications come from recognized bodies such as the U.S. Department of Agriculture for organically grown produce or the Marine Stewardship Council for responsibly sourced seafood.
    - These certifications tend to be more trusted by consumers, thereby enhancing a firm’s credibility and enabling them to command higher prices.

#### The Bigger Picture: Voluntary and Mandatory Approaches

The paper we’re discussing doesn’t stop at just exploring ecolabels. It also delves into the interplay between voluntary environmental initiatives and mandatory government regulation:

- **Voluntary Initiatives:**  
    Firms can choose between self-labeling and obtaining external certifications. The decision often hinges on their existing credibility. Generally, firms with lower credibility find it beneficial to pursue external certifications to build consumer trust. In contrast, highly credible firms might rely on their reputation and sometimes even avoid the extra cost of certification.
- **Government Regulation:**  
    Beyond voluntary measures, government agencies are actively involved in pushing firms toward better environmental performance. Regulations—like California’s Green Chemistry Law, which mandates the use of environmentally benign chemicals—set minimum standards that all firms must meet. Such regulations help address credibility concerns that arise from self-labeling. However, they also introduce challenges by imposing uniform standards that might stifle competition or overlook the nuanced value consumers place on environmental impro

#### Objectives and Roadmap
1. What is the impact of firm credibility and competition?
2. What is the impact of external certification?
3. When and how should the government intervene?

---


Let’s now dive into the heart of our analysis—the base model that underpins the study. This model lays the groundwork for understanding how firms compete on environmental quality using self-labels, before we bring in external certifications or government regulation. I'll walk you through the key components.

#### Modeling Environmental Quality Competition

**1. Two Competing Firms with Differing Credibilities**
We consider a simple setting with **two firms**, which we’ll call **Firm H** and **Firm L**. These firms are asymmetric in terms of their environmental credibility:

- Each firm’s credibility is denoted by $\mu_i$, where $i \in \{H, L\}$.
- We assume that $0 < \mu_L < \mu_H < 1$, meaning that Firm H is inherently more credible than Firm L.

An important assumption here is that credibility is **exogenous**—it is fixed and does not change based on the firms’ actions or competitors’ responses. (Later on, we extend the model to allow for dynamic reputational changes, but for now, this assumption keeps our analysis tractable.)

**2. Self-Labeling in the Absence of External Checks**
In our base case, there’s no external certification or government regulation. Firms rely solely on **self-labeling** to communicate their environmental quality. However, because consumers remain somewhat skeptical about self-declared claims, a product’s **perceived environmental quality** is given by the product of the firm’s credibility and the actual quality level, that is, $\mu_i\cdot g_i$.

- **Environmental Quality Choice:**  
    Each firm chooses an environmental quality level, $g_i$, from the interval $(0, 1)$. Think of $g_i$ as representing the percentage reduction in pollution or the degree of environmental improvement per unit of product.
- **Cost of Quality:**  
    To achieve a given level of environmental quality, a firm incurs a **quadratic cost** of $g_i^2$. This cost captures research and development expenditures or other investments needed to enhance environmental performance. Variable production costs are assumed to be independent of $g_i$ and normalized to zero.

**3. Consumer Demand—Price and Perceived Environmental Quality Matter**
- $q_H=\frac{1}{2}-p_H+(p_L-p_H)+\beta(\mu_Hg_H-\mu_Lg_L)$
- $q_L=\frac{1}{2}-p_L+(p_H-p_L)+\beta(\mu_Lg_L-\mu_Hg_H)$

Consumers make purchasing decisions based on two factors:
- **Price Sensitivity:**  
    As expected, an increase in a firm’s price results in a drop in demand. Specifically, for every unit increase in price, one consumer leaves the market or switches to the competitor.
- **Preference for Environmental Quality:**  
    Consumers also care about environmental performance. However, since they can’t directly observe the true quality, they base their decisions on the **perceived quality**, $\mu_i\cdot g_i$. A higher perceived quality translates into higher demand, all else being equal.

Each firm’s profit is then given by:  
$\Pi_i=q_i⋅p_i−g_i^2$​, where $q_i$ is the demand for Firm i’s product and $p_i$ is its price. Notice that the cost component, $g_i^2$, represents the fixed cost associated with achieving a higher environmental standard.

**4. The Two-Stage Game**
The competition unfolds in two stages:
- **Stage 1: Quality Choice (Self-Labeling)**  
    Both firms simultaneously decide on the environmental quality level for their products.
- **Stage 2: Pricing Decision**  
    After announcing their quality levels, the firms set their prices simultaneously to maximize profits.

#### Evaluating Broader Implications: The 3BL Metrics
To assess the broader impact of these competitive choices, we adopt three key metrics:
4. **Social Implications (Consumer Surplus):**  
    Consumer surplus is used to measure the social benefits that accrue from the competition. It reflects how much value consumers derive from both lower prices and the environmental quality differentiation between the products.
5. **Environmental Implications (Environmental Damage):**  $E^j=\sum q_i^j(1-g_i^j)$
    We define environmental damage as the total amount of pollutants released into the environment. For each unit of product, the amount of pollution is ($1 - g_i$), so higher environmental quality (a higher $g_i$) directly translates into lower environmental damage.
6. **Economic Implications (Firm Profits):**  
    Finally, each firm’s profit is considered as the economic outcome. Changes in credibility and the ensuing quality choices affect not only the competitive positioning but also the profitability of the firms.

This framework provides a clear picture of how firm credibility and self-labeling drive green product development in the absence of external checks. In the next part of our discussion, we will build on this foundation to explore how voluntary external certification and government regulation further influence these dynamics.

---

Let's now add another layer to our analysis—**voluntary external certification**. Up until now, we've seen how firms compete using self-labels, where the environmental quality consumers perceive is discounted by the firm’s credibility. But what happens when an **external certifier** steps in?

#### Introducing External Certification

In this section, we consider a scenario where an external party—specifically, an NGO dedicated to minimizing environmental damage—offers a certification program. Remember, the key here is that external certification is inherently more credible. That means if a firm’s product carries the NGO’s certification, consumers perceive its environmental quality exactly as stated, without any credibility discount. In contrast, a self-labeled product is still seen as having quality multiplied by the firm’s credibility ($\mu_i\cdot g_i$).

**How Does the Certification Work?**  
The process unfolds in a few steps:
7. **Certification Announcement:**  
    The NGO first announces its certification scheme. It sets an environmental quality target, which we call $g^G$ (with $g^G \geq 0$), and it also specifies a fixed certification fee, denoted by $\tau^G$.
8. **Firm Decision—Adopt or Not?**  
    With the certification scheme in place, each of the two firms (H and L) then decides simultaneously whether to adopt this external certification (G) or stick with their self-label (S).
9. **Quality Choice and Pricing:**  
    After choosing their certification path, both firms then decide on the environmental quality level for their products and set their prices in a similar two-stage process as before.

An important insight from the analysis is that **the NGO ends up not charging any certification fee**—that is, $\tau^{G*}=0$. This zero fee allows the NGO to demand the highest possible environmental quality improvement from any firm that chooses to be certified, essentially using credibility as its currency.

#### How Do Firms Respond?

The introduction of external certification leads to a fascinating strategic twist, which the paper details in **Proposition 3**. The outcome depends critically on a threshold value of Firm H’s credibility relative to Firm L, denoted as $\bar{\mu}^G(\mu_L)$. Two distinct scenarios emerge:
10. **Full Certification Adoption:**
    - **When $\mu_H$ is relatively low**, the NGO sets an environmental quality standard $g^G_I$.
    - In this case, both firms find it beneficial to adopt the external certification.
    - As a result, both Firm H and Firm L offer the same certified environmental quality  and end up earning the same profit.
11. **Partial Certification Adoption:**
    - **When $\mu_H$ is high**, the NGO responds by setting a higher environmental quality target, $g^G_{II}$, where $g^G_{II} > g^G_I$.
    - Here, Firm L—suffering more from credibility discounting—chooses to adopt the certification to boost its perceived quality.
    - In contrast, Firm H, enjoying higher inherent credibility, opts to self-label. Consequently, Firm H sets a lower environmental quality so that it can differentiate its product and maintain profitability.

#### Comparing the Broader Impacts

Finally, let's look at how external certification affects the overall stakeholder outcomes using the 3BL metrics—social, environmental, and economic.

**Key Findings from Proposition 4:**
- **Profit Implications:**  
    Firm H’s profit under self-labeling is higher than under certification, while Firm L’s profit improves with certification. In the partial adoption scenario, this reversal makes Firm L the profit leader.
- **Environmental Outcomes:**  
    Certification consistently reduces environmental damage. That is, the environmental damage under certification ($E^G$) is lower than under self-labeling ($E^S$). This makes sense because certification forces firms to meet a higher, more credible quality standard.
- **Consumer Surplus:**  
    The impact on consumer surplus is mixed:
    - If Firm H’s credibility is relatively low, then consumer surplus is higher under self-labeling.
    - Conversely, if Firm H’s credibility is high, the enhanced differentiation in environmental quality improves consumer surplus under certification.


#### Wrapping Up This Section

To summarize this part:

- **External certification** removes the credibility discount that self-labels suffer, providing a clear signal of environmental quality.
- Depending on the relative credibility of the competing firms, we see two distinct outcomes: either both firms adopt certification or only the less credible firm does so, with important implications for market leadership in environmental quality and profitability.
- **Environmental benefits** are clear: certification reduces overall environmental damage. However, the economic and social impacts are more complex, creating winners and losers among the firms and affecting consumer surplus in different ways.

---

Let’s now turn our attention to another critical mechanism for driving green product development: **government regulation**. Unlike external certification—which is voluntary and applies selectively—government regulation is mandatory. It affects both firms simultaneously and is designed to safeguard the interests of all stakeholders.


#### The Regulator’s Objective

In this framework, the government steps in with a **mandatory minimum environmental standard**, denoted by $g^R​\geq0$. The regulator’s aim is to maximize overall societal welfare by balancing three key elements:
- **Economic Gains:** The profits of both firms.
- **Social Benefits:** Consumer surplus.
- **Environmental Outcomes:** The level of environmental damage, which is penalized by a coefficient $\theta$ (with $\theta$ capturing how much weight the regulator places on environmental damage).

Mathematically, societal welfare is defined as: $W^j:=\Pi^j_L+\Pi_H^j+CS^j-\theta E^j$
This objective function ensures that the regulator values not only the profits and consumer benefits but also converts environmental damage into a comparable dollar value.

#### How Regulation Works in Our Model

Once the regulator sets the mandatory standard $g^R$​, both firms are required to label their products accordingly—they must at least meet this minimum environmental quality. However, the twist lies in consumer perception. Under regulation, consumers only discount environmental quality claims by the extent that a product exceeds the minimum standard. In other words, the demand functions adjust so that any quality above $g^R$​ is what drives consumer choice.

**Sequence of Events Under Regulation:**
12. **Regulatory Decision:**  
    The regulator chooses $g^R$​ to maximize societal welfare.
13. **Firm Responses:**  
    given $g^R$​, each firm must self-label its product with an environmental quality $g_i^R$​ that is at least $g^R$.
14. **Pricing Stage:**  
    Firms then set their prices, and consumer demand is influenced by the extent to which their products’ environmental qualities—beyond $g^R$​—differ.

#### Equilibrium Outcomes Under Regulation

The equilibrium under regulation depends on the relative credibility of the firms, particularly that of Firm H, denoted by $\mu_H​$. Two thresholds in $\mu_H$​ emerge from the analysis—let’s call them $\mu^R$​ and $\underset{\bar{}}{\mu}^R$. These thresholds partition the outcomes into three regions:
- If $\mu_H\leq\underset{\bar{}}{\mu}^R$, the regulator imposes a relatively **stringent standard**, $g^R_I$. Both firms are compelled to exactly meet this standard: $g^R_L=g^R_H=g^R_I$. In this scenario, both firms’ profits become equal, as they have no scope to differentiate based on environmental quality.
- When $\mu^R<\mu_H<\underset{\bar{}}{\mu}^R$, the regulator sets a **less stringent standard**, $g^R_{II}$, where $g^R_{II}​$ falls between the self-labeling choices $g^S_L​$ and $g^S_H$​ that we observed in the absence of regulation. Here, Firm L meets the minimum exactly, while Firm H opts to **overcomply**—choosing an environmental quality higher than $g^R_{II}​$. This overcompliance allows Firm H to differentiate its product, though it comes at an extra cost.
- If $\mu_H\geq\underset{\bar{}}{\mu}^R​$, then the regulator imposes a standard gRIIIgRIII​ that is effectively so low that it does not bind—meaning the firms revert to their self-labeling decisions. In this region, the government effectively chooses not to intervene because Firm H’s high credibility already drives high environmental quality.

#### Overall 3BL Implications

- **Economic Outcomes:**  
    Regulation tends to reduce the profits of Firm H relative to the self-labeling scenario ($\Pi^S_H>\Pi^R_H$​). For Firm L, regulation may benefit it if and only if $\mu_H$ is sufficiently low.
- **Social Outcomes (Consumer Surplus):**  
    Consumer surplus under regulation ($CS^R$​) is generally lower than that under self-labeling ($CS^S$​). This is due to the reduced differentiation in product attributes that consumers value.
- **Environmental Outcomes:**  
    On the environmental front, regulation consistently **reduces environmental damage** ($E^R<E^S$), achieving one of its primary objectives.

#### Concluding Thoughts on Regulation
To sum up, government regulation acts as a blunt but effective instrument:

- **It enforces a baseline level of environmental performance** that both firms must adhere to, thereby benefiting the environment.
- **It adjusts the competitive landscape** by limiting how much firms can differentiate themselves based on environmental quality.
- **It creates trade-offs:** While it improves environmental outcomes and may even boost Firm L’s standing, it can reduce consumer surplus and penalize the more credible Firm H.

---

Now that we’ve examined how both voluntary external certification and mandatory regulation shape green product development individually, let’s explore how these two mechanisms interact when they operate simultaneously. In today’s market, with firms increasingly able—and motivated—to signal their environmental performance voluntarily, governments find themselves in a position where they must decide: Should they intervene, or should they let the voluntary mechanisms, like NGO certification, do the heavy lifting?

#### 6. The Role of Government

In this next section, we ask: **How should the government act when external certification is already in play?** With rising voluntary environmental initiatives, governments are now operating in an ecosystem where firms not only improve their environmental performance but also actively communicate these improvements. This raises an important question: **To intervene or not to intervene?**

The framework we consider now involves a two-stage process:
15. **Regulatory Decision:**  
    First, a societal welfare–maximizing regulator sets a **mandatory minimum environmental standard**. We denote this standard with a $\tilde{g}^R$​, to indicate that we’re now looking at outcomes when both regulation and external certification coexist.
16. **Certification Response:**  
    After the regulator makes its move, an NGO—whose objective is to minimize environmental damage—announces an external certification scheme. Importantly, this NGO has the flexibility to adjust its certification in response to the government’s imposed standard.


#### When Should the Government Intervene?

- **If firms, particularly Firm H, are already highly credible and if consumers place a high premium on environmental quality, then government non-intervention is preferable.** This scenario allows the NGO to drive beneficial product differentiation, thereby enhancing consumer surplus and overall societal welfare.
- **If, however, firms are less credible or consumers undervalue environmental quality, the government should step in.** In that case, regulatory intervention ensures that both firms meet a minimum standard, although it may reduce consumer surplus by limiting differentiation.

