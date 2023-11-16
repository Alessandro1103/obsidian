Date: 2023-11-16
Time: 21:34
Tags:
Up: 

---
# Homework1 (cose da aggiungere)

## Post-Pruning (ci vuole molto)

To improve the algorithm and prevent overfitting, one approach I can try, specifically for the decision tree model is to cut the subtree rooted at a specific node. I provided an algorithm that implements post-pruning of a decision tree using cost-complexity pruning. Then I evaluated the accuracy of each pruned tree on the test set and then identifying the alpha value associated with the highest accuracy.

``` python
precision recall f1-score support 0 0.99 0.98 0.99 1720 1 0.99 0.99 0.99 1624 2 0.98 0.98 0.98 1654 3 0.94 0.94 0.94 1642 4 0.97 0.98 0.97 1652 5 0.95 0.95 0.95 1769 6 0.99 0.98 0.98 1723 7 0.99 0.98 0.98 1618 8 0.99 0.99 0.99 1639 9 0.99 0.99 0.99 1609 accuracy 0.98 16650 macro avg 0.98 0.98 0.98 16650 weighted avg 0.98 0.98 0.98 16650
```

In fact, I got an improvement, even if very small. I went from 0.975976 to 0.976937 accuracy. To get this result I had to wait 31m 52.4s, which was unexpected and defenetly too much for the result obtained.


---
# References

[Post-Pruning|pag83]
