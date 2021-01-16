# Graphene-automatic-detection

The purpose of this project is to automatically identify and separate the layers of graphene flakes from the optical microscopic images. 


This repository includes
- Implemented an U-Net architecture as the first step to segment the background and the graphene flakes.
- Implemented a BT–Net architecture to find the thresholds of the pixel values of single and bilayer graphene flakes.
- Support Vector Machine(SVM) method using a Gaussian kernel to separate the graphene flakes.
- A comaprison among BT-Net, SVM methods and image processing methods.


## Dataset 
The graphene image dataset was prepared with a mechanical exfoliation method on several SiO2 substrates. All the images were taken using an optical microscope with x20, x50 and x100.   
The original dataset was provided by [Nanoelectronics lab](http://nano.phys.ncku.edu.tw) at National Cheng Kung University.


## Labeling 
The labeling software used for this project is [Labelbox](https://labelbox.com).   

A generated json file from Labelbox will then converted into a [COCO dataset](https://cocodataset.org/#home) for use.

[Labeling Tutorial]()


## Image Preprocessing method
Applied image preprocessing to increase the object detection rate under different lighting and contrast conditions. With the preprocessing methods, the object detection can be performed more accurately under different conditions, such as images taken by different cameras.  


## UNet Architecture
In this project, an UNet architecture was implemented to segment the background and the graphene flakes.   
- Click [here](https://www.youtube.com/watch?v=2nHsBEQst7g) to check the Youtube tutorial!   
- The architecture is as follows. [cite]  
- Images to demonstrate.


## Bi-Threshold-Net architecture(BT-Net)
The purpose of the BT-Net is to define the red, blue and green upper thresholds and the lower thresholds of the pixel intensity for both single layer and bilayer graphene flakes. Once the upper and lower thresholds for different layers of graphene are found, a color segmentation method was applied to separate the graphene flakes.    


![](/images/graphene_process.png)

The BT-Net structure is shown below.
<img src="/images/BTNet.png" width="800" height="400">


A modified loss function is defined to improve the result of the training model. 

- The definition of the loss funciton is as follows. 



## Support Vector Machine(SVM) Method
SVM is a supervised learning model used for regression and classification analysis. Once the background and the graphene flakes were separated using the U-Net architecture, the SVM method was implemented. Here the SVM algorithm was implemented with different kernels including Gaussian kernel, polynomial kernel and linear kernel to demonstrate the differences. Kernel function was picked to suit the problem. 

- 
- 


## Image Processing Methods

- Otsu's method.  

- Watershed method.
- canny edge filter

## Result Comparison and Discussion
Detection rate(DR) and false alarm rate(FAR) were calculated pixel by pixel.  
| Method       | monolayer DR(%) | monolayer FR(%) | bilayer DR(%) | bilayer FR(%) |
| :---         |      ---:       |          ---:   |          ---: |          ---: |
| SVM          | 87(new)/67(prev)              | 0.26            |90(new)/85(prev)             |0.35           |
| BT-Net       | 81.06                |     2.85            |90.06               | 2.89              |
| Otsu's method|  65.42               |      1.91           |     57.57          |   2.77            |

  
- Demonstration of SVM results(GT: ground truth; G: green; R: red)  
<img src="/images/SVM.png" width="600" height="600"><br />  

- Demonstration the results of BT-Net compared to Otsu's method  
(a) and (b)The result using BT–Net compared to Otsu's method for bilayer graphene.(c)  and  (d)The result using BT–Net compared to Otsu's method for monolayer graphene.

<img src="/images/otsuRGBNN_compare.png" width="600" height="700">



## References
[1] K. S. Novoselov, A. Mishchenko, A. Carvalho, and A. H. C. Neto, “2d materials and van der waals heterostructures,” Science, vol. 353, no. 6298, p. aac9439, 2016.  
[2] M. C. Lemme, T. J. Echtermeyer, M. Baus, and H. Kurz, “A graphene field-effect device,” IEEE Electron Device Letters, vol. 28, pp. 282–284, 2007.  
[3] F. Xia, T. Mueller, Y. ming Lin, A. Valdes-Garcia, and P. Avouris, “A graphene field-effect device,” Nature Nanotechnology, vol. 4, pp. 839– 843, 2009.  
[4] S. Masubuchi and T. Machida, “Classifying optical microscope images of exfoliated graphene flakes by data-driven machine learning,” npj 2D Materials and Applications, vol. 3, no. 1, pp. 1–7, 2019.  
[5] S. Masubuchi, E. Watanabe, Y. Seo, S. Okazaki, T. Sasagawa, K. Watan- abe, T. Taniguchi, and T. Machida, “Deep-learning-based image seg- mentation integrated with optical microscopy for automatically search- ing for two-dimensional materials,” npj 2D Materials and Applications, vol. 4, no. 1, pp. 1–9, 2020.  
[6] Y. Saito, K. Shin, K. Terayama, S. Desai, M. Onga, Y. Nakagawa, Y. M. Itahashi, Y. Iwasa, M. Yamada, and K. Tsuda, “Deep-learning- based quality filtering of mechanically exfoliated 2d crystals,” npj Computational Materials, vol. 5, no. 1, pp. 1–6, 2019.  
[7] K. S. Novoselov, A. K. Geim, S. V. Morozov, D. Jiang, Y. Zhang, S. V. Dubonos, I. V. Grigorieva, and A. A. Firsov, “Electric field effect in atomically thin carbon films,” Science, vol. 306, no. 5696, pp. 666–669, 2004.  
[8] Y. Huang, E. Sutter, N. N. Shi, T. Y. Jiabao Zheng, D. Englund, H.- J. Gao, and P. Sutter, “Reliable exfoliation of large-area high-quality flakes of graphene and other two-dimensional materials,” ACS Nano, vol. 9, no. 11, pp. 10612–10620, 2015.  
[9] O. Ronneberger, P.Fischer, and T. Brox, “U-net: Convolutional networks for biomedical image segmentation,” vol. 9351, pp. 234–241, 2015.  
[10] N. Otsu, “A threshold selection method from gray-level histograms,” IEEE Transactions on Systems, Man, and Cybernetics, vol. 9, pp. 62– 66, 1979.  
[11] J. Zhang and J. Hu, “Image segmentation based on 2d otsu method with histogram analysis,” International Conference on Computer Science and Software Engineering.  
[12] K. Simonyan and A. Zisserman, “Very deep convolutional networks for large-scale image recognition,” In ICLR.  
