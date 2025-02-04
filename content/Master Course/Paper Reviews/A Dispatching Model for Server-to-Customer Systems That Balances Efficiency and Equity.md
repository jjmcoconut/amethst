Laura A. McLay, Maria E. Mayorga

# Introduction

**Equity in Public Resource Allocation**: Critical but controversial in EMS systems, where both equity and efficiency must be balanced; improvements in efficiency can often introduce inequities.

**EMS Dispatch as Resource Allocation**: EMS dispatch prioritizes calls based on urgency, aiming to allocate ambulances fairly among patients; equity impacts availability for other calls.

**Equity Challenges in Dispatch Decisions**:
- Balancing immediate need (e.g., low-priority cases) against potential future high-priority needs.
- Fairness in patient outcomes and waiting times.

**Equity Measurement Variability**:
- Literature lacks consensus on evaluating equity; perspectives include ex ante vs. ex post equity (resource allocation vs. outcome focus).
- Equity measures vary widely and are inconsistently applied in EMS research.
- Social scientists use broader criteria for equity, which highlights challenges in balancing diverse stakeholder views.

**Purpose of the Paper**:
- To explore how different equity measures impact EMS dispatch policies.

**Methodology**:
- Develops an equity-constrained Markov Decision Process (MDP) model focused on dispatching ambulances to prioritized patients.
- Four equity constraints tested: two customer-centered, two server-centered.
- Includes computational study with EMS data from Hanover County, VA.

__Research Question:__
- How can equity and efficiency be optimally balanced when dispatching distinguishable servers (e.g., ambulances) to prioritized customers in emergency medical service (EMS) systems, and how do different equity measures affect dispatching policies?

# Markov Decision Process Models

**Objective**: Develop an MDP model for server-to-customer systems, assigning servers (e.g., ambulances) to prioritized customers (e.g., high/low-priority patients) with equity constraints.

**Model Type**: Linear programming MDP, enabling equity constraints without expanding the state space for efficient algorithm implementation.

**Key Elements**:
- **Customers**: Arriving service calls, categorized as high (H) or low (L) priority.
- **Servers**: Differentiated by response and service times (time to scene, treatment, transport, and return).
- **Reward**: Probability of serving high-priority customers within a response time threshold (RTT), measuring system-wide efficiency.

**Assumptions**:
1. A server must be dispatched if available.
2. Only servers at home stations can be dispatched.
3. One server per customer.
4. Servers return to home stations post-service.
5. Service times are independent of priority, exponentially distributed.
6. Zero-length customer queue (no wait times).

**Modifications & Impact**:
- **Assumptions may be relaxed** to include more realistic scenarios like dispatching from auxiliary locations or rerouting servers.
- Incorporating service time variability would require a non-Markov model, expanding state space.

**Zero-Length Queue Justification**:
- Ensures simplicity; queued customers add minimal value to the objective.
- Simulations show minimal impact on coverage/equity metrics.

**Practical Insights**:
- EMS dispatch often follows non-idling policies for liability and service assurance.
- Queue inclusion slightly increases server busy probabilities but does not significantly alter results.

**Result**: In a computational example, the proportion of lost customers was minimal (0.049), supporting model assumptions.

## 3.1 Base Model—Unconstrained MDP Model Overview

**MDP Model Review**
- Infinite-horizon, undiscounted, average reward MDP model.
### 3.1.1 Input Parameters
- **$n$**: Total number of customer locations.
- **$m$**: Number of servers (fixed locations).
- **$h$**: Customer priority set $(h \in H = \{H, L\})$; H for high priority, L for low priority.
- **$λ$**: Expected customer arrival rate (Poisson parameter).
- **$P_i$**: Conditional probability a customer arrives at location $i$.
- **$P_{h|i}$**: Probability of customer priority $h$ at location $i$.
- **$\mu_{ij}$**: Expected service time for server $j$ at location $i$ (exponentially distributed).
- **$u^h_{ij}$**: Expected reward for dispatching server $j$ to a customer with priority $h$ at location $i$.

*Note*: Parameters $λ$, $P_i$, and $P_{h|i}$ estimate customer arrival and prioritization based on CAD data. Model accommodates different customer priority classifications.

### Assumptions
- Infinite, undiscounted horizon for steady-state optimal dispatching policy analysis.
- Insight into policies beyond closest-server dispatch during high-demand periods.

### 3.1.2 States
- **System state $s$**: Combination of free (0) and busy servers at various locations $i$.
- **State space $S$**: $s = (s_1, s_2, ..., s_m)$ where $s_j = 0$ (server free) or $s_j = i$ (server busy at $i$).
- State $s$ reflects server configurations, excluding customer priority and location details.

### 3.1.3 Actions
- **Available actions $X(s,(h,i))$**: Set of actions when a customer with priority $h$ arrives at location $i$ in state $s$.
- Each state can result in up to $m$ dispatch actions.

### 3.1.4 Rewards
- Reflects marginal value of actions in terms of performance measures (e.g., response time).
- Cumulative density function of response time used for calculating rewards.
- No available servers dispatch a null server with zero reward.

### 3.1.5 Transition Probabilities
- Two transition types:
	1. Busy server completes service (based on expected service time $\mu_{ij}$).
	2. New customer arrival (based on $λ$)—server dispatched if available.
- Discrete-time MDP formulated using uniformization; maximum transition rate $\gamma$ set as: $$\gamma = λ + \sum_{j=1}^{m} \max_{i=1,2,...,n}\frac{1}{ \mu_{ij}}$$
  Scaled such that $\gamma = 1$.

**Optimal Policy**
- Optimal policy maximizes average reward per stage $g$.
- Optimality equations involve server availability indicators and value function $w(s)$.
- Value iteration not feasible with side constraints; alternate efficient formulation needed.
