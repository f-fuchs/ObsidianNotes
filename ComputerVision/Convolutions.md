
*Blue maps are inputs, and cyan maps are outputs.*

## Convolution animations

|no padding, no strides | Arbitrary padding, no strides | half padding, no strides| Full padding, no strides|
| ----------------------| ------------------------------| ------------------------| ------------------------|
| ![[no_padding_no_strides.gif]]|![[arbitrary_padding_no_strides.gif]]|![[same_padding_no_strides.gif]]|![[full_padding_no_strides.gif]]|
| $\mathbb{R}^{4 \times 4} \rightarrow \mathbb{R}^{2 \times 2}$ |||| 
|No padding, strides| Padding, strides | Padding, strides (odd)| Full padding, no strides||
| ![[no_padding_strides.gif]]|![[padding_strides.gif]]|![[padding_strides_odd.gif]]||
| $\mathbb{R}^{4 \times 4} \rightarrow \mathbb{R}^{2 \times 2}$ |||| 

## Transposed convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._



## Dilated convolution animations

_N.B.: Blue maps are inputs, and cyan maps are outputs._


## Sources
- https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md