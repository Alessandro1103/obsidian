Date: 2024-01-03
Time: 16:49
Tags:
Up: 

---
# IA exam arguments

## Graph algorithms

### Definitions

**Evaluation function f(n)**: is a heuristic that uses problem-specific knowledge to estimate the cost of the cheapest path from node n to the goal, guiding the search algorithm more efficiently towards the solution

**The perfect heuristic**: is a heuristic function h(n) that provides the exact cost of the cheapest path from any state n to a goal state. In this context, if h(n)=0, it indicates that state n is a goal state.
![[Pasted image 20240104001559.png|200]]

### Alpha-Beta pruning

Alpha-beta pruning is an optimization technique for the minimax algorithm that skips evaluating branches in a game tree if they cannot possibly influence the final decision, thereby reducing the number of nodes that are evaluated in the search tree.
2 fundamental rules:
- prune if alpha>=beta
- at level MAX, only alpha change, viceversa

### MinMax algorithm

The minimax algorithm is a decision rule used for minimizing the possible loss in a worst-case scenario when the opponent is trying to maximize their own score, typically applied in game theory and artificial intelligence to find the optimal move for a player assuming that the opponent is also playing optimally.

### A* search

**Optimal?** Yes, if the heuristic we use is consistent (h(n)≤c(n,n′)+h(n′))
**Complete?** Yes, because thanks to g(n) in f(n) we avoid being stuck in a loop

### Uniform Lost Search

Uniform Cost Search means we always expand the lowest state

**Optimal?** Yes, it always find the least cost costly path
**Complete?** Yes, always find solution if exist, it never gets stuck because it explore all possible path

### Iterative Deepening Search

**Optimal?** If the arcs are weighted it perform like BFS so it gets the solution that is least deep
**Complete?** Yes, because it explore all possible path, it does not get stuck

The IDS algorithm, works by repeatedly executing a depth-limited search with increasing depth limits until the goal is found, combining the benefits of depth-first search's space efficiency and breadth-first search's completeness.

Example:
![[Pasted image 20240103234716.png|300]]

### BFS
The Breadth-First Search (BFS) algorithm systematically explores a graph by visiting all nodes at the current depth level before proceeding to nodes at the next depth level.

Example:
![[Pasted image 20240103235327.png|200]] ![[Pasted image 20240103235351.png|200]]

### DFS
The Depth-First Search (DFS) algorithm explores a graph or tree by starting at the root node and expanding as far as possible along each branch before backtracking.

Example:
![[Pasted image 20240103235316.png|200]] ![[Pasted image 20240103235418.png|200]]

### HillClimbing

![[Pasted image 20240106195354.png|300]] 
![[Pasted image 20240106195320.png|300]]

## Propositional Logic

### Definitions
A knowledge base is ==consistent== if it admits at least one model.

### CNF

### Unification
Modify 2 functions to be equal
The variable can transformed in parameters and another functions

Example:
- Expression 1: f(x,g(y))
- Expression 2: f(h(a),g(b))

Unification process:
- x can be unified with h(a)
- y can be unified with b
So: {x/h(a),y/b}

We cant unify if:
- different name of functions: f(x) and g(x)
- number of arguments: f(x,y) and f(x)
- contradiction: f(x,y) and f(a,b)
- cyclic: f(x) and f(g(x))
			 f(x,g(x)) and f(a,b)  (x cant be variable and function)
- clash of variable and constant: f(x,a) and f(a,y)

### FOL
P→Q = ¬P∨Q
∀x∃y(P(x,y)) = ∀x(P(x,f(x)))
∀x¬P(x) = ¬∃xP(x)

∃x replace x=a if there is no ∀ before
∃x replace x=s(x) if there is ∀ before


### Resolution
Example:
![[Pasted image 20240103233638.png|300]]

### DPLL

Example:
![[Pasted image 20240104142121.png|300]]

The ==clause learning== helps resolving the conflicts:
1. Check when there is a conflict (usually is the last operation)
2. Check the last Splitting Rule
3. Assign the opposite value to the Splitting Rule
4. Add the variable to the CNF
5. Continue from that Splitting Rule (intuitively we continue doing Unit Propagation, since we'll have {OppositeVariable})

Example:
![[Pasted image 20240104142138.png|300]]
![[Pasted image 20240104142153.png|300]] ![[Pasted image 20240104142225.png|300]]

## Languages

### Strips

#### Progression
#### Regression

### FDR

### PDDL

---
# References
