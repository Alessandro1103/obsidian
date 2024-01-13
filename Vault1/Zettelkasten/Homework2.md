Start: 2023-12-28 at 17:24
Tags: #Report
Up: 

---
# Homework2

# Introduction

In this report I describe the development of a Convolutional Neural Network (CNN) to solve an image classification task in a gym environment. My goal is to understand and predict the actions of a racing car based on input images. I have been given a dataset of 96x96 colour images, sorted into folders by action ID. In particular, the meaning of each class is as follows
- 0: do nothing
- 1: steer left
- 2: steer right
- 3: accelerate
- 4: brake
I will evaluate my models using key performance, in particular the F1-score, and I will conduct a thorough analysis over each models on different parameters. This analysis will be presented through clear visualizations and a detailed discussion of the results.

The code presented might be particular because it's not designed to work on a single space. I had to work on both Colab and Linux because one lacks a feature of the other, in particular I used Colab for its GPU disponibility, and Linux for its compatibility with the gymnasium library. To do this, I had to write and run the classification problem in Colab space, storing the best model classified by F1 score. Then use this best model, in the file of the game environment to see if the model it's acceptable or not.

# Common Elements

## Data augmentation

![[Pasted image 20240112170509.png|300]] ![[Pasted image 20240112165911.png|300]]

The image demonstrates a data augmentation technique involving cropping and resizing, applied to images used in training a machine learning model. This model is designed to learn the behavior of a racing car in a Gym environment. The cropping process is targeted to remove irrelevant parts of the image, such as a black bar at the bottom, which might be a UI element or an unnecessary part of the environment. This ensures that the model focuses on the most crucial aspects for decision-making, like the track boundaries and the car's position on the road. After cropping, the image is resized back to its original dimensions. This step is crucial to maintain a consistent input size, a requirement for effectively training the convolutional neural network (CNN).


## Libraries
Here I present a number of libraries I used in the code, selecting the most important ones. First, I used TensorFlow, a core library for machine learning. My main use for it was in building and training neural network models. Then there was cv2, which is an OpenCV library for Python, used for tasks related to seeing and understanding images and videos. To use Colab, I had to utilize google.colab: It provided functionality to access and manage files in Google Drive from my Colab notebooks. Keras Tuner was instrumental in helping me tune the hyperparameters of my neural networks. Lastly, Scikit-Learn was crucial in evaluating the performance of my classification models.

## CNN
A CNN, or Convolutional Neural Network, is a type of deep learning algorithm that I could use to analyze visual images. It was designed to automatically and adaptively learn spatial hierarchies of features from images. This works exceptionally well for image classification problems because a CNN could pick up on patterns like edges, textures, and shapes to determine what's in an image. There were a few main components that made up a CNN, different layers that could improve or degrade the performance of the model:

- Convolutional layers: These layers applied a series of filters to the input to detect features such as edges, colors, or other visual aspects.
- Activation functions: After each convolution, an activation function was applied to introduce non-linearities into the model, allowing it to learn more complex patterns.
- Pooling layers: These layers reduced the spatial dimensions (width and height) of the input volume for the next convolutional layer. This helped to reduce the computational load, number of parameters, and overfitting.
- Dense layers: After several convolutional and pooling layers, the high-level reasoning in the neural network was done via fully connected layers. Neurons in a fully connected layer had full connections to all activations in the previous layer.
- Batch normalization layers: These layers normalized the input layer by adjusting and scaling the activations.
- Flatten layers: These layers were used to flatten the input into a one-dimensional array for the transition from the convolution/pooling layers to the fully connected layers.

These factual components, like convolutional layers and activation functions, were intrinsic to how a CNN functioned and remained consistent in their roles and operations.

## Metrics
In my image classification task, I was working with a dataset where the distribution of images across classes was quite uneven. Specifically, I had 133 images in class 0, 275 in class 1, 406 in class 2, a large number of 1896 images in class 3, and only 39 images in class 4. This uneven distribution meant I couldn't just rely on accuracy to gauge my model's performance because it might have just been good at predicting the class with the most images (class 3 in my case) and not so good with the others.

This was why I looked at precision, which helped me understand how accurate my model was when it predicted a particular class. For example, if my model predicted an image as class 4, precision told me how likely it was that this image really belonged to class 4. This was especially crucial for classes like 0 and 4, which had fewer images.

Then there was recall, which showed me how good my model was at identifying all the images from a particular class. For classes with fewer images, like class 0 and class 4, a high recall meant my model was good at finding these rare instances, which was essential.

I also used the F1-Score, which combined precision and recall into one metric. It gave me a balanced view of how well my model was doing overall, considering both how many correct predictions it made and how many instances of each class it could correctly identify.

Finally, the confusion matrix was really useful. It showed me where my model was getting things right and where it was confusing two classes. This detailed breakdown was especially helpful for seeing how my model handled the classes with fewer images, like class 0 and class 4. By looking at all these different measures, I was able to get a much clearer and fairer picture of my model's true performance across all classes.

## Optimizer
Of all the optimisers, I had chosen Adam, the most popular optimiser, because it combines the advantages of two other extensions of stochastic gradient descent: AdaGrad and RMSProp. I decided to stick with only one optimiser because changing the optimiser could be difficult, as dynamically changing the code often introduces different errors. Although other optimisers, such as SGD, could be used for fitting linear classifiers and neural networks, using them would have required writing different codes for each optimiser. I preferred Adam because it seemed to me to be the best option. Although SGD is usually faster, it is less stable than more sophisticated optimisers because it updates the model for each training example, rather than for the whole dataset.


# Model 1

In the first model, I just wanted to define a simple architecture and see how the model responded to varying the epochs and learning rate.

In the first tries I was confused because the accuracy was not good over the whole model (about 0.5-0.6%), so I spent a lot of time changing the architecture and finding the best combination between the layers. At the beginning I did not prepare all the code to understand how the dataset was balanced, so since I wrote the classification report I was thinking about some error in the dataset. After reviewing the size of the datasets I understood how the code was performing so badly and why increasing the epochs did not improve the accuracy.  

This model uses convolutional layers to extract features from the input images, followed by max-pooling to reduce dimensionality. It includes batch normalisation and activation layers to stabilise and speed up training. The use of a residual connection helps to train deeper networks by allowing gradients to flow through the network more effectively. Finally, fully connected layers and a softmax output layer are used for classification. After several trials and some research, I decided to use a residual network, known for its "skip connections", which allow the input of one layer to be added directly to the output of a subsequent layer.  Using ResNets allows us to efficiently train deeper networks, which significantly improves my model's ability to handle complex tasks such as image classification. 

As I said, I ran the code over the learning rates in an array from 0.1 to 0.00001, and the epochs over these values 25, 50 and 100. Compiling all these things took a lot of time, I used to go to sleep and leave the computer running until the morning when the compilation was done. In this situation I thought that increasing the learning rate and the epochs might give better results. It didn't, as I'll see later.
It's interesting how at the first operation i got:
![[Pasted image 20240113072315.png|300]]
I thought there were some bugs in the code. Fortunately, the last iteration had some more realistic graphics:
![[Pasted image 20240113072446.png|300]]
Not good but more consistent with the accuracy. 

Before showing what the best classification I got is, the thinking behind this ranking about classification does not depend on accuracy, because since the dataset is so unbalanced, it makes no sense to check the overall accuracy, but it might be more useful to understand which class is better classified, etc. So I decided to combine precision and recall using the F1 score, which provides a more balanced measure that captures how well the model performs on both the majority (4th) and minority classes. This makes it a more reliable metric for evaluating model performance in scenarios where the class distribution is skewed.

The best model find in the iterations is:
![[Pasted image 20240113073319.png|300]]
with this report:
Classification Report - LR: 0.0001, Epochs: 25
              precision    recall  f1-score   support
           0   0.270000  0.203008  0.231760       133
           1   0.284722  0.447273  0.347949       275
           2   0.520581  0.529557  0.525031       406
           3   0.788991  0.725738  0.756044      1896
           4   0.000000  0.000000  0.000000        39
    accuracy                       0.633321      2749
   macro avg   0.372859  0.381115  0.372157      2749
weighted avg   0.662601  0.633321  0.645010      2749

The Macro and Weighted Averages in your classification report are good indicators for understanding how your model is performing. The Macro Average treats each class equally, resulting in a lower score of 37.21%, which reflects the model's poor performance on minority classes. On the other hand, the Weighted Average takes into account the class imbalance, showing a higher score of 64.50%. This higher score is primarily due to the model's better performance on the majority class. These averages highlight the impact of class distribution on the model's apparent effectiveness.

From this model, I understood that this kind of classification doesn't need a large number of epochs, because if the number is too large, it is easy to find an overfitting situation, which leads to a less precise situation.


# Model 2

Since from model 1 I understood the ideal number of epochs and the learning rate, it might be a good idea to try to understand better how to make the architecture perform better, since from my human point of view this type of classification can be very difficult, so there is no single answer on how to build a good architecture for evaluating these images. In fact, this model only works in 15 and 25 epochs, iterating on kernel size, number of filters, dropouts, etc. The scoring system is the same as before, I run all the models and take the one that gives the best F1 score.


# Conclusion

# Bibliography
