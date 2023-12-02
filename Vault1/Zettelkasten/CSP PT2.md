Date: 2023-12-02
Time: 17:54
Tags:
Up: 

---
# CSP PT2

**Inference**: deducing additional constraints, that follow from the already known constraints

Definition of **Equivalence**: 
Let $\gamma = (V, D, C)$ and $\gamma' = (V, D', C')$ be constraint networks sharing the same set of variables. We say that $\gamma$ and $\gamma$ are equivalent, written $\gamma \equiv \gamma$, if every solution of $\gamma$ is a solution of $\gamma'$ , and viceversa

Definition of **Tightness**:
Let $\gamma = (V, D, C)$ and $\gamma'= (V, D',C')$ be constraint networks sharing the same set of variables. We say that $\gamma$ is tighter than $\gamma$, written $\gamma \sqsubseteq \gamma$, if:
i. (i) For all v ∈ V : D0 v ⊆ Dv. (ii) For all u 6= v ∈ V : either Cuv 6∈ C or C 0 uv ⊆ Cuv. γ 0 is strictly tighter than γ, γ 0 @ γ, if at least one of these inclusions is strict.


---
# References
