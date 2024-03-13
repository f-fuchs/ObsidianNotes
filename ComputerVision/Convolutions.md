
# Animations

*Blue maps are inputs of shape ($n, n$), cyan maps are outputs of shape ($m,m$) and the shaded areas are the kernels of shape ($k,k$) with stride $s$ and padding $p$ .*
## Convolution animations

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

## Transposed convolution animations

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


## Dilated convolution animations

In addition to the parameters above, dilated convolution introduce a dilation $d$ which specifies the spacing between kernel elements (a dilation of one is the value for a "connected kernel" as seen above). With this the output shape $(m,m)$ can be calculated with $m=\lfloor\frac{n+2p-d \cdot (k-1)-1}{s}+1\rfloor$.

| No padding, no stride, dilation                               |
| ------------------------------------------------------------- |
| ![[dilation.gif]]                                             |
| $n=7, k=3,s=1, p=0, d=2$                                      |
| $m=\lfloor\frac{7+2 \cdot 0 - 2 \cdot (3-1)-1}{1}+1\rfloor=3$ |

## Sources
- https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md
- https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html
- https://pytorch.org/docs/stable/generated/torch.nn.ConvTranspose2d.html