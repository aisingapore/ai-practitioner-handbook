# What are the various data split strategies?

Contributor(s): Lee Xin Jie


## 1. Static Train Test Split
The most common train test split strategy is to create static training, validation and test data sets.

### Train Set
The train set is the subset of the data that will be used to train the ML model. The model’s performance on the train set will only provide an indication of how well the model will perform on previously seen data.

### Validation Set
The validation set, also commonly referred to as the development set, consists of data that is unseen during model training. It provides an estimation of the model’s performance during production.  The validation set is often used during model hyperparameter tuning and algorithm selection. When performing algorithm selection, it is important to ensure that the validation set used is the same across all algorithms to ensure a fair comparison.

### Test Set
The test set is the second hold-out set that will not be used during training. Since the validation set is commonly used to influence the modelling decisions, our ML model pipeline is likely to be biassed in performing well on the validation set. Hence, we will need a completely unseen set of data to provide a final benchmark of our model’s performance on unseen data. It is important to not use this test set to influence your modelling decision. Otherwise you will get an inflated sense of how well the model will perform in real life. You should only evaluate your model on the test set during the final step of the pipeline. As such, it is common for the train set performance to be higher than the validation performance, which in turn, should be higher than the test performance.

### Split Ratio
There is no single ‘golden’ data splitting proportion. In general, the larger your dataset, the lower the proportion of data you have to set aside for the validation and test sets. If you have a dataset with a billion data points, you could theoretically set aside 1% of the data for the test set, and still have a sufficiently large test set of 10 million data points. Vice-versa, the smaller your dataset, the larger the proportion of data that should be set aside for your validation and test sets. This will allow you to have a more confident estimation of model performance during production, as your model’s performance will be determined on a larger and more diverse validation/test set. 

One commonly used rule of thumb will be to adopt a 70-20-10 split for your train, validation and test sets respectively. Ultimately, you should prioritise selecting a ratio catered to your needs.


## 2. Cross Validation
A single, static validation set could potentially present a biassed assessment of model performance. This is particularly the case with smaller datasets where favourable validation performance may arise by chance. Cross-validation is an alternative to having a static validation set. In cross-validation, you will conduct multiple rounds of model training, each time with a different section of your dataset serving as the validation set. This will minimise the variance associated with choosing any particular choice of validation set. However, cross-validation does come with the penalty of additional training time. So it is usually recommended when you are dealing with a smaller dataset.


## 3. Stratified Split
For datasets with unbalanced distribution of targets and/or features, you may want to consider stratified splitting. Stratified splitting aims to split your dataset, while maintaining similar proportions of any desired features/targets across your train, validation and test sets. 

An example of a dataset with features that are skewed in their distribution will be a credit worthiness classification problem, where you may have fewer individuals in the dataset with ages of less than 20 years old.  If it is critical to model the behaviour of this age group, you can stratify the dataset based on age buckets.

An example of a dataset with imbalanced targets will be a fraud detection dataset, where fraudulent examples are typically the minority. In this case, you will stratify the dataset based on the target.

In general, the larger the dataset, the less likely features and targets will be unevenly distributed. You should still check your dataset for any uneven distribution in features and targets.


## 4. Temporal Split
When you are dealing with problems related to forecasting future values, you may want to consider temporal splitting. As an example, assume you have data from January to April. You may want to set aside data from January to February for your training dataset, March for your validation dataset, and April for your test dataset.

In fast moving environments such as fraud detection and cyber attack classification, bad actors might develop new fraud and cyber attacks techniques. It may be necessary to continuously train the model on the latest data to predict future frauds and cyber attacks, even though the task does not involve forecasting. Evaluating the model on historical frauds and attacks may be insufficient. Hence, you may choose to consider temporal splitting in this scenario.

In scenarios where there are high correlations between successive times, such as in weather forecasting, you will also want to consider temporal splits and avoid placing February 1 in the training set and February 2 in the validation set to minimise data leakage.

For seasonal data, you may want to take seasonality into account when performing temporal splits. As an example, you can place the first 20 days of every month into the training set, the next 5 days into the validation set, and the last 5 days in the test set.


## References

- Building Machine Learning Powered Applications: Going from Idea to Product
- Machine Learning Design Patterns: Solutions to Common Challenges in Data Preparation, Model Building, and MLOps
- Machine Leaning Yearning: Technical Strategy for AI Engineers, In the Era of Deep Learning