# Introduction
- Supplier의 impact를 감소시키는 방법을 배우는 것은 Discounted profit을 늘릴 수 있다 iff initial learning cost가 크지 않다면
- 이 논문은 매니저가 자발적으로 투자자들에게 supplier의 impact를 알린다는 전재하에 learning과 reduction of supplier's impact를 통해 Discounted profit을 최대화 할 수 있는 방법을 찾을 것이다.
	- 무조건 알고 있는 사실은 발표해야 하지만 찾을 노력을 하지 않아서 모른다고 할 수 있다
- Investor들에게 공개하는거지 consumer들에게 공개하는게 아니다 - 많이 다르다
	- Bad news가 공개되면 consumer들은 투명하다고 좋아할 수 있다, investor들은 그렇지 않다
- 
- Does the manager get a brief intuition of the supplier's riskiness?

# Model Formulation

![[Pasted image 20250203200319.png]]
- G: supplier's impact(Investor & manager are uncertain)
- C: cost to learn about supplier's impact
- R: reduction potential of supplier's impact
- Investor & Manager has common information about joint pdf for R.V. (C,G,R)
	- C,G: real-valued R.V.
	- R: function-valued R.V.
- Learn about the supplier's impact & spend $k \in [0,\infty)$  then reduce supplier impact by $R(k)$ 
	- $R(k)$ is nonnegative, increasing, right continuous function of k
- supplier's impact reduced to $g-r(k)$, firm's current period profit reduced by $c+k$
- $\tau$: Discounted expected cost per unit impact by supplier
- $\hat{l}(C),\hat{k}(G,R),\hat{d}(C,G,R)$: Indicator function of investigator's belief
- $M_\emptyset = E[(1-\hat{l}(C))G+\hat{l}(C)(G-R(\hat{k}(G,R)))|\hat{d}(C,G,R)=\emptyset]$
- Firm valuation - non-mandatory disclosure
	- $$V-\begin{cases}
  \tau M_\emptyset & \text{if the manager does not learn} \\
  C+k+\tau M_\emptyset & \text{if the manager learns, incurs impact-reduction cost k and does not inclose} \\
  C+k+\tau(G-R(k)) & \text{if the manager learns, incurs impact-reduction cost k and discloses the impact}
  \end{cases}
  $$
	- Manager problem: $min(\tau M_\emptyset,C+E[min_{i \in \{1,\emptyset\}}\{k+\tau M_i\}])$
- Firm valuation - mandatory disclosure
	- $$V-\begin{cases}
  \tau E[G] & \text{if the manager does not learn} \\
  C+k+\tau(G-R(k)) & \text{if the manager learns, incurs impact-reduction cost k}
  \end{cases}
  $$
	- Manager problem: $min(\tau E[G],C+E[min_{k \in [0,\infty)]}\{k+\tau R(k)\}])$
		- Solution: $(l^*,k^*,d^*)$
- $\kappa^*(R)$: optimal $k$ conditional on $R=r$
	- $κ^∗ ( R) ∈ argmin_{k \in [0,\infty)}\{k− τR  ( k)\}$
- EDP: Expected Discounted Profit

__Assumptions__
- Investors cannot observe the manager’s decisions about learning and impact reduction and do not update their beliefs about those decisions upon observing the current period profit
	- Maintains a stable equilibrium where investors' beliefs are based on prior distributions, preventing disruptions from real-time observations
- Support of the impact reduction function $R$ is a finite set
	- Mathematical simplicity & Prevent unbounded impact reductions
- $C$ is independent of $(G,R)$
- $κ^∗(R) + τ(G− R(κ^∗(R)))> τE[G]$
	- Manager might learn that the discounted cost associated with the supplier’s impact (even with optimal impact reduction) is higher than expected without learning
	- Without this assumption manager would always choose to disclose the supplier’s impact after learning, so a disclosure mandate would have no effect

# Results
## Voluntary Disclosure

__Lemma 1 (Voluntary Disclosure)__
1. In an equilibrium, the manager learns if and only if $C ≤ \bar{c}_v$. After learning, the manager chooses to reduce the supplier’s impact according to $κ^∗(R$) and disclose it if and only if $G ≤\hat{g} (R, M_∅)$; otherwise, the manager does not disclose and pursues only the immediately profitable impact reduction $R(0)$. Together, $\bar{c}_v,\hat{g}(R, M_∅)$, and $M_∅$ satisfy 
$$\bar{c}_v= τM_∅− E[min(τM_∅, κ^∗(R) + τ(G− R(κ^∗(R))))] $$
$$\hat{g}(R, M_∅) =M_∅ + (τR(κ^∗(R)) − κ^∗(R)  )/(τ)$$
$$M_∅=\frac{F(\bar{c}_v)E[(G− R(0))1\{G >\hat{g}(R, M∅)\}] + (1− F(\bar{c}_v))E[G]}{F(\bar{c}_v)Pr(G >\bar{g}(R, M_∅)) + (1− F(\bar{c}_v))}$$
2. An equilibrium exists.
3. In any equilibrium, investors’ expectation of the impact in the event of nondisclosure $M_∅$ is strictly greater than the expected impact without learning $E[G]$, that is, $M_∅ > E[G]$.
4. If the equilibrium is unique, decreasing the learning cost $C$ (in first order stochastic dominance) strictly increases the learning cost threshold $\bar{c}_v$.
	- (a): $C\leq\bar{c}_v$ iff 관리자가 학습함
	- (c): 비공개를 관찰한 투자자들은 공급업체의 영향을 더 높게 추정
		- 비공개를 관찰한 투자자들은 관리자가 학습하지 않았거나, 학습했지만 공급업체의 영향이 높다는 나쁜 소식을 숨기고 있다고 생각하게 되기 때문이다.
	- (d): 비공개 $\rightarrow$ 투자자들의 학습 비용에 대한 사전 분포가 낮을수록, 투자자들은 관리자가 학습했지만 나쁜 소식을 숨기고 있을 확률이 더 높다고 생각하게 됨 $\rightarrow$ 공급업체의 영향에 대한 기대치($M_∅$)가 더 높아지게 됨 $\rightarrow$ 관리자는 좋은 소식을 공개하기 위해 더 높은 수준의 학습 비용을 감수하려는 동기를 갖게 된다.

## Voluntary Disclosure vs Mandatory Disclosure

__Proposition 1__
1. A mandate for disclosure strictly reduces the probability that the manager learns: $$\bar{c}_m < \bar{c}_v$$with $\bar{c}_v$ representing the learning cost threshold in any equilibrium under voluntary disclosure. However, if $C ≤ \bar{c}_m$, so that the manager nevertheless learns, the mandate for disclosure results in weakly greater impact reduction.
	- Mandatory Disclosure, Nondisclosure $\rightarrow$ Investors know that manager did not learn
	- $\bar{c}_m$ is invariant with $C$

__Proposition 2__
1. A disclosure mandate results in strictly higher impact in expectation if
   $$E[R(0)] > 0 \space and \space w.p.\space 1 \space k^∗(G, R)= 0$$
	- Reduced probability to learn $\rightarrow$ increased expected impact by supplier

일반적인 조건 하에서 Mandatory Disclosure가 구매 회사의 관리자가 공급업체의 사회적 또는 환경적 부정적 영향을 파악하고 이를 줄이는 것을 막음으로써 사회나 환경에 해를 끼칠 수 있다. 

__Proposition 3__
1. A disclosure mandate strictly increases the buying firm’s valuation and discounted profit, in expectation.
	- Disclosure mandate는 매니저가 학습하고 영향력을 줄이는 것을 유도하기 때문에 EDP가 증가한다 -> Expected valuation 도 증가한다
	- Nondisclosure일 때 Investor들이 supplier impact 예상치가 더 작다

__Proposition 4__
1. A disclosure mandate can strictly reduce the supplier’s impact only if $τ > \underline{τ}$.
2. With voluntary disclosure, the manager withholds information from investors with nonzero probability if and only if (8) holds, which is equivalent to $τ < \bar{τ}$.
3. Under a disclosure mandate, as $τ$ increases, the learning cost threshold $c_m$ strictly increases and the supplier’s impact decreases.
	- $\tau \leq \underline{\tau}$
		- 매니저가 영향력 감소에 돈을 안씀
		- Buyer가 supplier impact로 바로 손실을 안 볼 경우 $\tau$가 작다.
	- $\tau \geq \bar{\tau}$
		- 매니저가 항상 공개 -> Disclosure Mandate가 쓸모 없음
	- o/w
		- Disclosure Mandate: Strictly reduce supplier's impact, $\tau \uparrow \space\rightarrow$  supplier impact $\downarrow$ 
		- Voluntary Mandate: Not all the case

# Extensions

## Shared Supplier
We have second buyer firm(B2) with $\tau_2 \in (0,\tau)$

All propositions 1-4  hold for both buying firms.

__Proposition 5__
1. With voluntary disclosure (and not under a disclosure mandate), cooperation can strictly reduce the learning cost threshold and result in higher impact.
2. With voluntary disclosure (and not under a disclosure mandate), cooperation can strictly reduce the expected values of both buying firms’ valuations and discounted profits.
3. The supplier’s expected impact can be strictly higher with a disclosure mandate and cooperation than with voluntary disclosure and noncooperation.
	- Cooperation overcomes B2 freeride problem
	- From (1)
		- Disclosure Mandate -> increase learning cost threshold, reduce supplier impact
		- Voluntary disclosure -> cooperation이 학습, 영향력 감소 막을 수 있음
		- cooperation이 $\tau \rightarrow \tau+\tau_2$ 처럼 작동하기 때문이다.
	- From (2)
		- Voluntary disclosure: harm both buying firm & supplier
			- cooperation -> increase likelihood of learning -> nondisclosure: investors think supplier has larger impact than usual -> overinvest on learning
		- Disclosure mandate: buying firms & managers benefit
	- From (3)
		- In some cases disclosure mandate reduces the probability of learning

## Alternative Supplier

Learning cost is $\gamma C$

__Proposition 6__
1. With voluntary disclosure, the manager commits to a supplier if and only if $γ >\hat{γ}_v$, where $1 <\hat{γ}_v$. Under a disclosure mandate, the manager commits to a supplier if and only if $γ >\hat{γ}_m$, where $1 <\hat{γ}_m<\hat{γ}_v$.
2. For $γ ≤\hat{γ}_m$, a disclosure mandate is ineffective.For $γ ∈ (\hat{γ}_m,\hat{γ}_v]$, a disclosure mandate strictly increases the probability that the manager learns. For $γ >\hat{γ}_v$, Propositions 1, 2, 3, and 4 hold.
	- Commitment는 $\gamma$가 클 때 일어난다
	- Disclosure mandate는 $\gamma$-threshold를 낮춰 commitment를 더 자주하게 된다$(\hat{\gamma}_m<\hat{\gamma}_v)$
		- Prop3: disclosure mandate는 commit할 때 buyer, supplier 모두 이득을 본다
	- 매니저가 alternative로 바꿀 옵션이 있다 -> voluntary도 optimal impact reduction을 찾은뒤 영향력 감소 시키고 무조건 공개한다 -> mandate는 쓸모 없는 옵션이다

## Manager's Objective/Information for Investors

$\theta$: weight assigned to EDP -> valuation has $1-\theta$

__Proposition 7__ 
1. A disclosure mandate has the same effect on learning, impact reduction, the firm’s expected discounted profit, and its valuation as increasing $θ$ to 1.
	- Disclosure mandate has effect of
		- Manager to maximize EDP
		- Eliminate investors' uncertainty about supplier's impact

__Proposition 8__
1. With voluntary disclosure, if the equilibrium is unique, the learning cost threshold $\bar{c}_v$ strictly decreases with $θ$.
	- Voluntary disclosure
		- $\theta$ increases(investors more likely to learn supplier impact) -> manager less likely to learn

# Concluding Remarks

Disclosure mandate or shifting a manager’s priority to long-term profits over short-term valuation has a significant impact on how firms address supplier issues. It outlines three main mechanisms:

1. Avoidance of Learning: Firms may avoid investigating supplier impacts if the costs exceeds the potential future profit benefits, fearing a negative impact on their valuation.
2. Motivated Impact Reduction: When firms do investigate supplier impacts, they are more likely to take corrective actions rather than hide information, benefiting both the firm and stakeholders.
3. Increased Investor Confidence: Transparency from disclosure reassures investors, enhancing the firm’s valuation.

Overall, the mandate may initially discourage learning but ultimately promotes
impact reduction, improving both expected profits and market value.