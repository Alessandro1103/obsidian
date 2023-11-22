Date: 2023-11-20
Time: 15:35
Tags:
Up: [[IA]]

---
# Classical Search PT2

## Informed Search

If is it good to expand a node $s$ is given by a **heuristic function** $h(s)$, which estimates the cost of an the cheapest path from $s$ to the goal. 

The **heuristic function**:
Let $\prod$ be a problem with states $S$. A heuristic function, short heuristic, for $\prod$ is a function $h : S \rightarrow R^+_0 \cup \{\infty\}$ so that, for every goal state $s$, we have $h(s) = 0$. The *perfect heuristic* $h^*$ is the function assigning every $s \in S$ the cost of a cheapest path from $s$ to a goal state, or $\infty$ if no such path exists.

$h$ has to be accurate but the calculation must not be demanding (contradiction).
Given a problem $\prod$, a heuristic function $h$ for $\prod$ can be obtained as goal distance within a simplified (relaxed) problem $\prod'$.

Definition **Admissibility**, **Consistency**:
Let $\prod$ be a problem with state space Θ and states $S$, and let $h$ be a heuristic function for $\prod$. We say that $h$ is *admissible* if, for all $s \in S$, we have $h(s) ≤ h^∗(s)$. We say that $h$ is *consistent* if, for all transitions $s \xrightarrow{a} s'$ in $\Theta$, we have $h(s) − h(s') \leq c(a)$

Proposition **Consistency $\Rightarrow$ Admissibility**. Let $\prod$ be a problem, and let $h$ be a heuristic function for $\prod$. If $h$ is consistent, then $h$ is admissible. 


**BFS**:
Use an evaluation function $f(n)$ for each node $n$, and expand the most desiderable unexpanded node. Implementation:
- **Greedy BFS**: expand the node that is closest to the goal. The evaluation function has this form: $f(n)=h(n)$ (heuristic function). The algorithm is complete but not optimal.
- **A* Search**: avoid expanding paths that are already expensive. the evaluation function has this form: $f(n)=g(n)+h(n)$ where 
	- $g(n)$ = cost to reach $n$
	- $h(n)$ = estimated cost to goal from $n$
	- $f(n)$ = estimated total cost of path through $n$ to goal
  It has completeness and optimal


Definition. Let $\prod$ be a problem with state space $\Theta = (S, A, c, T, I, S^G)$, and let $h$ be a consistent heuristic function for $\prod$. We define the *h-weighted state space* as $\Theta^h = (S, A^h , c^h , T^h , I, S^G)$ where: 
- $A^h := {a[s, s']\; |\; a \in A,\; s \in S,\; s' \in S,\;(s, a, s') \in T}$. 
- $c^h : A^h \rightarrow  R^+_0$ is defined by $c^h (a[s, s']) := c(a) − [h(s) − h(s')]$. 
- $T^h = {(s, a[s, s'], s')\; |\; (s, a, s') \in T}$.

![[Pasted image 20231120164007.png]]

Theorem **Optimality of $A^*$**. Let $\prod$ be a problem, and let $h$ be a heuristic function for $\prod$. If $h$ is consistent, then the solution returned by $A^∗$ (if any) is optimal.

Different variants of $A^*$:
- Our variant of $A^∗$ does duplicate elimination but not re-opening. 
- Re-opening: involves removing nodes from the closed list (nodes that have already been explored) and adding them back to the open list. This allows the algorithm to explore alternative paths and potentially find a shorter path than the one initially discovered.
- With a consistent heuristic, can’t happen so we don’t need re-opening for optimality. 
- Given admissible but inconsistent $h$, if we either use duplicate elimination with re-opening or don’t use duplicate elimination at all, then $A^∗$ is optimal as well. Hence the well-known statement $A^∗$ is optimal if h is admissible".

Let’s consider an *extreme case*: 
What happens if $h$ = $h^∗$? 
- Greedy Best-First Search: 
	- If all action costs are strictly positive, when we expand a state, at least one of its successors has strictly smaller $h$. The search space is linear in the length of the solution. 
	- If there are 0-cost actions, the search space may still be exponentially big (e.g., if all actions costs are 0 then $h^∗ = 0$). 
- $A^∗$ : 
	- If all action costs are strictly positive, and we break ties ($g(n) + h(n) = g(n') + h(n')$) by smaller $h$, then the search space is linear in the length of the solution. 
	- Otherwise, the search space may still be exponentially big.



---
# References
