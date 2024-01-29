Date: 2024-01-25
Time: 15:55
Tags:
Up: 

---
# ML

## Introduction
**What is a Learning Problem**
A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.

**Formal Definition of ML**
Given $f: X \rightarrow Y$ and a dataset $D$, we want to learn $\hat{f}$ such that $\hat{f}(x) \approx f(x)$ for $\forall x \in X \setminus X_D$.



## Notation
$V(b)$ = the true target function that gives optimal solution.
$\hat V(b)$ = the learned function (approximation of V(b) computed by the learning algorithm), alse called weight (w).
$V_{train}(b)$ = the training value obtained at b from the training dataset (which does not contain all the possible variables).

We wish to $\hat V(b) \approx V(b)$ $\forall b \in B/B_d$ù

## LMS (Least mean squared)
"w" is the weight of the learning function, improved by:
$$
error(b) = V_{train}(b) - \hat V(b)
$$
It's the same if we have a set of parameters to describe the learning function:
$$
error(b, \bar w) = |V_{train}(b) - \hat V(b, \bar w)|
$$

And the parameters that have the minimum error are:
$$
\bar w ^* = \underset{\bar{w}}{\text{argmin}} \ error (b, \bar w)
$$
## Types of ML problems
**Supervised**: the dataset is $D: \{(x_i, t_i)^N_{i=1}\}$

with the following labels:
X can be either Discrete or Continuous
Y can be either Regression (continuous) or Classification (discrete)

**Unsupervised**: the dataset is $D: \{(x_i)^N_{i=1}\}$
**Reinforcement**: the dataset is a trajectory of the dynamic system, $D = \{(s_0, a_1, r_1, s_1, \ldots, a_n, r_n, s_n)^N_{i=1}\}$

## Concept Learning
Concept learning is a classification, with $X$ discrete and $Y$ boolean:
$$
C: X\rightarrow Y
$$
$c$ is the target function, and we use the hypothesis $h$ to approximate $c$, and estimate the value of $x$:
$$
D = \{(x_i, c(x_i))^n_{i=1}\}
$$

**Definition**
Concept learning can be viewed as the task of searching through a large space of hypotheses, implicitly defined by the hypothesis representation. The goal of this search is to find the hypothesis that best fits the training examples.

To find the best approximation $h^* \in H$ of the c problem:
1. Define the hypothesis space H
2. Define a performance metric to determine the best approximation
3. Define an appropriate algorithm (selects among all the possible $h_p$ the best one)

**Best solution among hypothesis**:
A hypothesis $h$ is consistent with a set of training examples $D$ of the target concept $c$ if and only if $h(x) = c(x)$ for each training example $(x, c(x))$ in $D$. 

The set of ==consistent== hypothesis is called **version space**: 
$$
VS_{H,D} = \{h \in H |\ h \ is \ consistent\ with\ D\}
$$

There is no best hypothesis in VS. A bigger VS is not better than the small ones (lose of generical power). There is an association between H space and X space:
$$
h_1(x) = 
\begin{cases} 
1 & \text{if } x \in S_{h_1}, \\
0 & \text{if } x \in X / S_{h_1}.
\end{cases}
$$

## Error/Accuracy

The **true error** of a model is the probability that extracting an input value from the input distribution the model will make a mistake respect to the true function:
$$
\text{error}_D(h) = \Pr_{x \in D} [f(x) \neq h(x)]
$$
we can't compute this error, because $f(x)$ (the target function) is unknown.

The **sample error** is the percentage of mistakes that I do in the subset S:
$$
\text{error}_S(h) = \frac{1}{n} \sum_{x \in S} \delta(f(x) \neq h(x))
$$
$f(x)$ is base on a small subset $S$
Note: $\text{accuracy}(h) = 1 - \text{error}(h)$

If $accuracy_S(h)$ is very high, but $accuracy_D(h)$ is poor, then out system would not be very useful.

**Estimation Bias**:
$$
\text{bias(h)} = E_S[\text{error}_S(h)] - \text{error}_D(h)
$$
We hope to get $bias = 0$.
The smaller the set $S$, the greater the expected variance.
For unbias estimate, $h$ and $S$ must be chosen independently.
It needs a practical way to compute the expected value.
Its useful to understand if the hypothesis is strictly dependent on the Sample set (overfitting) or maybe understand if the hypothesis does not represent the sample correctly (underfitting).

We can use the **Confidence Intervals** to compute an interval around the sample error that has some probability that includes the true error. $\text{error}_D(h)$ lies in interval:
$$
\text{error}_S(h) \pm z_N \sqrt{\frac{\text{error}_S(h)(1 - \text{error}_S(h))}{n}}
$$

| $N$% | 50% | 68% | 80% | 90% | 95% | 98% | 99% |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| $z_N$ | 0.67 | 1.00 | 1.28 | 1.64 | 1.96 | 2.33 | 2.58 |

where $N$% is the probability of get $\text{error}_D(h)$

To obtain an **unbiased estimation** $\text{error}_S(h)$ we create a partition of the dataset, compute a hypothesis $h$ using training set $T$ and evaluate $\text{error}_S$ 

**K-Fold Cross Validation**
We split the Dataset in multiple subset, we want each subset to be big enough
$$
\text{error}_{L,D} = \frac{1}{k} \sum_{i=1}^{k} \delta_i
$$
**Confusion Matrix**:

| True Class \ Predicted Class | Yes | No |
| ---- | ---- | ---- |
| Yes | TP: True Positive | FN: False Negative |
| No | FP: False Positive | TN: True Negative |
|  |  |  |

Recall $= \frac{|\text{true positives}|}{|\text{real positives}|} = \frac{TP}{TP + FN}$ \\ ability to avoid false negatives (1 if FN $= 0$) 
Precision $= \frac{|\text{true positives}|}{|\text{predicted positives}|} = \frac{TP}{TP + FP}$ \\ ability to avoid false positives (1 if FP $= 0$)
F1-score $= \frac{2 \cdot (\text{Precision} \cdot \text{Recall})}{(\text{Precision} + \text{Recall})}$
ROC curve 

## Metrics for Regression

**Mean Absolute Error (MAE)**:
$$
\frac{1}{n} \sum_{i=1}^{n} \left| \hat{f}(x_i) - t_i \right|
$$
It's less sensitive to outliers compared to MSE because it treats all errors equally

**Mean Squared Error (MSE)**:
$$
\frac{1}{n} \sum_{i=1}^{n} (\hat{f}(x_i) - t_i)^2
$$
Tends to penalize large errors more significantly than MAE due to the squaring operation

**Root Mean Squared Error (RMSE)**:
$$
\sqrt{\text{MSE}}
$$
**K-Fold Cross Validation**:

Can be extended to regression problems using appropriate metrics.


## Decision Tree

Consider a discrete input space described with $m$ attributes, $X = A_1 \times \ldots \times A_m, \text{ with } A_i \text{ finite}$, and a classification problem for $f:X\rightarrow C$
A **decision tree** is a tree with the following characteristics:
- Each internal node tests an attribute $A_i$
- Each branch denotes a value of an attribute $a_{i,j} \in A_i$
- Each leaf node assigns a classification value $c \in C$

The final tree represents the learned function, and represents classification function by making decisions explicit.
Decision Trees represent a **disjunction of conjunctions** of constraints on the attribute values of instances. Each path from the tree root to a leaf corresponds to a conjunction of attribute tests, and the tree itself to a disjunction of these conjunction.

**ID3 Algorithm**
1. Create a Root node for the tree
2. if all Examples are positive, then return the node Root with label +
3. if all Examples are negative, then return the node Root with label -
4. if Attributes is empty then return the node Root with label = "most common value of Target_attribute in Examples"
5. Otherwise:
	- A $\leftarrow$ the "best" decision attribute for Examples
	- Assign A as decision attribute for Root
	- For each value $v_i$ of A
		- add a new branch from Root corresponding to the test $A = v_i$
		- $Examples_{v_i}$ = subset of Examples that have value $v_i$ for A
		- if $Examples_{v_i}$ is empty then add a leaf node with label =  "most common value of Target_attribute in Examples"
		- else add the tree ID3($Examples_{v_i}$, Target_attribute, Attributes-{A})

With **entropy** we measure the impurity of the data (Impurity = mix of different class). It's used to determine the best attribute for splitting the data at each node. The goal is to reduce the entropy, choosing the attribute that brings less entropy. Minimize entropy is the same as maximizing **information gain**. Information gain is how well an attribute separates data, calculated as difference in data before and after the split.
$$
\text{Entropy}(S) = -p_0 \log_2 p_0 - p_1 \log_2 p_1
$$

==Example==: if we have the set S = \[9+, 5-\] (9 positive examples, 5 negative examples), $\text{Entropy}(S) = -(9/14) \log_2 (9/14) - (5/14) \log_2 (5/14)$

In case of multi-valued target functions (c-wise classification)
$$
\text{Entropy}(S) = \sum_{i=1}^{c} -p_i \log_2 p_i
$$
![[Pasted image 20240127182134.png|300]]

The expected reduction in entropy of S caused by knowing the value of attribute A:
$$
\text{Gain}(S, A) = \text{Entropy}(S) - \sum_{v \in \text{Values}(A)} \frac{|S_v|}{|S|} \text{Entropy}(S_v)
$$
==Example==: if we have for "Wind" that $S_{Weak} = [6+,2-]$ and $S_{Strong} = [3+,3-]$ the gain is the follow:
$$
\text{Gain}(S, \text{Wind}) = \text{Entropy}(S) - \frac{8}{14}\text{Entropy}(S_{\text{Weak}}) - \frac{6}{14}\text{Entropy}(S_{\text{Strong}})
$$

Appling this to all attributes and find the MAX gain.

This algorithm can produce trees that overfit the training examples.
We will say that a hypothesis **overfits** the training examples if some other hypothesis fits the training examples less well actually performs better over the entire distribution of instances

To avoid overfitting the tree should stop growing wen data split not statistically significant, or when the tree full grow prune it (post-prune). If we have examples with some **missing value** we can substitute the value with the most common value.

An example consists of removing the subtree rooted at that node, making it a leaf node, and assigning it the most common classification of the training examples affiliated with that node. Nodes are removed only if the resulting pruned tree performs no worse than the original over the validation set

When there are many values for a node, instead using Gain, we can use **GainRatio**:
$$
\begin{align*}
&\text{GainRatio}(S, A) = \frac{\text{Gain}(S, A)}{\text{SplitInformation}(S, A)} \\
&\text{SplitInformation}(S, A) = - \sum_{i=1}^{c} \frac{|S_i|}{|S|} \log_2 \frac{|S_i|}{|S|}
\end{align*}
$$

ID3 can be modified to take into account attribute costs by introducing a **cost term** into the attribute selection measure, for example in case of medical diagnosis (price 150€) or robotics (cost 23 seconds), we can replace gain with:
$$
\begin{align*}
&\frac{\text{Gain}^2(S, A)}{\text{Cost}(A)} \\
&\frac{2\text{Gain}(S, A) - 1}{(\text{Cost}(A) + 1)^w}
\end{align*}
$$
with $w \in [0,1]$ determines importance of cost.

Another algorithm could be **Random Forest** that considers different trees with variations (different slit, different dataset...)

## Classification as Prob. estimation

Given target function $f: X \rightarrow Y$, dataset $D$ and a new instance $x'$, best prediction $\hat f (x')=v^*$
$$
v^* = \underset{v \in V}{\mathrm{argmax}} \ P(v | x', D)
$$

Given a dataset $D$ and hypothesis space $H$, compute a probability distribution over $H$ given $D$
$$
P(h|D) = \frac{P(D|h)P(h)}{P(D)}

$$
where:
- $P(h)$ = prior probability of hypothesis $h$
- $P(D)$ = prior probability of training data $D$ (normalization factor)
- $P(h|D)$ = probability of $h$ given $D$ (posterior, information we want to extract after we look at the dataset)
- $P(D|h)$ = probability of $D$ given $h$ (likelihood)

We want the most probable hypothesis $h$ given $D$, in other words the **Maximum a posteriori** hypothesis $h_{MAP}$:
$$
h_{\text{MAP}} = \underset{h \in H}{\mathrm{argmax}} \ P(h|D) = \underset{h \in H}{\mathrm{argmax}} \ \frac{P(D|h)P(h)}{P(D)} = \underset{h \in H}{\mathrm{argmax}} \ P(D|h)P(h)
$$
If we assume that all the hypothesis have the same probability then the **Maximum likelihood** $h_{ML}$ is
$$
h_{\text{ML}} = \underset{h \in H}{\mathrm{argmax}} \ P(D|h)
$$

![[Pasted image 20240128011724.png|400]]

As algorithm we can use **Brute Force MAP Hypothesis Learner**, that for each hypothesis $h$ in $H$ calculate the posterior probability getting the $h_{MAP}$. It's *impractical* because we can not iterate over all the possible hypothesis. 

==Example==: there are 3 possible hypothesis $h1$, $h2$, $h3$:
$$
P(h_1|D) = 0.4, \ P(h_2|D) = 0.3, \ P(h_3|D) = 0.3, 
$$
given a new instance, each hypothesis returns these results:
$$
h_1(x) = + \ \ h_2(x) = - \ \ h_3(x) = -
$$
we can say that the most probably classification of $x$ is "-"

Let's consider the **Bayes Optimal Classifier** (the best classifier):
Consider target function $f:X\rightarrow V$, $V = \{v_1, ..., v_k\}$, data set $D$ and a new instance $x \notin D$:
$$
P(v_i|x, D) = \sum_{h \in H} P(v_i|x, h)P(h|D)
$$
so if we want the best class for a new $x$:
$$
v_{OB} = \sum_{h \in H} P(v_i|x, h)P(h|D)
$$
Still *impractical*.

==Example==: 
$$
\begin{align*} 
P(h_1|D) &= 0.4, & P(-|x, h_1) &= 0, & P(+|x, h_1) &= 1 \\ P(h_2|D) &= 0.3, & P(-|x, h_2) &= 1, & P(+|x, h_2) &= 0 \\ P(h_3|D) &= 0.3, & P(-|x, h_3) &= 1, & P(+|x, h_3) &= 0 \\ 
\end{align*}
$$
therefore 
$$
\begin{align*}
&\sum_{h_i \in H} P(+|x, h_i)P(h_i|D) = 0.4 \\
&\sum_{h_i \in H} P(-|x, h_i)P(h_i|D) = 0.6 \\
\end{align*}
$$
and 
$$
v_{\text{OB}} = \underset{v_j \in V}{\mathrm{argmax}} \sum_{h_i \in H} P(v_j|x, h_i)P(h_i|D) = -
$$

Taking the **log of the likelihood function** often results in a convex function that facilitates the optimization. When the function is monotonic (log) the max changes but the argmax remain the same.
$$
h_{\text{ML}} = \underset{h}{\mathrm{argmax}} \ P(D|h) = \underset{h}{\mathrm{argmax}} \ \mathcal{L}(D|h)
$$

If we want to solve the problem without enumerating all the hypothesis we have to consider the *conditionally independent rule*:
$$
P(X, Y|Z) = P(X|Y, Z)P(Y|Z) = P(X|Z)P(Y|Z)
$$
so the best prediction:
$$
\underset{v_j \in V}{\mathrm{argmax}}\ P(v_j|x, D) = \underset{v_j \in V}{\mathrm{argmax}}\ P(v_j|a_1, a_2 \ldots a_n, D)
$$

and on the **Naive Bayes classifier** assumption:
$$
v_{NB} = \underset{v_j \in V}{\mathrm{argmax}}\ P(v_j|D) \prod_i P(a_i|v_j, D)
$$

The algorithm just calculate iteratively $P(v_j|D)$ and the all the $P(a_i|v_j,D)$. The problem is that when we have no attribute, the probability is 0, so we can estimate the probability of a class computing the ratio between all the samples, adding a weight
$$
\begin{align*}
&\hat{P}(v_j|D) = \frac{|\{\langle \ldots, v_j \rangle\}|}{|D|}\\

&\hat{P}(a_i|v_j, D) = \frac{|\{\langle \ldots, a_i, \ldots, v_j \rangle\}|}{|\{\langle \ldots, v_j \rangle\}|}\\
\end{align*}
$$

## Probabilistic models for classification

The goal in classification is to take an input vector x and to assign it to one of K discrete classes Ck where $k = 1, ..., K$. The input space is divided into decision regions whose boundaries are called decision boundaries or decision surfaces. Data sets whose classes can be separated exactly by linear decision surfaces are said to be linearly separable. For regression problems, the target variable $t$ was simply the vector of real numbers whose values we wish to predict. In the case of classification, there are various ways of using target values to represent class labels. 

Given $f : X \to C (X \subseteq \mathbb{R}^d), D = \{ (x_i, c_i) \}_{i=1}^n \text{ and } x \notin D$, estimate:
$$
P(C_i|x,D)
$$

Two families of models:
- Generative: estimate $P(x|C_i)$ and then compute $P(C_i|x)$ with Bayes (called generative because once we know $P(x|C_i)$ we know how to generate new samples.
- Discriminative: estimate $P(C_i|x)$ directly

I can write:
$$
P(C_1|x) = \frac{P(x|C_1)P(C_1)}{P(x)} = \frac{P(x|C_1)P(C_1)}{P(x|C_1)P(C_1) + P(x|C_2)P(C_2)}
$$
and applied to the assumption that $P(x|C_i) = \mathcal{N}(x; \mu_i, \Sigma)$ we obtain:
$$
a = \ln \frac{P(x|C_1)P(C_1)}{P(x|C_2)P(C_2)} = \ln \frac{\mathcal{N}(x; \mu_1, \Sigma)P(C_1)}{\mathcal{N}(x; \mu_2, \Sigma)P(C_2)} = \ldots = w^T x + w_0
$$
![[Pasted image 20240129155503.png|500]]

The image on the left is used to show how the data $x$ is distributed when it is coming from either class $C_1$ or $C_2$. The image on the right the graphic shows the probability of the data belonging to class $C_1$ given the data $x$.

---

# References
