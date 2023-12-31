Date: 2023-12-09
Time: 17:22
Tags: #Università #IA #English 
Up: [[IA]]

---
# Causal Graphs

## Causal Graphs

![[Pasted image 20231209172321.png|400]]

![[Pasted image 20231209172343.png|400]]

Example:
![[Pasted image 20231209172407.png|300]] ![[Pasted image 20231209172458.png|300]]

## DTGs

![[Pasted image 20231209172557.png|400]]

![[Pasted image 20231209172659.png|400]]

## Example result

Lemma of **Decomposition**: You can decompose an FDR planning task into two smaller tasks that have no interactions, and then solve each of those tasks optimally, you can always combine the solutions of those tasks to find an optimal solution to the original task

Consider a leaf vertex v in the conflict graph CG(\prod) of an FDR planning task \prod. This means that v is not connected to any other vertices in the conflict graph, which suggests that v does not interact with any other variables in the task.
Furthermore, since G(v) is undefined, this implies that v does not have any specific goal or purpose. In other words, v's state is not relevant to the overall goal of the planning task.
Based on these observations, we can simplify $\prod$ by removing v from the task. This modified task, which is denoted by $\prod'$, still contains all the actions and variables that are relevant to achieving the goal of the task. Any (optimal) plan for $\prod'$ is an (optimal) plan for $\prod$

Lemma of **Simplification**: If you have an $FDR$ planning task $\prod$ and a root vertex $v$ with a connected $DTG$ and invertible value transitions, you can solve the problem of planning for $\prod$ by solving the problem of planning for the task $\prod'$ that is obtained by removing $v$ and restricting $I$ and $G$ to $V \backslash {v}$, remove any assignment to $v$ from all action preconditions, and remove all actions $a$ where $eff_a(v)$ is defined. 

![[Pasted image 20231210134012.png|100]]

Final plan:
1. Order the variables topologically $v_1, \dots, v_n$ from "servants" to "clients"
2. Iteratively apply the simplification1 to $v_1, \dots, v_n$. Then $\prod'$ is empty, and the empty plan $\vec{a} := <>$ solves it:
	1. Remove $v$ from $\prod$ to obtain $\prod'$; find plan $\vec{a}$ for $\prod'$
3. Iteratively apply the simplification2 to $v_n, \dots, v_1$:
	1. Extend $\vec{a}$ with move sequence for $v$ that achieves all preconditions on $v$ as needed, then moves to $v$'s own goal (if any) at the end.

Example:
![[Pasted image 20231210135017.png|400]]

Theorem of **Complexity**:
Restrict the input to FDR tasks $\prod = (V, A, c, I, G)$ such that $CG(\prod)$ is acyclic and, for all $v \in V$ , all value transitions of $v$ are invertible. Then PlanEx can be decided in polynomial time

---
# References
