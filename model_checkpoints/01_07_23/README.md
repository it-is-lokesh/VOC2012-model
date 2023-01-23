# Training results

In todays model, we have used more dropout layers and higher dropout rate than yesterday as shown. 

Model:
```
model = tf.keras.Sequential([
    Conv2D(32, kernel_size=(5,5), padding='valid', activation='relu', input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.2),

    Conv2D(64, kernel_size=(5,5), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.3),

    Conv2D(128, kernel_size=(3,3), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.5),
    
    Conv2D(256, kernel_size=(3,3), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.5),

    Flatten(),
    Dense(128, activation='relu'),
    Dropout(rate=0.4),
    Dense(64, activation='relu'),
    Dropout(rate=0.2),
    Dense(20, activation='sigmoid')
])
```
After continuing the iterations, we find that the training loss and validation loss now are kind of following each other, though there are fluctuations in validation loss.

- Task for tomorrow: Continue the simulation until the training loss is decreasing.