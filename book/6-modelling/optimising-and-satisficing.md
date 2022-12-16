# What are some internal and external considerations when selecting evaluation metrics?

Contributor(s): Er YuYang, Senior AI Engineer

---

This guide assumes that you have a fair understanding of the business value of the AI/ML project, and have an appreciation of the implementation difficulty of the evaluation metrics. Internal considerations refer to those concerning the development team, while external considerations refer to those concerning business users/stakeholders.

### 1. Understanding the problem space

#### Problem statement

Understanding how the AI/ML solves the problem statement helps to identify the correct optimising metrics (explained in section 2) for assessing the performance of the model. Complementarily, understanding the deployment environment helps in choosing the satisficing metrics (explained in section 3). In most cases, optimising metrics tend to be ML metrics, while satisficing metrics tend to be non-ML metrics.

There is often a trade-off between ML and non-ML metrics. For instance, a more complex model can return better ML metrics, but can also come with longer training and inference times (non-ML metrics). As such, developers and business users are faced with a choice as to which metrics to prioritise based on the business value of the AI solution.

#### Technical ability of stakeholders
   
It is important to understand the level of technical ability possessed by eventual end-users and/or maintainers of the AI/ML solution. This understanding can help identify metrics that these stakeholders are *comfortable* with.

Comfortable metrics are important for for ease of communicating with the stakeholders. Importantly, they allow future technical teams to understand and improve the AI/ML model in later stages of its life cycle.

### 2. Optimising metrics

The goal here is to establish a single-number evaluation metric, as multiple evaluation metrics make it hard to compare between different models.

For instance, Classifier A has precision of 95% with recall of 90% and Classifier B has precision of 98% with recall of 85%. Neither classifier is obviously superior and does not immediately guide you towards picking one. In this case, you may consider taking the F1 score, which is the harmonic mean of precision and recall.

To obtain a single-number metric for multi-class classification problems, you can combine metrics of each class into single metric using average or weighted average. However, keep the metrics separated if you are evaluating intraclass performance instead of overall model performance.

### 3. Satisficing metrics

In theory, optimising metrics should be maximised as much as possible. In practice, however, practical tradeoffs/compromises have to be made. These take the form of satisficing metrics, which are often non-ML related. Examples of satisficing metrics include:

- Running/inference time
- Training time
- Memory/storage usage (particularly applicable for edge deployment)

It is not practical or cost-efficient to increase optimising metrics by a minuscule percentage while making disproportionate trade-offs on satisficing metrics. For example, increasing model accuracy by 0.0001 may required significantly longer and more expensive computation time. Deployment considerations (eg. size of model, runtime) may also come into play here.

### 4. Combining optimising and satisficing metrics

Consideration of both optimising and satisficing metrics means that there are at least two sets of numbers to optimise. How can we adhere more closely to the more elegant single-number metric approach?

One approach is to derive a single metric through a forumla. For instance:

      metrics = accuracy of model - 0.5 * runtime

Another approach is to first define an "acceptable" threshold for the satisficing metric through consultation with stakeholders. The development team can then work to maximise the optimising metrics within acceptable bounds of the satisficing metric.

Once your team is aligned on the evaluation metric to optimise, they will be able to make faster progress.

## References
[*Machine Learning Yearning*, Chapers 8 and 9](https://github.com/ajaymache/machine-learning-yearning/blob/master/full%20book/machine-learning-yearning.pdf)