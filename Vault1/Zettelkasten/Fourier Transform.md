Date: 2024-06-02
Time: 17:21
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Fourier Transform

> [!quote] 
> Any univariate function can be rewritten as a weighted sum of sines and cosines of different frequencies.

## Fourier Analysis (1D)

General formula:
$$
A \,\sin(\omega x+ \phi)
$$
To analyse the frequency inside of a signal is often used the *frequency spectrum graph*: it visualizes the different frequencies present in a signal and their respective amplitudes or intensities. In the horizontal axis we have the different frequency, and in the vertical axis the amplitude of each frequency component. In the x=0 is shown the signal average


```slide-note
file: FourierTransform.pdf
page: 14
scale: 0.8
```

For pure tones, such as the sine wave, the frequencies are distinct.
For more complex signals, more frequencies are involved.
In the case of random noise, there is a wide range of frequencies.

```slide-note
file: FourierTransform.pdf
page: 21
scale: 0.8
```

The DFT is a mathematical technique used to transform a sequence of data points in the time domain into components in the frequency domain. The DFT can also be represented as a matrix multiplication, which is a more computationally straightforward interpretation for implementations. Each row of $W$ corresponds to a frequency $k$, and each column corresponds to a time index $x$. The matrix product then calculates the contribution of each time-domain sample to each frequency-domain component.

```slide-note
file: FourierTransform.pdf
page: 28
scale: 0.8
```

## Fourier Analysis (2D)


```slide-note
file: FourierTransform.pdf
page: 30
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 33
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 35
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 36
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 37
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 39
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 40
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 41
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 42
scale: 0.8
```

Amplitude doesn't carry the image information. Infact the phase is one that contains image information and is very important for reconstruction.

![[Pasted image 20240602190536.png|200]]

Convolution in the spatial or time domain is equivalent to multiplication in the frequency domain, and vice versa.

```slide-note
file: FourierTransform.pdf
page: 45
scale: 0.8
```

$h(x,y)$ is the Gaussian Filter

```slide-note
file: FourierTransform.pdf
page: 46
scale: 0.8
```

The result we obtain is the same:
```slide-note
file: FourierTransform.pdf
page: 47
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 49
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 50
scale: 0.8
```

The Box Blur uses a simple averaging filter where each pixel in the output image is the average of its neighbouring pixels within a square (box-shaped) window. This tends to give a uniformly blurred effect.
Box Blur is computationally simpler and faster to compute, especially with integer calculations or in hardware. It may be preferred in real-time applications where speed is more critical than visual quality.

Gaussian Blur uses a Gaussian function to weigh the neighbouring pixels, which results in a smoother and more natural blurring effect. Pixels closer to the center of the kernel have more influence than those further away.
Gaussian Blur is preferred in applications where image quality is paramount, such as in photography processing, graphics design, and areas where a smoother blur is required to simulate out-of-focus effects.
## Revisiting Sampling

```slide-note
file: FourierTransform.pdf
page: 67
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 68
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 69
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 70
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 71
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 72
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 73
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 74
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 75
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 76
scale: 0.8
```

```slide-note
file: FourierTransform.pdf
page: 77
scale: 0.8
```




** Process exited - Return Code: 0 **
Press Enter to exit terminal

