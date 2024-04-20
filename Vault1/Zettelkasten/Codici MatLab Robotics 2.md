Date: 2024-04-19
Time: 15:36
Tags: #MatLab 
Up: [[Robotics2]]

---
# Codici MatLab Robotics 2

Questo codice è del midterm del 2023, esercizio 1, serve per la **derivata di una J**
``` MATLAB
clc
close all

syms l1 l2 l3 l q1 q2 q3 rx1 ry1 rx2 ry2 rx3 ry3 q1dot q2dot q3dot t

J=[-l*(sin(q1)+sin(q1+q2)+sin(q1+q2+q3)) -l*(sin(q1+q2)+sin(q1+q2+q3)) -l*(sin(q1+q2+q3));...
-l*(cos(q1)+cos(q1+q2)+cos(q1+q2+q3)) -l*(cos(q1+q2)+cos(q1+q2+q3)) -l*(cos(q1+q2+q3))];
J1=diff(J,q1)*q1dot
J2=diff(J,q2)*q2dot
J3=diff(J,q3)*q3dot
Jtot=J1+J2+J3;
Jtot=double(subs(Jtot,[q1,q2,q3, q1dot,q2dot,q3dot l],[0 0 pi/2 0.8 0 -0.8 0.5])*[0.8; 0 ;-0.8])
```





---
# References
