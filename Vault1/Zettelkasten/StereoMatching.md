Date: 2024-05-15
Time: 12:16
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Stereo Matching

## Motivation and history

**Parallax** is a phenomenon where the position or direction of an object appears to differ when viewed from different positions. In simpler terms, it's the apparent shift of an object against a background due to a change in observer position.

Humans perceive depth because of parallax. When you move, objects that are closer to you move faster across your field of view compared to objects that are far away. This is another way we gauge depth and distance while moving, such as when driving or walking.

## Basic two view stereo setup

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 21 
scale: 0.8 
```

Stereo matching is the process used to find correspondences between two stereo images. It involves algorithms that identify similar or identical regions in different images to establish how far objects are from the viewer or camera. The depth information, obtained from the disparities in these correspondences, helps in constructing the 3D structure of the scene.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 22 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 23 
scale: 0.8 
```

We need to resort on a system like this, where we have the image plane, find the epipolar line that are parallel. We have to calculate the displacement of one image to the other, since if we have a situation like this, there is no rotation of the two camera. 

![[Pasted image 20240609125943.png|300]]

The two coloured images on the left are stereo images. They are two snapshots of the same scene taken from slightly different viewpoints. The differences between these two images are key to deriving depth information.

When you compare two stereo images, objects that are closer to the camera will appear to move more between the two images compared to objects that are farther away. This apparent motion is called disparity.

**Depth from disparity**:
![[Pasted image 20240609135712.png|200]]

$\frac{x}{f} = \frac{B_1}{z}$ and $\frac{-x'}{f} = \frac{B_2}{z}$, resulting in: 
$$
x-x' = \frac{fB}{z}
$$
Disparity is inversely proportional to depth.

![[Pasted image 20240609140253.png|200]]

$\frac{x}{f} = \frac{B_1}{z}$ and $\frac{x'}{f} = \frac{B_2}{z}$, resulting in: 
$$
z = \frac{fB}{x-x'}
$$
Same here.

The conditions to compute the depth are:
1. A baseline (distance from cameras) enough large
2. Modify the image so that the epipolar lines are horizontal and aligned across both images.

The difference between the two camera needs to be large enough. And the image needs to be warped.

To make the epipolar lines horizontal:
1. Calibrate the cameras
2. Estimate the Fundamental/Essential matrix
3. Rectification Transform (find the rotation matrices for each camera that will align the epipolar lines with the horizontal axis of the image)

The relationship between the two cameras needs to be:
$$
\begin{align*}
&R = I &
t = (T,0,0)
\end{align*}
$$
meaning that the rotation between the two cameras is the identity, and the translation is only in the x-axis.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 31 
scale: 0.8 
```

This involves calculating the homographic transforms that will reproject the images onto a common, coplanar surface aligned with the baseline.
We need to rectify both images, like warping.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 33 
scale: 0.8 
```

Rotation matrices ($R_1$, $R_2$) are used to transform the images such that their epipolar lines become parallel. The principal axis is the main axis of each camera lens, usually perpendicular to the imaging plane. The Rectified Camera 1 is Camera 1 after its image has been transformed to align the epipolar lines

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 34 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 35 
scale: 0.8 
```

The epipolar lines are now parallel. Now it is easier to calculate the depth:
 
```slide-note 
file: StereoMatching_CV2324.pdf 
page: 36 
scale: 0.8 
```

>[!Algorithm]
>1. Rectify images
>2. For each pixel:
>	1. Find epipolar line
>	2. Scan line for best match (SSD, Cross-Correlation, SAD...)
>	3. Compute depth from disparity: $z = \frac{fB}{x-x'}$

## Local Stereo Matching Algorithm

Local stereo matching algorithms involve comparing a small window of pixels around a pixel in one image to corresponding windows along the same epipolar line in the other image to find the best match.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 39 
scale: 0.8 
```

The measures are:
- SAD: $\sum\ |I_1(x,y) - I_2(x+i, y+j)|$
- SSD: $\sum\ [I_1(x,y) - I_2(x+i, y+j)]^2$
- Zero-mean SAD: $\sum |(I_1(x,y) - \mu_1) - (I_2(x+i, y+j) - \mu_2)|$
- Normalized Cross Correlation (NCC)


```slide-note 
file: StereoMatching_CV2324.pdf 
page: 44 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 47 
scale: 0.8 
```

We have to consider the problem of occlusion, when the image in the right shows a part that in the left is not shown (and viceversa). This situation brings to inconsistencies in the algorithms that needs to elaborate them.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 51 
scale: 0.8 
```

A DSI is a matrix where each element represents the match score of a patch in one image with a patch at a corresponding position in the other image, adjusted for disparity.


```slide-note 
file: StereoMatching_CV2324.pdf 
page: 52 
scale: 0.8 
```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 53 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 54 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 55 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 56 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 57 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 58 
 scale: 0.8 
 ```
## Challenges in Stereo Matching

What are the challenges in the matching problem?

### Uniqueness

The uniqueness constraint states that each point in one image should correspond to at most one point in the other image. This principle is crucial for ensuring that the matching process is deterministic and reduces ambiguity. 
Uniqueness often does not hold in real-life scenarios due to: Repetitive Patterns, Symmetrical Objects, Scene Complexity.

### Smoothness

The smoothness constraint in computer vision implies that the disparity between corresponding points in stereo images generally changes gradually across most of the image. 

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 63 
scale: 0.8 
```

At the left we have a depth map of the left image, where colors indicate depth level: warmer colors (like red) denote closer objects, and cooler colors (like green) signify farther ones.

### Occlusions

Occlusions occur when certain parts of the scene are visible in one image but are blocked in the other. This happens because of the different perspectives or angles from which each image is taken.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 64 
scale: 0.8 
```

The **Left-Right Consistency Test** is a validation technique in stereo vision used to ensure that the disparity maps generated from matching the left image to the right image are consistent when the process is reversed (i.e., matching the right image to the left image). This helps in detecting and correcting errors such as outliers and occlusions.

## Stereo Matching with Dynamic Programming


```slide-note 
file: StereoMatching_CV2324.pdf 
page: 69 
scale: 0.8 
```

This path is the result of an algorithm that selects the best disparity for each pixel along the scanline based on criteria such as minimizing disparity gradients (to ensure smooth transitions) and maximizing match quality (based on image similarity).

![[Pasted image 20240613165549.png]]

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 72 
scale: 0.8 
```

We want to minimize a cost function:

$$
\begin{align*}
C(i,j)=\min([ & C(i−1,j−1)+\text{dissimilarity}(i,j),\\
&C(i−1,j)+\text{occlusionCostant},\\&C(i,j−1)+\text{occlusionCostant}])
\end{align*}
$$

In order to remove the occluded points we can use the **Occlusion Filling**. The occluded pixel are coloured by black, then we use the nearest valid pixel and fill the occlusion with that. It has to be done first in one direction and then in the opposite.

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 77 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 79 
scale: 0.8 
```

## Stereo Matching with Graph Cut algorithm

The main cause of discontinuities in depth maps is the noise, even if happens we don't care, so we can assume that: *depth should change smoothly*. So we need to find a function to prove this, guarantee *Match quality* and *Smoothness*.

$$
E(d) = E_d(d) + \lambda E_s(d)
$$

where $E$ is the total energy to minimize, $E_d$ is the data term that measure the dissimilarity between pixels (lower values = better match), $E_s$is the smoothness term that encourages smooth changes in disparity between adjacent pixels. $\lambda$ is a parametrization term.

$$
E_d(d) = \sum_{(x,y)\in I}C(x,y,d(x,y))
$$
 $C$ is a general cost function, we can consider a SSD (sum of squares formula) function.

$$
E_s(d) = \sum_{(p,q)\in \epsilon}V(d_p, d_q)
$$
$V$ is a function that measures disparities, in particular we can measure disparity respect the point that that point is connected to, if we consider 4-connection or 8 changes a lot.![[Pasted image 20240613180407.png|100]]
$V$ can be:
$$
\begin{align*}
&V(d_p, d_q) = |d_p-d_q| \\\\
&V(d_p, d_q) = 
\begin{cases} 
0 & \text{if } d_p = d_q \\
1 & \text{if } d_p \neq d_q
\end{cases}
\end{align*}
$$
The first treats all disparities linearly, the second one provides penalties if $d_p$ and $d_s$ are different. This separation is more sharp.

Otherwise we have to consider the **Dynamic Programming**: 
$$
D(x,y,d)=C(x,y,d)+\min​_{d'}\{D(x-1,y,d')+\lambda|d-d'|\}
$$

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 90 
scale: 0.8 
```

## Stereo in Deep Learning era


```slide-note 
file: StereoMatching_CV2324.pdf 
page: 96 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 97 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 98 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 99 
scale: 0.8 
```

```slide-note 
file: StereoMatching_CV2324.pdf 
page: 100 
scale: 0.8 
```

## Active stereo with structured light


 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 102 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 103 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 104 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 105 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 106 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 107 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 108 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 109 
 scale: 0.8 
 ```

