Date: 2023-12-10
Time: 15:49
Tags: #English #IA #Università 
Up: [[IA]]

---
# Progression and Regression

## Progression

is another word for Forward Search:
Let $\prod = (P, A, c, I, G)$ be a STRIPS planning task. The progression search space of $\prod$ is given by: 
- InitialState() = I 
- GoalTest(s) =
	- True if $G \subseteq s$
	- False otherwise 
- ChildState(s, a) = {$s' \ | \ \Theta_\prod \; has \ the \ transition \ s \rightarrow^a s'$} The same definition applies to FDR tasks $\prod = (V, A, c, I, G)$

## Regression

## Pros and Cons


---
# References

![[post-handout 2.pdf]]