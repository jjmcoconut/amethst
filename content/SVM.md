##### Find a linear function(hyperplane) to separate positive, negative examples - which maximizes the margin

![[Pasted image 20231209153840.png|500]]

### Objective
$$ argmin_{\textbf{w},b} \frac{1}{2} ||\textbf{w}||^2 $$

Subject to $$ y_i(\textbf{x}_{i}\textbf{w}+b) \geq 1 $$

By using Lagrangian
$$ argmin_{w,b}max_{\alpha \geq 0} \frac{1}{2}||\textbf{w}||^2 +\alpha_i(1-y_i(\textbf{x}_{i}\textbf{w}+b)) $$

Solution of Lagrangian: $$ \textbf{w} = \sum^{n}_{i=1} \alpha_{i}y_{i}{\textbf{x}}_i $$

### Kernel
For situations that it cannot be separated linearly, we use the kernel trick to separate it.
For example,

![[Pasted image 20231209155718.png|500]]


### Multi-class SVMs
As explained above, SVMs are used to classify two classes. In order to classify multiple classes. There are 2 simple methods to do this.

**1. One vs Others**
	- Train: learn an SVM for each class vs rest
	- Test: apply SVM for class and assign the class that returns the highest decision value

**2. One vs One**
	- Train: learn SVM for each pair
	- Test: Each learned SVM votes for a class(Class with most votes?)

### Pros and Cons

1. Pros
	- Kernel baed -> very powerful, flexible

2. Cons
	- No multiple class SVM
	- Computation, Memory
		- Training time $\geq O(n^2)$
 