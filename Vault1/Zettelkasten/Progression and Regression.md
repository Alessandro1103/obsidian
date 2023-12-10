Date: 2023-12-10
Time: 15:49
Tags: #English #IA #Università 
Up: [[IA]]

---
# Progression and Regression

## Progression

is another word for Forward Search:
Let $\prod = (P, A, c, I, G)$ be a STRIPS planning task. The *progression* search space of $\prod$ is given by: 
- $InitialState()$ = $I$ 
- $GoalTest(s)$ =
	- True if $G \subseteq s$
	- False otherwise 
- $ChildState(s, a)$ = {$s' \ | \ \Theta_\prod \; has \ the \ transition \ s \rightarrow^a s'$} 

The same definition applies to FDR tasks $\prod = (V, A, c, I, G)$

## Regression

is another word for Backward Search:
Let $\prod = (P, A, c, I, G)$ be a STRIPS planning task. The *regression* search space of $\prod$ is given by: 
- $InitialState()$ = $G$ 
- $GoalTest(s)$ =
	- True if $g \subseteq I$
	- False otherwise 
- $ChildState(s, a)$ = {$g' \ | \ g' = regr(g,a)$} 

The same definition applies to FDR tasks $\prod = (V, A, c, I, G)$

Definition of FDR Regression:
Let $(V, A, c, I, G)$ be an $FDR$ planning task, $g$ be a partial variable assignment, and $a \in A$. We say that $g$ is regressable over a if
1. $eff_a \cap g \neq \emptyset$
2. there is no $v \in V$ s.t. $v \in V [eff_a] \cap V [g]$ and $eff_a (v) \neq g(v)$
3. there is no $v \in V$ s.t. $v \notin V [eff_a]$, $v \in V[pre_a] \cap V [g]$, and $pre_a(v) \neq g(v)$

![[Pasted image 20231210160305.png]]

## Pros and Cons


---
# References

![[post-handout 2.pdf]]