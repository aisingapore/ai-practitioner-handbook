# Potential scenarios of bias, unfairness, data leakage in data splits and suggestions to remedy

Contributor(s): Lee Xin Jie, Senior AI Engineer (100E)


## Potential scenarios of bias and unfairness in data splits and suggestions to remedy

Having biases in datasets may lead to unfairness in our models. We want to ensure that model predictions are fair for different groups of users and scenarios.

There are 2 sources of such bias and unfairness:
- i) The full dataset is skewed to certain subgroups (eg. we are training a model to predict voting behaviour in Singapore but the dataset contains 95% Chinese).
- ii) The splitting of the full dataset into train, validation and test sets introduces skewness (eg. the train set contains 30% aged above 60 while the validation set contains 15% aged above 60).

This article discusses point ii).

*Point i) is related to ensuring a representative dataset is curated at the start of the project, and this is partly discussed in [What are the key areas to look out for in the data when framing the AI project?](../1-pre-project-phase/key_areas_in_data.md).*

Certain problems are inherently imbalanced. For example, fraud detection datasets usually have fewer fraudulent examples than normal examples. In such a scenario, you should favour a stratified data split over a random split to ensure that there are equal proportions of fraudulent to normal examples in each data split. You will want to avoid a situation where your train set is predominantly normal, and your development set has a higher proportion of fraudulent data than in reality.

When dealing with datasets involving geographical and demographical slices, you may also want to consider stratified data split to ensure that each split contains a balanced set of examples across geographical and demographical attributes. This will help reduce any potential unfairness in model predictions between users from different geographical and demographical slices.


## Potential scenarios of data leakage in data splits and suggestions to remedy

Data leakage is the scenario where during training, the model has access to information that will not be available during production. Often, if your model performs surprisingly well on the validation/test set (e.g. 100% test set performance), you should perform a check for data leakages. Data leakages should be avoided, as they allow the model to leverage on leaked information during training and achieve inflated performance on the validation/test set.

A common example of data leakage is **temporal data leakage**, which may occur when you are building a model to forecast future events based on past events. For example, you are building a model to predict the price of a stock in future, and you have past daily data of the stock’s prices. If you perform a random data split, it is likely that the train set may contain future stock prices, while the test set may contain past stock prices. This will allow the model to leverage on future stock prices it encounters during training to predict past prices on the test set, thereby inflating the model’s performance. 

In temporal problems involving high correlations between successive times, you should also aim to group successive days together in the same data split to minimise data leakage.

Datasets with **duplicated data points** are also likely to cause data leakages. If a random data split is adopted, you may have the same data points in both the train and test set. This will result in inflated test performance.

Datasets with **near duplicates** can also subtly introduce data leakage. One example will be in computer vision, where it is possible to have multiple images that are near duplicates but not perfect duplicates. This can easily occur when the data comes from video streams made up of continuous sequences of images. For example, if you are training a model to classify car models, you may have images of the exact same car taken 1 second apart. In this case the images are likely to have very similar characteristics. If you split the dataset randomly, you are likely to split these images into each of the train, validation and test set. Your model will then likely evaluate well on the images assigned to the test set, since it has already encountered similar images during training. In this scenario, you should consider a stratified splitting of your dataset, where images of the same car should be assigned to a single dataset split. You could use timestamps or image hashing to achieve this.

When **engineering features**, ensure that you do not inject data leakage during the process. If you are building a model to predict how many items a user will purchase at a store on a particular day, you will want to only engineer features that are available during inference in production. Examples of features leveraging information that won’t be available are the number of items sold in the store during the same day, or a moving average of the number of items purchased by the user up to and including the day itself, etc.

Having a **repeatable data split algorithm** is important to avoid introducing unforeseen data leakages during model retraining. Imagine the scenario where an unrepeatable random data split algorithm is adopted. When you have new datasets, you will likely generate new data splits and trigger model retraining. After retraining, you will often have to compare the performance of the old model vs the new model, to choose which model to deploy. An unrepeatable data split algorithm may mean that some of the old training data may fall into the new validation dataset. Hence, your old model may appear to perform better on the new validation dataset and you will deploy that model. However you may soon realise that the actual model performance in production is lower after deployment.


## References

- [Building Machine Learning Powered Applications: Going from Idea to Product](https://www.oreilly.com/library/view/building-machine-learning/9781492045106/)
- [Machine Learning Design Patterns: Solutions to Common Challenges in Data Preparation, Model Building, and MLOps](https://www.oreilly.com/library/view/machine-learning-design/9781098115777/)