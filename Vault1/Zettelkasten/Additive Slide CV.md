Date: 2024-06-17
Time: 17:47
Tags:
Up: 

---
# Additive Slide CV

In this documents I am going to write some topics that could be relevant from packs of slides that I ignored during the study of the exam:

## Bag-of-Words

The "Bag of Words" (BoW) model is a simplified representation used in both natural language processing and computer vision. It involves breaking down text or visual information into parts, treating each element as an isolated unit without considering the order or structure in which they appear.

- In the realm of natural language processing, BoW models transform documents into vectors of word counts. The idea is to represent documents as the frequency of their words, disregarding grammar and word order but maintaining multiplicity.
- Similarly, in computer vision, BoW models are used to break down images into collections of "visual words." This process involves identifying key features or patterns in images and treating them as discrete, quantifiable elements.

>[!algorithm]
>1. **Feature extraction**
>2. **Learn Visual Vocabulary**, cluster the extracted features 
>3. **Quantize Features**, assign each feature in new images to the nearest visual word in the vocabulary
>4. **Create Histograms**, how many times a visual world appears in the image
>5. **Train Classifier**, use histograms to train a classifier


Deep learning models can learn hierarchical features automatically from data, from low-level features in initial layers to high-level semantic features in deeper layers.

