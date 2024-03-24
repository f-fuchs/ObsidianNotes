The vanishing gradient problem arises because of the repeated application of the chain rule through many layers of the network. As the gradients propagate backwards, they are multiplied by the gradients of the activation functions. Activation functions such as sigmoid or tanh have regions where their gradients are very small, particularly for large or small input values. When gradients pass through many layers, each multiplication by a small gradient can cause the overall gradient to shrink exponentially, leading to vanishing gradients.

One way to deal with the vanishing gradient problem are newer activation functions, whose derivatives have a larger output space. The most common one is ReLu and its variants.

![[1024px-ReLU_and_GELU.svg.png]]