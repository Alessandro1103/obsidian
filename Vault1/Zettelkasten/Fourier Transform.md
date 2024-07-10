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


![[Pasted image 20240621223313.png|400]]

For *pure tones*, such as the sine wave, the frequencies are distinct.
For more *complex signals*, more frequencies are involved.
In the case of *random noise*, there is a wide range of frequencies.

![[Pasted image 20240621223335.png|400]]

The DFT is a mathematical technique used to transform a sequence of data points in the time domain into components in the frequency domain. The DFT can also be represented as a matrix multiplication, which is a more computationally straightforward interpretation for implementations. Each row of $W$ corresponds to a frequency $k$, and each column corresponds to a time index $x$. The matrix product then calculates the contribution of each time-domain sample to each frequency-domain component.

![[Pasted image 20240621223359.png|500]]
## Fourier Analysis (2D)

![[Pasted image 20240621223423.png|400]]

![[Pasted image 20240621223444.png|400]]

![[Pasted image 20240621223507.png|400]]

![[Pasted image 20240621223526.png|400]]

![[Pasted image 20240621223545.png|400]]

![[Pasted image 20240621223603.png|400]]

![[Pasted image 20240621223619.png|400]]

![[Pasted image 20240621223642.png|400]]

![[Pasted image 20240621223700.png|400]]

Amplitude doesn't carry the image information. Infact the phase is one that contains image information and is very important for reconstruction.

![[Pasted image 20240602190536.png|200]]

Convolution in the time domain is equivalent to multiplication in the frequency domain, and vice versa.

![[Pasted image 20240621223721.png|400]]

$h(x,y)$ is the Gaussian Filter

![[Pasted image 20240621223740.png|400]]

The result we obtain is the same:
![[Pasted image 20240621223800.png|400]]

**Gaussian Blur**:
![[Pasted image 20240621223835.png|350]]

**Box Blur**:
![[Pasted image 20240621223851.png|350]]

The Box Blur uses a simple averaging filter where each pixel in the output image is the average of its neighbouring pixels within a square (box-shaped) window. This tends to give a uniformly blurred effect.
Box Blur is computationally simpler and faster to compute, especially with integer calculations or in hardware. It may be preferred in real-time applications where speed is more critical than visual quality.

Gaussian Blur uses a Gaussian function to weigh the neighbouring pixels, which results in a smoother and more natural blurring effect. Pixels closer to the center of the kernel have more influence than those further away.
Gaussian Blur is preferred in applications where image quality is paramount, such as in photography processing, graphics design, and areas where a smoother blur is required to simulate out-of-focus effects.
## Revisiting Sampling

The Nyquist-Shannon theorem in relation to the Gaussian pyramid underscores the importance of adequate sampling to avoid aliasing. Gaussian blurring, applied as a low-pass filter, helps reduce the signal's highest frequencies, ensuring that the sampling frequency remains above twice the highest frequency present in the image to prevent aliasing. The cutoff frequency for blurring is tied to the filter's standard deviation, and selecting an appropriately sized mask ensures the Gaussian filter effectively encompasses significant data, minimizing edge effects.

## Hybrid Images


![[Pasted image 20240621223923.png|400]]

![[Pasted image 20240621223939.png|400]]
