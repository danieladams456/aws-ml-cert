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

- underfitting: too generic, not enough predictive power
- overfitting
  - model tracks training data too closely, "memorizes" noise and attempts to extrapolate that on predictions
  - this leads to not generalizing well on new data
  - more common problem than underfitting
