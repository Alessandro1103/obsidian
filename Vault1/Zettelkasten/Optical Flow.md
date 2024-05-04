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
  
- Barber Pole: ![[Screenshot from 2024-05-04 12-38-34.png|70]]The apparent motion is pointing upwards, the actual motion is in the right direction.


---
# References
