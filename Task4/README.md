## Predicting similarity of taste for foods given their photos. Final grade 5/6

# Challenge description:

In this task we are given a folder containing 10000 pictures of different foods (not uploaded here for size constraints) and a training set consisting of **ordered triplets** (the training triplets contain names of only to the first 5000 pictures, the other 5000 are instead appearing in the test, so that when our algorithm will be tested, it will work on pictures that it has never seen before). An ordered triplet might be: 00002, 00034, 00018 meaning that the food in picture 00002.jpg is more similar in taste to the food in picture 00034.jpg then it is to the plate depicted in 00018.jpg. Our aim is, given a test set file containing unordered triplets, to find which food in the second and third entry is the most similar to the food in the first entry.

# Solution:

We applied the already trained (not exclusively on foods) Res-net neural network to the training set of images. When applied to an image, Res-net, returns a vecotor with about 350 entries. Each entry corresponds to a category (say pizza, or chair) and is filled with the probability of the image to belong to that specific category.
