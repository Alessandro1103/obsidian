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

## Modeling the Initial State

Example:
![[Pasted image 20240102181920.png|300]]

``` PDDL
(define (problem blocksworld-prob1)
	(:domain blocksworld-ground)
	(:init (AisTopMost) (AonB) (BonC) (ConTable)
		   (DisTopMost) (DonE) (EonTable))
	(:goal (and (AisTopMost) (AonD) (DonC) (ConTable)
		   (EisTopMost) (EonB) (BonTable))))
```

It is not complete, it is missing the gripper

## Modeling the Actions

Example:
Let's say we want an action to put one block on another:
- we need to have the object on the gripper
- we need the support where to put it

``` PDDL
(:action stack-A-onto-B
	:precondition (and (holding A) (BisTopMost))
	:effect (and (not (holding A)) (not (BisTopMost)) (AonB) (gripperFree)
			(AisTopMost))
```

Now we want to remove one block from another:

``` PDDL
(:action unstack-A-from-B
	:precondition (and (gripperFree) (AonB) (AisTopMost)
	:effect (and (not (gripperFree)) (holding A) (not (AonB)) (not 
			(AisTopMost)) (BisTopMost)))
```


## Lifted Model

Since there are so many actions, we can generalize with predicates

Example of Domain:
``` PDDL
(define (domain blockworld-lifted)
	(:types block)
	(:predicates (topMost ?b - block)
				 (on ?b1 ?b2 - block)
				 (onTable ?b - block)
				 (holding ?b - block)
				 (gripperFree)
	)
	(:action take-from-table
		:parameters (?b - block)
		:precondition (and (gripperFree) (onTable ?b) (topMost ?b))
		:effect (and (not (gripperFree))
					 (holding ?b)
					 (not (onTable ?b))
					 (not (topMost ?b))))
	(:action unstack
		:parameters (?b1 ?b2 - block)
		:precondition (and (gripperFree) (topMost ?b1) (on ?b1 ?b2))
		:effect (and (not (gripperFree)) (holding ?b1) (not (topMost ?b2)) 
				(not (on ?b1 ?b2)) (topMost ?b2)))
	...
	)
```


---
# References
