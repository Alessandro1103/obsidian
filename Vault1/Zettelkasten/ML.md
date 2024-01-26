Date: 2024-01-25
Time: 15:55
Tags:
Up: 

---
# ML

## Introduction
**What is a Learning Problem?**
A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.

**Formal Definition of ML**?
Give $f: X \rightarrow Y$ and a dataset $D$, we want to learn $\hat{f}$ such that $\hat{f}(x) \approx f(x)$ for $\forall x \in X \setminus X_D$.



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

The set of ==consistent== hypothesis is called version space: 
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

The true error of a model is the probability that extracting an input value from the input distribution the model will make a mistake respect to the true function:
$$

$$

---
# References
