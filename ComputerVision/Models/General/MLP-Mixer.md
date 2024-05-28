# MLP-Mixer

Modern deep vision architectures consist of layers that mix features $(i)$ at a given spatial location,
$(ii)$ between different spatial locations, or both at once. 
- CNNs: 
	- $(ii)$ is implemented with $N \times N$ convolutions (for $N > 1$) and pooling
	- $(i)$ is implemented with$1 \times 1$ convolutions
	- larger kernels perform both $(i)$ and $(ii)$
- Vision Transformers and other attention-based architectures:
	- self-attention layers allow both $(i)$ and $(ii)$ 
	- MLP-blocks perform $(i)$

The Mixer architecture clearly separates the per-location (channel-mixing) operations $(i)$ and cross-location (token-mixing) operations $(ii)$. Both operations are implemented with MLPs. Mixer takes as input a sequence of $S$ non-overlapping image patches, each one projected to a desired
hidden dimension $C$. This results in a two-dimensional real-valued input table, $X \in \mathbb{R}^{S×C}$ . If the
original input image has resolution $(H, W )$, and each patch has resolution $(P, P )$, then the number of patches is $S = \frac{HW}{P^2}$. All patches are linearly projected with the same projection matrix.  
	*similar to [[Vision Transformer]]*


Mixer consists of multiple layers of identical size, and each layer consists of two MLP blocks. The first one is the token-mixing MLP: it acts on columns of $X$ (i.e. it is applied to a transposed input table X), maps $\mathbb{R}^S  \rightarrow \mathbb{R}^S$ , and is shared across all columns. The second one is the channel-mixing MLP: it
acts on rows of X, maps RC 7 → RC , and is shared across all rows.

![[mixer_figure.png]]
## Resources

- https://arxiv.org/pdf/2105.01601 (MLP-Mixer: An all-MLP Architecture for Vision)
- https://raw.githubusercontent.com/google-research/vision_transformer/
