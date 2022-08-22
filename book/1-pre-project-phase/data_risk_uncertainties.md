# What are the potential data risks/uncertainties that the AI engineer will be inheriting from the project?
Contributor: Tan Kwan Chet 

---
## Data Risks/Uncertainties

Having understood the business challenge and AI problem at hand, this is where you need to delve into understanding the data the sponsor has collected. You need to assess if there are risks/uncertainties posed within the data collected and annotated for solving the AI problem. Because a good AI model not only relies on algorithms but also quality data.

### Quote from Andrew Ng
> AI systems need both code and data, and “all that progress in algorithms means it's actually time to spend more time on the data,” Ng said at the recent EmTech Digital conference hosted by MIT Technology Review.

Here are 3 questions good for uncovering potential data risks/uncertainties:

1. Does the data include information that can predict the target?
In the case of detecting fraudulent transactions, it will be important to identify if there are relevant predictors to construct the AI model (e.g. transaction amount, transaction purpose). Another important point would be to ascertain the size of target to be detected within the image/video for object detection. Usually, it will be fairly resonable for the AI model to detect an object of between 10% and 50% of the image size. If there is a need for detecting objects smaller than 10% of the image size, then it will be deemed more challenging and you will need to do necessary research to find models for specifically detecting small objects. 

2. Do you have the data labels?
If it is a binary classification label - positive sentiment and negative sentiment, the imbalanced label proportion would result in training an AI model biased towards the majority class. This is because the AI model is trained on limited examples to identify the minority class. However, if it is a regression target, then you need to have different ranges of values. You want to avoid training a regression model on the data that has very discrete values. For examples, if you observe the target variable centres around 1 or 2 values such as 5 or 10, then the question would be is it necessary to train the model on it? Or rather, is it better to convert this variable into a categorical one?

3. Do you have the correct granularity of the data?
It is critical to ensure that the training data and production data share the same level of granularity (e.g. hourly, daily, weekly, monthly or yearly) as what your sponsor expects in prediction. So if the sponsor expects the prediction to on hourly basis and the sponsor collects the data daily, then it will not be possible to build such an AI model to produce a granular prediction based on aggregated data. It is also worthy to note that if expected prediction is at a higher or similar granularity as the training or production data, then it is possible to build an AI model. 


## References 
- [MLOps-From-Model-centric-to-Data-centric-AI](https://www.deeplearning.ai/wp-content/uploads/2021/06/MLOps-From-Model-centric-to-Data-centric-AI.pdf)
- [Why it’s time for 'data-centric artificial intelligence'](https://mitsloan.mit.edu/ideas-made-to-matter/why-its-time-data-centric-artificial-intelligence)
- [Is My Data Any Good? A Pre-ML Checklist](https://services.google.com/fh/files/blogs/data-prep-checklist-ml-bd-wp-v2.pdf)