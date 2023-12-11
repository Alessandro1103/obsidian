Date: 2023-12-11
Time: 12:28
Tags: #Università #IA #English 
Up: [[IA]]

---
# Critical Path Heuristics

![[Pasted image 20231211122920.png|400]]

![[Pasted image 20231211123029.png|400]]

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

This is the relaxed planning graph:


---
# References
