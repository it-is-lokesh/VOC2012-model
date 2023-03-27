For the same model as yesterday, the output activation has been replaced with softmax instead of sigmoid activation. 

Model:
```
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
    Dense(20, activation=softmax)
])
# Learning rate = 0.001
# Minimum delta forsSaturation = 0.02 (loss)
```

With the sigmoid activation, the model acheived saturation (in terms of loss) earlier than the one with softmax activation. Also with the softmax activation, the training accuracy is higher after the saturation than the one with softmax activation.

In the next model, we increase the complexity of the densely connected layers.

Model:
```
model = tf.keras.Sequential([
    Conv2D(4, kernel_size=(5,5), padding='valid', activation=leaky_relu, input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.2),

    Conv2D(2, kernel_size=(5,5), padding='valid', activation=leaky_relu),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.3),

    Flatten(),
    Dense(128, activation=leaky_relu),
    Dropout(rate=0.4),
    Dense(64, activation=leaky_relu),
    Dropout(rate=0.2),
    Dense(20, activation=softmax)
])
```
Even in this model, the accuracy is hardly able to increase above 49%.

In the next model, we increase the number of layers in CNN with some changes in the dropout rates as shown below.
Model:
```
model = tf.keras.Sequential([
    Conv2D(8, kernel_size=(5,5), padding='valid', activation=leaky_relu, input_shape=(128,128,3)),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.5),

    Conv2D(4, kernel_size=(5,5), padding='valid', activation=leaky_relu),
    MaxPooling2D(pool_size=(2,2), padding='valid'),
    Dropout(rate=0.3),

    Flatten(),
    Dense(128, activation=leaky_relu),
    Dropout(rate=0.2),
    Dense(64, activation=leaky_relu),
    Dropout(rate=0.1),
    Dense(20, activation=softmax)
])
```

In this model, the loss is gradually decreasing initially as well as the accuracy is steadily increasing. This means that the model is not underfitting the parameters. We observe that though the validation accuracy follows the training accuracy, the losses do not.  