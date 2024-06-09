Date: 2024-06-01
Time: 14:00
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Image Pyramids

## Gaussian Pyramid

It's a series of lower resolution version of the original image. 

>[!Algorithm] Gaussian Pyramid
>1. Take the original image
>2. Apply Gaussian Blurring
>3. Sub-sample the Blurred image
>4. Go to point 2

Reducing an image by $\frac{1}{4}$, the sum of this infinite geometric series lead to: $S=\frac{a}{1-r}$, where $a$ is the first element, $r$ is the common ratio: $S = \frac{1}{1-\frac{1}{4}} = \frac{4}{3}$. This value represents the possible space occupied by the image if we tend to infinite, $\frac{4}{3}$ of the original size.

## Laplacian Pyramid

```slide-note 
file: ImagePyramid.pdf 
page: 13
scale: 0.8
```

The residual highlights the details that have been "lost" due to the blurring process.
If we store the *residuals* we can reconstruct the original image after its blurriness.

```slide-note 
file: ImagePyramid.pdf 
page: 17
scale: 0.8
```

>[!Algorithm] Laplacian pyramid
>1. Start with Gaussian Pyramid
>2. Subtract Adjacent Gaussian Levels (for each level in the Gaussian pyramid, subtract the next level)
>3. Calculate the Residual Images and store them
>4. Store the Smallest Gaussian Image


```slide-note 
file: ImagePyramid.pdf 
page: 19
scale: 0.8
```

>[!Algorithm] Reconstruct Laplacian pyramid
>1. Start from the smallest and highest image in the Gaussian pyramid
>2. Up-sample (e.g. bilinear, bicubic...) and add the residual
>3. Repeat for all levels

The space calculation made before can be done for this as well. In particular instead of levels we store residuals, so the result is the same.

Image pyramids are used in: 
- Image compression
- Image blending
- Denoising
- Multi-scale detection/registration

## Steerable pyramid

The Steerable Pyramid is a multi-scale, multi-orientation image decomposition method. Used in texture analysis, compression, denoising, edge detention. 

![[Pasted image 20240602170728.png|320]]

## Wavelets pyramids

Wavelet analysis is a method used to separate the information in an image into high-frequency details and low-frequency approximations using high-pass and low-pass filters.

```slide-note 
file: ImagePyramid.pdf 
page: 36
scale: 0.8
```
```slide-note 
file: ImagePyramid.pdf 
page: 37
scale: 0.8
```
