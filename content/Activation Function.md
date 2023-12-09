An activation function in a neural network determines the output of a neuron, introducing non-linearity to enable the network to learn complex patterns and relationships in data.

Without the activation function the hidden layers will be useless since $output = W_nW_{n-1}\cdots W_1\textbf{x} = W\textbf{x}$.

### Expectations for activation functions

1. When we adjust the weights a little, we want the output to change by a small amount.
	Therefore, we do not accept activation functions that magnify the result in a large scale like $f(\textbf{x}) = 100\textbf{x}^2$.
2. The activation function should be nonlinear
	If the activation function is linear, there is no reason to have that hidden layer. 
	$W_{i+1}f_i(W_i\textbf{h}_{i-1})=W_{i+1}(aW_i\textbf{h}_{i-1}+b)=aW_{i+1}W_i\textbf{h}_{i-1}$ 
	Is it same?
	
### Examples of activation functions
1. Sigmoid activation function
	$\sigma(z)=\frac{1}{1+e^{-z}}$: nonlinear
	$\frac{d}{dz}\sigma(z)=\sigma(z)(1-\sigma(z))<1$ -> Small changes in output given small change in weight.
2. ReLU
	$f(x) = max(0,x)$, also non-linear, and derivative $\leq1$ 
	This may look linear but the mapping is linear in only local areas

 