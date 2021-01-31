# Graphene-automatic-detection

This work investigates the important problem of autonomous graphene detection in microscopic substrate images. We study the application of hybrid deep learning(DL)/machine learning(ML) techniques to segment the monolayer and bilayer graphene. We implement a modified U-Net model to segment the graphene flakes from the background. By using the segmentation results from the U-Net model, we implement a support vector machine (SVM) to separate the monolayer and bilayer graphene flakes. There are two features including the graphene and the background pixel values from microscopic images as the inputs for the SVM model. We achieve detection rates of 87.09\% and 90.41\% for monolayer and bilayer graphene. 


This repository includes
- Implement a modified U-Net architecture as the first step to segment the background and the graphene flakes.
- Implement a Support Vector Machine(SVM) method using a Gaussian kernel to separate the graphene flakes.


## Dataset 
The graphene image dataset was prepared with a mechanical exfoliation method on several SiO2 substrates. All the images were taken using an optical microscope with x20, x50 and x100.   
The original dataset was provided by [Nanoelectronics lab](http://nano.phys.ncku.edu.tw) at National Cheng Kung University.


## Labeling 
The labeling software used for this project is [Labelbox](https://labelbox.com).   

A generated json file from Labelbox will then converted into a [COCO dataset](https://cocodataset.org/#home) for use.

[Labeling Tutorial]()

## Process of graphene segmentation
<img src="/images/process.png" width="800" height="220">


## Image Preprocessing method
Applied image preprocessing to increase the object detection rate under different lighting and contrast conditions. With the preprocessing method, the object detection can be performed more accurately under different conditions, such as images taken by different cameras.  
Below shows the result comparison between before and after the image preprocessing method for the implementation of support vector machine.

<img src="/images/preprocess.png" width="800" height="220">

## UNet Architecture
In this project, an UNet architecture was implemented to segment the background and the graphene flakes.   
- Click [here](https://www.youtube.com/watch?v=2nHsBEQst7g) to check the Youtube tutorial!   
- The architecture is as follows. [cite]  
- Images to demonstrate.



A modified loss function is defined to improve the result of the training model. 




## Support Vector Machine(SVM) Method
SVM is a supervised learning model used for regression and classification analysis. Once the background and the graphene flakes were separated using the U-Net architecture, the SVM method was implemented. Here the SVM algorithm was implemented with different kernels including Gaussian kernel, polynomial kernel and linear kernel to demonstrate the differences. Kernel function was picked to suit the problem. 


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

## Test the robustness of the model
Graphene images can be captured using different kind of camera which might cause color shift and results in incorrect detection of the graphene. And thus, in order to make sure that the graphene flakes captured with different camera can be detected correctly, image preprocessing was applied to resolve this issue. We shifted the color channel intentionally and applied the image preprocessing  on those images. The following plot shows the relationship between the detection rate and the number of the shifted pixel values.
Raw image is the original image. True mask is the ground truth image.   
<img src="/images/raw.png" width="350" height="200"><br />    

Modified images are the images after shifting the pixel values(ranges from 30, 25,...-25,-30). Preprocessed the modified images are the images applied with data preprocessing.  

(a) is the original images with the shifted pixel values; (b) is the images after applying image preprocessing on (a); (c) is the prediction results from the SVM
<img src="/images/shift_plus.png" width="650" height="400"><br />  
<img src="/images/shift_minus.png" width="650" height="400"><br />   
<img src="/images/Detection_rate.png" width="550" height="400"><br />   

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
[13]Y. Cao, V. Fatemi1, S. Fang, K. Watanabe, T. Taniguchi, E. Kaxiras, and P. Jarillo-Herrero1, “Unconventional superconductivity in magic-angle graphene superlattices,” vol. 556, pp. 43–50, 2018.
[14] J. G. G. S. Ramos, T. C. Vasconcelos, and A. L. R. Barbosa, “Spin-to- charge conversion in 2d electron gas and single-layer graphene devices,” vol. 123, 2018.
[15] F. Bovolon, L. Bruzzone, and L. Carlin, “A novel technique for subpixel image classification based on support vector machine,” IEEE TRANSACTIONS ON IMAGE PROCESSING, vol. 19, pp. 2983–2999, 2010.
[16] K. Sakthivel, R. Nallusamy, and C. Kavitha, “Color image segmentation using svm pixel classification image,” IEEE TRANSACTIONS ON IMAGE PROCESSING, vol. 8, pp. 1924–1930, 2014.
[17] X.-Y. Wang, T. Wang, and J. Bu, “Color image segmentation using pixel wise support vector machine classification,” Pattern Recognition, vol. 44, pp. 777–787, 2011.
[18] O. Chapelle, P. Haffner, and V. N. Vapnik, “Support vector machines for histogram-based image classification,” IEEE TRANSACTIONS ON NEURAL NETWORKS, vol. 10, pp. 1055–1064, 1999.
[19] T. M. Cover, “Geometrical and statistical properties of systems of linear inequalities with application in pattern recognition,” vol. 14, pp. 326– 334, 1965.
[20] N. Cristianini and J. Shawe-Tayloi, “An introduction to support vector machines,” 2000.
