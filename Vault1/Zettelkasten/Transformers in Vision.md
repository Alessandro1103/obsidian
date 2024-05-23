Date: 2024-05-07
Time: 10:16
Tags: #ComputerVision #Università
Up: [[Computer Vision]] 

---
# Transformers in Vision

## Introduction

This is a schematic of a Transformer model architecture, starting from the bottom here is a detailed description of the components:
1. **Inputs**: raw data (like text or images).
2. **Input Embedding**: the inputs are converted into a format that model can work with more effectively, typically a high-dimensional space where similar inputs are closer together.
3. **Positional Encoding**: are added to the input embeddings to provide the model with information about the order of the input elements.
4. **Encoder/Decoder**: the left box represents the encoder, that processes the input data and converts it into a set of feature vectors that capture the essence of the input. The right box represents the decoder, that generate output data based on the encoded information and any part of the output that has already been generated.
5. **Multi-Head Attention**: this allows the model to focus on different positions of the input sequence, important for understanding complex dependencies:
	- **Masked Multi-Head Attention**: used primarily in the decoder part of the transformer to ensure predictions for a sequence position can only depend on known outputs at earlier positions.
	- **Multi-Head Attention**: in both encoder and decoder, facilitating the model to attend to all positions of the sequence simultaneously.
6. **Add and Normalization**: it's a feedforward operation, the results are added to the input of each sub-layer and normalized. This helps in stabilizing the learning process.
7. **Feed Forward**: a feed-forward neural network is applied to each position separately and identically. This layer transforms the data internally to better capture complex relationships.
8. **Nx**: This denotes that the blocks are repeated "N" times.
9. **Output Embedding and Positional Encoding**: Similar to the input side but typically used in the decoder to generate the final result.
10. **Linear Layer and Softmax**: the output is transformed into a final output space, and the softmax function is applied to turn logits into probabilities for each class of word.


```slide-note 
file: Transformers in Vision2.pdf 
page: 7,8
scale: 0.8
```

Focus on fact that the Queries are taken from Target, which are used to search through the keys to retrieve the most relevant values. The Keys and Values are taken from the Source, these are vector representations that capture the semantic and contextual nuances of each world.

```slide-note 
file: Transformers in Vision2.pdf 
page: 9,10,11
scale: 0.8
```

### Self attention

```slide-note 
file: Transformers in Vision2.pdf 
page: 12,13,14,15,16,17,18,19,20,21
scale: 0.8
```

```slide-note 
file: Transformers in Vision2.pdf 
page: 22
scale: 0.8
```
The key advantage of multi-head attention is that it allows the model to consider different parts of the input sequence from multiple perspectives simultaneously. This ability to focus on various aspects of the sequence in parallel helps the Transformer model capture a more nuanced and complete representation of the input data, leading to improved performance on tasks like translation, text generation, and more.


### Multi Head attention

```slide-note 
file: Transformers in Vision2.pdf 
page: 23,24,25,26,27
scale: 0.8
```

### Positional Encoding

```slide-note 
file: Transformers in Vision2.pdf 
page: 28,29
scale: 0.8
```

### The residuals

```slide-note 
file: Transformers in Vision2.pdf 
page: 30
scale: 0.8
```

### The encoder

```slide-note 
file: Transformers in Vision2.pdf 
page: 31
scale: 0.8
```

### Conclusions

```slide-note 
file: Transformers in Vision2.pdf 
page: 32,33,34,35
scale: 0.8
```


## Why self attention for vision?

```slide-note 
file: Transformers in Vision2.pdf 
page: 39,40
scale: 0.8
```

### How do we design vision attention models?

```slide-note 
file: Transformers in Vision2.pdf 
page: 45,46,48,49,50,51,52,54,55,56,61,62
scale: 0.8
```

## Takeaways

```slide-note 
file: Transformers in Vision2.pdf 
page: 91
scale: 0.8
```
