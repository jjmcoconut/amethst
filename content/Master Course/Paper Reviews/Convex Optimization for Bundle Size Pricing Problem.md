Xiaobo Li, Hailong Sun, Chung Piaw Teo

# 1. Introduction
## Bundle Pricing Problem

__Overview__
- Study of risk-neutral monopolist selling heterogeneous products
- Focus on bundle-size pricing (BSP)
- Firm offers menu of bundles with different sizes and prices
- Customers have random valuations and maximize surplus
- Firm's objective: Maximize expected profit

__BSP Characteristics__
- Balance between mixed bundling and pure bundling
- Fewer prices to set compared to mixed bundling
- More flexible than pure bundling
- Can approximate mixed bundling profits well

__Practical Applications__
- Cable TV companies
- Theater companies and sports teams
- Streaming services (e.g., Netflix)

__Challenges__
- Efficiently finding optimal prices is extremely hard
- Involves optimizing over order statistics
- Complicated distribution of customer valuations over bundles
- Tractability of resulting pricing problem unknown

__Approximation Approach__
- Use discrete choice modeling
- Need to capture correlation structure of bundle valuations
- Limitations of common parametric choice models

__Cross-Moment Model (CMM)__
- Seeks extremal distribution from set with fixed mean vector and covariance matrix
- Captures correlations of valuations over bundles
- Easily simulated given distributions of valuations over products

__Main Contributions__
1. BSP problem under CMM is convex and efficiently solvable
2. First to solve BSP using convex optimization techniques
3. Unified and efficient approach for various distributions and dimensions
4. Extensive simulation studies show:
	- Small approximation error compared to uncorrelated approach
	- Competitive with simulation optimization method
	- Performs well compared to other approximation schemes
5. Technique extendable to other pricing problems with discrete choice constraints

Here's a summary of the Bundle Size Pricing (BSP) problem in a note-taking format:

# 3. Bundle Size Pricing

__Setting__
- Firm selling n heterogeneous products
- Homogeneous customer population
- Customer valuations: random vector $\tilde{u} = (\tilde{u}_1, ..., \tilde{u}_n)^T$
- $\tilde{u}$ follows distribution F with finite first and second moments
- $\tilde{u}_0 = 0$ (deterministic valuation for outside option)

__Firm's Offering__
- Set of bundle sizes: $S ⊆ {1, ..., n}$
- $|S| = m$
- Price vector of bundles: $p$

__Customer Behavior__
- Choose bundles to maximize total surplus
- Surplus = valuation of bundle - price
- Additive valuations for items
- At most one of each item in purchased bundle

__Notation__
- $\tilde{u}_{(i)}$: ith order statistic of \tilde{u} (ith smallest value)
- $\tilde{w}_s(\tilde{u})$: maximum valuation for bundle of size s
- $\tilde{w}_s(\tilde{u}) = Σ_{k=0}^{s-1} \tilde{u}_{(n-k)}$ for $s ∈ S$
- $\tilde{w}_0 = \tilde{u}_0 = 0$
- $c_s$: cost of size-s bundle (homogeneous marginal costs)

Problem Formulation
- Objective: Maximize expected profit
- Decision variables: $p$ (price vector)
- Constraints: 
  - Prices non-negative ($p ≥ 0$)
  - Demand based on customer surplus maximization

$$\begin{align}
&\max_{p\geq0}\quad Σ_{s∈S} (p_s - c_s)  q_s(\textbf{p})\\
&s.t.\quad q^*_s(\textbf{p}) = P_{\tilde{w}\sim G} \left(s = \text{arg}\max_{i∈\{0\}∪S} (\tilde{w}_i(\tilde{\textbf{u}}) - p_i)\right)\forall s ∈ S
\end{align}$$


Challenges
1. Characterizing distribution $G$ (joint distribution of $\tilde{w}$)
2. Calculating expected demand $q^*(p)$
3. Solving bilevel program under $G$

Proposed Solution
- Construct tractable approximation using cross-moment model

Here's a summary of the given text in note-taking style:

# 4. BSP Under the Cross-Moment Model (CMM)

### Key Concepts:
- Distribution $G$: difficult to characterize
- Empirical moments of $w̃(ũ)$: easily simulated from distribution $F$
- $ω = E_G[w̃(ũ)], \Sigma = Cov_G(w̃(ũ))$
- $Θ = \{θ | E_θ[w̃] = ω, Cov_θ(w̃) = \Sigma\}$

### CMM Problem:
- Solves upper bound of expected utility surplus of customers
- $Z^* = \sup_{\theta\in\Theta}{E_θ[\max_{s ∈ \{0\} ∪ S}(w̃s(ũ) - ps)]}$

### BSP-CMM Approximation:
$$
\begin{align}
&\max_{p ≥ 0}\sum_{s ∈ S}(p_s - c_s )q_s(\textbf{p})  , \\
&s.t. q_s(\textbf{p}) = \mathbb{P}_{\tilde{w}\sim\theta^*(\textbf{p})}\left(s-\arg\max_{i\in\{0\}∪ S}\{ \tilde{w}_i(\tilde{\textbf{u}})-p_i \}\right)\forall s\in S
\end{align}$$
- $θ^*(\textbf{p}) = \arg\sup_{θ ∈ Θ}E_θ[\max_{s ∈ \{0\} ∪ S}(w̃_s(\textbf{ũ}) - p_s)]$

### Reasons for Approximation:
1. $θ^*(p)$ and $G$ share first and second moments
   - $q(p)$ expected to be a good approximation of $q^*(p)$
   - Supported by numerical experiments
   - Capturing correlation of valuations is important

2. CMM choice probabilities more tractable than other models (e.g., MNP)
   - MNP requires evaluating multidimensional integrals
   - CMM can be solved using SDP formulation or concave function maximization

### CMM vs. MNP:
- CMM closely approximates MNP in choice probability predictions
- CMM more computationally efficient