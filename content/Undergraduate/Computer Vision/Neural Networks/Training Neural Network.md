### Loss Function

This measures how 'good' our network is classifying the training examples with respect to the parameters of the model.

Example: $\frac{1}{n}\sum^{n}_{i=1}||f(x_I)-y_i||^2$ ($f(x_i)$: predicted value, $y_i$: true value)


### [[Spaceship Titanic ANN]]
- An example of training a simple neural network.
- Used Adam for optimization, BCELoss for criterion(loss function).
- 