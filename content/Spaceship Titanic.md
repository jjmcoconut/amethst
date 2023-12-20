### Dataset Analysis

![[Pasted image 20231217142524.png]]
1. **Probability Estimation:**  
   - Estimate the probability of transportation based on the given dataset:
	   - Assign 0 for absolutely not transported
	   - Assign 1 for absolutely transported

2. **Algorithms to Consider:**  
   - Explore various algorithms for estimation, including:
	   - Random Tree Regressor
	   - Multi-linear Regression (considering correlation)
	   - Explore other potential algorithms

3. **Issues to Address:**  
   - **Null Values:** How to process missing values?
   - Does cabin information contribute to the analysis?
   - Destination information has multiple items, with most being TRAPPIST-1e, but 481 others exist.

### Missing Values

Identify four types of missing values:

1. **Structurally Missing Data:**  
   Data missing because it shouldn't exist; e.g., age of the youngest kid for a childless couple.

2. **MCAR (Missing Completely At Random):**  
   Randomly occurring missing values with no pattern; e.g., data loss due to a weighing machine running out of batteries.

3. **MAR (Missing At Random):**  
   Missing values related to other observations; e.g., predicting missing height using age, gender, and weight.

4. **NMAR (Not Missing At Random):**  
   Deliberate missing values, not random; e.g., survey participants intentionally skipping questions.

![[Pasted image 20231217150914.png|500]]
In this case it is a MCAR(Missing Completely at Random). Because by this correlation matrix, we can see that 'Transported' is not highly related to rest of the variables. - May be wrong but, For the first attempt I will assume it is a MCAR and do the process for it.

[Tang, F. Random Forest Missing Data Algorithms](https://onlinelibrary.wiley.com/doi/abs/10.1002/sam.11348?casa_token=OiJWkMrMoFwAAAAA:4THtuzmH1Q9uDcNB2J90Qx1rwArrw4IeVXuEHDrivOwKVm3YDhbq_l0nK71iLxnYjq7Pgey-joyuhRIP) 
This paper analyzed which kind of strategy was best for each case. I may as well read it.

1. First Attempt - [[KNNImpute]]
	By using KNNImpute we fill the missing values by using KNN.
	But the problem is that it only fill values when it is numerical not categorical. Therefore we need to change all string values into numbers.
	We do that by using LabelIncoder(in sklearn.processing)
```py
	label_encoder = LabelEncoder()
	df_encoded = df.apply(lambda series: pd.Series(
		label_encoder.fit_transform(series[series.notnull()]),
		index=series[series.notnull()].index
	))
```
This converts all string values into integers.
Also there is a way to restore it back to its original value after KNNImpute. However in this project we do not need to do it. 

After that we use KNNImpute
```py
imputer = KNNImputer(n_neighbors=1)
df_imputed = pd.DataFrame(imputer.fit_transform(df_encoded), columns=df.columns)
```
(Still finding the optimum n_neighbors)
-> Found out that these parameters does not matter. The best result from tuning parameters returned a worse percentage than the first one.