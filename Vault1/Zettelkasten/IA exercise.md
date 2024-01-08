Date: 2024-01-03
Time: 10:11
Tags:
Up: 

---
# IA exercise

## STRIPS FDR and PDDL

**Problem Description:**

Consider the following scenario: Alex wants to organize a community library day. He has three different types of books: fiction, non-fiction, and children's books. He also has three different sections in the library where the books can be placed: Section A, Section B, and Section C. To organize the books, Alex has to label each section with the appropriate genre. Initially, Alex has not labeled any sections and can only work on one section at a time. He can carry one label at a time and can place it on any section.

Alex's goal is to correctly label Section A for fiction, Section B for non-fiction, and Section C for children's books.

**Task:**

(a) Give a STRIPS formalization of the initial state and the goal.

(b) Give a STRIPS formalization of the actions: LookAt, PickUpLabel, PlaceLabel, MoveToSection. Please use "object variables", i.e., write the actions up in a parameterized way and indicate, for each parameter, by which objects it can be instantiated (e.g., `move(x,y)` for all `x, y ∈ {SectionA, SectionB, SectionC}`).

**Predicates:**

- `LookingAt(section)`: To indicate that Alex is focusing on section `section ∈ {SectionA, SectionB, SectionC, none}`.
- `LabelAvailable(label)`: To indicate that label `label ∈ {Fiction, NonFiction, Children}` is available and not currently being held.
- `HandEmpty()`: To indicate that Alex's hand is empty.
- `HoldingLabel(label)`: To indicate that Alex is holding label `label ∈ {Fiction, NonFiction, Children}`.
- `Labeled(section, label)`: To indicate that label `label ∈ {Fiction, NonFiction, Children}` has been placed on section `section ∈ {SectionA, SectionB, SectionC}`.

Feel free to add more predicates if necessary to complete the formalization.

This problem requires you to define the initial state, the goal state, and the actions that can change the state in terms of the predicates provided. The actions will include preconditions and effects that will help reach the goal state from the initial state.

Solution:
``` STRIPS
V: {LookingAt(s) for each s ∈ {SectionA, SectionB, SectionC}, HandEmpty(), LabelAvailable(l) for each ∈ {Fiction, NonFiction, Children}, HoldingLabel(l) for each ∈ {Fiction, NonFiction, Children}, NotLabeled(s,l) for each l ∈ {Fiction, NonFiction, Children} and for each s ∈ {SectionA, SectionB, SectionC}, Labeled(SectionA,Fiction), Labeled(SectionA,Non-Fiction), Labeled(SectionB,Children)}

I: {LookingAt(none), HandEmpty(), LabelAvailable(l) for each l ∈ {Fiction, NonFiction, Children}, NotLabeled(s,l) for each l ∈ {Fiction, NonFiction, Children} and for each s ∈ {SectionA, SectionB, SectionC}}

G: {Labeled(SectionA, Fiction)
	Labeled(SectionB, NonFiction)
	Labeled(SecitonC, Children)
}

A: {
	ToLook(s1,s2)
		pre: LookingAt(s1)
		add: LookingAt(s2)
		del: LookingAt(s1)
	for each s1, s2 ∈ {SectionA, SectionB, SectionC} and s1!=s2
	TakeLabel(l)
		pre: HandEmpty() LabelAvailable(l)
		add: HoldingLabel(l)
		del: HandEmpty() LabelAvailable(l)
	for each l ∈ {Fiction, NonFiction, Children}
	DropLabel(l)
		pre: HoldingLabel(l)
		add: HandEmpty() LabelAvailable(l)
		del: HoldingLabel(l)
	for each l ∈ {Fiction, NonFiction, Children}	
	ToLabel(s,l)
		pre: HoldingLabel(l) LookingAt(s) NotLabeled(s,l)
		add: Labeled(s,l)
		del: NotLabeled(s,l)
	for each l ∈ {Fiction, NonFiction, Children} and
	for each s ∈ {SectionA, SectionB, SectionC}
	}
```

``` FDR
V: {LookingAt(s) = {T,F} for each s ∈ {SectionA, SectionB, SectionC}
	HandEmpty() = {T,F}
	LabelAvailable(l) = {T,F} for each l ∈ {Fiction, NonFiction, Children}
	HoldingLabel(l) = {T,F} for each l ∈ {Fiction, NonFiction, Children}
	Labeled(SectionA,Fiction) = {T,F} 
	Labeled(SectionB,NonFIction) = {T,F}
	Labeled(SectionC,Children) = {T,F}
}
I: {
	LookingAt(s) = F for each s ∈ {SectionA, SectionB, SectionC}
	HandEmpty() = T
	LabelAvailable(l) = T for each l ∈ {Fiction, NonFiction, Children}
	HoldingLabel(l) = F for each l ∈ {Fiction, NonFiction, Children}
	Labeled(SectionA,Fiction) = F 
	Labeled(SectionB,NonFIction) = F
	Labeled(SectionC,Children) = F
}

G: {
	Labeled(SectionA,Fiction) = T
	Labeled(SectionB,NonFIction) = T
	Labeled(SectionC,Children) = T
}

A: {
	ToLook(s1,s2)
		pre: LookingAt(s1) = T
		eff: LookingAt(s2) = T, LookingAt(s1) = F
	for each s1, s2 ∈ {SectionA, SectionB, SectionC}
	
	TakeLabel(l)
		pre: HandEmpty() = T, LabelAvailable(l) = T
		eff: HoldingLabel(l) = T, HandEmpty() = F, LabelAvailable(l) = F
	for each l ∈ {Fiction, NonFiction, Children}
	
	DropLabel(l)
		pre: HoldingLabel(l)
		eff: HandEmpty() LabelAvailable(l) HoldingLabel(l)
	for each l ∈ {Fiction, NonFiction, Children}
	
	ToLabel(s,l)
		pre: HoldingLabel(l) = T, LookingAt(s) = T, Labeled(s,l) = F
		eff: Labeled(s,l) = T, Labeled(s,l) = T
	for each l ∈ {Fiction, NonFiction, Children} and
	for each s ∈ {SectionA, SectionB, SectionC}
}
```


---
# References
