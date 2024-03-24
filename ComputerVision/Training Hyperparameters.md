
## Learning Rate

The learning rate indicates the step size that gradient descent takes towards local optima.
![[different_learning_rates.png]]

## Epoch

One forward pass and one backward pass of _all_ the training examples.

## Batch Size

The number of training examples in one forward/backward pass. The higher the batch size, the more memory space you'll need.

### Relationship with Learning Rate
There are some works done on this problem. Some authors suggest that when multiplying batch size by $k$, we should also multiply the learning rate with $\sqrt{k}$ to keep the variance in the gradient expectation constant. Also, more commonly, a simple linear scaling rule is used. It means that when the batch size is multiplied by $k$, the learning rate should also be multiplied by $k$.

larger batch sizes provide more accurate estimates of the gradient, which allows for larger learning rates without causing instability in training.
A larger batch size means less weight updates

### Relationship with Generalization
There's a relationship between batch size and generalization performance. Smaller batch sizes introduce more noise into the parameter updates, which can sometimes lead to better generalization. Therefore smaller batch sizes are a form of Regularization. 
## Number of Iterations

Number of forward/backward passes, each pass using [[Training Hyperparameters#Batch Size| batch size]] number of examples. 