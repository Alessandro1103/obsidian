Date: 2024-06-06
Time: 15:50
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# FeaturesCV3

## SIFT

We'll delve into the **SIFT** (Scale Invariant Feature Transform) algorithm, which is widely used in computer vision for object recognition, robotica mapping, and image stitching. SIFT is used both as a detector and a descriptor. It detects and describes local features in images. 

1. **Multi-scale Extreme Detection**: This step involves searching for stable features across multiple scales. It uses a scale-space representation.
2. **Keypoint Localization**: After identifying potential interest points, SIFT refines these keypoints to achieve more accurate localization.
3. **Orientation Assignment**: Each keypoint is assigned one or more orientations based on local image gradient directions. This step ensures that the keypoint descriptor is rotation invariant.
4. **Keypoint Descriptor**: The local image gradients are measured at the selected scale in the region around each keypoint. These are transformed into a representation that allows for significant levels of local shape distortion and change in illumination.
### SIFT detector

The SIFT detector uses the **Difference of Gaussians** (DoG) method to approximate the Laplacian of Gaussian (LoG). 
$$
\text{DoG}(x, y, \sigma) = G(x, y, k\sigma) - G(x, y, \sigma)

$$
where $G(x,y,\sigma)$ is the Gaussian blur at scale $\sigma$ and $k$ is a constant that determines the scale multiplication for each subsequent Gaussian blur.

```slide-note
file: Features3.pdf
page: 10
scale: 0.8
```

#### Creation of the pyramid
The image pyramid is created by repeatedly blurring and subsampling the image. Each level of the pyramid represents a different octave (scale) in the scale-space representation. At each octave the image is progressively blurred more to create a set of images each at a higher scale. To go to the next octave, the image is downsampled by a factor of 2.

```slide-note
file: Features3.pdf
page: 12
scale: 0.8
```

#### Extrema detector

![[Screenshot from 2024-06-06 16-27-02.png|150]]

In order to find the best keypoint we look at the neighbors, 8 in the same level, and 9 in the plane upper and down (each), so we ends in 26 neighbors. It's like using a window of 3x3x3. If that pixel is a local min/max then it is a candidate for keypoint.

#### Illumination-thresholding

During the process of keypoint detection using the Difference of Gaussians images, one important step is to remove low contrast features (below a threshold), don't provide reliable information.  

```slide-note
file: Features3.pdf
page: 14
scale: 0.8
```

#### Keypoint Orientation

The next thing is to assign an orientation to each keypoint, this orientation provides rotation invariance. For all levels, compute Gradient magnitude and orientation. 

![[Screenshot from 2024-06-06 16-46-05.png|300]]

Then we create an histogram, this histogram spans 360 degrees, divided into 36 bins (each representing a 10-degree interval). The contributions of the gradients to the histogram are weighted by their magnitudes, ensuring that directions in which the gradient is stronger have a greater influence on the histogram.

>[!example]
>![[Screenshot from 2024-06-06 16-59-20.png|300]]
>
>In this case, taking the gradient from a picture we don't see, the gradient direction of a pixel is about 18 degrees. We go into the histogram and add a value proportional to the magnitude of that orientation. This is done for all pixels we think are keypoints and the ones near them. At the end the peak of the histogram is the keypoint. All the peaks over the 80% are converted in new keypoints.


```slide-note
file: Features3.pdf
page: 19
scale: 0.8
```

### SIFT descriptor

For each detected keypoint is assigned:
- Location
- Scale (magnitude)
- Orientation

```slide-note
file: Features3.pdf
page: 23
scale: 0.8
```

>[!Algorithm build SIFT descriptor]
>The steps of building the SIFT descriptor are as following:
>1. Use the Gaussian blurred image that corresponds to the keypoint's scale
>2. Select the 16x16 window around the keypoint
>3. Calculate the gradient angle of the 16x16 window, and then rotate it of the keypoint's angle, so that the window becomes more robust to rotations
>4. Divide the 16x16 window in 4x4 grids (16 cells) 
>5. Compute the histogram (8 bins for 360 degrees) for each 2x2 grid

The result is a SIFT descriptor of 128 vectors: 4x4 histograms, each with 8 orientation bins.

![[Screenshot from 2024-06-11 10-11-17.png|300]]

![[Screenshot from 2024-06-06 19-20-28.png|300]]

SIFT descriptor properties:
- Invariant to rotation (if we assume that a rotation of x, will generate a keypoint that is rotated by x)
- Invariant to scale (DoG scaled the image at the start)![[Screenshot from 2024-06-07 10-45-54.png|200]]
- Invariant to illumination
- Slightly robustness to affine transformation and to noise![[Screenshot from 2024-06-07 10-46-24.png|200]]
## SURF

The SURF is a feature detection framework, his procedure is divided in:
1. Interest Point Detection
2. Interest Point Description
3. Interest Point Matching
### SURF detection
#### Filtering Approach 
Unlike SIFT, which uses a Gaussian pyramid, SURF employs box filters that can be computed quickly using integral images.
**Integral Images**: are tool used to quickly and efficiently calculate the sum of values in a rectangular subset of a grid. This, with a classical box filters, approximate the Gaussian filters

![[Screenshot from 2024-06-07 11-07-25.png|200]]

$$
I_{\Sigma}(x, y) = \sum_{i=0}^{x} \sum_{j=0}^{y} I(i, j)
$$

```slide-note
file: Features3.pdf
page: 36
scale: 0.8
```

#### Hessian Matrix Blob Detector
The determinant of this matrix is a measure (max) of response for each pixel to select candidate points.

![[Screenshot from 2024-06-07 11-17-23.png|300]]

$$
\begin{align*}
& H(x,\sigma) = \begin{bmatrix}
L_{xx}(x,\sigma) & L_{xy}(x,\sigma)\\
L_{xy}(x,\sigma) & L_{yy}(x,\sigma)
\end{bmatrix}
& L_{xx}(x, \sigma) = \frac{\partial^2}{\partial x^2} (G(x, \sigma) \ast I(x))
\end{align*}
$$

So the L are the partial derivatives of the convolution of Gaussian per the image.
$$
\text{det}(H_{\text{approx}}) = D_{xx}D_{yy} - (wD_{xy})^2
$$
where $D$ are the box filters approximation.

#### Laplacian Indexing

Applied during the matching phase. Distinguish between interest points on bright blobs against dark backgrounds and the reverse scenario. 

#### Scale-Space representation

To match interest points across different scales, a pyramidal scale space is built. Rather than serial downsampling, each successive level of the pyramid is built by upscaling the image in parallel. Each scale is defined as the response of the image convolved with a box filter of a certain dimension. The scale space is further divided into octaves.

#### Orientation Assignment

To achieve rotational invariance in the SURF algorithm, the orientation of each keypoint is calculated by analyzing Haar wavelet responses in the x and y directions within a circular neighborhood of radius $6s$, where $s$ is the scale of detection. These responses are weighted by a Gaussian centered at the keypoint and plotted in a two-dimensional space. The dominant orientation is identified by summing responses within a $\pi/3$ radians sliding window to create a local orientation vector. The longest vector from this process defines the keypoint's orientation, balancing robustness with angular resolution to ensure the descriptor's rotation invariance.

![[Pasted image 20240611125154.png|300]]

#### Feature Vector

The SURF descriptor extraction involves centering a $20s$ sized, orientation-aligned square window on an interest point and dividing it into a $4 \times 4$ grid. Each sub-region calculates Haar wavelet responses at 25 sample points, weighted by a Gaussian for robustness against noise and deformation. These responses are summed to form local feature vectors, which are concatenated into a 64-element vector that describes the local image structure around the interest point, ensuring *rotation invariance* and *robustness to transformations*.

$$
V = \begin{bmatrix}\sum d_x\\ \sum d_y\\\sum |d_x|\\\sum |d_y|\end{bmatrix}
$$
where $d_x$ are the horizontal responses (a vector of 16 values), same for $d_y$.

## Binary descriptors

The strategy of binary descriptors is:
- Select a patch around a keypoint
- Select a set of pixel pairs in that patch (no strategy needed)
- Intensity Comparison:   $$ b = \begin{cases} 1 & \text{if } I(s_1) < I(s_2) \\ 0 & \text{otherwise} \end{cases} $$
Indeed, this defines a code for a patch around a keypoint, and this code will be the descriptor. This descriptor is the element that we aim to find in other images.

```slide-note
file: Features3.pdf
page: 46
scale: 0.8
```

**Advantages**:
- Compact descriptor: the number in binary gives us the length too
- Fast to compute: simply intensity value comparisons
- Trivial and fast to compare: hamming distance $$
  d_{Hamming}(B_1, B_2) = sum(xor(B_1, B_2))
  $$
## BRIEF

This is the first binary image descriptor. In the following there are some methodology for choosing the pairs we need to compare (sampling pairs):
- $I$: Uniform random sampling
- $II$: Gaussian sampling
- $III$: $s_1$ Gaussian; $s_2$ Gaussian centered around $s_1$
- $IV$: Discrete location from a Coarse polar grid
- $V$: $s_1=(0,0)$; $s_2$ are all location from a coarse polar grid
### ORB (Oriented FAST and Rotated BRIEF)
#### Extension: Rotation Compensation

In this part we need to estimated the center of mass and the main orientation of the area/patch. 

Image moment:
$$
m_{pq} = \sum_{x,y} x^p y^q I(x,y)
$$
Center of mass:
$$
C = \left( \frac{m_{10}}{m_{00}}, \frac{m_{01}}{m_{00}} \right)
$$
>[!example]
>$$
>\begin{bmatrix}
>1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9
>\end{bmatrix}
>$$
>Zero Moment: $m_{00} = 1+2+3+4+5+6+7+8+9=45$
>First Moment about x: $m_{10} = 1*0+2*1+3*2+4*0+5*1+6*2+7*0+8*1+9*2=51$
>First Moment about y: $m_{01} = 1*0+2*0+3*0+4*1+5*1+6*1+7*2+8*2+9*2=63$ 
>Center of Mass
>$C = \left(\frac{m_{10}}{m_{00}}, \frac{m_{01}}{m_{00}}\right) = \left(\frac{51}{45}, \frac{63}{45}\right) \approx \left(1.13, 1.4\right)$
>Orientation $\theta$
>$\theta = atan2(m_{01}, m_{10}) = atan2(63,51)$
>
>as you can see the first moments, are calculated considering a certain row or column bond with 0,1,2

To achieve rotation invariance, the image patch around each keypoint is rotated by $\theta$ around $C$:
$$
s' = T(C,\theta)s
$$
The descriptor is the same as before: binary string.

Pairs should be/have:
- uncorrelated (new information)
- high variance (feature more discriminative)

## Freak sampling

```slide-note
file: Features3.pdf
page: 57
scale: 0.8
```
## Feature Matching

When we have Image Matching we want to find in a image the maximum number of keypoints, for each keypoint, search similar descriptor in a reference image. 

If we find a feature in image $I_1$, how do I find the best match (feature in image $I_2$)? So this happens after we applied a SIFT etc. Once we found the best keypoint in a image we use a feature matching.
To do so, we need to define a distance function and compares the two descriptors (mean squared error, mean absolute error...). Then test all the features in $I_2$, find the one with min distance or test all the features in $I_2$, find top k matches.

One of the best measurement is the **Radio test**:
$$
distance\ ratio = \frac{||f_1-f_2||}{||f_1-f'_2||}
$$
where $f_1$ is the feature descriptor from image $I_1$, $f_2$ is the best match for $f_1$ in image $I_2$ (smallest distance match), $f'_2$ is the second-best match for $f_1$ in image $I_2$ (second smallest distance match).
This process is made multiple times, the the distance ratio found are sorted. 

A lower ratio indicates a more confident match.
Setting a threshold simplify the calculus: 
$$
\text{If  } \frac{||f_1-f_2||}{||f_1-f'_2||}< \rho \text{ (e.g., 0.5)}
$$

this means the best match $f_2$ must be at least twice as close to $f_1$ as the second best match $f'_2$. 
Higher threshold (lower $\rho$) gives less matches (eliminates false positive) but more accurate.

## Evaluating Results

How can we measure the performance of a feature matcher? Imposing another threshold can help, removing the bottom part of the distance found.


```slide-note
file: Features3.pdf
page: 72
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 73
scale: 0.8
```

Suppose we want to minimize false positives. How do we set the threshold?

### ROC curve

An ROC curve is generated by plotting the TPR against the FPR at various threshold levels

![[Screenshot from 2024-06-07 13-55-33.png|150]]

![[Screenshot from 2024-06-07 13-55-44.png|150]]

The AUC is the area under the ROC curve, higher AUC (between 0 and 1) better the system guesses.

### Accuracy

$$
\frac{tp + tn}{tp+fp+tn+fn}
$$
It is the proportion of correct predictions among the total number of cases examined.
### Precision
Precision measures the accuracy of the positive predictions made by a classifier. It answers the question, "Of all the instances predicted as positive, how many were truly positive?"
$$
\frac{tp}{tp+fp}
$$

### Recall
Recall measures the ability of a classifier to capture all the relevant positive instances. It answers the question, "Of all the true positive instances, how many were successfully predicted?"
$$
\frac{tp}{tp+fn}
$$
### F1 score
Combines both precision and recall into a single metric. It is the harmonic mean of precision and recall, providing a balanced measure that takes both false positives and false negatives into account.
$$
\text{F1 score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}

$$
