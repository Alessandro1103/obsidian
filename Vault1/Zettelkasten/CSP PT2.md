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
AC3 (Arc Consistency 3):



---
# References
