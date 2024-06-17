Date: 2024-05-10
Time: 15:20
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Camera Calibration

Cameras are dimensional reduction machines, as they take the 3D world and turn it into 2D.  

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
### Gaussian Lens (Thin Lens) Law

![[Pasted image 20240510153932.png]]

### Standard

![[Pasted image 20240510153618.png]]

![[Pasted image 20240510153657.png]]

![[Pasted image 20240510153707.png]]

The complete formula is the following: 
$$
\begin{align*}
&u=m_x x_i = m_xf\frac{x_c}{z_c}
&v=m_y y_i = m_yf\frac{y_c}{z_c}
\end{align*}
$$
where $m_x$ and $m_y$ are the pixel densities.

![[Pasted image 20240510153717.png]]

![[Pasted image 20240510153739.png]]

![[Pasted image 20240510153757.png]]

![[Pasted image 20240510153817.png]]


![[Pasted image 20240510153941.png]]

![[Pasted image 20240510153949.png]]

Every point on line L (except origin) represents the homogenous coordinate of **u**(u,v)

![[Pasted image 20240510153955.png]]

![[Pasted image 20240510154006.png]]

This gives us a "linear model" for Perspective Projection

![[Pasted image 20240510154021.png]]

So $M_{int}$ that takes you from a point, homogeneous coordinate representation of a point in a camera coordinate frame 3D, to it's pixel coordinate in the image ($\tilde u$).

**Extrinsic Parameter**:
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

Since we are working with homogenous coordinates, scaling the coordinates doesn't make sense (we are normalizing dividing in $u$ and $v$ the last row). Since we have more columns than rows we have multiple solutions. We can choose to minimize the norm such that: $||p||^2 = 1$ so we can minimize:
$$
\min_p||Ap||^2
$$
which bring to us:
$$
\min_p(p^T A^T Ap)\ \text{such that} \ p^Tp =1
$$
So we define a **Loss function** (find the p that minimize L):
$$
L(p,\lambda) = p^T A^T A p - \lambda(p^T p -1)
$$
Taking derivatives of $L(p,\lambda)$ w.r.t. $p$: 
$$
\begin{align*}
& A^T Ap = \lambda p &\text{Eigenvalue Problem}
\end{align*}
$$

Eigenvector **p** with smallest eigenvalue $\lambda$ of matrix $A^TA$ minimizes the loss function $L(p)$


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

where  $r^2 = x^2 + y^2$  (radial distortion). The first part (the one multiplies x and y) is the **radial distortion**, the second one is the **tangential distortion**. Images needs to be **undistorted**.

The lens distortion can be represented as:
$$
\begin{align*}
&{}^CX_u = {}^CX_d + \delta_x &{}^CY_u = {}^CY_d + \delta_y
\end{align*}
$$
If there is no lens distortion both $\delta=0$.

![[Pasted image 20240510165911.png|400]]

### Stereo and Triangulation

![[Pasted image 20240510170005.png|500]]

![[Pasted image 20240510170018.png|500]]

![[Pasted image 20240510173420.png|500]]

This is a visual representation where the intensity of each pixel indicates the disparity, or the difference in horizontal position, of matching pixels between the left and right images.

![[Pasted image 20240510172033.png|500]]


![[Pasted image 20240510172050.png|500]]

