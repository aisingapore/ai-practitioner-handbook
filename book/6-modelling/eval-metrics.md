# What are the considerations (internally by the team), and externally (by the stakeholders) when selecting evaluation metrics?

Contributor(s): Er YuYang

This guide assumes that you have a fair understanding of why the stakeholders is developing the AI/ML project (understand the business value), and have a reasonable understanding for the implementation difficulty of the evaluation for given the dataset.

# Overview

1. Understanding stakeholder's problem and environment 

2. Optimizing metrics

   a. Selecting metrics for classification problems

   b. Selecting metrics for regression problems

3. Satisficing metrics

## 1. Understanding the problem and environment 

<u>Problem statement & deployment environment</u>

   Understanding how the AI/ML solves the problem statement help to identify the correct optimizing metrics (explained in section 2) to determine the performance of the model. At the same time, understanding the deployment environment will helps in choosing the satisficing metrics (explained in section 3). In most case, optimizing metrics tend to be the ML metrics, while satisficing metrics tend to be the non-ML metrics.

<u>Technical competence of the different stakeholders</u>
   
   Understanding the level of competence of the end-users or technical team maintaining the AI/ML model help to identify a <b>comfortable</b> metrics (explained in section 2) to use 
   - for ease of communicating with end-users during project phase
   - allows the technical team to easily understand the metric that was used, hence able to improve the AI/ML model after the project handover
   
<u>Summary</u>

The main purpose is to understand the problem and stakeholders, as there is often a trade-off between ML and non-ML metrics on the whole. For instance, a more complex model tends to come with larger training and inference time. Hence, sponsors are faced with a choice as to which metrics to prioritise based on the business value of the AI solution.

## 2. Optimizing metrics

The goal is to establish a single-number evaluation metric, as having multiple evaluation metrics make it hard to compare against different algorithms.

For instance, Classifier A has precision of 95% with recall of 90% and Classifier B has precision of 98% with recall of 85%, Neither classifier is obviously superior and does not immediately guide you towards picking one.

When comparing with different model in classification problem with multiple class, combined metrics of each class into single metric using average on weighted average. However, keep the metrics separated if you are evaluating the class performance instead of the model performance.


## a.) Selecting metrics for classification problems
This section covers some of the most common metrics used for evaluating model for classification-related problems, which cuts across diverse use cases like objection detection, named entity recognition (NER), anomaly detection, recommender systems, etc. In these problems, the precision, recall and F1 family is a very generic and flexible metrics that can be applied throughout.

<u>Commonly used evaluation metrics</u>

1. Accuracy = $\frac{TP + TN}{TP + FP + TN + FN}$
   
   Avoid using this metrics as it is usually not suitable for practical usages due to the fact it contains many flaws as a evaluation metrics.

2. Precision = $\frac{TP}{TP+FP}$

   Simplified explaination: Out of the <u>positive predictions</u>, how many are correct. It focuses on finding positive cases.

3. Recall = $\frac{TP}{TP+FN}$

   Simplified explaination: Out of the <u>actual positive</u>, how many are correct. It focuses on weeding out the negative cases.

4. F1 Score = 2 * $\frac{Precision * Recall}{Precision + Recall}$
   
   F1 score is the harmonic mean of precision and recall

<u>Considerations</u>

Precision is more important than recall when you cannot afford to have any FP as compare to FN. Often associate with cost, when cost of acting is high but the cost of not acting is low, then precision is preferred. Recall is more important than precision when you cannot afford to have any FN as compare to FP. It is more important when the opportunity cost of passing up is high. 

Example: The opportunity cost is low when there is certain recommendation were missing out but more costly when there is a wrong recommendation as it translates to not buying the recommended item, then precision is preferred. The opportunity cost of missing out of detecting fraud or disease would be high as compare to cost of acting to perform routine check on non-fraud/non-disease case, then recall is preferred.

|  |           Recommender System              |                Fraud/Disease Detection               |
|--| ----------------------------------------- | ---------------------------------------------------- |
|TP| Marked as preferred, is preferred         | Marked as fraud/disease, is fraud/disease            |
|FP| <b>Marked as preferred, not preferred</b> | Marked as fraud/disease, not fraud/disease           |
|TN| Not marked as preferred, not preferred    | Not Marked as fraud/disease, not fraud/disease       |
|FN| Not marked as preferred, is preferred     | <b>Not marked as fraud/disease, is fraud/disease</b> |

If both Precision and Recall are equally important than F1 score should be used. There are variation of F1 score: 
- micro (globally by counting total positive)
- macro (calculate f1 for each label then perform unweighted mean)
- weighted (calculate f1 for each label then perform weighted mean)

When using weighted/micro f1 for imbalanced data means we are assessing the model while prioritising the majority class (as minority class have lesser influence over the final f1 score). When using macro f1 for imbalanced data, it means that we give equal importance to the minority class (minority class have same weightage as majority, hence greater influence over the final f1 score).

Hence if the data is unbalanced, the choice between weighted and unweighted is dependent on the business objective. If the minority class is the 'costly', then weighted/micro f1 is not suitable since it does not give the same influence/weightage for minority class, then it would be better to assess based on macro f1.

To summarize, there are often few tradeoffs in choosing one metrics over another. Below is some common questions to ask the stakeholders in order to recommend a suitable metrics for the problem that AI/ML is trying to solve.
- Is precision or recall more important? or are they all equally important?
- Which class is more important, or are they all equally important?

## b.) Selecting metrics for regression problems
This section covers some of the most common metrics used for evaluating model for regression problems. 

1. Mean Square Error (MSE)

   Average of the squared differences between the actual and the predicted values. The lower the value, the better the regression model. It penalizes the outliers most.

2. Root Mean Square Error (RMSE)
   
   Square root of MSE, recommends to use when MSE value is too big for comparsion

3. Mean Absolute Error (MAE)

   Similar to Mean Square Error (MSE) but taking sum of absolute value of error. MSE gives larger penalization to big prediction error as compare to MAE.

<u>Considerations</u>

MSE, RMSE, MAE are not very useful when comparing against different models when outliers that is presented are very extreme.

4. R2
   
   One of the popular metrics, express as percentage. Large R2 value indicates a better fit, the closer to 1, the better the regression model. Easier for comparsion against different models as it ranges from 0 to 1.  

5. Adjusted R Square

   Similar to R2 but adds precision and reliabilty by considering additional independent variables that tend to skew the results of R-squared measurements.

## 3. Satisficing metrics

Satisficing is a decision making strategy that aims for a satisfactory or adequate results rather than the optimal solution. Sometimes, it is hard to get a single number evaluation metric due to the non-ML metrics.

Example of some non-ML metrics
- runtime (inference time)
- training time
- memory usage
- size of model (more applicable for deployment on edge device)

It is not practical or cost efficient to increase the optimizing metrics by a minuscule percentage, using longer training time which results in higher cost.  Deployment consideration (eg. size of model, runtime) may also affect the usablity of the model.

a) One approach is to derive a single metrics by forumla

For instance:

      metrics = accuracy of model - 0.5 * runtime

b) Another approach is to define what is an "acceptable" threshold for the satisficing metrics, then maximize the optimizing metrics.

Once your team is aligned on the evaluation metric to optimize, they will be able to make faster progress.

# Reference
<a href="https://github.com/ajaymache/machine-learning-yearning/blob/master/full%20book/machine-learning-yearning.pdf">Chapter 8 and 9 of Andrew's Ng</a>

<a href="https://towardsdatascience.com/accuracy-precision-recall-or-f1-331fb37c5cb9">Accuracy, Precision, Recall or F1</a> 

<a href="https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f">Micro, Macro & Weighted Averages of F1</a>
