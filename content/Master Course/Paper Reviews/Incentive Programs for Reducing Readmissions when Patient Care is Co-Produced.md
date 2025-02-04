Author: Dimitrios A. Andritsos, Christopher S. Tang


# Introduction

- Hospital readmissions are a major concern globally, contributing to poor care quality and excess costs.
- US: ~1 in 5 Medicare FFS patients rehospitalized within 30 days; ~75% of these readmissions may be avoidable.
- Europe: Readmissions add stress to national health budgets (e.g., 14.2% 30-day readmission rate in a French study).
- Various readmission-reduction efforts (e.g., patient education, discharge planning) can reduce readmissions by 25–50%.
- Hospitals, often reimbursed on an FFS basis, lack financial incentives to reduce readmissions, as they benefit from more admissions.
- Policy makers are exploring alternative reimbursement schemes like:
 - **Pay-for-performance (P4P):** Hospitals rewarded/penalized based on readmission rates (e.g., US HRRP, UK NHS Payment by Results).
 - **Bundled payment (BP):** Single payment for initial admission and potential readmission, transferring financial risk to hospitals.
- Debate: Hospitals argue that patient behavior (often uncontrollable) influences readmission rates.
- Increasing focus on **co-production** of care, where hospitals and patients jointly work on disease management programs (e.g., personalized care, follow-ups).
- Growing interest in patient cost-sharing to manage healthcare demand and reduce moral hazard.

**Study Aim**
- Examines the "joint effect" of hospital and patient incentives on reducing readmissions.
- Models strategic interactions between:
	 1. **Funder** (chooses reimbursement scheme: FFS, P4P, BP).
	 2. **Hospital** (chooses hospital-specific effort to reduce readmissions).
	 3. **Patient** (chooses patient-specific effort to reduce readmissions).

**Key Findings**
1. **FFS** fails to motivate hospital or patient to reduce readmissions.
2. **P4P** is more effective than BP in reducing readmissions, especially when penalties are strict or co-production is weak.
3. **BP** is more cost-effective for the funder, lowering total patient and hospital costs, especially when treatment costs are high.
4. **Patient cost-sharing** can be beneficial for the funder under both P4P and BP.
5. Hospitals are more incentivized to engage patients who are effective in self-managing their care.

# Modeling

## Hospital Readmission under Health Co-Production

**Episode of Care (EOC)**:
- Two phases: 
	1. **Hospitalization phase**: Starts with admission, ends with discharge.
	2. **Post-discharge phase**: Begins after discharge, with or without readmission within a specific time window (e.g., 30 days in the U.S. for Medicare, 28 days in the U.K. for NHS).
  
**Readmission Assumption**:
- Focus on whether a patient is readmitted at least once within the EOC’s window, based on existing studies (e.g., Carey 2015).
- Readmission results from a poor health condition, denoted as $\eta\in[0,1]$ where $\eta=1$ indicates "good" health and $\eta=0$ indicates "bad" health.

**Modeling Co-Production**:
- Joint efforts of hospital and patient
	- Hospital readmission-reduction efforts $x$ (e.g., patient education, follow-ups)
	- Patient self-management efforts $y$ (e.g., medication adherence, lifestyle adjustments).
- Efforts as Complements: Hospital and patient efforts are interdependent; higher effort from one increases the effectiveness of the other (Cobb-Douglas production function).
- Equation for health condition: $\eta = v x^\alpha y^\beta$
	- $\alpha$ and $\beta$ represent elasticity of health condition with respect to hospital and patient efforts.
	- $v$ is a productivity factor representing the effectiveness of the co-production process

**Patient Activation**:
- Defined by a patient's ability to manage their own care (knowledge, confidence, skills).
- Two patient types based on activation levels: 
	1. Low activation $v_1$
	2. High activation $v_2$
- Patient activation is not accounted for in reimbursement schemes but can affect readmission probability.

**Readmission Probability**:
- $m$: A patient's probability of readmission
	- $m =\rho(1-\eta)= \rho (1 - v x^\alpha y^\beta)$
- $\rho$: the baseline readmission probability if no efforts are exerted ($x=0$ or $y=0$).

## Patient's Problem

**Patient effort is independent of the reimbursement scheme** (FFS, P4P, or BP).
- Patient's effort $y$ depends on hospital's effort $x$, not on the reimbursement model.
- The patient chooses effort level $y$ to minimize total expected disutility during an episode of care.

**Effort cost assumptions:**
- Patient’s effort $y$ is costly and increases convexly, modeled as $k_p y^\zeta$, where $\zeta \geq 1$ and $k_p > 0$.

**Patient’s total costs:**
- For each hospital visit (initial admission and possible readmission), the patient incurs:
	- **Inconvenience cost ($t$):** Represents disutility from hospital visits, time away from work, etc.
	- **Monetary cost ($C$):** Represents patient’s cost-sharing (e.g., co-payments).
- Combined cost: $c_p = t + C$ (total patient cost of hospitalization).
- __Expected total cost during an episode of care (EOC)__
	- $\Pi_p = (1 + m) c_p + k_p y^\zeta = (1 + \rho(1-vx^\alpha y^\beta)) c_p + k_p y^\zeta$

__Proposition 1__
$$y^*(x)=min\{ (v\phi_p)^{\frac{1}{\zeta-\beta}}x^{\frac{\alpha}{\zeta-\beta}},1 \}$$
- Higher $c_p$ or lower $k_p$, higher $v$, higher $x$ increases patient incentive to exert more effort.
- __Intuitive explanation__
	- Higher $c_p$ $\rightarrow$ people do not want to go more often $\rightarrow$ need to exert more effort
	- Lower $k_p$ $\rightarrow$ cost on putting effort more efficient $\rightarrow$ can have more effort with same money
	- Higher $v,x$ $\rightarrow$ larger return when increasing effort than usual $\rightarrow$ exert more effort (Backfire?)

## Hospital's Problem

**Hospital's effort decision:**
- Hospital selects effort level $x_i$ for each patient type $i \in \{1, 2\}$ to maximize its total expected operating margin.
- Total number of index admissions (EOCs) is $N$, and $N_i = N f_i$ is the number of type-$i$ patients, where $f_1 + f_2 = 1$.

**Hospital's variables for margin:**
- Overall readmission rate $r = m_1f_1+m_2f_2$
- **Treatment cost $c_h$ per patient visit**: Assumed equal for initial admission and readmission.
- **Readmission-reduction effort cost**: Modeled as $k_h x^\zeta$, with convex increasing costs of effort
	- $\zeta$ same as patient's $\zeta$
- **Penalty costs (under P4P/BP)**: Included in operating margin when applicable.


### Fee for Service (FFS)
- **Reimbursement**: Fixed amount $R$ per patient visit
- **Payment issued by funder**: $M_h^{(F)} = N(1 + r(x_1, x_2))R$
- __Hospital's expected operating margin__
	- $$\Pi_h^{(F)}(x_1,x_2)=N(1+r(x_1,x_2))(R-c_h)-\sum_{i=1}^2N_ik_hx_i^\zeta$$
	- Maximize operating margin by managing efforts ($x_1$ and $x_2$) for patient groups.
- **Key result (Lemma 1)**
	- No incentive for hospitals or patients to reduce readmissions
	- $(x_i^{(F)},y_i^{(F)}) = (0,0)$ for $i\in\{1,2\}$ 
	- $r^{(F)} = \rho$.
- __Intuitive explanation
	- $(x_i^{(F)},y_i^{(F)}) = (0,0)$ for $i\in\{1,2\}$
		1. Hospital's margin increases by $r$
		2. no reason to put effort ($y=0$)
		3. $r=\rho$  no matter what
		4. patient wants to minimize its expected total cost 
		5. patient puts no effort because effort is a cost ($x=0$)

### Pay for Performance (P4P)
- **Penalties**: Imposed if the readmission rate $r(x_1, x_2)$ exceeds a threshold $\tau$ set by the funder.
	- Penalty function: $R\times \frac{N(r - \tau)^+} {u}$
	- $u$: Penalty strength (Smaller u, larger penalty)
- **Hospital behavior**: 
	- $r < \tau$: hospital receives full reimbursement, equivalent to FFS.
		- $r=\tau$ dominates $r < \tau$ $\rightarrow$ No need to this about this case
	- $r \geq \tau$: hospital faces penalties and aims to minimize readmissions.
- __Hospital's expected operation margin__
	- $$\Pi_h^{(P)}(x_1,x_2)=N(1+r(x_1,x_2))(R-c_h)-\sum_{i=1}^2N_ik_hx_i^\zeta-\frac{NR(r(x_1,x_2)-\tau)}{u}$$
- **Proposition 2**:
	- If reimbursement $R$ is large enough, hospital exerts effort to achieve $r^{(P)} = \tau$.
	- If $R$ is smaller, readmission rate $r^{(P)} > \tau$ but decreases as $R$ increases.
	- Hospital exerts more effort with high-activation (type-2) patients than low-activation (type-1), leading to “cherry-picking” high-effort patients.
- __Intuitive explanation__
	- $R$ large $\rightarrow$ cost of penalty > cost of effort improvement $\rightarrow$ tries to match $r=\tau$
		- Cost of penalty is proportional to $R$
	- $R$ small $\rightarrow$ cost of penalty < cost of effort improvement (in the start) $\rightarrow$ increase $r$ until cost of penalty and effort improvement becomes same
	- Can differ cost of improvement for type 1/2 & type 2 is more efficient $\rightarrow$ more effort on type 2
		- $c_{High}\times x_{High} +c_{Low}\times x_{Low}$ w.r.t. $x_1+x_2=constant$ makes the maximum

### Bundled Payment (BP)
- **Reimbursement**: Single payment $R$ covers entire episode of care (EOC).
- **Hospital behavior**: 
	- The magnitude of $R$ does not affect hospital's effort to reduce readmissions.
	- Hospital exerts more effort for type-2 patients than type-1, as in P4P.
- __Hospital's expected operating margin__
	- $$\Pi_h^{(B)}(x_1,x_2)=N(R-c_h(1+r(x_1,x_2)))-\sum_{i=1}^2N_ik_hx_i^\zeta$$
## Funder's Problem

**Funder's objective** ($\Pi_f$): Minimize (total patient costs + total funder payments to the hospital)
- Two versions:
	1. **Full Coverage**: Patient is fully insured. Funder determines optimal reimbursement $R$.
	2. **Partial Coverage**: Patient shares costs. Funder optimizes both reimbursement $R$ and co-payment $C$.

### 5.1 Fee-for-Service (FFS)
- No effort exerted by hospital or patient ($x_i = y_i = 0$).
- Readmission rate $r^{(F)} = \rho$ 
- Objective: $\Pi_f = N(1 + \rho)(t + c_h)$.
- __Intuitive explanation:__
	- $R^{(F)} = c_h$
		- Marginal profit of hospital must be nonnegative
	- $C=0,C>0$ does not effect in this case
		- $\Pi_f$ is the sum of total patient's cost + total funder payments. If C>0 it just simply adds $N\rho C$ to patients and subtracts $N\rho C$ to funder payments.

### 5.2 Pay-for-Performance (P4P)
#### Full Coverage (Co-payment $C = 0$)
- $r \geq \tau$ default
- Funder’s problem: Minimize $\Pi_f(r)$ while ensuring hospital participation and $\tau \leq r \leq q$
	- $$\Pi_f^{(P)}(r)=NR(r)(1+r)-\frac{NR(r)(r-\tau)}{u}+tN(1+r)+\frac{N\beta t(\rho-r)}{\zeta }$$
- When $\hat{v}$ is large it is optimal to take $R^{(P)}$ large enough to induce $r^{(P)}=\tau$
- If $\hat{v}$ is small then take r such that $\Pi_h^{(p)}(r)=0$ which induces $r^{(P)}>\tau$

#### Partial Coverage (Co-payment $C > 0$)
- Funder’s outflow becomes $(R - C)$.
- $$\Pi_f^{(P)}(R,C)=NR(1+r(R,C))-\frac{NR(r(R,C)-\tau)}{u}+tN(1+r(R,C))+\frac{N\beta t(\rho-r(R,C))}{\zeta }$$
- __Intuitive explanation:__
	- Problem reduced to a single-variable optimization if $c_h > t$
		- Amount of money getting from funder is increased because the cost of treating the patient is large.
	- Optimal to impose co-payment(exert patient effort, lower $R$)
		1. C>0 
		2. increase in $c_p$ 
		3. patient effort increase 
		4. cost of increasing effort becomes smaller 
		5. Able to reduce penalty (match equilibrium between penalty cost, cost of increasing effort) 
		6. reducing penalty means decreasing $R$ or increasing $u$

### 5.3. Bundled Payment (BP)

#### 5.3.1. Full Coverage ($C = 0$):
- **Funder’s payment**: $M_h^{(B)} = NR$.
- **Patient cost**: $c_p = t$
- $$\Pi_f^{(B)} = N(R+(1+\rho)t)-\frac{N\phi\rho t(\zeta-\beta)}{\zeta}$$

#### 5.3.2. Partial Coverage ($C > 0$):
- **Funder’s payment**: $M_h^{(B)} = NR - N(1 + r)C$.
- **Patient cost**: $c_p = t + C$
- $$\Pi_f^{(B)} = N(R+(1+\rho)t)-\frac{N\phi(C)\rho ((\zeta-\beta)t-\beta C)}{\zeta}$$
  
**Proposition 7**
- Co-payment is optimal
	1. C>0 
	2. $c_p$ is increases 
	3. patient effort increases
	4. hospital exert more effort(different from P4P because payment from funder is fixed so it needs to reduce $r$) 
	5. $r$ decreases
	6. R decreases($\because$ decrease in $r$ make lower $R$ available to satisfy $\Pi_h\geq0$)
	- Increase in $\hat{v}$ makes the same result


# Result
## 5.4. Choosing the Optimal Reimbursement Scheme

**Comparison Criteria**:
1. Readmission rates.
2. Funder’s objective.

### 5.4.1. Full Coverage: Patient Co-Payment ($C = 0$)
**Proposition 8 (Readmission rates)**:
1. Always true that $\Pi^{(P)} \leq \Pi^{(F)}$ and $\Pi^{(B)} \leq \Pi^{(F)}$.
2. Two cases:
	 - (a) If $\tau \leq \rho(1 - \phi(\hat{v} = 1))$, then $r^{(P)} \leq r^{(B)}$.
	 - (b) If $\hat{v} \leq \hat{v}^{r}_{FI}$, then $r^{(P)} \leq r^{(B)}$, otherwise $r^{(P)} > r^{(B)}$.
  
**Key Insights**:
- Both P4P and BP incentivize reducing readmissions (lower rates than FFS).
- __Intuitive explanation__
	- If $\tau$ is low, P4P has lower readmission rates
		1. P4P's penalty starts early on & penalty of P4P is bigger than BP
		2. P4P needs to decrease $r$ more than usual while BP stays the same
	- P4P performs better when $\hat{v}$ is low
		1. Penalty per unit increase in readmission probability is greater in P4P
		2. Hospital should increase their effort greater in P4P
		3. Patient also puts more effort to reduce $r$ than P4P
		4. Reduction of $r$ is larger in P4P
	- BP performs better when $\hat{v}$ is high
		- P4P reduction of $r$ ends when $r=\tau$

**Proposition 9 (Funder’s objective)**:
1. Funder’s objective is always lower with P4P and BP than FFS.
2. Two cases:
	- (a) If $\hat{v} > \hat{v}^{(P)}_{FI}$:
		- i. If $\Pi_f^{(P)}(u = \frac{\rho - \tau}{1 + \rho}) > \Pi_f^{(B)}$, then $\Pi_f^{(B)} \leq \Pi_f^{(P)}$ for all $u$.
		- ii. Otherwise, there exists a threshold $u_{FI}$ where $\Pi_f^{(P)} \leq \Pi_f^{(B)}$ when $u \leq u_{FI}$ and $\Pi_f^{(P)} > \Pi_f^{(B)}$ otherwise.
	- (b) If $\hat{v} \leq \hat{v}^{(P)}_{FI}$ and hospital treatment cost $c_h$ is high, BP is better than P4P.

**Key Insights**:
- FFS least effective in minimizing funder’s objective.
- P4P is effective but can be costly, especially with low productivity ($\hat{v}$).
	- $R$ needs to be increased because the effort of the hospital & patient should be very high
- BP is better if patient-hospital interactions are less effective or if treatment costs are high.
	- In BP, funder pays a constant amount to hospital, the hospital needs to decrease $r$
	- In P4P, hospital may ask for higher $R$ because of the increased penalty


### 5.4.2. Partial Coverage: Patient Co-Payment $(C > 0)$

**Proposition 10: Equilibrium Readmission Rates (FFS, P4P, BP)**  
1. Always true: $\Pi^{(P)} \leq \Pi^{(F)}$ and $\Pi^{(B)} \leq \Pi^{(F)}$.  
2. If co-payment $C(B)$ is fixed:
	- $\Pi^{(P)} \leq \Pi^{(B)}$ when $\tau \leq \rho(1-\phi(C = C(B)))$.  
	- $\Pi^{(P)} > \Pi^{(B)}$ otherwise.

**Analysis**:
- FFS results in the highest readmission rates compared to P4P and BP.
- If $\tau$ is small, P4P achieves a lower readmission rate than BP.
- If $\tau$ is large, BP leads to a lower readmission rate.
	- Same reason as $C=0$

**Proposition 11: Funder’s Objective Under Partial Patient Coverage**  
1. Always true: $\Pi_f^{(P)}, \Pi_f^{(B)} \leq \Pi_f^{(F)}$ (P4P and BP are better than FFS for the funder).  
2. When $\Pi^{(\tau)} = \tau$ and $a > b$, there exists a threshold $c_{h_{PI}}$:
	- If $c_h \leq c_{h_{PI}}$, there are thresholds $\hat{v}_{PI_1}$ and $\hat{v}_{PI_2}$ such that:
		- If $\hat{v}_{PI_1} \leq \hat{v} \leq \hat{v}_{PI_2}$, P4P outperforms BP ($\tilde{\Pi}_f^{(P)} \geq \Pi_f^{(B)}$).
		- Otherwise, BP outperforms P4P.
	- If $c_h > c_{h_{PI}}$, BP is always better than P4P ($\Pi_f^{(B)} > \Pi_f^{(P)}$).

**Analysis**:
- P4P and BP induce readmission-reduction efforts, unlike FFS.
- When hospital treatment costs are low, P4P is preferred in intermediate patient productivity ranges ($\hat{v}$).
	1. $c_h$ low 
	2. safe to invest money on effort to reduce $r$ (intermediate $\hat{v}$ is needed here for suitable penalty)
	3. reduces patients total cost 
	4. reduces funder's optimizing function 
		1. $c_h$ low 
		2. $R$ low 
		3. $\Pi_f$ increased by lesser penalty < $\Pi_f$ reduced by patient cost
- When hospital costs are high, BP is always optimal for the funder.
	- Same as $C=0$


# Conclusion

- **FFS (Fee for Service)**: Not ideal for reducing readmissions since hospitals lack incentives. 

- **P4P vs. BP**:
	- **P4P** induces greater effort, especially when the penalty threshold $s$ is low, but is expensive to implement.
	- **BP** is preferable when hospital treatment costs are high, particularly if the co-productive relationship is less effective.

- **Cost-effectiveness**: 
	- P4P is only cost-effective when the penalty is significant. 
	- BP is better when the co-productive relation is weak, as it produces the same effort regardless of reimbursement size.

- **Patient co-payments**: 
	- Co-payments reduce readmissions and funder obligations
	- Excessive cost-sharing may deter care-seeking.

- **Cherry-picking risk**: 
	- Hospitals may prefer patients who are better at self-managing their conditions, focusing efforts on the most cost-effective patients. 
	- Contrary to the idea that hospitals would help the least capable patients.



