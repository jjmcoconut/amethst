### Methodology
An object is classified by a plurality vote of its neighbors, with the object being assigned to the class most common among its _k_ nearest neighbors. k must not be a multiple of number of classes

1. For a new point find k closest points from a training data set
2. The labels of the k points vote to classify the new point

