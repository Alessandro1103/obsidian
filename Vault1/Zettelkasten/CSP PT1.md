Date: 2023-11-28
Time: 19:01
Tags: #English #IA #Università 
Up: [[IA]]

---
# CSP PT1

A constraint is a condition that every solution must satisfy.
Given:
	A set of variables, each associated with its domain
	A set of constraints over these variables
Find:
	An assignment of variables to values

## Networks

A constraint network (constraint satisfaction problem (CSP)) is defined by:
- A finite set of variables
- A finite domain for each variable
- A set of constraints

Definition of **Constraint Network**: 
A binary constraint network is a triple $\gamma = (V, D, C)$ where:
- $V = \{v_1, . . . , v_n\}$ is a finite set of variables.
- $D = \{D_{v1} , . . . , D_{vn}\}$ is a corresponding set of finite domains.
- $C = \{C_{\{u,v\}}\}$ is a set of binary relations (constraints), where for each C_{\{u,v\}} we have $u, v \in V$ , $u \neq v$, and $C_{\{u,v\}} \subseteq D_u × D_v$ .
We require that $C_{\{u,v\}}, C_{\{x,y\}} \in C \implies \{u, v\} \neq \{x, y\}$. We will write $C_{uv}$ instead of $C_{\{u,v\}}$ for brevity.

Example:
![[Pasted image 20231128192052.png]]

An **Unary Constraint** is a relation $C_v$ over a single variable, i.e., a subset $C_v \subseteq D_v$ of that variable's domain. 

## Consistency

Definition of **Assignment**:
Let $\gamma = (V, D, C)$ be a constraint network. A partial assignment is a function $a : V' \rightarrow \bigcup_{v \in V} D_v$ where V ′ ⊆ V and $a(v) \in D_v$ for all $v \in V'$. If $V′ = V$, then $a$ is a total assignment, or
assignment in short.
A partial assignment assigns some variables to values from their respective domains. A total assignment is defined on all variables. 

Definition of **Consistency**:
Let $\gamma = (V, D, C)$ be a constraint network, and let $a$ be a partial assignment. We say that $a$ is inconsistent if there exist variables $u, v \in V$ on which $a$ is defined, with $C_{uv} \in C$ and
$(a(u), a(v))  \notin C_{uv}$. In that case, $a$ violates the constraint $C_{uv}$. We say that $a$ is consistent if it is not inconsistent.

Definition of **Solution**:
Let $\gamma = (V, D, C)$ be a constraint network. If $a$ is a total consistent assignment, then $a$ is a solution for γ. If a solution to $\gamma$ exists, then $\gamma$ is solvable; otherwise, $\gamma$ is inconsistent.

Definition of **Extensibility**:
Let $\gamma = (V, D, C)$ be a constraint network, and let $a$ be a partial assignment. We say that $a$ can be extended to a solution if there exists a solution $a'$ that agrees with $a$ on the variables where $a$ is defined.

If $a$ can be extended to a solution then $a$ is consistent.



---
# References
