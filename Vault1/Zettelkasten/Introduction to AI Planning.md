Date: 2023-11-21
Time: 14:21
Tags: #English #Università #IA 
Up: [[IA]]

---
# Introduction to Planning

## Strips Planning

Strips is the simplest possible logics-based planning language. It has only Boolean variables.

![[Pasted image 20231209120709.png|400]]
![[Pasted image 20231209120720.png|400]]

![[Pasted image 20231209120916.png|400]]

In summary we have:
- Facts: (state or condition of the problem) e.g. onTable(x)
- Initial State: e.g. onTable(E)
- Goal: e.g. on(E,C)
- Actions: action/functions, each have:
	- pre: state or condition before
	- add: state or condition after
	- del: state or condition that need to be removed

The problem:
Given STRIPS task $\prod = (P,A,I,G)$, we need to find an action sequence $\vec{a}$ leading from $I$ to a state that contains $G$, when pretending that preconditions and deletes are empty. We have no certainty about to find the shortest possible $\vec{a}$. This is a NP problem, there is no algorithm. 

We have:
**Satisficing Planning:**
- Input:
- Outpu
**Optimal Planning:**



---
# References
