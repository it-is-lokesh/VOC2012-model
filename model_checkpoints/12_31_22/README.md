# Training results (12/31/2022)

These weights are being optimized using a simple learning model shown below.
``` 
model = tf.keras.Sequential([
    Conv2D(32, kernel_size=(5,5), padding='valid', activation='relu', input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    
    Conv2D(64, kernel_size=(5,5), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Conv2D(128, kernel_size=(3,3), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    
    Conv2D(128, kernel_size=(3,3), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Flatten(),
    Dense(128, activation='relu'),
    Dense(64, activation='relu'),
    Dense(20, activation='sigmoid')
])
```
We observe that though the training loss decreases with the #iterations, the validation set loss takes a U shape curve, meaning it decreases until a few iterations and then increases. This means the model is moving towards overfitting or high variance. We also need to keep in mind that the training and validation datasets come from the same distribution.