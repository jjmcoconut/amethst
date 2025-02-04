
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
- Can exchange to each other using exponential, logarithmic function
- Able to calculate trend by smoothing(find the optimal k)
###### Example
 - Original data
   ![[Pasted image 20231227210047.png|500]]
- Resulting data
  ![[Pasted image 20231227210109.png|500]]
###### Stationary Test - Augmented Dickey-Fuller 
- Null hypothesis($H_0$): The time series data is non-stationary
- Alternative hypothesis($H_a$): The time series is stationary

###### Making time series stationary
- Differencing: subtract each data point in the time series from its successor
- 1 or 2 differencing makes it stationary


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
If $\phi_1>0$ then $S_x(f)$ decreases as $f$ increases. It will show a peak on $f=0$
If $\phi_1<0$ then $S_x(f)$ increases as $f$ increases. It will show a peak on $f=0.5$

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

AR(2) is stationary iff size of all the roots from the characteristic equation are greater than 1

Example: $X_t - 0.2X_{t-1}-0.63X_{t-2}=a_t$
	$\phi(z)=1-0.2z-0.63z^2=0 \Leftrightarrow (1-0.9z)(1+0.7z)=0$
	Then we get the solutions $r_1=1/0.9>1$ and $r_2=1/-0.7=-1.43$ 
	Since all root size is bigger than 1, it is stationary

##### AR(2) with 2 Real Roots

$$X_t-0.2X_{t-1}-0.63X_{t-2}=(1-0.9B)(1+0.7B)X_t=a_t$$
This will show a combination of two 1st order behaviors.
- Spectral density will show a peak both on $f=0, f=0.5$,  but slightly higher peak at $f=0$ since $r_1$ is closer to 1 than $r_2$
- Autocorrelations show a damped exponential with a slight indication of oscillating behavior

##### AR(2) with Complex Conjugate Roots
- Autocorrelation is a damped sinusoidal with frequency
  $$f_0=\frac{1}{2\pi}cos^{-1}(\frac{\phi_1}{2\sqrt{-\phi_2}})$$
- Realizations are pseudosinusoidal with frequency $f_0$
- Spectral density has peak on $f_0$


### AR(p) Models
$$X_t = \beta + \phi_1X_{t-1}+\phi_2X_{t-2}+\cdots+\phi_pX_{t-p}+a_t$$
- $\phi_1$: real, nonzero
- $a_t$: white noise process with finite variance $\sigma_a^2$
- $\beta$: constant value $(1-\phi_1-\phi_2-\cdots-\phi_p)\mu$
  
##### Facts about AR(p)
- $E[X_t] = \mu$
- $Var(X_t) = \gamma_0=\frac{\sigma_a^2}{1-\phi_1\rho_{k-1}-\cdots-\phi_p\rho_{t-p}}$
- $\rho_k = \phi_1\rho_{k-1}+\cdots+\phi_p\rho_{t-p}$
- $S_x(f)=\frac{\sigma_a^2}{\gamma_0 |1-\phi_1e^{-2i\pi f}-\cdots-\phi_pe^{-2pi\pi f}|^2}$
- With mean 0:
  $$
  \begin{aligned}
  X_t-\phi_1X_{t-1}-\cdots-\phi_pX_{t-p} &= a_t \\
  (1-\phi_1B-\cdots-\phi_pB^p)X_t &= a_t\\
  \phi(B)X_t &= a_t
  \end{aligned}
  $$
  $\phi(z)$ is the characteristic equation $\phi(z) = 1-\phi_1z-\cdots-\phi_pz^p$
  
##### Stationarity of AR(p)

AR(p) is stationary iff size of all the roots from the characteristic equation are greater than 1

##### Factor Tables for AR(p)

- 1st order and 2nd order factors serve as DNA of an AR(p) model
- Features of AR(p) model are simply a combination of 1st, 2nd order factors(no 3rd order features)

Example: Factor table for $X_t-1.95X_{t-1}+1.85X_{t-2}-0.855X_{t-3}=a_t$

| Factor | Roots | $r^{-1}$ | $f_0$ |
| :--- | ---- | ---- | ---- |
| $1-0.95B$ | $1.05$ | 0.95 | 0 |
| $1-B+0.95B^2$ | $0.55 \pm 0.90i$ | 0.95 | 0.16 |
- The size of roots are bigger than 1. It is stationary
- In this case the size of the roots are similar. It has almost equal dominance
  In other cases, the one with the size closest to 1(the smallest when stationary) will be the most dominant factor.

#### Linear filters for AR(p)

##### General linear Process
$$X_t=\mu = \sum_{j=0}^\infty \Psi_ja_{t-j}$$
Is a __general linear process__ if
- $a_t$ is a white noise process
- $\sum_{j=0}^\infty|\Psi_j|<\infty$

###### A GLP is stationary process
pf) later
###### Variance of GLP is $\sigma_X^2 = \sigma_a^2 \sum_{j=0}^\infty \Psi_j^2$
pf) later

##### AR(1) in GLP Form
$$
(1-\phi_1B)(X_t-\mu)=a_t
$$
$$
\begin{aligned}
X_t - \mu &= \frac{1}{1-\phi_1B}a_t \\
&= (1+\phi_1B+\phi_1^2B^2 + \cdots)a_t \\
&=  (\sum_{k=0}^\infty \phi_1^kB^k)a_t \\
& = \sum_{k=0}^\infty\phi_1^ka_{t-k} \\
& = \sum_{k=0}^\infty\Psi_ka_{t-k} \space(\Psi_k=\phi_1^k)
\end{aligned}
$$
__WTS: $\sum_{j=0}^\infty|\Psi_j|<\infty$__ 
 $$\sum_{k=0}^\infty |\Psi_k|=\sum_{k=0}^\infty |\phi_1^k|=\frac{1}{1-|\phi_1|}<\infty \space(\because|\phi_1|<1)$$

##### AR(p) in GLP Form

$$X_t-\mu = \phi^{-1}(B)a_t$$

Calculate this as the same way as AR(1)

#### MA Models

MA(q) Model:
$$X_t-\mu = a_t -\theta_1a_{t-1}-\cdots-\theta_qa_{t-q})$$

##### MA(1) Model
$$X_t - \mu = a_t-\theta_1a_{t-1}$$
- $X_t-\mu = \theta(B)a_t$ 
- characteristic function: $\theta(B)=1-\theta_1B$
- $E[X_t]=\mu$
- $Var(X_t)=\sigma_X^2(=\gamma_0)=\sigma_a^2(1+\theta_1^2)$
- Autocorrelations
	- $\rho_0=1$
	- $\rho_1=-\frac{\theta_1}{1+\theta_1^2} \space(show: |\rho_1|\leq 0.5)$
	- $\rho_k=0, \space k>1$
- $S_x(f)=\frac{\sigma_a^2}{\sigma_X^2}|1-\theta_1e^{-2\pi if}|^2$
- System frequencies are represented by __dips__ in the spectral density

##### MA(2) Model
$$X_t - \mu = a_t-\theta_1a_{t-1}-\theta_2a_{t-2}$$
- $X_t-\mu = \theta(B)a_t$ 
- characteristic function: $\theta(B)=1-\theta_1B-\theta_2B^2$
- $E[X_t]=\mu$
- $Var(X_t)=\sigma_X^2(=\gamma_0)=\sigma_a^2(1+\theta_1^2+\theta_2^2)$
- Autocorrelations
	- $\rho_0=1$
	- $\rho_1=-\frac{\theta_1+\theta_1\theta_2}{1+\theta_1^2+\theta_2^2}$
	- $\rho_2=-\frac{\theta_2}{1+\theta_1^2+\theta_2^2}$
	- $\rho_k=0, \space k>1$
- $S_x(f)=\frac{\sigma_a^2}{\sigma_X^2}|1-\theta_1e^{-2\pi if}-\theta_2e^{-4\pi if}|^2$
- System frequencies are represented by __dips__ in the spectral density

##### MA(q) Model
$$X_t-\mu = a_t -\theta_1a_{t-1}-\cdots-\theta_qa_{t-q})$$
- $X_t-\mu = \theta(B)a_t$ 
- characteristic function: $\theta(B)=1-\theta_1B-\cdots-\theta_qB^q$
- $E[X_t]=\mu$
- $Var(X_t)=\sigma_X^2(=\gamma_0)=\sigma_a^2(1+\theta_1^2+\cdots+\theta_q^q)$

Invertibility
- $X_t-\mu = \theta(B)a_t$ can be written as $\theta^{-1}(B)(X_t-\mu)=a_t$
- $$
	\begin{aligned}
	\theta^{-1}(B)(X_t-\mu) &= (\sum_{k=0}^\infty \pi_kB^k)(X_t-\mu) \\
	&=\sum_{k=0}^\infty \pi_k(X_{t-k}-\mu)
	\end{aligned}
	$$
	$$\sum_{k=0}^\infty \pi_k(X_{t-k}-\mu)=a_t$$
- Definition: MA(q) is __invertible__ if $\sum_{k=0}^\infty |\pi_k|<\infty$
- MA is invertible iff all roots of $\theta(z)=0$ have size bigger than 1

Reasons for invertibility
- __Uniqueness__
  Consider MA(1) model $X_t=(1-\theta_1B)a_t$ and $Y_t = (1-\frac{1}{\theta_1}B)b_t$
  We have autocorrelations as $\rho_1 = \frac{-\theta_1}{1+\theta_1^2}$ and $\rho_1^\prime = \frac{-\theta_1^{-1}}{1+\theta_1^{-2}}=\frac{-\theta_1}{1+\theta_1^2}$ 
  We can see that $\rho_1 = \rho_1^\prime$
  But given $|\theta_1|<1$ we can see that 
  - $X_t=(1-\theta_1B)a_t \Rightarrow \sum |\pi_k| = \sum |\theta_1^k| < \infty$: invertible
  - $X_t=(1-\frac{1}{\theta_1}B)a_t \Rightarrow \sum |\pi_k| = \sum \frac{1}{|\theta_1^k|} = \infty$: not invertible
  So if we choose invertible models, we can get a unique model

- Present events are associated with the past in sensible manner
  Suppose $\mu = 0$ then
  $$
  \begin{aligned}
  Y_t = (1-\frac{1}{\theta_1}B)b_t &\Rightarrow \sum_{k=0}^\infty \frac{1}{|\theta_1^k|}X_{t-k}=a_t \\
  & \Rightarrow X_t= a_t-\sum_{k=1}^\infty \frac{1}{|\theta_1^k|}X_{t-k}
  \end{aligned}
  $$
  which $\frac{1}{|\theta_1^k|}$ grows to infinity which means it is not sensible

#### ARMA(p,q) Models
$$(1-\phi_1B-\cdots-\phi_pB^p)(X_t-\mu) = (1-\theta_1B-\cdots-\theta_qB^q)a_t$$
or $\phi(B)(X_t-\mu) = \theta(B)a_t$
##### ARMA(p,q) with p>0 is stationary iff all roots of $\phi(z)=0$ are bigger than 1

##### ARMA(p,q) with q>0 is invertible iff all roots of $\theta(z)=0$ are bigger than 1

#### AR(p) vs ARMA(p,q)

Because $\sum|\pi_k|<\infty$, we can see that $|\pi_k| \rightarrow 0$ as $k \rightarrow \infty$. This means that the coefficients of __infinite order AR__ become negligible beyond some point
 

### ARMA Fitting

ARMA(p,q) fitting has two steps
1. Identifying p,q
2. Identifying $\phi_1,\cdots,\phi_p,\theta_1,\cdots,\theta_q,\mu,\sigma_a^2$

But the actual way to figure out the ARMA(p,q) model calculates $\phi_1,\cdots,\phi_p,\theta_1,\cdots,\theta_q,\mu,\sigma_a^2$ for every candidate p,q and then take the best combination using some method(AIC).

#### Finding $\phi, \theta$ given $p,q$ 
- __MOM(Method of Moments)__
	- AR(1) $X_t = \phi_1 X_{t-1}+\epsilon_t$ we can get then $\phi_1$ is the true lag1-autocorrelation which we can estimate as $\rho_1$
	- AR(2) $X_t = \phi_1X_{t-1}+\phi_2X_{t-2}+\epsilon_t$ then we get two equations using measured autocorrelations as true autocorrelation.
	  $$
	  \begin{aligned}
	  \rho_1 = \phi_1 + \rho_1\phi_2 \\
	  \rho_2 = \rho_1\phi_1 + \phi_2
	  \end{aligned}
	  $$
	  Then the result will appear as
	  $$\hat{\phi}_1 = \frac{r_1(1-r_2)}{1-r_1^2},\hat{\phi_2}=\frac{r_2-r_1}{1-r_1^2}$$
	- MA(1) $X_t = \epsilon_t -\theta_1\epsilon_{t-1}$ 
	  $$
	  \begin{aligned}
	  \rho_1 &= \frac{Cov(X_t,X_{t-1})}{Var({X_t})} \\
	  &=\frac{Cov(\epsilon_t-\theta_1\epsilon_{t-1},\epsilon_{t-1}-\theta_1\epsilon_{t-2})}{Var(\epsilon_t-\theta_1\epsilon_{t-1})} \\
	  & = \frac{-\theta_1\sigma_\epsilon^2}{(1+\theta_1^2)\sigma_\epsilon^2} \\
	  &=-\frac{\theta_1}{1+\theta_1^2}
	  \end{aligned}
	  $$
	- With higher-order MA it is hard to calculate using MOM, and is inaccurate
- __MLE__
  $$L(\phi,\theta,\sigma|\textbf{x})=(2\pi)^{-\frac{n}{2}}det({\Gamma(\phi,\theta,\sigma)})^{-\frac{1}{2}}e^{-\frac{1}{2}\textbf{x}^T\Gamma^{-1}\textbf{x}}$$
  $$log(L)=-\frac{1}{2}(nlog(2\pi)+log(det(\Gamma))-\textbf{x}^T\Gamma\textbf{x})$$
  where $\Gamma$ is a autocovariance matrix of $\textbf{x}=[x_1,x_2,\cdots,x_n]^T$ depending on $\phi,\theta,\sigma$ 
	-  AR(1) $X_t = \phi_1 X_{t-1} +\epsilon_t$ 
	  $$
	  \Gamma = \frac{\sigma_\epsilon^2}{1-\phi_1^2}
	  \begin{bmatrix}
	  1 & \phi_1 & \phi_1^2 & \cdots & \phi_1^{n-1} \\
	  \phi_1 & 1 & \phi_1 & \cdots & \phi_1^{n-2} \\
	  \vdots & \vdots & \vdots & \ddots & \vdots \\
	  \phi_1^{n-1} & \phi_1^{n-2} & \phi_1^{n-3} & \cdots & 1
	  \end{bmatrix}
	  \space(\because Var(X_t)=\frac{\sigma_\epsilon^2}{1-\phi_1^2})
	  $$
	  - MA(1) $X_t = \epsilon_t -\theta_1 \epsilon_{t-1}$
	    $$\Gamma=\sigma_\epsilon^2
	    \begin{bmatrix}
	    1+\theta_1 & \theta_1 & 0 &\cdots & 0 \\
	    \theta_1 & 1+\theta_1 & \theta_1 & \cdots & 0 \\
	    \vdots & \vdots & \vdots & \ddots &\vdots \\
	    0 & 0 & 0 & \cdots & 1+\theta_1
	    \end{bmatrix}$$
- __Yule-Walker Estimation__
- __Burg__

#### Estimating $\mu,\sigma$
- $\mu = \bar{x}$
- $\sigma_\epsilon^2 = \frac{1}{n-p}\sum_{i=p+1}^n \hat{\epsilon_t}^2 \space(\hat{\epsilon_1}=\cdots=\hat{\epsilon_{p}}=0)$

#### ARMA Model Identification - White Noise Test
The ARMA is well fit if 
- $\hat{\rho_k} \approx \frac{1}{\sqrt{n}}$
- $\hat{\rho_i}, \hat{\rho_j}$ is uncorrelated when $i \neq j$
- $\hat{\rho_k}s$ is approximately normal

By this information we can make hypothesis:
- $H_0: \rho_k=0$
- $H_a: \rho_k \neq 0$
We can reject $H_0$ by 5% level significance if $|\hat{\rho_k}|>1.96/\sqrt{n}$
However even we accept $H_0$ we cannot say that the residual is a white noise for 100% possibility.
![[IMG_E93EE08D6D4B-1.jpeg|500]]
According to the realization we can see that it is not a white noise but on graph (c) we can see that every bar does not go over the 95% significance line. Which leads to accepting $H_0$

#### Selecting p,q for ARMA(p,q)

Select p,q that minimizes for each criterion
- AIC: $ln(\hat{\sigma_\epsilon^2})+\frac{2}{n}(p+q+1)$
- BIC: $ln(\hat{\sigma_\epsilon^2})+\frac{ln(n)}{n}(p+q+1)$
- AICC: $ln(\hat{\sigma_\epsilon^2})+\frac{n+p+q+1}{n-p-q-3}$
No criterion is always better than the other(No free lunch theorem).

### Forecasting using ARMA(p,q)

#### Definition
- $\hat{X}_{t_0}(l)$ is the forecast of $X_{t_0 + l}$ given data up to time $t_0$
- $\hat{X}_{t_0}(l)=X_{t_0+l} \text{ if } l \leq 0$ 
- $\hat{\epsilon}_{t_0}(l) = 0$ if $l > 0$

#### Probability Limits for ARMA Forecasts

Forecast error: $e_{t_0}(l)=X_{t_0+l}-\hat{X}_{t_0}(l)$

If we represent ARMA in GLP form: 
- $X_t -\mu = \sum_{k=0}^\infty \psi_k \epsilon_{t-k}$
- $X_{t_0+l} -\mu = \sum_{k=0}^\infty \psi_k \epsilon_{t_0+l-k}$
Then we can calculate forecast error $e_{t_0}(l)$:
- $e_{t_0}(l)=\sum_{k=0}^{l-1} \psi_k\epsilon_{t_0+l-k}$
- $e_{t_0}(l) \sim N(0,\sigma_\epsilon^2\sum_{k=0}^{l-1}\psi_k)$

Then we can know that
$$
\frac{e_{t_0}(l)-0}{\sigma_\epsilon \sqrt{\sum_{k=0}^{l-1} \psi_k^2}} = 
\frac{X_{t_0+l}-\bar{X}_{t_0}(l)}{\sigma_\epsilon \sqrt{\sum_{k=0}^{l-1} \psi_k^2}}
\sim N(0,1)
$$
Then the prediction interval can be calculated as
$$\bar{X}_{t_0}(l) \pm z_{1-\frac{\alpha}{2}}\hat{\sigma_\epsilon}\sqrt{\sum_{k=0}^{l-1}\psi_k^2}$$
- Sometimes the time series cannot have a negative value(number of chairs, etc.) but the prediction interval may produce a negative value. In this case we should adjust that value to 0.

#### Forecast Performance

$$RMSE = \sqrt{\frac{1}{k}\sum_{k=t_0+1}^{t_0+k}(f_k-x_k)^2}$$
### ARIMA(p,d,q) Models

#### Definition
$(1-B)^d$ is the $d(d \geq 0)$th difference operator.
$X_t$ is a __ARIMA(p,d,q)__ model iff $\phi(B)(1-B)^dX_t =\theta(B)\epsilon_t$ where $\phi(B)$ is stationary, $\theta(B)$ is invertible

- ARIMA(0,1,0): $(1-B)X_t = \epsilon_t$ is same as AR(1) model with $\phi_1 = 1$
- Check for a (1-B) if the sample autocorrelation decreases slowly.
  ![[Pasted image 20240116164433.png]]
  Since ARIMA(2,2,0) has $(1-B)^2$ we can see that the first two plots have strong positive correlations

#### Methods of Deciding to Include 1-B Factors

- Naive approach
	- Simply just fit a ARMA(p,q) model and check if there is a 1-B factor inside it.
	- This method is very dangerous since the result white noise makes can differ the results in a significant way.
- Unit root tests
	- ADF(Augmented Dickey-Fuller)
		- $H_0$: Model contains a unit root
		- $H_a$: Model does not contain a unit root
	- KPSS
		- $H_0$: Model does not contain a unit root
		- $H_a$: Model contains a unit root
	- Model Comparison
		- Correctly detect unit roots(unit roots inside model)
		  KPSS performs better than ADF
		  ![[Pasted image 20240116165936.png]]
		- Correctly not detect unit roots(stationary model)
		  ![[Pasted image 20240116170209.png]]
		  Since the table represent incorrect percentages, lower percentages are better.
		  ADF has a better estimation for this. However it still dangerous for cases when $\phi_1>0.95$

#### Fitting ARIMA(p,d,q)

1. Detect unit roots until the differentiated model is a stationary model.
	- The number of differences required to stationarize the model is the estimated value d.
	- In most cases d does not exceed 2.$(d \leq 2)$
1. Fit a ARMA(p,q) for the stationarized model.

#### Forecasting with ARIMA

Fitted ARIMA(p,d,q): $\hat{\phi}(B)(1-B)^dX_t = \hat{\theta}(B)a_t$
1. Organize $\hat{\phi}(B)(1-B)^d$
2. Leave only $X_t$ on the left side and move the rest to the right.
3. Do the rest same as ARMA(p,q) model
From ARMA(p,q) we can get the prediction interval using the fact in GLP form
$$
\frac{e_{t_0}(l)-0}{\sigma_\epsilon \sqrt{\sum_{k=0}^{l-1} \psi_k^2}} = 
\frac{X_{t_0+l}-\bar{X}_{t_0}(l)}{\sigma_\epsilon \sqrt{\sum_{k=0}^{l-1} \psi_k^2}}
\sim N(0,1)
$$
Then the prediction interval can be calculated as
$$\bar{X}_{t_0}(l) \pm z_{1-\frac{\alpha}{2}}\hat{\sigma_\epsilon}\sqrt{\sum_{k=0}^{l-1}\psi_k^2}$$

### Seasonal Models

#### Definition

$X_t$ is a stationary ARIMA model iff $\phi(B)(1-B^s)X_t = \theta(B)\epsilon_t$ 
- s is a non-negative integer, the length of the season
- if $s=0$ then it is a ARMA(p,q) model
- if $s=1$ then it is a ARIMA(p,1,q) model

All forms of $1-B^s$ can be divided into $1-\alpha B,1-\beta B -\gamma B^2$  
For example, $1-B^4 = (1-B)(1+B)(1+B^2)$

#### Fitting Seasonal ARIMA Models to Data

1. Select the value s
2. Seasonally differentiate the data
3. Fit ARMA(p,q) on the differentiated data

#### Forecasting ARIMA Models

Fitted ARIMA(p,d,q): $\hat{\phi}(B)(1-B^s)X_t = \hat{\theta}(B)a_t$
1. Organize $\hat{\phi}(B)(1-B^s)$
2. Leave only $X_t$ on the left side and move the rest to the right.
3. Do the rest same as ARMA(p,q) model


### ARCH and GARCH Models

#### Why do we need this?
![[Pasted image 20240116173000.png|600]]
Features of this data
- Mean 0
- Variance does not change gradually in time. But, has sudden periods of increased and decreased variability.
It is a non-stationary process - has the behavior of a white noise
However, if we square the data then the data becomes correlated.

#### ARCH(1) Model

$u_t = \epsilon_t \sqrt{\alpha_0 + \alpha_1u_{t-1}^2}$
- $\alpha_0, \alpha_1$ are constants
- $\epsilon_t \sim N(0,1)$
- $\epsilon_t$ is uncorrelated with $u_{t-j}^2, \space j>0$

__Notes__
- $u_t^2=\epsilon_t^2(\alpha_0 +\alpha_1u_{t-1}^2)=\alpha_0 + \alpha_1u_{t-1}^2+w_t$
- $Var(u_t) = E[u_t^2]$
- $Var(u_t)$ given $u_{t-1}^2$ is $\sigma_{t|t-1}^2 = \alpha_0 +\alpha_1u_{t-1}^2$

#### ARCH(q) Model

$u_t = \epsilon_t \sqrt{\alpha_0 + \alpha_1u_{t-1}^2+\cdots +\alpha_pu_{t-p}^2}$
- $\alpha_0, \alpha_1, \cdots, \alpha_p$ are constants
- $\epsilon_t \sim N(0,1)$
- $\epsilon_t$ is uncorrelated with $u_{t-j}^2, \space j>0$

#### GARCH(p,q) Model

$u_t = \epsilon_t \sqrt{\alpha_0 + \alpha_1u_{t-1}^2+\cdots +\alpha_pu_{t-p}^2 +\beta_1\sigma_{t-1|t-2}^2+\cdots+\beta_q\sigma_{t-q|t-q-1}^2}$
- $\alpha_0, \alpha_1, \cdots, \alpha_p,\beta_1,\cdots,\beta_q$ are constants
- $\epsilon_t \sim N(0,1)$
- $\epsilon_t$ is uncorrelated with $u_{t-j}^2, \space j>0$

#### Appropriateness of ARCH/GARCH Fit to Set of Data

After fitting GARCH we can get the $\epsilon_t$ by
$$\hat{\epsilon}_t = \frac{u_t}{\sqrt{\alpha_0 + \alpha_1u_{t-1}^2+\cdots +\alpha_pu_{t-p}^2 +\beta_1\sigma_{t-1|t-2}^2+\cdots+\beta_q\sigma_{t-q|t-q-1}^2}}$$
Under the assumption $\epsilon_t \sim N(0,1)$ and uncorrelated check
- If $\epsilon_t$ follows $N(0,1)$
- Is uncorrelated by checking the plot and sample autocorrelation