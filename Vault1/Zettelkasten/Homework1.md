Date: 2023-11-07
Time: 10:39
Tags: #ML #Università 
Up: [[ML]]

---
# Homework1


## Introduction

The problem presented is a classification problem, over 2 dataset to train the model, and 2 test, to evaluate the result obtained by the training. To do so, it is necessary to begin importing a large amount of python tools from the python library: including, Pandas, Numpy, Pyplot, Swaborn Istance, Training/Testing/Splitting (from SKLearn), etc.


### First dataset
The first dataset contains 50000 elements with 100 parameters. 

### Second dataset


## First Test (decisionTree)

The first step taken to work on this homework works on finding a solution. To see if everything was well managed I try to train and test the dataset over a random method. The test is made over the dataset1. In particular I split the data to create 2 set, one for the training and one for the test. Doing so, I could evaluate the results, in order to generate an appropriate model for the blind test. 
In the first try I didn't think about a pre-processing method, I could use a dataset standardization, or check the outlines to see if I could improve the distribution to get a better solution. Avoiding every kind of simplification, or improvements, I just run the code over the DecisionTree() method, obtaining a proper solution. Just to verify the correct evaluation over the test, I measured the mean accuracy: 0.976036, which is very close to the average result I was obtaining, I take this as point of start to improve the code. It's quite good considering the condition already explained before. 

## Decision Tree

Since the results were fine, I'm able to add some features and came up with a better solution. The first thing that was added was a well-functioning classification evaluation. A first to measure accuracy, useful to represent the proportion of true positives among all instances predicted to be positive by the model. It gives the percentage of cases correctly classified as belonging to that class out of all cases classified as belonging to that class.
A second measure that includes accuracy, but splits it into the 10 classes to better understand where the errors occur. We can even see the recall, or true positive rate, which indicates how well the model is capturing all positive instances of a class. In this measure, we also have the f1-score, which is the harmonic mean of precision and recall, and is particularly useful for obtaining a measure between accuracy and recall. 
I also calculated the confusion matrix to understand where the errors are, if there are more false positives or false negatives. Finally, I even did a cross-validation to get a more robust evaluation.

In addition to the obvious fitting of the model and creating a predictor variable, I did some pruning of the tree. In particular, I performed a rule post-pruning to avoid over fitting, and rule pruning can lead to simpler models by eliminating branches of the decision tree that do not contribute significantly to model performance. To do so, I had to infer the decision tree from the training set, growing the tree until the training data is fit as well as possible. Then convert the learned tree into an equivalent set of rules, generalize each rule by removing preconditions and sort the pruned rules by their estimated accuracy.

I conducted pre- and post-pruning performance measurements to ascertain how the outcomes vary.

To have a better comparison and to understand which method is better suited for this problem, I tried to find a solution using the following methods. 

## Kernel methods

With kernel methods, we don't need to represent each instance of the input space, but we will define a kernel function between them: Linear, Polynomial, RBF, Sigmoid. In this case, the model is not well adaptable. Since I do not know beforehand which methods perform better with which parameters, I can use GridSearch, which is able to find the best hyper parameters for this problem through cross-validation. 
In order to get a prediction I had to apply the best parameters to the original model. 
The code run is very simple, it has no special features. 

## Gaussian methods

Within the realm of regression models, I explored the Gaussian method to ascertain if a stochastic process could yield diverse results. In probabilistic regression, test predictions take the form of predicted values with associated uncertainties. In practical applications, one often seeks a reliable prediction, achievable as the solution to a decision problem. This problem involves predicted values and a specification of the consequences tied to making particular predictions, encapsulated within the loss function. After careful consideration, 

I needed to introduce an attribute to the Logistic Regression model because the algorithm was struggling to converge to a single result. In optimization terms, convergence signifies that the algorithm has stabilized, and further iterations do not yield substantial improvements in the model parameters. In logistic regression, convergence happens when the optimization algorithm discovers the model coefficient values that minimize the loss function.
In particular, I set a limit on the number of iterations. 


# Pre-Processing methods

After organizing all the models, I had to think about pre-processing methods.
My initial focus was on standardization of the features. This method was implemented to bring uniformity to the scale of each feature, a critical factor for the proper functioning of various machine learning algorithms. By standardizing features to have a mean of 0 and a standard deviation of 1, I aimed not only to facilitate model convergence but also to enhance the model's resilience against scale-related biases and outliers.
Addressing the challenge of missing data, I opted for a straightforward and effective method-mean imputation. This involved replacing missing values with the mean value of their respective features. This approach ensures that the dataset retains its statistical characteristics, minimizing the impact of missing values on subsequent analyses. I actually noticed that there were no missing values in the first data set, but I did not know what the blind set might present.

# Evaluations

All the methods I used have the same accuracy or in generale score evaluation to get a good comparison over the results:

## Decision Tree vs Decision Tree



---
# References
