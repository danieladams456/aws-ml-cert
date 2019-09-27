# Model Training, Tuning, and Debugging

## Neural Networks

- Perceptron
  - simplest neural network
  - list of input features
- Neural networks
  - input layer, output layer, and hidden layers
  - hard to interpret
  - generally expensive to train, fast to predict
- Convolutional neural network (CNN)
  - convolutions are filters, feed into next layer
  - pooling takes 4x4 matrix to single scalar by either max or average
  - alternate convolution + pooling?
  - once done with convolutions/pooling, feeds into fully connected layers
- Recurrent neural network (RNN)
  - has feedback to previous layers to model order of observations

## K Nearest Neighbors (KNN)

- calculate response of a new observation based on how close it is to the training data set
- need to define distance between observations
  - [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance)
  - [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry)
  - any vector norm
- find the `k` nearest neighbors to the new observation we want to classify
  - `k`=6, class `a`=3, class `b`=2, class `c`=1 -> observation classified as `a`
  - commonly use `k = sqrt(N)/2`
    - smaller `k`: more local
    - larger `k`: more generic
- non-parametric
  - did not create any functions or create any models
  - has to remember all training data for inference
  - space and prediction time complexity grows with size of training data
  - the more dimensions, the more sparse your data gets
    - single factor 0 to 1 with 100 points is the same as three factors with 100^3 = 1,000,000 data points

## Linear and Non-Linear Support Vector Machines

- uses linear separability (if you plot the observations on N dimensions and draw a line between them)
- finds optimal hyperplane to maximize margins from support vectors (training examples close to the boundary)
- nonlinear SVM
  - choose a distance function named a "kernel"
  - use that function to map into a higher dimension space
  - now can use linear SVM in the new space
- not memory efficient since stores support vectors

## Decision Trees and Random Forest

- benefits
  - automatically picks features and tunes thresholds
  - easy to interpret
  - less need for transformation
- cautions
  - potential for overfitting, need to prune
- entropy: relative measure of disorder in data source
  - disorder is present when distinction between two or more observable groups (targets) is not pure
    - 50 customers approved, 50 rejected in same group
  - as you sub-divide data, you get to more pure (20 approved, 1 rejected)
- methodology
  - nodes are split based on the feature that has the largest information gain (IG) between parent and split nodes
  - one method to quantify IG is comparing entropy before and after splitting
  - You could go all the way until response is pure with one class, but generally stops at a certain criteria to prevent overfitting
- Ensemble method/Random forest
  - randomly select subset of training data (both observations and features) to create multiple trees
  - use majority voting to pick label
  - more expensive to train since training potentially 100s of trees
