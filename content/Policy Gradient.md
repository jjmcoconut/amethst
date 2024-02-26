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