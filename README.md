ClusterAnalysiswithR
====================

Cluster Analysis with Python

A very common task in data analysis is that of grouping a set of objects into subsets such that all elements within a group are more similar among them than they are to the others. The practical applications of such a procedure are many: given a medical image of a group of cells, a clustering algorithm could aid in identifying the centers of the cells; looking at the GPS data of a user’s mobile device, their more frequently visited locations within a certain radius can be revealed; for any set of unlabeled observations, clustering helps establish the existence of some sort of structure that might indicate that the data is separable.

#####Mathematical background

The k-means algorithm takes a dataset X of N points as input, together with a parameter K specifying how many clusters to create. The output is a set of K cluster centroids and a labeling of X that assigns each of the points in X to a unique cluster. All points within a cluster are closer in distance to their centroid than they are to any other centroid.
