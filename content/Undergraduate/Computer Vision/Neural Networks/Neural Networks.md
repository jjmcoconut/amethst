A neural network is a computer model emulating the brain's structure, using interconnected nodes to process information for tasks like pattern recognition in machine learning.

![[Pasted image 20231209230012.png|500]]
A simple example of neural network(with just neurons)

If the neural network has n layers(Input layer, (n-2)hidden layer, output layer)
- $W_1, W_2,\cdots,W_{n-1}$: weight matrices
- $\textbf{h}_1, \textbf{h}_2, \cdots, \textbf{h}_{n-2}$: values of hidden layer(bias $b$ is included as 1 in the first element in $h_i$)
- $f_1,f_2,\cdots,f_{n-1}$: [[Activation Function]] for each layer
	- If we do not have activation functions we get the result of $output = W_nW_{n-1}\cdots W_1\textbf{x}$. This is because the weight matrices can be multiplied since the dimensions are matched perfectly.

The first hidden layer is calculated by $\textbf{h}_1 = f_1(W_1\textbf{x})$   

The rest of it is calculated by $\textbf{h}_i =f_i(W_i\textbf{h}_{i-1})$, $output = h_{n-1}$ 

![[Pasted image 20231209233938.png|500]]
A simple neural network with features explained above()

[[Training Neural Network]]


[[Convolutional Neural Networks]]
- Type of artificial neural network designed for visual data processing, using specialized layers to automatically learn and identify hierarchical patterns, such as edges and textures, enabling effective image recognition and classification.

