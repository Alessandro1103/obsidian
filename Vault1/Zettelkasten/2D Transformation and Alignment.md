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


![[Pasted image 20240621225637.png|400]]

![[Pasted image 20240621225649.png|400]]

![[Pasted image 20240621225658.png|400]]

### Perspective (Homography)


![[Pasted image 20240621225751.png|400]]

![[Pasted image 20240621225808.png|400]]

![[Pasted image 20240621225826.png|400]]

## Computing 2D Transformations

![[Pasted image 20240621225845.png|400]]
### Linear Least Squares

![[Pasted image 20240621225903.png|500]]

If we have more equations than unknowns we need to find the *least squares solution*:

![[Pasted image 20240621225923.png|450]]

![[Pasted image 20240621225940.png|450]]

![[Pasted image 20240621225956.png|450]]

![[Pasted image 20240621230012.png|450]]
### Affine

![[Pasted image 20240621230029.png|400]]

![[Pasted image 20240621230042.png|400]]

The cost function is still a Mean Squared Error (MSE):
![[Pasted image 20240621230122.png|400]]

### Homography

![[Pasted image 20240621230202.png|400]]

![[Pasted image 20240621230216.png|400]]

![[Pasted image 20240621230229.png|400]]

![[Pasted image 20240621230241.png|400]]

![[Pasted image 20240621230253.png|400]]

![[Pasted image 20240621230307.png|500]]

### Final

>[!Algorithm]
>1. Compute image features for A and B
>2. Match features between A and B
>3. Compute homography between A and B using least squares on set of matches


## Outliers

![[Pasted image 20240621230332.png|450]]

![[Pasted image 20240621230350.png|450]]

For all possible lines, select the one with the largest number of inliers

![[Pasted image 20240621230404.png|450]]

### RANSAC

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

![[Pasted image 20240621230440.png|300]]

![[Pasted image 20240621230456.png|400]]

### Image Warping

Image warping involves applying a geometric transformation to an image to align it with a reference image for panorama stitching. To do this, each image undergoes a transformation using a homography to match the reference image’s coordinate frame. 
$$
g(x,y) = f(T(x,y))
$$
However, issues such as pixels not landing precisely in the center of the target image and resulting holes in the output image (due to uncovered pixel locations) can occur.

![[Screenshot from 2024-06-11 17-14-51.png|300]]

These issues are addressed using backward warping rather than forward warping. **Backward warping** involves first mapping the corners of the original image (using the transformation) to determine the target image’s bounds and then mapping from this output space back to the original image to ensure all pixels are filled accurately, often employing interpolation to optimize the pixel values.

![[Screenshot from 2024-06-11 17-15-34.png|300]]


![[Screenshot from 2024-06-11 17-16-33.png|300]]

![[Screenshot from 2024-06-11 17-17-16.png|300]]

![[Screenshot from 2024-06-11 17-18-11.png|300]]
### Blending Images

After images are aligned, blending is essential to minimize visible seams due to exposure differences or lens characteristics like vignetting. The initial approach might involve averaging overlapping pixel values across images, but this often results in visible seams. A more sophisticated method involves using a **weighted blending technique** where each pixel’s contribution is adjusted based on its proximity to the edge of its image, increasing confidence in its value the further it is from the boundary. This is achieved by employing a smooth transition weighting function that adjusts the contribution of each image in the overlap areas. When properly applied, this technique produces a seamless panorama, eliminating artifacts that could distract from the visual continuity of the scene.

To do so, we use the Laplacian Pyramid:

>[!Algorithm Blending]
>1. Build Laplacian Pyramids LA and LB from images A and B
>2. Build Gaussian Pyramids GR from selected region R
>3. Form a Combined Pyramid: $LS(i,j) = GR(i,j) \cdot LA(i,j) + (1 - GR(i,j)) \cdot LB(i,j)$
>4. Collapse the LS pyramid to get the final blended image
