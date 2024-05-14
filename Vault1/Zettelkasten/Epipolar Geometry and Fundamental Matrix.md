Date: 2024-05-14
Time: 11:08
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Epipolar Geometry and Fundamental Matrix

We have a point in a image and we wand to know where is the point in the others images.

Camera motion: We have no information in camera meters, and we want to calculate it

Structure from motion: we have differenti projection of the 3d object, and i want to compute the 3d coordinates of that point, and extract the camera parameters.

How to compute the camera calibration by P. Its possible to obtain P by svd, and we can scompose the matrix in k (kernel parameter) and R (rotation coordinates)

Now that our cameras are calibrated, can we find the 3D scene point of a pixel?
We miss the depth: "image"

**Uncalibrated Stereo**: We need the information of the two cameras, we suppose that the intrinsic parameter (optical center...) are known for both, assuming we have already calibrated everything. 
We want to estimate the point P, we assume camera metrix k in known, we want to find a few reliable corresponding points, find relative camera position t and orientation R respact to other, finde dense correspondace respect to the other. After that we need to compute depth using Triangulation.

## Epipolar Geometry

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


