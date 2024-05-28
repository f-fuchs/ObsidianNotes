---
dg-publish: true
---

# Linear Layer

## Element-wise

$$
\vec{y}= A \times \vec{x}+\vec{b}
$$

- $\vec{x} \in \mathbb{R}^{H_{in}}$
- $A \in \mathbb{R}^{H_{out} \times H_{in}}$, $A^T \in \mathbb{R}^{H_{in} \times H_{out}}$
- $\vec{b} \in \mathbb{R}^{H_{out}}$
- $\vec{y} \in \mathbb{R}^{H_{out}}$

```run-python
import torch

H_in, H_out = 5, 10
x = torch.rand(H_in, 1) # one dimensional vectors in pytorch are row vectors
A = torch.rand(H_out, H_in)
b = torch.rand(H_out, 1) # one dimensional vectors in pytorch are row vectors

print(f"{x.shape =}")
print(f"{A.shape =}")
print(f"{b.shape =}")
print(f"{(A @ x ).shape =}")
```

%%
add good illustration
%%

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

H_in, H_out,  N = 5, 10, 100
X = torch.rand(N, H_in) # one dimensional vectors in pytorch are row vectors
A = torch.rand(H_out, H_in)
b = torch.rand(H_out, 1) # one dimensional vectors in pytorch are row vectors

print(f"{X.shape =}")
print(f"{A.shape =}")
print(f"{b.shape =}")
print(f"{(X @ A.T).shape =}")
```

## Resources

- <https://pytorch.org/docs/stable/generated/torch.nn.Linear.html>
