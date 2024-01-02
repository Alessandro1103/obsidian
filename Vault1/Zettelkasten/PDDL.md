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

![[Pasted image 20231209170613.png|300]] ![[Pasted image 20231209170728.png|300]]

![[Pasted image 20231209170953.png|300]] ![[Pasted image 20231209171226.png|300]]
![[Pasted image 20231209171404.png|300]] ![[Pasted image 20231209171255.png|300]] ![[Pasted image 20231209171308.png|300]] ![[Pasted image 20231209171333.png|300]] 

## Modeling the initial state

Example:
![[Pasted image 20240102181920.png|300]]

(define (problem blocksworld-prob1)
	(:domain blocksworld-ground)
	(:init (AisTopMost) (AonB) (BonC) (ConTable)
		   (DisTopMost) (DonE) (EonTable))

---
# References
