Date: 2024-06-02
Time: 23:03
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Features

We can have:
- **Global Features**: are attributes that generalize the entire object within an image
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

1. **Object Recognition**: Identifying and labelling objects within an image. Feature detection helps in distinguishing objects based on their distinct characteristics such as shape, texture, and color.

2. **Localization and Mapping**: Essential in robotics and autonomous vehicle navigation, this process involves determining the position of the device relative to its environment and constructing a map of the surrounding area using detected features.

3. **3D Reconstruction**: Creating three-dimensional models from two-dimensional images. Features detected across multiple images are used to infer the depth and structure of the scene, building a spatial representation.

4. **Augmented Reality**: Enhancing the real world with digital overlays. Feature detection allows the AR system to understand the environment and accurately place digital objects in real-world contexts.

5. **Image Matching (hard situation, SIFT features matching)**: Comparing and aligning different images based on detected features, even under challenging conditions such as changes in scale, orientation, and lighting. SIFT (Scale-Invariant Feature Transform) is a robust method for matching features across varied scenarios.
## What is good feature

```slide-note
file: Features.pdf
page: 21
scale: 0.8
```

```slide-note
file: Features.pdf
page: 22
scale: 0.8
```

```slide-note
file: Features.pdf
page: 23
scale: 0.8
```

```slide-note
file: Features.pdf
page: 24
scale: 0.8
```

```slide-note
file: Features.pdf
page: 25
scale: 0.8
```

```slide-note
file: Features.pdf
page: 26
scale: 0.8
```

```slide-note
file: Features.pdf
page: 27
scale: 0.8
```

```slide-note
file: Features.pdf
page: 28
scale: 0.8
```

```slide-note
file: Features.pdf
page: 29
scale: 0.8
```

```slide-note
file: Features.pdf
page: 30
scale: 0.8
```

```slide-note
file: Features.pdf
page: 31
scale: 0.8
```

```slide-note
file: Features.pdf
page: 32
scale: 0.8
```

```slide-note
file: Features.pdf
page: 33
scale: 0.8
```

```slide-note
file: Features.pdf
page: 34
scale: 0.8
```

```slide-note
file: Features.pdf
page: 35
scale: 0.8
```

```slide-note
file: Features.pdf
page: 36
scale: 0.8
```

```slide-note
file: Features.pdf
page: 37
scale: 0.8
```

```slide-note
file: Features.pdf
page: 38
scale: 0.8
```

```slide-note
file: Features.pdf
page: 39
scale: 0.8
```

```slide-note
file: Features.pdf
page: 40
scale: 0.8
```

```slide-note
file: Features.pdf
page: 41
scale: 0.8
```

```slide-note
file: Features.pdf
page: 42
scale: 0.8
```

```slide-note
file: Features.pdf
page: 43
scale: 0.8
```

```slide-note
file: Features.pdf
page: 44
scale: 0.8
```

```slide-note
file: Features.pdf
page: 45
scale: 0.8
```

```slide-note
file: Features.pdf
page: 46
scale: 0.8
```

```slide-note
file: Features.pdf
page: 47
scale: 0.8
```

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

```slide-note
file: Features.pdf
page: 50
scale: 0.8
```

```slide-note
file: Features.pdf
page: 51
scale: 0.8
```

```slide-note
file: Features.pdf
page: 52
scale: 0.8
```

```slide-note
file: Features.pdf
page: 53
scale: 0.8
```

```slide-note
file: Features.pdf
page: 54
scale: 0.8
```

```slide-note
file: Features.pdf
page: 55
scale: 0.8
```

```slide-note
file: Features.pdf
page: 56
scale: 0.8
```

```slide-note
file: Features.pdf
page: 57
scale: 0.8
```

```slide-note
file: Features.pdf
page: 58
scale: 0.8
```

```slide-note
file: Features.pdf
page: 59
scale: 0.8
```

```slide-note
file: Features.pdf
page: 60
scale: 0.8
```

```slide-note
file: Features.pdf
page: 61
scale: 0.8
```

```slide-note
file: Features.pdf
page: 62
scale: 0.8
```

```slide-note
file: Features.pdf
page: 63
scale: 0.8
```

```slide-note
file: Features.pdf
page: 64
scale: 0.8
```

```slide-note
file: Features.pdf
page: 65
scale: 0.8
```

```slide-note
file: Features.pdf
page: 66
scale: 0.8
```

```slide-note
file: Features.pdf
page: 67
scale: 0.8
```

```slide-note
file: Features.pdf
page: 68
scale: 0.8
```

```slide-note
file: Features.pdf
page: 69
scale: 0.8
```

```slide-note
file: Features.pdf
page: 70
scale: 0.8
```

```slide-note
file: Features.pdf
page: 71
scale: 0.8
```

```slide-note
file: Features.pdf
page: 72
scale: 0.8
```

```slide-note
file: Features.pdf
page: 73
scale: 0.8
```

```slide-note
file: Features.pdf
page: 74
scale: 0.8
```

```slide-note
file: Features.pdf
page: 75
scale: 0.8
```

```slide-note
file: Features.pdf
page: 76
scale: 0.8
```

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

```slide-note
file: Features.pdf
page: 80
scale: 0.8
```

```slide-note
file: Features.pdf
page: 81
scale: 0.8
```

```slide-note
file: Features.pdf
page: 82
scale: 0.8
```

```slide-note
file: Features.pdf
page: 83
scale: 0.8
```

```slide-note
file: Features.pdf
page: 84
scale: 0.8
```

```slide-note
file: Features.pdf
page: 85
scale: 0.8
```

```slide-note
file: Features.pdf
page: 86
scale: 0.8
```

```slide-note
file: Features.pdf
page: 87
scale: 0.8
```

```slide-note
file: Features.pdf
page: 88
scale: 0.8
```

```slide-note
file: Features.pdf
page: 89
scale: 0.8
```

```slide-note
file: Features.pdf
page: 90
scale: 0.8
```

```slide-note
file: Features.pdf
page: 91
scale: 0.8
```

```slide-note
file: Features.pdf
page: 92
scale: 0.8
```

```slide-note
file: Features.pdf
page: 93
scale: 0.8
```

```slide-note
file: Features.pdf
page: 94
scale: 0.8
```

```slide-note
file: Features.pdf
page: 95
scale: 0.8
```

```slide-note
file: Features.pdf
page: 96
scale: 0.8
```

```slide-note
file: Features.pdf
page: 97
scale: 0.8
```

```slide-note
file: Features.pdf
page: 98
scale: 0.8
```

```slide-note
file: Features.pdf
page: 99
scale: 0.8
```

```slide-note
file: Features.pdf
page: 100
scale: 0.8
```

```slide-note
file: Features.pdf
page: 101
scale: 0.8
```




** Process exited - Return Code: 0 **
Press Enter to exit terminal