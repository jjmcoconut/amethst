### Objective
Suppose there are K clusters $C_1, C_2, \cdots, C_k$ with centroids $c_1, c_2, \cdots, c_k$.

The least square error is defined as $D=\sum^K_{k=1}\sum_{x_i \in C_k}||x_i-c_k||^2$ 

Out of all possible combinations of $C_1,C_2,\cdots,C_n$ find the one that minimizes $D$

### Method
- Input
	- K: number of clusters
	- $x_1,x_2,\cdots,x_n$: set of points
- Init
	- Place centroid $c_1,c_2,\cdots,c_n$ at random locations
- While cluster assignment changes:
	- for all $x_1,x_2,\cdots,x_n$ 
		- find nearest centroid $c_j$
		- assign point $x_i$ to cluster $C_j$ 
	- for each cluster $C_1,C_2,\cdots,C_n$
		- new centroid $$c_j =\frac{1}{|C_j|} \sum_{x_i \in C_j}x_i$$ 
- Time complexity: $O(iteration\times clusters \times instances \times dimensions)$  

### Pros and Cons
1. Pros
	- Very simple
	- Converges to minimum of the error function $D$
- Cons
	- Memory-intensive
	- Parameter K is needed for input
	- Sensitive to initialzation & outliers