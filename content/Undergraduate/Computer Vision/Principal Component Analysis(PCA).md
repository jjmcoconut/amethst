PCA is a statistical technique for reducing the dimensionality of a dataset. This is accomplished by linearly transforming the data into a new coordinate system where (most of) the variation in the data can be described with fewer dimensions than the initial data(Wikipedia,2023).

### Define

Given points $x_1,x_2,\cdots,x_n$ let $w_{(1)},w_{(2)},\cdots,w_{(k)}$ be the $1,2,\cdots,d$ component, the vector that maximizes the variance when projected onto $span(w_{(1)},w_{(2)},\cdots,w_{(i)})$ 

### First Component
In order to maximize variance, the first weight vector $w_{(1)}$ thus has to satisfy

$$w_{(1)}=arg⁡max_{‖w‖=1}{\sum_i(x_i⋅w)2}$$

Equivalently, writing this in matrix form gives

$$w_{(1)}=arg⁡max_{‖w‖=1}{‖Xw‖^2}=arg⁡max_{‖w‖=1}{w^TX^TXw}$$

By using the eigenvalue, eigenvectors of $X^TX: \lambda_i, e_i$, with the order of $\lambda_1>\lambda_2>\cdots>\lambda_k$ 

$$max_{||w||=1}w^TX^TXw=e_1^TX^TXe_i = e_1^T\lambda_1e_1 = \lambda_1e_1^te_1 = \lambda_1||e_1||^2 = \lambda_1$$

First component is the eigenvector with largest eigenvalue: $W_{(1)}=e_1$

### Nth component

Needs thinking

Without $w_{(1)}$ on $\mathbb{R}^d$  we can see that $w_{(2)}=e_2$. However it is a question to me that is the $span(w_{(1)},w_{(2)})$ is the best combination to maximize the variance? Why do need to fix $w_{(1)}$ same as the value we have got on the first component? Is there really not a better solution?