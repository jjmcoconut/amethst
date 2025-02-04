Soo-Haeng Cho, Christopher S. Tang

# 1. Introduction
## Flu Vaccine Industry Overview
- Mismatches in demand and supply are common
- Causes:
  - Production yield uncertainty (biological nature)
  - Demand uncertainty (flu activity unpredictability)

## Examples of Supply-Demand Mismatch
- 2006-2007 season: 18.4 million dose oversupply
- 2004-2005 season: 50 million dose undersupply (Chiron plant contamination)

## Research Focus
- Evaluating selling strategies for vaccine manufacturers
- Managing uncertain supply and demand

## Key Questions
1. When should manufacturers sell vaccines?
	- Before uncertainties resolved
	- After uncertainties resolved
	- Both before and after
2. Retailer benefits:
	- Postponing orders?
	- Additional ordering opportunity?

## Selling Strategies Examined
1. Advance selling
2. Regular selling
3. Dynamic selling (combination of 1 and 2)

## Trade-offs in Selling Strategies
- Prebook vs. regular wholesale price
- Risk-bearing: retailer vs. manufacturer
- Dynamic interactions in combined strategy

## Model Characteristics
- Stackelberg games (manufacturer as leader, retailer as follower)
- Uncertain supply and demand (uncorrelated)
- Fixed capacity and full utilization
- No demand forecast updating
- Stackelberg vertical competition
- Uncertain retail price

## Key Findings
1. Manufacturer perspective:
	- Dynamic selling strategy dominates
	- Demand uncertainty beneficial
	- Supply uncertainty detrimental
2. Retailer perspective (counterintuitive results):
	- Postponing ordering can be detrimental
	- More ordering opportunities can be detrimental
	- Supply uncertainty can be beneficial


# 3. Model
- Two-level: One manufacturer ($M$) and one retailer ($R$)
- Seasonal product
- Long production lead time
- Zero variable production cost
- Unsold products discarded after season

## Key Variables
- $k$: Production capacity (fixed)
- $\tilde{\theta}$: Random production yield
- $\tilde{\epsilon}$: Random demand component
- $p$: Retail price ($p = 1 + \tilde{\epsilon} - q$)
- $q$: Quantity available for sales

## Assumptions
- Proportional random yield model
- Linear demand curve
- Inventory "clearance" rule
- Independent $\tilde{\epsilon}$ and $\tilde{\theta}$
- Common knowledge of distributions and capacity

## Selling Strategies
1. Dynamic Selling Strategy
	- Period 1: Prebook $w_1, x_1$ (Before $\tilde{\theta},\tilde{\epsilon}$ is realized)
		- Manufacturer observes $\tilde{\theta}$ and delivers $a_1=\min\{k\theta,x_1\}$
	- Period 2: Regular order $w_2, x_2$ (After observing $\theta,\epsilon$)
		- Manufacturer delivers $a_2=\min\{k\theta-a_1,x_2\}$
	- $q=a_1+a_2$
	- $p=1+\epsilon-(a_1+a_2)=1+\epsilon-\min\{k\theta,x_1\}-\min\{k\theta-a_1,x_2\}$
1. Advance Selling Strategy
	- Prebook only $w_1, x_1$ (Before $\tilde{\theta},\tilde{\epsilon}$ is realized)
	- $q=a_1=\min\{k\theta,x_1\}$
	- $p=1+\epsilon-\min\{k\theta,x_1\}$
2. Regular Selling Strategy
	- Regular order only $w_2, x_2$ (After observing $\theta,\epsilon$)
	- $q=a_2=\min\{k\theta,x_2\}$
	- $p=1+\epsilon-\min\{k\theta,x_2\}$

## Model Notation

| Symbol             | Definition                                 |
| ------------------ | ------------------------------------------ |
| $k$                | Production capacity                        |
| $\tilde{\theta}$   | Random production yield                    |
| $\tilde{\epsilon}$ | Random demand component                    |
| $p$                | Retail price                               |
| $q$                | Quantity available for sales               |
| $(w_1, x_1)$       | Prebook wholesale price and order quantity |
| $(w_2, x_2)$       | Regular wholesale price and order quantity |
| $a_1$              | Quantity delivered for prebook order       |
| $a_2$              | Quantity delivered for regular order       |
| $\Pi_M, \Pi_R$     | Manufacturer's profit, retailer's profit   |


# 4. Equilibrium Analysis
- We use backward induction to derive subgame-perfect Nash equilibrium
## 4.1 Dynamic Selling Strategy

### Second Period
- $l'\equiv k\theta-a_1=k\theta-\min\{k\theta,x_1\}$: Remaining supply after first period
	- Consider only when $l'>0(a_1=x_1)$
- $a_2 = \min\{l',x_2\}$
- $p=1+\epsilon-x_1-\min\{l',x_2\}$
- $\Pi_R(x_2,w_2;x_1,w_1)=[(1+\epsilon-x_1-\min\{l',x_2\})-w_2]\min\{l',x_2\}+[(1+\epsilon-x_1-\min\{l',x_2\})-w_1]x_1$
- Optimum regular order quantity: $x^{AB}_2(x_1, w_2) = \max\{0, (m' - w_2)/2\}, \text{ where } m' ≡ 1 + \epsilon - 2x_1$
- Actual quantity delivered: $\min\{l',x^{AB}_2\}$
- $$\begin{align} \Pi_M(w_2;x_1,w_1,m',l')&=w_2a_2^{AB}+w_1a_1\\&=\begin{cases}w_1x_1 &\text{if } m'\leq0\text{ or }w_2>m'\\ w_2l'+w_1x_1 &\text{if } m'>0\text{ and } w_2\leq m'-2l'\\ w_2\frac{m'-w_2}{2}+w_1x_1 &\text{if } m'>0\text{ and } w'-2l'<w_2<m'\end{cases} \end{align}$$
- Ex post equilibrium outcomes (Lemma 2):
	- Case (i): $m' > 0$ and $l' ≥ m'/4$ 
		- $w_2^{AB}=m'/2$
		- $\Pi_M(x_1,w_1)=m'^2/8+w_1x_1$
		- $x_2^{AB}(x_1)=m'/4$
		- $\Pi_R(x_1,w_1)=m'^2/16+(1+\epsilon-x_1-w_1)x_1$
		- Behave as if there is no supply constraint, outcomes are independent of $k$
	- Case (ii): $m' > 0$ and $l' < m'/4$
		- $w_2^{AB}=m'-2l'$
		- $\Pi_M(x_1,w_1)=(m'-2l')l'+w_1x_1$
		- $x_2^{AB}(x_1)=l'$
		- $\Pi_R(x_1,w_1)=l'^2+(1+\epsilon-x_1-w_1)x_1$
		- $m'$ positive but limited to $l'$ -> Compensate lower sales volume: increase $w_2^{AB}$ 
	- Case (iii): $m' ≤ 0$
		- $w_2^{AB}>0$
		- $\Pi_M(x_1,w_1)=w_1x_1$
		- $x_2^{AB}(x_1)=0$
		- $\Pi_R(x_1,w_1)=(1+\epsilon-x_1-w_1)x_1$
		- Realized market potential $m'\leq0$: No orders

### First Period
- $$\begin{align} E_{\tilde{\theta},\tilde{\epsilon}}[\Pi_R(x_1,w_1)]=&E_{\tilde{\theta},\tilde{\epsilon}}[\{(1+\tilde{\epsilon}-\min\{k\tilde{\theta},x_1\})-w_1\}\min\{k\tilde{\theta},x_1\}] \\ &+P\left(\tilde{m}'>0,\tilde{l}'\geq\frac{\tilde{m}'}{4}\right)E_{\tilde{\theta},\tilde{\epsilon}}\left[\frac{\tilde{m}'^2}{16}\middle|\tilde{m}'>0,\tilde{l}'\geq\frac{\tilde{m}'}{4}\right] \\ &+P\left(\tilde{m}'>0,0<\tilde{l}'<\frac{\tilde{m}'}{4}\right)E_{\tilde{\theta},\tilde{\epsilon}}\left[\tilde{l}'^2\middle|\tilde{m}'>0,0<\tilde{l}'<\frac{\tilde{m}'}{4}\right] \end{align}$$
	- $\tilde{m}'=1+\tilde{\epsilon}-2x_1,\tilde{l}'=k\tilde{\theta}-x_1$
- $$\begin{align} E_{\tilde{\theta},\tilde{\epsilon}}[\Pi_M(x_1,w_1)]=&E_{\tilde{\theta},\tilde{\epsilon}}[w_1\min\{k\tilde{\theta},x_1\}] \\ &+P\left(\tilde{m}'>0,\tilde{l}'\geq\frac{\tilde{m}'}{4}\right)E_{\tilde{\theta},\tilde{\epsilon}}\left[\frac{\tilde{m}'^2}{8}\middle|\tilde{m}'>0,\tilde{l}'\geq\frac{\tilde{m}'}{4}\right] \\ &+P\left(\tilde{m}'>0,0<\tilde{l}'<\frac{\tilde{m}'}{4}\right)E_{\tilde{\theta},\tilde{\epsilon}}\left[(\tilde{m}'-2\tilde{l}')\tilde{l}'\middle|\tilde{m}'>0,0<\tilde{l}'<\frac{\tilde{m}'}{4}\right] \end{align}$$
- No closed-form expressions for $x^{AB}_1(w_1)$ and $w^{AB}_1$

## 4.2 Advance or Regular Selling Strategy

#### 4.2.1 Advance Selling Strategy
- Single-period Stackelberg game before uncertainties resolved
- Retailer's expected profit
	- $E_{\tilde{\theta},\tilde{\epsilon}}[\Pi_R(x_1,w_1)]=E_{\tilde{\theta},\tilde{\epsilon}}[\{(1+\tilde{\epsilon}-\min\{k\tilde{\theta},x_1\})-w_1\}\min\{k\tilde{\theta},x_1\}]$
- Manufacturer's expected profit
	- $E_{\tilde{\theta},\tilde{\epsilon}}[\Pi_M(w_1)]=E_{\tilde{\theta},\tilde{\epsilon}}[w_1\min\{k\tilde{\theta},x_1^A(w_1)\}]$
	- Predicting retailer's BR $x_1^A(w_1)$, manufacturer optimizes $w_1^A$
- Equilibrium outcomes (Lemma 3):
	- Retailer's optimal prebook order quantity: $x^A_1(w1) = \max\{0, (1 - w_1)/2\}$
	- Case (i): $k\theta_L ≥ 0.25$ (No supply shortage)
		- $w_1^A=1/2$
		- $E\Pi_M^A=1/8$
		- $x_1^A(w_1)=1/4$
		- $E\Pi_R^A=1/16$
	- Case (ii): $k\theta_L < 0.25$ (Supply shortage)
		- $w_1^A>1/2$
		- $E\Pi_M^A<1/8$
		- $x_1^A(w_1)<1/4$
		- $E\Pi_R^A<1/16$

### 4.2.2 Regular Selling Strategy
- Single-period Stackelberg game after uncertainties resolved
- Retailer's profit function
	- $\Pi_R(x_2,w_2)=\{(1+\epsilon-\min\{k\theta,x_2\})-w_2\}\min\{k\theta,x_2\}$
- Manufacturer's profit function
	- $\Pi_M(w_2) = w_2 \min\{k\theta, x^B_2(w_2)\}$
- Ex post equilibrium outcomes (Corollary 1):
	- Case (i): $k\theta ≥ (1 + \epsilon)/4$
		- $w_2^B=(1+\epsilon)/2$
		- $\Pi_M^B=(1+\epsilon)^2/8$
		- $x_2^B(w_2^B)=(1+\epsilon)/4$
		- $\Pi_R^B=(1+\epsilon)^2/16$
	- Case (ii): $k\theta < (1 + \epsilon)/4$
		- $w_2^B=1+\epsilon-2k\theta$
		- $\Pi_M^B=(1+\epsilon-2k\theta)k\theta$
		- $x_2^B(w_2^B)=k\theta$
		- $\Pi_R^B=(k\theta)^2$


# 5. Profit Comparison Under Different Selling Strategies

## 5.1 Advance Selling vs. Regular Selling

#### Theorem 1:
- Manufacturer's perspective:
	- Regular selling dominates advance selling ($E\Pi^B_M ≥ E\Pi^A_M$)
		- Manufacturer can utilize information about the realized supply to set his regular wholesale price
	- Equality holds when:
		1. No supply uncertainty and retailer's demand always exceeds supply
		2. No demand uncertainty and supply always sufficient
		- If one of these hold, information of $\tilde{\theta},\tilde{\epsilon}$ does not have any value
- Retailer's perspective:
	- With ample supply: Regular selling dominates ($E\Pi^B_R ≥ E\Pi^A_R$)
	- With potential supply shortage
		- Manufacturer sets a high wholesale price
		- Advance selling can dominate ($E\Pi^A_R > E\Pi^B_R$) but not always
			- For moderate size $k$ which still implies shortage

## 5.2 Dynamic Selling vs. Advance or Regular Selling

### Lemma 4:
- Dynamic selling dominates regular selling for both firms
	- Manufacturer can always set $w_1$ high enough to let retailer choose $x^{AB}_1(w_1)=0$
- $E\Pi^{AB}_M ≥ E\Pi^B_M$ and $E\Pi^{AB}_R ≥ E\Pi^B_R$
- Equality holds when $x^{AB}_1 = 0$
	- Does not dominate advance selling because setting $w_2$ high to get $x_2=0$ is not credible

### Theorem 2:
- Manufacturer's perspective:
	- Dynamic selling dominates advance selling ($E\Pi^{AB}_M ≥ E\Pi^A_M$)
		- $\because E\Pi^{AB}_M≥ E\Pi^B_M ≥ E\Pi^A_M$ (Lemma 4 & Theorem 1(a))
- Retailer's perspective:
	- With ample supply: Dynamic selling dominates ($E\Pi^{AB}_R ≥ E\Pi^A_R$)
	- With potential supply shortage: Advance selling can dominate ($E\Pi^A_R > E\Pi^{AB}_R$)

# 6. Numerical Study

### Setup:
- $\tilde{\theta}$: Uniform distribution between $1-r$ and $1+r$ ($r ∈ (0,1)$)
- $\tilde{\epsilon}$: High demand ($e$) with 0.5 probability, low demand ($-e$) with 0.5 probability ($e ∈ (0,0.75)$)
- 630 scenarios: $k$ (0.1 to 1), $e$ (0.1 to 0.7), $r$ (0.1 to 0.9)

### Key Findings:
1. Confirms results from Theorems 1 and 2
2. $E\Pi^{AB}_R < E\Pi^A_R$ when capacity k is tight

## 6.1 Comparative Statics

#### General observations:
- Expected profits of both firms are nondecreasing in capacity $k$

#### Advance selling strategy:
- Higher supply uncertainty hurts manufacturer's profit
	- As supply uncertainty increases, the manufacturer bears more risk because he receives all orders before the uncertainties are resolved
- Supply uncertainty can benefit retailer
	- Manufacturer reduces his prebook wholesale price to secure a larger prebook order from the retailer
- Demand uncertainty $e$ doesn't affect equilibrium outcomes

#### Regular selling strategy:
- Supply uncertainty detrimental to manufacturer, can benefit retailer
- Demand uncertainty beneficial to manufacturer, effect on retailer not monotonic

#### Dynamic selling strategy:
- Most outcomes don't change monotonically
- General patterns similar to advance or regular selling

## 6.2 Supply Chain Performance and Consumer Welfare

![[Pasted image 20241114124424.png|500]]

1. Decentralized vs. Centralized Supply Chain:
	- $\Pi_{SC}=\max_q (1+\epsilon-q)q$
	- Centralized supply chain always performs better
	- Dynamic selling reduces efficiency loss (11% vs. 30% for advance, 18% for regular)
	- Efficiency loss increases with capacity $k$, not sensitive to $e$ or $r$

2. Consumer Welfare (area under demand curve):
	- $CS=\int_0^q (q+\epsilon-\hat{q})d\hat{q}=(1+\epsilon)q-q^2/2$
	- Dynamic selling performs best, advance selling worst
	- Changes with $k$, $r$, and $e$ similar to supply chain profits

3. Overall Performance Ranking:
	1. Dynamic selling
	2. Regular selling
	3. Advance selling