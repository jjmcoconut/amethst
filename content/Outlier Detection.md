## Methods

### Statistical(Parameter based)
#### Z-score
Just simply calculate the z-value given the dataset using the mean value as sample mean and standard deviation as the sample standard deviation.

$$z = \frac{x-\mu}{\sigma}$$
In my personal opinion using t-score seems more logical. Although if we assume the total population is large t-value converges to z-value.

#### Tukey's Range Test
- Assumptions
	- Observations being tested are independent
	- Data are normally distributed with corresponding mean
	- Std is same among data from different means
- Method
	1. Calculate ANOVA under hypothesis $H_0: \mu_1=\mu_2=\cdots=\mu_n$(Use F distribution)
	2. Calculate critical value(Q)
	   - Get critical value q from Tukey-Kramer distribution table using
		- $\alpha$: Type I error rate(prob of rejecting $H_0$) 
		- $k$: Number of population
		- $N-k$: Total number of observation - Number of population
	   - $$Q=q\times \sqrt{\frac{MSE}{n}}$$
	3. Compare group means with critical value
	- $Difference=|Mean_1-Mean_2|$ 
	- If this is larger than $Q$ then the means are significantly different

#### Grubb's Test
- Hypothesis
	- $H_0$: There is no outliers
	- $H_a$: There is exactly one outlier
- Method
1. $G=\frac{max_{i=1,\cdots,N}|Y_i-\bar{Y}|}{s}$
2. Calculate
	$$g>\frac{N-1}{\sqrt{N}}\sqrt{\frac{t_{\alpha/(2N),N-2}^2}{N-2+t_{\alpha/(2N),N-2}^2}}$$
	If $g>G$ reject $H_0$

### Density

#### [[K Nearest Neighbors Classification]]
Just simply add(or take the mean) the distance to k-nearest neighbors.
```py
from sklearn.neighbors import NearestNeighbors
threshold = 5
nhbds = NearestNeighbors(n_neighbors = 10)
nhbds.fit(df)
dist,_ = nhbds.kneighbors(df)
mean_dist = dist.mean(axis=1)
outlier_idx = np.where(mean_dist>threshold)
```

#### Local Outlier Factor
##### Math
The key idea is to estimate the local density around each data point
- Reachability Distance(RD) from point A to point B is
	$$RD_k(A,B)=max(dist(A,B),k-dist(B))$$
- Local Reachability Density: inverse of average reachability distance from A to k-nhbds
	$$LRD_k(A)=\frac{|N_k(A)|}{\sum_{B \in N_k(A)} RD_k(A)}$$
- Local Outlier Factor: average ratio of local reachability(LRD) to its nhbds.
	$$LOF_k(A)=\frac{\sum_{B \in N_k(A)} \frac{LRD_k(A)}{LRD_k(B)}}{|N_k(A)|}$$
- Points with $LOF_k(A)>1$ are considered potential outliers
##### Code
```py
import numpy as np
from sklearn.neighbors import LocalOutlierFactor
lof_model = LocalOutlierFactor(n_neighbors=20, contamination=0.1)
outliers_prediction = lof_model.fit_predict(X
outlier_indices = np.where(outliers_prediction == -1)[0]
outliers = X[outlier_indices] 
print("Outliers:", outliers)
```

#### Isolation Forests (Ensemble Technique)

##### Math

1. **Tree Construction:**
   - The algorithm builds a collection of isolation trees, which are essentially binary trees. These trees are constructed by randomly selecting a feature and a split point for each node until the data points are isolated into individual leaf nodes.

2. **Path Length Calculation:**
   - For each data point, the algorithm calculates the path length required to isolate the point in the tree. Anomalies or outliers are expected to have shorter path lengths since they require fewer splits to be isolated.
   - The average path length in an isolation tree with `n` nodes is given by `2 * (log(n-1) + 0.5772)`. The term `0.5772` is a constant derived from the harmonic number. The shorter the average path length, the more likely the point is an outlier.

3. **Scoring:**
   - The average path length across all trees is calculated for each data point. A shorter average path length indicates that the point is more likely to be an outlier.
   - The scoring for a data point is calculated by taking the average path length across all trees. The formula is `score(x) = 2^(-E(x) / c(n))`, where `E(x)` is the average path length for point `x`, and `c(n)` is a normalization factor given by `2 * (log(n-1) + 0.5772) - (2*(n-1)/n)`.

4. **Thresholding:**
   - A decision threshold is set to classify points as outliers or inliers. Points with average path lengths below the threshold are considered outliers.
   - The threshold for classifying a point as an outlier is typically set based on percentiles or a predefined contamination parameter. Points with scores below the threshold are labeled as outliers.

Isolation Forest is efficient and particularly useful for high-dimensional data. It takes advantage of the fact that outliers are less likely to follow the same patterns as normal instances, resulting in shorter paths during tree construction. The simplicity and scalability of the algorithm make it a popular choice for outlier detection tasks.
##### Code
```py
from sklearn.ensemble import IsolationForest
import numpy as np
import matplotlib.pyplot as plt
clf = IsolationForest(contamination=0.05)
clf.fit(your_data)
predictions = clf.predict(your_data)
num_outliers = np.sum(predictions == -1)
print(f"Number of outliers: {num_outliers}")
decision_values = clf.decision_function(your_data)
plt.scatter(your_data[:, 0], your_data[:, 1], c=predictions, cmap='viridis')
plt.title('Isolation Forest Outlier Detection')
plt.show()

contamination_values = [0.01, 0.05, 0.1, 0.15]
for contamination_value in contamination_values:
    clf = IsolationForest(contamination=contamination_value)
    clf.fit(your_data)
    predictions = clf.predict(your_data)
    num_outliers = np.sum(predictions == -1)
    print(f"Contamination: {contamination_value}, Number of outliers: {num_outliers}")
```

#### One-class [[SVM]]

##### Code
```py
from sklearn.svm import OneClassSVM
import numpy as np
model = OneClassSVM(nu=0.05)
model.fit(X_train)
predictions = model.predict(X_test)
```
[_class_ sklearn.svm.OneClassSVM(_*_, _kernel='rbf'_, _degree=3_, _gamma='scale'_, _coef0=0.0_, _tol=0.001_, _nu=0.5_, _shrinking=True_, _cache_size=200_, _verbose=False_, _max_iter_=-1)](https://scikit-learn.org/stable/modules/generated/sklearn.svm.OneClassSVM.html)

### Neural Networks

#### Replicator Neural Networks & Bayesian Network & [[Hidden Markov Model]]

This is not Recurrent Neural Network!

[paper link](https://togaware.com/papers/dawak02.pdf)

#### Autoencoders

##### Code
1. Prepare dataset with significant amount of normal(non-outlier) data for training
2. Design an autoencoder architecture(Encoder & Decoder).
3. Train the autoencoder with only the normal data.
4. Set the threshold from the resulting reconstruction error
5. Identify the outliers by comparing reconstruction error, threshold



```py
import torch
import torch.nn as nn
import torch.optim as optim
from torch.utils.data import DataLoader, TensorDataset

class Autoencoder(nn.Module):
	def __init__(self,input_size,hidden_size):
		super(Autoencoder,self).__init__()
		self.encoder = nn.Linear(input_size,hidden_size)
		self.decoder = nn.Linear(hidden_size,input_size)
	def foward(self,x):
		x = self.encoder(x)
		x = torch.relu(x)
		x = self.decoder(x)
		return x

normal_data = # Normal data
train_loader = DataLoader(TensorDataset(normal_data),batch_size = 8, shuffle=True)

input_size = 30
hidden_size = 4
autoencoder = Autoencoder(input_size,hidden_size)
criterion = nn.MSELoss()
optimizer = optim.Adam(autoencoder.parameters(),lr=0.01)

num_epochs = 10
for epoch in num_epochs:
	for data in train_loader:
		inputs,_ = data
		optimizer.zero_grad()
		outputs = autoencoder(inputs)
		loss = criterion(outputs,inputs)
		loss.backward()
		optimizer.step()

all_data = # Normal & potentially anomalous data
all_outputs = autoencoder(all_data)

mse_loss = nn.MSELoss(reduction='none')
reconstruction_error = torch.mean(mse_loss(all_outputs,all_data),dim=1)
threshold = torch.percentile(construction_error,95)
anomalies = all_data[reconstruction_error>threshold]
outlier_indices = torch.nonzero(reconstruction_error>threshold).squeeze()
```

#### LSTM

After work

#### Minimum Covariance Determinant

##### Math
1. Get Covariance matrix $S=\frac{1}{n-1}\sum_{i=1}^n (X_i-\bar{X})(X_i-\bar{X})^T$
2. Mahalanobis Distance Calculation: $D_i = (X_i-\bar{X})^TS^{-1}(X_i-\bar{X})$
3. Get the dataset $H$ that minimizes $det(S_H)$ 
4. Calculate the Mahalanobis distance using $S_H$: $D_i=(X_i-\bar{X}_H)^TS^{-1}(X_i-\bar{X}_H)$ 
5. Define threshold using chi-square distrbution $\chi_{p,\alpha}^2$ 

#### [[Convolutional Neural Networks]]

Used in image, video data analysis.

[paper link](https://pdf.sciencedirectassets.com/320278/1-s2.0-S2590123023X00024/1-s2.0-S2590123023001536/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEL7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCpZCvQUa8nnpCzjhc8qpNWynLVzQMdcGYSbp5GnBT5cgIhAOh7RIwLMS9yumfwBdUk1YMM2ZKeUosGsQR4hSb3menyKrMFCFcQBRoMMDU5MDAzNTQ2ODY1Igz7qwfXApvW2vcIPGwqkAWXHdXvZoWPjJi8FSBO5A%2BmAV0h7tvvdy08moWkDl1sDohIy3j4M7ljMOOjMR5JM7qyyhxPYp%2BxwBWbnu9iVFk3jkl4pk4F7LiulLLMa%2FNzqn1HZzwEcDaTgtf3HyJOnXd2cZKKq%2BXzdRrz1uhtgQNJ3MNhj2TVzQf2pLkCAg%2FFNaNnl9xOccqIzW7WVxXbRtdl8Qr1CsIp3Y4ObpIXy%2BC6JlRL53ogjbIY9tArkmIVpeW2Nd9iMen36jkGtvlpFVLgoH69fDvOQRqnGrhqCHdZD9XYp0PR5nhQEwTuzSUza%2FMhEpQtpWNIq8lYsei40I54jILU80Le%2Frb8ljeMM5%2BVq2AxBy8JiT7GFcStLaz1nxSrDtCcns%2Fzwx5yqRkJ8g0si1OdfP1lnmZLd%2FySMBGxZXy7JbLbZ%2BVmvq4ej970zyJDiVW95ydF9ZoMtopxSsU4eajSZGIm%2Bj5uAzzH3eZ5GHM1rjtBnWL3ru8xvqz1tQtTTHLp0ZZ9fA9MbbKAxjN3ZOfkIO6irBgpXR665VXJKHvez8iZx4FaSbJCCheJ%2B4Mjoh2FALYhcjhyRbyP7wHS4p%2FDUFSE98PV3kTVwKOtyFmp2UAuCySdeZfTMOZ3kk4fzXr609k2RhWKKY3br7I68Jkt18362YoOCCxFZhUcbBUhB355hHp%2FD0%2FV47JO00%2BAh2vH4S08xg2Cfp%2Bx47vO6tdPxL4N%2BoyqwKDRAQWxulay44lt7fBet7%2FTl7txbdqKtiN3xhmThTN9sLFK0QX%2BSaO%2FW8%2BHR6QPF8bTNhtTetWBw%2Bc0RvIo4ZPW9s8GK2NFVAwyV6yVxHKhxK9oFLvFYu6bPBYMNNgSCdP5oaH28qJS3etmQULJbu3DTiaBdzCd49OsBjqwAXTQij2gwt9B%2BVdvd6%2Bpgz413JkS5vElljZ9QLLVI65ob90ZmQ678KcnySDnUrtk9LQ6Ab4M%2BbJhDf4%2BiMTBbc5cRI1UTtKqFyf8JDP%2Fcg5bilFCuaZC8IlRp2p9ChkHPq1JGC2gmELB7UYH%2F%2FLAkTYz%2FmTWCe%2FPTUXXcjQUi3at6CHeT%2Ft9eRk%2BXmH1YvZM14LbSnanaca4FhFImCKnpB8S7np0JYx%2FHequf%2FIE95EF&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240103T064251Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYUETBPXGS%2F20240103%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=57faadfd3c83ed54426df5f6a4050f798edbd4cab5ace1625b661c89e25ecc73&hash=7d06f3d12db4aa7323dcc2339fa4774d7e4e849a366dd0160c27b5a7e7627a0c&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S2590123023001536&tid=spdf-1ffc2eda-3f0c-4489-9d04-7a7c98694857&sid=c8fe38cb9209714d6058a803365354259c16gxrqa&type=client&tsoh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&ua=1112585406575a51075f&rr=83f943a14a70a7d7&cc=kr)


### [Cluster](Clustering) Based

[paper link](https://www.sciencedirect.com/science/article/abs/pii/S0167865503000035)

#### Using [[Mean Shift Clustering]]

##### Code
```py
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import MeanShift, estimate_bandwith
from sklearn.datasets import make_blobs
# Create data
X,_ = make_blobs(n_samples=300, centers=4, cluster_std=1.0)
outliers = np.random.uniform(low=-10,high=10,size=(10,2))
X=np.vstack([X,outliers])
bandwith = estimate_bandwith(X,quantile=0.2,n_samples=500)
labels = ms.labels_
cluster_centers = ms.cluster_centers_
labels_unique = np.unique(labels)
n_clusters = len(labels_unique)

plt.figure(figsize=(10,6))
for k in range(n_clusters):
	my_members = labels==k
	plt.scatter(X[my_members,0], X[my_members,1],label=f'Cluster {k}')
plt.scatter(outliers[:,0], outliers[:,1], marker='x', color='red', label='Outliers')
plt.scatter(cluster_centers[:, 0], cluster_centers[:, 1], marker='o', color='black', s=200, label='Cluster Centers')
plt.title('Mean Shift Clustering for Outlier Detection')
plt.legend()
plt.show()
```

