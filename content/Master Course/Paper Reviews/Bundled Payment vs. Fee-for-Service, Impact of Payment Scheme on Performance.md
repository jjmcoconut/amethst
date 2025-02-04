Elodie Adida, Hamed Mamani, Shima Nassiri

# Abstract

**Traditional Reimbursement (FFS)**: 
- Encourages high volume of care, not necessarily efficient care.
- Incentivizes excessive treatment intensity, leading to suboptimal system payoffs.

**New Payment Models**: **Bundled Payment (BP)**: 
- Tests removing volume-based incentives.
- Can result in suboptimal patient selection and treatment levels (too high or too low).
- Exposes providers to significant financial risk.
- Performance is highly sensitive to the bundled payment value and the provider's risk aversion.

**Provider's Decision**: 
- Providers choose treatment intensity based on a risk-averse utility function.
- May reject patients based on cost profile.
- Risk aversion negatively impacts performance under both FFS and BP.

**Hybrid and Stop-Loss Payment Mechanisms**:
- Designed to address the flaws of FFS and BP.
- Can complementarily lead to system-optimal decisions by balancing incentives and risk.


# Introduction

- **Affordable Care Act (ACA)**: Aims to reform U.S. healthcare, specifically the fee-for-service (FFS) system which compensates providers based on service volume, not quality.
- **Criticism of FFS**: FFS incentivizes unnecessary treatments, leading to high costs without improving care quality.
- **Bundled Payment (BP) System**: Proposed by Centers for Medicare & Medicaid Services (CMS) in 2013 to replace FFS. BP compensates providers with a lump sum for an entire care episode, regardless of complications, incentivizing better care management to avoid financial losses.
- **Pros & Cons of BP**:
	- **Proponents**: Claim BP can lower costs and improve care by reducing unnecessary procedures and focusing on patient outcomes.
	- **Opponents**: Concern that BP may lead to financial risks for providers, patient selection bias, and reduced care quality.

**Research Questions**:
1. Incentives for patient selection.
2. Treatment levels under different payment systems.
3. Financial risks for providers.
4. Utility and system payoff comparison between payment schemes.
5. Possibility of an improved payment system.
6. Impact of provider risk aversion.

**Methodology**:
- **Modeling BP and FFS**: Models how providers select patients, choose treatment levels, and handle risks under BP and FFS.
- **Key Factors**: Variability in patient costs, provider risk aversion, and patient selection are analyzed.

**Findings**:
- **FSF Outcomes**: FFS does not encourage system-optimal patient selection; providers tend to over-treat.
- **BP Outcomes**: BP treatment levels vary, but outcomes depend on provider risk aversion and payment value.
- **Risk Exposure**: BP exposes providers to financial risks, especially if complications arise.
  
**Hybrid Payment Models**:
  1. **Hybrid FFS-BP System**: Balances FFS and BP features, better suited for less risk-averse providers.
  2. **Stop-Loss Mechanism**: Protects highly risk-averse providers from excessive financial losses.

# Model

## 3.1. Modeling Framework
**Key elements**: 
- Population includes a finite number of beneficiaries (patients), a provider, and an insurer.
- Patients seek treatment for a non-emergency medical condition.
- Provider can accept or reject beneficiaries.
**Beneficiary utility**: 
- Receives payoff $V$ when treated.
- Denied treatment results in zero utility (reservation utility).
- Provider selects treatment level $t \in [t, \bar{t}]$ to maximize the patient's expected utility.
**Provider assumptions**: 
- Modeled as risk-averse with constant absolute risk aversion (CARA) utility function.
- Risk aversion coefficient is $\theta$.
- First-stage treatment cost $c_1(t)$ increases with treatment intensity.
- Success probability of treatment is $q(t)$.
**Treatment outcome**: 
- Failure results in complications needing further treatment, with disutility $T_B$ for the beneficiary and penalty $T_P$ for the provider (e.g., reputational damage).
- No further treatment decision by the provider in the second stage.
- Second-stage treatment cost $c_2$ applies if complications arise.
- Second-stage cost $c_2$ is random with support $[c, \bar{c}]$, reflecting patient heterogeneity.
**Beneficiary type ($\mu$)**: 
- Represents expected second-stage treatment cost.
- Types are distributed over $[\mu, \bar{\mu}]$ with probability distribution function $f(\cdot)$.
- Provider can identify beneficiary type before deciding to accept.
- Conditional distribution of second-stage costs is $g_\mu(\cdot)$ with mean $\mu$ and variance $s_\mu^2$.
**Assumption**: 
- The family of conditional probability distributions $g_\mu(\cdot)$ has the **monotone likelihood ratio property**, meaning $g_{\mu_2}(x) / g_{\mu_1}(x)$ is non-decreasing for $\mu_1 \leq \mu_2$.

## 3.2 Discussion

### 3.2.1 Treatment Level:
- Treatment level ($t$) represents intensity of care (e.g., tests, consultations), not quality.
- Providers balance cost and benefits of different treatments.
- Simplified model to capture key incentives and trade-offs in payment systems.

### 3.2.2 Beneficiary:
- Beneficiaries' payoff from treatment is homogeneous 
- Payoff is $0$ if denied, $V$ for success, and $V - T_B$ for failure.
- Beneficiaries don’t make decisions; model assumes risk-neutral beneficiaries.
- Utility function (pay-oﬀ $w$, treatment level $t$)
	- $$\pi^B(w)=q(t)U^B(V)+(1-q(t))U^B(V-T^B)$$

### 3.2.3 Insurer:
- Modeled as risk-neutral since they insure a large population, benefiting from risk pooling.
- Utility: financial cost of reimbursing the provider for every beneficiary treated

### 3.2.4 Provider:
- Providers are risk-averse (utility follows CARA, with risk-aversion coefficient $\theta$).
- Utility function:
	- $$\pi^P(t)=q(t)U^P(w_1)+(1-q(t))U^P(w_2)$$
	- $w_1, w_2$: Differ by policy
	- Utility from payoff $w$: $U^P(w)=\frac{1}{\theta}(1-e^{-\theta w})$
- Providers aim to maximize expected utility from patient outcomes.
- Providers may reject patients based on expected costs, avoiding complex cases or high-risk patients ("defensive medicine").
- Provider’s treatment level and selection decisions are made for each individual beneficiary

### 3.2.5 Treatment Costs and Success Probability:
- $c_1(t)$: First-stage cost, increase and are convex with higher treatment levels
- $q(t)$: Success probability increases but at a diminishing rate.
- First-stage treatment intensity don’t affect second-stage costs
- Success probability does not depend on the patient type

# Results

## 1. Fee-for-Service (FFS)
   - $$\begin{align}
	   \pi^P(t)&=q(t)U^P((\kappa-1)c_1(t))+(1-q(t))U^P((\kappa-1)c_1(t)+c_2-T^P)\\
	   \pi^I(t)&=-\kappa(c_1(t)+(1-q(t))c_2)\\
	   \pi^B(t)&=q(t)U^B(V)+(1-q(t))U^B(V-T^B)
    \end{align}$$
   - **Provider Incentives:** The provider is reimbursed for each procedure/test, with a margin proportional to treatment costs ($\kappa > 1$). This leads to a trade-off between treatment intensity and the potential for higher reimbursement or failure-driven utility gains.
   - **Key Findings:**
     - Providers may prefer higher treatment intensity to maximize reimbursement, especially when failure offers lower negative utility.
     - Costlier beneficiaries yield higher expected provider utility, leading to potential "reverse patient selection" where less costly patients may be denied treatment if their treatment failure imposes a significant reputational penalty.

## 2. Bundled Payment (BP)
   - $$\begin{align}
	   \pi^P(t)&=q(t)U^P(B-c_1(t))+(1-q(t))U^P(B-c_1(t)-c_2-T^P)\\
	   \pi^I(t)&=-B\\
	   \pi^B(t)&=q(t)U^B(V)+(1-q(t))U^B(V-T^B)
    \end{align}$$
   - **Payment Structure:** Providers receive a lump sum (B) to cover treatment costs, including any second-stage costs if treatment fails.
   - **Key Findings:**
     - Treatment intensity under BP tends to be lower than under FFS due to the lump sum, which does not incentivize higher intensity treatments unless failure is costly.
     - Providers are more likely to reject higher-cost beneficiaries to avoid incurring second-stage costs, leading to "direct patient selection."

## 3. System Optimum
   - $$w^S(t)=-c_1(t)+(1-q(t))(-T^P-c_2-T^B)+V$$
   - **Objective:** A central planner would aim to maximize total system utility (beneficiary, insurer, provider), achieving a Pareto-optimal solution.
   - The central planner makes decisions to maximize the system's total expected utility by optimizing the treatment level and patient selection criteria. Setting the treatment intensity t and the patient selection threshold $\mu$ to maximize the system's overall expected payoff.

   - **Key Findings:**
     - Costlier beneficiaries require higher treatment intensity for system optimization, but providers may still opt to reject very costly patients due to the high likelihood of treatment failure.
     - FFS does not align well with the system optimum, whereas BP presents closer alignment but still faces issues with patient selection and treatment intensity optimization.

## 4. Comparison of Payment Systems

**Research Question 1:** *Do the payment schemes under consideration give incentives for patient selection?*
- **Fee-for-Service (FFS):**
	- **Incentive Structure:** Providers are reimbursed per procedure, receiving a margin over costs (κ > 1).
	- **Outcome:**
		- Providers’ expected utility increases with the patient’s expected cost (μ), incentivizing acceptance of high-cost patients.
		- Could lead to "reverse patient selection," where low-cost patients might be less attractive due to insufficient expected utility.
		- **Intuitive Reason:** More treatments and higher-cost patients mean more revenue; there's no financial disincentive to accepting high-cost patients.
		- **Note:** Reverse patient selection is not commonly observed in practice.
- **Bundled Payment (BP):**
	- **Incentive Structure:** Providers receive a fixed lump-sum payment (B) to cover all services for a patient episode.
	- **Outcome:**
		- Providers’ expected utility decreases with higher expected patient costs (μ), incentivizing them to avoid high-cost patients ("direct patient selection").
		- **Intuitive Reason:** Fixed payments create financial risk when actual costs exceed B, especially with high-cost patients.
- **System Optimum:**
	- **Objective:** Maximize total expected system payoff (provider, insurer, and patient utilities combined), achieving Pareto optimality.
	- **Outcome:**
		- May be optimal to deny treatment to high-cost patients to maximize system efficiency.
		- **Intuitive Reason:** High-cost patients may reduce overall system utility due to costs outweighing benefits.
- **Conclusion:** BP aligns provider incentives with the system's interest in cost containment by encouraging avoidance of high-cost patients, whereas FFS does not promote patient selection that benefits the overall system.

**Research Question 2:** *What is the treatment level selected by the provider, and how does it compare with what would be system-optimal?*
- **FFS:**
	- **Treatment Level:** Providers tend to select the highest possible treatment intensity to maximize reimbursement.
	- **Outcome:**
		- Leads to overtreatment compared to the system-optimal level.
		- **Intuitive Reason:** More intensive treatments result in higher payments.
- **BP:**
	- **Treatment Level:**
		- Providers choose an intermediate treatment intensity, adjusting based on patient’s expected second-stage cost (μ):
			- **Higher μ:** Increase treatment to prevent costly complications.
			- **Lower μ:** Decrease treatment to reduce costs.
	- **Outcome:**
		- Can result in under-treatment compared to the system-optimal level.
		- **Intuitive Reason:** Fixed payment incentivizes cost-saving measures, potentially at the expense of optimal care.
- **System Optimum:**
	- **Treatment Level:**
		- An intermediate level that balances cost and patient benefit.
		- Increases with the patient’s expected cost (μ).
		- **Intuitive Reason:** Optimal care requires adjusting treatment intensity to maximize overall utility.
- **Conclusion:** Neither FFS nor BP leads to the system-optimal treatment level; FFS encourages overtreatment, while BP may cause under-treatment.

**Research Question 3:** *How does the financial risk borne by the provider compare across different payment schemes?*
- **FFS:**
	- **Risk Exposure:** Minimal financial risk for providers; they are reimbursed per service, and insurers bear most cost variability.
	- **Intuitive Reason:** Providers' costs are covered, and revenue increases with services rendered.
- **BP:**
	- **Risk Exposure:** Significant financial risk due to fixed payments and variability in patient costs.
		- Particularly challenging for providers with small patient populations.
	- **Risk Mitigation:** Larger patient populations allow for better risk pooling, reducing financial risk.
	- **Intuitive Reason:** Fixed payments mean providers absorb any cost overruns, which can be substantial with high-cost patients.
- **Conclusion:** BP increases financial risk for providers compared to FFS, potentially affecting treatment decisions and patient acceptance.

**Research Question 4:** *How do the utility of the provider and the total system payoff compare across the different payment schemes?*
- **FFS:**
	- **Provider Utility:** Increases with patient cost (μ), encouraging acceptance of high-cost patients and potential overtreatment.
		- **Intuitive Reason:** Higher costs lead to higher reimbursements.
	- **System Payoff:** May result in higher overall costs without improved patient outcomes.
		- **Intuitive Reason:** Incentives for over-treatment do not align with efficient resource use.
- **BP:**
	- **Provider Utility:** Decreases with patient cost (μ), leading to avoidance of high-cost patients and possible under-treatment.
		- **Intuitive Reason:** Providers aim to minimize costs to stay within the fixed payment.
	- **System Payoff:** Improves cost efficiency but may compromise patient care quality.
		- **Intuitive Reason:** Cost containment might come at the expense of adequate treatment.
- **System Optimum:**
	- **Objective:** Balance cost and patient benefit to maximize total system utility.
		- **Intuitive Reason:** Optimal outcomes are achieved when resources are used efficiently while providing necessary care.
- **Conclusion:** Both FFS and BP misalign provider utility with total system payoff, either promoting over- or under-treatment.

## 5. Proposed Solutions

   **Hybrid Payment System (HP):** 
- $$\begin{align}
\pi^P(t)&=q(t)U^P(B'-(1-\beta)c_1(t))+(1-q(t))U^P(B-(1-\beta)c_1(t)-(1-\beta)c_2-T^P)\\
\pi^I(t)&=-B-\beta[c_1(t)+(1-q(t))c_2)]\\
\pi^B(t)&=q(t)U^B(V)+(1-q(t))U^B(V-T^B)
\end{align}$$
- Combines elements of FFS and BP, offering a variable payment based on treatment costs to better align treatment intensity and patient selection with the system optimum.

 **Stop-Loss Protection:** 
- $$\begin{align}
\pi^P(t)&=q(t)U^P(B-c_1(t))+(1-q(t))U^P(B-c_1(t)-\min\{c_2,S\}-T^P)\\
\pi^I(t)&=-B-(1-q(t))(c_2-\min\{c_2,S\})\\
\pi^B(t)&=q(t)U^B(V)+(1-q(t))U^B(V-T^B)
\end{align}$$
- Caps the provider's second-stage costs, reducing the risk from high-cost beneficiaries and potentially aligning incentives closer to the system optimum when BP treatment exceeds optimal intensity.

**Research Question 5:** *Is there another payment system that could alleviate the shortcomings of schemes currently under consideration?*
- **Hybrid Payment (HP) System:**
	- **Structure:** Combines fixed payments (like BP) with variable payments based on service costs (like FFS), with a cost-sharing factor (β < 1).
	- **Outcome:**
		- Can align provider incentives with system-optimal decisions when parameters are appropriately set.
		- Shares financial risk between provider and insurer.
		- **Intuitive Reason:** Balances incentives for cost control and adequate care by rewarding efficiency without encouraging overuse.
- **Stop-Loss Protection:**
	- **Structure:** Modifies BP by capping the provider's financial responsibility for exceptionally high costs beyond a threshold (S).
	- **Outcome:**
		- Reduces financial risk from outlier cases.
		- Encourages acceptance of high-cost patients and treatment levels closer to the system optimum.
		- **Intuitive Reason:** Protects providers from extreme losses, promoting equitable patient care.
- **Conclusion:** Alternative schemes like HP and stop-loss protection can better align provider incentives with system goals, mitigating issues inherent in FFS and BP.

**Research Question 6:** *What role does the provider’s risk aversion play?*
- **Impact on Decisions:**
	- **Under FFS and BP:**
	- Increased risk aversion leads to treatment decisions deviating from the system optimum.
		- **FFS:** Risk-averse providers may still overtreat due to guaranteed reimbursements.
		- **BP:** Risk-averse providers may under-treat to minimize potential losses, affecting care quality.
	- **Under HP and Stop-Loss:**
		- Risk-sharing mechanisms accommodate risk aversion, aligning decisions closer to the system optimum.
		- **Intuitive Reason:** Sharing financial risk reduces the provider's burden, allowing for more balanced treatment decisions.
- **Alignment with System Optimum:**
	- **Low Risk Aversion:** Providers' decisions under BP may more closely align with optimal levels.
	- **High Risk Aversion:** Without risk-sharing, providers may prioritize financial security over optimal care.
- **Conclusion:** Provider risk aversion significantly influences treatment choices; payment schemes need to incorporate risk-sharing to align individual incentives with system efficiency.

# Conclusion

**Summary of Findings from Numerical Experiments:**
1. **BP Performance Sensitivity:** The bundled payment (BP) system's performance (system payoff and provider utility) depends heavily on the value of the bundled payment (B). Higher B values favor BP performance, but the system imposes significant financial risk on providers.
2. **Impact of Risk Aversion:** Increased provider risk aversion reduces the performance of both FFS and BP, particularly under BP, where patient selection rises and system payoff and provider utility decrease.
3. **Hybrid and Stop-Loss Systems:** These payment mechanisms are more effective at reducing downside risk (especially in smaller patient populations) compared to BP when B is small.
4. **Coordination Potential:** For most parameter values, a coordinating mechanism (hybrid or stop-loss) can be found. Hybrid payment systems are better suited for lower risk aversion, while stop-loss mechanisms work well with higher risk aversion.

**Concluding Remarks:**
- The paper uses a model-based approach to evaluate FFS and BP payment systems in healthcare.
- **FFS Limitations:** While FFS avoids patient selection and provider risk, it incentivizes excessive treatment intensity, leading to higher costs for insurers.
- **BP Sensitivity:** BP system success is highly sensitive to the bundle payment value and provider risk aversion. Poor implementation could lead to suboptimal patient selection, financial risks, and reduced care access.
- **Potential Solutions:** Minor adjustments to BP—such as hybrid payment models or stop-loss mechanisms—can improve performance and reduce provider risk. These adjustments could align provider decisions more closely with system-optimal outcomes.
- **Future Considerations:** Further empirical research (e.g., from BPCI pilot data) is needed to validate these findings and explore model refinements for different types of healthcare providers.


