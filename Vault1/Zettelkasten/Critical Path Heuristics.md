Date: 2023-12-11
Time: 12:28
Tags: #Università #IA #English 
Up: [[IA]]

---
# Critical Path Heuristics

![[Pasted image 20231211122920.png|400]]

The perfect regression heuristic is a function that estimates the cost of achieving a subgoal $g$ from a state $s$.

```
r*(s, g) = { 0 g ⊆ s 
		   { min a∈A,regr(g,a)#1 c(a) + r*(s, regr(g, a)) otherwise
```

regr(g,a) is the result of regressing g by a. Regressing a goal by an action means removing from the goal any preconditions that are satisfied by the effects of the action, and adding to the goal any post conditions that are not satisfied by the preconditions of the action.
The perfect regression heuristic r* works by recursively considering all possible actions that can be taken to achieve the subgoal `g`. If the subgoal is already true in the current state, then the cost of achieving it is 0. Otherwise, the cost is the minimum cost of achieving the subgoal by taking any possible action.

![[Pasted image 20231211123029.png|400]]

Example:
![[Pasted image 20231211234203.png|400]]

Spiegazione:
- the first point applies the definition of critical paths, choosing |g|>1
- the second point applies the third definition of critical paths, when the set of subgoals to be achieved is the empty set, the critical path heuristic returns a value of 0. This because the goal has already been achieved, and there is no cost associated with taking no actions. In this case $h^1(I,\{at(Sy)\})$ we can see that $I = at(Sy)$ so it's achieved. Same for $v(Sy)$
- the third point applies the second definition of critical paths, it takes into account the cost of actions and the relationships between subgoals 
 ![[Pasted image 20231211123106.png|400]]

Proposition of $h^m$ is **Admissible**:
$h^m$ is consistent and goal-aware, and thus also admissible and safe

Proposition of $h^m$ gets more accurate as $m$ grows: 
$h^{m+1}$ dominates $h^m$

Proposition of $h^m$ is perfect in the limit:
There exists $m$ s.t. $h^m = h^∗$

![[Pasted image 20231211123641.png|400]]

## Dynamic Programming

Consider all subgoals with length less than or equal to $m$. Set the value of $h^m(s, g)$ to 0 if g is a subset of s, and to infinity otherwise. Then, update the value of each g based on the actions that can be applied to the values that have already been calculated, until the values stop changing.

We start by defining $h^m$ iteratively, to make this approach explicit. Then, we define a dynamic programming algorithm that corresponds to this iterative definition.

![[Pasted image 20231211124251.png|400]]

Example m=1:
![[Pasted image 20231211124704.png|500]]
Example m=2:
![[Pasted image 20231211124723.png|500]]

## Graphplan

![[Pasted image 20231211130256.png|400]]

Definition. Let $\prod = (P, A, c, I, G)$ be a STRIPS planning task. The 1-planning graph heuristic $h^1_{PG}$ for $\prod$ is the function $h^1_{PG}(s) := min\{i \ | \ s \subseteq F_i\}$, where $F_i$ are the fact sets computed by a 1-planning graph (and the minimum over an empty set is $\infty$)

---
# References
