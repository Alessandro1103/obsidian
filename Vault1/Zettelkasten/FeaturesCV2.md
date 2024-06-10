Date: 2024-06-05
Time: 17:31
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Features2

## Feature descriptors

A good feature descriptor should ensure that patches with similar content yield similar descriptors, regardless of minor variations in the image. Consistency in descriptors allows for accurate matching across different images.

### Image patch
just use the pixel values of the patch

![[Pasted image 20240605174150.png|400]]

| Non-Invariant                 | Invariant |
| ----------------------------- | --------- |
| Light, Color, Rotation, Scale |           |

### Image gradients:
differences between adjacent pixel values are calculated

![[Pasted image 20240605174314.png|400]]

| Non-Invariant   | Invariant        |
| --------------- | ---------------- |
| Rotation, Scale | Light, Intensity |

### Color histogram
counts the number of pixels for each color in an image

![[Pasted image 20240605174751.png|400]]

| Non-Invariant | Invariant       |
| ------------- | --------------- |
| Light, Color  | Rotation, Scale |

### Spatial histograms
compute histograms over spatial "cells"

![[Pasted image 20240605175141.png|400]]

| Non-Invariant   | Invariant               |
| --------------- | ----------------------- |
| Rotation, Scale | Deformation, Traslation |
Computationally expensive.
### Orientation normalization
use the dominant (strongest gradient) image gradient direction to normalize its orientation (of the patch, so that this gradient direction is vertical or horizontal)

![[Pasted image 20240605175821.png|400]]

Changes in lighting affect the intensity and spectral composition, sensible to light changes.

## Histogram Comparison

This is a sequence of method to compare histograms.

#### Histogram Intersection
Normalized histograms:
$$
\cap(Q, V) =  \sum_{i} \min(q_i, v_i)

$$
Non-normalized histograms
$$
\cap(Q, V) = \frac{1}{2} \left( \frac{\sum_{i} \min(q_i, v_i)}{\sum_{i} q_i} + \frac{\sum_{i} \min(q_i, v_i)}{\sum_{i} v_i} \right)

$$
where $Q$ and $V$ represent the histograms, and for each we take the $i^{th}$ bin of that histogram.
This measure quantifies the commonality between two histograms, effectively determining how similar two images are based on their color or feature distributions. It may not adequately capture differences in spatial distribution of features. It is also susceptible to variations in image exposure and lighting conditions that can significantly alter the histograms.

#### Euclidean distance

$$
d(Q, V) = \sum_{i} (q_i - v_i)^2
$$

The range is from 0 to infinity, where 0 indicates identical histograms and higher values indicate greater dissimilarity. Each bin contributes equally to the total distance, regardless of its relative importance or the statistical distribution within the histograms. This can sometimes lead to less *discriminative comparisons*, especially if certain histogram bins are more significant than others in the context of the application.

#### Chi-square
$$
\chi^2(Q, V) = \sum_{i} \frac{(q_i - v_i)^2}{q_i + v_i}
$$
The Chi-square test has a strong statistical foundation, providing a way to test if two distributions are statistically different from each other. The Chi-square value ranges from 0 to infinity, where 0 indicates no difference between the histograms and higher values suggest greater disparity.
The Chi-square test requires a sufficient number of samples in each histogram bin to be valid, which may not always be practical in images with limited color diversity or in smaller images.

## HOG descriptor

HOG stands for "Histogram of Oriented Gradients". It used for object detection. How to extract HOG descriptors:

>[!Algorithm]
>1. Image Pre-processing: the image patch (subpart of the image) is normalized to a 1:2 proportion (64x128)
>2. Gradient calculation (angles and magnitude)
>3. Histogram of Oriented Gradients in Cells
>4. Block Normalization


The angles are unsigned: from 0 to 180
The histogram captures the predominant directions of the gradients.

![[Pasted image 20240605183616.png|400]]

Each pixel votes in the histogram bin based on its gradient magnitude. This vote is distributed between bins when the gradient direction does not align exactly with a bin center.
We ends up with a 9-bin histogram.

Using a 16x16 Block Normalization, meaning we take 4 times 8x8 blocks, and a **L2 Norm** (classic orthonormalization of a vector) we prevent light variations. The 16x16 block has 4 histograms, concatenated in 36x1 element vector. The window is then moved by 8 pixels and the process is repeated.

>[!example]
>This is a 8x8 block of an image
>$$
>\begin{bmatrix}
>52 & 55 & 61 & 66 & 70 & 61 & 64 & 73 \\
>63 & 59 & 55 & 90 & 109 & 85 & 69 & 72 \\
>62 & 59 & 68 & 113 & 144 & 104 & 66 & 73 \\
>63 & 58 & 71 & 122 & 154 & 106 & 70 & 69 \\
>67 & 61 & 68 & 104 & 126 & 88 & 68 & 70 \\
>79 & 65 & 60 & 70 & 77 & 68 & 58 & 75 \\
>85 & 71 & 64 & 59 & 55 & 61 & 65 & 83 \\
>87 & 79 & 69 & 68 & 65 & 76 & 78 & 94 \\
>\end{bmatrix}
>$$
>$G_x$[0,0] = 55 - 52 = 3
>$G_y$[0,0] = 63 - 52 = 11
>
>Magnitude[0,0] = $sqrt(G_x^2 + G_y^2) = 11.4$
>Orientation[0,0] = $atan2(G_y, G_x) * (180 / \pi) = 74.5$  (in degrees, range 0-180 for unsigned gradients)
>
>
>
>|               |     |     |     |                     |                     |     |
>| ------------- | --- | --- | --- | ------------------- | ------------------- | --- |
>| **Magnitude** |     |     |     | $(80-74.5)/20*11.4$ | $(74.5-60)/20*11.4$ |     |
>| **Bin**       | 0   | 20  | 40  | 60                  | 80                  | ... |
>
>After we filled this, we need to fill another 3 8x8, and then apply a normalization over the 16x16 overall block.





$\text{Magnitude Contribution} = \left(\frac{\text{Distance to Opposite Bin}}{\text{Total Interval}}\right) \times \text{Total Magnitude}$

```slide-note
file: Features2.pdf
page: 29
scale: 0.8
```

