Fuzzy Clustering
================================

We have so far worked with classiﬁcation methods which implicitly assume that there are distinct classes. The World is not made like that. If there are classes,
they are vague and have intermediate and untypical cases. With one word, they are fuzzy.

Fuzzy classiﬁcation means that each observation has a certain probability of belonging to a class. In the crisp case, it has probability 1 of belonging to one
class, and probability 0 of belonging to any other class. In a fuzzy case, it has probability < 1 for the best class, and probabilities > 0 for several other classes
(and the sum of these probabilities is 1).

Fuzzy classiﬁcation is similar to K-means clustering in ﬁnding the optimal classiﬁcation for a given number of classes, but the produced classiﬁcation is
fuzzy: the result is a probability proﬁle of class membership. The fuzzy clustering is provided by function fanny in package cluster.

Fuzzy clustering defaults to Euclidean metric, but current versions can accept
any dissimilarities. In the following, we also need to use lower “membership exponent” (memb.exp): the default 2 gives complete fuzziness and fails here, and
lower values give crisper classiﬁcations.
<pre><code>
R> library(cluster)
R> cfuz <- fanny(d, 3, memb.exp=1.7)
</code></pre>
The function returns an object with the following items:
<pre><code>
R> names(cfuz)
</code></pre>
Here membership is the probability proﬁle of belonging to a certain class, and
clustering is the most likely crisp classiﬁcation.

- http://cc.oulu.fi/~jarioksa/opetus/metodi/sessio3.pdf
