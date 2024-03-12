
*Blue maps are inputs of shape ($n, n$), cyan maps are outputs of shape ($m,m$) and the shaded areas are the kernels of shape ($k,k$) with stride $s$ and padding $p$ .*

## Convolution animations

The output shape of a convolution can be calculated with $m=\frac{n+2p-(k-1)}{s}$.

| no padding, no strides            | Arbitrary padding, no strides         | half padding, no strides          | Full padding, no strides          |
| --------------------------------- | ------------------------------------- | --------------------------------- | --------------------------------- |
| ![[no_padding_no_strides.gif]]    | ![[arbitrary_padding_no_strides.gif]] | ![[same_padding_no_strides.gif]]  | ![[full_padding_no_strides.gif]]  |
| $n=4, k=3,s=1, p=0$               | $n=5, k=4,s=1, p=2$                   | $n=5, k=3,s=1, p=1$               | $n=5, k=3,s=1, p=2$               |
| $m=\frac{4+2 \cdot 0-(3-1)}{1}=2$ | $m=\frac{5+2 \cdot 2-(4-1)}{1}=6$     | $m=\frac{5+2 \cdot 1-(3-1)}{1}=5$ | $m=\frac{5+2 \cdot 2-(3-1)}{1}=7$ |
| No padding, strides               | Padding, strides                      | Padding, strides (odd)            | Full padding, no strides          |
| ![[no_padding_strides.gif]]       | ![[padding_strides.gif]]              | ![[padding_strides_odd.gif]]      |                                   |
| $n=6, k=3,s=2, p=0$               | $n=4, k=3,s=1, p=0$                   | $n=4, k=3,s=1, p=0$               |                                   |
| $m=\frac{6+2 \cdot 0-(3-1)}{2}=2$ |                                       |                                   |                                   |

## Transposed convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._



## Dilated convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._


## Sources
- https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md