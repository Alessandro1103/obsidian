Date: 2023-12-28
Time: 17:25
Tags:
Up: 

---
# Homework2 (cose da aggiungere)

Modello 1 and 2 are ready, I can start to provide description of the model 1 I would say. I could still improve both files, changing some hypervalues.

When I had to create a first model of training for the CNN i added in this sequence:
- Flatten(input_shape=(96, 96, 3)),
- Dense(64, activation='relu'),
- Dense(32, activation='relu'),
- Dense(len(class_names), activation='softmax')

with the compile parameters:
- optimizer='adam',
- loss=tf.keras.losses.categorical_crossentropy,
- metrics=['accuracy']

with data Augmentation:
- train_datagen = ImageDataGenerator(rescale=1./255)
- test_datagen = ImageDataGenerator(rescale=1./255)

with evaluation:
- Test Loss: 1.1776816844940186 
- Test Accuracy: 0.5587486624717712

``` 
What to do
	1. **Input Layer:**
	    
	    - Purpose: To receive the input images.
	    - Structure: Usually defined implicitly by the `input_shape` parameter in the first layer of the model.
	2. **Convolutional Layers (Conv2D):**
	    
	    - Purpose: To extract features from the input image. Convolutional layers apply a number of filters to the input, which can capture various aspects of the image, such as edges, textures, or more complex patterns in deeper layers.
	    - Structure: Often start with a smaller number of filters and increase in deeper layers. For example, start with 32 filters, then 64 in the next Conv2D layer, and so on.
	3. **Activation Function (ReLU):**
	    
	    - Purpose: To introduce non-linearity into the model, allowing it to learn more complex patterns.
	    - Structure: Often used immediately after each Conv2D layer. ReLU (Rectified Linear Unit) is a common choice due to its simplicity and efficiency.
	4. **Pooling Layers (MaxPooling2D):**
	    
	    - Purpose: To reduce the spatial dimensions (width, height) of the input volume for the next convolutional layer. It helps reduce the computational load, memory usage, and also helps reduce overfitting.
	    - Structure: Typically follow one or more Conv2D layers. Max pooling is a common choice, where the maximum element is selected in a window (e.g., 2x2).
	5. **Dropout:**
	    
	    - Purpose: To reduce overfitting by randomly setting a fraction of input units to 0 at each update during training.
	    - Structure: Can be used after pooling layers or fully connected layers. Common dropout rates are between 0.2 and 0.5.
	6. **Flattening:**
	    
	    - Purpose: To convert the 2D feature maps into a 1D feature vector, making it possible to connect to a fully connected layer (Dense layer).
	    - Structure: Used once after the final pooling or Conv2D layer to flatten the output for the Dense layers.
	7. **Fully Connected Layers (Dense):**
	    
	    - Purpose: To perform classification based on the features extracted and pooled by the convolutional and pooling layers. The last Dense layer has the number of neurons equal to the number of classes and usually uses the softmax activation function for multi-class classification.
	    - Structure: Often, one or more Dense layers are used. The first Dense layer may have a relatively high number of neurons (e.g., 128 or 256) and is followed by the output Dense layer.
	8. **Output Layer:**
	    
	    - Purpose: To produce the final classification output.
	    - Structure: A Dense layer with the number of neurons equal to the number of classes. For multi-class classification, the softmax activation function is typically used.
```

<<<<<<< HEAD
For the new model the F1 metrics, had to be done in separate way because there was no module by default.


In the second model:
In questa versione, ho utilizzato kernel più piccoli e ho inserito blocchi di connessioni residue (simili a quelli trovati in architetture come ResNet) per aiutare a prevenire la scomparsa dei gradienti durante l'addestramento. Inoltre, ho ridotto il numero e la dimensione dei layer densi per limitare l'overfitting e ho aumentato il tasso di dropout per la stessa ragione. Ho anche utilizzato una stride più piccola nei layer convoluzionali per preservare più informazioni spaziali.

=======
Nella simulazione 1, seria, quei picchi potevano sembrare o sono effettivamente overfitting


>>>>>>> origin/main
---
# References
