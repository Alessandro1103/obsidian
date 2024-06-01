Date: 2024-05-28
Time: 11:37
Tags:
Up: 

---
# Formulario Computer Vision

## Point Processing

**Gamma Correction**
$$
V_{out} = AV_{in}^{\gamma} 
$$
**Histogram Equalization**
$$
\begin{align*}
& p(r)=\frac{\text{Number of pixels with intensity r}}{\text{Total number of pixels}} \\
& T(r) = \text{round}\bigg(255 \sum_{i=0}^r p(i)\bigg) & 0\leq r \leq 255 \\
\end{align*}
$$
## Filtering

**Cross-Correlation and Convolution**
$$
\begin{align*}
& G[i, j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u, v] F[i + u, j + v] & G = H \otimes F \\
& G[i, j] = \sum_{u=-k}^{k} \sum_{v=-k}^{k} H[u, v] F[i - u, j - v] 
& G = H * F
\end{align*}
$$
**Padding & Stride**
$$
O = \left\lfloor \frac{I + 2P - K}{S} \right\rfloor + 1
$$
**Gaussian Kernel**
$$
G_\sigma = \frac{1}{2 \pi \sigma^2} e^{-\frac{x^2 + y^2}{2 \sigma^2}}
$$
**Bilateral Filter**
$$
h[m, n] = \frac{1}{W_{mn}} \sum_{k, l} g[k, l] r_{mn}[k, l] f[m + k, n + l]
$$
**Thresholding**
$$
g(m, n) = \begin{cases} 255, & \text{if } f(m, n) > A \\ 0, & \text{otherwise} \end{cases}
$$
## Sampling and 