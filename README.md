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
The labeling software used for this project is [Labelbox](https://labelbox.com). 


A generated json file from Labelbox will then converted into [COCO dataset]() for use.

[Details]()

## UNet Architecture
Click [here](https://www.youtube.com/watch?v=2nHsBEQst7g) to check the Youtube tutorial!

- The architecture is as follows. [cite]


## Bi-Threshold-Net architecture(BT-Net)
The purpose of the BT-Net is to define the red, blue and green upper thresholds and the lower thresholds of the pixel intensity for both single layer and bilayer graphene flakes. Once the upper and lower thresholds for different layers of graphene are found, a color segmentation method was applied to separate the graphene flakes.  
A modified loss function is defined to improve the result of the training model. 

- The definition of the loss funciton is as follows. 
- The architecture is as follows.[cite]


## Support Vector Machine(SVM) Method
SVM is a supervised learning model used for regression and classification analysis. Once the background and the graphene flakes were separated using the U-Net architecture, the SVM method was implemented using a Gaussian kernel, a polynomial kernel and a linear kernel to demonstrate the differences. Kernel function was picked to  suit the problem. 

- 
- 


## Image Processing Methods

- Otsu's method.  

- Watershed method.
- canny edge filter

## Result Comparison and Discussion


## References
# References
[[1]Wikipedia page of support vector machine](https://en.wikipedia.org/wiki/Support_vector_machine) 
[[2]scikit learn page of support vector machine](https://scikit-learn.org/stable/modules/svm.html) 
