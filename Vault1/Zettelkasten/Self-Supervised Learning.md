Date: 2024-05-07
Time: 11:09
Tags: #ComputerVision #Università 
Up: [[Computer Vision]]

---
# Self-Supervised Learning

Data annotation is one of the main problem in Deep Learning, and in general in AI.

![[Screenshot from 2024-05-07 11-10-46.png|300]]

The time increase in complex problems, there could be some errors:
- **Fine-grained recognition**: 
- **Class unawareness**: 
- **Insufficient training data**: small amount of data.

Rare concepts:
![[Screenshot from 2024-05-07 11-15-23.png|400]]


![[Screenshot from 2024-05-07 11-16-38.png]]

In case like this the annotation time is 90 minutes per image, with multiple annotators
So has become pretty likely that dataset are now sintetic, like stereo modepth and Optical Flow, which can be difficult task for humans:![[Screenshot from 2024-05-07 11-18-13.png]]


## In the context of Computer Vision

we watn to obtain the label from the data itself, extracting a property, that can help me classify it.

The task can be multimple:
- Predict anu part of the input form any other part
- Predict the future form the past
- Predict the future from the recent past
- Predict the past from the present
- Predict the top from the bottom
- Predict the occluded from the visible

An usage made for Supervised learning is to correct a corrupted version. After training, only the encoder is kept and the decoder is thrown away. This can be used for an another type of classification or maybe in other datasets.

![[Screenshot from 2024-05-07 11-21-48.png|500]]

Self-supervise learning learn model parameters using dataset of data-data pairs $\{x_i,x_i'\}^N_{i=1}$, like for example self sepervised stereo/flow, contrastive learning.


## Task-specific Models

### Unsupervised Learning of Depth and Ego-Motion

![[Screenshot from 2024-05-07 11-28-13.png|500]]

train CNN to jointly predict depth and relative pose from three video frames. 

![[Screenshot from 2024-05-07 11-31-49.png|450]]

Traditional U-Net with multi-scale prediction/loss. Final objective includes photoconsistency, smoothness. 