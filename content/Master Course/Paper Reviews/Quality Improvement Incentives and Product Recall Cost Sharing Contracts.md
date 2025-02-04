Gary H. Chao, Seyed M. R. Iravani, R. Canan Savaskan

![[Grewal Riedl Serafeim (2019) MS.png]]
# 1. Introduction

__Samsung Galaxy Note 7 recall__
![[Pasted Image 20250121110557_840.png]]
- Sep 16: Samsung announced full recall of Galaxy Note 7
- 2.5 million devices were recalled globally
- Replacement devices were provided
- Primary issues: design defects and manufacturing flaws in the batteries

__Cost of recall__
![[Pasted image 20250121123817.png]]
If the supplier and manufacturer were separate companies:
- Whose fault is it?
- Optimal recall cost sharing contract using this information?
- What if supplier hides its quality information?

# 3. Model
![[Pasted image 20250121123701.png]]

# 4. Complete Information

## 4.1. Benchmark: Centralized Supply Chain

$$\begin{align*}
\max_{\eta_s,\eta_m}\quad \overbrace{r}^{\mathclap{\text{product selling price}}}-\underbrace{(u_m+u_s)}_{\mathclap{\text{unit production costs}}}-\omega
\underbrace{\Big[ 1-e^{-[\lambda^0_m(1-\eta_m)+\lambda_s^0(1-\eta_s)]} \Big]}_{\text{Probability of recall}}-\underbrace{(C_m(\eta_m)+C_s(\eta_s))}_{\text{effort costs}}
\end{align*}$$

- Complementary effort: $\frac{\partial^2 \Pi^C}{\partial \eta_m\partial\eta_s}=\omega\lambda_m^0\lambda_s^0 e^{-[\lambda^0_m(1-\eta_m)+\lambda_s^0(1-\eta_s)]}$
- First best effort: $(\eta_s^{*C},\eta_m^{*C})$
- First best quality: $\lambda_s^0(1-\eta_m^{*C})+\lambda_m^0(1-\eta_m^{*C})$
- First best profit: $\Pi^C(\eta_s^{*C},\eta_m^{*C})$

## 4.2. No Cost Sharing (N)

__Manufacturer internalizes total recall costs__
$$\begin{align*}
\max_{\eta_m}\Pi_m^N=\max_{\eta_m} \overbrace{r}^{\mathclap{\text{product selling price}}}-(u_m+\underbrace{p_0}_{\mathclap{\text{procurement cost}}})-\omega
\underbrace{\Big[ 1-e^{-[\lambda^0_m(1-\eta_m)+\lambda_s^0(1-\eta_s)]} \Big]}_{\text{Probability of recall}}-\underbrace{C_m(\eta_m)}_{\text{effort cost}}
\end{align*}$$
$$\begin{align*}
\max_{\eta_s}\Pi_s^N=\max_{\eta_s} p_0-u_s-C_s(\eta_s)
\end{align*}$$

- Complementary effort: $\frac{\partial^2 \Pi^N_m}{\partial \eta_m\partial\eta_s}=\omega\lambda_m^0\lambda_s^0 e^{-[\lambda^0_m(1-\eta_m)+\lambda_s^0(1-\eta_s)]}$
- Supplier exerts zero effort
- Result: $\eta_m^{*N}<\eta_m^{*C}$

## 4.3. Selective Root Cause Analysis Contract (S)

__Recall cost__
- $T\leq\bar{T}$: Responsible party incurs total recall cost 
- $T>\bar{T}$: Supplier : Manufacturer = R : 1-R


$$\begin{align*}
\max_{\eta_m}\Pi_m^S=\max_{\eta_m} r-(u_m+\overbrace{p}^{\mathclap{p\geq p_0: \text{ Incentive}}})-(\omega+c_r)G
\underbrace{\Big[ 1-e^{-\Lambda_T\bar{T}} \Big]}_{\mathclap{\text{First product failure before }\bar{T}}}-\omega(1-R)
\underbrace{\Big[ e^{-\Lambda_T\bar{T}}-e^{-\Lambda_T } \Big]}_{\mathclap{\text{First product failure after }\bar{T}}}-C_m(\eta_m)
\end{align*}$$
$$\begin{align*}
\max_{\eta_s}\Pi_s^S=\max_{\eta_s} p-u_s-\underbrace{(\omega+c_r)}_{\mathclap{\text{Total recall cost if investigate}}}(1-G)
\Big[ 1-e^{-\Lambda_T\bar{T}} \Big]-\omega R
\Big[ e^{-\Lambda_T\bar{T}}-e^{-\Lambda_T } \Big]-C_s(\eta_s)
\end{align*}$$
- $\Lambda_T=\lambda_m^0(1-\eta_m)+\lambda_s^0(1-\eta_s)$
- $G=\lambda_m^0(1-\eta_m)/[\lambda_m^0(1-\eta_m)+\lambda_s^0(1-\eta_s)]$

__Result__:
- There always exist $R,\bar{T}$ such that $(\eta_s^{*S},\eta_m^{*S})=(\eta_s^{*C},\eta_m^{*C})$

__Impact of analysis cost $(c_r)$__:
- If $c_r=0$, contract that results in $(\eta_s^{*C},\eta_m^{*C})$ maximizes profit

## 4.4. Partial Cost Allocation Contract (P)

__Recall cost__
- Manufacturer's fault
	- Supplier : Manufacturer = $R_m:1-R_m$
- Supplier's fault
	- Supplier : Manufacturer = $R_s:1-R_s$

$$\begin{align*}
\max_{\eta_m}\Pi_m^P=\max_{\eta_m} r-(u_m+p)-(\omega+c_r)\big(G(1-R_m)+(1-G)(1-R_s)\big)
( 1-e^{-\Lambda_T} )-C_m(\eta_m)
\end{align*}$$
$$\max_{\eta_s}\Pi_s^P=\max_{\eta_s} p-u_s-(\omega+c_r)\big(GR_m+(1-G)R_s\big)
( 1-e^{-\Lambda_T} )-C_s(\eta_s)$$


__Result__:
- There always exist $R_m,R_s$ such that $(\eta_s^{*P},\eta_m^{*P})=(\eta_s^{*C},\eta_m^{*C})$

__Comparison S vs. P when $c_r>0$__
- Contract S results in higher total supply chain profits than contract P
	- S: Investigates only if first product failure is before $\bar{T}$
	- P: Always investigates

# 5. Efficiency of Contracts

$$\text{Cost inefficiency}=\frac{\text{Contract X's supply chain cost - Coordinated supply chain cost}}{\text{Coordinated supply chain cost}}\times100\%$$
- Supply chain cost = $\Pi_s+\Pi_m$

$$\text{Quality inefficiency}=\frac{\text{Contract X's failure rate - Coordinated failure rate}}{\text{Coordinated failure rate}}\times100\%$$
- Failure rate = $\Lambda_T=\lambda_m^0(1-\eta_m)+\lambda_s^0(1-\eta_s)$

![[Pasted image 20250121165418.png|500]]
1. Contract F is always inferior to contract S (both cost & quality)
2. Contract P leads to overinvestment, resulting in higher costs and improved quality.

# 6. Asymmetric Information About Supplier’s Component Quality

__Supplier Type__
- High failure type: failure rate $\lambda_{s_H}^0$
	- Probability $\alpha$
- Low failure type: failure rate $\lambda_{s_L}^0$
	- Probability $1-\alpha$

__Assumption__
- Only two types of quality improvements efforts exist
	- $\eta_{s_j}^H$: high effort
	- $\eta_{s_j}^L$: low effort

__Selective menu for each supplier type__
- $S_L=(p_L,R_L,\bar{T}_L)$ for low failure type supplier
- $S_H=(p_H,R_H,\bar{T}_H)$ for high failure type supplier
	- $R_H<R_L,\bar{T}_H<\bar{T}_L$: Costly for high failure rate supplier to misrepresent type

Even when manufacturer does not have complete information, he can design menu of contract S that fits both supplier types to induce supplier effort


# 7. Numerical Study for the Information Asymmetry Case

![[Pasted image 20250121193144.png|500]]

- __Conservative case__: Contract based on higher supplier failure rate
	- Only using $\lambda_{s1}^0$ 
- __Perfect information case__: Manufacturer knows if supplier is using $\lambda_{s1}^0$ or $\lambda_{s2}^0$
- __Menu of contracts__: Manufacturer weighted average $\lambda_{s1}^0:\lambda_{s2}^0=\alpha:1-\alpha$

|                           | Perfect $\rightarrow$ Conservative | Menu $\rightarrow$ Conservative | Perfect $\rightarrow$ Menu |
|:-------------------------:|:----------------------------------:|:-------------------------------:|:--------------------------:|
|     __Cost Increase__     |     Avg: 10.14%<br>Max: 46.28%     |    Avg: 9.35%<br>Max: 46.3%     |         Avg: 0.79%         |
| __Failure Rate Increase__ | Avg:1.1%<br>Min: -12%, Max: 89.06% |   Avg: 13.79%<br>Max: 102.98%   |        Avg: -12.69%        |

- Failure rate may decrease when: Perfect $\rightarrow$ Conservative & Perfect $\rightarrow$ Menu
	- Quality may be better when using menu or conservative case than perfect information case
	- Manufacturer is forced to induce inefficient efforts
- Menu of contracts effective in
	- Reducing costs
	- Improving quailty


# Conclusion


|         | Complete Information                               | Information Asymmetry |
| :-----: | -------------------------------------------------- | --------------------- |
| $c_r=0$ | Contract S, P achieves<br>optimum quality & profit |                       |
| $c_r>0$ | Contract S > Contract P                            |                       |


# Calculation

Let 
$$\begin{align*}
\Pi_s^S&=p-u_s-(\omega+c_r)(1-G)\Big[ 1-e^{-\Lambda_T\bar{T}} \Big]-\omega R\Big[ e^{-\Lambda_T\bar{T}}-e^{-\Lambda_T } \Big]-C_s(\eta_s)\\&= p-u_s-Z(\lambda_{S_j}^0,R,\bar{T},\eta_{s_j}^b)-C_s(\eta_{s_j}^b)
\end{align*}$$
- $Z(\lambda_{S_j}^0,R,\bar{T},\eta_{s_j}^b)=(\omega+c_r)(1-G)\Big[ 1-e^{-\Lambda_T\bar{T}} \Big]+\omega R\Big[ e^{-\Lambda_T\bar{T}}-e^{-\Lambda_T } \Big]$


We need
- $\Pi_s^S(\lambda_{s_H}^0,S_H)>\Pi_s^S(\lambda_{s_H}^0,S_L)$
- $\Pi_s^S(\lambda_{s_L}^0,S_L)>\Pi_s^S(\lambda_{s_L}^0,S_H) \iff -\Pi_s^S(\lambda_{s_L}^0,S_H)>-\Pi_s^S(\lambda_{s_L}^0,S_L)$

Sum above:
- $\Pi_s^S(\lambda_{s_H}^0,S_H)-\Pi_s^S(\lambda_{s_L}^0,S_H)>\Pi_s^S(\lambda_{s_H}^0,S_L)-\Pi_s^S(\lambda_{s_L}^0,S_L)$
- $\iff$ $Z(\lambda_{S_H}^0,R_H,\bar{T}_H,\eta_{s_j}^b)-Z(\lambda_{S_L}^0,R_H,\bar{T}_H,\eta_{s_j}^b)<Z(\lambda_{S_H}^0,R_L,\bar{T}_L,\eta_{s_j}^b)-Z(\lambda_{S_L}^0,R_L,\bar{T}_L,\eta_{s_j}^b)$ with $R_H<R_L,\bar{T}_H<\bar{T}_L$
- $\iff$ $Z(\lambda_{S_H}^0,R,\bar{T},\eta_{s_j}^b)-Z(\lambda_{S_L}^0,R,\bar{T},\eta_{s_j}^b)$ increasing in $R,\bar{T}$ 
- $\iff$ $\frac{\partial^2 Z}{\partial \lambda \partial R}>0, \frac{\partial^2 Z}{\partial \lambda \partial \bar{T}}>0$ - This is satisfied from Lemma 2

But
- 10 > 1
- 4 < 6
	- 10 - 6 = 4 > 1-4 = -3