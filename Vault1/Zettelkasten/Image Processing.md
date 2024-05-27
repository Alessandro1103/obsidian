Date: 2024-05-27
Time: 12:16
Tags: #ComputerVision #Università  
Up: [[Computer Vision]]

---
# Image Processing

For each coloured image we use a matrix for each color, what we obtain at the end is a tensor.

![[Pasted image 20240527122033.png|400]]

## Point Processing

Each pixel is a version of the previous one
  ![[Pasted image 20240527122724.png|400]]
**Gamma Correction**: is a technique used to adjust the luminance of an image. It's based on the principle that out eyes perceive light non-linearly, we are more sensitive to dark then light tones. $V_{out} = AV_{in}^{\gamma}$


### Histogram Equalization 

It is a type of graph that represents the frequency distribution of a dataset. Equalization change the intensity so the contrast is improved. We can understand how well the colors are distributed looking at the "cumulative intensity" (the black line). If linear the image is well contrasted. 

![[Pasted image 20240527124212.png|400]]

**Intensity Histogram**: $p(r)=\frac{\text{Number of pixels with intensity r}}{\text{Total number of pixels}}$ it is a graph representing the distribution of pixel intensities in an image. 

![[Pasted image 20240527125102.png|300]]
![[Pasted image 20240527125143.png|300]]

**Formula**: 
$$
\begin{align*}
& T(r) = \text{round}\bigg(255 \sum_{i=0}^r p(i)\bigg) & 0\leq r \leq 255
\end{align*}
$$

![[Pasted image 20240527125844.png|400]]

### Local Histogram

Local histogram equalization is realized selecting, for each pixel, a suitable neighbourhood on which the histogram equalization is computed.

![[Pasted image 20240527131218.png|400]]

## Filtering

The objective is to form a new image whose pixel values are a combination of the original pixel values.

The 2D filter is separable if it can b written as the product of a "column" and a "row".
$$
\begin{bmatrix}
1 & 1 & 1 \\
1 & 1 & 1 \\
1 & 1 & 1 \\
\end{bmatrix} = \begin{bmatrix}
1 \\ 1 \\ 1 
\end{bmatrix} * \begin{bmatrix}
1 & 1 & 1
\end{bmatrix}
$$
The cost of convolution with a separable filter is: $2\ \times\ (L\ \times\ M\ \times\ N)$
The cost of convolution with a non-separable filter is: $L^2\ \times\ M\ \times\ N$

### Noise reduction

For each pixel location, calculate the average value from all the images (images of the same subject, all identical except for the noise). This averaging process helps to reduce random noise, as the noise will vary across the images, but the actual scene content will remain constant.



### Cross Correlation

Use a kernel to modify the pixels in the image:
$$
\begin{align*}
& G[i, j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u, v] F[i + u, j + v] & G = H \otimes F
\end{align*}
$$
Neither associative nor commutative ![[Pasted image 20240527132321.png|100]]

### Convolution

Use a kernel to modify the pixels in the image:

$$
\begin{align*}
& G[i, j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u, v] F[i - u, j - v] 
\end{align*}
$$

Convolution is a multiplication like operation: commutative, associative, distributive, scalars factor out, identity multiplication. Kernel is flipped (horizontally and vertically): 

![[Pasted image 20240527132517.png|200]]

### Handling boundaries

![[Pasted image 20240527132628.png|500]]

### Padding & Stride in CNN

$$
O = \left\lfloor \frac{I + 2P - K}{S} \right\rfloor + 1
$$
>[!example]
>Supponiamo di avere un input di dimensione $I=32$ (32x32), un filtro (kernel) di dimensione $K=3$, uno stride di $S=1$, e un padding di $P=1$: 
>$$
>O = \left\lfloor \frac{32 + 2x1 - 3}{1} \right\rfloor + 1 = \left\lfloor \frac{31}{1} \right\rfloor + 1 = 31 + 1 = 32
>$$


### Gaussian Kernel

Follows the gaussian formula: 
$$
G_\sigma = \frac{1}{2 \pi \sigma^2} e^{-\frac{x^2 + y^2}{2 \sigma^2}}
$$

It is able to remove the high-frequency components from the image (low-pass filter)

### Box filtering vs Gaussian filtering

![[Pasted image 20240527152749.png|300]]

### Sharpening

![[Pasted image 20240527153041.png|500]]

Let's review the steps:
1. Take the original image
2. Smooth the image using a gaussian filter
3. Extract the detail removing from the original image the smoothed version
4. Take the original image
5. Add to the origina image the extracted detail image, and scale it by $\alpha$

In formula: $$\text{Sharped image} = F\ *\ ([1+\alpha]e - \alpha H)$$
where:
- F is the image
- H is the gaussian filter
- $\alpha$ is the proportional sharpening
- e is a identity kernel, used to transform the scalar in a matrix


### Bilateral Filtering

When we get close to an edge we can not use the gaussian filter, we would lose the edge. It's better for us to use the Bilateral filtering:
$$
h[m, n] = \frac{1}{W_{mn}} \sum_{k, l} g[k, l] r_{mn}[k, l] f[m + k, n + l]
$$
which is very similar to the gaussian filter but:
- $\frac{1}{W_{mn}}$ is a normalization factor
- $r_{mn}$ is a intensity range weighting, that is favor similar pixels

### Thresholding 

It's a **non-linear filter**:
$$
g(m, n) = \begin{cases} 255, & \text{if } f(m, n) > A \\ 0, & \text{otherwise} \end{cases}
$$

## Sampling & Aliasing

### Down-Sampling 

If the image is too big, we can reduce it, but we will lose quality.

![[Pasted image 20240527161635.png|500]]

To reduce the the dimensionality (down-sampling) we have the following method:
- **Direct Method**: reduces the resolution of the original image in *one step* by the specified factor
- **Repeat Method**: reduce the resolution iteratively 2 by 2

>[!example]
>Using a Direct 4x we downscale the original by a factor of 4
>Using a Repeat 4x we downscale the original by a factor of 2, then by a factor of 2

In this context we can use a pre-filter with a Gaussian filter. Doing so we the image subsampled, zoomed results in a more homogeneous result:

![[Pasted image 20240527162639.png|300]]

This is called **Gaussian pyramid**.

### Up-sampling

If we have an image too small we can make it 10 times as big. The simplest approach is to duplicate each row and column 10 times (Nearest neighbour Interpolation).

![[Pasted image 20240527163222.png|500]]

![[Pasted image 20240527163333.png|300]]


### Aliasing

Occurs when your sampling rate is not high enough ot capture the amount of detail in your image. To avoid aliasing: $f_s \geq 2 \ f_{max}$ where:
- $f_s$ is the sampling frequency
- $f_{max}$ is the highest frequency in the signal

## Image Derivatives
