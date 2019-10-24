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

## Model Training: Validation Set

- features, model selection, and hyperparameter tuning are an iterative process
- tuning goals
  - detect if overfitting or underfitting
  - find any special cases where the model gives inaccurate results
- **Testing Data != Validation Data**
  - training data + testing data = whole
  - training data further split down into training set and validation set
    - your iterative model selection and model tuning target improvements in the validation set
    - this can lead to overfitting towards the validation set
    - keeping the testing data until the very end and using it only once lets you test true generalization of the model
  - problems
    - in small data sets, your validation data set might be too small to be representative, or your training data set might be too small to train on
    - solution
      - use [cross-validation](https://towardsdatascience.com/cross-validation-in-machine-learning-72924a69872f) ("k-fold" and "holdout method")
      - separate training data into chunks (just say 5 of 20%). One chunk is the validation data set, but try 5x and use a different one each time

![train, validate, test data sets](pictures/train-validate-test-data-sets.png)

## Model Tuning: Bias Variance Tradeoff

- [Towards Data Science](https://towardsdatascience.com) articles
  - [Regularization](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a)
  - [Balancing Bias and Variance](https://towardsdatascience.com/balancing-bias-and-variance-to-control-errors-in-machine-learning-16ced95724db)
  - [Cross-Validation](https://towardsdatascience.com/cross-validation-in-machine-learning-72924a69872f)
- definitions
  - total error (x) = bias^2 + variance + irreducible error
  - bias: "systematic different between true model and estimated model"
  - variance: "given a data point, what is the range of response I would get back from the model"
- results
  - high bias: indication of under-fitting since the model isn't lining up with the real values
  - high variance: indication of over-fitting since small change in input leads to a large change in output
- "total test error"
  - variance + bias ^2
  - want to minimize this

![total test error](pictures/bias-variance-tradeoff.png)

- using learning curves to evaluate the model
  - detect if model is under or over fitting
  - also can show the impact of training data size to see if you can train in smaller batches or need more data (when convergence slows down)

![learning curves](pictures/learning-curves.png)

## Model Tuning: Error Analysis

- types
  - classification: easy to use confusion matrix to look at which ones went wrong and in what ways
  - regression: need to analyze residuals (difference between actual and predicted), look at outliers, which direction it is wrong more often, etc
- common problems
  - data problems (standardize variants of a word)
  - labeling errors
  - under or over-representation of a class

## Model Tuning: Regularization

- motivation
  - lots of features make it into the models, leads to overfitting
  - regularization: add penalty score into the const function for complexity
- types
  - can calculate penalty by the sum of the absolute value weights of each feature
    - **important**: each variable must be scaled to the same scale, i.e. 0-1. This makes the weights be on an even playing field
  - cost function combines MSE (mean squared error) and the penalty term
  - linear regression example:
    - L1 = abs value of weight, can be used to drop out terms
    - L2 = square of weight, generally don't drop out, but will decrease weight of unimportant terms
  - regularization strength `alpha` adjusts the weight between MSE and the regularization penalty
