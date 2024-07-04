---
dg-publish: true
---

# Convolutional Layer

## 2D Convolutions

*Blue maps are inputs of shape ($n, n$), cyan maps are outputs of shape ($m,m$) and the shaded areas are the kernels of shape ($k,k$) with stride $s$ and padding $p$.*

### Convolution

The output shape $(m,m)$ can be calculated with $m=\lfloor\frac{n+2p-(k-1)-1}{s}+1\rfloor$.

| no padding, no strides                              | Arbitrary padding, no strides                       | half padding, no strides                            |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| ![[no_padding_no_strides.gif]]                      | ![[arbitrary_padding_no_strides.gif]]               | ![[same_padding_no_strides.gif]]                    |
| $n=4, k=3,s=1, p=0$                                 | $n=5, k=4,s=1, p=2$                                 | $n=5, k=3,s=1, p=1$                                 |
| $m=\lfloor\frac{4+2 \cdot 0-(3-1)-1}{1}+1\rfloor=2$ | $m=\lfloor\frac{5+2 \cdot 2-(4-1)-1}{1}+1\rfloor=6$ | $m=\lfloor\frac{5+2 \cdot 1-(3-1)-1}{1}+1\rfloor=5$ |
| Full padding, no strides                            | No padding, strides                                 | Padding, strides                                    |
| ![[full_padding_no_strides.gif]]                    | ![[no_padding_strides.gif]]                         | ![[padding_strides.gif]]                            |
| $n=5, k=3,s=1, p=2$                                 | $n=5, k=3,s=2, p=0$                                 | $n=5,k=3,s=2,p=1$                                   |
| $m=\lfloor\frac{5+2 \cdot 2-(3-1)-1}{1}+1\rfloor=7$ | $m=\lfloor\frac{5+2 \cdot 0-(3-1)-1}{2}+1\rfloor=2$ | $m=\lfloor\frac{5+2 \cdot 1-(3-1)-1}{2}+1\rfloor=3$ |

### Transposed Convolution

The output shape $(m,m)$ can be calculated with $m=(n-1) \cdot s-2 \cdot p+ k$.

In contrast to standard convolution the actual padding $p_t$ is not $p$, but $(k-1)-p$. Therefore $p=(k-1)-p_t$.

| no padding, no strides                      | Arbitrary padding, no strides                    | half padding, no strides                    |
| ------------------------------------------- | ------------------------------------------------ | ------------------------------------------- |
| ![[no_padding_no_strides_transposed.gif]]   | ![[arbitrary_padding_no_strides_transposed.gif]] | ![[same_padding_no_strides_transposed.gif]] |
| $n=2, k=3,s=1, p_t=2$                       | $n=6, k=4,s=1, p_t=1$                            | $n=5, k=3,s=1, p_t=1$                       |
| $p=(3-1)-2=0$                               | $p=(4-1)-1=2$                                    | $p=(3-1)-1=1$                               |
| $m=(2-1) \cdot 1 - 2 \cdot 0+ 3=4$          | $m=(6-1) \cdot 1 - 2 \cdot 1+ 4=5$               | $m=(5-1) \cdot 1 - 2 \cdot 1+ 3=5$          |
| Full padding, no strides                    | No padding, strides                              | Padding, strides                            |
| ![[full_padding_no_strides_transposed.gif]] | ![[no_padding_strides_transposed.gif]]           | ![[padding_strides_transposed.gif]]         |
| $n=7, k=3,s=1, p_t=0$                       | $n=2, k=3,s=2, p_t=2$                            | $n=3,k=3,s=2,p_t=1$                         |
| $p=(3-1)-0=2$                               | $p=(3-1)-2=0$                                    | $p=(3-1)-1=1$                               |
| $m=(7-1) \cdot 1 - 2 \cdot 2+ 3=5$          | $m=(2-1) \cdot 2 - 2 \cdot 0 + 3=5$              | $m=(3-1) \cdot 2 - 2 \cdot 1 + 3=5$         |

### Dilated Convolution Animations

In addition to the parameters above, dilated convolution introduce a dilation $d$ which specifies the spacing between kernel elements (a dilation of one is the value for a "connected kernel" as seen above). With this the output shape $(m,m)$ can be calculated with $m=\lfloor\frac{n+2p-d \cdot (k-1)-1}{s}+1\rfloor$.

| No padding, no stride, dilation                               |
| ------------------------------------------------------------- |
| ![[dilation.gif]]                                             |
| $n=7, k=3,s=1, p=0, d=2$                                      |
| $m=\lfloor\frac{7+2 \cdot 0 - 2 \cdot (3-1)-1}{1}+1\rfloor=3$ |

## Convolutions in Machine Learning

A multi-channel convolution with multiple input channels can be visualized as a three-dimensional tensor (as shown in gray in the image below). This tensor is multiplied element-wise with three-dimensional chunks of the input image and then summed over all dimensions, resulting in one value per image chunk. *(Essentially, we take a weighted sum of the three-dimensional chunk)*. **Therefore, for each output channel, we need one three-dimensional tensor or kernel**.

*This remains a 2D convolution because the filter strides are only along the height and width dimensions (**NOT** depth). The number of movement directions of the filter determines the dimensions of convolution*

| Standard Convolution    | Depthwise Convolution          |
| ----------------------- | ------------------------------ |
| ![[conv2d-3d.svg\|270]] | ![[conv2d-depthwise.svg\|400]] |

Depthwise convolutions are a variation of the operation described above. In a standard 2D convolution with multiple input channels, the filter matches the depth of the input and allows channels to mix freely to generate each element in the output. In contrast, depthwise convolutions keep each channel separate, hence the name depthwise.

## Sources

- [GitHub - vdumoulin/conv_arithmetic: A technical report on convolution arithmetic in the context of deep learning](https://github.com/vdumoulin/conv_arithmetic)
- [Depthwise separable convolutions for machine learning - Eli Bendersky's website (thegreenplace.net)](https://eli.thegreenplace.net/2018/depthwise-separable-convolutions-for-machine-learning/)
- [ConvTranspose2d — PyTorch 2.3 documentation](https://pytorch.org/docs/stable/generated/torch.nn.ConvTranspose2d.html)
- [Conv2d — PyTorch 2.3 documentation](https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html)
