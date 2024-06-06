Date: 2024-06-06
Time: 15:50
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# FeaturesCV3

We'll delve into the **SIFT** (Scale Invariant Feature Transform) algorithm, which is widely used in computer vision for object recognition, robotica mapping, and image stitching. SIFT is used both as a detector and a descriptor. It detects and describes local features in images. 

1. **Multi-scale Extreme Detection**: This step involves searching for stable features across multiple scales. It uses a scale-space representation.
2. **Keypoint Localization**: After identifying potential interest points, SIFT refines these keypoints to achieve more accurate localization.
3. **Orientation Assignment**: Each keypoint is assigned one or more orientations based on local image gradient directions. This step ensures that the keypoint descriptor is rotation invariant.
4. **Keypoint Descriptor**: The local image gradients are measured at the selected scale in the region around each keypoint. These are transformed into a representation that allows for significant levels of local shape distortion and change in illumination.
## SIFT detector

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

In order to find the best keypoint we look at the neighbors, 8 in the same level, and 9 in the plane upper and down (each), so we ends in 26 neighbors. 

![[Screenshot from 2024-06-06 16-27-02.png|150]]

The image pyramid is created by repeatedly blurring and subsampling the image. Each level of the pyramid represents a different octave (scale) in the scale-space representation. At each octave the image is progressively blurred more to create a set of images each at a higher scale. To go to the next octave, the image is downsampled by a factor of 2.

```slide-note
file: Features3.pdf
page: 12
scale: 0.8
```

**Illumination-thresholding**
During the process of keypoint detection using the Difference of Gaussians images, one important step is to remove low contrast features (below a threshold), don't provide reliable information.  

```slide-note
file: Features3.pdf
page: 14
scale: 0.8
```

### Keypoint Orientation

The next thing is to assign an orientation to each keypoint, this orientation provides rotation invariance. For all levels, compute Gradient magnitude and orientation. 

![[Screenshot from 2024-06-06 16-46-05.png|300]]

Then we create an histogram, this histogram spans 360 degrees, divided into 36 bins (each representing a 10-degree interval). The contributions of the gradients to the histogram are weighted by their magnitudes, ensuring that directions in which the gradient is stronger have a greater influence on the histogram.

>[!example]
>![[Screenshot from 2024-06-06 16-59-20.png|300]]
>
>In this case, taking the gradient from a picture we don't see, the gradient direction of a pixel is about 18 degrees. We go into the histogram and add a value proportional to the magnitude of that orientation. This is done for all pixels





```slide-note
file: Features3.pdf
page: 18
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 19
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 20
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 21
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 22
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 23
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 24
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 25
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 26
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 27
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 28
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 29
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 30
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 31
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 32
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 33
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 34
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 35
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 36
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 37
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 38
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 39
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 40
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 41
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 42
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 43
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 44
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 45
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 46
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 47
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 48
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 49
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 50
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 51
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 52
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 53
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 54
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 55
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 56
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 57
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 58
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 59
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 60
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 61
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 62
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 63
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 64
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 65
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 66
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 67
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 68
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 69
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 70
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 71
scale: 0.8
```

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

```slide-note
file: Features3.pdf
page: 74
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 75
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 76
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 77
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 78
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 79
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 80
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 81
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 82
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 83
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 84
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 85
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 86
scale: 0.8
```

```slide-note
file: Features3.pdf
page: 87
scale: 0.8
```




** Process exited - Return Code: 0 **
Press Enter to exit terminal