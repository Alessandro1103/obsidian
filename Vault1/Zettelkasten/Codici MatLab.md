Date: 2024-04-19
Time: 15:36
Tags: #MatLab 
Up: 

---
# Codici MatLab

Questo codice è del midterm del 2023, esercizio 1, serve per la **derivata di una J**
``` MATLAB
J1=diff(J,q1)*q1dot
J2=diff(J,q2)*q2dot
J3=diff(J,q3)*q3dot
...
Jn=diff(J,qn)*qndot

Jtot=J1+J2+J3...+Jn;
```

Per ottenere la **Jacobiana**, e il **gradiente**:
``` MATLAB
clc
close all

syms q1 q2 q3

p = [cos(q1) + cos(q1+q2); sin(q1) + sin(q1+q2)]
J = jacobian(p,[q1,q2])
H = sin(q2)^2+sin(q3)^2
gradient = gradient(H, [q1 q2 q3])
```



---
# References
