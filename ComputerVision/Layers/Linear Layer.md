# Linear Layer

## Element-wise

$$
\vec{y}=\vec{x} \times A^T+\vec{b}
$$
- $\vec{x} \in \mathbb{R}^{H_{in}}$
- $A \in \mathbb{R}^{H_{out} \times H_{in}}$, $A^T \in \mathbb{R}^{H_{in} \times H_{out}}$
- $\vec{b} \in \mathbb{R}^{H_{out}}$
- $\vec{y} \in \mathbb{R}^{H_{out}}$

```run-python
import torch

H_in, H_out = 5, 10
x = torch.rand(H_in)
A = torch.rand(H_out, H_in)
b = torch.rand(H_out)

print(f"{x.shape =}")
print(f"{A.shape =}")
print(f"{A.T.shape =}")
print(f"{b.shape =}")
print(f"{(x@A.T).shape =}")
```
## Matrix
$$
Y = X \times A^T + \vec{b} \times\vec{1}^T
$$
- $X \in \mathbb{R}^{N \times H_{in}}$
- $A \in \mathbb{R}^{H_{out} \times H_{in}}$, $A^T \in \mathbb{R}^{H_{in} \times H_{out}}$
- $\vec{b} \in \mathbb{R}^{H_{out}}$
- $\vec{1} \in \mathbb{R}^{N}$
- $Y \in \mathbb{R}^{N \times H_{out}}$

```run-python
import torch

b = torch.tensor([[0], [1], [2], [3]])
t = torch.tensor([[1], [1], [1], [1], [1]])

print(f"{b.shape =}")
print(f"{t.shape =}")
print(f"{t.T.shape =}")
print(f"{b @ t.T =}")
```
## Resources
- https://pytorch.org/docs/stable/generated/torch.nn.Linear.html