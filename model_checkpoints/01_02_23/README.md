# Training results

In our second day training, we have used the same model as previous day but normalized the training data.

Model:
```
model = tf.keras.Sequential([
    Conv2D(32, kernel_size=(5,5), padding='valid', activation='relu', input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Conv2D(64, kernel_size=(5,5), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Conv2D(128, kernel_size=(3,3), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.3),
    
    Conv2D(128, kernel_size=(3,3), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Flatten(),
    Dense(128, activation='relu'),
    Dropout(rate=0.2),
    Dense(64, activation='relu'),
    Dense(20, activation='sigmoid')
])
```
We observe the similar U shape curve for validation loss, but we can notice that the validation loss follows the training loss better than the previous cases.

- Task for tomorrow: Increase the dropout value of the existing dropout layers and note the results.