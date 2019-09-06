# Introduction to Data Science

### Rationale

- data is the key of machine learning, solution is only as good as the data it's built upon
- ML technique choice depends heavily on data available

### Goal of machine learning

Given a training set, find approximation of the underlying function (that maps data attributes to target values) that best generalizes, or predicts, labels for new examples.

# Types of Machine Learning

- **Supervised**
  - true label provided, model learns from feedback of labels within training data set
  - categories
    - regression: continuous numerical value
    - classification: categorical (binary or multi-class)
- **Unsupervised**
  - no target outcome/label
  - Common tasks
    - look for clusters based on relative differences of observations
    - dimensionality reduction by identifying covariant features
  - "semi-supervised" is where some items have labels and others don't
- **Reinforcement**
  - algorithm not told which answer is correct, but given reward or penalty based on performance

# Key Issues in ML

### Data Quality

- consistency
  - gathered in a consistent manner over time and locations?
  - aligned with business problem we want to solve?
- accuracy: are labels and features correct?
- noisy data: fluctuations in input/output that make it hard to see patterns
- missing data
  - many ML algorithms can't deal with missing data
  - might have to fill them in via default or mean value, otherwise drop observation
- outliers: errors, typos might need to be identified and removed
- bias: need to find and be aware of

### Model Quality

- underfitting:
  - too simple, flexible enough to model the real pattern
  - not enough predictive power
- overfitting
  - model tracks training data too closely, "memorizes" noise and attempts to extrapolate that on predictions
  - this leads to not generalizing well on new data
  - corresponds to high variance - small change in training data leads to a big change in output
  - more common problem than underfitting

# Machine Learning Methods: Linear Regression

### Linear Methods

- function form is `f(x) = Φ(w^t * x)`
  - `Φ` is activation function
  - `w^t` is weight
  - `x` is observation
- optimize by gradient descent
  - simple for one computer, everything in method
  - stochastic method with mini-batches for multi-computer distributed

### Univariate Linear Regression

- single feature and real value response
- only two parameters, `w0` (intercept) and `w1` (slope)
- best line minimizes sum of squared error
  - squared error is partially chosen since easier to compute than abs value or another function
  - also that we assume Gaussian distribution (0 centered, fixed variance, aka normal distribution/bell curve) and squaring helps react more to outliers, pulling in the line faster

### Multivariate Linear Regression

$x^2*\phi + w_0$

$f(x) = Φ(w^t * x)$

$f(x) = \phi(w^t * x)$

i
be
