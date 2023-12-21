[Video link](https://www.youtube.com/watch?v=uBeM1FUk4Ps)

### __1. [[Likelihood function]]__

- Given a probability density or mass function $x \mapsto f(x|\theta)$ the likelihood function is $\theta \mapsto f(x|\theta)$ 
	
### __2. Stationarity and Wold Representation Theorem__
- Stochastic process{$\cdots, X_{t-1}, X_t,X_{t+1},\cdots$} consisting of random variables indexed by time index t is a __time series__
- The stochastic behavior of {$X_t$} is determined by specifying the probability density / mass functions (pdf's)
	$$p(x_{t_1},x_{t_2},\cdots,x_{t_m})$$
	for all finite collections of time indexes
	$$\{(t_1,t_2,\cdots,t_m),m<\infty\}$$
- __Definition__: A time series is __Strictly Stationary__ if (Invariance under time translation)
	$$p(t_1+\tau,t_2+\tau,\cdots,t_m+\tau)=p(t_1,t_2,\cdots,t_m) \space \forall\tau,\forall m, \forall(t_1,t_2,\cdots,t_m)$$
- __Definition__: A time series $\{ X_t \}$ is __Covariance Stationary__ if (for all constant time t)1

	$$
	\eqalign{
	E(X_t) &= \mu \\
	Var(X_t) &= \sigma_X^2\\
	Cov(X_t,X_{t+\tau}) &=\gamma(\tau)
	}
$$
	
	The __auto-correlation function__ of $\{ X_t \}$ is
	$$\eqalign{
	\rho(\tau) &= \frac{Cov(X_t,X_{t+\tau})}{\sqrt{Var(X_t)Var(X_{t+\tau})}}\\
	&= \frac {\gamma(\tau)}{\gamma(0)}
	}$$
- __Wold Representation Theorem__
	Any zero-mean covariance stationary time series $\{ X_t \}$ can be decomposed as $X_t = V_t +S_t$ where
	- $\{ V_t \}$ is a linearly deterministic process i.e. a  linear combination of past values of $V_t$ with constant coefficients. (past values can perfectly predict)
	- $S_t=\sum_{i=0}^{\infty}\psi_i\eta_{t-i}$(weighted average of $\eta_i$(white noise)) is an infinite moving average process of error terms where
		- $\psi_0 =1,\space\sum_{i=0}^{\infty}\psi_i^2<\infty$ 
		- $\{ \eta_i \}$ is linearly unpredictable white noise i.e. 
		  $E(\eta_i)=0,E(\eta_i^2)=\sigma^2,E(\eta_i\eta_j)=0 \space \forall i,\forall j \neq i$  and ${\eta_i}$ is uncorrelated with $\{ V_j \}: E(\eta_iV_j)=0, \forall i,j$  

- Intuitive Application of Wold Representation Theorem
	Suppose we want to specify a covariance stationary time series $\{ X_t \}$ to model actual data from real time series $\{x_t,t=0,1,\cdots,T\}$
	Consider the following strategy
	- Initialize a parameter p, the number of past observations in the linearly deterministic term of the Wold Decomposition of $\{X_t\}$
	- Estimate the linear projection of $X_t$ on $(X_{t-1},X_{t-2},\cdots,X_{t-p})$
		- Consider an estimation sample of size n with endpoint $t_o\leq T$
		- Let $\{ j=-(p-1),\cdots,0,1,2,\cdots,n \}$ index the subseries of $\{ t=0,1,\cdots,T \}$ corresponding to the estimation sample and define $\{ y_j:y_j=x_{t_0-n+j} \}$, (with $t_0\geq n+p$)
		- Define the vector $\textbf{Y}_{\tau \times 1}$ and matrix $\textbf{Z}_{\tau \times [\rho+1]}$ as:
		$$
		\textbf{y}= \begin{pmatrix}
		y_1 \\
		y_2 \\
		\vdots \\
		y_n 
		\end{pmatrix}
		\space
		\textbf{Z} = \begin{bmatrix}
		1 & y_0 & \cdots & y_{-(p-1)} \\
		1 & y_1 & \cdots & y_{-(p-2)} \\
		\vdots & \vdots & \ddots & \vdots \\
		1 & y_{n-1} & \cdots & y_{n-p}
		\end{bmatrix}
		$$
		- Apply OLS to specify the projection:
		$$\eqalign{
		\hat{\textbf{y}} &=\textbf{Z}(\textbf{Z}^T\textbf{Z})^{-1}\textbf{Z}\textbf{y}\\
		&= \hat{P}(Y_t|Y_{t-1},Y_{t-2},\cdots,Y_{t-p}) \\
		&= \hat{\textbf{y}}^{(p)}
		}$$
	- Compute the projection residual$$\hat{\epsilon}^{(p)} = \textbf{y}=\hat{\textbf{y}}^{(p)}$$
	- Specify moving average model: $\epsilon_t^{(p)}=\sum_{i=0}^{\infty}\psi_j\eta_{t-i}$ 
	- Case analysis
		- $\hat{\epsilon}^{(p)}$ should be orthogonal to $Y_{t-s}, s>p$. If not, increase p and start again
		- Evaluate the consistency of $\hat{\eta}_t$ with the white noise assumptions. If not, change the specification of moving average model(add additional lags, deterministic variables)

- __Lag Operator__
	Lag operator __L()__ shifts a time series back by one time increment $L(X_t) = X_{t-1}$
	Applying the operator recursively$$L^k(X_t) = X_{t-k}$$
	Inverse of these operators $$L^{-n}(X_t) = X_{t+n}$$
	- Wold Representation with Lag Operators 
		
		$$\eqalign{
		X_t &= \sum_{i=0}^{\infty} \psi_i\eta_{t-i} + V_t \\
		&= \sum_{i=0}^{\infty} \psi_iL^i(\eta_n)+V_t \\
		&= \psi(L)\eta_t+V_t \space \space(\psi(L)=\sum_{i=0}^{\infty}\psi_iL^i)
		}$$
		Suppose $\psi^{-1}(L)$ is invertible, and assume $V_t=0\space(X_t^*=X_t-V_t)$. Then 
		$$\eqalign{
		X_t &=\psi(L)\eta_t \\
		\psi^{-1}(L)X_t &= \eta_t
		}$$
		When $\psi^{-1}(L)$ exists, the time series $\{ X_t \}$ is __Invertible__ and has auto-regressive representation: 
		$$X_t=\sum_{i=0}^{\infty}\psi_i^*X_{t-i}+\eta_y$$

### __3. ARMA(p,q) Models__
- Time series $\{ X_t \}$ follows ARMA(p,q) Model with auto-regressive order p, moving-average order q 
	
	$$X_t = \mu +\phi_1(X_{t-1}-\mu)+\phi_2(X_{t-2}-\mu)+\cdots+\phi_p(X_{t-p}-\mu)+\eta_t+\theta_1\eta_{t-1}+\cdots+\theta_q\eta_{t-q}$$
	
	Where $\{\eta_t\}$ is $WN(0,\sigma^2)$, __White Noise__ with 
	
	$$\eqalign{
	E(\eta_t) &= 0, &\forall t\\
	E(\eta_t^2) &= \sigma^2<\infty, &\forall t, \space and \space E(\eta_t\eta_s) = 0, \forall t \neq s
	}$$ 
	With lag operators 
	
	$$\eqalign{
	\phi(L) &= (1-\phi_1L-\phi_2L^2-\cdots-\phi_pL^p)\\
	\theta(L) &=(1+\theta_1L+\theta_2L^2+\cdots+\theta_qL^q)
	}$$
	
	We can write 
	
	$$\phi(L)(X_t-\mu) = \theta(L)\eta_t$$
	
	and the Wold decomposition is 
	
	$$X_t=\mu+\psi(L)\eta_t, \space where \space \psi(L)=[\psi^{-1}(L)]\theta(L)$$
	
- __Order-p Auto-Regression Model: AR(p)__ 
	$\psi(L)(X_t-\mu)=\eta_t$ where $\{ \eta_t \}$ is $WN(0,\sigma^2)$ and $\psi(L)=1-\psi_1L-\cdots\phi_pL^p$ 
	- $X_t = \mu\phi(1)+\sum_{j=1}^p\phi_jX_{t-j}+\eta_t$
	- Stationary Conditions:
		let $\lambda_1,\cdots \lambda_p$ be roots of $\phi(z)=0$ ($z$: complex variable) Then 
		
		$$\phi(L)=(1-\frac{1}{\lambda_1}L)(1-\frac{1}{\lambda_2}L)\cdots(1-\frac{1}{\lambda_p}L)$$

	 - Claim: covariance stationary iff roots of $\phi(z)=0$ lie inside $\{ z:|z|\leq1 \}$ or $\{ |\lambda_i|>1 \}$ 
		 - for complex $\lambda: |\lambda|>1,$ $(1-\frac{1}{\lambda}L)^{-1} = \sum_{i=0}^\infty (\frac{1}{\lambda})^iL^i$ 
		 - $\phi^{-1}(L)=\prod_{j=1}^p[(1-\frac{1}{\lambda_j}L)^{-1}]$  
	 - __AR(1) Model__
		 $X_t-\mu = \phi(X_{t-1}-\mu)+\eta_t$
		 - The characteristic equation for AR(1) is $(1-\phi z) = 0$ with root $\lambda = \frac{1}{\phi}$
		 - AR(1) is stationary if $|\phi|<1$ ($|\lambda|>1$)
			
		$$\eqalign{
			 E(X_t) &= \mu \\
			 Var(X_t) &= \sigma_x^2 = \frac{\sigma^2}{1-\phi} \\
			 Cov(X_t,X_{t-1}) &= \phi\sigma_x^2
		 }$$
		 
		 - For $|\phi|<1$ the Wold decomposition of AR(1) is $X_t = \mu+\sum_{j=0}^{\infty}\phi^j\eta_{t-j}$ 
			 - if $0<\phi<1$ AR(1) is exponential mean-reversion to $\mu$
			 - if $-1 <\phi<0$ AR(1) is oscillating exponential mean-reversion to $\mu$
		 - For $\phi = 1$ The Wold decomposition does not exit(just a simple random walk)
		 - For $\phi>1$ the AR(1) is explosive
		 - Examples
			 - Interest rates
			 - Real exchange rate
			 - Valuation ratios
	 - Yule Walker Equations for AR(p) Processes
		From $X_t - \mu =\phi_1(X_{t-1}-\mu)+\phi_2(X_{t-2}-\mu)+\cdots+\phi_p(X_{t-p}-\mu)+\eta_t$ we can write __Yule-Walker Equations__ 
		
		$$\eqalign{
		E[(X_t-\mu)(X_{t-j}-\mu)] &= \phi_1E[(X_{t-1}-\mu)(X_{t-j}-\mu)]+\phi_2E[(X_{t-2}-\mu)(X_{t-j}-\mu)]+\\
		& \space \cdots +\phi_pE[(X_{t-p}-\mu)(X_{t-j}-\mu)]+ E[\eta_t(X_{t-p}-\mu)]\\
		\gamma(j) &=\phi_1\gamma(j-1)+\phi_2\gamma(j-2)+\cdots+\phi_p\gamma(j-p)+\delta_0\sigma^2
		}$$
		
		$$
		\begin{pmatrix}
		\gamma(1)\\
		\gamma(2)\\
		\vdots \\
		\gamma(p)
		\end{pmatrix}
		 =
		\begin{bmatrix}
		\gamma(0) & \gamma(1) &\cdots &\gamma(-(p-1))\\
		\gamma(1)& \gamma(0) &\cdots &\gamma(-(p-2))\\
		\vdots & \vdots & \ddots &\vdots \\
		\gamma(p-1)& \gamma(p-2) &\cdots &\gamma(0)
		\end{bmatrix}
		\begin{pmatrix}
		\phi_1\\
		\phi_2\\
		\vdots \\
		\phi_p
		\end{pmatrix}
		$$
		
		Since $\gamma()$ is covariance $\gamma(i)=\gamma(-i)$ the middle matrix is symmetric

- __Order-q Moving Average Model: MA(q)__
	$X_t-\mu = \theta(L)\eta_t$, where $\theta(L) = 1+\theta_1L+\cdots+\theta_qL^q$ 
	- Process $\{ X_t \}$ is invertible if all roots of $\theta(z)=0$ are outsize unit circle

		$$\eqalign{
		E(X_t) &= \mu \\
		Var(X_t) &= \gamma(0) = \sigma^2(1+\theta_1^2+\cdots+\theta_q^2) \\
		Cov(X_t,X_{t+j}) &= \begin{cases}
		0 & j>q \\
		\sigma^2(\theta_j+\theta_{j+1}\theta+\cdots+\theta_q\theta_{q-j}) & 1<j\leq q
		\end{cases}
	}$$
### 3. Accommodating Non-stationarity by Differencing
- Many economic time series exhibit non-stationary behavior consistent with random walks.
- __Differencing Operators:__ 

	$$\eqalign{
	\Delta &= 1-L \\
	\Delta^2 &= (1-L)^2 \\
	\Delta^k &= (1-L)^k
}$$
- Example: Linear Trend Reversion Model
	Suppose $X_t=TD_t+\eta_t$ where 
	- $TD_t = a+bt$, a deterministic linear trend
	- $\eta_t \sim AR(1)$ ($\eta_t = \phi\eta_{t-1}+\xi_t$ where$|\phi|<1$ and $\xi_t$ is $WN(0,\sigma^2)$
	- 
		$$\eqalign{
		\Delta X_t &= b+\eta_t \\
		&= b+(\eta_t-\eta_{t-1})\\
		&= b+ (1-L)\eta_t
	}$$
	
	