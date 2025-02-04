Soo-Haeng Cho, Xin Fang, Sridhar Tayur, Ying Xu

![[Combating Child Labor, Incentives and Information Disclosure in Global Supply Chains.png]]

# 1. Introduction

__Introduction & Context__
- Definition (ILO): Child labor is work harmful to children’s well-being or schooling.
- Scale: 168 million child laborers worldwide in 2012 (~11% of children).
- Global Outsourcing Impact: Demand for cheap labor fosters child labor. Examples include cotton (Uzbekistan), cocoa (Ivory Coast), carpets/garments (India, Pakistan), toys/electronics (China).

__Challenges for Firms__
1. Costly, Imperfect Inspections
	- Hard to monitor scattered/small production sites. E.g., India’s carpet industry with 175,000+ looms.
	- Complex global networks in garment/footwear industries.
2. Penalty Schemes
	- Threatening contract termination or imposing corrective actions requires leaving the supplier higher profit margins.
	- Incentive/bonus systems (e.g., Bayer CropScience offering 5% bonus) are also expensive.

__Existing Initiatives__
- Third-Party Monitoring: Organizations conduct local site inspections; consumer education campaigns raise awareness. Reputation loss possible for implicated firms.
- Collaborative Strategies: Firms form groups (e.g., Child Labor Elimination Group, Atlanta Agreement) to share data and reduce monitoring costs.
- Information Disclosure:
- Annual CSR reports (e.g., Apple, Sony, Nike).
- California Transparency in Supply Chains Act: Requires large firms to disclose efforts to combat forced/child labor. Websites like KnowTheChain record disclosures.

__Research Gap__
- Limited studies on the effectiveness of disclosure and improved inspections for reducing child labor.
- Need to understand whether disclosed inspection policies actually help curb child labor or create unintended consequences.


# 3. Model

__Supply Chain Setup:__
- A manufacturer outsources production to a supplier using a wholesale price contract.
- The supplier can hire either adult labor (costly) or child labor (cheaper).

__Manufacturer Decisions:__
- Sets wholesale price ￼$w$
- Chooses inspection level ($\theta$￼): high ($\theta_H$￼) or low ($\theta_L$￼).

__Supplier Decisions:__
- Accepts contract if profitable.
- Decides whether to use child labor or adult labor.

__Inspection Types:__
- Internal Inspections (￼$\theta$): Manufacturer detects child labor use (probability depends on ￼$\theta$).
- External Inspections ($e$): Third parties (NGOs, media) may detect child labor independently.

__Scenarios:__
1.	Nondisclosure: Manufacturer does not reveal inspection level.
2.	Disclosure: Manufacturer discloses inspection level to suppliers and third parties.

__Sequence of Events:__
1.	Manufacturer offers wholesale price ￼.
2.	Supplier decides whether to accept and chooses labor type.
3.	Manufacturer conducts inspections (￼$\theta$).
4.	External inspections occur.
5.	Supplier faces penalties if child labor is detected.

__Penalties for Supplier:__
- Internal detection: Must compensate child workers and hire adults (incurs extra cost ￼).
- External detection: May lose future contracts with the manufacturer.

__Profit Calculations:__
- Manufacturer Profit: 
	- $$U(w,\theta,d)=v-w-I(\theta)-gd(1-\theta)e(\theta)$$
	- Includes retail price, inspection cost, and goodwill loss if child labor is exposed.
- Supplier Profit: 
	- $$\Pi(w,\theta,d)=(1-\gamma de(\theta)(1-\theta))(w-s_H+d\Delta(\theta))$$
	- ￼$\Delta(\theta)=s_H-\{(1-\theta)s_L+\theta(s_H+m)\}$ 
		- Savings from using child labor, reduced by inspection penalties.


# 4. Nondisclosure Scenario


__Key Setup__
- Manufacturer does not disclose inspection level $\theta$ to the supplier.
- Manufacturer sets wholesale price $w$.
- Manufacturer and supplier decide $\theta$ and $d$ (use of child labor) simultaneously.

__Variables & Equations__
- Equilibrium Variables:
	- $\theta^{non}(w)$: Manufacturer’s inspection level.
	- $d^{non}(w)$: Supplier’s decision on child labor.
- Wholesale price:
$$\begin{align*}
\max_{w} \quad &U(w, \theta^{non}(w), d^{non}(w))\\
s.t. \quad &w - s_H + \Delta(\theta^{non}(w))  d^{non}(w) \geq 0
\end{align*}$$
- Best Responses:
	- Manufacturer:
	$$ \theta^{non}(w) = \arg\max_{\theta \in {0, \theta_H}} \big[ v - w - I(\theta) - e(1 - \theta)g \cdot d^{non}(w) \big] $$
	- Supplier:
$$ d^{non}(w) = \arg\max_{d \in {0, 1}} \big[ (1 - \gamma e(1 - \theta^{non}(w))d) \cdot (w - s_H + \Delta(\theta^{non}(w)) \cdot d) \big] $$

__Equilibrium Analysis__
$$(w^{non},\theta^{non}(w),d^{non}(w))=\begin{cases}
(s_H+(\frac{1}{\gamma e}-1)\Delta(\theta_L),\theta_L,0)\\
(s_H-\Delta(\theta_H),\theta_H,1)\\
(s_H-\Delta(\theta_L),\theta_L,1)
\end{cases}$$

__Strategies in Nondisclosure Scenario__
1.	Premium Alone:
	- No inspections.
	- Manufacturer pays high $w$ to deter child labor.
2.	Inspection Alone:
	- Manufacturer conducts inspections to replace child labor ($d_E = 1 - \theta_H$).
3.	Do Nothing:
	- No premium or inspection.
	- Supplier uses child labor freely ($d_E = 1$).

__Key Insights__
1.	Impact of Costs:
	- High goodwill cost ($g$): Encourages premium alone or inspection strategies.
	- Low inspection cost ($I$): Manufacturer prefers inspections over premiums, possibly increasing child labor due to reliance on imperfect inspections.
2.	Impact of Future Business ($\gamma$):
	- Higher $\gamma$ reduces $w$ needed to deter child labor, making premium alone more likely.
3.	Impact of External Inspections ($e$):
	- Higher $e$ increases pressure to combat child labor, either via premiums or inspections.

__Subgame-Perfect Equilibrium__
- Outcomes Depend on $g$, $I$, \text{and} $e$:
- Premium Alone: $d_E = 0$ (best outcome for child labor).
- Inspection Alone: $d_E = 1 - \theta_H$ (moderate reduction).
- Do Nothing: $d_E = 1$ (worst outcome).


# 5. Disclosure Scenario

Key Setup
- Manufacturer publicly discloses inspection level $\theta$.
- Supplier observes $\theta$ before deciding whether to use child labor ($d$).
- Manufacturer sets $w$ and $\theta$ to maximize profit.

Variables & Equations
- Equilibrium Variables:
	- $\theta^{dis}$: Manufacturer’s disclosed inspection level.
	- $d^{dis}$: Supplier’s decision on child labor.
	- $w^{dis}$: Wholesale price set by the manufacturer.
- Manufacturer’s Profit: $$\begin{align*}
\max_{w, \theta}\quad& U(w, \theta, d^{dis}(\theta, w))\\
s.t. \quad &w - s_H + \Delta(\theta)  d^{dis}(\theta,w) \geq 0
\end{align*}$$
- Supplier’s Constraints:
$$ d^{dis}(\theta, w) = \arg\max_{d \in {0, 1}} \big[ (1 - \gamma e(\theta)(1 - \theta)d) \cdot (w - s_H + \Delta(\theta) \cdot d) \big] $$

Equilibrium Analysis
$$(w^{dis},\theta^{dis},d^{dis})=\begin{cases}
\left(s_H+\left(\frac{1}{\gamma e_H}-1\right)\Delta(e_L),\theta_L,0)\right)\\
(s_H-\Delta(\theta_H),\theta_H,1)\\
(s_H-\Delta(d_L),\theta_L,1)\\
\left(s_H+\left\{\frac{1}{\gamma e_L(1-\theta_H)}-1\right\}\Delta(\theta_H),\theta_H,0\right)
\end{cases}$$

Strategies in Disclosure Scenario
1.	Premium Alone:
	- No inspections.
	- Manufacturer pays a high $w$ to deter child labor ($d^{dis} = 0$).
2.	Inspection Alone:
	- Manufacturer inspects ($\theta = \theta_H$) but pays no premium.
	- Child labor is partially mitigated ($d_E = 1 - \theta_H$).
3.	Do Nothing:
- No inspections or premium.
	- Supplier uses child labor freely ($d_E = 1$).
4.	Premium and Inspection:
	- Manufacturer inspects and pays a moderate premium.
	- Completely deters child labor ($d_E = 0$).

Key Insights
1.	Impact of Costs:
	- High goodwill cost ($g$): Manufacturer adopts premium and inspection strategy to avoid public backlash.
	- Low inspection cost ($I$): Manufacturer relies on inspections but pays a lower premium, effectively deterring child labor.
2.	Impact of External Inspections ($e$):
	- High $e_H$: Increases pressure on the manufacturer to adopt inspections or pay premiums.
	- Low $e_L$: Encourages premium and inspection strategy by lowering supplier incentives for child labor.
3.	Supplier Penalty ($m$):
	- Higher penalties ($m$) reduce child labor savings for suppliers, making premium and inspection strategies more viable.
4.	Premium and Inspection Advantage:
	- Combines benefits of inspections and premiums, reducing costs for the manufacturer while ensuring no child labor.

Subgame-Perfect Equilibrium
- Possible Outcomes:
	- Premium Alone: $(\theta_L, 0)$.
	- Inspection Alone: $(\theta_H, 1)$.
	- Do Nothing: $(\theta_L, 1)$.
	- Premium and Inspection: $(\theta_H, 0)$.
- Best Outcome: Premium and inspection strategy eliminates child labor entirely while lowering overall costs.