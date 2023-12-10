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

Lemma of **Simplification**: If you have an $FDR$ planning task $\prod$ and a root vertex $v$ with a connected $DTG$ and invertible value transitions, you can solve the problem of planning for $\prod$ by solving the problem of planning for the task $\prod'$ that is obtained by removing $v$ and restricting $I$ and $G$ to $V \backslash {v}$, remove any assignment to $v$ from all action preconditions, and remove all actions $a$ where $eff_a(v)$ is defined

---
# References
