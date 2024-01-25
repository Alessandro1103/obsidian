Date: 2024-01-25
Time: 15:55
Tags:
Up: 

---
# ML

## Introduction
**What is a Learning Problem?**
A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.

## Notation
$V(b)$ = the true target function that gives optimal solution.
$\hat V(b)$ = the learned function (approximation of V(b) computed by the learning algorithm), alse called weight (w).
$V_{train}(b)$ = the training value obtained at b from the training dataset.

## LMS (Least mean squared)
"w" is the weight of the learning function, improved by:
$$
error(b) = V_{train}(b) - \hat V(b)
$$

---
# References
