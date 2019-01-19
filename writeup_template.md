# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/visualization.jpg "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/placeholder.png "Traffic Sign 1"
[image5]: ./examples/placeholder.png "Traffic Sign 2"
[image6]: ./examples/placeholder.png "Traffic Sign 3"
[dangerous]: ./web/dangerous_curve_right.png "dangerous_curve_right"
[keep_right]: ./web/keep_right.png "keep_right"
[no_passing]: ./web/no_passing.png "no_passing"
[priority_road]: ./web/priority_road.png "priority_road"
[roundabout]: ./web/roundabout.png "roundabout"
[exploratory]: ./exploratory.png "Exploratory"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a histogram showing how the data is distributed between 43 labels


![alt text][exploratory]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

### Preprocessing
As part of the preprocessing step, I combined all the dataset and reshuffled to generate the training, validation and testing datasets using the train_test_split function. Follwed by normalizing the data so the data has close to zero mean and equal variance. In future, I would like to experiment with data augmentation to generate additional data. As seen in the above histogram, the distribution of data between various labels is uneven.
We could use data augmentation to balance it out and that would help produce even better results

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 3x3     	| 1x1 stride, same padding, outputs 32x32x64 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 16x16x64 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x16	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, valid padding, outputs 5x5x16		|
| Flatten       		| outputs 400  									|

| Fully connected		| outputs 120  									|
| Softmax				|           									|
|						|												|
|						|												|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, 
I used an adam optimizer
with a batch size of 256
learning rate of 0.002
running it for 10 epochs.


#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:

* validation set accuracy of 97.4% 
* test set accuracy of 97.5%

It's an iterative approach :
* The LeNet-5 architecture.Since I already had an implementation for the LeNet-5 architecture
* Just went ahead with that in the beginning by just modifying the image channel depth to 3. Later, more fully connected layers were added to the bottom and a dropout layer with a 0.9 dropout was also included in between these fully connected layers. But this did not help increase the accuracy, so I reverted back to the original architecture
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
* What helped was shuffling and normalizing of data in the pre-processing stages. The learning rate hyperparameter was increased from 0.001 to 0.002 for faster convergence 
*  I observed that with the default learning rate, it required more number of epochs to reach the optimum accuracy.

* The validation set accuracy is very close to the test set accuracy, the model is working well. In future, data augmentation coupled with a droupout layer should help increase the accuracy.

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web are in web Folder
![alt text][dangerous]
![alt text][keep_right]
![alt text][no_passing]
![alt text][priority_road]
![alt text][roundabout]


The last image might be difficult to classify because of its low contrast ratio.



#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image     			        |     Prediction	   					| 
|:-----------------------------:|:-------------------------------------:| 
| Dangerous curve to the right	| Dangerous curve to the right	 		| 
| No passing	       			| No passing							|
| Keep right	        		| Keep right							|
| Priority road	           		| Priority road					 		|
| Roundabout mandatory	   		| Roundabout mandatory					|


The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 97.2%

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 8th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a Dangerous curve to the right sign (probability of 1.0),The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.00         			| Dangerous curve to the right					| 
| 1.00     				| No passing									|
| 1.00 					| Keep right									|
| 0.95	      			| Roundabout mandatory   		 				|
| 1.00				    | Priority road      							|


### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


