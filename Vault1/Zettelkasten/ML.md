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

Applying this to all attributes and find the MAX gain.

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
the $h_{ML}$ it provides a way to estimate the parameters of a model in such a way that the observed data becomes as probable as possible given those parameters

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
v_{OB} = \underset{v_j \in V}{\mathrm{argmax}} \sum_{h \in H} P(v_i|x, h)P(h|D)
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
we assume:
$$
\underset{v_j \in V}{\mathrm{argmax}}\ P(v_j|x, D) = \underset{v_j \in V}{\mathrm{argmax}}\ P(v_j|a_1, a_2 \ldots a_n, D)
$$

and on the **Naive Bayes classifier** assumption and obtaining $P(a_i|v_j,D)$ by Bayes<:
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
P(C_1|x) = \frac{P(x|C_1)P(C_1)}{P(x)} = \frac{P(x|C_1)P(C_1)}{P(x|C_1)P(C_1) + P(x|C_2)P(C_2)} = \frac{1}{1 + \exp(-a)} = \sigma(a)

$$
and applied to the assumption that $P(x|C_i) = \mathcal{N}(x; \mu_i, \Sigma)$ we obtain:
$$
a = \ln \frac{P(x|C_1)P(C_1)}{P(x|C_2)P(C_2)} = \ln \frac{\mathcal{N}(x; \mu_1, \Sigma)P(C_1)}{\mathcal{N}(x; \mu_2, \Sigma)P(C_2)} = \ldots = w^T x + w_0
$$
![[Pasted image 20240129155503.png|500]]

The image on the left is used to show how the data $x$ is distributed when it is coming from either class $C_1$ or $C_2$. The image on the right the graphic shows the probability of the data belonging to class $C_1$ given the data $x$.

To obtain the **Maximum likelihood** for 2 classes we have:
$$
P(t|\pi, \mu_1, \mu_2, \Sigma, D) = \prod_{n=1}^{N} [\pi \mathcal{N}(x_n; \mu_1, \Sigma)]^{t_n} [(1 - \pi)\mathcal{N}(x_n; \mu_2, \Sigma)]^{(1-t_n)}
$$
What we are obtaining is if the variable $x$ depends on which distribution, not if it belongs to class 1 or 2
maximizing the log likelihood we obtain:
$$
\begin{align*}
&\pi = \frac{N_1}{N} \\
&\mu_1 = \frac{1}{N_1} \sum_{n=1}^{N} t_n x_n \quad &\mu_2 = \frac{1}{N_2} \sum_{n=1}^{N} (1 - t_n) x_n \\
&\Sigma = \frac{N_1}{N} S_1 + \frac{N_2}{N} S_2 \\
\end{align*}
$$
with  $S_i = \frac{1}{N_i} \sum_{x_n \in C_i} (x_n - \mu_i)(x_n - \mu_i)^T, \quad i = 1, 2$
In this way  $\mu_1$ will have only elements from $C_1$ because $t_1$ is equal to 1 only if $x_n$ belongs to $C_1$, viceversa for $\mu_2$. $t$ is no more a vector but it's a matrix ($N \times K$) where each line is 0 except for the correct class (column) where is 1. $\pi$ is a vector, where the sum is equal to 1. $\Sigma$ si the covariance matrix, symmetric so we choose only half.
==Example==:
assume d = 4 (input space), with k = 3 (classes), how many *independent* parameter I have?
$$
\begin{align*}
&\pi = 
\begin{bmatrix}
 \pi_1\\ \pi_2\\ \pi_3
\end{bmatrix}
&\mu_1 = 
\begin{bmatrix}
 \mu_{11}\\ \mu_{12}\\ \mu_{13}\\ \mu_{14}
\end{bmatrix}
&\mu_2 = 
\begin{bmatrix}
 \mu_{21}\\ \mu_{22}\\ \mu_{23}\\ \mu_{24}
\end{bmatrix}
&\mu_3 = 
\begin{bmatrix}
 \mu_{31}\\ \mu_{32}\\ \mu_{33}\\ \mu_{34}
\end{bmatrix}
\\
&\Sigma = 
\begin{bmatrix}
* & 0 & 0 & 0 \\
* & * & 0 & 0 \\
* & * & * & 0 \\
* & * & *  & *
\end{bmatrix}
\end{align*}
$$ So if we consider *independent* parameter, for $\pi$ we have 2 parameter, because we know that the sum is equal to 1 ($3 \ variables - 1\ constrain\ =\  2\ parameters$). For $\mu_i$ that is the $\min$ of the values of the samples: 4, no constraints so the total is 12. From $\Sigma$ since, it's symmetric, we can take just 10 of 16. So the total is 24  

So we obtain the prediction of the new sample:
$$
P(C_1|x') = \sigma(w^T x' + w_0) 
\begin{cases}
> 0.5 \Rightarrow C_1 \\
\leq 0.5 \Rightarrow C_2 \\
\end{cases}
$$
This can be extended to K classes. The general **notation** will become:
$$
\begin{align*}
&P(C_i|x) = \frac{\exp(a_k)}{\sum_j \exp(a_j)} \\
&a_k = w^T x + w_0
&w^T x + w_0 = \begin{pmatrix} w_0 & w \end{pmatrix} \begin{pmatrix} 1 \\ x \end{pmatrix}
\end{align*}
$$
with $X$ a matrix ($N \times d$) of input values, t a vector ($N$) of output values

### Parametric Models

$\mathcal{M}_\theta: P(t|\Theta, D), \quad D = (X, t)$ with the solution ($\Theta$ are just parameters):
$$
\Theta^* = \underset{\Theta}{\mathrm{argmax}}\ \ln P(t|\Theta, X)
$$
and if $\mathcal{M}_\theta$ belongs to the exponential (simplify with "ln") family ($\tilde w$ are parameters of the linear combination)
$$
\tilde w^* = \underset{\tilde w}{\mathrm{argmax}}\ \ln P(t|\tilde w, X)
$$

So a Probabilistic discriminative model, for **Logistic regression** based on maximum likelihood is 
$$
p(t|\mathbf{w}) = \prod_{n=1}^{N} y_n^{t_n} (1 - y_n)^{1-t_n}
$$
with $y_n = p(C_1|\mathbf{x}_n) = \sigma(\mathbf{w}^T \mathbf{x}_n)$
As usual we can define an error function by taking the negative log of the likelihood, which gives the **cross-entropy error** (Maximum likelihood principle):
$$
\begin{align*}
&E(\mathbf{\tilde w}) = - \ln p(t|\mathbf{\tilde w}) = - \sum_{n=1}^{N} [t_n \ln y_n + (1 - t_n) \ln(1 - y_n)] \\
&\tilde{\mathbf{w}}^* = \underset{\tilde{\mathbf{w}}}{\mathrm{argmin}}\ E(\tilde{\mathbf{w}})
\end{align*}
$$
where $y$ as before is defined by parameters($w$), it's a vector for all the prediction I have, so $y_n$ is a scalar. We start with a random w-value, and I can get the E with the formula. Using the gradient I can obtain the direction I want to take to minimize the error, until it gets to 0.
![[Pasted image 20240129200252.png|400]]

This is the gradient and the incrementation:
$$
\begin{align*}
&\nabla E(\tilde{\mathbf{w}}) = \sum_{n=1}^{N} (y_n - t_n) \tilde{x}_n \\
&\tilde{\mathbf{w}} \leftarrow \tilde{\mathbf{w}} - H(\tilde{\mathbf{w}})^{-1} \nabla E(\tilde{\mathbf{w}})
\end{align*}
$$
where $H(\tilde{\mathbf{w}}) = \nabla\nabla E(\tilde{\mathbf{w}})$, and it's called the **Learning rate**.
For **multi-classes Logistic regression**:
$$
P(T|\tilde{\mathbf{w}}_1, \ldots, \tilde{\mathbf{w}}_K) = \prod_{n=1}^{N} \prod_{k=1}^{K} P(C_k|\tilde{x}_n)^{t_{nk}} = \prod_{n=1}^{N} \prod_{k=1}^{K} y_{nk}^{t_{nk}}
$$

The main difference between Logistic regression and regression is that, regression makes elixis over the dataset, Logistic regression separates the data with a line (Log reg. fails when the data are not linearly separable like a donut, we want the Gaussian distribution).

## Linear Classification

Using the **notation** for 2 classes:
$$
\begin{align*}
&y(x) = w^T x + w_0 = \tilde{w}^T \tilde{x}, \text{ with:} \\
&\tilde{w} = \begin{pmatrix} w_0 \\ w \end{pmatrix}, \tilde{x} = \begin{pmatrix} 1 \\ x \end{pmatrix}
\end{align*}
$$
![[Pasted image 20240130104039.png|200]]
for k-classes:
$$
\begin{align*}
&y(x) = \begin{pmatrix}
y_1(x) \\
\vdots \\
y_K(x)
\end{pmatrix} = \begin{pmatrix}
w_1^T x + w_{10} \\
\vdots \\
w_K^T x + w_{K0}
\end{pmatrix} = \begin{pmatrix}
\tilde{w}_1^T \\
\vdots \\
\tilde{w}_K^T
\end{pmatrix} \tilde{x} = \tilde{W}^T \tilde{x}, \text{ with:} \\
&\tilde{W}^T = \begin{pmatrix}
\tilde{w}_1^T \\
\vdots \\
\tilde{w}_K^T
\end{pmatrix}, \text{ i.e.: } \tilde{W} = (\tilde{w}_1, \ldots, \tilde{w}_K)
\end{align*}
$$

When there are multiple classes, a single linear boundary cannot effectively separate all the classes, as there can be regions of ambiguity where a sample could reasonably belong to more than one class:
![[Pasted image 20240130105645.png|200]] ![[Pasted image 20240130105704.png|200]]

The left one is "One versus the rest" which maps $K-1$ binary classifier.
The right one is "One versus one" which maps $\frac{K(K-1)}{2}$ binary classifier.
The correct solution is the **K-class discriminant**:
![[Pasted image 20240130111009.png|200]]

### Least Squares
$$
\begin{flalign*}
&\text{Given } D = \{ (x_n, t_n) \}_{n=1}^N, \text{ find the linear discriminant }& \\ \\
&y(x) = \tilde{W}^T \tilde{x} & \\ \\
&\text{1-of-K coding scheme for } t: x \in C_k \rightarrow t_k = 1, t_j = 0 \text{ for all } j \neq k. & \\
&\text{E.g., } t_n = (0, \ldots, 1, \ldots, 0)^T & \\ \\
&\tilde{x} = \begin{pmatrix}
\tilde{x}_1^T \\
\vdots \\
\tilde{x}_N^T
\end{pmatrix}, \quad T = \begin{pmatrix}
t_1^T \\
\vdots \\
t_N^T
\end{pmatrix} &
\end{flalign*}
$$
The objective is to minimize the error function:
$$
E(\tilde{\mathbf{W}}) = \frac{1}{2} \text{Tr} \left\{ (\tilde{\mathbf{X}}\tilde{\mathbf{W}} - \mathbf{T})^T (\tilde{\mathbf{X}}\tilde{\mathbf{W}} - \mathbf{T}) \right\}
$$
where $T$ is the target value, $X$ are the data and $W$ are the weights. In closed form solution, we can derivate $E(W)$ and resolve it for $W$ obtaining $W = X^\dagger T$ which substituting in the original solution we obtain: 
$$
y(\mathbf{X}) = \tilde{\mathbf{W}}^T \tilde{\mathbf{X}} = \mathbf{T}^T (\tilde{\mathbf{X}}^\dagger) \tilde{\mathbf{X}}
$$

Since now we have $W$ we can calculate all the things
$$
\begin{align*}
&y(x) = \tilde{W}^T \tilde{x} = 
\begin{pmatrix}
y_1(x) \\
\vdots \\
y_K(x)
\end{pmatrix}
&k = \underset{i \in \{1, \ldots, K\}}{\mathrm{argmax}} \{ y_i(x) \}
\end{align*}
$$

![[Pasted image 20240130111333.png|300]]
*Not robust with outliers*

### Perceptron
![[Pasted image 20240130161303.png|300]]
$$
\sigma(x) = 
\begin{cases}
1 & \text{if } w^T x > 0 \\
-1 & \text{otherwise}
\end{cases}
= \text{sign}(w^T x)
$$
The perceptron takes a vector of real valued inputs calculates a linear combination of these inputs, then outputs a 1 if the result is greater than some threshold and -1 otherwise. One way to learn an acceptable weight vector is to begin with random weights, then iteratively apply the perceptron to each training example, modifying the perception weights whenever it misclassifies an example. The change is based one the **Squared Error** (loss function)
$$
E(w) = \frac{1}{2} \sum_{n=1}^N (t_n - o_n)^2 = \frac{1}{2} \sum_{n=1}^N (t_n - w^T x_n)^2
$$
$w^T x_n$ is the prediction that the model does on $x_n$, $t_n$ is the prediction in the dataset. We update $w$:
$$
\begin{align*}
&w_i \leftarrow w_i + \Delta w_i, \\
&\Delta w_i = -\eta \frac{\partial E}{\partial w_i} = \eta \sum_{n=1}^N (t_n - w^T x_n) x_{i,n}
\end{align*}
$$
where $\eta$ is the learning rate. It can be applied in different way:
- Batch mode: Consider all dataset D
$$
\Delta w_i = \eta \sum_{(x,t) \in D} (t - o(x)) x_i
$$
- Mini-Batch mode (best mode, middle via): Choose a small subset S
$$
\Delta w_i = \eta \sum_{(x,t) \in S} (t - o(x)) x_i
$$
- Incremental mode: Choose one sample
$$
\Delta w_i = \eta (t - o(x)) x_i
$$
![[Pasted image 20240130163437.png|200]] ![[Pasted image 20240130163658.png|300]]

The image on the right, describe the training rule:
initial parameter vector $w$ shown as a black arrow, with the corresponding decision boundary (black line). The data pointed in green is misclassified and so its feature vector is added to the current weight vector, giving the new decision boundary, this until we get close enough to the solution

### Fisher's linear discriminant

We have to consider a dimensionality reduction. Consider two classes case, determine $y=w^Tx$ and classify $x \in C_1 \text{ if } y \geq -w_0$, $x \in C_2 \text{ otherwise}$. Adjusting $w$ to find a direction that *maximizes* class separation, $m_i$ represents the mean of the distributions.
$$
m_1 = \frac{1}{N_1} \sum_{n \in C_1} x_n, \quad m_2 = \frac{1}{N_2} \sum_{n \in C_2} x_n
$$
Choose $w$ that maximizes $J(w) = w^T (m_2 - m_1)$, subject to $||w||=1$
![[Pasted image 20240130164814.png|200]]
the elements on the line are the projection of the points. As we can see there is the middle part of the line that overlaps the classes that brings to misclassification. The Fisher idea is to maximize a function that will give a large separation between the projected class, adding a degree of freedom to rotate. First of all we see how $J(w)$ changes:
$$
J(\mathbf{w}) = \frac{\mathbf{w}^T S_B \mathbf{w}}{\mathbf{w}^T S_W \mathbf{w}}
$$
and deriving this, and put it equal to 0, we obtain:
$$
w \propto S_w^{-1} (m_2 - m_1)
$$
$S_w$ is not a skew symmetric function, it's called **scatter matrix**. It's a sort of covariance matrix.
![[Pasted image 20240130165628.png|200]]
Fisher's linear discriminant is given by the function $y=w^T x$ and the classification of new instances is given by $y\geq -w_0$ where:
$$
\begin{align*}
&w = S_W^{-1} (m_2 - m_1) 
&w_0 = w^T m
\end{align*}
$$
$m$ is the global mean.

### support Vector Machines

SVM aims at maximum margin providing for better accuracy, it is also robust to outliers.
![[Pasted image 20240130172017.png|200]]

If we consider a binary classification, where $t_n \in \{+1,-1\}$ and the model is:
$$
y(x) = w^T x + w_0
$$
then:
$$
\exists w, w_0 \text{ s.t. }
\begin{cases}
y(x_n) > 0, & \text{if } t_n = +1 \\
y(x_n) < 0, & \text{if } t_n = -1
\end{cases}
$$
The margin is defined as the smallest distance between the decision boundary and any of the samples. 
$$
\min_{n=1,\ldots,N} \frac{|y(x_n)|}{\|w\|}
$$
We want to maximize the margins of $w$, knowing the dataset $D$ and the hyperplane $h^*: w^{*T} x + w_0^* = 0$:
$$
w^*, w_0^* = \underset{w, w_0}{\mathrm{argmax}} \frac{1}{\|w\|} \min_{n=1,\ldots,N} [t_n(w^T x_n + w_0)]
$$
We can scale all the points until we have $t_n(w^T x_n + w_0)\geq 1$ and the formula becomes:
$$
w^*, w_0^* = \underset{w, w_0}{\mathrm{argmax}} \frac{1}{\|w\|} = \underset{w, w_0}{\mathrm{argmin}} \frac{1}{2}\|w\|^2
$$
When the maximum margin hyperplane $w^*$, $w_0$ is found, there will be at least 2 closest points $x_k^+$ and $x_k^-$:

![[Pasted image 20240130173146.png|170]]               $\begin{align*}&w^{*T} x_{k}^{+} + w_0^* = +1\\ &w^{*T} x_{k}^{-} + w_0^* = -1\end{align*}$ 


So now to resolve $w^*$ (quadratic programming problem) with **Lagrangian** method:
$$
w^* = \sum_{n=1}^N a_n^* t_n x_n
$$
where $a^*$ are Lagrange multipliers: results of the Lagrangian optimization problem. The constraint of Lagrange are:
- $\sum_{n=1}^N a_n t_n =0$ 
- $a_n \geq 0$

then for each $x_n \in D$, either $a^*_n = 0$ or $t_n y(x_n)=1$ (if $t_n y(x_n)>1$ then the data lie over the boundary).
Support vector: $x_k$ such that $t_k \ y(x_n)=1$ and $a_k^*>0$ 
$$
SV = \{ x_k \in D | t_k y(x_k) = 1 \}
$$
To create the border, we consider only the points that are equal to 1, so the outliers are not considered in this choice. The hyperplanes expressed with support vectors (here we are consider to integrate the Lagrangian method inside the orginal formula $y = w^Tx + w_0$):
$$
y(x) = \sum_{x_j \in SV} a_j^* t_j x^T x_j + w_0^* = 0
$$

In conclusion we can say that the SVM is particularly useful when dealing with very **high-dimensional spaces** (we consider few points).

If we have error, we can treat them with **slack variables**;
- $\xi_n = 1$ the sample lies on the decision boundary
- $\xi_n > 1$ the sample will be mis-classified

The solution is not so different:
$$
w^*, w_0^* = \underset{w, w_0}{\mathrm{argmin}} \left( \frac{1}{2} \|w\|^2 + C \sum_{n=1}^N \xi_n \right)
$$
If C is low we give more importance to margins
If C is high we give more importance to constraints

### Non Linear function

![[Pasted image 20240131185041.png|300]]
$$
\begin{align*}
&y(x) = w^T \phi(x) + w_0 \quad \text{(two classes)} \\
&y_k(x) = w_k^T \phi(x) + w_{k0} \quad \text{(multiple classes)}
\end{align*}
$$
The $\phi$ function change the space, it's a transformation function that maps all the point in a linear dimension

## Linear Regression

The model to approximate the target function $f$ is $y(x;w)$. 
In linear model for linear function:
$$
\begin{align*}
&y(x; w) = w_0 + w_1 x_1 + \ldots + w_d x_d = w^T x \\
&\text{with } x = \begin{bmatrix}
1 \\
x_1 \\
\vdots \\
x_d
\end{bmatrix} \text{ and } w = \begin{bmatrix}
w_0 \\
w_1 \\
\vdots \\
w_d
\end{bmatrix}
\end{align*}
$$
The "1" in the vector "x" is used to simply the calculation and put everything as a multiplication of vectors.

![[Pasted image 20240201105553.png|300]]

Using non-Linear function:
$$
\begin{align*}
&y(x; w) = \sum_{j=0}^{M} w_j \phi_j(x) = w^T \phi(x), \\
&\text{with } w = \begin{bmatrix}
w_0 \\
\vdots \\
w_M
\end{bmatrix}, \quad \phi(x) = \begin{bmatrix}
\phi_0(x) \\
\vdots \\
\phi_M(x)
\end{bmatrix}, \quad \text{and } \phi_0(x) = 1.
\end{align*}
$$
Apply for example Polynomial curve fitting:
![[Pasted image 20240201111540.png|300]]

### Maximum likelihood and least squares

The target value is given by $y(x;w)$ affected by additive noise $\epsilon$
$$
t = y(x;w)+\epsilon
$$
where $y(x,w)$ is equal to $w^T \phi(x)$ because we are working with non linear function.
Assume Gaussian noise $P(\epsilon|\beta)=\mathcal{N}(\epsilon|0,\beta^{-1})$ where $\beta$ is the precision (inverse variance)
$$
P(t|x, w, \beta) = \mathcal{N}(t|y(x; w), \beta^{-1})
$$
$y(x;w)$ is the mean, $\beta^{-1}$ is the variance.
The **Maximum likelihood** is:
$$
\begin{align*}
&\underset{w, \beta}{\mathrm{argmax}} P(\{t_1, \ldots, t_N\} | x_1, \ldots, x_N, w, \beta) \\
\end{align*}
$$
the **error minimization** is:
$$
\underset{w}{\mathrm{argmin}} \ E_D(w) = \underset{w}{\mathrm{argmin}} \frac{1}{2} \sum_{n=1}^N [t_n - w^T \phi(x_n)]^2
$$
Note: $E_D(\mathbf{w}) = \frac{1}{2} (\mathbf{t} - \Phi \mathbf{w})^T (\mathbf{t} - \Phi \mathbf{w}),$

The algorithms is always the same, find the gradient of the Error $\nabla E_D = 0$ and upgrade the parameter $w$: $w_{ML} = (\phi^T \phi)^{-1} \phi^T t$.

For regularization to control overfitting and avoid $E_D=0$:
$$
\underset{w}{\mathrm{argmin}} \ E_D(w) + \lambda E_W(w)
$$
$\lambda$ how much we want to penalize the terms that are too high.

### Multiple Outputs

$y$: vector with K components:
$$
y(x; W) = W^T \phi(x)
$$
$W^T$ is a matrix of dimension $M\times K$, and $\phi$ has dimension $M$. Similarly as before:
$$
W_{ML} = (\phi^T \phi)^{-1} \phi^T t
$$

## Kernel

The idea of kernel methods is that instead of representing each instance of the input space, in a particular feature space, we will define a kernel function. We don't need to represent x anymore but we need to define a function between 2 input values, to measure how this input are similar. 
- Linear: $k(x,x') = x^T x'$
- Polynomial: $k(x,x') = (\beta x^T x'+\gamma)^d$
- Radial Basis Function $k(x,x') = exp(-\beta |x-x'|^2)
- Sigmoid $k(x,x')=tanh(\beta x^T x' + \gamma)$

For example in **SVM - classification**, we have $y(x;\alpha) = sign(w_0+\sum_{n=1}^N \alpha_n x_n^T x)$ that in **Kernelized SVM** becomes:
$$
y(x;\alpha) = sign(w_0+\sum_{n=1}^N \alpha_n k(x_n,x))
$$
For **SVM - regression** we can consider to minimize the loss function:
$$
J(w) = \sum_{n=1}^N E(y_n, t_n) + \lambda ||w||^2
$$
applying the kernel trick, that from the formula before we obtain $\alpha$ as:
$$
\alpha = (K + \lambda I_N)^{-1} t
$$
and from $\lambda$ we obtain C (inverse of $\lambda$): 
$$
J(w) = C \sum_{n=1}^N E(y_n, t_n) + \lambda ||w||^2
$$
which can be approximated by something way less difficult to calculate:
$$
E_\epsilon(y,t) =
\begin{cases}
0 & \text{if } |y-t|<\epsilon\\
|y-t|-\epsilon & \text{otherwise}\\
\end{cases}
$$
![[Pasted image 20240201124512.png|300]]

Since this is not differentiable we can introduce slack variables $\xi_n^+$ and $\xi_n^-$:
$$
\begin{align*}
&t_n \leq y_n + \epsilon + \xi_n^+
&t_n \geq y_n - \epsilon - \xi_n^-
\end{align*}
$$
so the point $t_n$ that satisfies the above constraints are inside the $\epsilon \text{-tube}$. If we consider $\xi>0$ we can remove the equal in the constraints and the loss function becomes:
$$
J(w) = C \sum_{n=1}^N (\xi_n^+ + \xi_n^-) + \lambda ||w||^2
$$
and from the same condition as before we can define the Support vectors (Lagrange):
- $\hat a_n > 0 \rightarrow \epsilon + \xi_n + y_n - t_n = 0$
- $\hat a_n' > 0 \rightarrow \epsilon + \xi_n - y_n + t_n = 0$

![[Pasted image 20240201132607.png|300]]
red line = model
green dot = data
blue dot = support vectors
By Lagrange the samples inside the tube do not contribute, outside yes

 
## Instance Based

The disadvantage of parametric models, is that the chosen density might be a poor model of the distribution that generates the data, which can result in poor predictive performance. K-NN is the first non-parametric model (we don't want an intermediate representation like hypothesis).

**K-NN**:
The K-NN works finding points that are close to query points (x')
KNN depends on:
- data (if its a lot results in a lot of computation) (we prefer small dataset)
- distance function (a good distance function can result in better results)

Likelihood of class c for new instance x:
$$
p(c|x, D, K) = \frac{1}{K} \sum_{x_n \in N_K(x_n, D)} \mathbb{I}(t_n = c),
$$
with $N_K(x_n,D)$ the $K$ nearest points to $x_n$ and $\mathbb{I}(e) = \begin{cases} 1 & \text{if } e \text{ is true} \\0 & \text{if } e \text{ is false}\end{cases}$
![[Pasted image 20240201144446.png|400]]

**Locally weighted regression**:
Fit a local regression model around the query sample $x_q$:
1. Compute $N_K(x_q,D)$: K-nearest neighbors of $x_q$
2. Fit a regression model $y(x;w)$ on $N_K(x_q,D)$
3. Return $y(x_q;w)$


![[Pasted image 20240201144724.png|300]]

## Multiple Learners

Models can be trained in parallel or in sequence.
In general we train a set of models $y_m(x)$ over all the dataset:
This method is called *Voting*:
$$
\begin{align*}
&y_{voting}(x) = \sum_{m=1}^M w_my_m(x)
&y_{voting}(x) =  \underset{w}{\mathrm{argmin}} \sum_{m=1}^M w_mI(y_m(x) = c)
\end{align*}
$$
the first one for regression the second for classification. Here are some example of **structures**:
- Voting: ![[Pasted image 20240201161507.png|100]]
- Mixture of experts: ![[Pasted image 20240201161523.png|100]]  where the gating function assign weights to each expert, weights based on input
- Stacking: ![[Pasted image 20240201161813.png|100]]
- Cascading: ![[Pasted image 20240201161744.png|100]] the first learner is more accurate then the second and go on. The second learner benefit from the additional information provided by the first learner. $w$ is a feature, like brown hair and if it does not arrive to the threshold means that hai are not brown, maybe similar but not brown.

*Bagging*: very similar to voting but now we use a pre-processing in which the original dataset is sampled in different subsets (subsets, not partitions) and then there are used to train the models: 
$$
y_{bagging}(x) = \frac{1}{M} \sum_{m=1}^{M} y_m(x)
$$
*Boosting*: In this approach we have a sequential Learning, similar ot bagging but the models are trained in a sequential order and the info of the next dataset depends on the previous one. 

![[Pasted image 20240201163644.png|300]]
Each base classifier $y_m(x)$ is trained on a weighted form of the training set (blue arrows) in which the weights $w_n^{(m)}$ depend on the performance of the previous base classifier $y_{m-1}(x)$ (green arrows). Once all base classifiers have been trained they are combined to give the final classifier $Y_M(x)$ (red arrows).

**AdaBoost**: AdaBoost trains a new classifier using a data set in which the weighting coefficients are adjusted according to the performance of the previously trained classifier so as to give greater weight ot the misclassified data points.
1. Initialize $w_n = \frac{1}{N}$ 
2. For $m = 1, ..., M$:
	- minimize the weighted error $J_m = \sum_{n=1}^{N} w_n^{(m)}I(y_m(x_n) \neq t_n)$
	- update the weight $w_n^{(m+1)} = w_n^{(m)} exp[\alpha_mI(y_m(x_n) \neq t_n]$
3. Evaluate $\epsilon_m = \frac{\sum_{n=1}^{N} w_n^{(m)} \mathbb{I}(y_m(x_n) \neq t_n)}{\sum_{n=1}^{N} w_n^{(m)}} \quad \text{and} \quad \alpha_m = \ln \left( \frac{1 - \epsilon_m}{\epsilon_m} \right)$ 
4. Output the final classifier (make prediction using the final model which is given by) $Y_M(x) = \text{sign} \left( \sum_{m=1}^{M} \alpha_m y_m(x) \right)$

![[Pasted image 20240201164946.png|400]]
The dimension of the circles are the weights.
AdaBoost can be explained as the sequential minimization of an exponential error function. The error function measures how well a weak learner is able to classify data. Calculated by taking the exponential of the negative of the weak learner's output.

Advantages:
Fast, simple, easy to program, no prior knowledge about $w$, no other parameters, can be combined to find $w$.
Issues:
Performance depends on data (can there be insufficient data), sensitive to noise.

## ANN

We study NN, FNN, MLP to overcome the limitation of linear models (linear function dependency). 

**FNN**: these models are called feedforward because information flows through the function being evaluated from x. There are no feedback connections in which outputs of the model are fed back into itself. When feedforward neural networks are extended to include feedback connections, they are called recurrent neural networks.

**Architecture design**:
- How many hidden layers? *Depth* Increase the depth gives best results in terms of accuracy.
- Hoe many units in each layer? *Width*
- Which kind of units? *Activation functions*
- Which kind of cost function? *Loss function* In NN the loss function are non convex so it's possible to find local minimum

The choice of **network output and cost function** are related depending on the task to achieve.
- *Regression*: $y=W^Th+b$  with activation function = *identity*, since the output of neurons are linear units. The cost function is *maximize the likelihood* (cross-entropy) that is equivalent to minimizing mean squared error. These choices do not make the function *saturate* (sigmoid or tanh can saturate if the values are very high or very low, saturation refers to a state where changes in the input to an activation function result in little or no change in the output).
- *Binary classification*: $y=\sigma (w^Th+b)$  with activation function = *sigmoid*. The Loss function is the *Binary cross-entropy (Bernoulli distribution)*. Output unit saturates only when it gibes the correct answer
- *Multi-class classification*: $y_i = \frac{exp(\alpha^{(i)}}{\sum_j exp(\alpha_j)}$ the activation function is the *softmax*. The Loss function is the *Categorical cross-entropy (Multinomial distribution)*. Output units saturate only when there are minimal errors.

In general for **Hidden unit activation functions** there are (no predictable):
- Sigmoid = $\sigma(\alpha)$
- Tanh = $tanh(\alpha)$
- Relu = $max(0, \alpha)$

For **Gradient Computation**:
we can split the computation of the gradient in two parts. In the first part given the input and the desired output, we can compute the network forward (from the input to the output), when we reach the last label we can compute a comparison with the desired output. With this knowledge (second part) we can go back through the green arrow to the start. This algorithm is only used to compute the gradients, is not a training algorithm, is not specific to FNN. It's easy to calculate the gradient because FNN is a chain, and we can apply the chain rule to derivatives: $\frac{dz}{dx} = \frac{dz}{dy}\frac{dy}{dx}$

![[Pasted image 20240201183927.png|150]]

*BackPropagation algorithm*:
Forward step: given the parameters of the networks, input, target value and the loss function, we compute the loss function applied to the output of the network (y) and the target value (t)
Backward step: goes back from this error and compute the derivative of this error with respect ot all the parameters of the network by going back from the output layer to the input layers

==Example==:
![[Pasted image 20240201190232.png|200]] 
![[Pasted image 20240201190249.png|200]] 
![[Pasted image 20240201190308.png|200]]  

Now that we have a method for estimating the gradient, we use it to find a solution of our Optimization problem that minimize the error function or the loss function:
- *Stochastic Gradient Descent*: implements the learning rate that gradually decrease over time. It uses the minibatch. The problem on changing the lr, is that we don't know where we start (we could begin close to the solution and after the initial iteration go far away).
- *SGD with momentum*: designed to accelerate learning, especially in the face of high curvature, small but consistent gradients, or noisy gradients. The momentum term increases for dimensions whose gradients point in the same direction and reduces updates for dimensions whose gradients change directions
- *Nesterov momentum*: instead of calculating the gradient at the current position, Nesterov momentum calculates the gradient at the position after the current momentum is applied


**Regularization**:
used to reduce overfitting:
- Parameter norm penalties: add a regularization term $E_{reg}$ to the cost $J(\theta)$
- Dataset Augmentation: generate additional data and include them in the dataset
- Early Stopping
- Parameter sharing: constraint on having subsets of model parameters to be equal. Advantages also in memory storage.
- Dropout

---

# References
