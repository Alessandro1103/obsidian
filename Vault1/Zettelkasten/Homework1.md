Date: 2023-11-07
Time: 10:39
Tags: #ML #Università 
Up: [[ML]]

---
# Homework1

- [ ]  Fare una stampa del dataset totale e prendere alcune features come esempio e discussione per il kernel method


## Introduction

The project's objective was to experiment with a dataset in order to test machine learning algorithms' ability to identify patterns within the data. The main aim was to create and hand in a detailed report that presents findings obtained from studying the selected dataset, and systematically analyzing the algorithms used. 
The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. To do so, it is necessary to begin importing a large amount of python tools from the python library: including, Pandas, Numpy, Pyplot, Swaborn Istance, Training/Testing/Splitting (from SKLearn), etc.

In the initial phase of this project, focused on the analysis of the first dataset, I want to test how well the decision tree respects a stochastic method. In the middle of this comparison, I can test some knowledge I've acquired during the course that I'm curious about. For example, the difference in performance between the generative and the logistic methods. In the second part, i.e. on data set 2, I would check the difference between using a processing method and not using it. In order not to repeat myself, I would try some other methods.

## First Dataset

The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1. In particular I split the data to create 2 set, one for the training and one for the test. Doing so, I could evaluate the results, in order to generate an appropriate model for the blind test. 
In the first try I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of simplification, or improvements, I just run the code over the DecisionTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the mean accuracy: 0.976036, which is very close to the average result I was obtaining, I take this as point of start to improve the code. It's quite good considering the condition already explained before. 

### Pre-Processing methods

After organizing all the models, I had to think about pre-processing methods.
My initial focus was on standardization of the features. This method was implemented to bring uniformity to the scale of each feature, a critical factor for the proper functioning of various machine learning algorithms. By standardizing features to have a mean of 0 and a standard deviation of 1, I aimed not only to facilitate model convergence but also to enhance the model's resilience against scale-related biases and outliers.
Addressing the challenge of missing data, I opted for a straightforward and effective method-mean imputation. This involved replacing missing values with the mean value of their respective features. This approach ensures that the dataset retains its statistical characteristics, minimizing the impact of missing values on subsequent analyses. I actually noticed that there were no missing values in the first data set, but I did not know what the blind set might present.

### Evaluations methods

When testing machine learning algorithms, various methods and measurements are important in order to assess their efficacy. The accuracy metric is fundamental as it evaluates a model's overall performance by measuring the correctness of predictions on a test dataset. The confusion matrix goes further than measuring accuracy. It breaks down the number of predicted true positives, true negatives, false positives, and false negatives, offering insights into how the model performs on each individual class. The classification report adds to this by giving a detailed overview of the precision, recall, and F1 score for each class, giving a better understanding of how the model behaves across different categories. To ensure a reliable evaluation amid dataset variations, we employ cross-validation techniques. These encompass methods such as ShuffleSplit and k-fold cross-validation, enabling an extensive evaluation of model efficiency under different circumstances. This comprehensive evaluation tactic seeks to engender a complete comprehension of machine learning algorithms' capabilities and inadequacies when handling convoluted datasets.

### Decision Tree

Since the results were fine, I'm able to add some features and came up with a better solution. The first thing that was added was a well-functioning classification evaluation. A first to measure accuracy, useful to represent the proportion of true positives among all instances predicted to be positive by the model. It gives the percentage of cases correctly classified as belonging to that class out of all cases classified as belonging to that class.
A second measure that includes accuracy, but splits it into the 10 classes to better understand where the errors occur. We can even see the recall, or true positive rate, which indicates how well the model is capturing all positive instances of a class. In this measure, we also have the f1-score, which is the harmonic mean of precision and recall, and is particularly useful for obtaining a measure between accuracy and recall. 
I also calculated the confusion matrix to understand where the errors are, if there are more false positives or false negatives. Finally, I even did a cross-validation to get a more robust evaluation.

In addition to the obvious fitting of the model and creating a predictor variable, I did some pruning of the tree. In particular, I performed a rule post-pruning to avoid over fitting, and rule pruning can lead to simpler models by eliminating branches of the decision tree that do not contribute significantly to model performance. To do so, I had to infer the decision tree from the training set, growing the tree until the training data is fit as well as possible. Then convert the learned tree into an equivalent set of rules, generalize each rule by removing preconditions and sort the pruned rules by their estimated accuracy.

I conducted pre- and post-pruning performance measurements to ascertain how the outcomes vary.

To have a better comparison and to understand which method is better suited for this problem, I tried to find a solution using the following methods. 

### Decision Tree (pruned) vs Decision Tree (not pruned)
I want to use both the SimpleImputer and StandardScaler methods. The fascinating thing we can do with decision trees is to choose between pre-pruning and post-pruning. We can't predict which method is better when the tree needs this kind of operation. So the first result, which I've already checked, is about accuracy, it's easy to check how this value increases during the second test, over the pruned tree. In fact, it goes from ??? to ???, but how do the false positives and false negatives react to this change? I'm curious to see if the already known classes that are confused with each other improve or get worse. I expect that these values won't get better, I if I don't have a good classification if I can describe them better, why should they improve since I'm generalizing?

First Confusion matrix:


After the pruning:


### Gaussian methods (generative vs logistic)

Within the realm of regression models, I explored the Gaussian method to ascertain if a stochastic process could yield diverse results. In probabilistic regression, test predictions take the form of predicted values with associated uncertainties. In practical applications, one often seeks a reliable prediction, achievable as the solution to a decision problem. This problem involves predicted values and a specification of the consequences tied to making particular predictions, encapsulated within the loss function. I thought a discriminative solution might be a better solution because I didn't have to generate any other samples, and for large dataset it suits well. So I started to run the logistic regression code, and in the end I was curious to see if I had made the right choice, so I looked for a solution for a generative model. 
I also needed to introduce an attribute to the Logistic Regression model because the algorithm was struggling to converge to a single result. In optimization terms, convergence signifies that the algorithm has stabilized, and further iterations do not yield substantial improvements in the model parameters. In logistic regression, convergence happens when the optimization algorithm discovers the model coefficient values that minimize the loss function. 


As I expected, the logistic regression performs much better than the generative. In fact, the general accuracy of the logistic is: 0.989069, instead the accuracy obtained from the generative method is: 0.968889. This difference can also be seen in the classification report, which, as I said, describes the accuracy across all the different classes:

This is Generative solution:
![[Pasted image 20231123230229.png|400]]

This is Logistic solution:
![[Pasted image 20231123230326.png|400]]

So, logistic model is performing better overall, with a higher accuracy compared to generative model. Both models face challenges with Class 4, but the drop in performance is more noticeable in Model 2.

Considering the nature of logistic regression (a discriminative model) and the generative model, the results align with the typical strengths and weaknesses of these approaches. Logistic regression, being discriminative, often performs well in classification tasks, especially when the decision boundary is complex. On the other hand, generative models might struggle if the underlying data distribution is complex or if there's a mismatch between the assumed distribution and the true distribution of the data.

## Second dataset

### Decision Tree

In this case, I would just like to observe the variance in the outcomes obtained from an algorithm run on both a standardized dataset and an unmodified dataset. I also employed a technique that limits or caps values to set boundaries, which mitigates the impact of extreme values on the data. The processed information is trimmed, which signifies that numbers below the lowest point are altered to the lowest limit, and numbers beyond the highest point are modified to the highest limit. This halts unusual values from affecting the analysis whilst preserving the primary data distribution. So in this case the pre processing methods are more and more aggressive.

### Kernel methods

With kernel methods, we don't need to represent each instance of the input space, but we will define a kernel function between them: Linear, Polynomial, RBF, Sigmoid. In this case, the model is not well adaptable. Since I do not know beforehand which methods perform better with which parameters, I can use GridSearch, which is able to find the best hyper parameters for this problem through cross-validation. 
In order to get a prediction I had to apply the best parameters to the original model. 
The code run is very simple, it has no special features. 

### Decision Tree vs Decision Tree pre processed

![[Pasted image 20231128153015.png]]
![[Pasted image 20231128153024.png]]

Both confusion matrices show high values on the diagonal (true positives), indicating that the model performs well in correctly classifying instances for each class. Comparing the two confusion matrices (with and without pre processing), it seems that pre processing hasn't dramatically changed the model's performance. The patterns of correct and incorrect classifications appear similar in both cases. Taking into account the cross-validation, we obtain by shuffling all the data in 5 parts and then taking the mean of all the accuracies: 

Accuracy of the model: 0.974859
Accuracy of the pre processed model: 0.974523



---
# References
