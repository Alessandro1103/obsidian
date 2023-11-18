Date: 2023-11-18
Time: 10:58
Tags:
Up: [[IA]]

---
# Classical Search

## Part 1

### Classical Search Problems

A **Classical Search Problem** has this settings:
- Finite number of states and actions
- Single agent
- Fully observable
- Deterministic
- Static


A formal definition of **Search Problems**:
- The underlying base concept are state spaces
- State spaces are graphs
- Paths to goal states correspond to solutions
- Cheapest such paths correspond to optimal solutions

Every problem $\prod$ specifies a state space $\Theta$: 

Definition of **State Space**:
A state space is a 6-tuple $\Theta = (S, A, c, T, I, S^G)$ where: 
- $S$ is a finite set of *states*. 
- $A$ is a finite set of *actions*. 
- $c : A → R_0^+$ is the *cost function*. 
- $T \subseteq S × A × S$ is the *transition relation*. We require that $T$ is deterministic, i.e., for all $s$ ∈ $S$ and $a$ ∈ $A$, there is at most one state $s'$ such that $(s, a, s') \in T$. If such $(s, a, s')$ exists, then $a$ is applicable to $s$. 
- $I \in S$ is the *initial state*. 
- $S^G \subseteq S$ is the set of *goal states*. 
We say that $\Theta$ has the transition $(s, a, s')$ if $(s, a, s') \in T$. We also write  $s \rightarrow^a s'$, or $s \rightarrow s'$ when not interested in $a$. We say that $\Theta$ has unit costs if, for all $a \in A$, $c(a) = 1$.

Terms:
- $s'$ successor of $s$ if $s \rightarrow s'$
- $s$ successor of $s'$ if $s \rightarrow s'$
- $s'$ is reachable from $s$ if there exists a sequence of transitions that brings us from $s$ to $s'$.
- $s'$ is reachable (without reference) means reachable from $I$.
- $s$ is solvable if some $s' \in S^G$ is reachable from $s$; else, $s$ is a dead end.

Definition of **State Space Solutions**:
Let $\Theta = (S, A, c, T, I, S^G)$ be a state space, and let $s \in S$. $A$ *solution* for $s$ is a path from $s$ to some $s' \in S^G$. The solution is *optimal* if its cost is minimal among all solutions for $s$. A solution for $I$ is called a solution for $\Theta$. If a solution exists, then $\Theta$ is solvable.

### Descriptions

$\prod$ is the description of the problem
$\Theta$ is the state space corresponding to this description
Huge state spaces $\Theta$ can often be specified by small problem descriptions $\Theta$. 

Let's see different ways to describe a problem:

The **explicit description**:
$\prod = \Theta$: we simply input the state space graph

It's impossible for large state spaces, can be solved easily, in the size of the state space: Dijkstra.

The **blackbox description**:
- $InitialState()$: Returns the initial state of the problem
- $GoalTest(s)$: Returns a Boolean
- $Cost(a)$: Return the cost of action $a$
- $Actions(s)$: Return the set of actions that are applicable to state $s$
- $ChildState(s,a)$: Requires that action $a$ is applicable to state $s$

Huge state spaces can be specified with little program code

The **declarative description**:
- $P$: Set a Boolean variables (propositions)
- $I$: Subset of $P$, indicating which propositions are true in the initial state
- $G$: Subset of $P$, where s is a goal staffe if $G \subseteq s$
- $A$: Set of actions $a$
	- $pre_a$: precondition of $a$
	- $add_a$: add list
	- $del_a$: delete list
- $c$: Maps each $a \in A$ to its cost $c(a)$

Example (Missionaries and Cannibals):
![[Pasted image 20231118120447.png|340]]  ![[Pasted image 20231118120546.png|340]]

**Search Terminology**:
- Search node $n$: Contains a state reached by the search, plus information about how it was reached. 
- Path cost $g(n)$: The cost of the path reaching n. 
- Optimal cost $g^∗$: The cost of an optimal solution path. For a state $s$, $g^∗(s)$ is the cost of a cheapest path reaching $s$. 
- Node expansion: Generating all successors of a node, by applying all actions applicable to the node’s state $s$. Afterwards, the state $s$ itself is also said to be expanded. 
- Search strategy: Method for deciding which node is expanded next. 
- Open list: Set of all nodes that currently are candidates for expansion. Also called *frontier*. 
- Closed list: Set of all states that were already expanded. Used only in graph search, not in tree search. Also called explored set.

The *Duplicate Elimination* distinguish if we are working with a Tree Search(don't use it) or a Graph Search (use it):
- Maintain a closed list:
- Check for each generated state $s'$ whether $s'$ is in the closed list. If so, discard $s'$.
The *Tree search* implies also a one way reachable state, a state can be reached by only one predecessor.

### Blind Search

Does not require any input beyond the problem API

*Data Structure* for Every Search Node $n$ 
- $n$.State: The state (from the state space) which the node contains. 
- $n$.Parent: The node in the search tree that generated this node. 
- $n$.Action: The action that was applied to the parent to generate the node. 
- $n$.PathCost: $g(n)$, the cost of the path from the initial state to the node (as indicated by the parent pointers).

*Operations* on Search Nodes Solution($n$): 
- Returns the path to node $n$. (By backchaining over the $n$.Parent pointers and collecting n.Action in each step.) 
- ChildNode(problem,$n$,$a$): Generates the node $n'$ corresponding to the application of action $a$ in state $n$.State. That is: 
	- $n'$.State $:=$problem.ChildState($n$.State, $a$); 
	- $n'$.Parent $:=$ $n$; 
	- $n'$.Action $:=$ $a$; 
	- $n'$.PathCost $:=$ $n$.PathCost + problem.Cost($a$).

*Operations* for the Open List:
- Empty?(frontier): Returns true if there are no more elements in the open list. 
- Pop(frontier): Returns the first element of the open list, and removes that element from the list. 
- Insert(element, frontier): Inserts an element into the open list.

**BFS** (Breadth-First Search):
Expand nodes in the order they were produced (FIFO).
![[Pasted image 20231118124530.png]]
Guarantees: Completeness and Optimality
Time Complexity and Time Complexity: 
- Generated nodes: $O(b^d)$, where b is the maximal branching factor, d is the goal depth. (Operation: $b+b^2+\dots+b^d$)
- Node Expansion: $O(b^{d+1})$, since we would generate for each node at level d the successor (and do not check it) before finishing with the nodes at level d. 

**DFS** (Depth-First Search):
Expand the most recent nodes in (LIFO).
![[Pasted image 20231118144352.png|400]]
It is complete only if the state space is acyclic. It's not optimal since it chooses some direction and hopes for the best.
Space Complexity and Time Complexity:
Space: $O(bm)$, it stores only a single path form the root to a leaf node. Once the node has been expanded it can be removed from memory. $m$ is the maximal depth reached
Time: $O(b^m)$ it has to explore the combination of $b$ paths, with depth $m$ 

**Uniform-Cost Search**:
Expand nodes with lowest path cost $g(n)$:

## Part 2

---
# References
