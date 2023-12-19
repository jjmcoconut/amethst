The likelihood function in statistics is a measure that quantifies the probability of observing a given set of data, given a specific statistical model and its parameters.
Given a probability density or mass function $x \mapsto f(x|\theta)$ the likelihood function is $\theta \mapsto f(x|\theta)$ 

1. Example - Normal linear regression
	Let $\textbf{y}=\textbf{X}\beta + \epsilon$, where $\epsilon_{i}$ are iid $N(0,\sigma^2)$ 
	which means $\epsilon \sim N_n(\textbf{0}_n,\sigma^2\textbf{I}_n)$ or $\textbf{y} \sim N_n(\textbf{X}\beta,\sigma^2\textbf{I}_n)$ 
	Then we have the likelihood function $L(\beta,\sigma^2)=p(\textbf{y}|\textbf{X},\textbf{B}, \sigma^2)$ 
	$$L(\beta,\sigma^2)=(2\pi\sigma^2)^{-\frac{n}{2}}e^{-\frac{1}{2}(\textbf{y-X}\beta)^T(\sigma^2\textbf{I}_n)^{-1}(\textbf{y-X}\beta)}$$
	Then the log likelihood will look like
	$$log L = -\frac{n}{2}log(2\pi\sigma^2)-\frac{1}{2\sigma^2}(\textbf{y}-\textbf{X}\beta)^T(\textbf{y}-\textbf{X}\beta)$$
	To get the maximum of this we just take the derivative to zero. $$ \eqalign{
		\frac{\partial}{\partial \beta}logL = 0 & \Leftrightarrow \frac{\partial}{\partial \beta}(\textbf{y}-\textbf{X}\beta)^T(\textbf{y}-\textbf{X}\beta)=0 \\
		& \Leftrightarrow -2\textbf{y}^T\textbf{X} + 2\beta^T\textbf{X}^T\textbf{X}=0 \\
		& \Leftrightarrow \beta = (\textbf{X}^T\textbf{X})^{-1}\textbf{X}^T\textbf{y}
	}$$
	