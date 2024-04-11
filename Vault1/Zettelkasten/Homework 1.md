# Homework 1 - Alessandro De Luca

## Problem 1

To determine the number of degrees of freedom necessary to satisfy the constraints and achieve the desired mobility, I need to apply Grubler's formula for planar mechanisms:
$$
m = \sum_{i=1}^{n} d_i - 3(n + 1 - l)
$$
where $m$ denotes the mobility, $d_i$ are the degrees of freedom at each joint, $n$ is the number of joints, and $l$ is the number of links, including the fixed link or frame.
Considering that each joint in our mechanism, whether active or passive, contributes a single degree of freedom, and there are no additional constraints affecting the mobility:
The summation of the degrees of freedom provided by each joint is:
$$
\begin{align*}
& \sum_{i=1}^{n} d_i = 4 \times 1 = 4 & m = 4 - 3(4 + 1 - 4) = 4 - 3 = 1
\end{align*}
$$

Thus, according to Grubler's formula, the given planar mechanism has a single degree of freedom.

Considering the robot's design and the assumption that its links can pass through each other without collision, each joint, including the camera, follows a circular trajectory. This design grants the robot a single degree of freedom (DOF), which adequately supports pointing tasks within a two-dimensional space.
Given my focus on a singular variable, $q_1$, it becomes necessary to parameterize the angles associated with the passive joints. To achieve this, I set:  
$$
\begin{pmatrix}
q1 \\
q2 \\
q3
\end{pmatrix} = \begin{pmatrix}
\theta \\
- \theta \\
\theta - \pi
\end{pmatrix} 
$$
There's no need to take into account the angle $q_4$, measured from the x-axis to the final segment of the fourth link, nor the length extending from the fourth joint to the end effector. This is because the angle formed with the x-axis by the terminal portion of the fourth link mirrors the third angle, $q_3$. Consequently, including a variable $q_4$ would be redundant, as it would merely duplicate the value of $q_3$. 
![[5a03e3ba-aed8-4548-ba2a-d56bc31c9979-removebg-preview 1.png|400]]
In order to obtain the differential kinematics, I have to calculate the direct kinematics.
$$
p = 
\begin{bmatrix}
    p_x \\
    p_y
\end{bmatrix} = \begin{bmatrix}
    l(c_1 + c_{12} + c_{123}) \\
    l(s_1 + s_{12} + s_{123})
\end{bmatrix}
$$
The omission of the $d$ component in the representation of the direct kinematics is deliberate, due to the specific focus of my problem on pointing accuracy, which prioritizes angular orientation over linear distance. Moreover the next steps requires to focus on the joint 4, not on the end-effector.
The next step is to calculate the Jacobian:
$$
J(q_1, q_2, q_3) = \begin{pmatrix}
    \frac{\partial f}{\partial q_1} \frac{\partial f}{\partial q_2} \frac{\partial f}{\partial q_3}
\end{pmatrix} = \begin{bmatrix}
    -l(s_{123} + s_{12} + s_1) & -l(s_{123} + s_{12}) & -ls_{123} \\
l(c_{123} + c_{12} + c_1) & l(c_{123} + c_{12}) & lc_{123}
\end{bmatrix}
$$
from this formula we can exhibit the differential kinematics. The objective is calculate the joint velocity and since the joint 4 is stuck the velocity is null. 
$$
J\dot{q} = 0
$$
To find the configuration of the end effector, the first step is to open the closed chain, presenting two configurations:
![[e6b25912-93f8-4d73-b9b9-174d58dd4c4e-removebg-preview.png|300]]     ![[71ca1fd8-1a38-4838-8171-d67b86e210bf-removebg-preview.png|300]]

The Jacobian matrix can be separated on the elements related to the active joint and the elements related with the unactive joints. 
$$
J\dot{q} = \begin{pmatrix}
    J_{actuated} & J_{unactuated}
\end{pmatrix} \begin{pmatrix}
    \dot{q}_{actuated} \\
    \dot{q}_{unactuated}
\end{pmatrix} = 0
$$
knowing that the joint actuated is $q_1$, the unactuated are the remaining ones, the equation before can also be written as:
$$
J_{act} \ \dot{q_1} = J_{unact}
\begin{pmatrix}
    \dot{q}_2 \\
    \dot{q}_3
\end{pmatrix}   
$$
And since the only value that I actually control is $q_1$, I can write the remaining variables as dependent on the one said before:

$$
\begin{bmatrix}
    \dot{q}_2\\
    \dot{q}_3
\end{bmatrix} = -\begin{bmatrix}
    J_{unact}
\end{bmatrix}^{-1} \ J_{act} \ \dot{q}_1
$$
The inversion of the Jacobian will only be feasible in non singular configurations, whenever $det|J_{unact}|\neq0$, the calculation bring to:
$$
l^2 \cdot sin(q_3) = 0 \Leftrightarrow q_3 = k \pi \ k \in \mathbb{Z}
$$
We are in a singular configuration whenever the joint axes collapse into the x-axis of the absolute reference frame. Concluding I present the final equation:
$$
\begin{bmatrix}
    \dot{q}_2\\
    \dot{q}_3
\end{bmatrix} = \begin{bmatrix}
    -\frac{s_{23} + s{3}}{s_3} \\
    \frac{s_{23} + s{2}}{s_3}
\end{bmatrix} \dot{q}_1
$$
and substituting $\begin{cases} q_2=-q_1 \\ q_3 = q_1 - \pi \end{cases}$ we get:
$$
\begin{bmatrix} 
\dot{q}_2 \\ 
\dot{q}_3 
\end{bmatrix} = \begin{bmatrix} 
-\dot{q}_1 \\ 
\dot{q}_1 
\end{bmatrix}
$$

Between the three singularities I can say that, we find the only one

## Problem 2

To determine the number of degrees of freedom necessary to satisfy the constraints and obtain the desired degrees of mobility, we apply Grubler's formula for planar mechanisms:

$$
m = \sum_{i=1}^{n} d_i - 3(n + 1 - l)
$$

where $m$ represents the mobility, $d_i$ are the degrees of freedom at each joint, $n$ is the number of joints, and $l$ is the number of links. \newline

Given that each revolute joint contributes 1 degree of freedom, and assuming the remote center of motion (RCM) constraint prohibits translational movement, the virtual joint would thus contribute 2 degrees of freedom—accounting for vertical movement and rotation. Therefore, the total summation of $d_i$ is 6. The constant 3 in the formula accounts for the planar nature of the robot. Here, $n$, which is the number of joints, is 4 (including the virtual RCM joint), and $l$, the number of links, is also 4. Substituting these values into Grubler's formula, we obtain:

$$
m = 1 + 1 + 1 + 2 - 3 \cdot (4 + 1 - 4) = 2
$$

Thus, the robot has 2 degrees of freedom. \newline
To obtain the RCM Jacobian, we need to calculate the elements using the following formula:
$$
J_{RCM} = 
\begin{bmatrix}
    J_i + \lambda (J_{i+1} - J_i) & | & p_{i+1} - p_i
\end{bmatrix}
$$
And considering the 3R robot, as before a 2R robot, and then 
$$
\begin{align*}
&p_3 = \begin{bmatrix} 
p_{x3} \\
p_{y3}
\end{bmatrix} = \begin{bmatrix}
l_1 c_{1} + l_2 c_{12} \\
l_1 s_{1} + l_2 s_{12}
\end{bmatrix} &
J_3 = \begin{bmatrix}
-l_1 s_{1} - l_2 s_{12} & -l_2 s_{12} \\
l_1 c_{1} + l_2 c_{12} & l_2 c_{12}
\end{bmatrix} \\
& p_4 = \begin{bmatrix}
p_{x4} \\
p_{y4}
\end{bmatrix} = \begin{bmatrix}
l_1 c_{1} + l_2 c_{12} + l_3 c_{123} \\
l_1 s_{1} + l_2 s_{12} + l_3 s_{123}
\end{bmatrix} 
& J_4 = \begin{bmatrix}
-l_1 s_{1} - l_2 s_{12} - l_3 s_{123} & -l_2 s_{12} - l_3 s_{123} & -l_3 s_{123} \\
l_1 c_{1} + l_2 c_{12} + l_3 c_{123} & l_2 c_{12} + l_3 c_{123} & l_3 c_{123} \\
\end{bmatrix}
\end{align*}
$$

Since $J_4$ and $J_3$ have different dimensions due to the additional degree of freedom represented in $J_4$, and our interest lies in a subspace of motion that the third joint does not influence, we adapt $J_3$ to match the dimensions of $J_4$ by appending a column of zeros. This modification reflects the scenario where the third joint's motion has no impact on the end-effector's position or orientation with respect to the task at hand. Such a condition might arise, for instance, if the third joint is temporarily fixed or if the system operates under a constraint that nullifies the effect of the third joint's motion (as in some Remote Center of Motion applications). \newline
Performing all the operation the matrix obtained is the following:


$$
J_{rcm} =  
\begin{bmatrix}
- l_2 s_{12} - l_1 s_1 - l_3 \lambda s_{123}, & - l_2 s_{12} - l_3 \lambda s_{123}, & -l_3 \lambda s_{123}, & | & l_3 c_{123} \\  
l_2 c_{12} + l_1 c_1 + l_3 \lambda c_{123}, & l_2 c_{12} + l_3 \lambda c_{123}, & l_3 \lambda c_{123}, & | & l_3 s_{123}
\end{bmatrix} 
$$

