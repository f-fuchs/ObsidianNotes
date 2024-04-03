
## One Layer Neural Network

![[One_hidden_layer.png]]
$$
\begin{aligned}
\hat{y} &= \sigma \left(W^{(2)} \times \sigma(W^{(1)} \times \vec{x}+\vec{b^{(1)}}) + \vec{b^{(2)}} \right) \\
W^{(i)} &= \text{weight matrix of layer }i \\
\vec{b^{(i)}} &= \text{bias vector of layer }i \\
\vec{x} &= \text{input vector} 
\end{aligned}
$$
## Multilayer Perceptron (MLP)

A multilayer perceptron (MLP) is a type of FNN, consisting of fully connected neurons with a nonlinear kind of activation function, organized in at least three layers, notable for being able to distinguish data that is not linearly separable.