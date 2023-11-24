Date: 2023-11-24
Time: 11:51
Tags: #Università #IA #English 
Up: [[IA]]

---
# Local Search

"Local search" refers to an optimization approach that focuses on finding acceptable solutions in the vicinity of the current solution in a search space. Instead of exploring the entire solution space, local search confines itself to exploring the "neighborhood" of the current solution.

Example:
![[Pasted image 20231124120039.png|500]]
Local search algorithm are not systematic, this can lead to a lack of guarantees regarding the global optimality of the solution found, it doesn't look for all the solution but a better one. This means that the algorithms use very little memory (constant space). It finds reasonable solutions even in large or infinite state spaces. One example of algorithm: 

The **Hill-Climbing**:
keeps choosing actions leading to a direct successor state with best heuristic value. It stops when no more immediate improvements can be made.
No completeness, no optimality.
The time complexity depends on the single run, can be either huge or small. Memory instead has no consumption. $O(b)$

![[Pasted image 20231124122252.png|600]]

There are some difficulties: it can happen that all the neighbors look worse than the current state or if il all look the same the moves will be chosen randomly. In these cases we can do a restart and choose different path using random walks, i.e. moving to a successor chosen uniformly at random from the set of successors:
![[Pasted image 20231124123131.png|600]]
In the context of search algorithms a "plateau" refers to a region in the search space where the heuristic values of states are the same.

State Space Landscape:
![[Pasted image 20231124123517.png|500]]
Hill climbing is incomplete and can get stuck on local minima, random walk is very slow, if we merge these two, we obtain: Simulated Annealing.

The **Simulated Annealing**:
escape local maxima by allowing some "bad" moves but gradually decrease their size and frequency

Idea $\rightarrow$ keep k states in memory instead of 1. At each step, all successors of k states are generated, if any is a goal, stop. Often, all k states end up on same local hill.
If we choose k successors randomly, biased towards good ones, this leads to **Stochastic Beam Search**. 

The **Genetic Algorithms**:



---
# References
