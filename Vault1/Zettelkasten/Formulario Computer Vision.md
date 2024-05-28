Date: 2024-05-28
Time: 11:37
Tags:
Up: 

---
# Formulario Computer Vision

## Image Processing

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
