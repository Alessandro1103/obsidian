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
- [ ] Aggiungere il post-pruning, già scritto in daAggiungere.ipynb
- [ ] 

---
# Soluzione

## Introduction
The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. The first dataset contains 50000 elements with 100 parameters.  

## First Test
The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1. In particular I split the data to create 2 set, one for the training and one for the test. Doing so, I could evaluate the result, in order to generate an appropriate model for the blind test. I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of simplification, or improvements, I just run the code over the DecisionalTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the accuracy: 0.976036, which is very close to the average result I was obtaining, I take this as point of start to improve the code. It's quite good considering the condition already explained before. 

Since I created a base, now I can start to decorate and develop a more complex code.
First of all I want to understand how the data are distributed, so I can represent them in a graphical way with 

Another method to evaluate a classification problem is using a confusion matrix, to understand, beyond the correct result, if there are more or less false positive or false negative and if the model tends to confuse 2 or more classes. The matrix shows that the evaluation is good, but it can be improved.
![[Pasted image 20231116181213.png]]



---
# References
