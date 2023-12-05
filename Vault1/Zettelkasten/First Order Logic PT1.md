Date: 2023-12-05
Time: 17:09
Tags: #English #Università #IA 
Up: [[IA]]

---
# First Order Logic PT1

![[post-handout.pdf]]

## Syntax

- Variables: $x$, $x_1$, $x_2$, $\dots$, $x'$, $x''$, $\dots$, $y$, $\dots$, $z$, $\dots$
- Truth/Falseness: $\top$, $\bot$
- Operators: $\neg$, $\lor$, $\land$, $\rightarrow$, $\leftrightarrow$
- Quantifiers: $\forall$, $\exists$ 

Definition of **Signature**:
A signature $\Sigma$ in predicate logic is a finite set of constant symbols, predicate symbols, and function symbols

Constant symbols: $BlockA$, $BlockB$, $\dots$
Predicate symbols: $Block(.)$, $Above(.)$, $\dots$
Function symbols: $WeightOf(.)$, $Succ(.)$, $\dots$

**Example**:
$\forall [Dog(x) \rightarrow \exists y Chases(x,y)]$, which in words means "Every dog chases something"

Definition of **Term**:
Let $\Sigma$ be a signature. Then:
1. Every variable and every constant symbol is a $\Sigma$-term
2. If $t_1, t_2, \dots, t_n$ are $\Sigma$-terms and $f \in \Sigma$ is an $n$-ary function symbol, then $f(t_1, t_2, \dots, t_n)$ also is a $\Sigma$-term
Terms without variables are ground terms



---
# References
