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
page: 13
scale: 0.8
```

```slide-note
url: https://drive.google.com/file/d/1EXA4ZQxLT0WYcJwIrj6-cwD-_Rk8tWG3/view?authuser=2&usp=classroom_web 
page: 16, 17, 18
scale: 0.2
```

We have two planes, two optical center (camera location), we need to estimate p. 
The line between the optical center, is called Baseline. The point Epipole, is in the image plane, these creates the epipolar plane, generating an epipolar line, which is the intersection of the epipolar plane with the image plane, passing throught epipole. The two epipolar line are not the same. 

We can build Epipolar contraints, the only thing i can do is to backpokect x to a ray in 3d. I can find x in the other epipolar line, so I want to find x in the other image. I want to find the mathc in the other image. I can not find the exact location of the point, i can estimate it. 

When we have converging camera, to estimate the epipole. The epiole can be outsite the image plane. Epipolar lines converge, for each point in the 3d image, is it possible to build a new epipolar line. 

In parallel cameras the Epipole is at infinity. 

... Forward Motion

1. line
2. optical center
3. line
4. optical center 
5. epipole

match one point in one image and find it in the other image. Epipolar constraint rexuces search to a single line. How do we compute the pipolar line?

## Essential Matrix

Given a point in one image mulipluing by the essential matrix will tell us the epipolar line in the second view. 

... epipolar line formulas

x is expressed in camera coordinate system, we still have no information of the 3d world, we have the pixel value. 

... properties of E matrix

E si rank is important for estimate the parameter

...

What the difference between the essential matrix and homography?
matrix maps a point to a line, homography point to a point

## Fundamental Matrix

In order to be able to use essential matrix, we need to make an assumption: the intrinsic matrices are identities. The coordinate system of the camera are equal. 

We need to introduce the fundamental matrix that is a generalization of the essential matrix where the  assumption is removed. 
...

## 8-point Algorithm

We need to understand how to estimate the F
Find correspondences, we can run a detector and match the key point, and after that, we have the key point matched: x

...

we could have some problem with the algorithm, could happens that the difference between the column is very huge, that yields to poor results. 

So ve need to normalize, instead of using a general dimension we can transform the image in a scale that is between -1 to 1. Now the x is driven by T transformation. 
Use the eight point algorithm to compute F
In order to comeback to the original point we need to enforce the rank 2 constraint, we wanto to take svd of f andthrow out the smallest singular valura, and we need to transform formdamental matrix nack to riginal units, if T and Tì are the normalizing tranfomations in the two images than the fundamental matrix in orginal coordinates is T'^T F T. This is done to obtaine the coordinate in the originalk space. 

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


