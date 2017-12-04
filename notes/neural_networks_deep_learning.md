## Logistic Regaression
### Loss function: $ L(\hat{y}, y) = -(y * log(\hat{y}) + (1-y) * log(1-\hat{y})) $    (__cross-entropy__, also known as Log Loss)
This is to make the gradient descent easier. Mean Squared Error as in linear regression cannot be used here, because squaring sigmoid function results in a non-convex function with many local minimums. Taking log gives you smooth monotonic function.

### Cost function: while loss function is applied to single training example, cost function is the overall cost - the average of the loss functions of the entire training set.
$ J(w, b) = 1/m * \sum{L(.., ,,)}

## Neural network
### Weights
weights are initialized with a very small number. this is to ensure that gradient descent can start with a relatively large gradient (tanh function)


### Train/Test set Rule of Thumb:
- Split:
	- traditional (relatively small dataset): 70/30, 60/20/20
	- Big data: 98/1/1 or even 99.5/.4/.1 (e.g. 1,000,000 examples, 10,000 dev, 10,000 test)

- Mismatched train/test distribution:
	- make sure dev, test data come from same distribution
- It might be ok to not have a test set (only dev set). if you don't need an unbiased estimate of the performance of the model.

### Bias and Variance
- High bias (underfitting) 
	- judged by looking at training error
	- Try bigger network
	- train longer
	- change NN architecture
- High variance (overfitting) 
	- judged by looking at difference of dev vs train set error
	- get more data
	- regularization
	- change NN architecture

### Regularization:
- L1/L2 regularization. 
	- L1 is sparse. used to compress the model (many weights are 0). but in practice not used often. L2 is most often used.
	- may need to try different values of lambda
- dropout regularization: randomly dropout nodes (zero-out some hidden units) in each layer for different training examples. Keepprob could be diff for diff layers, depending on layer size (larger size, lower keepprob). No dropout at test time (you don't want output to be random). Use interted dropout to ensure the expected value of Z are still roughly the same. It has similar effect to L2 regularization. In Computer vision, dropout is almost always used. but in other disciplines, only use when there is overfitting problem. with dropout, it is not easy to debug (plotting J vs # iterations), because cost J is not well defined.

### Data augmentation:
random flipping/zoom in/rotation/distortion of img data.

### Early Stopping:
plot dev set error together with J. stop when dev set error is min. 

### Orthogonalization:
- Optimize cost function J first
- then focus on reducing overfitting.

### Normalize inputs
- easier to optimize (gradient descent) when inputs are in similar scales. 
- subtract out mean, normalize variance. use same mean, variance to normalize test set.

### Optimization of gradient descent
#### Mini-batch gradient descent
Typical mini-batch size: 64, 128, 256, 512. Can be tuned as a hyperparameter