Date: 2023-12-12
Time: 16:30
Tags: #Università #English #IA 
Up: [[IA]]

---
# Delete Relaxation Heuristics

## Delete Relaxation

![[Pasted image 20231212163800.png|400]]

![[Pasted image 20231212164013.png|400]]

![[Pasted image 20231212165819.png|400]]
![[Pasted image 20231212171127.png|400]]
![[Pasted image 20231212184117.png|400]]

## h+ Heuristic
![[Pasted image 20231212184530.png|400]]
$h^+$ = minimum effort to reach the goal under delete relaxation

Proposition of $h^+ is Consistent$:
Let $\prod = (P,A,c,I,G)$ be a STRIPS planning task. Then $h^+$ is consistent, and thus admissible, safe, and goal-aware.

![[Pasted image 20231212185851.png|400]]

Theorem is **Optimal Relaxed Planning is Hard**:
$PlanOpt^+$ is NP-complete

## $h^{add}$ and $h^{max}$

![[Pasted image 20231212190032.png|400]]
![[Pasted image 20231212190049.png|400]]

Proposition of **$h^{max}$ is Optimistic**:
$h^{max} \leq h^+$, and thus $h^{max} \leq h^*$

Proposition of **$h^{max}$ is Pessimistic**:
For all STRIPS planning task $\prod$, $h^{add}\geq h^+$


---
# References
