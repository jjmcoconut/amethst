### Dataset Analysis

![[Pasted image 20231217142524.png]]
1. By given dataset we need to estimate the probability of being transported.
	- 0 for being absolutely not transported
	- 1 for being absolutely transported
2. Some kind of algorithms to consider
	- Random tree regressor
	- Multi linear regression(with correlation)
	- Others?
3. Problems
	- __Null values - How do I process these values?__
	- Does cabin information also matter?
	- Destination information has a lot of items(Most of it TRAPPIST-1e but there are 481 others)
	- 