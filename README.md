# Training VOC 2012 Dataset

This project is an attempt to understand how the model architecture is affecting the accuracy of the model. I have made all the documentation clear to let the learners get a better intuition on CNNs.

The dataset is a collection of 17125 images divided into 20 classes. 
The results and discussion for each training model have been included in the "model_checkpoints" folder according to the date it was being trained. Hope this documentation helps you get a clear idea of how to work on Computer Vision projects. Comments are welcomed :)

Link to download dataset: http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar <br>
For more information regarding the dataset, refer http://host.robots.ox.ac.uk/pascal/VOC/voc2012/ <br>

Note: The folder naming format in the model_checkpoints forder is MM_DD_YY.

### Important Results concluded
#### (i) Normalization and dropout experiments:
- Using normalization over the data allows the model to acheive better accuracy and smooth training curve, whereas without the normalization applied, the validation accuracy suffers from uncertainity. In other works, the model acheives more confidence upon normalization.
- We have run the iterations with and without using dropout, and noticed that the accuracy gets saturated after certain #iterations. This can be explained as the modle gets overfitted without using the dropout layers.
- Dropout serves as a good method to reduce overfitting, and allows the model to have multiple 'trigger' perceptrons for a similar set of features in the input image. This simply allows the model to perform better on a completely different dataset.
- Since we are optimizing on the training data, though the validation loss deviates from the training loss, the performance of the model over training and validation data remains the same (or say almost the same).

#### (ii) Activation functions and learning rates:
- We generally do not use tanh and sigmoid activations for the hidden layers, rather they are suitable for the output layers. They are also used in LSTM cells.
- Leaky ReLU performs better than simple ReLU since it does not saturate the negative values of the perceptrons. These activations are suitable for hidden layers. They are not used for LSTM cells.
- Leaky ReLU speeds up the training rate, but we need to optimize the value of alpha for better output. In some models, the parameter alpha is also learnt during the training itself!

Have questions? Email me: g.sailokesh9@gmail.com