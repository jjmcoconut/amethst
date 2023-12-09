
### Functions for learning
Define $g(\textbf{x}) = (\sqrt{2\pi})^{-\frac{d}{2}}e^{-\frac{||\textbf{x}||^2}{2}}$ (The probability of $d$ dimension $N(0,1)$)

Then the mean shift vector $m(\textbf{x})$ is

$$m(\textbf{x})=\frac{\sum^n_{i=1}\textbf{x}_ig(\frac{||\textbf{x}-\textbf{x}_i||^2}{h})}{\sum^n_{i=1}g(\frac{||\textbf{x}-\textbf{x}_i||^2}{h})}-\textbf{x}$$

### Methodology
1. Choose kernel and bandwith
2. For each point
	- Center a window on that point
	- Compute the mean of the data in the search window
	- Center the search window at the new mean location
	- Repeat until convergence
3. Assign points that lead to nearby modes to the same cluster

### Mean Clustering vs K-mean Clustering


| | Mean Shift | K-mean |  
| - | -------- | -------- |  
| Assume spherical cluster | X | O |  
| Parameter | Window size | K |
| Robust to outliers | Window O | X |
| Result differs by parameters | O | O |
| Expensive | O(More than K-mean) | O |


Example picture

![[Pasted image 20231209192106.png|400]]


