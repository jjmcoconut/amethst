
### [[Reinforcement Learning]]
One area of machine learning coordinating the relationship between the Agent and the Environment

### [[Policy Gradient]]
A way to optimize a policy-based reinforcement learning method using parameters for the policy

### [[CVaR(Conditional Value-at-Risk)]]
Risk measure that quantifies the potential loss in value of an investment portfolio beyond a certain confidence level

# Goal of this Paper: Predictive CVaR Policy Gradient
Making weight of each cost as the probability of current sample trajectory from worst 1-fraction senarios predicted at the moment the cost incurred

Method: [[Policy Gradient]]

### Policy Space
- $\Pi^{H}$: set of all non-anticipating policies  
	- for any policy $\pi \in \Pi^H$ is a $(\pi_t)_{t=1,\cdots,T}$ such that $A_t \sim \pi_t(\cdot|H_t)$, $\pi_t:H_t \rightarrow A_t$ 
- $\Pi^\chi$: set of all Markov policies
	- for any policy $\pi \in \Pi^\chi$ is a $(\pi_t)_{t=1,\cdots,T}$ such that $A_t \sim \pi_t(\cdot|X_t)$, $\pi_t:X_t \rightarrow A_t$ 
This paper focuses on a certain family of Markov policies $\Pi^\Theta$ parameterized by a multi-dimension policy parameter $\theta \in \Theta \subset \mathbb{R}^d$

### Policy Optimization with CVaR
Goal: finding a optimal policy $\pi^* \in \Pi^\Theta$ that minimizes CVaR
$$\min_{\pi \in \Pi^\Theta}\{J_q(\pi):=q\cdot\text{CVaR}_q^\pi [\sum_{t=1}^TC_t]\}
\Leftrightarrow \min_{\pi \in \Pi^\Theta} \text{CVaR}_q^\pi[C_{1:T}]
$$

### Gradient Estimators Risk-Neutral Policy Gradient(q=1)
- Score function trick
	Optimizing a randomized policy $A_t \sim \pi_t^\theta(\cdot|X_t)$
	$$\hat{\triangledown}_\theta J_{q=1}(H_{T+1})=\sum_{t=1}^T \frac{\partial \text{ln}\pi_t^\theta(A_t|X_t)}{\partial \theta} \sum_{s=t}^T C_t$$
- Direct differentiation
	Optimizing a deterministic policy $A_t = \pi_t^\theta(X_t)$ in a differentiable environment that the sample path can be differentiated by $\theta$
	$$\hat{\triangledown}_\theta J_{q=1}(H_{T+1})=\sum_{t=1}^T \frac{\partial\pi_t^\theta(X_t)}{\partial \theta}\sum_{t=1}^T\frac{dC_s}{dA_t}$$
- Randomized finite difference methods:
	$$\hat{\triangledown}_\theta J_{q=1}(H_{T+1},\tilde{H}_{T+1})=\frac{\epsilon}{\sigma}\sum_{t=1}^T(\tilde{C}_t-C_t{})$$
	$\tilde{H}_{T+1}$: sample trajectory with $\tilde{\theta} = \theta+\epsilon$ with $\epsilon \sim N(0,\sigma^2I_d)$

## Algorithm

### 1. Risk-Neutral Reformulation
From variational represenation of CVaR(Rockafellar et al., 2000)
$$J_q(\pi)=\min_{\eta \in \mathbb{R}}\text{E}^\pi[q\eta+(C_{1:T}-\eta)^+]$$
And for this paper we can write it as
$$J_q(\pi)=\min_{\eta \in \mathbb{R},\theta \in \Theta}\text{E}^{\pi_\theta}[q\eta+(C_{1:T}-\eta)^+]$$

### 2. Predictive Tail Probability Process
- Predictive tail probability process
	Given policy $\pi \in \Pi^H$, threshold $\eta \in \mathbb{R}$
	$$Q_t^{\pi,\eta}:=\text{P}(C_{1:T}\geq\eta|H_{t+1})$$
	In words $Q_t^{\pi,\eta}$ is the probability of the final cost exceeding the threshold $\eta$ given policy $\pi$ and information up to time $t$
- Rao-Blackwellized time decomposition
	$$
	\begin{aligned}
	Q_t^{\pi,\eta}&=\text{I}[{C_{1:T}}\geq \eta] \\
	Q_0^{\pi,\eta}&=\text{E}^\pi[Q_T^{\pi,\eta}|H_{t+1}] \\
	Q_T^{\pi,\eta}&=\text{P}^\pi(C_{1:T}\geq\eta)
	\end{aligned}
	$$
- Lemma
	Given policy $\pi \in \Pi^H$, threshold $\eta \in \mathbb{R}$
	$E^\pi[(C_{1:T}-\eta)^+]=E^\pi[\sum_{t=1}^TQ_t^{\pi,\eta}C_t]-\eta Q_0^{\pi,\eta}$
	 
- Proposition
	given $\pi \in \Pi^H$, define $\eta^\pi :=\text{VaR}_q^\pi[C_{1:T}]$ the solution to $J_q(\pi)=\min_{\eta \in \mathbb{R}}\text{E}^\pi[q\eta+(C_{1:T}-\eta)^+]$
	1. If $C_{1:T}$ has no probability mass at $\eta^\pi$: $J_q(\pi)=E^\pi[\sum_{t=1}^T Q_t^{\pi,\eta^\pi}C_t]$
	2. Else: $|J_q(\pi)-E[\sum_{t=1}^TQ_t^{\pi,\eta^\pi}C_t]|\leq |\eta^\pi|P(C_{1:T}=\eta^\pi)$

- Predictive tail probability estimation
	Originally $Q_t^{\pi,\eta}$ should be a function of $H_{t+1}$. However we consider only Markov policies $\pi^\theta \in \Pi^\Theta$ 
	__Proposition__
	$\forall \pi \in \Pi^\chi,\exists (f_t^\pi)_{t=1,\cdots,T}$ with $f_t^\pi:\chi\times\mathbb{R} \rightarrow[0,1]$ such that $Q_t^{pi,\eta}=f_t^\pi(X_{t+1},C_{1:t}-\eta)$ 
	- We can get $Q_t^{\pi,\eta}$ by giving the information of the state at the next time, and the total cost till now minus the threshold. - We. do not need the entire history information.
### 3. Predictive CVaR Policy Gradient Algorithm
1. Policy($\theta$) Optimization
	Optimize policy parameter $\theta$ solving $\min_{\theta \in \Theta} E[\sum_{t=1}^T \hat{Q}_tC_t]$ 
2. Predictive tail probability($\phi$) estimation
	Optimize function $(f_t^\phi)_{t=1,\cdots,T}$ parameterized by $\phi$ solving $\min_{\phi \in \Phi}E[\sum_{t=1}^T (I\{C_{1:T}\geq\eta\} -f_t^\phi (X_{t+1},C_{1:t}-\eta))^2]$
3. $\text{VaR}_q$ value estimation
	learn $\text{VaR}_q$ value of total cost distribution solving $\min_{\eta\in\mathbb{R}}E[q\eta+(C_{1:T}-\eta)^+]$

__Algorithm__
Initialize $\theta,\eta,\phi$
for $k=1,2,\cdots$
	Run $\pi^\theta$ and obtain sample trajectory $H_{T+1}=(X_1,A_1,C_1,\cdots,X_T,A_T,C_T)$
	$\hat{Q}_t \leftarrow f_t^\phi(X_{t+1},C_{1:t}-\eta)$ for all $t=1,2,\cdots,T$
	$H_{T+1}^Q \leftarrow (X_1,A_1,\hat{Q}_1C_1,\cdots,X_T,A_T,\hat{Q}_TC_T)$
	update $\theta,\phi,\eta$ in order

For this
1. Continuous action state
2. parameter of policy should be reasonable

State space: $\mathbb{R}$
Action space: [-1,1]
Reward
- +1 for each integer in [-4,9]
- -0.2 for each move
- +10 for points -5 and 10
T=22
Let $A_t = \pi_t^\theta(X_t) = tanh(\theta_1 + \theta_2S_t+\theta_3\text{I(not visited -5)}+\theta_4\text{I(not visited 10)}+\epsilon)$, $\epsilon \sim N(0,1)$

갑자기 어느 순간부터 Markov 특성이 빠짐?
