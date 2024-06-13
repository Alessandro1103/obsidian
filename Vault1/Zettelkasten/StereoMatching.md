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
## Beyond local stereo matching

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

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 66 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 67 
 scale: 0.8 
 ```
## Stereo Matching with Dynamic Programming

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 68 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 69 
 scale: 0.8 
 ```
We need to considere the disparity matrix, the ceneter part, and we need to find a path that bring us from start point to the end.

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 70 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 71 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 72 
 scale: 0.8 
 ```

Since we have some missing areas, due to the occlusion

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 73 
 scale: 0.8 
 ```

Occlusin costatnt suggest the presence of the occlusion 

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 74 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 75 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 76 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 77 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 78 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 79 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 80 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 81 
 scale: 0.8 
 ```
## Stereo Matching with Graph Cut algorithm

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 82 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 83 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 84 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 85 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 86 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 87 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 88 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 89 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 90 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 91 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 92 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 93 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 94 
 scale: 0.8 
 ```

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 95 
 scale: 0.8 
 ```

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

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 101 
 scale: 0.8 
 ```

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

 ```slide-note 
 file: StereoMatching_CV2324.pdf 
 page: 110 
 scale: 0.8 
 ```
