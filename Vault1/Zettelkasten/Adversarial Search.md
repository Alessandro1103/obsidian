Date: 2023-11-25
Time: 08:15
Tags: #Università #English #IA 
Up: [[IA]]

---
# Adversarial Search

Adversarial search means playing against an opponent. 

Definition **Game State Space**:
A game state space is a 6-tuple $\Theta = (S, A, T, I, S^T, u)$ where:
- $S$, $A$, $T$, $I$: States, actions, deterministic transition relation, initial state. They are as in classical search problems, except:
	- $S$ is the disjoint union of $S^{Max}$, $S^{Min}$ and $S^{T}$
	- A is the disjoint union of $A^{Max}$ and $A^{Min}$
	- For $a \in A^{Max}$, if $s \xrightarrow{a} s'$ then $s \in S^{Max} and s' \in S^{Min} \cup S^T$
	- For $a \in A^{Min}$, if $s \xrightarrow{a} s'$ then $s \in S^{Min} and s' \in S^{Max} \cup S^T$
- $S^T$ is the set of terminal states
- $u: S^T \rightarrow R$ is the utility function

Commonly used terminology: state=position, end state=terminal state, action=move

Why games are hard to solve:
Definition **Strategy**:
Let $\Theta$ be a game state space, and let $X \in {Max, Min}$. A strategy for $X$ is a function $\sigma^X: S^X \rightarrow A^X$ so that $a$ is applicable to $s$ whenever $\sigma^(s) = a$.
We need to prepare for all possibilities, a strategy is optimal if it yields the best possible utility for X assuming perfect opponent play. 
We can have 3 solutions:
- Ultra weak: 

---
# References
