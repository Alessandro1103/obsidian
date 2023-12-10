Date: 2023-12-10
Time: 19:54
Tags: #IA #English #Università 
Up: [[IA]]

---
# Heuristic Search

Definition of **Heuristic Function**:
Let $\prod$ be a planning task with state space $\prod' = (S, L, c, T, I, S^G)$. A heuristic function, short heuristic, for $\prod$ is a function $h : S \rightarrow R^+_0 \cup \{\infty\}$. Its value $h(s)$ for a state $s$ is referred to as the state’s heuristic value, or $h$ value.

Definition of **Remaining Cost, $h^*$**. Let $\prod$ be a planning task with state space $\Theta_\prod = (S, L, c, T, I, S^G)$. For a state $s \in S$, the state’s remaining cost is the cost of an optimal plan for $s$, or $\infty$ if there exists no plan for $s$. The perfect heuristic for $\prod$, written $h^∗$, assigns every $s \in S$ its remaining cost as the heuristic value.

Definition of **Safe/Goal-Aware/Admissible/Consistent**:ù
**Safe:** A heuristic is safe if it never overestimates the cost of reaching a goal state. This means that if the heuristic estimates that it costs a certain amount to reach a goal state, then the actual cost of reaching that goal state can never be higher than that amount.
**Goal aware:** A heuristic is goal aware if it always returns a cost of 0 for goal states. This means that the heuristic recognizes that goal states are the desired outcome of a planning task, and that it doesn't cost anything to reach a goal state.
**Admissible:** A heuristic is admissible if it never underestimates the cost of reaching a goal state. This means that if the heuristic estimates that it costs a certain amount to reach a goal state, then the actual cost of reaching that goal state can never be lower than that amount.
**Consistent:** A heuristic is consistent if it satisfies the following relationship:

```
h(s) <= h(s') + c(a)
```

where:

- h(s) is the heuristic estimate of the cost of reaching a goal state from state s
- h(s') is the heuristic estimate of the cost of reaching a goal state from state s'
- c(a) is the cost of transitioning from state s to state s' via action a

In other words, a consistent heuristic never overestimates the cost of transitioning from one state to another.

Let $\prod$ be a planning task, and let $h$ be a heuristic for $\prod$. If $h$ is admissible, then $h$ is goal-aware. If $h$ is admissible, then $h$ is safe. If $h$ is consistent and goal-aware, then $h$ is admissible. No other implications of this form hold.


---
# References
