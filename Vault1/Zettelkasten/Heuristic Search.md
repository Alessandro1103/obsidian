Date: 2023-12-10
Time: 19:54
Tags: #IA #English #Università 
Up: [[IA]]

---
# Heuristic Search

Definition of **Heuristic Function**:
Let $\prod$ be a planning task with state space $\prod' = (S, L, c, T, I, S^G)$. A heuristic function, short heuristic, for $\prod$ is a function $h : S \rightarrow R^+_0 \cup \{\infty\}$. Its value $h(s)$ for a state $s$ is referred to as the state’s heuristic value, or $h$ value.

Definition of **Remaining Cost, $h^*$**. Let $\prod$ be a planning task with state space $\Theta_\prod = (S, L, c, T, I, S^G)$. For a state $s \in S$, the state’s remaining cost is the cost of an optimal plan for $s$, or $\infty$ if there exists no plan for $s$. The perfect heuristic for $\prod$, written $h^∗$ , assigns every $s \in S$ its remaining cost as the heuristic value.

Definition of **Safe/Goal-Aware/Admissible/Consistent**:
Let $\prod$ be a planning task with state space $\Theta_\prod = (S, L, c, T, I, S^G)$, and let h be a heuristic for $\prod$. The heuristic is called: 
- safe if, for all $s \in S$, $h(s) = \infty$ implies $h^* (s) = \infty$; 
- goal-aware if $h(s) = 0$ for all goal states s ∈ S G; 
- admissible if $h(s) ≤ h^∗ (s)$ for all $s \in S$; 
- consistent if $h(s) ≤ h(s '')$ + c(a) for all transitions $s \rightarrow^a s'$ .

Let $\prod$ be a planning task, and let $h$ be a heuristic for $\prod$. If $h$ is admissible, then $h$ is goal-aware. If $h$ is admissible, then $h$ is safe. If $h$ is consistent and goal-aware, then $h$ is admissible. No other implications of this form hold.


---
# References
