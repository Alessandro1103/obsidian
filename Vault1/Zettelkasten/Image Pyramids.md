Date: 2024-06-01
Time: 14:00
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Image Pyramids

## Gaussian Pyramid

It's a series of lower resolution version of the original image. 

**Algorithm**: 
1. Take the origina image
2. Apply Gaussian Blurring
3. Sub-sample the Blurred image
4. Go to point 2

Reducing an image by $\frac{1}{4}$, the sum of this infinite geometric series lead to: $S=\frac{a}{1-r}$, where $a$ is the first element, $r$ is the common ratio: $S = \frac{1}{1-\frac{1}{4}} = \frac{4}{3}$.

## Laplacian Pyramid

```slide-note 
file: ImagePyramid.pdf 
page: 13
scale: 0.8
```

The residual highlights the details that have been "lost" due to the blurring process.
If we store the *residuals* we can reconstruct the origina image after its blurriness.

```slide-note 
file: ImagePyramid.pdf 
page: 17
scale: 0.8
```

**Algorithm**:
1. Start with Gaussian Pyramid
2. Subtract Adjacent Gaussian Levels (for each level in the gaussian pyramid, subtract the next level)
3. Calculate the Residual Images and store them
4. Store the Smallest Gaussian Image


```slide-note 
file: ImagePyramid.pdf 
page: 19
scale: 0.8
```

**Algorithm** (reconstruct):
1. Start from the smallest and highest image in the Gaussian pyramid
2. Up-sample (e.g. bilinear, bicubic...) and add the residual
3. Repeat for all levels

Image pyramids use: 
- Image compression
- Image blending
- Denoising
- Multi-scale detection/registration


```slide-note 
file: ImagePyramid.pdf 
page: 35
scale: 0.8
```
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
```slide-note 
file: ImagePyramid.pdf 
page: 38
scale: 0.8
```


** Process exited - Return Code: 0 **
Press Enter to exit terminal