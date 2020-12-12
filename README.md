# Graphene-automatic-detection

The purpose of this project is to automatically identify and separate the layers of graphene flakes from the optical microscopic images. 


This repository includes
- U-Net architecture implemented as the first step to segment the background and the graphene flakes.
- BT–Net architecture to find the thresholds of the pixel values of single and bilayer graphene flakes.
- Support Vector Machine(SVM) method using a Gaussian kernel to separate the graphene flakes.
- A comaprison among BT-Net, SVM methods and image processing methods.


## Dataset 
The original dataset is provided by [Nanoelectronics lab](http://nano.phys.ncku.edu.tw) at National Cheng Kung University.


## Labeling 
The labeling software is [Labelbox](https://labelbox.com). 


A generated json file from Labelbox will then converted into [COCO dataset]() for use.

[Details]()

## UNet Architecture
- The architecture is as follows. [cite]
## Bi-Threshold-Net architecture(BT-Net)
The purpose of the BT-Net is to define the red, blue and green upper thresholds and the lower thresholds of the pixel intensity for both singer layer and bilayer graphene flakes. A self-designed loss function is defined to improve the result of the training model. 

- The definition of the loss funciton is as follows. 
- The architecture is as follows.[cite]


## Support Vector Machine Method
Once the background and the graphene flakes were separated using the U-Net architecture, the SVM method was implemented using a Gaussian kernel.

- 
- 


## Image Processing Methods

- Otsu's method.
- Watershed method.
- canny edge filter

## Result Comparison and Discussion


