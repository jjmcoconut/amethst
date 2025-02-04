### Methodology
1. Init: Make image as graph G=(V,E)
	- Node for every pixel
	- Edge between every pair of pixels, weighted by similarity or affinity of 2 nodes.
	- Example for $w(u,v)$ is $e^{\frac{1}{2\sigma^2}(Intensity(u)-Intensity(v))^2}$
		- Small $\sigma$: group nearby points
		- Large $\sigma$: group far points
2. Break graphs into segments
	- Delete links that cross between segments $A,B$ 
	- cost of $Cut(A,B) = \sum_{a \in A, b \in B}w(u,v)$
	- Best cut = $A,B$ that minimizes $Cut(A,B)$

### Drawbacks
1. Minimum cuts tend to cut off very small, isolated components![[Pasted image 20231209200746.png|300]]
	- Can be fixed by normalizing the cut by weight of all edges incident to the segment
	- Normalized cut cost: 
		 $Ncut(A,B) = \frac{cut(A,B)}{asso(A,V)}+\frac{cut(A,B)}{asso(B,V)}$ where $asso(A,V)=\sum_{u \in A, t \in V}w(u,t)$ 
		