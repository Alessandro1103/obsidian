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
- Ultra weak: the goal is to determine the outcome of the game (win, lose, or draw) from the starting position, assuming both players play perfectly.
- Weak: Provide a strategy that is optimal from the beginning of the game
- Strong: Provide a strategy that is optimal from any valid state

Computing a strategy is infeasible (almost all the games).

**Minimax**:
It's a strategy that minimizes the possible loss for a worst-case scenario, assuming that the opponent is also playing optimally. 
It can be represented in a tree model, a depth-first search in game tree, with Max in the root. We have to apply an utility function to terminal positions. Bottom-up for each inner node $n$ in the tree, compute the utility $u(n)$ of $n$ as follows:
- If it’s Max’s turn: Set $u(n)$ to the maximum of the utilities of $n$’s successor nodes.
- If it’s Min’s turn: Set $u(n)$ to the maximum of the utilities of $n$’s successor nodes.
Selecting a move for Max at the root: Choose one move that leads to a successor node with maximal utility.

![[Pasted image 20231125101907.png]]

The Minmax is the simplest possible game search algorithm. But it's infeasible (search tree way too large). To make it feasible we can limit search depth, applying an evaluation function to the cut-off states, or use *alpha beta pruning* to reduce search, or use the Monte Carlo Tree Search (MCTS). 

---
# References
