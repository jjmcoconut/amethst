
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
	  So it must satisfy $$ 
- $\sigma_{X_t}^2 = \sigma^2 <\infty$
- $\gamma_{X_{t_1}X_{t_2}}$ and $\rho_{X_{t_1}X_{t_2}}$  depend only on $t_2-t_1$
- 