Date: 2023-12-09
Time: 14:49
Tags: #English #IA #Università 
Up: [[IA]]

---
# AI Planning Formalisms

![[Pasted image 20231209145010.png|400]]
![[Pasted image 20231209145059.png|400]]

Example:
![[Pasted image 20231209145324.png|400]]

![[Pasted image 20231209145837.png|400]]

![[Pasted image 20231209150003.png|400]]

Example:
![[Pasted image 20231209151415.png|400]]

We can represent states or situations that are not reachable in a STRIPS state space, as long as they are consistent with the terminology
For example:
![[Pasted image 20231209150935.png|400]]

## FDR Planning

![[Pasted image 20231209151201.png|400]]

![[Pasted image 20231209151223.png|400]]

Example:
![[Pasted image 20231209151515.png|400]]

![[Pasted image 20231209151541.png|400]]

  
The main difference between a STRIPS state space and an FDR state space is that FDR state spaces allow for variables with finite domains. This means that in FDR state spaces, the values of variables can be restricted to a specific set of values. In STRIPS state spaces, on the other hand, the values of variables can be any proposition.

Another difference between the two state spaces is that FDR state spaces use a different transition function. In STRIPS state spaces, the transition function simply removes the preconditions of an action from the current state and adds the effects of the action to the current state. In FDR state spaces, on the other hand, the transition function overwrites the previous variable values with the new values specified by the effects of the action.



---
# References
