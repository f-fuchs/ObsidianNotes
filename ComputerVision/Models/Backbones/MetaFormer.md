---
dg-publish: true
---

# MetaFormer

MetaFormer is a general architecture abstracted from [[Transformer]]s by not specifying the token mixer. It adopts a hierarchical structure similar to traditional [[Convolutional Neural Networks (CNN)|CNN]]s and recent hierarchical Transformer variants like [[Swin Transformer]].
![[metaformer_architecture.png]]
Specifically, MetaFormer has 4 stages with $\frac{H}{4} \times \frac{W}{4}$ , $\frac{H}{8} \times \frac{W}{8}$ , $\frac{H}{16} \times \frac{W}{16}$ , and $\frac{H}{32} \times \frac{W}{32}$ tokens respectively, where $H$ and $W$ represent the width and height of the input image. The embedding sizes $C_i$ are either 64, 128, 320, and 512 for small-sized models or 96, 192, 384, and 768 for medium-sized models. Assuming there are $L$ MetaFormer blocks in total, stages 1, 2,
3, and 4 will contain $L/6$, $L/6$, $L/2$, and $L/6$ MetaFormer blocks respectively. The MLP expansion ratio is set as 4.

## MetaFormer Block

The input $I$ (the image for the first block and the processed tokens for later ones) is first processed by an input embedding $X = \mathrm{InputEmb}(I)$, where $X \in \mathbb{R}^{N×C}$ denotes the embedding tokens with sequence length $N$ and embedding dimension $C$. The $\mathrm{InputEmb}$ consists of a patch embedding (using overlapping patches) and linear projection analog to [[Vision Transformer|ViT]]s.

Then, embedding tokens are fed to repeated *MetaFormer* blocks, each of which includes two residual sub-blocks. Specifically, the first sub-block mainly contains a token mixer to communicate information among tokens and this sub-block can be expressed as

$$
Y = \mathrm {TokenMixer}(\mathrm {Norm}(X)) + X, 
$$

Note that the main function of the token mixer is to propagate token information although some token mixers can also mix channels like attention.

The second sub-block primarily consists of a two-layered MLP with non-linear activation,

$$
Z = \sigma \left(\mathrm {Norm}(Y)W_1\right)W_2 + Y, 
$$

where $W_1 \in \mathbb{R}^{C×rC}$ and $W_2 \in \mathbb{R}^{rC×C}$ are learnable parameters with MLP expansion ratio $r$; $\sigma(·)$ is a non-linear activation function.

### Token Mixer

Below are some examples for different token mixers, from trivial cases like the Identity function to Attention or Convolution.

![[metaformer.png]]
![[metaformer_baselines.png]]

## Resources

- <https://arxiv.org/abs/2111.11418> (MetaFormer Is Actually What You Need for Vision)
	- <https://github.com/sail-sg/poolformer>
- <https://arxiv.org/abs/2210.13452> (MetaFormer Baselines for Vision)
	- <https://github.com/sail-sg/metaformer>
