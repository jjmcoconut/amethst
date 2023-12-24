
__Time Series__
- Time series is a collection of random variables $\{ X_t \}$, indexed on time
- Collection of random variables is generically referred to as a stochastic process. With the index set as time, we refer to the stochastic process as time series.
- For each time t, time series has its own random variable '$X_t$'

__Realization__
- Realization of time series $\{ X_t \}$ is a specific outcomes of the random process

__Covariance Stationary__
- The time series $\{X_t \}$ is covariance stationary if
	- $\mu_x = \mu$
	- $\sigma_{X_t}^2 = \\sigma^2 <\infty$
	- $\gamma_{X_{t_1}X_{t_2}}$ and $\rho_{X_{t_1}X_{t_2}}$  depend only on $t_2-t_1$
- Example)
  ![[Pasted image 20231224181459.png|300]]
  This is not covariant stationary because the correlation, covariance is not dependent only with $t_2-t_1$ 

__White Noise Process__
- Process $X_t$ is said to be white noise if the following conditions hold
	- Each $X_t$ has zero mean and finite variance $\sigma_X^2$
	- $X_{t_1}, X_{t_2}$ are uncorrelated if $t_1 \neq t_2$

__Auto-correlation Plots__
- Original data
   ![[Pasted image 20231224181916.png|400]]
- Auto-correlation plots
  ![[Pasted image 20231224182049.png|400]]   

__Spectrum, Spectral Density__
- Let $X_t$ be a stationary time series with autocovariance $\gamma_k$ and autocorrelation $\rho_k$. Then for $|f| \leq 0.5$
	- The __spectrum__ of $X_t$ is defined by
	  $$P_x(f) = \sum_{k=-\infty}^{\infty}e^{-2\pi ifk}\gamma_k$$
	- The __spectral density__ of $X_t$ is defined by
	  $$S_x(f) = \sum_{k=-\infty}^{\infty}e^{-2\pi ifk}\rho_k$$
__Nyquist Frequency__
- For data $x_t, t=1,2,,\cdots,n$ then the Nyquist frequency is $\frac{1}{2}$, and the shortest observable period is 2.