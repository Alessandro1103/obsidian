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

Consider all subgoals g with size ≤ m. Initialize h m(s, g) to 0 if g ⊆ s, and to ∞ otherwise. Then, keep updating the value of each g based on actions applied to the values computed so far, until the values converge. 
- We start with an iterative definition of $h^m$ that makes this approach explicit. 
- We define a dynamic programming algorithm that corresponds to this iterative definition.

---
# References
