Martin A. Lariviere • Evan L. Porteus

# Introduction
- Supply Chain Contracts: Many transactions use simple price-only contracts (wholesale price) where the manufacturer sells to a retailer who is responsible for unsold items.
- Simplicity & Issues: Popular due to simplicity, but leads to inefficiencies, especially in decentralized systems, known as "double marginalization" (Spengler, 1950).
- Suboptimal Stocking: Retailers often stock less than optimal in such contracts.
- Returns Policies: Buyback rates and quantity limits can coordinate the supply chain and improve profit division (Pasternack 1985, Tsay 1999), but these policies incur administrative costs.
- Study Focus: Evaluates the performance of price-only contracts using a one-period model involving a manufacturer and retailer. It investigates:
	- Wholesale price determinants
	- Supply chain efficiency (measured as profit fraction)
	- Profit division
- Key Findings:
    - Role of Demand Variability: Lower variability (coefficient of variation) results in:
        - Higher wholesale prices
        - Improved supply chain efficiency
        - Larger manufacturer profit share
    - Manufacturer Advantage: Manufacturer benefits more than the retailer, especially with low demand variability.
    - Considerations for Lower Prices: Two factors may lead to lower wholesale prices:
        - Retailer participation in demand forecasting
        - Retailer power measured by opportunity cost or reservation utility
- __Research Questions:__
	1. What is the determinants of the wholesale price?
	2. How does demand distribution affect the supply chain efficiency?
	3. Division of realized supply chain profit.
	4. What factors makes manufacturer choose a lower wholesale price?
	5. Are price-only contracts effective?


# Model Formulation

**Model Overview:
- Manufacturer produces a good at cost $c$, sells to retailer at wholesale price $w$.
- Retail price $r$ is fixed.
- Demand has continuous distribution $\Phi(\bar{\Phi}=1-\Phi)$ with density $\phi$, with a finite mean.
- Manufacturer acts as Stackelberg leader, offering $w$ as take-it-or-leave-it.
- Retailer accepts terms that yield expected profit > 0.

**Integrated Firm Benchmark:**
- Integrated firm profit maximized by stocking level $y$.
- $$\Pi^I(y)=-cy+\int_o^yx\phi(x)dx+ry\bar{\Phi}(y)$$
- Optimal solution for integrated firm: $y^I = \Phi^{-1}[(r-c)/r]$.

**Retailer’s Problem:**
- Buys stock at wholesale price $w$ instead of cost $c$.
- $$\Pi^R(y)=-wy+\int_o^yx\phi(x)dx+ry\bar{\Phi}(y)$$
- Optimal solution for integrated firm: $y^R = \Phi^{-1}[(r-w)/r]$.

**Manufacturer’s Problem:**
- **Objective:** Set $w$ to maximize $M(w) = (w - c)y(w)$.
- **Inverse Demand Curve:** $y(w)$ as a function of $w$.
- **Marginal Revenue Function:**
	- $\frac{dM}{dy} = w(y) [1 - \frac{1}{v(y)}]$.
	- $v(y)$ = Elasticity of retailer’s order: $v(y) = \frac{w(y)}{y \frac{dw(y)}{dy}}$.
- **Generalized Failure Rate $g(y)$:**
	- $v(y) = \frac{1}{g(y)}$.
	- IGFR (Increasing Generalized Failure Rate): $g(y)$ is weakly increasing.
- **Theorem 1:**
	- **Conditions:** $\Phi$ is IGFR, finite mean, support $[a, b)$.
	- **Part (a):** First-order condition $(y)[1 - g(y)] = \frac{c}{r}$.
	- **Part (b):**
		- $\Pi^M(y)$ is unimodal on $[0, \infty)$.
		- Optimal $y^*$ is unique within $[a, \overline{y}]$.
		- Optimal sales quantity: $y^*$ or $a$.
- **Optimal Wholesale Price $w^*$:**
	- $w^* = \frac{c}{1 - g(y^*)}$.
	- **Dependency:** Decreases with higher elasticity $v(y^*)$.
		- High $v(y^*)$: Retailer is price sensitive → Lower $w^*$.
		- Low $v(y^*)$: Retailer less sensitive → Higher $w^*$.

# Impact of Market Size and Distribution Parameters

**Market Size**
- **Market Comparison**
	- **Markets 1 & 2**
	    - **Demand Distributions**: $\Phi_1$ is stochastically larger than $\Phi_2$ ($\Phi_1(x) \geq \Phi_2(x)$ for all $x$).
- **Theorem 2**
	- **Assumptions**:
	    - $\Phi_1(x) \geq \Phi_2(x)$ for all $x$.
	    - Generalized failure rates $g_1(x) \geq g_2(x)$ for all $x$.
	    - Optimal sales quantities $y_1^*$ and $y_2^*$ derived from Equation (4).
	- **Conclusions**:
	    - **(a)** Higher manufacturer profit in the larger market ($\Phi_1$).
	    - **(b)** If $g_1(x) \geq g_2(x)$, then $y_1^* \leq y_2^*$.
- **Insights**
	- Larger market leads to higher profit despite potentially lower sales quantity.
	- Optimal quantity influenced by both distribution shape $\Phi(x)$ and local behavior $\phi(x)$.
	- Demand elasticity is higher in larger markets, ensuring more sales.
	- **Note**: Theorem 2 does not specify wholesale price behavior.
- **Example: Uniform Demand Distributions**
	- **Markets Overview (r=10, c=4, uniform distribution$[A_i,B_i]$)**:
	    - **Market 1**: $A_1 = 100$, $B_1 = 500$, $y_1^* = 170$, $w_1^* = \$8.25$
	    - **Market 2**: $A_2 = 100$, $B_2 = 600$, $y_2^* = 200$, $w_2^* = \$8.00$
	    - **Market 3**: $A_3 = 180$, $B_3 = 500$, $y_3^* = 186$, $w_3^* = \$9.81$
	- **Findings**:
	    - Market 1: Smallest size, highest generalized failure rate, lowest sales quantity.
	    - Market 2: Larger than Market 1, lower price.
	    - Market 3: Highest price, not the smallest.
	- **Conclusion**: Market size ranks sales quantities but not wholesale prices.


__Determinants of the Wholesale Price__
1. **Wholesale Price Determination**
	- **Formula:**  $\hat{r}(y) = r[1 - g(y)]$
	- **Manufacturer’s Objective:** Determine the critical fractile for an adjusted retail price based on the demand distribution.
	- **Approach:** Focus on the fractiles of the demand distribution to set optimal prices.
2. **Theorem 3: Relationship Between Demand Distributions and Wholesale Prices**
	- **Assumptions:**
		- Two markets with demands $X_1$ and $X_2$.
		- Distributions: $\Phi_1$ and $\Phi_2$.
		- Generalized failure rates: $g_1$ and $g_2$.
		- $\Phi_1(0) = \Phi_2(0) = 0$.
		- $S(y) = \frac{\Phi_1^{-1}[\Phi_2(y)]}{y}$ is increasing in $y$.
	- **Conclusions:**
		- Optimal wholesale prices satisfy $w_1^* \leq w_2^*$.
		- $S(y)$ increases if $g_1[\Phi_1^{-1}(\alpha)] \leq g_2[\Phi_2^{-1}(\alpha)]$ for all $0 \leq \alpha \leq 1$.
3. **Star Order Concept**
	- **Definition:**  
	  If $S(x)$ is increasing in $x$, then $X_2$ is smaller than $X_1$ in the star order.
	- **Implications:**
		- **Scale Independence:** For any $\alpha > 0$, $\alpha X_2$ is smaller than $X_1$.
		- **Pricing Strategy:** Higher wholesale price is set if demand is $\alpha X_2$ compared to $X_1$.
		- **Exponential Distributions:** Wholesale price remains independent of the distribution’s mean.
4. **Lemma 1: Coefficient of Variation (CV) and Wholesale Price**
	- **Assumptions:**
		- Optimal quantity $y^*$ derived from Equation (4).
		- Demands modeled as $X_i = \delta_i + \lambda_i X$.
		- $\frac{\delta_1}{\lambda_1} < \frac{\delta_2}{\lambda_2}$.
	- **Conclusions:**
		- $w_1^* \leq w_2^*$.
		- Lower CV ($\frac{\delta}{\lambda}$) implies a higher wholesale price.
	- **Applicability:** Relevant for distributions like normal, gamma, and uniform.
5. **Practical Implications**
	- **Ordering of Wholesale Prices:**
		- Based on generalized failure rates or CV across different markets.
	- **Distribution-Specific Insights:**
		- **Gamma & Weibull Distributions:** Wholesale price increases with the shape parameter $k$.
		- **Normal Distribution:** Lower CV leads to higher wholesale prices.
		- **Uniform Distribution:** Consistent with Lemma 1; lower CV correlates with higher pricing.
	- **Example:**  
		- Market 1 (CV = 0.38) vs. Market 2 (CV = 0.41) vs. Market 3 (CV = 0.27):
			- Wholesale price ranking: Market 3 > Market 1 > Market 2.
6. **Summary**
	- **Demand Variability Impact:** Higher variability (higher CV) typically leads to lower wholesale prices, as manufacturers adjust prices based on the uncertainty in demand.
	- **Strategic Pricing:** Manufacturers leverage demand distribution characteristics (like CV and star order) to set optimal wholesale prices across different markets.
	- **Distribution Considerations:** Specific distribution properties (e.g., exponential, gamma) influence how demand variability affects pricing strategies.

---

# Supply-Chain Performance

- **Context**: Analyzes supply chain under a price-only contract.
- **Key Variables**:
	- **$\Pi^I$**: Integrated channel profit at optimal stocking level $y_I$.
	- **$\Pi^M, \Pi_R$**: Manufacturer and retailer profits with optimal quantity $y^*$ and price $w^*$.
	- **$\Pi^D$**: Decentralized system profit, $\Pi^D = \Pi^M + \Pi_R$.
- **Performance Aspects**:
	1. **Efficiency**: $\frac{\Pi^D}{\Pi^I}$ – fraction of possible profit attained.
	2. **Profit Division**:
	     - Ratio of profits $\frac{\Pi^M}{\Pi_R}$ or manufacturer’s share $\frac{\Pi^M}{\Pi^D}$.

__The Division of System Profit__
- **Profit Margins**:
	- Manufacturer: $w^*-c=r y^*\phi(y^*)$.
	- Retailer: $r-w^* =r \Phi(y^*)$.
- **Service Level Link**:
	- $\gamma=(w^*-c)/(r-w^*)$.
	- Connects service levels of decentralized vs. centralized systems.
- **Key Theorem**:
	- **Theorem 4**:
		- If distribution $\Phi$ is **concave** on $(0, y^*)$:
			- Service level in $[ \frac{r-c}{2r}, \frac{r-c}{r} ]$.
			- Retailer can capture >50% of $D$.
	    - If $\Phi$ is **convex** on $(0, y^*)$:
			- Service level < $\frac{r-c}{2r}$.
			- Manufacturer captures >50% of $\Pi^D$.
	- **Implications**:
		- **Concave $\Phi$**: High service level, retailer gains larger profit share.
		- **Convex $\Phi$**: Low service level, manufacturer dominates profit share.
- **Power Function Distribution**:
	- $\Phi(x) = (x/\theta)^k$, $k > 0, 0\leq x\leq\theta$.
	- Concave for $k < 1$; convex for $k > 1$.
	- Profit Sharing:
		- Retailer never captures >50% profit for power distribution.
		- Manufacturer typically captures majority profit, especially for large $k$.
	- CV decreases as $k$ increases.
- **Corollary 1**:
	- Conditions when $y^*$ is on convex portion:
	    - **Normal Distribution**: Specific CV threshold.
	    - **Gamma Distribution**: $k \geq 3.83$.
	    - **Weibull Distribution**: $k \geq 2$.
	- **Outcome**: Manufacturer often captures majority profit with common distributions.
- __Summary__
	- **Profit Sharing** is heavily influenced by the **concavity or convexity** of the demand distribution.
	    - **Concave $\Phi$**: Higher service levels, retailer gains more.
	    - **Convex $\Phi$**: Lower service levels, manufacturer gains more.
	- **Common Distributions** (Normal, Gamma, Weibull) often result in the manufacturer capturing the majority of profits, especially under conditions of convex demand characteristics.
	- **Retailer Advantage**: Limited to specific distribution shapes (primarily concave) and typically cannot exceed a 50% profit share in many common scenarios.

__Supply-Chain Efficiency__
- **Efficiency Measure**: $\frac{\Pi^D}{\Pi^I}$.
- **Findings**:
	- Efficiency improves as coefficient of variation (CV) decreases.
	- Initial drop in efficiency possible as CV falls, then improves.
	- Highest efficiency at lowest CV across all cost structures.
- **General Demand Model**:
	- **Theorem 5**:
	    - Demand $D = \delta+\lambda X$, $X$ is IGFR with distribution $\Phi$.
	    - (a) $\frac{\Pi^D}{\Pi^I}$ independent of parameter.
	    - (b) $\frac{\Pi^M}{\Pi^I}$ decreases with CV; $\frac{\Pi^D}{\Pi^I}$ approaches 1 as $\Psi$ → 0.
	- **Interpretation**:
	    - Reduced variability → Improved efficiency.
	    - Paradox: Lower variability → Higher wholesale price & worse service.
	    - Efficiency gains from smaller deviation between decentralized and centralized quantities.
- **Examples**:
	- **Normal Distribution**: Reduced variance tightens stocking around mean.
	- **Gamma Distribution**: Similar trend as CV decreases.
- __Summary__
	- **Less demand variability** → **Better efficiency** in the supply chain.
	- Efficiency improves as **inventory levels** between different parts of the supply chain become **more aligned**.
	- **Trade-offs**:
	    - **Higher prices** from manufacturers.
	    - **Worse service** (more stockouts).
	- **Main Point**: Reducing demand variability helps the supply chain run more smoothly, even though it may increase costs or lower service in some cases.

# Why the Manufacturer May Choose a Lower Price

**Simplicity of Price-Only Contracts:**
- Price-only contracts are attractive because they are simple.
- If demand variability is low, a **returns policy** may not be worth the additional cost.
- For low coefficients of variation (CVs), decentralized systems capture 75–80% of possible profit.
- The manufacturer tends to profit more by taking a larger share of the profit rather than improving overall efficiency.

**Forecasting Incentives:**
- If demand variability is reduced through **forecasting**, the manufacturer sets a higher wholesale price.
- If the manufacturer forecasts alone, it is beneficial for them.
- If forecasting is a joint effort, the retailer should be cautious because the manufacturer may raise the price afterward, reducing the retailer's profit.
- **Collaborative forecasting** requires a guarantee that both parties share the benefits fairly.

**Retailer Power:**
- If the retailer has an **opportunity cost (K)**, the manufacturer must offer a wholesale price that allows the retailer to earn at least **K**.
- A more powerful retailer (with higher **K**) forces the manufacturer to improve supply-chain performance by increasing stocking levels.
- **Higher retailer power** moves stocking levels closer to an integrated system, benefiting the overall supply chain while maintaining most of the manufacturer's profit. 