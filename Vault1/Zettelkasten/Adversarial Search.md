non Date: 2023-11-25
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
It reach completeness and optimality.
Time complexity: $O(b^m)$ with b branching factor and m depth of the solution
Space complexity: $O(bm)$ (depth-first exploration)

Let's impose a **Search depth limit** ("horizon") $d$ and apply an *evaluation function f* that maps game states to number to the non-terminal cut-off states.
An evaluation function can be:
Linear (weighted): $w_1f_1 + w_2f_2 + \dots + w_nf_n$, where the weights can be learned automatically, and the features have to be designed by human experts.

It's very difficult to predict the search runtime, we want to go as deeply as possible. The solution is to perform an Iterative deepening (chose d = 1,2,3.... and then return the result, if we want go deeper). The best solution is **Quiescence search**:
- Dynamically adapted $d$
- Search more deeply in "unquiet" positions (in chess when we change pieces)


Another solution we can get to is **Alpha Pruning** where, if we know that a subtree is going to return a value that can be already cut since there is another one which is better, we don't reach that subtree.
![[Pasted image 20231127173448.png]]

This can be obtained by a parameter, $\alpha$, which is the highest Max-node utility that search has found already on its path to n:
![[Pasted image 20231127173715.png|300x150]] ![[Pasted image 20231127173809.png|300x150]]
![[Pasted image 20231127173853.png|300x150]] ![[Pasted image 20231127173915.png|300x150]]

In a Min node n, if one of the successors already has utility $\leq \alpha$, then stop considering n. 
**Alpha-Beta Search**:
We can consider a spare, $\beta$ the lowest Min node utility that search has found already on its path to n. In a Max node n, if one of the successors already has utility $\geq \alpha$, then stop considering n.

![[Pasted image 20231127174616.png|300]] ![[Pasted image 20231127174632.png|300]]
![[Pasted image 20231127174642.png|300]] ![[Pasted image 20231127174651.png|300]]
![[Pasted image 20231127174817.png|300]] ![[Pasted image 20231127174839.png|300]]
![[Pasted image 20231127174911.png|300]] ![[Pasted image 20231127174931.png|300]]
![[Pasted image 20231127175108.png|300]] ![[Pasted image 20231127175124.png|300]]
![[Pasted image 20231127175135.png|300]] ![[Pasted image 20231127175209.png|300]]

Alpha beta search has two issues:
- It needs an accurate/fast evaluation function
- Has a very large branching factor, meaning there are many possible moves at each turn, making the game tree expansive and challenging to explore fully.

Last algorithm is the Monte Carlo Tree:
How to estimate the value of a state? Average utility over a number of simulations of complete games starting from the state (playout). A playout policy needs to bias the moves towards good ones. 

$\rightarrow$From what positions do we start the playouts, and how many
playouts do we allocate to each position?
- Pure Monte Carlo Search does simulations starting from the current state of the game and tracks which of the possible moves has the highest win percentage.
- Selection policy focuses the computation on important parts of the game tree, balancing exploration and exploitation.

Monte-Carlo Tree Search repeatedly follows the following steps:
1. Selection: traverse the tree starting at the root, applying the selection policy to choose successors until reaching a leaf node that has not been fully expanded.
2. Expansion: Grow tree by generating a new child of the leaf node by applying a new action.
3. Simulation: From the newly generated child node, perform a run of the game, selecting moves for both players according to the playout policy, to obtain the final reward.
4. Back-propagation: Use the result of the simulation to update all the search tree nodes going up to the root.
When time to decide is over, choose the “best” move and play it.
---
# References
