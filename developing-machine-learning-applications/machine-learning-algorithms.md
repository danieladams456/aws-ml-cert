# Machine Learning Algorithms Explained

## Supervised Learning

### Linear Supervised Algorithms

- **Logistic regression**
  - linear decision boundary (hyperplane) that separates classes
  - build a linear combination of features that gives a real number result
  - "logistic curve" maps that real number to the range (0,1)
    - less than 0.5 is class A, greater is class B
  - Sagemaker has an algorithm [linear learner](https://docs.aws.amazon.com/sagemaker/latest/dg/linear-learner.html) which does both linear + logistic regression
- **SVM**
  - find a hyperplane with maximum boundary between classes
  - kernel functions can let it apply to non-linearly separable boundaries

### Non-Linear Supervised Algorithms

- **Decision tree[s]**
  - can be flexible for non-linear relationships
  - variants with boosting (different trees work on different cases) or bagging (all trees vote) are common
  - Sagemaker includes [XGBoost](https://docs.aws.amazon.com/sagemaker/latest/dg/xgboost.html)
- **Factorization machines**
  - good for high dimensionality sparse data sets
  - click prediction and item recommendation
  - [Sagemaker algorithm](https://docs.aws.amazon.com/sagemaker/latest/dg/fact-machines.html)

## Unsupervised Learning

- **Clustering**
  - one difficulty is knowing how many clusters to predict
    - generally a hyperparameter not derived from the model data
    - generally up to humans to interpret results and ascribe meaning
  - [k-means](https://docs.aws.amazon.com/sagemaker/latest/dg/k-means.html)
- **Anomaly detection**
  - [random cut forest](https://docs.aws.amazon.com/sagemaker/latest/dg/randomcutforest.html)
    - also available in Kinesis data analytics
- **Topic modeling**
  - [neural topic modeling](https://docs.aws.amazon.com/sagemaker/latest/dg/ntm.html)
  - [latent dirichlet allocation (LDA)](https://docs.aws.amazon.com/sagemaker/latest/dg/lda.html)
    - variant used in Comprehend service
- **Dimensionality reduction**
  - [principal component analysis](https://docs.aws.amazon.com/sagemaker/latest/dg/pca.html)
  - feature engineering step before passing data to supervised algorithm

## Deep Learning

- stages
  - data sample is a vector of values
  - linearly combined with weights
  - run through an activation function to give an output
  - one layer of this is a perceptron and can do binary classification, but generally will use multiple fully connected layers
- training
  - feed forward pass does calculation on a data point using weights and biases
  - back propagation reduces the error between output and real label by adjusting weights and biases
- deep learning now can have
  - 1000 layers,
  - billions of parameters,
  - trained on millions of images
- convolutional neural network (CNN)
  - able to relate nearby pixels instead of just treating them independently
  - layers of convolutions can learn patterns of increasing complexity
  - uses:
    - object detection/image classification
    - semantic segmentation (outline something in the picture)
    - artistic style transfer
    - generate photos (deep-fakes)
- recurrent neural network (RNN)
  - "memory" of previous state
  - can be used for time series forecasting and speech recognition/translation
