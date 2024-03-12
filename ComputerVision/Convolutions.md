
*Blue maps are inputs of shape ($n, n$), cyan maps are outputs of shape ($m,m$) and the shaded areas are the kernels of shape ($k,k$) with stride $s$ and padding $p$ .*

## Convolution animations

The output shape of a convolution can be calculated with $m=\lfloor\frac{n+2p-(k-1)-1}{s}+1\rfloor$.

| no padding, no strides                              | Arbitrary padding, no strides                       | half padding, no strides                            | Full padding, no strides                            |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| ![[no_padding_no_strides.gif]]                      | ![[arbitrary_padding_no_strides.gif]]               | ![[same_padding_no_strides.gif]]                    | ![[full_padding_no_strides.gif]]                    |
| $n=4, k=3,s=1, p=0$                                 | $n=5, k=4,s=1, p=2$                                 | $n=5, k=3,s=1, p=1$                                 | $n=5, k=3,s=1, p=2$                                 |
| $m=\lfloor\frac{4+2 \cdot 0-(3-1)-1}{1}+1\rfloor=2$ | $m=\lfloor\frac{5+2 \cdot 2-(4-1)-1}{1}+1\rfloor=6$ | $m=\lfloor\frac{5+2 \cdot 1-(3-1)-1}{1}+1\rfloor=5$ | $m=\lfloor\frac{5+2 \cdot 2-(3-1)-1}{1}+1\rfloor=7$ |
| No padding, strides                                 | Padding, strides                                    | Padding, strides (odd)                              | Full padding, no strides                            |
| ![[no_padding_strides.gif]]                         | ![[padding_strides.gif]]                            | ![[padding_strides_odd.gif]]                        |                                                     |
| $n=5, k=3,s=2, p=0$                                 | $n=5,k=3,s=2,p=1$                                   | $n=6, k=3,s=2,p=1$                                  |                                                     |
| $m=\lfloor\frac{5+2 \cdot 0-(3-1)-1}{2}+1\rfloor=2$ | $m=\lfloor\frac{5+2 \cdot 1-(3-1)-1}{2}+1\rfloor=3$ | $m=\lfloor\frac{6+2 \cdot 1-(3-1)-1}{2}+1\rfloor=3$ |                                                     |

## Transposed convolution animations

| no padding, no strides                              | Arbitrary padding, no strides                       | half padding, no strides                            | Full padding, no strides                            |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| ![[no_padding_no_strides_transposed.gif]]           | ![[arbitrary_padding_no_strides_transposed.gif]]    | ![[same_padding_no_strides_transposed.gif]]         | ![[full_padding_no_strides_transposed.gif]]         |
| $n=4, k=3,s=1, p=0$                                   | $n=5, k=4,s=1, p=2$                                    | $n=5, k=3,s=1, p=1$                                   | $n=5, k=3,s=1, p=2$                                    |
| $m=\lfloor\frac{4+2 \cdot 0-(3-1)-1}{1}+1\rfloor=2$       | $m=\lfloor\frac{5+2 \cdot 2-(4-1)-1}{1}+1\rfloor=6$        | $m=\lfloor\frac{5+2 \cdot 1-(3-1)-1}{1}+1\rfloor=5$       | $m=\lfloor\frac{5+2 \cdot 2-(3-1)-1}{1}+1\rfloor=7$        |
| No padding, strides                                 | Padding, strides                                    | Padding, strides (odd)                              | Full padding, no strides                            |
| ![[no_padding_strides_transposed.gif]]              | ![[padding_strides_transposed.gif]]                 | ![[padding_strides_odd_transposed.gif]]             |                                                     |
| $n=5, k=3,s=2, p=0$                                   | $n=5,k=3,s=2,p=1$                                      | $n=6, k=3,s=2,p=1$                                    |                                                     |
| $m=\lfloor\frac{5+2 \cdot 0-(3-1)-1}{2}+1\rfloor=2$       | $m=\lfloor\frac{5+2 \cdot 1-(3-1)-1}{2}+1\rfloor=3$        | $m=\lfloor\frac{6+2 \cdot 1-(3-1)-1}{2}+1\rfloor=3$        |                                                     |


## Dilated convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._


## Sources
- https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md
- https://pytorch.org/docs/stable/generated/torch.nn.Conv2d.html
- https://pytorch.org/docs/stable/generated/torch.nn.ConvTranspose2d.html