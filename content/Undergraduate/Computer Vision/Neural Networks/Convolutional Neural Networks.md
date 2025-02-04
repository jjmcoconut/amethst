Using a fully connected network for a image will be need a large sized memory & computational power since images have a width$\times$height = n amount of pixels(eg. $200 \times 200=40000$ pixels, with RGB multiply 3 more) Then we have the weight array size $n\times len(h)$ where $len(h)$ usually is not smaller than n (resulting in $\approx 40000^2$ sized array)

### Motivation
1. Sparce iterations
- For image processing we care about local neighborhoods
2. Parameter sharing
- Tied weights: use same weights for more than one perceptron to achive equivariant representation 

![[Pasted image 20231210000746.png|500]]
A simple example of CNN with convolution, max pool

### Operations
1. Convolution(in Convolutional Neural Network)
- Conducting convolution with filter & image
- Mathematical operation of combining input data with a filter (kernel) to extract features, enabling the network to recognize patterns and spatial hierarchies in the data.
3. Pooling
- Taking a specific value in the window
- Similar to downsampling
- Examples
	- Max Pooling: $h^n_j(x,y)=max(h^{n-1}_k(i,j))\space (i\in N(x), j\in N(y))$ 
	- Average Pooling: $h^n_j(x,y)=\frac{1}{K}\sum h^{n-1}_k(i,j)\space (i\in N(x), j\in N(y))$ 
	- L2 Pooling $h^n_j(x,y)=\sqrt{\sum h^{n-1}_k(i,j)^2}\space (i\in N(x), j\in N(y))$ 
