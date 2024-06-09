Date: 2024-06-02
Time: 23:03
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Features

We can have:
- **Global Features**: are attributes that generalize the entire image or video
- **Local Features**: are descriptors of image patches or key points in the image of an object

```slide-note
file: Features.pdf
page: 7
scale: 0.8
```

```slide-note
file: Features.pdf
page: 8
scale: 0.8
```

```slide-note
file: Features.pdf
page: 9
scale: 0.8
```

## Why detect features

1. **Object Recognition**: Identifying and labeling objects within an image. Feature detection helps in distinguishing objects based on their distinct characteristics such as shape, texture, and color.

2. **Localization and Mapping**: Essential in robotics and autonomous vehicle navigation, this process involves determining the position of the device relative to its environment and constructing a map of the surrounding area using detected features.

3. **3D Reconstruction**: Creating three-dimensional models from two-dimensional images. Features detected across multiple images are used to infer the depth and structure of the scene, building a spatial representation.

4. **Augmented Reality**: Enhancing the real world with digital overlays. Feature detection allows the AR system to understand the environment and accurately place digital objects in real-world contexts.

5. **Image Matching**: Comparing and aligning different images based on detected features, even under challenging conditions such as changes in scale, orientation, and lighting. SIFT (Scale-Invariant Feature Transform) is a robust method for matching features across varied scenarios.
## What is good feature

In Local features the steps to found good feature is the following:
1. Detect interest points (keypoints) in the image. Normally are points with high variation in intensity.
2. Describe the keypoints in a way that captures their local appearance independently of other changes like lighting or perspective. To do so, we extract a feature descriptor (array of values) that encodes the appearance around each point. 
3. Match these descriptors across different images.

**Advantages**:
- *Locality*: robust to partial occlusion (part of the object is blocked) and cutter (when the scene is crowded with many objects) of the image
- *Quantity*: a single image can contain hundreds of local features
- *Distinctiveness*: uniquely identify and differentiate a wide range of objects
- *Efficiency*: real-time performance

The objective is to find features that are invariant to transformations:
- Geometric invariance: translation, rotation, scale …
- Photometric invariance: brightness, exposure …
## Harris Corner Detector

We do not check pixel by pixel. We use a patch that moving, will find what is looking for. If we move along a line without arriving to corners, the intensity do not change.

```slide-note
file: Features.pdf
page: 30
scale: 0.8
```

The main operation we perform is to calculate the Sum of Squared Differences (SSD) for each shift. This is done comparing the intensity we have now, with the intensity before:

$$
E(u, v) = \sum_{(x,y) \in W} \left[ I(x+u, y+v) - I(x, y) \right]^2
$$

We are happy if this error is high. For small motion assumption we can use the Taylor Series:
$$
\begin{align*}
&I(x+u, y+v) = I(x,y) + \frac{\partial I}{\partial x} u + \frac{\partial I}{\partial y}v = I(x,y) + \begin{bmatrix}I_x & I_y\end{bmatrix}\begin{bmatrix}u\\v\end{bmatrix} & I_x=\frac{\partial I}{\partial x},I_y=\frac{\partial I}{\partial y} 
\end{align*}
$$
which substituting with the Error before becomes:

$$ 
\begin{equation}
\begin{aligned}
E(u, v) & \approx \sum_{(x,y) \in W} \left[ I_x u + I_y v \right]^2 \approx Au^2 + 2Buv + Cv^2 \\
& = \begin{bmatrix}u& v\end{bmatrix} \begin{bmatrix}A & B \\ B & C\end{bmatrix} \begin{bmatrix}u\\ v\end{bmatrix} \\
& = \begin{bmatrix}u& v\end{bmatrix} H \begin{bmatrix}u\\ v\end{bmatrix} \\ \\
A & = \sum_{(x,y) \in W} I_x^2 \\
B & = \sum_{(x,y) \in W} I_x I_y \\
C & = \sum_{(x,y) \in W} I_y^2
\end{aligned}
\end{equation}
$$

If H is full: ![[Pasted image 20240603003113.png]]
If $I_x$ then $H = \begin{bmatrix}0 & 0 \\ 0 & C\end{bmatrix}$, means that the edge is horizontal:
![[Pasted image 20240603004327.png]]

If $I_y$ then $H = \begin{bmatrix}A & 0 \\ 0 & 0\end{bmatrix}$ its specular, means that the edge is vertical.

A possible version of the Harris matrix is M, this is called also Bilinear approximation:
$$
M = \sum_{(x,y) \in W} w(x,y) \begin{bmatrix} I_x^2 & I_x I_y \\ I_x I_y & I_y^2 \end{bmatrix}
$$
where we add $w$ which is a gaussian function that enhances the local information.

To understand how well each element is correlated with another and how the pixels change in a small location, we can use the **Covariance Matrix**:
$$
\begin{bmatrix}
\sum_{p \in P} I_x I_x & \sum_{p \in P} I_x I_y \\
\sum_{p \in P} I_y I_x & \sum_{p \in P} I_y I_y
\end{bmatrix}
$$
$P$ is the set of pixels in a given regione of the image.
To understand the behaviour of M we can analyse the eigenvalues:
$$
\begin{align*}
& M \mathbf{e} = \lambda \mathbf{e} & (M - \lambda I) \mathbf{e} = 0
\end{align*}
$$
After you find out what are the eigenvalues and eigenvector you can write the following:
$$
\begin{align*}
& M = R^{-1} \begin{bmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{bmatrix} R &
x^T \ M \ x = \text{const} \\\\

& \frac{(e_1^Tx)^2}{(\frac{1}{\sqrt{\lambda_{max}}})^2} + \frac{(e_2^Tx)^2}{(\frac{1}{\sqrt{\lambda_{min}}})^2} = 1


\end{align*}
$$

We can visualize all as an ellipse with axis lengths determined by the eigenvalues and orientation determined by R (composed by eigenvectors):

![[Pasted image 20240605113721.png|300]]

If the eigenvectors ($e$) are 1, so zero rotation, this is what we obtain:

![[Pasted image 20240605120604.png|300]]

We are moving in the direction with the minor eigenvalue (fastest).

![[Pasted image 20240605120724.png|400]]



```slide-note
file: Features.pdf
page: 48
scale: 0.8
```

```slide-note
file: Features.pdf
page: 49
scale: 0.8
```

The image in the left shows a common test image for corner detection. The image in the middle, with $\lambda_{max}$ shows the response form an algorithm that highlights areas with the largest eigenvalues. The lines are highlighted because these are the areas with one dominant gradient direction, corresponding to an edge. In $\lambda_{min}$ case, both eigenvalues are large because the gradient changes in multiple directions.

```slide-note
file: Features.pdf
page: 50
scale: 0.8
```

$\lambda_{min}$ is a measure of the intensity variation in the least varying direction. If $\lambda_{min}$ is large, it indicates significant variation in all directions, suggesting a corner. Choose the point where $\lambda_{min}$ is a local maximum. These points are more likely to be true corners, as they reprensent areas with the highest intensity variation in all directions.

**Harris operator**:
$$
f = \frac{determinant(H)}{trace(H)} = \frac{\lambda_1\lambda_2}{\lambda_1+\lambda_2}
$$
or:
$$
R = determinat(M) - k \cdot trace(M)^2
$$

which help determine the threshold for detecting a corner. It is a variant of taking just $\lambda_{min}$

>[!algorithm]
>1. Compute Gaussian derivatives at each pixel ($I_x$ and $I_y$)
>2. Compute second moment matrix H in a Gaussian window around each pixel
>3. Compute corner response function $f$ or $R$
>4. Threshold $f$ or $R$
>5. Find local maxima of response function

## Properties of Harris Corner Detector

When dealing with image features, such as corners, we aim for the features to be robust to various transformations. This robustness is described by the terms invariance and equivariance.

- **Invariance**: the *feature locations* do not change when the image undergoes certain transformations. In our case we want that our detector is invariant to the light, meaning that if an image is brightened or darkened the corner locations should remain the same.
- **Equivariance**: if we apply a transformation to an image, the detected features should correspondingly transform in a predictable way. In our case we want that if our image is rotated the detected corners should rotate similarly.

Properties:

- Corner location is equivariant w.r.t. translation (derivatives and window function are equivariant)
- Corner location is equivariant w.r.t. image rotation (the eigenvalues in the second moment ellipse rotates but the values remains the same)
- Partially invariant to affine intensity change:
	- If the intensity is only shifted, $I \rightarrow I + b$ the derivative removes the $b$
	- If the intensity is scaled, $I\rightarrow \ aI$ the derivative can not delete $a$ and the scaled values goes in the detector R, but since the threshold is fixed, some values that before where not considered, now are taken as edges
- Neither invariant nor equivariant to scaling, since if we zoom inside an edge a lot, we can not see the actual edge, we see it as a curve and the detector doesn't recognize it

To create a scale Invariant Detection we need to consider regions (patches) of different sizes around a point, a multi scale analysis. And even if scaled at some scale, the regions (or patches) represent the same portion of the image, even if the image itself has been scaled.

![[Pasted image 20240605132304.png|300]]

The challenge is to select regions (circles) of the right size around each point in the image independently, so that corresponding features can be detected even when the scale changes. The idea is to select the scale at which the feature (e.g., a corner) is most prominent or has the highest response. This can be done finding $f$ (or $R$) for each scale, and selecting the max.

![[Pasted image 20240605132855.png|300]]


>[!Algorithm Rilevazione Equivariant Keypoints]
>1. Construction of a scaled image pyramid (Laplace pyramid)
>2. Application of the LoG (instead of Harris Operator) for each level
>3. Finding the Maximum between scale and space
>4. Selecting points with the maximum LoG normalized response and recording the associated scale
>5. Output of keypoints

## Blob Detector

The Laplacian of Gaussian (LoG) is a popular technique used in image processing to detect regions of rapid intensity change, often used for blob detection. It combines the smoothing effect of the Gaussian filter with the edge-detection capabilities of the Laplacian operator.

```slide-note
file: Features.pdf
page: 77
scale: 0.8
```

```slide-note
file: Features.pdf
page: 78
scale: 0.8
```

```slide-note
file: Features.pdf
page: 79
scale: 0.8
```


