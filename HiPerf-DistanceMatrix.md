Distance Matrix by GPU

The measure of distance is an important tool in statistical analysis. It quantifies dissimilarity between sample data for numerical computation. A popular choice of distance metric is the Euclidean distance, which is the square root of sum of squares of attribute differences. In particular, for two data points x and y with n numerical attributes, the Euclidean distance between them is:

         ┌ -----------
         ││ n∑
d(x, y) = ∘  (xi - yi)2
           i=1
For example, the data frame mtcars consists of measurements from a collection of 32 automobiles. Since there are 11 measurement attributes for each automobile, the data set can be seen as a collection of 32 sample vectors in an 11 dimensional space. To find out the dissimilarity between two automobiles, say Honda Civic and Camaro Z28, we can calculate the distance between them with the dist function:

> x <- mtcars["Honda Civic",] 
> y <- mtcars["Camaro Z28",] 
> dist(rbind(x, y)) 
           Honda Civic 
Camaro Z28      335.89
Likewise, we can compute the distance between Camaro Z28 and Pontiac Firebird:

> z <- mtcars["Pontiac Firebird",] 
> dist(rbind(y, z)) 
                 Camaro Z28 
Pontiac Firebird     86.267
As the distance between Camaro Z28 and Pontiac Firebird (86.267) is smaller than the distance between Camaro Z28 and Honda Civic (335.89), we conclude that Camaro Z28 is more similar to Pontiac Firebird than to Honda Civic.

If we apply the same distance computation between all possible pairs of automobiles in mtcars, and arrange the result into a 32x32 symmetric matrix, with the element at the i-th row and j-th column being the distance between the i-th and j-th automobiles in the the data set, we will have the so-called the distance matrix. It can be computed for mtcars as:

> dist(as.matrix(mtcars))
In general, for a data sample of size M, the distance matrix is an M × M symmetric matrix with M × (M - 1)∕2 distinct elements. Hence for a data sample of size 4,500, its distance matrix has about ten million distinct elements. Nevertheless, depending on your application, a sample of size 4,500 may still to be too small to be useful.

The following measures the time spent on finding the distance matrix for a collection of 4,500 random vectors in a 120 dimension space. On a desktop computer with AMD Phenom II X4 CPU, it takes about 14 seconds to finish.

> test.data <- function(dim, num, seed=17) { 
+     set.seed(seed) 
+     matrix(rnorm(dim * num), nrow=num) 
+ } 
> m <- test.data(120, 4500) 
> system.time(dist(m)) 
   user  system elapsed 
 14.343   0.185  14.533
Now load the rpud package, and compute the same distance matrix using the rpuDist method. For rpud running on NVIDIA GTX 460 GPU, the execution time is about 1 second. Even better, with the rpudplus add-on, you can compute distance matrices for larger data sets that fit inside the system RAM available to R.

> library(rpud)                  # load rpud with rpudplus 
> system.time(rpuDist(m)) 
   user  system elapsed 
  0.674   0.305   0.980
Here is a chart that compares the performance between the CPU and GPU.

PIC
