## Predicting similarity of taste for foods given their photos (final grade 5/6)

### Challenge description:

In this task we are given a folder containing 10'000 pictures of different foods (not uploaded here for size constraints) and a training set consisting of **ordered triplets** (the dataset is divided into two equal parts of 5000 pictures: one is used for training and the other for the test). An ordered triplet might be [00002, 00034, 00018], meaning that the food in picture 00002.jpg is more similar in taste to the food in picture 00034.jpg then it is to the plate depicted in 00018.jpg. Given a triplet of the test set, our goal is to predict whether the first dish tastes more similar to the second or third one.

### Solution:

We loaded the weights pre-trained on 'imagenet' (not exclusively on food pictures) into tf.keras.applications.VGG16 neural network to the training set of images. When applied to an image, the pre-trained VGG16 returns a vector with about 350 entries corresponding to the set of possible categories (say pizza, or chair). Each entry stores the probability of the image to belong to that specific category. Furthermore, we performed **principal component analysis** (PCA) on these 350 dimensional vectors (this helped us reduce the runtime significantly). Then we exploited **unsupervised learning** thourgh **k-means** to cluster the dimensionalliy reduced vectors. In order to make predictions, we built a grid with pairs of classes (i.e. k-means clusters) as elements. In particular, consider we have again the training triplet [00002, 00034, 00018]. Also suppose that 00002 is mapped by k-means in cluster i-th, 00034 is mapped in cluster j-th and 00018 in cluster k-th, then we sum 1 to entries (i,j) and (j,i) in the grid, while we subtract 1 (i,k) and (k,i). For the predictions, we apply the same preprocessing (i.e. VGG16 regression and PCA) to test images, we then look at the (previously computed k-means) clusters they belong to and use the grids's values to measure taste similarity.

    The elements of the grid are computed using triplets, which is an array 
    containing triplets. +1 is summed in the entry of the grid corresponding
    to similar categories of each triplet element and -1 is summed when pairs
    are less similar. The grid is used to make predictions on triples_test which
    has the same structure as triplets.

We figured that most of the predictions done by setting a fixed value for the PCA components 
and the number of clusters in the Kmeans performed comparably well in cv. However this predictions are quite
different from one another. For this reason we exploited this diversity through the usage on an
averaging technique. To have many predictions we ran two for loops, over PCA dimension and number of
clusters in Kmeans. To ensure diversity of the predictions we measured distance between predictions 
and set the threshold = 20000, using cv. We then transformed the average values > 0.5 to 1 and < 0.5 to 0. 
This raised the cv score from 0.60 to 0.64.
