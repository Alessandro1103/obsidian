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

Proposition of **$h^{add}$ is Pessimistic**:
For all STRIPS planning task $\prod$, $h^{add}\geq h^+$. There exist $\prod$ and $s$ so that $h^{add}(s)>h^*(s)$

Both $h^{max}$ and $h^{add}$ approximate $h^+$ by assuming that singleton subgoal facts are achieved independently. $h^{max}$ estimates optimistically by the most costly singleton subgoal, $h^{add}$ estimates pessimistically by summing over all singleton subgoals.

## Relaxed Plan Heuristic

First, create a best-supporter function $bs$ that, for every fact $p$ in the set of facts $P$, returns the action that is considered to be the cheapest way to achieve $p$ (within the relaxation). Then, use this function to extract a relaxed plan by applying it to singleton subgoals and collecting all of the actions that are returned.

![[Pasted image 20231212192434.png|400]]
![[Pasted image 20231212192453.png|400]]

---
# References
