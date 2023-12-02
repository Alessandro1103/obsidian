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

**Theorem**:
Theorem. Let $\gamma$ and $\gamma'$ be constraint networks s.t. $\gamma' \equiv \gamma$ and $\gamma' \sqsubset \gamma$. Then, $\gamma'$ has the same solutions as $\gamma$ but fewer consistent partial assignments than $\gamma$.




---
# References
