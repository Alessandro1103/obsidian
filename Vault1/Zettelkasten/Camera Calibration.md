Date: 2024-05-10
Time: 15:20
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Camera Calibration

Cameras are dimensionality reduction machines, as they take the 3D world and turn it into 2D.  

![[Pasted image 20240510152137.png|400]]

## Design a Camera

1. The first basic idea was to put a sensor in front an object. The problem is that every light rays from every point in the 3D object hit every point on the sensor. This produces a blurry image.
2. The second idea was to put a barrier to filter the rays, and acquire only one direction.
   ![[Pasted image 20240510152559.png|400]]
   where $f$ is the focal length, $c$ the optical center of the camera.

In perspective projection, 3D points in camera coordinates are mapped to the image plane:

![[Pasted image 20240510152832.png|300]]


A lens can focus light rays coming from different directions to converge at a point, forming a clear and bright image. A lens focuses light such that objects at a certain distance are sharply defined at the sensor plane, with objects closer or farther from this focal plane appearing blurred.

![[Pasted image 20240510153408.png|300]]


## Technical formulation

### Standard

![[Pasted image 20240510153618.png]]

![[Pasted image 20240510153657.png]]

![[Pasted image 20240510153707.png]]

![[Pasted image 20240510153717.png]]

![[Pasted image 20240510153739.png]]

![[Pasted image 20240510153757.png]]

![[Pasted image 20240510153817.png]]

### Gaussian Lens (Thin Lens) Law

![[Pasted image 20240510153932.png]]

![[Pasted image 20240510153941.png]]

![[Pasted image 20240510153949.png]]

![[Pasted image 20240510153955.png]]

![[Pasted image 20240510154006.png]]

![[Pasted image 20240510154021.png]]

![[Pasted image 20240510154030.png]]

![[Pasted image 20240510154102.png]]

![[Pasted image 20240510154112.png]]

![[Pasted image 20240510154122.png]]



## Camera Calibration Procedure

1. Capture an image of an object of known geometry.
2. Identify correspondences between 3D scene points and image points.
   ![[Pasted image 20240510154623.png|300]]
   $$
   \begin{align*}
   & x_{w} = \begin{bmatrix} x_w \\ y_w \\ z_w \end{bmatrix} = \begin{bmatrix} 0 \\ 3 \\ 4 \end{bmatrix} \text{ (inches)}
   & \mathbf{u} = \begin{bmatrix} u \\ v \end{bmatrix} = \begin{bmatrix} 56 \\ 115 \end{bmatrix} \text{ (pixels)}
   \end{align*}
   $$

3. For each corresponding point $i$ in scene and image.

![[Pasted image 20240510160526.png]]

![[Pasted image 20240510160532.png]]
4. Rearranging the terms:
   ![[Pasted image 20240510160442.png|400]]
5. Solve for $p$:
   $A\ p = 0$

Since we are working with homogenous coordinates, scaling the coordinates doesn't make sense (we are normalizing dividing in $u$ and $v$ the last row). Since we have more columns than rows we have multiple solutions. We can choose to minimize the norm such that: $||p||^2 = 1$ or set the scale so that $p_{34}=1$. These scaling are used for standardizing the scale of transformation, for stability and scaling reasons. So we define a **Loss function**:
$$
L(p,\lambda) = p^T A^T A p - \lambda(p^T p -1)
$$

Taking the derivative and then consider the eigenvector *p* with smallest eigen value $\lambda$ of matrix $A^TA$ minimizes the loss function.

![[Pasted image 20240510163742.png|400]]

![[Pasted image 20240510163749.png|400]]

### Lens Distortion

The assumption of linear projection is violated in practice due to the properties of the camera lens which introduces distortions. Both **radial and tangential distortion** effects can be modelled easily. Let $x=x_c/z_c, \ y= y_c/z_c$ and $r^2=x^2+y^2$. The distorted point is obtained as:

$$
\begin{align*}
& x' = \left(1 + k_1 r^2 + k_2 r^4\right) \begin{pmatrix} x \\ y \end{pmatrix} + \begin{pmatrix} 2k_3 xy + k_4(r^2 + 2x^2) \\ 2k_4 xy + k_3(r^2 + 2y^2) \end{pmatrix}

&  x_s = \begin{pmatrix} f_x x' + c_x \\ f_y y' + c_y \end{pmatrix}
\end{align*} 
$$

where  $r^2 = x^2 + y^2$  (radial distortion). The first part (the one multiplies x and y) is the **radial distortion**, the second one is the **tangential distortion**. Images 
