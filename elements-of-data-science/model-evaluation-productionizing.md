# Model Evaluation and Productionizing

- business metrics and model metrics
- addressing overfitting
- things to consider when pushing to production
- model monitoring/maintenance

## Using ML Models in Production

- where to place in production environment (latency impact, code changes in apps to call it)
- maintenance issues
  - what happens if some features are unavailable at a given time
  - versioning of both features and model
- types of production environments
  - batch prediction
    - trained offline based on DB/data warehouse/data lake
    - predictions in report or in real-time via lookup
    - update predictions once a day/week/quarter
  - online prediction
    - training done offline
    - inference real-time
    - generally has a latency requirement, i.e. 100ms
  - online training
    - fast changing patterns like fraud detection

## Model Evaluation Metrics

- business metrics: related to revenue, profit, reduced costs
- analytical metrics: mean squared error
- confusion matrix (example will be simple binary)
  - counts of outcome vs actual class of test data
  - N by N matrix, diagonal are true categorizations
- metrics
  - **Accuracy** = `TP+TN / TP+TN+FP+FN` (true predictions over all predictions)
    - In many cases, true negatives dwarf other categories, making accuracy useless
  - **Precision** = `TP / TP+FP` (proportion of positive predictions that are actually correct)
  - **Recall** = `TP / TP+FN` (proportion of positive sets that are identified as positive)
  - **F1 Score** = `(2 * Precision * Recall) / (Precision + Recall)` (Combination of precision and recall, single metric for talking about a model)
- deciding which metric to use
  - choose the one that is most relevant to the business problem
  - are you more ok with false positives or false negatives or middle of the road

## Cross Validation

- in training, the model learns the noise, need to keep that down to a minimum
- if you have a large data set, you can use a validation set (subset of training set) to iterate on your model
  - iterating on test data of train/test split lets the model "learn" through human model decisions rather than having it be a completely objective
  - for smaller data sets where you want to use all your training data, there are other cross validation methods
- K fold cross-validation
  - issues solved
    - small data sets don't have enough data for training
    - a small unrepresentative test set will give invalid metrics
  - how it works
    - partition data into K "folds"
    - walk through all segments using that one as test and all others as training
    - large K: more time, more variance since using larger chunks and can memorize more
    - small K: more bias since using smaller chunks set to train and can memorize less
    - K between 5-10 is typical
- leave-one-out cross validation
  - K = number of data points
  - only used for tiny data sets where every data point is valuable
- stratified K fold cross-validation
  - preserve class proportions in the folds
  - helpful for imbalanced data so you don't get a fold with all of the one class that could mess up the model
  - or where there is seasonality or subgroups

## Metrics for Linear Regression

- mean squared error, `R^2`, and confidence interval
  - confusion matrix doesn't make sense for continuous variables
- mean squared error (MSE)
  - difference between actual and prediction, squared, mean
  - very commonly used
- `R^2`
  - explains the fraction of variance explained by the model (vs noise)
  - threshold is wide by type of problem (60% to 85%)
  - **warning!** R^2 always increases as more variables are added
    - higher R^2 doesn't always mean better model, have to balance overfitting
    - _adjusted R^2_ takes additional variables into account
- Normal Distribution
  - variance is average(square(observation - mean of data set))
  - standard deviation is square root of variance
  - 1 std dev contains 68% of observations, 2 contains 95%, 3 99.7%
    - useful for creating confidence intervals
  - [Central Limit Theorem](https://youtu.be/JNm3M9cqWyc)
    - as sample size goes up, average over the sample will approach the mean of any distribution
    - plot the frequency graph of many samples at that size, and the result is a normal distribution
    - as the sample size goes up (1000 observations of the mean of sample size 4 vs 1000 observations of the mean of sample size 8), standard deviation shrinks
- confidence interval
  - quantifies margin of error between prediction and true metric due to sampling randomness
  - [if true distribution is as stated], there is `x`% confidence that the metric lies within the interval
  - Z-score: the confidence interval (commonly .90 .95 .98 .99) translated into standard deviations
  - there exists formula for confidence interval of a proportion (80% of our users will do this)

## ML Models in Production

- deploy to production
  - A/B testing can help with both model validation as well as technical issues
  - [Martin Zinkevich Rules of Machine Learning](https://developers.google.com/machine-learning/guides/rules-of-ml)
- consider information security issues at the beginning of the project
  - model should be at the same classification level as the data it is derived from
- monitoring and maintenance
  - data availability can change over time (external training data sets, features)
  - software environment may change (python versions/packages)
  - high profile special cases may fail (i.e. Black Friday)
  - can be change in business goals (false positive vs false negative tolerance)
- performance deterioration
  - always be on the lookout for performance decreases so you can adjust
  - your validation/test data sets may need to be replaced over time as things change (new trends in business domain, mix of population)
  - if business problem change is big enough, it might require feature selection or algorithm change

## ML on AWS

- Sagemaker
  - full lifecycle build/train/deploy
  - managed notebook hosting
  - contains optimized models
- AWS pre-trained services
  - Amazon Rekognition image and video (trained on Amazon Prime Photos billions of images daily)
    - can still fine-tune for your specific application
  - Lex for speech recognition and language understanding
  - Polly for text to speech
  - Comprehend for text classification
  - Translate for language translation
- Other ecosystem
  - AWS Glue ETL
  - [DSSTNE](https://github.com/amzn/amazon-dsstne) for help training deep neural networks

## Common ML Mistakes

- you solved the wrong problem!
  - can be hard to map original business objective into ML problem
  - requires a lot of interaction between data science and business team
- data was flawed
  - quality not good enough
  - not the right data
  - big data != good data
- production performance doesn't match prototype
- takes too long to fail
  - data scientist has to be honest to leadership and say if a specific ML project is not going to work
  - earlier you stop a failing project the better
- don't use too complicated of a model
  - if two models give similar results, go for the simpler model
