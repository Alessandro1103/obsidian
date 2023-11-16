Date: 2023-11-07
Time: 10:39
Tags: #ML #Università 
Up: [[ML]]

---
# Homework1

- Fare un codice approssimativo
- 

---
# Soluzione

## Introduction
The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. The first dataset contains 50000 elements with 100 parameters.  

## First Test
The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1 dataset, tested over the blindTest1.csv. I didn't think about a pre-processing method, I could use a dataset standardization, or check the outliners to see if I could improve the distribution to get a better solution. Avoiding every kind of semplification, or improvements, I just run the code over the DecisionalTree() method, obtaining a proper solution, with sufficient evaluation. Just to verify the correct evaluation over the test, I measured the accuracy: 0.975736. It's quite good considering the condition already explined before. 

Another method to evaluate a classification problem is using a confusion matrix, to understand, beyond the correct result, if there are more or less false positive or false negative and if the model tends to confuse 2 or more classes. The matrix shows that even the evaluation is good, but it can be improved.
![[Pasted image 20231107110218.png]]

---
# References
