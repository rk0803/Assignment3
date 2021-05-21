# Assignment3
Design a neural network that can take 2 inputs:an image from MNIST dataset, and a random number between 0 and 9 and gives two outputs:the "number" that was represented by the MNIST image, and the "sum" of this number with the random number that was generated and sent as the input to the network

In this, I have tried two different architectures, and are available in Assignment3.1.ipynb and Assignment3.2.ipynb respectively. Shown below are their architectures :

## Model 1
![image](https://user-images.githubusercontent.com/82941475/119097694-ae47bc00-ba32-11eb-95d8-18c21c4aedc2.png)
## Model 2
![image](https://user-images.githubusercontent.com/82941475/119109279-ab52c880-ba3e-11eb-82fa-43de2a2c47d6.png)
There are few architectural details which are different in these two models and will be highlighted later.
#### Data Representation
The image of data taken from MNIST dataset is in 1X28X28. The random digit is converted to one-hot vector of size 10. Data is taken in batch size of 100. 
#### Data Generation
Random digits are generated using random.randint in the range of 0 to 9, while digit images are picked up from MNIST database.
The outputs to be compared with the output of Neural Net are labels (for image digit) and labels added with random digits generated to test the output of sum of digits.
#### Combining the two inputs
Two inputs are combined at two different points in the two models. In Model1, the random digit vector is concatenated with flattened out features after the CNN part before passing it to fully connected layers. While in Model2, the flattened out features are sent through fully connected layers all the way to building a vector of length 10 (i.e. output of recognising the image). At this point the random digit is concatenated making it of size 20 and is further sent to next set of fully connected layers to get the output of sum of two digits.
##### Loss function
Loss function used here is cross-entropy, because cross-entropy is a measure of the difference between two probability distributions for a given random variable or set of events.  It builds upon the idea of entropy from information theory and calculates the number of bits required to represent an average event from one distribution compared to another distribution. Loss is calculated in two parts : 
* Loss1 is the cross-entropy between label of the image and recognised output .
* Loss2 is the cross entropy between sum of label and random digit builds upon the idea of entropy from information theory and calculates the number of bits required to represent or transmit an average event from one distribution compared to another distribution and sum recognized.
* Total loss is Loss1+Loss2
#### Activation Function.
The activation function I have used here is **ReLu** in all the layers in Model1. While in Model 2 last two layers are **tanh** 

#### Optimization
The optimizer used here is SGD. Actually I tried both Adam and SGD. Definitely SGD worked better. With Adam, after few epochs, the loss started to increase, whereas with SGD, it steadily went down as can be seen below:
![image](https://user-images.githubusercontent.com/82941475/119106424-f91a0180-ba3b-11eb-87d2-2468ef12ed7c.png)


#### Evaluation of Results
The results are evaluated on test set loaded from the MNIST dataset. A new set of random digits in created as well. The trained model is run on the test set images and new set of randomly generated digits. The number of correctly predicted digits and correctly predicted sum is calculated.
* For model 1 : total_correct_digits:  9917 total_correct_sum:  9897
* For model 2 : total_correct_digits:  8957 total_correct_sum:  9897

### Model 1 Architecture Details:

Here I have two convolutional layers with 5 X 5 kernel size and maxpool2d. After that I flatten out the features to 192 (12X4X4) and 
concatenate the one-hot vector of the random digit which is the second input. So that makes first *fully connected layer* with 202 features and 
120 output features. Another *fully connected layer* is added which has 84 output features and final layer outputs a vector of size 28. 
I take the top 10 bits as the  digit recognized from image, and bottom 18 bits as the sum of this image digit and random digit.
<p>Net(</p>
 <p> (conv1): Conv2d(1, 6, kernel_size=(5, 5), stride=(1, 1))</p>
  <p>  (conv2): Conv2d(6, 12, kernel_size=(5, 5), stride=(1, 1)) </p>
  <p>  (fc1): Linear(in_features=202, out_features=120, bias=True) </p>
  <p>  (fc2): Linear(in_features=120, out_features=84, bias=True) </p>
  <p>  (out): Linear(in_features=84, out_features=28, bias=True)</p>
<p>)</p>

### Model 2 Architecture details:
Here I have two convolutional layers with 5 X 5 kernel size and maxpool2d. After that I flatten out the features to 192 (12X4X4) and pass it through full connected layers (120,60) and (60,10). This ouput of size 10 goes on become an output of Net and also concatenated with one-hot vector of the random digit which is the second input, becomes input further to next set fully connected layers (20, 100), (100, 60) and (60,18). This output of size 18 becomes the second ouput, one-hot vector representation of sum of two digits.
 <p> Net(
 <p>   (conv1): Conv2d(1, 6, kernel_size=(5, 5), stride=(1, 1)) </p>
 <p> (conv2): Conv2d(6, 12, kernel_size=(5, 5), stride=(1, 1))</p>
  <p>  (fc1): Linear(in_features=192, out_features=120, bias=True)</p>
  <p> (fc2): Linear(in_features=120, out_features=60, bias=True)</p>
  <p> (fc3): Linear(in_features=60, out_features=10, bias=True)</p>
   <p> (fc4): Linear(in_features=20, out_features=100, bias=True)</p>
   <p> (fc5): Linear(in_features=100, out_features=60, bias=True)</p>
   <p> (out): Linear(in_features=60, out_features=18, bias=True)</p>
)

