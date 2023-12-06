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
- A is a finite set of *actions*; each $a \in A$ is a triple $a = (pre_a , add_a, del_a)$ of subsets of $P$ referred to as the action’s *precondition*, *add list*, and *delete list* respectively; we require that $add_a \cap del_a = \emptyset$. 
- $I \subseteq P$ is the initial state. 
- $G \subseteq P$ is the goal.

Definition of **STRIPS State Space**: 
Let $\prod = (P, A, c, I, G)$ be a STRIPS planning task. The state space of $\prod$ is $\Theta_\prod = (S, A, T, I, SG) where: The states (also world states) S = 2P are the subsets of P. A is Π’s action set. The transitions are T = {s a−→ s 0 | prea ⊆ s, s0 = (JsK, a)}. If prea ⊆ s, then a is applicable in s and (JsK, a) := (s ∪ adda) \ dela. If prea 6⊆ s, then (JsK, a) is undefined. I is Π’s initial state. The goal states S G = {s ∈ S | G ⊆ s} are those that satisfy Π’s goal.

---
# References
