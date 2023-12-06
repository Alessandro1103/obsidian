Date: 2023-12-06
Time: 11:59
Tags:
Up: 

---
# First Order Logic PT2

![[post-handout 1.pdf]]

## Propositional

## Substitution & Unification

## FOL Resolution

- A literal $l$ is an atom or the negation thereof; the negation of a literal is denoted $\bar{l}$ (e.g., $\bar{\neg Q}$ = $Q$). 
- A clause $C$ is a set (=disjunction) of literals. 
- Our input is a set $\Delta$ of clauses. 
- The *empty clause* is denoted $\Box$. 
- A *calculus* is a set of inference rules.

Definition of **Derivations**: We say that a clause $C$ can be derived from $\Delta$ using calculus $R$, written $\Delta \vdash_R C$, if (starting from $\Delta$) there is a sequence of applications of rules from R, ending in C.

**Soundness**: A calculus R is sound if $\Delta \vdash C$ implies $\Delta \models C$. 
**Completeness**: A calculus R is refutation-complete if $\Delta \models \perp$ implies $\Delta \vdash_R \Box$, i.e., if $\Delta$ is unsatisfiable then we can derive the empty clause.

---
# References
