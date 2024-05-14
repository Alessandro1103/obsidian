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


