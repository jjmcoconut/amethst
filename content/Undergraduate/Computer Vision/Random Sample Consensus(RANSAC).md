### Assumptions
- Majority of good samples agree with the expected model
- Bad samples does not consistently agree with a single model(bad samples make different results)

### While improvement > threshold
1. Choose small subset of points uniformly at random
2. **Fit** a model to subset
3. Find all remaining points close to model and reject the rest as outlier
4. If consensus set size is greater than d, accept the line, and **refit** using all inliers.
We fit the model twice in one iteration

### Parameters
1. Initial number of points **s**
2. Distance threshold **t**
3. Number of sample iterations **N**

### Pros and Cons
**1. Pros**
	 - Simple & General
	 - Applicable to many problems
**2. Cons**
	 - Lots of parameter (s,t,N)
	 - Low inlier ratio -> does not work well

