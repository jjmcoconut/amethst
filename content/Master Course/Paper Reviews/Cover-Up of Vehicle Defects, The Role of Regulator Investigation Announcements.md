Soo-Haeng Cho, Victor DeMiguel, Woonam Hwang

# 1. Introduction

**Toyota Recall (2009-2010)**
- 8+ million vehicles recalled
- Sudden unintended acceleration defect
- 89 deaths, 57 injuries
- Criticized for cover-up attempt
- Knew of problem in 2007, didn't report to NHTSA
- Paid $1.2 billion to settle criminal charge

**GM Recall (2014)**
- 2.6 million vehicles recalled
- Faulty ignition switch
- 124 deaths, 275 injuries
- Aware of defect since 2004
- Paid $900 million to settle criminal charge

__Regulatory Issues__
- Manufacturers have more knowledge and resources than regulators
- Regulators often rely on manufacturers for information
- NHTSA: 57 employees handling 35,000 complaints/year

__US vs UK Regulatory Approaches__
- **United States (NHTSA)**
	- Manufacturers submit Early Warning Reporting (EWR) data
	- NHTSA announces ongoing investigations publicly
- **United Kingdom (DVSA)**
	- Collects information from manufacturers
	- Does not announce potential issues unless formal investigation concludes defect exists
	- Aims to encourage manufacturer cooperation

## Research Questions

1. How does the regulator's announcement policy affect manufacturers' propensity to cover up defects?
2. How does the announcement policy impact regulator's willingness to investigate and overall social welfare?

# 3. Model

__Model Overview__
- Product: Finite life cycle, price $p$, zero production cost
- Expected harm: $h ∈ (0,\bar{h}]$
- Prior probability of defect: $P(D)$
- Consumer demand rate: $d(p) = 1 - p/\bar{v}$
- Investigation cost: $C > 0$
- Investigation lead time: Random variable, mean $l ∈ (0,1)$

__Sequence of Events__
![[Pasted image 20250107102905.png|400]]
1. Nature chooses true state: Defective ($D$) or Nondefective ($N$)
2. Manufacturer receives private signal $s ∈ \{\tilde{D}, \tilde{N}\}$
3. Manufacturer decides to report ($R$) or not report ($NR$)
4. If reported, regulator decides to investigate immediatedly ($I$) or not ($NI$)
5. Voluntary Investigation
	- Triggered by consumer complaints if true state is D
	- Timing: $\hat{t} \sim \text{Uniform}[0, 1-l]$
	- Probability of no investigation: $P(\hat{t} = 1|D) = 1 - h/\bar{h}$

__Recall and Penalties__
- Recall cost: $r ∈ (0,p)$ per unit
- Manufacturer liable for consumer harm until recall
- Cover-up penalty: $K_1h + K_2$ (if discovered)
- Probability regulator finding out manufacturer’s cover-up: $\theta$

__Consumer Behavior__
- US: Demand decreases during investigation
- UK: Demand unaffected by investigation

__Manufacturer's Private Signal__
- Reliability: $\rho =\frac{T - Tmin}{Tmax - Tmin} ∈ [0,1]$
	- $T=P(D\wedge \tilde{D})+P(N\wedge \tilde{N})$
	- $T_{max}=1$
	- $T_{min}=P(D)^2+P(N)^2$
	- Assumption (unbiased): $P(\tilde{D})=P(D), P(\tilde{N})=P(N)$
- Posterior probabilities:
	* $P(D|\tilde{D}) = \rho + (1-\rho)P(D)$
	* $P(N|\tilde{D}) = (1-\rho)P(N)$

## 3.1. Manufacturer's Expected Profit

__Report and immediate investigation (R,I)__
- $$\pi_{(R,I)}^{US}=\underbrace{p[ld(p,h)+(1-l)d(p)]}_{\text{Manufacturer's sale revenue}}-P(D|\tilde{D})\underbrace{(r+h)}_{\mathclap{\text{Compensation cost}}}\overbrace{ld(p,h)}^{\mathclap{\text{\# of defect vehicle}}}$$
- $$\pi_{(R,I)}^{UK}=\underbrace{pd(p)}_{\mathclap{\text{Manufacturer's sale revenue}}}-P(D|\tilde{D})\overbrace{(r+h)}^{\mathclap{\text{Compensation cost}}}\underbrace{ld(p,h)}_{\mathclap{\text{\# of defect vehicle}}}$$

__Report and no immediate investigation (R,NI)__
- $$\begin{align}
\pi_{(R,NI)}^{US} = pd(p) - P(D|\tilde{D}&) \Bigg[ 
     \underbrace{\int_0^{1-l} l \big(d(p) - d(p,h)\big) g(\hat{t}|D) d\hat{t}}_{\text{Demand decrease (voluntarily investigation)}} \\
    & + \underbrace{\int_0^{1-l} (r+h) \big(d(p)\hat{t} + d(p,h)l\big) g(\hat{t}|D) d\hat{t}}_{\text{Recall, liablility cost (voluntarily investigation)}} \\
    & + \underbrace{\alpha h d(p) P(\hat{t}=1|D) }_{\text{Liability cost (no investigation)}}
\Bigg]
\end{align}$$
- $$\begin{align}
\pi_{(R,NI)}^{UK} = pd(p) - P(D|\tilde{D}&) \Bigg[ 
     \underbrace{\int_0^{1-l} (r+h) \big(\hat{t} + l\big)d(p) g(\hat{t}|D) d\hat{t}}_{\text{Recall, liablility cost (voluntarily investigation)}} \\
    & + \underbrace{\alpha h d(p) P(\hat{t}=1|D) }_{\text{Liability cost (no investigation)}}
\Bigg]
\end{align}$$
__No report (NR)__
- $$\pi_{(NR)}^j=\pi_{(R,NI)}^j-P(D|\tilde{D})\overbrace{(K_1h+K_2)}^{\mathclap{\text{cover-up penalty}}}\underbrace{\theta\int_0^{1-l}g(\hat{t}|D)d\hat{t}}_{\mathclap{\text{Conduct investigation \& find cover-up}}}$$

## 3.2. Regulator's Objective Function

__Regulator's Objective Function: Social Welfare__
- $W = \pi + S - \Gamma$
	- $\pi$: Manufacturer's expected profit
	- $S$: Expected consumer surplus
	- $\Gamma$: Regulator's expected cost

__Scenario 1 (R,I)__
- Customer's Surplus
	- $$S_{(R,I)}^{US}=\underbrace{l\int_{p+h}^\bar{v}(v-p-h)f(v)dv}_{\text{During investiagation}}+\underbrace{(1-l)\int_p^\bar{v}(v-p)f(v)dv}_{\text{After investigation}}$$
	- $$S_{(R,I)}^{UK}=\int_p^\bar{v}(v-p)f(v)dv$$
- Regulator's Cost: $\Gamma_{(R,I)}^j= C$

__Scenario 2 (R,NI)__
- __Customer Surplus__
	- $$\begin{align}
S_{(R,NI)}^{US} = \underbrace{P(D|\tilde{D})}_{\text{Defective}}& \Bigg[ 
     \underbrace{\int_0^{1-l}g(\hat{t}|D)d\hat{t}\Bigg((1-l)\int_p^\hat{v}(v-p)f(v)dv+l\int_{p+h}^\hat{v}(v-p-h)f(v)dv\Bigg)}_{\text{Voluntarily investigation (fully compensated)}} \\
    & + \underbrace{P(\hat{t}=1|D)\Bigg(\int_p^\hat{v}(v-p)f(v)dv-(1-\alpha)hd(p)\Bigg)}_{\text{No investigation (partially compensated)}}\Bigg] \\
    & + \underbrace{P(N|\tilde{D})\int_p^\bar{v}(v-p)f(v)dv}_{\text{Not defective}}
\end{align}$$
	- $$S_{(R,NI)}^{UK}=\int_p^\bar{v}(v-p)f(v)dv-\underbrace{P(D|\tilde{D})P(\hat{t}=1|D)(1-\alpha )hd(p)}_{\text{No investigation (partially compensated)}}$$
- __Regulator's Cost__: $\Gamma_{(R,NI)}^j= C\cdot P(D|\tilde{D})\int_0^{1-l}g(\hat{t}|D)d\hat{t}$

__Scenario 3 (NR)__
- Social welfare same as Scenario 2
- Penalty payment cancels out (transfer from manufacturer to regulator)

# 4. The Regulator's Investigation Decision


__Key Concept__
- Regulator investigates if $W_{(R,I)} \geq W_{(R,NI)}$

__Proposition 1: Conditions of Investigating Immediately__
- Regulator investigates immediately $\iff h\geq h_I^j, \rho \geq \rho_I^j(h)$
	- ![[Pasted image 20250107114940.png|300]]

__Corollary 1__
- $r\leq\bar{v}-\frac{3}{2}\bar{h}$ & US regulator investigates immediately $\rightarrow$ UK regulator investigates immediately
	- If US investigates immediately, UK also investigates immediately

**US vs UK:**
- US more reluctant to investigate immediately
- Reason: Public announcement reduces demand in US
- US investigates when $h, r, \rho$ are sufficiently high

**Impact of US Policy:**
- Good intentions: Reduce potential harm and recall cost
- Unintended consequence: More cautious in initiating investigations

# 5. The Manufacturer's Cover-Up Decision

__Proposition 2&3: Conditions of Cover-Up__
   - __US__: $h_I^{US} \leq h < h_R^{US} \wedge \rho \geq \rho_I^{US}(h)$ or $h \geq h_R^{US} \wedge \rho_I^{US}(h) \leq \rho < \rho_R^{US}(h)$
   - __UK__: $h_I^{UK} \leq h < h_R^{UK} \wedge \rho \geq \rho_I^{UK}(h)$
	   - ![[Pasted image 20250107121127.png|300]]

**Insights (Why Cover-Up?):**
- Lower expected harm ($h$): Higher chance of getting away with cover-up
- Lower possibility of defect ($\rho$): Avoid investigation announcement impact

**Key Difference:**
- UK cover-up decision depends only on expected harm ($h$)

__Comparison of US and UK Policies__
1. US policy leads to fewer investigations and more cover-ups of significant harm
2. US policy has unintended consequences:
	- Regulator reluctant to initiate investigations
	- Manufacturer covers up potential defects with significant harm
3. UK policy more effective in inducing manufacturer to report potential defects

# 6. Social Welfare

__Proposition 4&5 (Social Welfare Comparison)__
![[Pasted image 20250107153145.png|400]]
- Social welfare for NR and (R,NI) is identical $\rightarrow$ no immediate investigation
1. Both no immediate investigation:
	- US welfare higher if: $r + \frac{3}{2}h > \bar{v}$
		- UK always has bigger customer surplus 
			- US customer demand decreases (decreases more by harm $h$)
		- Demand drop reduces recall and liability cost
		- Harm, recall cost high & demand drop $\rightarrow$ manufacturer profit drop reduces
		- Harm($h$), recall cost($r$) high $\rightarrow$ US welfare higher
2. Both immediate investigation:
	- US welfare higher if: $\frac{1}{2}h + P(D|\tilde{D})(r + h) > \bar{v}$
		- Case 1 (High $h,r$) + High $P(D|\tilde{D})$
			- Consumer demand drop with certainty
			- Recall cost reduces only when defect actually exist $\rightarrow$ Need high $P(D|\tilde{D})$
3. UK: immediate investigation, US: no immediate investigation (Corollary 1)
	- UK welfare higher if: $\rho > \rho_W^{UK}(h)$
	- Numerical observation: $\rho_W^{UK}(h)\approx \rho_I^{UK}(h)\rightarrow$ UK welfare likely higher in this entire region

__General Findings__
- UK policy generally induces higher social welfare
- US policy better when defects with very serious harm and high recall costs

__Consumer Harm Comparison__
- UK may have slightly higher consumer harm for $h \leq h_R^{UK}$
- UK consumer harm lower when:
	1. UK investigates immediately, US doesn't
	2. Only US manufacturer covers up

# 8. Policy Recommendations and Conclusion

__US Policy__
- **Advantage:**
	- Provides early information to consumers
- **Disadvantage:**
	- Regulator reluctant to investigate
	- Discourages manufacturer from reporting significant defects

__Policy Recommendations__
1. **Announce investigations with more resources**
	- Shorten investigation lead time
	- Reduce impact on demand
	- Encourage manufacturer reporting
2. **Improve communication of defect probability**
	- Help consumers interpret information correctly
	- Reduce manufacturer incentive to cover up
	- Example: Color-coding scheme (red, orange, yellow)
3. **Hybrid policy**
	- Confidential investigation for significant harm
	- Prevent cover-ups of most worrying defects
	- Improve social welfare for high expected harm
4. **Two-phase investigation with silent preliminary phase**
	- Preliminary evaluation: Silent phase
	- Engineering analysis: Announce investigation
	- Encourage manufacturer reporting
