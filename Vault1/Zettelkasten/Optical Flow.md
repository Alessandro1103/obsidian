Date: 2024-05-04
Time: 12:07
Tags: #ComputerVision #Università #IA
Up: [[Computer Vision]]

---
# Optical Flow

**Definition**:
Optical flow is the apparent motion of objects, surfaces and edges in a visual scene, caused by the relative motion between an observer and a scene.

In fact the Optical Flow needs 2 images at 2 time steps, the classical Stereo model takes the images at the same time. To understand an Optical Flow, we need to project the movement made by a point in a 2D space, called Motion Field. The 3D dimensional space is projected in a 2D space. *The motion can be produced by both camera or object motion*. The actual Optical Flow is different form the Motion Field, since some motion are not understandable in 2D.

The optical flow fields tell us the 3D structure of world, motion of objects and motion of the observer. If we know the motion of the image, i.e. we have 2 images close in time, we can understand what is in between, *Video Interpolation*. If we want to compress a sequence of images, it is possible to use the optical flow field to predict how future frames will appear based on the movements detected.Instead of storing each new frame entirely, only the corrections necessary to adjust the prediction based on the optical flow are stored, *Video Compression*.

**2 Problems**:
- Aperture problem: 
  when we observe and image region through a small viewing window it is challenging to discern the true direction of motion of features. In particular for cases where we perceive the component of motion that is parallel to the edges.
  This issue is mitigated by using patches with different gradients.
  
  *Examples*:
  We have 2 matrices: 
  ![[Screenshot from 2024-05-04 12-56-04.png|300]]
  They represents tow image frames, consecutive in a sequence. The general formula is:
  $I_xu+I_yv+I_t=0$ where due to aperture problem (located in the position 3,3), only the vertical movement ($v$) is recovered, the horizontal movement ($u$) is null. Let's see the gradient:
  $$
  \begin{align*}
  &I_x(3,3) = 0 \\
  &I_y(3,3) = 1 & & \text{Solution:}\ v=1 \\
  &I_t(3,3) = I(3,3) - H(3,3) = -1
  \end{align*} 
  $$
  So we recover $v$ but not $u$.
  
- Barber Pole: ![[Screenshot from 2024-05-04 12-38-34.png|70]]The apparent motion is pointing upwards, the actual motion is in the right direction

## Estimating Optical Flow
The approach we want to explore to estimate the optical Flow is based on 3 assumptions:
- **Brightness constancy**: projection of the same point look the same in every frame
  ![[Screenshot from 2024-05-04 16-06-32.png|300]] 
  $I(x(t), y(t), t) = C$

- **Small motion**: points do not move very far
  ![[Screenshot from 2024-05-04 16-10-17.png|300]] 
  Optical flow (velocities): $u,v$
  Displacement: $\delta x, \delta y = (u\delta t, v\delta t)$
  
  For a small space-time step: $I(x + u\delta t,\ y + v \delta t,\ t + \delta t) = I (x, y, t)$ Based on Taylor expansion. I can write the following:
  $$
  \begin{align*}
  &\frac{\partial I}{\partial x} \delta x + \frac{\partial I}{\partial y} \delta y + \frac{\partial I}{\partial t}\delta t = 0 & \text{divide by } \delta t \text{ take limit } \delta t \rightarrow 0 \\
  & \frac{\partial I}{\partial x} \frac{dx}{dt} + \frac{\partial I}{\partial y} \frac{dy}{dt} + \frac{\partial I}{\partial t} \frac{dt}{dt} = 0
  \end{align*}
  $$
  
  Which means $I_x u + I_y v + I_t = 0$ or $u^T \nabla I  + I_t = 0$, where $I_x$ and $I_y$ are *Image gradients*, $I_t$ is a *Temporal gradient*, the $u$ and $v$ are *flow velocities*. 
  ![[Screenshot from 2024-05-04 16-38-17.png|300]]
  Based on $I_x u + I_y v + I_t = 0$ formula, you can find multiple solution to that equation. In particular these solution lies on a straight line. Since we are following a edge direction, we have to estimate the component of the optical flow:
  - Normal Flow: $u_n = - \frac{I_t}{||\nabla I||}$
  - Parallel Flow: there is no correct formula for local consideration.
  
- **Spatial coherence**: points move like their neighbors

To calculate the Optical Flow 2 algorithms are used:
- **Lucas-Kanade Optical Flow (1981)**: Uses the difference of the pixels' value to estimate the movement. Assumes that the Optical flow is constant for all the areas (inside the window). It's more a local method.
- **Horn-Schunck Optical Flow (1981)**: The pixels are all the same, the motion is small. The motion is uniform between *adjacent* pixels. More a global method. 

## Lucas Kanade solution

Let's impose a linear system: $Au=B$ in matrix is: 
$$
\begin{bmatrix}
I_x(1,1) & I_y(1,1) \\
I_x(k,l) & I_y(k,l) \\
\vdots & \vdots \\
I_x(n,n) & I_y(n,n)
\end{bmatrix} \begin{bmatrix}
u\\ v\end{bmatrix} = \begin{bmatrix}
I_t(1,1)\\ I_t(k,l)\\ \vdots\\ I_t(n,n)
\end{bmatrix}
$$
where $A$ is known and $n^2 \times 2$ , $u$ is unknown and $2 \times 1$, $B$ is known and $n^2 \times 1$. Since we have more solution (rows) than equations (columns) we can find the solution with the minimum norm: **Least Squares Solution**: $A^T A u = A^T B$ which in matrix formulation becomes:
$$
\begin{bmatrix}
\sum_W I_x I_x & \sum_W I_x I_y \\
\sum_W I_x I_y & \sum_W I_y I_y \\
\end{bmatrix} \begin{bmatrix} u \\ v\end{bmatrix} = \begin{bmatrix}
-\sum_W I_x I_t \\
-\sum_W I_y I_t
\end{bmatrix}
$$
since we want to find u:
$$
u = (A^T A)^{-1} A^T B
$$
The conditions for making the flow estimation work are: 
- $A^T A$ are invertible (determinant!=0)
- $A^T A$ eigenvalues should be well conditioned: $\lambda_1$ should not be too large respect to $\lambda_2$ and both shouldn't be too small. The eigenvalues are related to edge direction and magnitude (the eigenvector associated with the larger eigenvalue points in the direction of fastest intensity change, the other eigenvector is orthogonal to it).

![[Screenshot from 2024-05-04 17-34-50.png|300]]

So the perfect conditions to perform the LS solution is gradients different and large magnitudes, so corners and high texture regions.

**Coarse to fine Flow Estimation**: If the two pictures we have are too far in time, we have no more the assumption of small motion; the same pixels are now far from their original position. A way to avoid this is to reduce the quality of the image to "decrease" the gap between the pixels. Since now we are again in the small motion condition we can apply the following algorithm:

![[Screenshot from 2024-05-04 18-56-20.png|400]]


## Horn-Schunck Optical Flow

We have to consider the image I as a function of continuous variable x, y, t. Let's consider $u(x, y)$ and $v(x, y)$ as continuous flow fields. We have to minimize the following *energy functional*:
$$
E(u, v) = \iint \left( I(x + u(x,y), y + v(x,y), t+1) - I(x,y,t) \right)^2 \, \text{dx dy} + \lambda \cdot \iint \left( \|\nabla u(x, y)\|^2 + \|\nabla v(x, y)\|^2 \right) \, \text{dx dy} 
$$

where the first double integral penalizes differences between the brightness of a pixel at time $t$ and the precdicted brightness of the same pixel (after displacement) at time $t+1$. 0

---
# References