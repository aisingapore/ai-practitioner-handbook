# What are the considerations (internally by the team), and externally (by the shareholders) when selecting evaluation metrics?

Contributor(s): Er YuYang

This guide assumes that you have a fair understanding of why the stakeholders is developing the AI/ML project (understand the business value), and have a reasonable understanding for the implementation difficulty of the evaluation for given the dataset.


# High level metrics (classification)
This section covers some of the most common metrics used for evaluating model for classification problem. Do note that this is not exhaustive list by covers common high level metrics that are useful when communicating with stakeholders.

1. Accuracy = $\frac{TP + TN}{TP + FP + TN + FN}$
   
   Simple to explain but not suitable if the dataset is unbalanced

2. Precision = $\frac{TP}{TP+FP}$

   Precision focus on finding positive cases

3. Recall = $\frac{TP}{TP+FN}$

   Recall focus on weeding out the negative cases

4. F1 Score = 2 * $\frac{Precision * Recall}{Precision + Recall}$
   
   F1 score is the weighted mean of precision and recall

Precision is more important than recall when you cannot afford to have any FP as compare to FN. Also, often assoicate with cost, when cost of acting is high but the cost of not acting is low, then precision is preferred.

Recall is more important than precision whe you cannot afford to have any FN as compare to FP. Recall is important when the opportunity cost of passing up is high. 

Example: Missing out to detect spam email is okay but missing out of detecting fraud or disease is high (use recall metrics). Finding as many spam email is desirable than missing out to detect spam email (use precision). 

If both Precision and Recall are equally important than F1 score should be used.

5. Others common metrics

    a. ROC curve (receiver operating characteristic curve) 

    b. AUC (Area Under the ROC Curve)

Both above metrics requires predicted labels & predicted probabilities in order to plot curve.

# In-depth metrics
This section covers some of the depth metrics used in different AI domain. Do note that this is not exhaustive list.

1. Evaluation metrics for NER
   - Message Understanding Conference (MUC)
     - Corrrect (COR)
     - Incorrect (INC)
     - Partial (PAR)
     - Missing (MIS)
     - Spurius (SPU)
   - International Workshop on Semantic Evaluation (SemEval)
     - Strict
     - Exact
     - Partial
     - Type

2. Evaluation metrics for Object Detection
   - Intersection over Union (IOU)
   - Average Precision (AP)
   - Mean Average Precision (mAP)


# High level metrics (Regression)
This section covers some of the most common metrics used for evaluating model for regression problem. 

1. MAE
2. MSE
3. RMSE
4. RMSE
5. R2