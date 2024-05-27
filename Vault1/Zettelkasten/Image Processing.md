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

### Noise reduction

For each pixel location, calculate the average value from all the images (images of the same subject, all identical except for the noise). This averaging process helps to reduce random noise, as the noise will vary across the images, but the actual scene content will remain constant.

#### Cross Correlation

Use a kernel to modify the pixels in the image:
$$
\begin{align*}
& G[i, j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u, v] F[i + u, j + v] & G = H \otimes F
\end{align*}
$$
Neither associative nor commutative ![[Pasted image 20240527132321.png|100]]

#### Convolution

Use a kernel to modify the pixels in the image:

$$
\begin{align*}
& G[i, j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u, v] F[i - u, j - v] 
\end{align*}
$$

Convolution is a multiplication like operation: commutative, associative, distributive, scalars factor out, identity multiplication. Kernel is flipped (horizontally and vertically): ![[Pasted image 20240527132517.png|200]]

#### Handling boundaries

![[Pasted image 20240527132628.png|500]]

