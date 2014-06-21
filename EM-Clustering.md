The EM Algorithm
====================================================
The EM algorithm for clustering is described in detail in Witten and Frank (2001). 
The basic approach and logic of this clustering method is as follows: 
- Suppose you measure a single continuous variable in a large sample of observations. 
- Further, suppose that the sample consists of two clusters of observations with different means (and perhaps different standard deviations); within each sample, the distribution of values for the continuous variable follows the normal distribution. 

<hr>
### Categorical variables. 
The EM algorithm can also accommodate categorical variables. The method will at first randomly assign different probabilities (weights, to be precise) to each class or category, for each cluster. In successive iterations, these probabilities are refined (adjusted) to maximize the likelihood of the data given the specified number of clusters.

### Classification probabilities instead of classifications. 
The results of EM clustering are different from those computed by k-means clustering. The latter will assign observations to clusters to maximize the distances between clusters. 
The EM algorithm does not compute actual assignments of observations to clusters, but classification probabilities. In other words, each observation belongs to each cluster with a certain probability. Of course, as a final result you can usually review an actual assignment of observations to clusters, based on the (largest) classification probability.
