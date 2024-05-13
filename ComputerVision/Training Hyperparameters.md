---
dg-publish: true
---

# Training Hyperparameters

## Learning Rate

The learning rate indicates the step size that gradient descent takes towards local optima.

![[different_learning_rates.png]]

## Epoch

One forward pass and one backward pass of all the training examples.

## Batch Size

The number of training examples in one forward/backward pass. The higher the batch size, the more memory space you'll need.

### Relationship with Learning Rate

Larger batch sizes provide more accurate estimates of the gradient, which allows for larger learning rates without causing instability in training. Furthermore, a larger batch size means less steps per epoch which means each step has to go farther.

In theory when multiplying the batch size by $k$, we should also multiply the learning rate with $\sqrt{k}$ to keep the variance in the gradient expectation constant. In practice a simple linear scaling rule is used (batch size is multiplied by $k$, the learning rate should also be multiplied by $k$).

Adaptive learning rate methods, such as [[Adam]], RMSProp, and AdaGrad, adjust the learning rate dynamically during training based on the history of gradients. Therefore adjusting the learning rate may not be needed.

### Relationship with Generalization

There's a relationship between batch size and generalization performance. Smaller batch sizes introduce more noise into the parameter updates, which can sometimes lead to better generalization. Therefore smaller batch sizes are a form of Regularization.

## Number of Iterations

Number of forward/backward passes, each pass using [[Training Hyperparameters#Batch Size| batch size]] number of examples.
