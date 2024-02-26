One area of machine learning coordinating the relationship between the Agent and the Environment

### Algorithm
Given
$S$: Environment space
$A$: Action space
Reward space $\subset \mathbb{R}$

Every time $t$, Agent has its state $s_t \in S$, action $A(s_t)$
Whenever Agent takes an action $a \in A(s_t)$ it gets a new state $s_{t+1} \in S$ and reward $r_{t+1}$. From this interaction we try to learn the policy $\pi:S\rightarrow A$ that maximizes the total reward $R$

### Value-based
- Q-Learning
- SARSA
- DQN

### Policy-based
- [[Policy Gradient]]
- A2C
- A3C
- ACER
- TRPO
- PPO