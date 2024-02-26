### Policy $\pi$
The conditional probability of taking action $a \in A$ given state $s \in S$ 

### Policy-based Method
Taking action $a$ using a function of parameters $\theta \in \mathbb{R}^d$ with state $s$
$$\pi(a|s,\theta) = P(A_t = a|S_t = s,\theta_t = \theta)$$

### Policy Gradient Theorem
$J(\theta)$: Performance measure function of $\theta$ as 

Ex) MDP is a finite state space, finite action space, episodic, $\gamma=1$ 
	Then the performance measure function will be $J(\theta):=v_{\pi_\theta}(s_0)$ 
	Calculating the gradient of this does not look easy

Policy gradient theorem: way to calculate gradient
$$\triangledown_\theta J(\theta) \propto \sum_s \mu_{\pi_\theta}(s)\sum_a q_{\pi_\theta}(s,a)\triangledown_\theta(a|s)$$
$\mu_{\pi_\theta}(s)$: stationary distribution of $s$ when following policy $\pi_\theta$

Organizing the theorem
$$
\begin{aligned}
\triangledown J_\theta(\theta) &\propto \sum \sum_s \mu_{\pi_\theta}(s)\sum_a q_{\pi_\theta}(s,a)\triangledown_\theta(a|s) \\
&=\sum_s \mu_{\pi_\theta}(s)\sum_a\pi_\theta(a|s)q_{\pi_\theta}(s,a)\frac{\triangledown_\theta \pi_\theta(a|s)}{\pi_\theta(a|s)} \\
&=\sum_{s,a} \mu_{\pi_\theta}(s)\pi_\theta(a|s)\times q_{\pi_\theta}(s,a)\triangledown_\theta \text{ln} \pi_\theta(a|s) \\
&= E_{\pi_\theta}[q_{\pi_\theta(S_t,A_t)}\triangledown_\theta \text{ln}\pi_\theta (A_t|S_t)]
\end{aligned}
$$

### Reinforce: Monte-Carlo Policy-Gradient control for $\pi$

Input: $\pi(a|s,\theta)$
Parameter: $\alpha>0$ (step size)
Init: $\theta \in \mathbb{R}^d$ 

While True:
	Generate episode $S_0, A_0, R_1, \cdots, S_{T-1},A_{T-1},R_T$
	Generate $\pi(\cdot|\cdot,\theta)$
	for $t=0,1,\cdots,T-1$
		$G \leftarrow \sum_{k=t+1}^T \gamma^{k-t-1}R_k$
		$\theta \leftarrow \theta + \alpha\gamma^t\triangledown \text{ln}\pi(A_t|S_t,\theta)$

Advantages
- Has a converging feature - given $\alpha$ is small it reaches the local minimum

Disadvantages
- The variance is large - convergence may be slow

