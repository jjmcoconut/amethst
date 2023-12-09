#### Bias 
$$ y_i - E[\hat{y_i}] $$
Difference between the expected prediction of our model & true value

#### Variance
$$ (y_i - E[\hat{y_i}])^2 $$
Amount that the estimate of the target function will change if different training data was used

![[Pasted image 20231209144757.png|400]]

#### Generalization Error Effects
##### Underfitting
 - model is too simple to represent all the relevant class characteristics
 - High bias, Low variance
 - High training error, High test error

##### Overfitting
 - model is to complex & fits irrelevant characteristics in data
 - Low bias, High variance
 - Low training error, High test error

#### Bias-Variance Trade-off
$$ MSE = \frac{1}{N} \sum^{N}_{i=1}(y_{i} - \hat{y_{i}})^2  \frac{1}{N} \sum^{N}_{i=1}  (y_{i} - E[\hat{y_{i}}]+E\hat{[y_{i}}]-\hat{y_{i}})^2 $$ Then we can express it as 
$$ MSE =\frac{1}{N} \sum^{N}_{i=1} (y_i - E[\hat{y_i}])^2 + \frac{1}{N} \sum^N_{i=1} (E[\hat{y_i}]-\hat{y_i})^2 = E[y_i-E[\hat{y_i}]]  $$

Hmm..
$$MSE =Bias^2 + Var(y_i) $$

