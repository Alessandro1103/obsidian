Date: 2023-11-07
Time: 10:39
Tags: #ML #Università 
Up: [[ML]]

---
# Homework1

- [ ] Fare un codice approssimativo
- [ ] Fare dei grafici per vedere la distribuzione del dataset
- [ ] Fare un controllo sugli outlines
- [ ] Controllare il bilanciamento delle classi di output
- [ ] Grafici di correlazione tra le features
- [ ] Matrice di correlazione per vedere pattern tra le features

---
# Soluzione

## Introduction
The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. The first dataset contains 50000 elements with 100 parameters.  

## First Test
The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1. In particular I split the data to create 2 set, one for the training and one for the test. Doing so, I could evaluate the result, in order to generate an appropriate model for the blind test. I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of semplification, or improvements, I just run the code over the DecisionalTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the accuracy: 0.975976. It's quite good considering the condition already explained before. 

Another method to evaluate a classification problem is using a confusion matrix, to understand, beyond the correct result, if there are more or less false positive or false negative and if the model tends to confuse 2 or more classes. The matrix shows that the evaluation is good, but it can be improved.

\[\[1694 0 7 1 1 0 4 0 11 2\] 
 [ 2 1602 0 0 0 1 2 0 4 13] 
 [ 8 1 1619 12 6 3 2 2 1 0] 
 [ 2 1 8 1547 12 57 8 3 0 4] 
 [ 1 1 5 14 1614 9 3 5 0 0] 
 [ 0 0 5 71 10 1670 2 10 0 1] [ 1 2 4 11 6 2 1696 0 0 1] 
 [ 2 1 2 2 8 19 0 1583 0 1] [ 3 1 0 0 0 1 1 0 1630 3] 
 [ 1 7 0 2 0 0 0 2 2 1595\]\]





---
# References
