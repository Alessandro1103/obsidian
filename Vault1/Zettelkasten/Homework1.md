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
![[Pasted image 20231116181213.png]]

To improve the algorithm and prevent overfitting, one approach I can try, specifically for the decision tree model is to cut the subtree rooted at a specific node. I provided an algorithm that implements post-pruning of a decision tree using cost-complexity pruning. Then I evaluated the accuracy of each pruned tree on the test set and then identifying the alpha value associated with the highest accuracy.

``` python
ccp_path = model.cost_complexity_pruning_path(X_train, y_train)
ccp_alphas, impurities = ccp_path.ccp_alphas, ccp_path.impurities
pruned_trees = []
for ccp_alpha in ccp_alphas:
	pruned_tree = DecisionTreeClassifier(random_state=1127, ccp_alpha=ccp_alpha)
	pruned_tree.fit(X_train, y_train)
	pruned_trees.append(pruned_tree)
test_accuracies = [tree.score(X_test, y_test) for tree in pruned_trees]
best_alpha = ccp_alphas[np.argmax(test_accuracies)]
```

In fact, I got an improvement, even if very small. I went from 0.975976 to 0.976937 accuracy. To get this result I had to wait 31m 52.4s, which was unexpected and defenetly too much for the result obtained.


---
# References
