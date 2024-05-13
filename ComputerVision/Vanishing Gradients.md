---
dg-publish: true
---
The vanishing gradient problem arises because of the repeated application of the chain rule through many layers of the network. As the gradients propagate backwards, they are multiplied by the gradients of the activation functions. Activation functions such as sigmoid or tanh have regions where their gradients are very small, particularly for large or small input values. When gradients pass through many layers, each multiplication by a small gradient can cause the overall gradient to shrink exponentially, leading to vanishing gradients.

![[common_activation_functions.png]]

One way to deal with the vanishing gradient problem are newer activation functions, whose derivatives have a larger output space. The most common one is ReLu and its variants. While ReLu solves the Vanishing Gradients Problem it introduces a new problem, namely the dying ReLu problem.

![[ReLU_and_GELU.svg.png]]
## Dying ReLu Problem

The ReLU neuron enters a dead state when it always outputs $0$ for any input value. This state is difficult to recover from because the gradient is also $0$. During backpropagation, the gradient fails to flow because the outputs are $0$ as a result, the weights are not updated. In the worst case scenario, a constant function may result in which the entire neural network fails. 
Newer variants such as Leaky ReLU solve this problem by setting the derivative to a random small value instead of $0$. This gives the neuron a chance to recover.
## Further Resources

- https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html