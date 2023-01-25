# What are some common CV evaluation metrics?

Contributor(s): Calvin Neo, AI Engineer

---

This guide assumes a fair understanding of the computer vision-related tasks specifically image classification, object detection, and instance segmentation and their accompanying terms such as bounding boxes (bboxes) and masks. Additionally, it assumes an understanding of classification metrics such as F1 score, precision and recall. 

The purpose of this article is to guide AI engineers on key considerations when evaluating metrics for object detection and instance segmentation tasks. For the most part, conventional classification metrics can be used to evaluate image classification tasks. Hence, an understanding of image classification would be useful here. In this case, refer to the article on [classification metrics](./classification-metrics-guidelines.md).

## Mean Average Precision (mAP)

There are many articles on how to calculate mAP available. It is thus instructive to instead discuss considerations when reading mAP.

In discussing mAP evaluation, consider the output below:

| Average Precision 	| IOU       	| Area   	| Max Detections 	| mAP   	|
|-------------------	|-----------	|--------	|----------------	|-------	|
| Average Precision 	| 0.5       	| all    	| 1000           	| 0.743 	|
| Average Precision 	| 0.75      	| all    	| 1000           	| 0.213 	|
| Average Precision 	| 0.50:0.95 	| all    	| 100            	| 0.326 	|
| Average Precision 	| 0.50:0.95 	| small  	| 1000           	| 0.127 	|
| Average Precision 	| 0.50:0.95 	| medium 	| 1000           	| 0.349 	|
| Average Precision 	| 0.50:0.95 	| large  	| 1000           	| 0.406 	|

Where mAP for IOU = 0.50:0.95 measures the AP values at IOUs 0.50 to 0.95, with a step of 0.05, and then averaging the values.   

Firstly, it is useful to evaluate the Intersection over Union (IOU) threshold value to understand how "tight" a bbox/mask. A higher IOU threshold value indicates that the model's inference closely overlaps with the ground truth, and is hence a more stringent evaluation criteria. Generally, the mAP suffers as the IOU threshold value increases. Thus, evaluating how much these values fall would be valuable clues on how well the model may produce tight bboxes/masks.

Using the outputs above, the second row shows that at IOU threshold of 0.50, the mAP is given by 0.743. Similarly, the third row showing IOU=0.75 threshold shows 0.213, a 0.53 fall in value. This indicates that the bboxes/masks produced by the model were not tight enough, and more training may be required. 

Secondly, the objects being detected can be broadly separated to small/medium/large objects based on the bbox/mask size. Here, it is assumed the small/medium/large are area of the bbox/mask, and that area threshold for these sizes are clearly defined. For more information on how to determine small/medium/large objects, see article on [Exploratory Data Analysis for Compter Vision Tasks](../5-data-mgmt-exp-proc/eda-cv-tasks.md). 

A model generally performs the worst on small objects and gets better as the size increases. Thus, evaluating this is also instructive. Considering the above outputs, the mAP is 0.127/0.349/0.406 on small/medium/large objects. Thus, it would be good to have the model be trained on more small objects in order to potentially improve its performance. 

## Frames Per Second (FPS)

FPS are generally measured by running multiple images through the pipeline and obtaining the amount of time taken to process each image, before converting it to frames per second. The way to do it is: 

$FPS = \frac{1}{\text{Average Time Taken Per Image}}$

Here, the AI Engineer would need to consider the following:

FPS should be calculated based off either model's or the software architecture's inference speed. For model's FPS, it is simply the inference speed solely on the model, without taking into account other processes like data ingestion/pre-processing and inference post-processing. The software architecture's inference speed considers all the different software components that is related to the inference such as the above mentioned processing steps.  

In most cases, though, the FPS of concern would be solely on the model since the main concern is to deliver a model. This is especially so when the concern of FPS is complicated by other factors outside of the model and beyond the AI Engineer's cotrol, namely internet connections and hardware. Whichever way, the onus is on the AI Engineer to communicate how the FPS was measured to manage expectations.

It is also important to consider what affects FPS. The first factor would be model size. A model that is deep, and hence tend to be larger in size, requires a longer processing time. Another factor is image size. Larger image size will take longer for inference. For example, a 416x416 image will be faster than 1080x960 image. While again this is obvious, it is also often overlooked by AI Engineers when reading papers that purport higher inference speeds, but downplays the role that smaller images have on inference speed.  

## Trade-off Between mAP and FPS

When a model has been identified based on mAP and FPS, further refinements can be made that may involve trading FPS for mAP or vice versa. For example, for certain models, the images that is passed in can have its size further reduced. The advantage here would be that inference speed is higher, and hence the FPS will be higher as well. However, since the image is reduced, the model may not have enough features to extract and map, further reducing its ability to accurately infer from the image. This drives down mAP. Increasing the image size will have the opposite effect. 

Hence, it is important to establish "good enough". That is, the engineer would need to work with the sponsor to come up with the metric threshold that would satisfy their use case. For example, if a model currently has mAP = 0.50, and FPS = 60, and the engineer knows that inference speed, for various reasons, would only need to be around 30, then they would be able to increase image size further to potentially increase mAP while accepting the FPS reduction.

It is also good to bear in mind diminishing returns. In the case above, if the FPS went down to 30 and the mAP went up to 0.52, would the trade-off be worth it? No in most cases. Thus, running through various parameters to find a good trade-off is important in such cases. 

## Adjusting Thresholds for Inference - Confidence and Non-max Suppression (NMS)

When a model makes an inference, it will give a confidence level of the object's class. If the confidence does not meet or exceed the threshold, then it will not be included. 

Similarly, when a model makes duplicative inference on the same object, meaning it has two or more bounding boxes on the same object, there has to be a mechanism to suppress these duplicative boxes.

Thus, the engineer may use the Confidence and/or NMS threshold to ensure to adjust the precision and recall of the model. 

To show this, consider the output below. Such a table can be generated by running the model on a combination of possible threshold values. 

| Confidence 	| NMS  	| IOU  	| Precision 	| Recall 	| F1 Score 	|
|------------	|------	|------	|-----------	|--------	|----------	|
| 0.3        	| 0.1  	| 0.5  	| 0.697     	| 0.752  	| 0.724    	|
| 0.5        	| 0.1  	| 0.5  	| 0.750     	| 0.732  	| 0.741    	|
| 0.7        	| 0.1  	| 0.5  	| 0.811     	| 0.697  	| 0.750    	|
| 0.3        	| 0.4  	| 0.5  	| 0.640     	| 0.789  	| 0.707    	|
| 0.5        	| 0.4  	| 0.5  	| 0.718     	| 0.759  	| 0.738    	|
| 0.7        	| 0.4  	| 0.5  	| 0.794     	| 0.717  	| 0.754    	|
| 0.3        	| 0.7  	| 0.5  	| 0.579     	| 0.800  	| 0.672    	|
| 0.5        	| 0.7  	| 0.5  	| 0.682     	| 0.768  	| 0.722    	|
| 0.7        	| 0.7  	| 0.5  	| 0.774     	| 0.723  	| 0.747    	|

It is clear here that Confidence and NMS threshold can appear to be at odds with each other. As Confidence Threshold is increases, the Precision increases, but Recall is lower. Conversely, a higher NMS threshold gives better recall.

## Prioritising Precision or Recall

As stated above, the AI Engineer has to continually engage with the product owner in determining which to prioritise. Obviously, they can also rely on F1-Score to harmonise the two. However, do keep in mind the following:

1. Choose Precision if quality is the the priority of the model. That is, it needs to identify objects and their classes. 
2. Choose Recall if quantity is the priority of the model. That is, it needs to identify many more objects without caring too much about whether the class was correctly identified. 

## Conclusion

This article addresses the conventional metrics for object detection and instance segmentation in the context of pushing a product. Beyond simply calculating these metrics, the AI Engineer would do well look out for granular details when evaluating the metrics in order to give a more accurate picture of model performance. 

