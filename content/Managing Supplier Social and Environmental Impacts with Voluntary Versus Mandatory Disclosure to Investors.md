# Introduction
- Supplier의 impact를 감소시키는 방법을 배우는 것은 Discounted profit을 늘릴 수 있다 iff initial learning cost가 크지 않다면
- 이 논문은 매니저가 자발적으로 투자자들에게 supplier의 impact를 알린다는 전재하에 learning과 reduction of supplier's impact를 통해 Discounted profit을 최대화 할 수 있는 방법을 찾을 것이다.
	- 무조건 알고 있는 사실은 발표해야 하지만 찾을 노력을 하지 않아서 모른다고 할 수 있다
- Investor들에게 공개하는거지 consumer들에게 공개하는게 아니다 - 많이 다르다
	- Bad news가 공개되면 consumer들은 투명하다고 좋아할 수 있다, investor들은 그렇지 않다
- 
- Does the manager get a brief intuition of the supplier's riskiness?

# Model Formulation
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

__Assumptions__
- Investors cannot observe the manager’s decisions about learning and impact reduction and do not update their beliefs about those decisions upon observing the current period profit
	- Maintains a stable equilibrium where investors' beliefs are based on prior distributions, preventing disruptions from real-time observations
- Support of the impact reduction function $R$ is a finite set
	- Mathematical simplicity & Prevent unbounded impact reductions
- $C$ is independent of $(G,R)$
- $κ∗(R) + τ(G− R(κ∗(R)))> τE[G]$
	- Manager might learn that the discounted cost associated with the supplier’s impact (even with optimal impact reduction) is higher than expected without learning
	- Without this assumption manager would always choose to disclose the supplier’s impact after learning, so a disclosure mandate would have no effect

# Results
## Voluntary Disclosure