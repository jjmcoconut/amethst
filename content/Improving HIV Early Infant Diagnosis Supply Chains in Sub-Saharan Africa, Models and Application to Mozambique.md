Jónas Oddur Jónasson, Sarang Deo, Jérémie Gallienc

# Introduction

__Early Infant Diagnosis (EID) Network for HIV__
- **Problem**: 
	- 90,000 children died of AIDS-related causes in sub-Saharan Africa (2015)
	- 150,000 infected with HIV
	- Without treatment, >1/3 of infected infants die before 1st birthday, >1/2 before 2nd
- **Diagnostic Challenges**:
	- HIV antibody test: high false-positive rate in infants
	- Virological testing (PCR) required: expensive, complex, limited availability
- **EID Network**:
	- Blood samples from clinics sent to labs for analysis
	- Key performance measure: Turnaround Time (TAT)
- **Importance of Reducing TAT**:
	- Enables earlier treatment initiation
	- Reduces infant mortality
	- Increases likelihood of result collection by caretakers
	- Improves subsequent health outcomes

__Research Questions__
1. How can we design of EID networks to predict health outcome?
2. How can we optimize the EID network to improve TAT and treatment initiation rates?
3. How do different network configurations affect treatment initiation rates?

# 3. Early Infant Diagnosis Systems and the Mozambique Data

## 3.1 Background on EID Systems in Sub-Saharan Africa

__HIV Transmission from Mother to Child__
- Risk can be reduced with PMTCT programs during pregnancy and delivery
- In 2013, only ~2/3 of pregnant women with HIV in low/middle-income countries enrolled in PMTCT
- ~17% of 1.4 million HIV-exposed infants were infected
- 89% of 240,000 newly infected children lived in Africa

__EID Testing__
- Recommended: virologic testing between 4-6 weeks after birth
- Only 44% of HIV-exposed infants in low/middle-income countries received test
- Less than 1/4 initiated on antiretroviral therapy (ART)


__EID Process Timeline__
![[Pasted image 20241204185244.png|500]]
1. Sample collection at clinic
2. Preprocessing clinic delay
3. Transportation delay
4. Lab batching delay
5. Lab congestion delay
6. Processing and postprocessing delays
7. Result communication back to clinic
8. Postprocessing clinic delay
9. Result communication to caretakers
10. Potential additional delays before treatment initiation

__Impact of Delays__
- Longer delays associated with lower likelihood of result collection/treatment initiation
- Infants may die before receiving results or starting treatment
- Delays beyond 30 days may reduce caretaker follow-up attempts

## 3.2 Mozambique EID Data Set

__Mozambique EID Network__
- 4 labs serving 400+ clinics across 11 regions, 128 districts
- Labs: Nampula, Quelimane, Beira (1 automatic PCR machine each), Maputo (1 automatic + 1 manual)
- Clinic-to-lab assignment based on regional administrative boundaries

__Mozambique EID Data (2011)__
- 34,791 infant records from 410 clinics
- Average age at testing: 88 days
- 75% of mothers participated in PMTCT
- 13% of infants tested HIV positive
- Average LCT: 25 days
- Average TAT: 40 days
- Pilot study (800 infants): 39% of caretakers collected test results

# 4. Simulation Model and Parameter Estimation

## 4.1 Operational Model

__Operational Model__
- Clinics: $i \in \mathcal{I} = \{1, ..., I\}$
- Labs: $j \in \mathcal{J} = \{1, ..., J\}$
- Assignment: $z_{ij} \in \{0, 1\}$
- Clinics assigned to lab $\mathcal{I}_j = \{i: z_{ij} = 1\}$

__Turnaround Time (TAT) Components__
$$TAT_i = C_{i,pre} + \sum_{j=1}^J z_{ij} T_{ij} + \sum_{j=1}^J z_{ij} LCT_j + C_{i,post}$$
- $C_{i,pre}$: Wait for transportation at clinic
- $T_{ij}$: Transportation time from clinic $i$ to lab $j$
- $LCT_j$: Lab cycle time for lab $j$
- $C_{i,post}$: Administrative delay at clinic after results received

__Clinic Delays__
- Sample arrivals: Zero-inflated Poisson (ZIP) model
	- $P(a_i=0)=(1-\pi_i)+\pi_ie^{-\lambda_i}$
	- $P(a_i=k)=\pi_i\frac{\lambda_i^k e^{-\lambda_i}}{k!}$ for $k>0$
- Transportation opportunities: Poisson process (rate $\gamma_i$)
- $C_{i,post}$: Assumed 1 day for all clinics

__Transportation Delays__
![[Pasted image 20241204191228.png|500]]
- Estimated based on clinic-lab location relationships
- Six clinic groups based on rural/district capital/regional capital and same/different region as lab

__Laboratory Delays__
$$LCT_j = B_j + W_j + P_j$$
- $B_j$: Lab batching delay
- $W_j$: Sojourn time of full batch
	- Erlang distribution: Flexibility to represent a range of distributions
	- Parameters fitted using Mozambique data
- $P_j$: Postprocessing delay
	- Simulated using empirical distribution for each lab
- Lab Queueing Model
	- $\sum_{i\in \mathcal{I}_j} GI^{[X_i]}/G^{(b,b)}_j/c_j$
	- $b = 92$ samples per batch
	- $c_j$: Number of testing machines per lab

## 4.2 Public Health Impact Model

__Clinical Model__
1. PMTCT Participation:
	- Simulated based on clinic-specific data ($Q_{i,P}$ or $Q_{i,NP}$)
2. HIV Infection:
	- Based on transmission rates for PMTCT ($V_P$) and non-PMTCT ($V_{NP}$) mothers
3. Time since infection at testing ($\zeta$):
	- Age at Testing: Simulated using countrywide empirical distribution
	- Age at Infection: Simulated based on published estimates

__Results Follow-Up Rates__
1. TAT impact:
	- 18% reduction in follow-up rate if TAT $1\rightarrow2,2\rightarrow 3$ month 
	- Constant rate for TAT ≥ 3 months
2. PMTCT vs non-PMTCT:
	- Odds ratio: 0.67 (PMTCT lower)
3. Infant mortality:
	- Simulated using Newell et al. (2004) mortality curve
	- Using communication delay $\eta$

__Treatment Follow-Up Rates__
1. Constant rate: $v = 75\%$
2. Additional delay ($\delta$): 3 weeks between result collection and treatment initiation

__Probability density function of follow-up for treatment__
- PMTCT: $F_P(\zeta, TAT_i, \eta, \delta)$
- Non-PMTCT: $F_{NP}(\zeta, TAT_i, \eta, \delta)$

__Expected number of infected infants treated from clinic $i$__
$$E[N_i] = v\pi_i \lambda_i \sum_{k∈\{P,NP\}} (Q_{i,k} V_k E[F_k(\zeta, TAT_i, \eta, \delta)])$$
- $\pi_i\lambda_i$: Average # of infants arrived at clinic $i$ (zero-inflated Poisson process)
- $Q_{i,P}$: Probability of mother participated in PMTCT
- $V_P$: Probability of mother transmitting HIV to child if participated in PMTCT

__Model Validation__
1. Compared simulated output with field data for:
	- Average TAT at clinic $i$ ($E[TAT_i]$)
	- Proportion of results received within one month ($P(TAT_i < 30)$)
	- Number of infected infants initiated on treatment ($E[N_i]$)
2. Results:
	- Simulated average TAT close to field data for all labs
	- TAT distribution matches field data
	- Simulated treatment initiation (38%) close to pilot study (39%)

Public health impact model allows us to see the change of numbers in infants initiating treatment but cannot be used to search for an improved network configuration.

# 5. Optimization Models
## 5.1 Lab Cycle Time Approximation
$$E[LCT_j]\approx \frac{(b-1)E[S_j]}{2bc_j\rho_j}+\frac{E[S_j]\rho_j^{\sqrt{2(c_j+1)}-1}}{bc_j(1-\rho_j)}\cdot\left(E+\frac{1}{2}+\frac{b_jSCV[S_j]}{2}\right)+E[S_j]+E[P_j]$$
   - Constant average clinic batch size: $E=\pi_i\lambda_i/\gamma_i$
   - Based on $\sum_{i\in \mathcal{I}_j} GI^{[X_i]}/G^{(b,b)}_j/c_j$ queueing system
   - Convex function of $\rho_j=\frac{\sum_i z_{ij}\pi_i\lambda_iE[S_j]}{b_jc_j}$ (lab $j$'s utilization)

## 5.2 Lab Assignment (OLA)

__Original:__
$$\max_{z_{ij},\rho_j}v\sum_{i=1}^I \pi_i\lambda_i\left( \sum_{k\in\{P,NP\}}Q_{i,k}V_kE[F_k(\zeta,TAT_i,\eta,\delta)] \right)$$
 * Constraints:
	 * Each clinic assigned to one lab $\sum_j z_{ij}=1$
	 * Lab utilization $\rho_j\leq1-\epsilon$

__OLA:__
$$\max_{z_{ijd},\tau_{jd},\rho_j} \sum_{i,j,d}z_{ijd}\left(\sum_w \phi_{dm}w_{im}\right)$$
- $w_{im}$: Expected infants starting treatment if results are available in month $m$ for clinic $i$
- $\phi_{dm}$: Proportion of results expected in month $m$ with TAT of $d$ days.
- $z_{ijd}=1$ if $z_{ij}=1$ and $\lfloor E[TAT_i]\rfloor =d$, 0 otherwise
- Constraints:
	- $\sum_{j,d}z_{ijd}=1$
	- $\rho_j\leq1-\epsilon$
	- $\sum_d \tau_{jd} d\geq \alpha_{ju}\rho_j+\beta_{ju}$ (LCT calculation)
		- $\tau_{jd}$" binary variable representing LCT of lab $j$ is $d$ days or not


## 5.3 Capacity Allocation (OCA)
$$\max_{z_{ijd},\tau_{jd},\rho_j} \sum_{i,j,d}z_{ijd}\left(\sum_w \phi_{dm}w_{im}\right)$$
   - Extends OLA to include capacity allocation decisions
   - Additional elements:
     * Set $\mathcal{J}$: product of lab locations and possible capacity decisions
     * $c_j$: Installing $c_j$ machines in location $l_j$
     * Binary variables $y_j$ for capacity allocation
   - New constraints:
     * $\sum_d \tau_{jd} d\geq \alpha_{ju}\rho_j+\beta_{ju}y_j$ (LCT calculation for selected lab)
     * $\sum_{i,d}z_{ijd}\pi_i\lambda_i\leq \frac{E[S_j]}{b_jc_j}y_j$ (Clinic assignment only to selected lab)
     * $\sum_{j}y_jc_j=K$ (Total allocated machine = National capacity)

# 6. Result

## 6.1 Optimal Lab Assignment (OLA) Impact

__Performance improvements__
- Average TATs reduced by 11% (37 to 33 days)
- Results available within a month increased by 26%
- Infected infants starting treatment increased by 4%
	- 12% fewer children dying before receiving results
	- 3% fewer children lost due to caretaker non-follow-up
	- Approximately 50 more infants treated annually

__Operational Mechanisms__
1. Load balancing
	- Distribution of sample load is more even across labs
		- Maputo lab utilization lowered
		- Samples from multiple regions allowed at each lab
		- Average of 7 regions per lab in OLA vs. 3 in Status Quo (SQ)
2. Clinic prioritization: 
	- Clinics with long delays assigned to specific labs.
	- Clinics likely to get results in a month benefit from less congested labs.
		- Nampula lab (Serves clinics with low clinic delays)
			* Similar LCTs as SQ
			* Average TAT shortened by 3 days
		- Beira lab (Serves clinics from all regions with long clinic delays)
			* LCTs shortened by 5 days
			* No significant impact on average TATs (little increase does not affect much)
			* Operated at higher utilization

## 6.2 Optimal Capacity Allocation (OCA) Impact

__Consolidation strategy__
- All diagnostic capacity consolidated in Nampula lab

__Comparison with Optimal Lab Assignment (OLA)__
- OCA more drastic, requires more system changes
- OCA benefits nearly twice those of OLA across all metrics

__Performance improvements__
- 22% decrease in average TATs
- 50% increase in results available within one month
- 7% increase in infected infants starting treatment

__Operational Mechanisms__
1. Consolidation trade-off:
	- Longer transport times are outweighed by shorter LCTs.
		- Increase in transportation times (6 to 11 days)
		- Dramatic reduction in LCTs (21 to 8 days)
2. Congestion and batch pooling:
	- Capacity pooling cuts congestion; batching cuts preprocessing.
		- Batching delays: 2 days to 0.5 days
		- Congestion delays: 9 days to 1 day
		- Postprocessing delays: 4-day decrease due to Nampula's efficiency

## 6.3 Managerial Considerations for EID Network Design

__Administrative Considerations for OLA__
- Assigning district clinics to the same lab: Achieves similar benefits as OLA.
- Optimizing at regional level: Results in significantly worse performance

__OCA Robustness to Utilization Changes__
- Capacity consolidation optimal or near-optimal for all utilization levels (5% to 95%)
	- Important for scale-up phase of EID programs
	- Proper capacity allocation impacts performance even with ample initial capacity

__OCA for Increasing Transportation Times__
- Consolidation in Nampula (Con[N]):
	* Optimal for transportation times up to 15% longer than observed
	* Outperforms Status Quo (SQ) for times up to 300% longer
- Very high transportation times:
	* OCA capacity allocation same as SQ
	* OCA still outperforms SQ due to improved lab assignment

# Conclusion

__Methodology__
1. **Discrete Event Simulation Model**:
	- Operational submodel: sample collection, transport, lab processing
	- Clinical submodel: PMTCT participation, age at infection/testing
	- Behavioral submodel: TAT impact on caretaker follow-up
2. **Optimization Models**:
	- Optimal Lab Assignment (OLA)
	- Optimal Capacity Allocation (OCA)

__Results for Mozambique__
- **Optimal Clinic-Lab Reassignment**:
	- 11% reduction in average TAT
	- 3.6% increase in infected infants receiving treatment
- **Capacity Consolidation (OCA solution)**:
	- 22% reduction in average TAT
	- Up to 6.9% increase in treatment initiation

__Sensitivity Analysis__
- Network design decisions most important for high/low utilization
- Capacity consolidation robust for short/moderate transportation times
- Decentralized capacity distribution better for longer transportation times (≈15% longer than Mozambique)

__Significance__
- First analytical framework for EID network design recommendations
- Insights potentially applicable to other sub-Saharan African countries
- Characterization of optimal capacity allocation for various utilization and transportation delays