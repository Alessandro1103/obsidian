Date: 2024-06-07
Time: 16:18
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# 2D Transformation and Alignment

If we want to create mosaics (take two picture and understand how the should be connected, modifying shape, scale etc) , what we need to do is to understand how an image change. 

We can have general warping:
- filtering, change the range of image: ![[Screenshot from 2024-06-07 16-26-08.png|300]]
- warping, change the domain of image:![[Screenshot from 2024-06-07 16-26-20.png|300]]
In more general way a (global) warping:

![[Screenshot from 2024-06-07 16-28-11.png|300]]

We can define a transformation matrix called $T$:
$$
\begin{align*}
& p'=T(p) & \begin{bmatrix} x' \\ y' \end{bmatrix} = T \begin{bmatrix} x \\ y \end{bmatrix}
\end{align*}
$$
called global because it is the same for any point $p$

## Types of 2D Transformations

### Linear

We have **Rotation** by an angle $\theta$. $R=\begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$ where $R^{-1}=R^T$.

**Scale** around a point: $S = \begin{bmatrix}s_x & 0 \\ 0 & s_y \end{bmatrix}$.

**Shear**: $SH = \begin{bmatrix}1 & sh_x \\ sh_y & 1\end{bmatrix}$

**Mirror**: $M = \begin{bmatrix}-1 & 0 \\0 & -1\end{bmatrix}$

Only linear 2D transformations can be represented with a 2x2 matrix, for example translation is not possible.

### Affine

In order to represent a translation we need to move to 3x3 matrix:
$$
\begin{bmatrix}
1&0&t_x \\
0&1&t_y \\
0&0&1
\end{bmatrix}
$$
every transformation represented by a 3x3 matrix with last row $\begin{bmatrix}0& 0& 1\end{bmatrix}$, we call an *affine* transformation.


```slide-note
file: TransformationAlignment.pdf
page: 23
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 24
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 25
scale: 0.8
```

### Perspective (Homography)


```slide-note
file: TransformationAlignment.pdf
page: 27
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 31
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 32
scale: 0.8
```

## Computing 2D Transformations

```slide-note
file: TransformationAlignment.pdf
page: 34
scale: 0.8
```
### Linear Least Squares

```slide-note
file: TransformationAlignment.pdf
page: 36
scale: 0.8
```

If we have more equations than unknowns we need to find the *least squares solution*:

```slide-note
file: TransformationAlignment.pdf
page: 39
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 40
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 41
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 42
scale: 0.8
```

### Affine

```slide-note
file: TransformationAlignment.pdf
page: 48
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 49
scale: 0.8
```

The cost function is still a Mean Squared Error (MSE):

```slide-note
file: TransformationAlignment.pdf
page: 50
scale: 0.8
```

### Homography

```slide-note
file: TransformationAlignment.pdf
page: 52
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 53
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 54
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 55
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 56
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 57
scale: 0.8
```

### Final

>[!Algorithm]
>1. Compute image features for A and B
>2. Match features between A and B
>3. Compute homography between A and B using least squares on set of matches


## Outliers

```slide-note
file: TransformationAlignment.pdf
page: 61
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 62
scale: 0.8
```

For all possible lines, select the one with the largest number of inliers

```slide-note
file: TransformationAlignment.pdf
page: 66
scale: 0.8
```

### RASAC

In order to find a model parameters that maximize the number of inliers, we make the following assumptions:
- All inliers will agree with each other on the model parameters (e.g., translation vector in the context of image alignment)
- Outliers will (hopefully) not agree with each other and with the inliers

The condition to work is that there are less than 50% of outliers

>[!Algorithm General RANSAC]
>1. Randomly choose $s$ samples
>2. Fit a model to those samples
>3. Count the number of inliers that approximately fit the model
>4. Repeat $N$ times
>5. Choose the model that has the largest set of inliers

>[!Algorithm homography RANSAC]
>1. Select four feature pairs
>2. Compute homography H
>3. Compute inliers where dist($p_i'$, $Hp_i$)<$\epsilon$
>4. Keep largest set of inliers
>5. Re-compute least squares H estimate on all of the inliers

```slide-note
file: TransformationAlignment.pdf
page: 76
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 78
scale: 0.8
```

### Warping

```slide-note
file: TransformationAlignment.pdf
page: 80
scale: 0.8
```

$$
g(x,y) = f(T(x,y))
$$

```slide-note
file: TransformationAlignment.pdf
page: 81
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 82
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 83
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 84
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 85
scale: 0.8
```

### Blending

```slide-note
file: TransformationAlignment.pdf
page: 88
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 89
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 92
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 93
scale: 0.8
```

To do so, we use the Laplacian Pyramid:

>[!Algorithm Blending]
>1. Build Laplacian Pyramids
>2. Build Gaussian Pyramids
>3. Form a Combined Pyramid: $LS(i,j) = GR(i,j) \cdot LA(i,j) + (1 - GR(i,j)) \cdot LB(i,j)$
>4. Collapse the LS pyramid to get the final blended image
