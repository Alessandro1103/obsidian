Date: 2024-05-14
Time: 11:08
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Epipolar Geometry and Fundamental Matrix

## Introduction

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 2
scale: 0.8
```

We have a point in a image and we wand to know where is the point in the others images.

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 3
scale: 0.8
```

We have no information in camera parameters, and we want to calculate it

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 4
scale: 0.8
```

We have different projection of the 3D object, and i want to compute the 3D coordinates of that point, and extract the camera parameters.

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 5
scale: 0.8
```

The relationship between 3D points and their 2D image projection is represented by equation: $x = f(X; p) = PX$ where P is the camera matrix which transform 3D coordinates in 2D. The camera matrix P can be decomposed into intrinsic parameters K and extrinsic \[R|t\] (R rotational, t translation). To find the camera center C we have $Pc=0$. 

Now that our cameras are calibrated, can we find the 3D scene point of a pixel?

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 7
scale: 0.8
```

We can not due to the loss of depth information. But we can if we have additional information like multiple camera perspectives, to pinpoint the exact location along the ray where he lies down.

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 9
scale: 0.8
```

**Uncalibrated stereo**: We need the information of the two cameras, suppose the intrinsic parameters (optical centre...) are known for both, assuming we have already calibrated everything. 

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 10
scale: 0.8
```

## Epipolar Geometry

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 14,15,16,17
scale: 0.8
```

We need to estimate $p$.
We have two planes, two optical center (camera location) called $o$ and $o'$, the line between the optical center, is called *Baseline*. The point Epipole, is in the image plane, these creates the epipolar plane, generating an epipolar line, which is the intersection of the epipolar plane with the image plane, passing through epipole. The two epipolar line are not the same. 

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 19
scale: 0.8
```
We can establish epipolar constraints. The only thing I can do is to project x onto a ray in 3D. I can find x on the corresponding epipolar line in the other image. My goal is to match x in this second image. While I cannot determine the exact location of the point, I can estimate it.

**Converging cameras**

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 20
scale: 0.8
```

Converging cameras result in finite epipoles within the images, epipolar lines that converge at the epipoles, and a well-defined epipolar geometry that aids in finding correspondences for 3D reconstruction.

**Parallels Cameras**

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 25
scale: 0.8
```

Parallel cameras lead to epipoles at infinity and parallel epipolar lines, which greatly simplifies the epipolar geometry and the process of finding corresponding points for 3D reconstruction.

**Forward Motion**

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 29
scale: 0.8
```

For forward motion, the epipole is located at the focus of expansion (the principal point), and the epipolar lines radiate outward from this point.

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 30
scale: 0.8
```

1. point $x'$
2. camera centers $o$ and $o'$
3. corresponding epipolar line
4. camera center 
5. epipole

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 33
scale: 0.8
```

To match a point in one image and find it in another, we use the epipolar constraint, which reduces the search to a single line. How do we compute the epipolar line?
## Essential Matrix

Given a point in one image, multiplying it by the essential matrix will determine the corresponding epipolar line in the second view. So we have a relation between $l'$ and $x$. We write this "relation" as $Ex = l'$.
Writing the Epipolar line as: $ax + by+x =0$ or in vector form: $l = \begin{bmatrix} a \\ b \\ c \end{bmatrix}$. If a point $x$ is on the epipolar line $l$, then the dot product $x^Tl = 0$.

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 39
scale: 0.8
```

We don't know how to obtain $E$.

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 44,45,46
scale: 0.8
```

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

The essential matrix $E$ operates on camera-coordinate system points, requiring camera calibration data, and enforces the epipolar constraint $x'^{T}E\hat x=0$. The fundamental matrix $F$, expressed as $F=K^{−T}EK^{−1}$, generalizes $E$ by accommodating image-coordinate points, making it applicable without explicit camera calibration. $F$ allows working directly with raw image data, linking image points across views under the epipolar constraint $x'^{T}Fx=0$. This flexibility makes $F$ especially useful in scenarios where calibration data is unavailable. 

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

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 63,64,65,66
scale: 0.8
```

We can calculate the epipole with $Fe = 0$ so using a SVD (Singular Value Decomposition).

```slide-note 
file: EpipolarGeometry_FundamentalMatrix_CV2324.pdf 
page: 81
scale: 0.8
```

## 8-point Algorithm

We need to understand how to estimate the F
Find correspondences, we can run a detector and match the key point, and after that, we have the key point matched: x

we could have some problem with the algorithm, could happens that the difference between the column is very huge, that yields to poor results. 

To normalize, instead of using a general dimension, we can transform the image into a scale that ranges from -1 to 1. Now, the $x$ is driven by $T$ transformation. Use the eight-point algorithm to compute $F$. In order to return to the original point, we need to enforce the rank 2 constraint. We want to take the SVD of $F$ and discard the smallest singular value, and then transform the fundamental matrix back to the original units. If $T$ and $T'$ are the normalizing transformations in the two images, then the fundamental matrix in original coordinates is $T'^T F T$. This is done to obtain the coordinates in the original space.

If we know the calibration matrices of the two camers, we can estimate the essential matrix: E = K^T F K
THe essential matrix gives us the relative rotation and translation bwtween the cameras, or thei extrinsinc parameters.
Fundamental matrix lets us compute relationship up to scale for cameras with unknown instrinsic calibraions. Estimating the fundamental matrix is a kind of "weak calibration". 

**Normalized eight point algorithm**:
1. normalize points
2. constrauct the Mx9 matrix A (M= 8 atleats)
3. Find the svd of A
4. entries of F are the elements of column of V corrsponding to the least singular valur
5. enforce rank2 contraint on F
6. unnomalize F

...

the geometry of three views is described by a 3x3x3 tensor called the trifocal tensor
the geometry of four views is described by a 3x3x3x3 tensor called the quarifocal tensor
...

## Triangulation

I need to find  the camera center c apply the pseudo inverse of P on x, then connvet the two points (c and x), and find P+x -> Back projection

How do we find the exact point on the ray? is not possible

WE go to the correspondence, I can P' from the with fundamental matrix. 

Since x and px lies in the same line the cross product is the same. 


