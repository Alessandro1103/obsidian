Date: 2023-11-25
Time: 08:15
Tags: #Università #English #IA 
Up: [[IA]]

---
# Adversarial Search

Adversarial search means playing against an opponent. 

Definition **Game State Space**:
A game state space is a 6-tuple $\Theta = (S, A, T, I, S^T, u)$ where:
- $S$ is the disjoint union of $S^{Max}$, $S^{Min}$ and $S^{T}$
- A is the disjoint union of $A^{Max}$ and $A^{Min}$
- For $a \in A^{Max}$, if $s \xrightarrow{a} s'$ then $s \in S^{Max} and s' \in S^{Min} \cup S^T$

---
# References
