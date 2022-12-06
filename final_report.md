# Final Report
## Introduction / Background 
The snake is a widely spread species across the world. Although many snake species do not possess fatal venom, several snake classes have poison in their venom that can impair human health severely. The symptoms include tissue death swelling, bleeding and destruction of blood cells, nerve damage and even death. According to a report, between 81,000-138,000 people die from snakebite each year. Many more survive but may do so with lasting disabilities or disfigurement. The staggering statistics of causality from snakebite makes it even more imperative to identify which snakes are harmless and which are venomous. 

## Problem Definition 🌟
To help counteract this growth in poison by snakes, we aim to use machine learning supervised learning to evaluate the image of snakes and identify venomousness. We could do binary classification on our goal. The models our group utilized are *convolutional Neural Network* and *Support Vector Machine*.


## Data Collection 🌟
The dataset is sourced from [Kaggle](https://www.kaggle.com/code/mpwolke/venomous-non-venomous). It contains 2044 snake images of size 400 * 400 with them labeled venomous or non-venomous. It includes a variety of snake species, in total 715 venomous and 1060 non venomous. We divided the total dataset into a ratio around 87% trained data and 13% data for testing.


## Methods 🌟
### Data Processing and Cleaning 🌙
We collect our data, the images of snakes, from a trusted source (kaggle.com), and those images are well-labeled as venomous and non-venomous snakes and are all 3 x 400 x 400 in size.
One thing our group taken serious consideration on is the balance of the data group used for training. If we feed mainly non-venomous data into training, our model trained may not be sufficiently representative. The model could be confused when testing on venomous snake image. We prevented this from happening through dividing training dataset into 3 : 2 ratio of non-venomous : venomous. 
Our goal is to transform the images into the form of 1 x 40 x 40  that we can utilize in the following classification process.
First we create four sets, which are training data, training label, testing data and testing label. In this process, we first transform the colored images to black and white images and then transform the size of image to 1 x 40 x 40. Then we add each data to the set they belong to and add  corresponding labels to the label set. We assign the non-venomous snake as label 0 and the venomous snake as label 1. Finally, we use torch.stack and torch.tensor on the data set and label set separately to put them into a single matrix, so that we can use CNN on.

The dataset we have also comes in as one training set and one test set. The training/test ratio is roughly 1.5 : 8.5. 

### Convolutional Neural Network 🌙
To classify our data, we created and trained a **Convolutional Neural Network**. 
The CNNs are a class of neural networks that is suitable for classifying visual data by filtering data with convolutional layers and polling etc. 
For convolutional layers which involve a kernel with the image to produce a feature map, which is used to present several features within the image. We used a 3x3 kernel and sought 64 filters in our model.
Since the image may produce non-linear components when we perform gradient transitions between color and pixels etc. so in order to account for the non-linearity, we utilize the leaky_relu function in torch.nn.functional as the activation function to map the negative values to a near zero range.
Then we use MaxPool2d function with 4x4 kernel and stride of 4 to downsample our images into a smaller one such that we can solve the problem that features exist at different precise locations in images. The MaxPool2d classifies the images over the locations of the most prominent features, and therefore we can only account for variances there. After applying this function, we have the rows and columns reduced by one-quarter while keeping the most of our features.
We also apply the Dropout function as a regularization method in our model that will randomly drop some of the neurons of the network. With this function, the model will avoid overfitting.
Finally we end the model by flatten the layer and then apply the fully connected layer to the previously flattened layer. Then we can convert the data resulting from the previous convolution layers and pooling layers to a one-dimensional vector and predict which category of snake the data should belong to.
For optimizer, we used Adam with a learning rate of 0.001, and we used cross entropy as our loss function to help us understand how well our model performs. In the later update, we incorporate Adagrad(), Adamax() and Nadam() and get accuracy 1.00, 0.999 and 0.99 respectively. 

### Support Vector Machine
support vector machine (SVM) is a type of supervised learning algorithm that can be used for both classification and regression tasks. The goal of an SVM is to find the best decision boundary, or hyperplane, that can separate the data points in a given dataset into the desired classes. This makes SVM to be our priority choice as our goal is to do binary classification over snake venomous based on image. 
We then transform the data points in the input space into a higher-dimensional feature space using a mathematical function called a kernel. This transformation allows the data points to be separated more easily in the higher-dimensional space, even if they are not linearly separable in the original input space. Once our data points have been transformed into the 64 x 64 dimension space, the SVM algorithm finds the hyperplane that maximizes the margin, or distance, between the data points of the different classes. This hyperplane is called the maximum-margin hyperplane. It is important to note that the SVM algorithm does not only find one decision boundary, but a whole family of decision boundaries that are all parallel and equally distant from the data points of the different classes.
After that, we feed in test data and run 25 epochs on each testing data set. At first, the accuracy was not satisfactory, so we applied optimizer Maxpool, Conv2D and Nadam() to reach an average accuracy of 65.5%. 



## Results and Discussion 🌟
We used the accuracy and loss of the predictive model to measure its performance.
For calculating accuracy, we counted the number of correctly predicted labels divided by the total number of samples. For calculating loss, we used the cross entropy loss function for the neural network built in torch.nn. We then plotted the accuracy and loss for the training set and testing set.
On the CNN model, as can be seen from the accuracy plots, the model has a better performance on the training dataset than the testing dataset, which is not surprising. It has an average training accuracy of 85.5% and an average testing accuracy of 65%. Similarly, the training loss is much lower than the testing loss, which are 0.21 and 2.75, respectively. 
Having such a high testing loss is not satisfying and indicates that our predictive model is not working well. With our algorithm being theoretically correct, we believed that the main reason for such a result is the use of Grayscale on the images in the beginning of data preprocessing, which caused much information lost during the transformation. 
As we are about to utilize different training models on our dataset, we plan to reduce our loss value in a couple of ways. We will use dimension reduction methods during data preprocessing, and use regularization in our algorithm to avoid overfitting; we may also use k-fold cross validation to average test errors.
For the SVM part, our testing accuracy averaged to 65% and training accuracy was 85.5%. 
There are several reasons behind the low accuracy we achieved on the SVM model. Firstly, our dataset is unbalanced, with significantly more non-venomous snake data than venomous snake. As a result, our training data is mainly composed of non-venomous snakes, impairing the accuracy on identifying venomous snakes. Secondly, in the image used for testing, some of the image is messed up with background: the snake is perfectly faded in the background, causing difficulty to identify them even by human eye! Some others have a miscellaneous background, of similar texture as snake skin which added up to the difficulty of recognizing.


## Conclusion 🌟
In summary, while support vector machines can be used for image classification, they are typically not as effective as convolutional neural networks, which are specifically designed to process grid-like data such as images. The convolutional and pooling layers in a CNN are key components that allow it to effectively extract features from images and make accurate predictions. The distinguishment between CNN and SVM can also be seen on the accuracy we achieved, as we use the same testing dataset. The accuracy of CNN model is higher than SVM model. However, as to the aspect of computational efficiency, SVM took less time to train than CNN. 


<img src="https://github.com/Isobel0911/Isobel0911.github.io/blob/bdb053fbdf777ad43f335d445606267ca9c144a6/assets/css/Screenshot%202022-11-12%20205712.jpg" style="display: block; margin: auto;" />
<img src="https://github.com/Isobel0911/Isobel0911.github.io/blob/bdb053fbdf777ad43f335d445606267ca9c144a6/assets/css/Screenshot%202022-11-12%20205754.jpg" style="display: block; margin: auto;" />
<img src="https://github.com/Isobel0911/Isobel0911.github.io/blob/bdb053fbdf777ad43f335d445606267ca9c144a6/assets/css/Screenshot%202022-11-12%20205809.jpg" style="display: block; margin: auto;" />
<img src="https://github.com/Isobel0911/Isobel0911.github.io/blob/bdb053fbdf777ad43f335d445606267ca9c144a6/assets/css/Screenshot%202022-11-12%20205821.jpg" style="display: block; margin: auto;" />

## Contribution Table 🌟
**Haosheng Wu/Mingxuan Nie/Ruochen Shu**: Implement the supervised CNN model

**Haosheng Wu**: Clean and preproccess the data

**Dian Yang/Jiaying Deng**:Anaylsis the output of model and accuracy, evaluate current model
