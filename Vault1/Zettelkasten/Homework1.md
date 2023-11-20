Date: 2023-11-07
Time: 10:39
Tags: #ML #Università 
Up: [[ML]]

---
# Homework1


---
# Soluzione

## Introduction
The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. The first dataset contains 50000 elements with 100 parameters. 

## First Test
The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1. In particular I split the data to create 2 set, one for the training and one for the test. Doing so, I could evaluate the results, in order to generate an appropriate model for the blind test. 
In the first try I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of simplification, or improvements, I just run the code over the DecisionalTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the accuracy: 0.976036, which is very close to the average result I was obtaining, I take this as point of start to improve the code. It's quite good considering the condition already explained before. 

I applied standardization to ensure that all features share similar scales, with a mean centered around 0 and a standard deviation of 1. This choice was motivated by the need to enhance the performance and convergence of different machine learning algorithms, especially those that can be influenced by variations in the scale of input features.

Using Classification report I can access to more accurate performance information getting:
![[Pasted image 20231116230144.png]]



---
# References
