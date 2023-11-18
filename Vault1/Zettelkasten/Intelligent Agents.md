Date: 2023-11-18
Time: 09:29
Tags: #IA #Università #English 
Up: [[IA]]

---
# Intelligent Agents

An **Agent** is something that perceive the environment through sensor and act through actuators (humans, animals...). The agent does what it does trying to maximize a performance measure. This is not always possible, due to mechanism or algorithm loss. 
There are 2 kind of agents:
- Omniscient agent: knows everything about the environment and the actual effects of its action.
- Rational agent: always makes the best of what he has at its disposal.

An agent has a performance measure M and a set A of actions. Given a perception sequence P, as well as knowledge K about the world, it selects an action a∈A. This action "a" is *optimal* if it maximizes the expected value of M, given the evidence provided by P and K. The agent is rational if it always chooses an optimal a (this depends on what we consider acceptable). An observation can be a action too, since it must be done actively in some occasion. The decision often has to be approximate since it would take too much time/memory. 

Agent = Architecture + Program

![[Pasted image 20231118095946.png]]

We can distinguish other kind of agents depend on what we need:
- Table-Driven Agents: like a function it receives a perception, or a sequence of perceptions and by a "table" the agent knows what to do.
- Reflex Agents: maps between current perception and actions. Normally has 2 states.
- Reflex Model-based Agents: it tracks by an *Internal state* the to work where it can't see.
- Goal-Based Agents: create an hypothesis on the future. 
- Utility-Based Agents: works on a *utility function* that maps a state to a number which represents how desirable the state is.
- Learning Agents: be able to learn, useful if we dont know something about the environment. *Exploitation*: selects actions, *exploration* suggests actions to learn. 

The **environment** can be:
- Fully observable vs Partially observable
- Deterministic vs Stochastic: is the next state of the environment completely determined by the current state and the selected action?
	- Stochastic: uncertainty is quantified by using probabilities
	- Non-deterministic: uncertainty as actions with multiple outcomes, don't use probability.
	- Strategic: if the only non-determinism are actions of other agents.
- Episodic vs Sequential: if we consider an action only for the moment I choose it or thinking about the initial state and the goal.
- Static vs Dynamic: if it stays or change during the time. Semi-dynamic if the agent's performance score changes.
- Discrete vs Continuous
- Single agent vs Multi agent, if multi:
	- Competitive
	- Cooperative

The **approach** can be either:
- Domain-specific
- General


---
# References
