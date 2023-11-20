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



---
# References
