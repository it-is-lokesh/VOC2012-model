Todays first training model is as follows:

Model:
```
model = tf.keras.Sequential([
    Conv2D(4, kernel_size=(5,5), padding='valid', activation='relu', input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Conv2D(2, kernel_size=(5,5), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),

    Flatten(),
    Dense(128, activation='relu'),
    Dropout(rate=0.4),
    Dense(64, activation='relu'),
    Dropout(rate=0.2),
    Dense(20, activation='sigmoid')
])
```

Through this model, the training has acheived 75% accuracy quickly but there was a lot of bias, due to overfitting. Hence the next model is more simplified.

Model:
```
model = tf.keras.Sequential([
    Conv2D(4, kernel_size=(5,5), padding='valid', activation='relu', input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.2),

    Conv2D(2, kernel_size=(5,5), padding='valid', activation='relu'),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.3),

    Flatten(),
    Dense(64, activation='relu'),
    Dropout(rate=0.2),
    Dense(20, activation='sigmoid')
])
```

Now the model is underfitting, and we need to make a more robust model. The accuracy is hardly increasing above 45%. Interesting thing to note here is that the second model has half the number of training parameters but still the training time is the same as the first. The model is further showing some bias, but better than the first model.


Model:
```
leaky_relu = tf.keras.layers.LeakyReLU(alpha=0.3)
relu = tf.keras.layers.ReLU()

model = tf.keras.Sequential([
    Conv2D(4, kernel_size=(5,5), padding='valid', activation=leaky_relu, input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.2),

    Conv2D(2, kernel_size=(5,5), padding='valid', activation=leaky_relu),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.3),

    Flatten(),
    Dense(64, activation=leaky_relu),
    Dropout(rate=0.4),
    Dense(20, activation='sigmoid')
])
```

By using leaky relu activation, the model has acheived convergence quicker than the one which uses relu (10 epochs faster in this case).
For the same model as shown above, the activation threshold ReLU didn't show any significant result (maybe it is used elsewhere).
For the same model as shown above with learning rate increased from 0.001 to 0.1, initially the loss was reducing significantly but there was no change in the accuracy of the training as well as validation data. Later the loss overshooted to something in the order of 10^5, which means that the learning rate is too high.

Quick result - Since the loss function is logarithimic, for a linear decrease in the accuracy, the loss should reduce exponentially.