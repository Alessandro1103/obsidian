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

It is based on the resolution rule, which is a logical inference rule used in propositional logic.

**Example**:
$(A∨B)∧(¬A∨C)∧(¬B∨C)∧(¬C∨D)$
DPLL:
1. Initial Assignment: Start with an empty assignment.
2. Decision: Choose a variable to assign a truth value. Let's start with $A=True$.
3. Unit Propagation: Simplify the formula based on the assignment. In this case, the first clause becomes $(True∨B)$.
4. Decision: Choose another variable, say $B=True$.
5. Unit Propagation: Simplify the formula. Now, the second and third clauses become $C$.
6. Decision: Assign $C=True$.
7. Unit Propagation: The fourth clause becomes $D$.
8. Result: The formula is satisfied with $A=True$, $B=True$, $C=True$, and $D=True$
Resolution:

1. **Conversion to Clauses:**
    - �1=(�∨�)C1​=(A∨B)
    - �2=(¬�∨�)C2​=(¬A∨C)
    - �3=(¬�∨�)C3​=(¬B∨C)
    - �4=(¬�∨�)C4​=(¬C∨D)
2. **Resolution Steps:**
    - Resolve �1C1​ and �2C2​ on �A: (�∨�)(B∨C)
    - Resolve the result with �3C3​ on �B: �C
    - Resolve the result with �4C4​ on �C: �D
3. **Result:** The formula is satisfied with �=TrueA=True, �=TrueB=True, �=TrueC=True, and �=TrueD=True.

## UP Conflict Analysis



## Clause Learning



## Phase Trans.



---
# References
