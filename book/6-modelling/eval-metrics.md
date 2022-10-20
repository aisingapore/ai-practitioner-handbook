# What are the considerations (internally by the team), and externally (by the stakeholders) when selecting evaluation metrics?

Contributor(s): Er YuYang

This guide assumes that you have a fair understanding of why the stakeholders is developing the AI/ML project (understand the business value), and have a reasonable understanding for the implementation difficulty of the evaluation for given the dataset.

# Overview

1. Understanding stakeholder's problem and environment 

2. Optimizing metrics

   a. Selecting metrics for classification problems

   b. Selecting metrics for regression problems

3. Satisficing metrics

# 1. Understanding the problem and environment 

a. Problem statement

   Understanding how the AI/ML solves the problem statement help to identify the correct optimizing metrics (explained in section 2) to determine the preformance of the model.

b. Technical competence of the different stakeholders
   
   Understanding the level of competence of the stakeholder help to identify which optimizing metrics (explained in section 2) to use when communicating with them.

c. Deployment environment

   Understanding the deployment enviornment will helps in choosing the satisficing metrics explained in section 3.

# 2. Optimizing metrics

The goal is to establish a single-number evaluation metric, as having multiple evaluation metrics make it hard to compare against different algorithms.

For instance, Classifier A has precision of 95% with recall of 90% and Classifier B has precision of 98% with recall of 85%, Neither classifier is obviously superior and does not immediately guide you towards picking one.

When comparing with different model in classification problem with multiple class, combined metrics of each class into single metric using average on weighted average. However, keep the metrics separated if you are evaluating the class performance instead of the model performance.


## a.) Selecting metrics for classification problems
This section covers some of the most common metrics used for evaluating model for classification problems. Do note that this is not exhaustive list but covers the some of common high level metrics that are useful when communicating with stakeholders.

1. Accuracy = $\frac{TP + TN}{TP + FP + TN + FN}$
   
   Simple for explaining to stakeholders but not suitable if the dataset is unbalanced.

2. Precision = $\frac{TP}{TP+FP}$

   Simplified explaination: Out of the <u>positive predictions</u>, how many are correct. It focuses on finding positive cases.

3. Recall = $\frac{TP}{TP+FN}$

   Simplified explaination: Out of the <u>actual positive</u>, how many are correct. It focuses on weeding out the negative cases.

4. F1 Score = 2 * $\frac{Precision * Recall}{Precision + Recall}$
   
   F1 score is the weighted mean of precision and recall

Precision is more important than recall when you cannot afford to have any FP as compare to FN. Often associate with cost, when cost of acting is high but the cost of not acting is low, then precision is preferred. Recall is more important than precision whe you cannot afford to have any FN as compare to FP. It is more important when the opportunity cost of passing up is high. 

Example: Missing out to detect spam email is okay but missing out of detecting fraud or disease is high (use recall metrics for the latter). Finding as many spam email is desirable than missing out to detect spam email (use precision). 

If both Precision and Recall are equally important than F1 score should be used. There are variation of F1 score: 
- micro (globally by counting total positive)
- macro (calculate f1 for each label then complete <u>unweighted</u> mean)
- weighted (calculate f1 for each label then complete <u>weighted</u> mean)

Use weighted f1 when data is unbalanced.

5. Others common metrics

    a. ROC curve (receiver operating characteristic curve) 

    b. AUC (Area Under the ROC Curve)

    c. Confusion matrix

    d. Loss functions

Confusion matrix may be required in there is a need to see the exact number of TP, TN, FP, FN, sometimes uses for more technical-inclined stakeholders. Both metrics in 5a & 5b requires predicted labels & predicted probabilities in order to plot curve, avoid using when extracting proabilities is not possible or difficult. For loss functions, there is binary cross-entropy and multi-class entropy for binary/multi-class classification problems. These metrics are often used by internal development team.

## b.) Selecting metrics for regression problems
This section covers some of the most common metrics used for evaluating model for regression problems. 

1. Mean Square Error (MSE)

   Average of the squared differences between the actual and the predicted values. The lower the value, the better the regression model. It penalizes the outliers most.

2. Root Mean Square Error (RMSE)
   
   Square root of MSE, used when MSE value is too big for comparsion

3. Mean Absolute Error (MAE)

   Similar to Mean Square Error (MSE) but taking sum of absolute value of error. MSE gives larger penalization to big prediction error as compare to MAE.

MSE, RMSE, MAE are not very useful when comparing against different models when outliers that is presented very extreme.

4. R2
   
   One of the popular metrics, express as percentage. Large R2 value indicates a better fit, the closer to 1, the better the regression model. Easier for comparsion against different models as it ranges from 0 to 1.  

5. Adjusted R Square

   Similar to R2 but adds precision and reliabilty by considering additional independent variables that tend to skew the results of R-squared measurements

# 3. Satisficing metrics

Satisficing is a decision making strategy that aims for a satisfactory or adequate results rather than the optimal solution. Sometimes, it is hard to get a single number evaluation metric due to the non-ML metrics.

Example of some non-ML metrics
- runtime (inference time)
- training time
- memory usage
- size of model (more applicable for deployment on edge device)

It is not practical or cost efficient to increase the optimizing metrics by a minuscule percentage, using longer training time which results in higher cost. Deployment consideration (eg. size of model, runtime) may also affect the usablity of the model.

a) One approach is to derive a single metrics by forumla

For instance:

      metrics = accuracy of model - 0.5 * runtime

b) Another approach is to define what is an "acceptable" threshold for the satisficing metrics, then maximize the optimizing metrics.

Once your team is aligned on the evaluation metric to optimize, they will be able to make faster progress.

# Reference
https://github.com/ajaymache/machine-learning-yearning/blob/master/full%20book/machine-learning-yearning.pdf

https://www.davidsbatista.net/blog/2018/05/09/Named_Entity_Evaluation/

https://towardsdatascience.com/iou-a-better-detection-evaluation-metric-45a511185be1 