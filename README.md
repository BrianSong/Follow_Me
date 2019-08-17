# Udacity_RoboND_Follow_Me
*In this project, A quadrotor can identify a female target hero from crowd and follow her. The identification task is achieved by semantic segmentation in fully convolutional networks (FCN). Moreover, the quadrotor is controlled by PID that will be also discussed in this `README.md`.*

**Python with TensorFlow and Keras** are used for implementing this project and **Unity** is used for simulating the enviroment.

This is a `README` that includes all the key points and how I addressed each one.

**Steps to complete the project:**  


1. Clone the project repo [here](https://github.com/udacity/RoboND-DeepLearning-Project.git).
2. Fill out the TODO's in the project code.
3. Optimize your network and hyper-parameters.
4. Train your network and achieve an accuracy of 40% (0.40) using the Intersection over Union IoU metric which is final_grade_score at the bottom of your notebook.


## 1. Network Architecture

The final version network architecture of the fully convolutional networks (FCN) in this project is shown below:

![Network_Architecture](image/Network_Architecture.PNG)

To begin with, after the input is the six separable convolution layers that extracts features from an input image, each followed by a batch normalization. The reason to choose the separate convolutional layer instead of normal convolutional layer is that, the separate convolutional layer cam reduce the number of parameters needed, thus increasing efficiency for the encoder network. 

The followed batch normalization is based on the idea that, instead of just normalizing the inputs to the network, we normalize the inputs to layers within the network. It's called "batch" normalization because during training, we normalize each layer's inputs by using the mean and variance of the values in the current mini-batch. It has the advantages that: 1. Networks train faster; 2. Allows higher learning rates; 3. Simplifies the creation of deeper networks and 4. Provides a bit of regularization.

After the encoder section (six separable convolution layers) is the 1\*1 convolution. We can't use fully connected layers here because we need to preserve spatial information (every pixel in an image have to be classified).

Next is the decoder section where the feature maps are upsample using bilinear interpolation three times. Skip connection via concatenation after upsampling allows to use data from the input high resolution image. Two additional separable convolution layers are applied after concatenation and introduce nonlinearity by ReLu built-inside. After every separable convolution a batch normalization is also applied to provide better convergence and normalization. 

In the end, the final convolution provides classification probabilities for every pixel for semantic segmentation.

## 2. Neural network's parameters
### 2.1 Epoch
### 2.2 Learning Rate
### 2.3 Batch Size
