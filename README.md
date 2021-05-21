# Assignment3
Design a neural network that can take 2 inputs:an image from MNIST dataset, and a random number between 0 and 9 and gives two outputs:the "number" that was represented by the MNIST image, and the "sum" of this number with the random number that was generated and sent as the input to the network

In this, I have tried two different architectures, and are available in Assignment3.1.ipynb and Assignment3.2.ipynb respectively. Shown below are their architectures :

## Model 1
![image](https://user-images.githubusercontent.com/82941475/119097694-ae47bc00-ba32-11eb-95d8-18c21c4aedc2.png)
## Model 2
![image](https://user-images.githubusercontent.com/82941475/119097881-ddf6c400-ba32-11eb-8779-3498ec41bebc.png)
There are few architectural details which are different in these two models and will be highlighted later.
#### Data Representation
The image of data taken from MNIST dataset is in 1X28X28. The random digit is converted to one-hot vector of size 10. Data is taken in batch size of 100. 
#### Data Generation
Random digits are generated using random.randint in the range of 0 to 9, while digit images are picked up from MNIST database.
#### Combining the two inputs
Two inputs are combined at two different points in the two models. In Model1, the random digit vector is concatenated with flattened out features after the CNN part before passing it to fully connected layers. While in Model2, the flattened out features are sent through fully connected layers all the way to building a vector of length 10 (i.e. output of recognising the image). At this point the random digit is concatenated making it of size 20 and is further sent to next set of fully connected layers to get the output of sum of two digits.
##### Loss function
Loss function used here is cross-entropy. Loss is calculated in two parts : 
* Loss1 is the cross-entropy between label of the image and recognised output .
* Loss2 is the cross entropy between sum of label and random digit and sum recognized.
* Total loss is Loss1+Loss2
#### Optimization
The optimizer used here is SGD. Actually I tried both Adam and SGD. Definitely SGD worked better. With Adam, after few epochs, the loss started to increase, whereas with SGD, it steadily went down till it hit as low as becoming single digit. I didn't want to go further low to avoid overfitting to the training data.
#### Activation Function.
The activation function I have used here is RELU. Actually again here I tried, tanh as well. But the loss was coming to be very high and not going down.
#### Evaluation of Results
### Model1 Details:
##### Architecture 
Here I have two convolutional layers with 5 X 5 kernel size and maxpool2d. After that I flatten out the features to 192 (12X4X4) and 
concatenate the one-hot vector of the random digit which is the second input. So that makes first *fully connected layer* with 202 features and 
120 output features. Another *fully connected layer* is added which has 84 output features and final layer outputs a vector of size 28. 
I take the top 10 bits as the  digit recognized from image, and bottom 18 bits as the sum of this image digit and random digit.

