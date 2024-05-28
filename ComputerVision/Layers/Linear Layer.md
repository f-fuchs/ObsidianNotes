# Linear Layer

## Element-wise

$$
\vec{y}=\vec{x} \times A^T+\vec{b}
$$
- $x \in \mathbb{R}^{1 \times H_{in}}$
- $A \in \mathbb{R}^{H_{out} \times H_{in}}$, $A^T \in \mathbb{R}^{H_{in} \times H_{out}}$
- $b \in \mathbb{R}^{1 \times H_{out}}$
- $y \in \mathbb{R}^{1 \times H_{out}}$

## Matrix
$$
Y = X \times A^T + b
$$
- $X \in \mathbb{R}^{N \times H_{in}}$
- $A \in \mathbb{R}^{H_{out} \times H_{in}}$, $A^T \in \mathbb{R}^{H_{in} \times H_{out}}$
- $b \in \mathbb{R}^{1 \times H_{out}}$
- $Y \in \mathbb{R}^{N \times H_{out}}$
## Resources
- https://pytorch.org/docs/stable/generated/torch.nn.Linear.html