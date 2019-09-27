# Data Processing and Feature Engineering

## Encoding Categorical Variables

Categorical attribute (discrete) takes a finite set of values

- pandas dtype `category`
- issue: the machine learning algorithm must work on numbers
  - binary takes values of 1 or 0
  - more values is more complicated

Types of categorical variables

- ordinal: categories are ordered
  - i.e. small, medium, large
  - can be encoded as numbers by relative magnitude
  - `{'N':0, 'S':5, 'M':10, 'L':20}` and use pandas `.map(dict)` function
  - hardest problem is coming up with the best mapping, needs business intuition
- nominal: categories are unordered
  - i.e. red, green, blue
  - don't just map to sequence of integers magnitude is meaningless
  - OneHotEncoding: explode nominal attributes into binary attributes
    - is_red, is_blue, is_green
    - pandas `get_dummies(df)`
  - encoding with many classes
    - you might have too many features for your number of observations with OneHotEncoding
    - create hierarchical structure (state, then zip code)
    - group similar classes (stages into regions)

## Handling Missing Values

- common in real life data sets
- most ML algorithms can't deal with missing values automatically
- pandas
  - `df.is_null().sum()` by column and `df.is_null().sum(axis=1)` by row
  - `df.dropna()` drops all rows with nulls, more complex rules available like subset of cols or threshold
- risks
  - besides loosing training data, dropping rows can cause **bias** towards the subset that can complete all features
  - dropping columns can result in underfitting since you are throwing away features
- questions to ask before dropping/imputing missing values
  - are they missing at random, or is there a pattern/mechanism behind **why** they are missing?
    - if random can be imputed
    - is it because new features were added partway through data collection?
  - are there rows or columns missing that you are not expecting? might have to go back to the data source
- imputation
  - mean, median, most frequent (for categorical)
  - method for estimating value

## Feature Engineering

- create new features from existing features that have a better prediction power for the problem at hand
- often more art than science, may be domain specific
- rules of thumb
  - use intuition. What would a **human** use to predict this?
  - generate lots of features first, then use dimensionality reduction
  - don't overthink or use too much manual if/else logic (too difficult to maintain)
- examples
  - nonlinear transformations like square, square root, log
  - combinations like `x * y` to capture interactions

### Filtering and Scaling

- filtering examples
  - remove channels from image if color isn't important
  - remove frequencies from audio if power is less than a threshold (noise)
- scaling
  - motivation
    - some algorithms (KNN, gradient descent) are sensitive to different scales between features
    - some are not though, like decision trees and random forests
  - example: house bedrooms 1-4, price 200k-1M
  - calculated on training data only, then final transformation applied to test data/live predictions
  - options
    - MeanVariance: subtract mean and divide by standard deviation
      - results in mean 0, std dev 1
      - keeps outliers but reduces impact
    - MinMax: scale values so min is 0 and max 1
      - robust for small standard deviations
      - more sensitive to outliers
    - MaxAbs: divide by max abs value, don't shift
    - Robust scaling: based on median, 25th, and 75th quantiles
      - works well for ignoring outliers
- normalizing: row based and not column based
  - used in text analysis

### Transformation

- sometimes a polynomial relationship with features is a better fit - do quadratic transformation up front, then ML algorithm can be linear
- `sklearn PolynomialFeatures`
  - creates a^2, ab, b^2, etc and adds as new features
- if you have polynomial features in your final model, check for overfitting
  - it might fit the train data, but if it tries to predict data in the range it hasn't seen, it will likely peel off in an incorrect direction
- non-polynomial features available like `log` and `sigmoid`, radial functions used in support vector machines algorithms
- text based features
  - "bag of words" model most common: doesn't keep track of order of words
  - Inverse Document Frequency can be used to filter out common words like "the"
