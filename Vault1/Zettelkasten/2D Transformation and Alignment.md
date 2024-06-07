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


```slide-note
file: TransformationAlignment.pdf
page: 14
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 15
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 16
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 17
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 18
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 19
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 20
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 21
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 22
scale: 0.8
```

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

```slide-note
file: TransformationAlignment.pdf
page: 26
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 27
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 28
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 29
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 30
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

```slide-note
file: TransformationAlignment.pdf
page: 33
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 34
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 35
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 36
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 37
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 38
scale: 0.8
```

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

```slide-note
file: TransformationAlignment.pdf
page: 43
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 44
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 45
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 46
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 47
scale: 0.8
```

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

```slide-note
file: TransformationAlignment.pdf
page: 50
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 51
scale: 0.8
```

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

```slide-note
file: TransformationAlignment.pdf
page: 58
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 59
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 60
scale: 0.8
```

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

```slide-note
file: TransformationAlignment.pdf
page: 63
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 64
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 65
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 66
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 67
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 68
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 69
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 70
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 71
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 72
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 73
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 74
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 75
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 76
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 77
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 78
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 79
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 80
scale: 0.8
```

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

```slide-note
file: TransformationAlignment.pdf
page: 86
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 87
scale: 0.8
```

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
page: 90
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 91
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

```slide-note
file: TransformationAlignment.pdf
page: 94
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 95
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 96
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 97
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 98
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 99
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 100
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 101
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 102
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 103
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 104
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 105
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 106
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 107
scale: 0.8
```

```slide-note
file: TransformationAlignment.pdf
page: 108
scale: 0.8
```




** Process exited - Return Code: 0 **
Press Enter to exit terminal