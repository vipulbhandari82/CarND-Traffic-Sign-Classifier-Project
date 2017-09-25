# Traffic Sign Recognition

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my project code 

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic signs data set:

The size of training set is ? 34799 
The size of test set is ? 126300
The shape of a traffic sign image is ? 32x32x3
The number of unique classes/labels in the data set is ? 43
####2. Include an exploratory visualization of the dataset.
Here is an exploratory visualization of the data set. It is a bar chart showing how the Data

![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/Classes.png)


![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/download.png)

### Design and Test a Model Architecture
A lot of classes had files as few as 250 and some of the common classes had huge
amount of images. I added few methods described in geometric transformations for
opencv. I used translation, perspective transformation and rotation to enhance 
the dataset.

 Further, I increased any classes with number less than 1000 to have a minimum
 of 1000 images using these transformations. I did this so that real scenario of
 camera distance, disturbed or slanted signs, angle of camera etc. can be simulated.

#### Translation
 ![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/Translation.png)
#### Perspective Transformation
 ![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/perspective_transformation.png)
#### Rotation
 ![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/rotation.png)

This is how the data looked after this data agumentation.

![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/download2.png)

Further, As described in original Lenet paper, I converted the image to YUV format
and equalized histogram on a global level and then on a local level to enhance
contrast ofthe image. Then we normalized the image so that the machine learns 
a distance from a zero mean as input. Standardization is pretty commmon in ML.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

It is very similar to example in our studies of Lenet but I introduced a two layers
of dropout near the end.

Layer 1: Convolutional. Input = 32x32x3. Output = 28x28x6.

Activation.

Max Pooling. Input = 28x28x6. Output = 14x14x6.

Convolutional. Output = 10x10x16.

Activation.

Max Pooling. Input = 10x10x16. Output = 5x5x16.

Flatten. Input = 5x5x16. Output = 400.

Droput Probability 0.75

Fully Connected. Input = 400. Output = 120.

Relu

Dropout Probability 0.75

Epochs: I used 20 Epochs even though I think 10 may have been enough as the network quickly went to low validation error and remained there.

Learning rate: Standard rate of 0.01 was used. Though I experimented with 0.1 and 0.001 but both caused issues.

Optimiser: Adama optmizer was used as it uses veloccity and momentum and is one of the fastest on block.

Batch size : I used a batch size of 32 and I had an old gpu at home with only 2GB memory. Anything above failed with a memory error.


I started out with BW images and reached around 90% validation accuracy but it 
seemed to me I was discarding important information. After, reading the LEcun paper
I implemented the equilization enhancement of images which took me to 94% validation accuracy.
After enhancing the dataset with transformation to reduce overfitting and adding 
some droput layers at the very end, I was able to go over 97.2% validation set accuracy.

My final model results were:

validation set accuracy of ? 97.2 percent

test set accuracy of ? 95.9 percent

### Test a Model on New Images

I extracted some 5 images from the web, the first three were clear with bacground 
greenery and my network was able to recognize those images. But, I choose two images
from classes with few samples. Secondly, I made the background white. As I suspected, 
the network failed on on these images.

![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/webset.png)

![alt text](https://github.com/vipulbhandari82/CarND-Traffic-Sign-Classifier-Project/blob/master/webset2.png)

As you can see the model had a accuracy of 60% and as can be seen by the softmax images,
my NN is quite sure in first three images but fails in fourth images where the probabilties
are not that high. Even though NN is sure in fifth image as per softmax probability butit 
seemed to have learnt on shape circlerather than correct sign. So, as is evident some
improvements to this network is needed.






