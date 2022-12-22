# What are some of the ways to do EDA for CV tasks?

Contributor: Calvin Neo, AI Engineer

---

The purpose of this article is to guide new AI Engineers on performing Exploratory Data Analysis of Computer Vision tasks in a systematic manner. 

## Pre-EDA

## Image EDA  

### Basic Image Analysis  
The basic image analysis considers the broad characteristics of the images that have been obtained.  

The guiding questions are as such:  
1. What is the number of images provided? Is this the number of images promised to be delivered for experiments?
1. What is the format of images eg JPG/PNG/JPEG? If there are multiple formats given, what are the counts for each image format? 
1. What are the image sizes/resolution (eg 1080x960)? If there are multiple dimensions, what are the counts for each dimension?
1. How similar are the images to each other? You can do an EDA to check on this by performing image hashing to discover groups which are similar to each other.

### Image Colours
1. Colour Distribution per channel - What is the distribution of the colour in each channel? Is it normally distributed or multimodal? The goal is to see if there is a need to equalise the colour contrast.
1. You can try performing PCA or ISOMAP per channel to see how the images are related to each other.

![title](../assets/images/screenshots/isomap_pca.png)

## Annotations (Basic Overview)

### Bounding Boxes Formats

1. COCO - [x_min, y_min, width, height]
1. YOLO - [x_center, y_center, width, height]
1. Pascal VOC - [x_min, y_min, x_max, y_max]

Just be aware that these formats exist, and you'll need to manipulate them where necessary. 

For example, if the given format is in Pascal VOC, and the model requires it in YOLO format, we would need to convert the annotations to YOLO format for training.  

An example for during inference: Read images using CV2, run YOLOv3 model, convert then return in the desired format according to what the sponsor wants

### Masks

Masks are less confusing than bounding boxes because the annotations would give you the pixel-wise position of the mask.

Masks are provided in an array of x-y pairs. It will typically be:

```
masks_per_instance = [x_1, y_1, x_2, y_2, ... x_n, y_n]
```

Aside from that, Masks may also come in the form of PNG files, where the PNG's image size would correspond to the original image size. 

## Annotations EDA

### Annotations
1. How many instances of each classes have we got?
1. Bounding Box - what is Width and Height Distribution overall and per class?
1. Bounding Box - what is the overall size (W*H) overall and per class?
1. Bounding Box - Run a KMeans clustering on the Width and Height clusters.
1. Segmentation - what is distribution of the mask pixel counts overall and per class?

## Annotations Random Sample Checks

### Bounding Box and Mask Random Sample Checks

Bounding Boxes Random Sample Check refers to performing a check by sampling images and analysing their annotations. 

1. Are the masks/boxes drawn tight enough? 
1. Are the objects being occluded?
1. Are the objects truncated?

## References

Perceptual Hashing - https://www.phash.org/
