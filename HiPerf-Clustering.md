Hierarchical Cluster Analysis
==========================================
http://www.r-tutor.com/gpu-computing/clustering/hierarchical-cluster-analysis

With the distance matrix found in previous tutorial, we can use various techniques of cluster analysis for relationship discovery. For example, in the data set mtcars, we can run the distance matrix with hclust, and plot a dendrogram that displays a hierarchical relationship among the vehicles.

> d <- dist(as.matrix(mtcars))   # find distance matrix 
> hc <- hclust(d)                # apply hirarchical clustering 
> plot(hc)                       # plot the dendrogram
Careful inspection of the dendrogram shows that 1974 Pontiac Firebird and Camaro Z28 are classified as close relatives as expected.

<hr>

<!----------------->

Similarly, the dendrogram shows that the 1974 Honda Civic and Toyota Corolla are close to each other.

<!----------------->

In general, there are many choices of cluster analysis methodology. The hclust function in R uses the complete linkage method for hierarchical clustering by default. This particular clustering method defines the cluster distance between two clusters to be the maximum distance between their individual components. At every stage of the clustering process, the two nearest clusters are merged into a new cluster. The process is repeated until the whole data set is agglomerated into one single cluster. For a data set with 4,000 elements, it takes hclust about 2 minutes to finish the job on an AMD Phenom II X4 CPU.

<pre><code>
> test.data <- function(dim, num, seed=17) { 
+     set.seed(seed) 
+     matrix(rnorm(dim * num), nrow=num) 
+ } 
> m <- test.data(120, 4500) 
> 
> library(rpud)                  # load rpud with rpudplus 
> d <- rpuDist(m)                # Euclidean distance 
> 
> system.time(hclust(d))         # complete linkage 
   user  system elapsed 
115.765   0.087 115.914
</code></pre>
By code optimization, the rpuHclust function in rpud equipped with the rpudplus add-on performs much better. Moreover, as added bonus, the rpuHclust function creates identical cluster analysis output just like the original hclust function in R. Note that the algorithm is mostly CPU based. The memory access turns out to be too excessive for GPU computing.

> system.time(rpuHclust(d))      # rpuHclust with rpudplus 
   user  system elapsed 
  0.792   0.104   0.896
Here is a chart that compares the performance of hclust and rpuHclust with rpudplus in R:

<hr>

Exercises
Run the performance test with more vectors in higher dimensions.
Compute hierarchical clustering with other linkage methods, such as single, median, average, centroid, Ward’s and McQuitty’s.
