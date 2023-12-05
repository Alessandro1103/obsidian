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
Terms without variables are ground terms. Terms represents object.

Definition of **Atom**:
Let \Sigma be a signature. Then:
1. $\top$ and $\bot$ are $\Sigma$-atoms
2. If $t_1, t_2, \dots, t_n$ are terms and $P \in \Sigma$ is an $n$-ary predicate symbol, then $P(t_1, t_2, \dots, t_n)$ is a $\Sigma$-atom
Atoms without variables are ground atoms. Atoms represent atomic statements about objects

## Semantics

Example:
$\forall x[Block(x) \rightarrow Red(x)], Block(A)$
For all objects $x$, if $x$ is a block, then $x$ is red. $A$ is a block.

Definition of **Interpretation**:
Let $\Sigma$ be a signature. A $\Sigma$-interpretation is a pair $(U,I)$ where $U$, the *universe*, is an arbitrary non-empty set $[U=\{o_1, o_2, \dots\}]$, I is a function, notated as superscript, so that
1. I maps constant symbols to elements of $U:c^I \in U$
	$[Lassie^I = o_1]$
2. I maps $n$-ary predicate symbols to $n$-ary relations over U:
	$P^I\subseteq U^n \ \ [Dog^I={o_1, o_3}]$
3. I maps $n$-ary predicate symbols to $n$-ary functions over U:
	$f^I \in [U^n \rightarrow U] \ \ [FoodOf^I = \{(o_1 \rightarrow o_4),(o_2 \rightarrow o_5),\dots \}]$




---
# References
