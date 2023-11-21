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
In the first try I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of simplification, or improvements, I just run the code over the DecisionTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the mean accuracy: 0.976036, which is very close to the average result I was obtaining, I take this as point of start to improve the code. It's quite good considering the condition already explained before. 

Since the results were fine, I'm able to add some features and came up with a better solution. The first thing that was added was a well-functioning classification evaluation. A first to measure accuracy, useful to represent the proportion of true positives among all instances predicted to be positive by the model. It gives the percentage of cases correctly classified as belonging to that class out of all cases classified as belonging to that class.
A second measure that includes accuracy, but splits it into the 10 classes to better understand where the errors occur. We can even see the recall, or true positive rate, which indicates how well the model is capturing all positive instances of a class. In this measure, we also have the f1-score, which is the harmonic mean of precision and recall, and is particularly useful for obtaining a measure between accuracy and recall. 
I also calculated the confusion matrix to understand where the errors are, if there are more false positives or false negatives. Finally, I even did a cross-validation to get a more robust evaluation.

In addition to the obvious fitting of the model and creating a predictor variable, I did some pruning of the tree. In particular, I performed a rule post-pruning to avoid over fitting, and rule pruning can lead to simpler models by eliminating branches of the decision tree that do not contribute significantly to model performance. TO d

I conducted pre- and post-pruning performance measurements to ascertain how the outcomes vary.

---
# References
