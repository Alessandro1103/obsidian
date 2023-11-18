Date: 2023-11-18
Time: 10:58
Tags:
Up: [[IA]]

---
# Classical Search

## Part 1

A formal definition of **Search Problems**:
- The underlying base concept are state spaces
- State spaces are graphs
- Paths to goal states correspond to solutions
- Cheapest such paths correspond to optimal solutions

Every problem Π specifies a state space Θ: 
Definition of **State Space**:
A state space is a 6-tuple Θ = ($S$, $A$, $c$, $T$, $I$, $S^G$) where: 
- $S$ is a finite set of states. 
- $A$ is a finite set of actions. 
- $c$ : $A → R_0^+$ is the cost function. 
- $T$ ⊆ $S × A × S$ is the transition relation. We require that $T$ is deterministic, i.e., for all $s$ ∈ $S$ and $a$ ∈ $A$, there is at most one state $s'$ such that ($s$, $a$, $s'$) ∈ T. If such ($s$, $a$, $s'$) exists, then $a$ is applicable to $s$. 
- I ∈ S is the initial state. 
- $S^G$ ⊆ S is the set of goal states. We say that Θ has the transition (s, a, s0 ) if (s, a, s0 ) ∈ T. We also write s a−→ s 0 , or s → s 0 when not interested in a. We say that Θ has unit costs if, for all a ∈ A, c(a) = 1.
## Part 2

---
# References
