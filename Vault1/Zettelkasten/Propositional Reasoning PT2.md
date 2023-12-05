Date: 2023-12-05
Time: 10:06
Tags: #Università #English #IA  
Up: [[IA]]

---
# Propositional Reasoning PT2

Alcune parti sono poco chiare...

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
1. Conversion to Clauses:
    - $C1​=(A∨B)$
    - $C2​=(¬A∨C)$
    - $C3​=(¬B∨C)$
    - $C4​=(¬C∨D)$
2. Resolution Steps:
    - $C1$​ and $C2$​ on $A: (B∨C)$
    - Resolve the result with $C3$​ on $B: C$
    - Resolve the result with $C4​$ on $C: D$
3. Result: The formula is satisfied with $A=True$, $B=True$, $C=True$, and $D=True$.

Define the number of decisions (when the algorithm chooses a variable and assigns it a truth value (either True or False)) of a DPLL run as the total number of times a truth value was set by either unit propagation or the splitting rule. 
If DPLL returns “unsatisfiable” on $\Delta$, there exists a resolution derivation of unsatisfiability for $\Delta$, $\Delta$ $\vdash$ $\Box$. A resolution derivation is a series of application of the resolution rule to clauses, leading to a contradiction (empty clause $\Box$). The length of the resolution derivation is at most the number of decisions made by DPLL during its run.

**Example**:
![[Pasted image 20231205112113.png|300]] 
![[Pasted image 20231205112055.png|300]]

DPLL makes the same mistakes over and over again.

## UP Conflict Analysis

Definition of **Implication Graph**:
Let $\Delta$ be a set of clauses, and consider any search branch $\beta$ of DPLL on $\Delta$. The implication graph $G^{impl}$ is a directed graph. Its vertices are the choice and implied literals along $\beta$, as well as a separate conflict vertex $\Box_C$ for every clause $C$ that becomes empty

- Value of $P$ set by the splitting rule: choice literal, $P$ for $I(P) = 1$, respectively $¬P$ for $I(P) = 0$. 
- Value of $P$ set by the UP rule: implied literal $P$ respectively $¬P$. 
- Empty clause derived by UP: conflict literal $\Box$.

Example:
![[Pasted image 20231205113405.png|300]] 

Definition of **Conflict Graph**:
Let $\Delta$ be a set of clauses, and let $G^{impl}$ be the implication graph for some search branch of DPLL on $\Delta$. A *conflict graph* G$^{confl}$ is a sub-graph of $G^{impl}$ induced by a subset of vertices such that: 
1. G$^{confl}$ contains exactly one conflict vertex $\Box_C$.
2. If $l'$ is a vertex in G$^{confl}$, then all parents of $l'$, i.e. vertices $\bar{l}_i$ with a G$^{impl}$ $arc (\bar{l}_i , l' )$, are vertices in G$^{confl}$ as well. 
3. All vertices in G$^{confl}$ have a path to $\Box_C$.

A conflict graph captures "what went wrong" in a failed node. Starting at a conflict vertex, backchain through the implication graph until reaching choice literals


## Clause Learning
It is a technique used to enhance the efficiency of the solver by learning from conflicts encountered during the search process.


## Phase Trans.



---
# References
