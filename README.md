# Machine Learning-based Automatic Graphene Detection with Color Correction for Optical Microscope Images

- [Video demonstration](https://www.youtube.com/watch?v=mkgfjlF0cMw)
- [Article](http://arxiv.org/abs/2103.13495)
- Note: Please feel free to contact me at huiyingsiao@gmail.com if you are interested in using this tool to find monolayer and bilayer graphene on the substrates!

## Abstract
Graphene serves critical application and research purposes in various fields. However, fabricating high-quality and large quantities of graphene is time-consuming and it requires heavy human resource labor costs. In this paper, we propose a Machine Learning-based Automatic Graphene Detection Method with Color Correction (MLA-GDCC), a reliable and autonomous graphene detection from microscopic images. The MLA-GDCC includes a white balance (WB) to correct the color imbalance on the images, a modified U-Net and a support vector machine (SVM) to segment the graphene flakes. Considering the color shifts of the images caused by different cameras, we apply WB correction to correct the imbalance of the color pixels. A modified U-Net model, a convolutional neural network (CNN) architecture for fast and precise image segmentation, is introduced to segment the graphene flakes from the background. In order to improve the pixel-level accuracy, we implement a SVM after the modified U-Net model to separate the monolayer and bilayer graphene flakes. The MLA-GDCC achieves flake-level detection rates of 87.09\% for monolayer and 90.41\% for bilayer graphene, and the pixel-level accuracy of 99.27\% for monolayer and 98.92\% for bilayer graphene. MLA-GDCC not only achieves high detection rates of the graphene flakes but also speeds up the latency for the graphene detection process from hours to seconds.



## Dataset 
The graphene image dataset was prepared with a mechanical exfoliation method on several SiO2 substrates. All the images were taken using an optical microscope with x20, x50 and x100.   
The original dataset was provided by [Nanoelectronics lab](http://nano.phys.ncku.edu.tw) at National Cheng Kung University.


## Labeling 
The labeling software used for this project is [Labelbox](https://labelbox.com).   
A generated json file from Labelbox will then converted into a [COCO dataset](https://cocodataset.org/#home) for use.


## Complete process of the MLA-GDCC.
- Fig. 1 shows the process of MLA-GDCC. First, we apply a WB method to the original images to correct the color shifts caused by different cameras. Second, the modified U-Net architecture is used to segment the regions of interest from the background in the white-balanced images. Third, a multiplier is implemented to mask the background from the white-balanced images. Last but not least, a SVM is implemented to classify the monolayer and bilayer graphene.
<img src="/images/comple_process.png" width="1000" height="320">


## Image Preprocessing method
Applied image preprocessing to increase the object detection rate under different lighting and contrast conditions. With the preprocessing method, the object detection can be performed more accurately under different conditions, such as images taken by different cameras.  
Below shows the result comparison between before and after the image preprocessing method for the implementation of support vector machine.

<img src="/images/preprocess.png" width="800" height="220">

## UNet Architecture  
- Click [here](https://www.youtube.com/watch?v=2nHsBEQst7g) to check the Youtube tutorial!   
In order to segment both the single layer and the bilayer graphene flakes from the background more accurately, we modify the traditional U-Net architecture [29] by adding 5 convolutional layers in the decoder to generate more training parameters from the images. The inputs of the modified U-Net are RGB microscopic images of graphene on the SiO2 substrates, and all the input images are resized into 256 × 256 pixels. The outputs of the modified U-Net are the detected masks containing both monolayer and bilayer graphene flakes, which provides pixel-level probability maps for the graphene devices. 


## SVM: Color Pixels Classifier
A multiplier is implemented to mask the background in the white-balanced images as shown in Fig. 1. Only the regions of interest on the white-balanced images are left at the output of the multiplier. The limited features on the graphene dataset prevent the modified U-Net from classifying the monolayer and the bilayer graphene. Therefore, we use a SVM to identify and classify the monolayer and bilayer graphene flakes more accurately. SVM is a machine learning algorithm used to find the hyper-plane based on the dataset characteristics, this algorithm aims to maximize the margin of the hyper-plane and the data points in a linear or a nonlinear case.
Here we extract the RGB pixel values separately and assign the pixel values to indicate the layers of the graphene flakes. The features for the SVM algorithm include the mean values RGB pixel values and the mean RGB pixel values of the mode background pixel values. By using the detection masks from the U-Net, we use the histogram to select the peak value of the background for each R, G and B channel. Next, we average the three background RGB pixel values to obtain the mean RGB pixel value as one of the two features for the SVM algorithm. With the implementation of the SVM algorithm, we can discriminate two classes in our dataset. The two classes here are the monolayer and bilayer graphene mean RGB pixel values. The SVM algorithm does not require a lot of training data. Although the training dataset is small, which in our case is 246 images, the model achieves high detection rates of the monolayer and bilayer graphene flakes.


## Pixel-level evaluation metrics
| Method       | precision(%) | F1 score(%) | recall(DR)(%) | accuracy(%) |
| :---         |      ---:       |          ---:   |          ---: |          ---: |
| Monolayer    | 51.01           | 59.03           |70.05          |99.27         |
| Bilayer |  70.37              |      75.38       | 81.16         |98.92          |

  
- Demonstration of SVM results(GT: ground truth; G: green; R: red)  
<img src="/images/SVM.png" width="600" height="600"><br />  


## White Balance Method (WB)
Due to different types of the cameras used by different research groups to capture the graphene images, color shifts can happen on the images. Therefore, we implement a WB correction in the MLA-GDCC method to correct the color shifts. We implement a Gray world algorithm [4, 7, 17] as the WB method to make the average of all channels a gray image. With the WB correction, models can accurately detect the graphene on the color-shifted microscopic images captured by different cameras.    
   
With the implementation of the Gray world algorithm, the results show that the SVM model can detect the graphene flakes and identify the layers with high detection rates. The detection results of the color-shifted images are shown below. In both figures part (a) shows the images shifted with different numbers of pixel values in the blue channel. Part (b) shows the application of the Gray world algorithm on the images in part (a). Part (c) shows the output from the MLA-GDCC. 

- Fig 2. (a) shows the original images with pixel values in the blue channel added with the corresponding values on the images. (b) shows the images after applying white balance on (a). (c) shows the detection results from the SVM.  
<img src="/images/shift_plus.png" width="650" height="400"><br />    


- Fig 3. (a) shows the original images with the pixel values in the blue channel subtracted with the correspond- ing values on the images. (b) shows the images after applying white balance on (a). (c) shows the detection results from the SVM.  
<img src="/images/shift_minus.png" width="650" height="400"><br />   
<img src="/images/Detection_rate.png" width="550" height="400"><br />   


## References
[1] H. Alquran, I. A. Qasmieh, A. M. Alqudah, S. Alhammouri, E. Alawneh, A. Abughazaleh, and F. Hasayen. The melanoma skin cancer detection and classification using support vector machine. pages 1–5, 2017.  
[2] A. Balandin, S. Ghosh, W. Bao, I. Calizo, D. Teweldebrhan, F. Miao, and C. N. Lau. Superior thermal conductivity of single-layer graphene. Nano Letters, 8(3):902–907, 2008.  
[3] F.Bovolon,L.Bruzzone,andL.Carlin.Anoveltechniqueforsubpixelimageclassificationbasedonsupportvector machine. IEEE TRANSACTIONS ON IMAGE PROCESSING, 19:2983–2999, 2010.  
[4] G. Buchsbaum. A spatial processor model for object colour perception. 310:1–26, 1980.  
[5] Y. Cao, V. Fatemi1, S. Fang, K. Watanabe, T. Taniguchi, E. Kaxiras, and P. Jarillo-Herrero1. Unconventional
superconductivity in magic-angle graphene superlattices. 556:43–50, 2018.  
[6] O. Chapelle, P. Haffner, and V. N. Vapnik. Support vector machines for histogram-based image classification. IEEE
TRANSACTIONS ON NEURAL NETWORKS, 10:1055–1064, 1999.  
[7] G. Chen and X. Zhang. A method to improve robustness of the gray world algorithm. pages 250–255, 2015.  
[8] T. M. Cover. Geometrical and statistical properties of systems of linear inequalities with application in pattern
recognition. 14:326—-334, 1965.  
[9] N. Cristianini and J. Shawe-Tayloi. An introduction to support vector machines. 2000.  
[10] P. Gadosey, Y. Li, E. Agyekum, T. Zhang, Z. Liu, P. Yamak, and F. Essaf. Sd-unet: Stripping down u-net for segmentation of biomedical images on platforms with low computational budgets. Diagnostics, 10(2), 2020.  
[11] S. Hossain, R. Mou, M. Hasan, and and M. Razzak S. Chakraborty. Recognition and detection of tea leaf’s diseases using support vector machine. 2018 IEEE 14th International Colloquium on Signal Processing and Its Applications (CSPA), pages 150–154, 2018.  
[12] J.Hu,D.Li,Q.Duan,Y.Han,G.Chen,andX.Si.Fishspeciesclassificationbycolor,textureandmulti-classsupport vector machine using computer vision. Computers and Electronics in Agriculture, 88:133–140, 2012.  
[13] Y. Huang, E. Sutter, N. N. Shi, J. Zheng T. Yang, D. Englund, H-J Gao, and P. Sutter. Reliable exfoliation of large-area high-quality flakes of graphene and other two-dimensional materials. ACS Nano, 9(11):10612—-10620, 2015.  
[14] M. Islam, Anh Dinh, K. Wahid, and P. Bhowmik. Detection of potato diseases using image segmentation and multiclass support vector machine. pages 1–4, 2017.  
[15] JMercer. Functions of positive and negative type and their connection with the theory of integral equations. 209:415—-446, 1909.  
[16] V. Khryashchev, R. Larionov, A. Ostrovskaya, and A. Semenov. Modification of u-net neural network in the task of multichannel satellite images segmentation. 2019 IEEE East-West Design Test Symposium (EWDTS), pages 1–4, 2019.  
[17] Y. Kim, J-S Lee, A. Morales, and S-J Ko. A video camera system with enhanced zoom tracking and auto white balance. IEEE Transactions on Consumer Electronics, 48:428–434, 2002.  
[18] D. P. Kingma and J. Ba. Adam: A method for stochastic optimization. 2014.  
[19] M. C. Lemme, T. J. Echtermeyer, M. Baus, and H. Kurz. A graphene field-effect device. IEEE Electron Device
Letters, 28:282–284, 2007.  
[20] Y-M Lin and P. Avouris. Strong suppression of electrical noise in bilayer graphene nanodevices. Nano Letters,
8(8):2119–2125, 2008.  
[21] A. Luican, G. Li, A. Reina, J. Kong andR. R. Nair, K. S. Novoselov, A. K. Geim, and E. Y. Andrei. Single-layer
behavior and its breakdown in twisted graphene layers. Phys. Rev. Lett., 106:126802, Mar 2011.  
[22] L. Luo, D. Chen, and D. Xue. Retinal blood vessels semantic segmentation method based on modified u-net. pages
1892–1895, 2018.  
[23] S. Masubuchi and T. Machida. Classifying optical microscope images of exfoliated graphene flakes by data-driven
machine learning. npj 2D Materials and Applications, 3(1):1–7, 2019.  
[24] EdwardMcCannandMikitoKoshino.Theelectronicpropertiesofbilayergraphene.ReportsonProgressinPhysics,
76(5):056503, 2013.  
[25] K.S.Novoselov,A.K.Geim,S.V.Morozov,D.Jiang,Y.Zhang,S.V.Dubonos,I.V.Grigorieva,andA.A.Firsov.
Electric field effect in atomically thin carbon films. Science, 306(5696):666–669, 2004.  
[26] K. S. Novoselov, A. Mishchenko, A. Carvalho, and A. H. Castro Neto. 2d materials and van der waals heterostruc-
tures. Science, 353(6298):aac9439, 2016.  
[27] T. Ohta, A. Bostwick, T. Seyller, Karsten Horn, and Eli Rotenberg. Controlling the electronic structure of bilayer
graphene. Science, 313:951–954, 2006.  
[28] J. G. G. S. Ramos, T. C. Vasconcelos, and A. L. R. Barbosa. Spin-to-charge conversion in 2d electron gas and
single-layer graphene devices. 123, 2018.  
[29] O. Ronneberger, P.Fischer, and T. Brox. U-net: Convolutional networks for biomedical image segmentation.
9351:234–241, 2015.  
[30] Eisuke S. Masubuchi, and Watanabe, Yuta Seo, Shota Okazaki, Takao Sasagawa, Kenji Watanabe, Takashi
Taniguchi, and Tomoki Machida. Deep-learning-based image segmentation integrated with optical microscopy
for automatically searching for two-dimensional materials. npj 2D Materials and Applications, 4(1):1–9, 2020.  
[31] R. Saito, M. Hofmann, G. Dresselhaus, A. Jorio, and M. S. Dresselhaus. Raman spectroscopy of graphene and
carbon nanotubes. Advances in Physics, 60(3):413–550, 2011.  
[32] Y. Saito, K. Shin, K. Terayama, S. Desai, M. Onga, Y. Nakagawa, Y. Itahashi, Y. Iwasa, M. Yamada, and K. Tsuda.
Deep-learning-based quality filtering of mechanically exfoliated 2d crystals. npj Computational Materials, 5(1):1–6,
2019.  
[33] K. Sakthivel, R. Nallusamy, and C. Kavitha. Color image segmentation using svm pixel classification image. IEEE
TRANSACTIONS ON IMAGE PROCESSING, 8:1924–1930, 2014.  
[34] H. Seo, C. Huang, M. Bassenne, R. Xiao, and L. Xing. Modified u-net (mu-net) with incorporation of object-
dependent high level features for improved liver and liver-tumor segmentation in ct images. IEEE Transactions on
Medical Imaging, 39(5):1316–1325, 2020.  
[35] A. Sevastopolsky. Optic disc and cup segmentation methods for glaucoma detection with modification of u-net
convolutional neural network. 27:618–624, 2017.  
[36] C. Shearer, A. Slattery, A. Stapleton, J. Shapter, and C. Gibson. Accurate thickness measurement of graphene. Nanotechnology, 27(12):125704, feb 2016.  
[37] A.O.Vuola,S.U.Akram,andJ.Kannala.Mask-rcnnandu-netensembledfornucleisegmentation.pages208–212, 2019.  
[38] X-Y. Wang, T. Wang, and J. Bu. Color image segmentation using pixel wise support vector machine classification. Pattern Recognition, 44:777–787, 2011.
[39] F. Xia, T. Mueller, Y-M Lin, A. Valdes-Garcia, and P. Avouris. Ultrafast graphene photodetector. Nature Nanotech- nology, 4:839—-843, 2009.  
[40] Y. Yang, C. Feng, and R. Wang. Automatic segmentation model combining u-net and level set method for medical images. Expert Systems with Applications, 153:113419, 2020.  
[41] Q. Yao, Z. Guan, Y. Zhou, J. Tang, Y. Hu, and B. Yang. Application of support vector machine for detecting rice diseases using shape and color texture features. 2009 International Conference on Engineering Computation, pages 79–83, 2009.  
[42] W. Yao, Z. Zeng, C.Lian, and H. Tang. Pixel-wise regression using u-net and its application on pansharpening. 312:364–371, 2018.  
[43] Y.Zhang,andC.GiritT-TTang,Z.Hao,M.Martin,A.Zettl,M.Crommie,Y.Shen,andF.Wang.Directobservation of a widely tunable bandgap in bilayer graphene. Nature, 459:820–823, 2009.  
