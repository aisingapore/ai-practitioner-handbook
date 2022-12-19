# What are some of the ways to do EDA for CV tasks?

Contributor: Calvin Neo, AI Engineer

---

The purpose of this article is to guide new AI Engineers on performing Exploratory Data Analysis of Computer Vision tasks in a systematic manner. 

1. [Images](#images)
2. [EDA](#eda)
3. [Annotations](#annotations)

## Pre-EDA

## EDA  

### Images
1. What is the number of images provided? Is this the number of images promised to be delivered for experiments?
1. What is the format of images eg JPG/PNG/JPEG? 
1. What are the image sizes (eg 1080x960)? 
1. How similar are the images to each other? You can do an EDA to check on this by performing hash similarity.

### Image Colours
1. Colour Distribution per channel - What is the distribution of the colour in each channel? Is it normally distributed or multimodal? The goal is to see if there is a need to equalise the colour contrast.
1. You can try performing PCA or ISOMAP per channel to see how the images are related to each other.

### Annotations
1. How many instances of each classes have we got?
1. Bounding Box - what is Width and Height Distribution overall and per class?
1. Bounding Box - what is the overall size (W*H) overall and per class?
1. Bounding Box - Run a KMeans clustering on the Width and Height clusters?
1. Segmentation - what is distribution of the mask pixel counts overall and per class?

## Annotations

### Bounding Boxes Formats

1. COCO - [x_min, y_min, width, height]
1. YOLO - [x_center, y_center, width, height]
1. Pascal VOC - [x_min, y_min, x_max, y_max]

Just be aware that these formats exist, and you'll need to manipulate them where necessary. 

For example, if the given format is in Pascal VOC, and the model requires it in YOLO format, we would need to convert the annotations to YOLO format for training.  

An example for during inference: Read images using CV2, run YOLOv3 model, convert then return in the desired format according to what the sponsor wants

### Bounding Box Random Sample Checks

1. Are the boxes drawn tight enough? 
1. Are the objects being occluded?
1. Are the objects truncated?

### Masks

Masks are less confusing than bounding boxes because the annotations would give you the pixel-wise position of the mask.

Masks are provided in an array of x-y pairs. It will typically be:

```
masks_per_instance = [x_1, y_1, x_2, y_2, ... x_n, y_n]
```

Thus, when reading this, you can choose to distangle it by doing two list comprehensions

```
x_per_instance = [masks_per_instance[i] for i in range(0,n*2,2)]
y_per_insance = [masks_per_instance[i] for i in range(1,n*2,2)]
```

### Classes

Some models are 0-indexed, while some start from 1. 