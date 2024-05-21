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
page: 7
scale: 0.8
```

