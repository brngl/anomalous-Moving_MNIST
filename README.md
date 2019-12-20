# Anomalous Moving MNIST

This is an Anomalous Moving MNIST dataset generator. The dataset will contain Moving MNIST sequences with anomalies. It is built
starting from MNIST dataset.

### Moving MNIST
Moving MNIST contains 10,000 sequences each of length 20 showing 2 digits moving in a 64 x 64 frame.
http://www.cs.toronto.edu/~nitish/unsupervised_video/

### MNIST
The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.
http://yann.lecun.com/exdb/mnist/

## Anomalies
Anomalies are substitution of one or two of the digits of a frame (or more than one frame) with other similar digits.
The substituted digits are visibly similar but don't share the same label (value).
<div align=center><img width="180" height="90" src="https://github.com/brngl/images/blob/master/simili37.png"/></div>

## Procedure
We start from MNIST dataset containing 28x28 images of handwritten digits. We aim to determine when two images are similar.

1. We perform dimensionality reduction to obtain a 2-dimensional embedding, using **t-distributed stochastic neighbor embedding (t-SNE)**
algorithm. This algorithm tries to keep similar instances close and dissimilar instances apart.
<div align=center><img width="640" height="640" src="https://github.com/brngl/images/blob/master/bokeh_plot.png"/></div>

2. Then, we perfrom **K-Means** clustering
algorithm to take the instances of our interest. 
Choosing the number of clusters is a critical issue:
* **too few** clusters imply big sized groups, increasing the dissimilarity between instances.
* **too many** clusters imply small sized groups, decreasing the variety of instances.
<div align=center><img width="640" height="640" src="https://github.com/brngl/images/blob/master/bokeh_plot-kmeans.png"/></div>

3. Afterward, we take medoids as most significative digits to create non-anomalous frames of a sequence. Anomalous frames are 
obtained replacing medoids with random instances of their respective clusters.
<div align=center><img width="1920" height="68" src="https://github.com/brngl/images/blob/master/sim1.png"/></div>
