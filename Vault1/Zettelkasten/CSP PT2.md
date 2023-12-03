Date: 2023-12-02
Time: 17:54
Tags:
Up: 

---
# CSP PT2

**Inference**: deducing additional constraints, that follow from the already known constraints

Definition of **Equivalence**: 
Let $\gamma = (V, D, C)$ and $\gamma' = (V, D', C')$ be constraint networks sharing the same set of variables. We say that $\gamma$ and $\gamma$ are equivalent, written $\gamma \equiv \gamma$, if every solution of $\gamma$ is a solution of $\gamma'$ , and viceversa
==(I.E we have the same results)==

Definition of **Tightness**:
Let $\gamma = (V, D, C)$ and $\gamma'= (V, D',C')$ be constraint networks sharing the same set of variables. We say that $\gamma$ is tighter than $\gamma$, written $\gamma \sqsubseteq \gamma$, if:
1. For all $v \in V: D'_v \subseteq D_v$. 
2. For all $u \neq v \in V$ : either $C_{uv} \neq C$ or $C'{uv} \subseteq C_{uv}$. 
$\gamma'$ is *strictly tighter* than $\gamma$, $\gamma \sqsubset \gamma$, if at least one of these inclusions is strict.
==(I.E we have more constraints)==

**Theorem: Inference = Equivalence + Tightness**:
Theorem. Let $\gamma$ and $\gamma'$ be constraint networks s.t. $\gamma' \equiv \gamma$ and $\gamma' \sqsubset \gamma$. Then, $\gamma'$ has the same solutions as $\gamma$ but fewer consistent partial assignments than $\gamma$.

The more complex the inference, the smaller the number of search nodes, but the larger the runtime needed at each node. We can apply the inference before search starts or at every recursive call of backtracking. 

Definition **Arc Consistency**: 
Let $\gamma = (V, D, C)$ be a constraint network. 
1. A variable $u \in V$ is arc consistent relative to another variable $v \in V$ if either $C_{uv} \notin C$, or for every value $d \in D_u$ there exists a value $d' \in D_v$ such that $(d, d') \in C_{uv}$. 
2. The network $\gamma$ is arc consistent if every variable $u \in V$ is arc consistent relative to every other variable $v \in V$**.

**Forward Checking** (Inference, version1):
for each variable choose a domain variable, and upgrade all the other variable following the constraints. then choose a random domain variable for a general variable. 
It is sound = return an equivalent network

**Enforcing Arc Consistency** (inference, version2):
remove variable domain values until $\gamma$ is arc consistent
It is sound = return an equivalent network
It is subsumes Forward Checking = return a tighter network 

There are 2 algorithms, but first we need:
**Revise**:
the algorithm removes the domain variables that violate constraints.

**AC1** (Arc Consistency 1):
it use revise for all variables in both directions
**AC3** (Arc Consistency 3):
we create a set of constraints between neighbouring nodes, by revising, if successful, we link a neighbouring node to the one whose domain has been changed by the revise



![[Pasted image 20231203124546.png|400]]
![[Pasted image 20231203124553.png|400]]
![[Pasted image 20231203124601.png|400]]
u add the element removed before
![[Pasted image 20231203124614.png|400]]
![[Pasted image 20231203124622.png|400]]
![[Pasted image 20231203124631.png|400]]
![[Pasted image 20231203124637.png|400]]
order is important to understand when the element in the domain of that variable is not used, e.g. in (v1,v2), 5 is not used


**Theorem: Runtime of AC-3**:
Let $\gamma = (V, D, C)$ be a constraint network with $m$ constraints, and maximal domain size $k$. Then $AC-3(\gamma)$ runs in time $O(mk^3)$

This because *Revise* takes time $O(k^2)$

![[Pasted image 20231203133936.png]]

## Decomposition
we can exploit the structure of a network to decompose it into smaller parts that are easier to solve

Definition of **Constraint Graph**:
Let \gamma = (V, D, C) be a constraint network. The constraint graph of \gamma is the undirected graph whose vertices are the variables $V$ and that has an arc $\{u, v\}$ if and only if $C_{uv} \in C$. ![[Pasted image 20231203162101.png|300]]

**Theorem: Disconnected Constraint Graphs**:
Let $\gamma = (V, D, C)$ be a constraint network. Let $a_i$ be a solution to each connected component $V_i$ of the network's constraint graph. Then $a := \bigcup_i a_i$ is a solution to $\gamma$.

**Theorem: Acyclic Constraint Graphs**:
Let $\gamma = (V, D, C)$ be a constraint network with $n$ variables and maximal domain size $k$, whose constraint graph is acyclic. Then we can find a solution for $\gamma$, or prove $\gamma$ to be inconsistent, in time $O(nk^2)$.

**Algorithm: AciclicCG($\gamma$)**:
1. From a graph create a tree
2. Order parents and then children
3. Revise (last parent-> last son), if domain of parent is null, it's inconsistent

![[Pasted image 20231203163127.png|300]] ![[Pasted image 20231203163138.png|300]]
![[Pasted image 20231203163310.png|300]] ![[Pasted image 20231203163320.png|300]]
![[Pasted image 20231203163358.png|300]] ![[Pasted image 20231203163411.png|300]]
![[Pasted image 20231203163424.png|300]] 

## Cutsets

Definition of **Cutset**:
Let $\gamma = (V, D, C)$ be a constraint network, and $V_0 \subseteq V$. $V_0$ is a cutset for $\gamma$ if the sub-graph of $\gamma$’s constraint graph induced by $V\ \backslash \ V_0$ is acyclic. $V_0$ is optimal if its size is minimal among all cutsets for $\gamma$
==the cutset is the subset of a graph acyclic==




---
# References
