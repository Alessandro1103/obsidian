Date: 2023-11-21
Time: 14:21
Tags: #English #Università #IA 
Up: [[IA]]

---
# Introduction to Planning

## Strips Planning

Strips is the simplest possible logics-based planning language. It has only Boolean variables.

Definition of **STRIPS Planning Task**:
A STRIPS planning task, short planning task, is a 4-tuple $\prod = (P, A, I, G)$ where: 
- P is a finite set of *facts* (aka propositions). 
- A is a finite set of *actions*; each a \in A is a triple $a = (pre_a , add_a, del_a)$ of subsets of P referred to as the action’s precondition, add list, and delete list respectively; we require that add a ∩ del a = ∅. 
- I ⊆ P is the initial state. 
- G ⊆ P is the goal.

---
# References
