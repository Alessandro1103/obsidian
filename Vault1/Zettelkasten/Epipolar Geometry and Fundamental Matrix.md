Date: 2024-05-14
Time: 11:08
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Epipolar Geometry and Fundamental Matrix

## Introduction

Let's analyse the key topics in Multi-view geometry problems:
1. **Stereo correspondence**: the goal is to determine corresponding points across multiple images taken from different viewpoints.
2. **Camera motion**: the goal is to determine the camera parameters for each viewpoint.
3. **Structure from Motion**: estimate the 3D coordinates of a point in the object

In the previous lecture [[Camera Calibration]] we calibrated the camera, can we find the 3D scene point of a pixel now? NO, because when we look at a camera screen we don't know the depth $z$. Without $z$, you can determine the direction in which the object lies from the camera, but not how far it is along that direction.

But we can if we have additional information like multiple camera perspectives, to pinpoint the exact location along the ray where he lies down.

### Uncalibrated stereo
We need the information of the two cameras, suppose the intrinsic parameters (optical centre...) are not known for both, assuming we have already calibrated everything. 

![[Pasted image 20240621230741.png|400]]

## Epipolar Geometry

![[Pasted image 20240621230754.png|400]]

We need to estimate $p$.
We have two planes, two optical center (camera location) called $o$ and $o'$, the line between the optical center, is called *Baseline*. The point Epipole, is in the image plane, these creates the epipolar plane, generating an epipolar line, which is the intersection of the epipolar plane with the image plane, passing through epipole. *The two epipolar line are not the same*. 

![[Pasted image 20240621230808.png|400]]

We can establish epipolar constraints. The only thing I can do is to project x onto a ray in 3D. I can find x on the corresponding epipolar line in the other image. My goal is to match x in this second image. While I cannot determine the exact location of the point, I can estimate it.

### Converging cameras

![[Pasted image 20240621230824.png|400]]

Converging cameras result in finite epipoles within the images, epipolar lines that converge at the epipoles, and a well-defined epipolar geometry that aids in finding correspondences for 3D reconstruction.

### Parallels Cameras

![[Pasted image 20240621230849.png|400]]

Parallel cameras lead to epipoles at infinity and parallel epipolar lines, which greatly simplifies the epipolar geometry and the process of finding corresponding points for 3D reconstruction.

### Forward Motion

![[Pasted image 20240621230904.png|200]]

For forward motion, the epipole is located at the focus of expansion (the principal point), and the epipolar lines radiate outward from this point.

![[Pasted image 20240621230929.png|400]]
1. point $x'$
2. camera centers $o$ and $o'$
3. corresponding epipolar line
4. camera center 
5. epipole

![[Pasted image 20240621230949.png|400]]

To match a point in one image and find it in another, we use the epipolar constraint, which reduces the search to a single line. How do we compute the epipolar line?
## Essential Matrix

Given a point in one image, multiplying it by the essential matrix will determine the corresponding epipolar line in the second view. So we have a relation between $l'$ and $x$. 
We write this "relation" as $Ex = l'$.

In projective geometry, $\mathbf{x}^T \mathbf{l} = 0$ indicates that the point $\mathbf{x}$ lies on the line $\mathbf{l}$, with $\mathbf{x}^T \mathbf{l} = ax + by + c$ being the equation of the line evaluated at the point $\mathbf{x}$. This dot product equals zero when the point satisfies the line equation.


![[Pasted image 20240621231008.png|400]]

We don't know how to obtain $E$.

![[Pasted image 20240621231024.png|400]]

![[Pasted image 20240621231040.png|400]]

![[Pasted image 20240621231056.png|400]]

So $E$ is equal to: $E = \mathbf{R} [\mathbf{t}]_\times$​

**Properties of the E matrix**:
$$
\begin{align*}
&\text{Longuet-Higgins equation} & \mathbf{x}'^T E \mathbf{x} = 0 \\ \\
& \text{Epipolar lines} & \mathbf{x}^T \mathbf{l} = 0 && \mathbf{x}'^T \mathbf{l}' = 0 \\
&& \mathbf{l}' = E \mathbf{x} && \mathbf{l} = E^T \mathbf{x}' \\ \\
&\text{Epipoles} & \mathbf{e}'^T E = 0 &
& E \mathbf{e} = 0
\end{align*}
$$

What is the difference between the essential matrix and homography?
the matrix maps a point on a line, homography a point on a point

## Fundamental Matrix

In order to be able to use essential matrix, we need to make an assumption: the intrinsic matrices are identities. The coordinate system of the camera are equal. 

We need to introduce the fundamental matrix that is a generalization of the essential matrix where the assumption is removed. 

The essential matrix $E$ operates on camera-coordinate system points, requiring camera calibration data, and enforces the epipolar constraint $x'^{T}E\hat x=0$. The fundamental matrix $F$, expressed as $F=K^{−T}EK^{−1}$ (where $K$ is the calibration matrix, the intrinsically parameters of the camera 3x3), generalizes $E$ by accommodating image-coordinate points, making it applicable without explicit camera calibration. $F$ allows working directly with raw image data, linking image points across views under the epipolar constraint $x'^{T}Fx=0$. This flexibility makes $F$ especially useful in scenarios where calibration data is unavailable. 

**Properties of the F matrix**:
$$
\begin{align*}
&\text{Longuet-Higgins equation} & \mathbf{x}'^T F \mathbf{x} = 0 \\ \\
& \text{Epipolar lines} & \mathbf{x}^T \mathbf{l} = 0 && \mathbf{x}'^T \mathbf{l}' = 0 \\
&& \mathbf{l}' = F \mathbf{x} && \mathbf{l} = F^T \mathbf{x}' \\ \\
&\text{Epipoles} & \mathbf{e}'^T F = 0 &
& F \mathbf{e} = 0
\end{align*}
$$

![[Pasted image 20240621231124.png|400]]

![[Pasted image 20240621231138.png|400]]

![[Pasted image 20240621231146.png|400]]

![[Pasted image 20240621231206.png|400]]

We can calculate the epipole with $Fe = 0$ so using a SVD (Singular Value Decomposition).

![[Pasted image 20240621231226.png|500]]

## 8-point Algorithm

The 8-point algorithm is a fundamental method in computer vision for estimating the fundamental matrix (or the essential matrix) between two views of a scene.

![[Pasted image 20240621231244.png|300]]

Find correspondences, we can run a detector and match the key point, and after that, we have the key point matched: x

![[Pasted image 20240621231256.png|400]]

![[Pasted image 20240621231314.png|500]]

You need at least 8 points for the 8-point algorithm in computer vision because each pair of corresponding points provides one linear equation, and the fundamental matrix $F$ has 9 unknowns (its 9 elements). While using 9 points can theoretically give a unique solution to the homogeneous linear system for the fundamental matrix $F$, practical implementations typically use more points to ensure robustness against noise and to improve the accuracy of the solution. In all cases, the solution must also satisfy the rank-2 constraint, often enforced through SVD after the initial estimation.

![[Pasted image 20240621231337.png|400]]
We could have some problem with the algorithm, could happens that the difference between the column is very huge, that yields to poor results. 
To normalize, instead of using a general dimension, we can transform the image into a scale that ranges from -1 to 1. 

![[Pasted image 20240621231402.png|400]]
Now, the $x$ is driven by $T$ transformation. 

![[Pasted image 20240621231417.png|400]]
If we know the calibration matrices of the two cameras, we can estimate the essential matrix: $E = K'^T F K$. The essential matrix gives us the relative rotation and translation between the cameras, or their extrinsic parameters. The fundamental matrix lets us compute relationships up to scale for cameras with unknown intrinsic calibrations. Estimating the fundamental matrix is a kind of "weak calibration".


![[Pasted image 20240621231437.png|300]]

**Normalized eight-point algorithm**:
1. Normalize points
2. Construct the $M \times 9$ matrix $A$ ($M \geq 8$)
3. Find the SVD of $A$
4. Entries of $F$ are the elements of the column of $V$ corresponding to the least singular value
5. Enforce rank-2 constraint on $F$
6. Unnormalize $F$


![[Pasted image 20240621231503.png|380]]
## Triangulation

![[Pasted image 20240621231532.png|400]]

![[Pasted image 20240621231544.png|400]]

![[Pasted image 20240621231555.png|400]]

![[Pasted image 20240621231610.png|400]]


To find the exact point on the ray we need the other line:
![[Pasted image 20240621231813.png|400]]

We have no information of the projection matrix, so:
![[Pasted image 20240621231826.png|250]]

![[Pasted image 20240621231856.png|400]]

![[Pasted image 20240621231911.png|300]]

![[Pasted image 20240621231939.png|400]]

![[Pasted image 20240621232016.png|400]]

![[Pasted image 20240621232035.png|500]]

