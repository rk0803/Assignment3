# Assignment3
Design a neural network that can take 2 inputs:an image from MNIST dataset, and a random number between 0 and 9 and gives two outputs:the "number" that was represented by the MNIST image, and the "sum" of this number with the random number that was generated and sent as the input to the network

In this, I have tried two different architectures, and are available in Assignment3.1.ipynb and Assignment3.2.ipynb. Shown below are their architectures :

## Model 1
## Model 2
### Model1 Details:
##### Architecture 
Here I have two convolutional layers with 5 X 5 kernel size and maxpool2d. After that I flatten out the features to 192 (12X4X4) and 
concatenate the one-hot vector of the random digit which is the second input. So that makes first *fully connected layer* with 202 features and 
120 output features. Another *fully connected layer* is added which has 84 output features and final layer outputs a vector of size 28. 
I take the top 10 bits as the  digit recognized from image, and bottom 18 bits as the sum of this image digit and random digit.
##### Loss function
Loss function used here is cross-entropy. Loss is calculated in two parts : 
* Loss1 is the cross-entropy between label of the image and recognised output .
* Loss2 is the cross entropy between sum of label and random digit and sum recognized.
* Total loss is Loss1+Loss2
