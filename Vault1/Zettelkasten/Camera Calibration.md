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
4. Rearranging the terms:
5. Solve for $p$: