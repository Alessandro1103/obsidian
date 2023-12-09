Date: 2023-12-09
Time: 16:56
Tags: #Università #English #IA 
Up: [[IA]]

---
# PDDL

## Schematic Encodings

Schematics encodings use variables that range over objects:
- Predicates instead of STRIPS propositions. Arity: number of vars
- Action schemas instead of STRIPS actions. Arity: number of vars

Schematic action (respectively (pre, add, del)) example:
![[Pasted image 20231209170039.png|300]]

corresponds to the actions:
![[Pasted image 20231209170153.png|400]]

![[Pasted image 20231209170432.png|400]]

## PDDL Grammar

Example:
``` PDDL
(and (or (on A B) (on A C)) 
	 (or (on B A) (on B C)) 
	 (or (on C A) (on A B)))
```

![[Pasted image 20231209170613.png|400]]


## Extensions


---
# References
