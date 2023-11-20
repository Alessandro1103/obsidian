Date: 2023-11-20
Time: 15:35
Tags:
Up: [[IA]]

---
# Classical Search PT2

## Informed Search

If is it good to expand a node $s$ is given by a **heuristic function** $h(s)$, which estimates the cost of an the cheapest path from $s$ to the goal. 

The **heuristic function**:
Let $\prod$ be a problem with states $S$. A heuristic function, short heuristic, for $\prod$ is a function $h : S \rightarrow R^+_0 \cup \{\infty\}$ so that, for every goal state $s$, we have $h(s) = 0$. The *perfect heuristic* $h^*$ is the function assigning every $s \in S$ the cost of a cheapest path from $s$ to a goal state, or $\infty$ if no such path exists.

$h$ has to be accurate but the calculation must not be demanding (contradiction).
Given a problem $\prod$, a heuristic function $h$ for $\prod$ can be obtained as goal distance within a simplified (relaxed) problem $\prod'$.

Definition **Admissibility**, **Consistency**:
Let $\prod$ be a problem with state space Θ and states $S$, and let $h$ be a heuristic function for $\prod$. We say that $h$ is *admissible* if, for all $s \in S$, we have $h(s) ≤ h^∗(s)$. We say that $h$ is *consistent* if, for all transitions $s \rightarrow^a s'$ in $\Theta$, we have $h(s) − h(s') \leq c(a)$

We can either say: admissible is when the heuristic we find is 





---
# References
