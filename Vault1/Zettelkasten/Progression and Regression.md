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
Start at goal, and regress over actions to produce subgoals, until a subgoal is contained in the initial state.
Condition required: If $g'=regr(g,a)$, then for all $s'$ with $s' |= g'$, we have $s'[[a]]=s$ where $s |=g$.

Definition of **FDR Regression**:
Let $(V, A, c, I, G)$ be an $FDR$ planning task, $g$ be a partial variable assignment, and $a \in A$. We say that $g$ is regressable over a if
1. $eff_a \cap g \neq \emptyset$
2. there is no $v \in V$ s.t. $v \in V [eff_a] \cap V [g]$ and $eff_a (v) \neq g(v)$
3. there is no $v \in V$ s.t. $v \notin V [eff_a]$, $v \in V[pre_a] \cap V [g]$, and $pre_a(v) \neq g(v)$

![[Pasted image 20231210160305.png]]

Example:
![[Pasted image 20231210163017.png|400]]

Definition of **STRIPS Regression**: 
Let $(P, A, c, I, G)$ be a STRIPS planning task, $g \subseteq P$, and $a \in A$. We say that $g$ is regressable over a if 
1. $add_a \cap g \neq \emptyset$
2. $del_a \cap g = \emptyset$

![[Pasted image 20231210163035.png|400]]

## Pros and Cons

In favor of progression: 
- Regression has in the past often had serious trouble getting lost in gazillions of solvable but unreachable states. Reachable dead end states tend to be less frequent in practice. 
- Progression allows easy formulation of searches for more complex planning formalisms (numbers, durations, uncertainty, you name it).

---
# References

![[post-handout 2.pdf]]