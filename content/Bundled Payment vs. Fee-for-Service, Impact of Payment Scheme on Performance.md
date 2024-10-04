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
- Expected utility (pay-oﬀ $w$, treatment level $t$)
	- $$U^B(w)=q(t)U^B(V)+(1-q(t))U^B(V-T^B)$$

### 3.2.3 Insurer:
- Modeled as risk-neutral since they insure a large population, benefiting from risk pooling.
- Insurer’s utility is based on reimbursing providers.

### 3.2.4 Provider:
- Providers are risk-averse (utility follows CARA, with risk-aversion coefficient $\theta$).
- Expected utility
	- $$U^P(w)=\frac{1}{\theta}(1-e^{-\theta w})$$
- Providers aim to maximize expected utility from patient outcomes.
- Providers may reject patients based on expected costs, avoiding complex cases or high-risk patients ("defensive medicine").
- Provider’s treatment level and selection decisions are made for each individual beneficiary

### 3.2.5 Treatment Costs and Success Probability:
- First-stage cost $c_1(t)$ increase and are convex with higher treatment levels
- Success probability $q(t)$ increases but at a diminishing rate.
- First-stage treatment intensity don’t affect second-stage costs
- Success probability does not depend on the patient type
