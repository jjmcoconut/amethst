### Definition

Let $X_n, Y_n (n \geq 1)$ be discrete-time stochastic process. $(X_n,Y_n)$ is HMM if
- $X_n$ is Markov process, behavior not directly observable.
- $P(Y_n \in A | X_1=x_1,\cdots,X_n=x_n)=P(Y_n \in A|X_n=x_n)$ for every $n \geq 1, x_1,\cdots,x_n$ and every Borel set $A$
If $X_t,Y_t$ is continuous-time stochastic process, then $(X_n,Y_n)$ is HMM if
- $X_n$ is Markov process, behavior not directly observable.
- $P(Y_{t_0}\in A|\{X_t \in B_t\}_{t \leq t_0}) = P(Y_{t_0} \in A | X_{t_0} \in B_{t_0})$ for every $t_0$, every Borel set $A$, and every family of Borel sets $\{ B_t \}_{t \leq t_0}$ 

