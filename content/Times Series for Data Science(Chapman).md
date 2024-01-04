
__Time Series__
- Time series is a collection of random variables $\{ X_t \}$, indexed on time
- Collection of random variables is generically referred to as a stochastic process. With the index set as time, we refer to the stochastic process as time series.
- For each time t, time series has its own random variable '$X_t$'

__Realization__
- Realization of time series $\{ X_t \}$ is a specific outcomes of the random process

__Covariance Stationary__
- The time series $\{X_t \}$ is covariance stationary if
	- $\mu_x = \mu$
	- $\sigma_{X_t}^2 = \sigma^2 <\infty$
	- $\gamma_{X_{t_1}X_{t_2}}$ and $\rho_{X_{t_1}X_{t_2}}$  depend only on $t_2-t_1$
- Example)
  
  ![[Pasted image 20231224181459.png|300]]
  
  This is not covariant stationary because the correlation, covariance is not dependent only with $t_2-t_1$ 

__White Noise Process__
- Process $X_t$ is said to be white noise if the following conditions hold
	- Each $X_t$ has zero mean and finite variance $\sigma_X^2$
	- $X_{t_1}, X_{t_2}$ are uncorrelated if $t_1 \neq t_2$

##### Time Series Patterns
- Trend: Long-term decrease or increase in data
- Seasonal: Data rises and falls with fixed frequency
- Cyclic: Data rises and falls with unfixed frequency

###### Decomposing with python
```py
from pandas import read_csv
from matplotlib import pyplot
from statsmodels.tsa.seasonal import seasonal_decompose
series = read_csv('airline-passengers.csv', header=0, index_col=0)
result = seasonal_decompose(series, model='multiplicative')
result.plot()
pyplot.show()
```

- Multiplicative model is: y(t) Trend $\times$ Seasonality $\times$ Noise
- Additive model: y(t) Trend + Seasonality + Noise
- Able to calculate trend by smoothing(find the optimal k)
###### Example
 - Original data
   ![[Pasted image 20231227210047.png|500]]
- Resulting data
  ![[Pasted image 20231227210109.png|500]]
###### Stationary Test - Augmented Dickey-Fuller 
- Null hypothesis($H_0$): The time series data is non-stationary
- Alternative hypothesis($H_a$): The time series is stationary
- 

###### Making time series stationary
- Differencing: subtract each data point in the time series from its successor
- 1 or 2 differencing makes it stationary
- 


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

### ARMA Models

#### AR(1) Model

$$X_t = \beta + \phi_1X_{t-1}+a_t$$
- $\phi_1$: real, nonzero
- $a_t$: white noise process with finite variance $\sigma_a^2$
- $\beta$: constant value $(1-\phi_1)\mu$
	
##### AR(1) is stationary iff $|\phi_1|<1$
- $\mu_x = \mu$
	- $E[X_t]=E[\beta+\phi_1X_{t-1}+\epsilon_t] = \beta + \phi_1E[X_{t-1}]$
	  So it must satisfy $E[X_t]=E[X_{t-1}]$ 
	   $$E[X_t]=\beta+\phi_1E[X_t] \Leftrightarrow E[X_t]=\frac{\beta}{1-\phi_1}$$
- $\sigma_{X_t}^2 = \sigma^2 <\infty$
	- $V(X_t)=\phi_1^2V(X_{t-1})+2\phi_1Cov(X_{t-1},\epsilon_t)+V(\epsilon_t)$
	  $V(X_t)=\phi_1^2V(X_t)+\sigma_a^2 \Leftrightarrow V(X_t)=\frac{\sigma_a^2}{1-\phi_1^2}$ 
- $\gamma_{X_{t_1}X_{t_2}}$ and $\rho_{X_{t_1}X_{t_2}}$  depend only on $t_2-t_1$
	- $\beta = (1-\phi_1)\mu$
	  $X_t-\mu = \phi_1(X_{t-1}-\mu)+\epsilon_t$ ($\mu$ is constant)
	  $$
	  \begin{aligned}
	  \gamma_k &= E[(X_t-\mu)(X_{t-k}-\mu)] \\
	  &= E[(\phi(X_{t-1}-\mu)+\epsilon_t)(X_{t-k}-\mu)] \\
	  &= \phi_1E[(X_{t-1}-\mu)(X_{t-k}-\mu)] + E[\epsilon_t]E[X_{t-k}-\mu] \\
	  & = \phi_1\gamma_{k-1}
	  \end{aligned}
	  $$
	  By repeated substitution:
	  $\gamma_k=\phi_1^k\gamma_0=\phi_1^kV(X_t)=\phi^k\frac{\sigma_a^2}{1-\phi_1^2}$
-  All 3 conditions for stationarity is satisfied iff $|\phi_1^2|<1$

##### Backshift Operator B
$BX_t = X_{t-1}$
Then the AR(1) can be expressed as
$(1-\phi_1B)(X_t-\mu)=a_t$ or $\phi(B)(X_t-\mu)=a_t$ given $\phi(B) = 1-\phi_1B$

##### Properties of Stationary AR(1) Models

- With zero mean $(1-\phi_1B)X_t = a_t$
- $Var(X_t) = \frac{\sigma_a^2}{1-\phi_1^2}$
- $Cov(X_t,X_{t-k}) = \phi_1^kVar(X_t) = \phi_1^k\sigma_X^2$
- $\rho_k = \frac{\gamma_{|k|}}{\gamma_0} =\phi_1^{|k|}$ ($\gamma_k = \gamma_{-k}$)

##### Spectral Density of AR(1)

Spectral density is defined as $S_x(f) = \sum_{k=-\infty}^{\infty}e^{-2\pi ifk}\rho_k$
In the case of AR(1)
$$
\begin{aligned}
S_x(f) &=\frac{\sigma_a^2}{\gamma_0|1-\phi_1e^{-i2\pi f}|^2} \\
&= \frac{1-\phi_1^2}{|1-\phi_1e^{-2i\pi f}|^2} \\
& = \frac{1-\phi_1^2}{(1-\phi_1cos2\pi f)^2+(\phi_1sin2\pi f)^2}
\end{aligned}
$$
Derivative: $\frac{\partial}{\partial f} (1-\phi_1cos2\pi f)^2 + (\phi_1sin2\pi f)^2 = 4\pi \phi_1 sin(2\pi f)$  
So if $\phi_1>0$ then $S_x(f)$ decreases as $f$ increases
and if $\phi_1<0$ then $S_x(f)$ increases as $f$ increases

#### AR(2) Model
$$X_t = \beta + \phi_1X_{t-1}+\phi_2X_{t-2}+a_t$$
- $\phi_1$: real, nonzero
- $a_t$: white noise process with finite variance $\sigma_a^2$
- $\beta$: constant value $(1-\phi_1-\phi_2)\mu$

##### Facts about AR(2)
- $E[X_t] = \mu$
- $Var(X_t) = \gamma_0=\frac{\sigma_a^2}{1-\phi_1\rho_{k-1}-\phi_2\rho_{k-2}}$
- $\rho_k = \phi_1\rho_{k-1}+\phi_2\rho_{k-2}$
- $S_x(f)=\frac{\sigma_a^2}{\gamma_0 |1-\phi_1e^{-2i\pi f}-\phi_2e^{-4i\pi f}|^2}$
- With mean 0:
  $$
  \begin{aligned}
  X_t-\phi_1X_{t-1}-\phi_2X_{t-2} &= a_t \\
  (1-\phi_1B-\phi_2B^2)X_t &= a_t\\
  \phi(B)X_t &= a_t
  \end{aligned}
  $$
  $\phi(z)$ is the characteristic equation $\phi(z) = 1-\phi_1z-\phi_2z^2$
##### Stationarity of AR(2)

AR(2) is stationary iff all of the roots of the characteristic equation are greater than 1

E