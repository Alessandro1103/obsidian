Date: 2023-12-05
Time: 10:06
Tags: #Università #English #IA  
Up: [[IA]]

---
# Propositional Reasoning PT2


![[slideIA 1.pdf]]

## Davis-Putnam

The DPLL procedure is a complete SAT solver. A SAT problem is a boolean satisfiability problem (NP-complete).

**Example**:
![[Pasted image 20231205101501.png|300]] ![[Pasted image 20231205101523.png|300]]

We can say that $\Delta$ is unsatisfiable if the unit propagation is sound (return the same result -> does not improve)

The DPLL is similar to the BacktrackingWithInference, with Inference() = unit propagation

The Unit Propagation (UP) Rule corresponds to a calculus:
Definition of **Unit Resolution**:
Unit Resolution is the calculus consisting of the following inference rule:
$$
\frac{C \dot{\cup}\{\bar{l}\}, \{l\}}{C}
$$
that is, if $\Delta$ contains parent clauses of the form $C \dot{\cup}\{\bar{l}\}$ and $\{l\}$, the rule allows to add the resolvent clause $C$.
Unit propagation = Resolution restricted to the case where one of the parent clauses is unit.
UP is sound and not complete (UP makes only limited inferences, as long as there are unit clauses. It does not guarantee to infer everything that can be inferred)

## Resolution



## UP Conflict Analysis



## Clause Learning



## Phase Trans.



---
# References
