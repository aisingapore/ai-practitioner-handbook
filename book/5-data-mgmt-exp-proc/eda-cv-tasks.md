# What are some of the ways to do EDA for CV tasks?

Contributor: Calvin Neo, AI Engineer

---

The purpose of this article is to guide new AI Engineers on performing Exploratory Data Analysis of Computer Vision tasks in a systematic manner. 

## Image EDA  

### Basic Image Analysis  
The basic image analysis considers the broad characteristics of the images that have been obtained.  

The guiding questions are as such:  
1. What is the number of images provided? Is this the number of images promised to be delivered for experiments?
1. What is the format of images eg JPG/PNG/JPEG? If there are multiple formats given, what are the counts for each image format? 
1. What are the image sizes/resolution (eg 1080x960)? If there are multiple dimensions, what are the counts for each dimension?
1. How similar are the images to each other? You can do an EDA to check on this by performing image hashing to discover groups which are similar to each other.

### Colour Intensity of Image

The colour intensity of images can be explored by either averaging or  the channel values of each image 

### Image Similarity
1. PCA or ISOMAP per channel can be performed on the images to see how the images are related to each other.

![title](../assets/images/screenshots/isomap_pca.png)

## Annotations (Basic Overview)

### Bounding Boxes Formats

1. COCO - [x_min, y_min, width, height]
1. YOLO - [x_center, y_center, width, height]
1. Pascal VOC - [x_min, y_min, x_max, y_max]

For example, if the given format is in Pascal VOC, and the model requires it in YOLO format, we would need to convert the annotations to YOLO format for training.  

An example for during inference: Read images using CV2, run YOLOv3 model, convert then return in the desired format according to what the sponsor wants

### Masks Format

Masks annotations gives the pixel-wise positions of the mask.

Masks are provided in an array of x-y pairs. It will typically be:

```
masks_per_instance = [x_1, y_1, x_2, y_2, ... x_n, y_n]
```

Masks may also come in the form of PNG files, where the PNG's image size would correspond to the original image size. 

## Annotations EDA

### Basic Annotations Analysis

Guiding Questions - 
1. How many instances of each classes are there?
1. Bounding Box - what is Width and Height Distribution overall and per class?
1. Bounding Box - what is the overall size (W*H) overall and per class?
1. Bounding Box - What are the top few Width/Height combination? This can be found using clustering methods.
1. Segmentation - what is distribution of the mask pixel counts overall and per class?

### Colours of Annotations
The annotations have 1 or more channels per pixel. The most popular is Red, Blue and Green (RGB). 

#### Average Intensity per channel  
To explore this for all classes, we can firstly average the colour intensity of the annotation's pixels per channel. 
Secondly, countplot of the average colour intensity values could be generated. The screenshot below shows the 
counts of each annotation with the average values of the red channels separated by classes.

![title](../assets/images/screenshots/red_channel_average_counts.png)

#### Dominant Intensity per channel    

Besides averaging the intensity per annotation, the highest occurring value of the intensity of the annotation can 
also be used to analyse the colour of the annotation.  

![title](../assets/images/screenshots/red_channel_dominant_counts.png)

## Annotations Random Sample Checks

### Bounding Box and Mask Random Sample Checks

Bounding Boxes Random Sample Check refers to performing a check by sampling images and analysing their annotations. 

1. Are the masks/boxes drawn tight enough? 
1. Are the objects being occluded? In other words, were parts of the object blocked by another object?
1. Are the objects truncated? In other words, were parts of the objects being spilling out of the image?

For occlusion and truncation, it is recommended to include "occlusion" and "truncation" in the metadata of the annotation. 

## References

Perceptual Hashing - https://www.phash.org/
VOC annotation guide - http://host.robots.ox.ac.uk/pascal/VOC/voc2011/guidelines.html
