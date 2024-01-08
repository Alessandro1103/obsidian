Date: 2024-01-05
Time: 15:05
Tags:
Up: 

---
# Note

Problem

(define (domain safe-party-domain)
	(:requirements :strips)
	(:predicates (agent ?a) (safe ?x) (adj ?x ?y) 
				 (movable ?x) (at ?a ?x) (group ?g))
	(:action move
		par: (?a ?from ?to)
		pre: (and (agent ?a) (at ?a ?from) (adj ?from ?to) 
			 (movable ?to))
		eff: (and (at ?a ?to) (not (at ?a ?from)))
	)
	(:action divide
		par: (?g ?a ?from ?to) 
		pre: (and (group ?g) (agent ?a) (at ?a ?from) (at ?group ?from) 
			 (movable ?to) (adj ?from ?to))
		eff: (and (safe ?from) (not (at ?group ?from))
			 (not (movable ?to)) (not (movable ?from))) 
	)
)

Domain

(define (problem safe-party-domain)
	(:domain safe-party-domain)
	(:object a g1 g2 A_0_0 A_0_1 A_0_2 A_1_0 A_1_1 A_1_2 A_2_0 A_2_1 
			 A_2_2 B_0_0 B_0_1 B_0_2 B_1_0 B_1_1 B_1_2 B_2_0 B_2_1 
			 B_2_2 )
	(:init (movable A_0_0) ...
		   (adj A_0_0 A_0_1) (adj A_0_1 A_0_0) ...
		   (adj A_0_0 A_1_0) (adj A_1_0 A_0_0) ...
		   (safe A_0_0) ...
		   (agent a) (group g1) (group g2) (at g1 A_1_1) (at g2 B_0_2) 
		   (at a A_2_1)
	(:goal (and (safe all)))
)

---
# Exercises
![[Pasted image 20240105164041.png]]

(define (domain MARRtino-works-in-hotel)
	(:requirements :strips)
	(:predicates (martino ?m) (dirty ?x) (at ?x ?y) (adj ?x ?y) 
				 (room ?x) (movableINTO ?) (behavior ?m) (frontDoor ?x))
	(:action move
		par: (?m ?from ?to)
		pre: (and (martino ?m) (at ?m ?from) (adj ?from ?to))
		eff: (and (at ?m ?to) (not (at ?m ?from)))
	)
	(:action enter
		par: (?m ?from ?to)
		pre: (and (martino ?m) (at ?m ?from) (adj ?from ?to) (room ?to)
			  (movableINTO ?to) (frontDoor ?from))
		eff: (and (at ?m ?to) (behavior ?m) (not (at ?m ?from)))
	)
	(:action quit
		par: (?m ?from ?to)
		pre: (and (martino ?m) (at ?m ?from) (adj ?from ?to) 
			  (room ?from) (frontDoor ?to))
		eff: (and (at ?m ?to) (not (behavior ?m)) (not (at ?m ?from)))
	)
	(:action clean
		par: (?m ?x)
		pre: (and (martino ?m) (room ?x) (at ?m ?x) (dirty ?x) 
			 (behavior ?m))
		eff: (and (not (dirty ?x)))
	)
)

(define (problem MARRtino-works-in-hotel)
	(:domain MARRtino-works-in-hotel)
	(:object m 
			 H_1_1 H_1_2 H_1_3 H_1_4 
			 H_2_1 H_2_2 H_2_3 H_2_4
			 H_3_1 H_3_2 H_3_3 H_3_4
			 H_4_1 H_4_2 H_4_3 H_4_4)
	(:init (room H_1_1) (room H_1_2) (room H_1_3) (room H_4_1) 
		   (room H_4_2) (room H_4_3) (movableINTO H_1_2) 
		   (movableINTO H_4_3) (dirty H_1_2) (dirty H_4_1) (dirty H_4_3)
		   (at m H_2_1) (adj H_1_1 H_1_2) (adj H_1_2 H_1_1) .. 
	)
	(:goal (not (dirty H_1_2) (dirty H_4_1) (dirty H_4_3)))
)

![[Pasted image 20240105180441.png|400]] 
![[Pasted image 20240105180455.png|300]]

State Space
<Pp1, Pp2, Pg1, Pg2, Pa, Pf1, Pf2, Sf1, Sf2, Ta, Sa, Cg1, Cg2>
Pp1 = {0,..,8}
Pp2 = {0,..,8}
Pg1 = {0,..,8}
Pg2 = {0,..,8}
Pa = {0,..,8}
Sf1 = {0,1}
Sf2 = {0,1}
Ta = {0,1}
Sa = {0,1}
Cg1 = {0,1}
Cg2 = {0,1}


Initial State
<8, 8, 6, 1, 5, 2, 5, 0, 0, 0, 0, 0, 0>
Goal State
<\_, \_, \_, \_, \_, \_, \_, 1, 1, \_, \_, \_, \_>

Operators
<P0,P1,P2,P3,P4,P5,P6,P7,G1,G2,G3,G4,G5,G6,G7> ->
<P0*,P1*,P2*,P3*,P4*,P5*,P6*,P7*,G1*,G2*,G3*,G4*,G5*,G6*,G7*>

Move(py,x)
description: move a player from a node to another one
preconditions:
effect: Ppy=x

TakeArrow()
description:  
preconditions: |Pg1-Pg2|!=1
effect: Ta=1

ShootArrow(Ppx,Pgy)
description:
preconditions: |Ppx-Pgy|=1 |Ppx-Pgz|!=1 where z is |y-z|=1
effect: Pa=Pgy Sa=1 Ta=0


![[Pasted image 20240105214619.png|500]]
![[Pasted image 20240105214641.png|300]]

State Space
<P0,P1,P2,M0,M1,M2,Pg,Sg,Pb,Rb,Cm,Am,Dp>
P1,P2,P3,M2,Pg,Pb = {0,..,8}
M0,M1 = {0,4}
Rb, Cm, Am, Sg, Dp = {0,1}
(Rb = ring the bell, Cm = Capture policemen, Am = Assault policemen, Sg = Steal gold, Dp = Distract policeman)

Initial Space
P0=1 P1=1 P2=1 M0=4 M1=4 M2=3 Pg=7 Sg=0 Pb=8 Rb=0 Cm=0 Am=0 Dp=0

Goal Space
Sg=1

Operators
Move(Px, y)
description: move a player Px to y
precondition: 
effect: Px=y

RingTheBell()
description: Ring the bell to distract the policeman
precondition: |Pb-M2|>2 Px\=\=Pb
effect: Dp=1 Rb=1

CapturePoliceman()
description: 
precondition: Dp=1 |M0-M2|>2 Rb=1
effect: Cm=1 M0=0 M1=0

AssaultPolicemen(Mx)
description: 
precondition: |M0-M2|>1 and (P0=P1=P2=M0 or Px=Py=M2)
effect: Am=1 

StealTheGold()
description:
precondition: |Am+Cm|=3 and Sg=0 and Px=Pg
effect: Sg=1

Solution:
Move(P0,3), Move(P1,3), AssaultPolicemen(M2), Move(P2,8), RingTheBell(), Move(P2,4), CapturePoliceman(), Move(P2,7), StealTheGold

![[Pasted image 20240106104532.png]]

(define (domain Change-Toys)
	(:requirements :strips)
	(:predicates (Georgie ?g) (Clown ?c) (Balloon ?b) (Boat ?b) 
				 (Holding ?x ?y) (at ?x ?y) (occupied ?x)
				 (Connected ?x ?y) (CommonPlace x?) (HandsFree ?x))
	(:action MoveG
		par: ?g ?from ?to
		pre: (and (Georgie ?g) (at ?g ?from) (occupied ?from)
			 (Connected ?from ?to)
		eff: (and (at ?g ?to) (not (at ?g ?from)) (occupied ?to) 
			 (not (occupied ?from)))
	)
	(:action DropGBo
		par: ?g ?b ?x
		pre: (and (Georgie ?g) (at ?g ?x) (CommonPlace x?) 
			 (Holding ?g ?b) (Boat ?b))
		eff: (and (not (Holding ?g ?b)) (at ?b ?x) (HandsFree ?x))
	)
	(:action PickGBa
		par: ?g ?b ?x
		pre: (and (Georgie ?g) (at ?g ?x) (CommonPlace x?)
			 (Balloon ?b) (at ?b ?x) (HandsFree ?g))
		eff: (and (Holding ?g ?b) (not (at ?b ?x)) (not(HandsFree ?x)))
	)
	... specular action for G
)

(define (problem Change-Toys)
	(:domain Change-Toys)
	(:object g c Ba Bo P0 P1 P2 P3 P4 P5 P6)
	(:init (Georgie g) (Clown c) (Balloon Ba) (Boat Bo) 
		   (Connected P0 P1) (Connected P1 P0)...
		   (Connected P1 P4) (Connected P4 P1)...
		   (at g P0) (at c P6)
		   (Holding g Bo) (Holding c Ba)
		   (occupied P6) (occupied P0)
		   (CommonPlace P1)
	)
	(:goal (Holding g Ba) (Holding c Bo)
		   (at g P3) (at c P5))
)

![[Pasted image 20240107102148.png|400]]

∃ ¬ ∀

1. ∀x(Bitter(x) or Sweet(x))
2. ∀x(Bitter(x)) or ∀y(Sweet(y))
3. ∃y∀x(Loved(x,y))
4. ∀x∀y(¬Loved(x,y))
5. ∃x(Noisy(x) -> ∀y(Annoyed(y)))

![[Pasted image 20240107104356.png|400]]

∃ ¬ ∀

6. ∀x(Frogs(x) -> Green(x))
7. ∀x(Frogs(x) -> ¬Green(x)) = ¬∃x(Frogs(x) and Green(x))
8. ¬∃x(Frogs(x) and Green(x))
9. ∃x(Frogs(x) and ¬Green(x))
10. ∃x(Mechanic(x) and Likes(x,Bob))
11. ∃x(Mechanic(x) and Likes(x,x))
12. ∀x(Mechanic(x) and Likes(x,Bob))
13. ∃x(Mechanic(x) and ∀y(Nurse(y) -> Likes(x,y)))
14. ∃x(Mechanic(x) and ∀y(Nurse(y) -> Likes(y,x)))



---
# References
