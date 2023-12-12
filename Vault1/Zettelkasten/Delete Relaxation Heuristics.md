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
![[Pasted image 20231212194434.png|400]]

![[Pasted image 20231212194533.png|400]]

![[Pasted image 20231212194644.png|400]]
![[Pasted image 20231212194745.png|400]]


![[Pasted image 20231212195228.png|400]]
![[Pasted image 20231212195556.png|400]]

## FDR

![[Pasted image 20231212195722.png|400]]

## Summary

- The delete relaxation simplifies STRIPS by removing all delete effects of the actions. 
- The cost of optimal relaxed plans yields the heuristic function h +, which is admissible but hard to compute. 
- We can approximate h + optimistically by h max, and pessimistically by h add . h max is admissible, h add is not. h add is typically much more informative, but can suffer from over-counting. 
- Either of h max or h add can be used to generate a closed well-founded best-supporter function, from which we can extract a relaxed plan. 
- The resulting relaxed plan heuristic h FF does not do over-counting, but otherwise has the same theoretical properties as h add; in practice, it typically does not over-estimate h ∗ . 
- The delete relaxation can be applied to FDR simply by accumulating variable values, rather than over-writing them. This is formally equivalent to treating variable/value pairs like STRIPS facts.



---
# References
