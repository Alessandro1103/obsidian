Start: 2023-12-28 at 17:24
Tags: #Report
Up: 

---
# Homework2

# Introduction


For this homework, I had to work in Colab and in the Linux space. Colab could not perform the "play" due to an error with the gymnasium. In Linux, or more specifically my PC, I couldn't provide a great GPU to run such a large amount of code.

![[Pasted image 20240112170509.png|300]]

![[Pasted image 20240112165911.png|300]]

# Common Elements

## Libraries
Here I present a number of libraries I use in the code, I have selected the most important ones. First, I use TensorFlow, a core library for machine learning. I use it mainly for building and training neural network models. cv2, which is an OpenCV library for Python, which I use for tasks related to seeing and understanding images and videos. To use Colab, I had to use google.colab: It provides functionality to access and manage files in Google Drive from my Colab notebooks. Keras Tuner helps me to tune the hyperparameters of my neural networks. Scikit-Learn helps me to evaluate the performance of my classification models.

## CNN
A CNN, or Convolutional Neural Network, is a type of deep learning algorithm that I can use to analyse visual images. It's designed to automatically and adaptively learn spatial hierarchies of features from images. This works really well for image classification problems because a CNN can pick up on patterns like edges, textures and shapes to determine what's in an image. There are a few main components that make up a CNN, different layers that can improve or degrade the performance of the model:
- Convolutional layers: apply a series of filters to the input to detect features such as edges, colours or other visual aspects.
- Activation functions: After each convolution, an activation function is applied to introduce non-linearities into the model, allowing it to learn more complex patterns.
- Pooling layers: These layers reduce the spatial dimensions (width and height) of the input volume for the next convolutional layer. This helps to reduce the computational load, number of parameters and overfitting.
- Dense layers: After several convolutional and pooling layers, the high-level reasoning in the neural network is done via fully connected layers. Neurons in a fully connected layer have full connections to all activations in the previous layer.
- Batch normalisation layers: These layers normalise the input layer by adjusting and scaling the activations.
- Flatten layers: These layers are used to flatten the input into a one-dimensional array for the transition from the convolution/pooling layers to the fully connected layers.

## Metrics
In my image classification task, I'm working with a dataset where the distribution of images across classes is quite uneven. Specifically, I have 133 images in class 0, 275 in class 1, 406 in class 2, a large number of 1896 images in class 3, and only 39 images in class 4. This uneven distribution means I can't just rely on accuracy to gauge my model's performance because it might just be good at predicting the class with the most images (class 3 in my case) and not so good with the others.
This is why I'm looking at precision, which helps me understand how accurate my model is when it predicts a particular class. For example, if my model predicts an image as class 4, precision tells me how likely it is that this image really belongs to class 4. This is especially crucial for classes like 0 and 4, which have fewer images.
Then there's recall, which shows me how good my model is at identifying all the images from a particular class. For classes with fewer images, like class 0 and class 4, a high recall means my model is good at finding these rare instances, which is essential.
I'm also using the F1-Score, which combines precision and recall into one metric. It gives me a balanced view of how well my model is doing overall, considering both how many correct predictions it makes and how many instances of each class it can correctly identify.
Finally, the confusion matrix is really useful. It shows me where my model is getting things right and where it's confusing two classes. This detailed breakdown is especially helpful for seeing how my model handles the classes with fewer images, like class 0 and class 4. By looking at all these different measures, I can get a much clearer and fairer picture of my model's true performance across all classes.

## Optimizer

# Model 1

# Model 2

# Conclusion

# Bibliography
