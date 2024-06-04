---
dg-publish: true
---

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

The Mixer architecture clearly separates the per-location (channel-mixing) operations $(i)$ and cross-location (token-mixing) operations $(ii)$. Both operations are implemented with MLPs. Mixer takes as input a sequence of $S$ non-overlapping image patches, each one projected to a desired hidden dimension $C$. This results in a two-dimensional real-valued input table, $X \in \mathbb{R}^{S×C}$. If the original input image has resolution $(H, W)$, and each patch has resolution $(P, P)$, then the number of patches is $S = \frac{HW}{P^2}$. All patches are linearly projected with the same projection matrix.  
	*similar to [[Vision Transformer]]*

Mixer consists of multiple layers of identical size, and each layer consists of two MLP blocks. The first one is the token-mixing MLP: it acts on columns of $X$ (i.e. it is applied to a transposed input table $X$), maps $\mathbb{R}^S  \rightarrow \mathbb{R}^S$, and is shared across all columns. The second one is the channel-mixing MLP: it acts on rows of $X$, maps $\mathbb{R}^C  \rightarrow \mathbb{R}^C$, and is shared across all rows.

![[mixer_figure.png]]

Each MLP block contains two [[[Linear Layer|fully-connected layers]] and a nonlinearity applied independently to each row of its input data tensor. Additionally, other standard components like [[Skip-Connections|skip-connections]] and [[Normalization Layers#Layer Norm|layer normalization]] are used. A Mixer layer can be written as follows:

$$
\begin{align}
U &= X^T + \sigma \Bigl(\text{LayerNorm}(X)^T \times W_1^T \Bigr) \times W_2^T
\\
Y &= U^T +  \sigma \Bigl(\text{LayerNorm}(U^T) \times W_3^T \Bigr) \times W_4^T
\end{align}
$$

 - $X \in \mathbb{R}^{S \times C}$
 - $W_1 \in \mathbb{R}^{D_S \times S}$
 - $W_2 \in \mathbb{R}^{S \times D_S}$
 - $W_3 \in \mathbb{R}^{D_C \times C}$
 - $W_4 \in \mathbb{R}^{C \times D_C}$
 - $\sigma$ is an element-wise nonlinearity ([[GELU]])
 - $\text{LayerNorm}(X)^T \times W_1^T \in \mathbb{R}^{C \times D_S}$
 - $\sigma \Bigl(\text{LayerNorm}(X)^T \times W_1^T \Bigr) \times W_2^T \in \mathbb{R}^{C \times S}$
 - $U \in \mathbb{R}^{C \times S}$
 - $\text{LayerNorm}(U^T) \times W_3^T \in \mathbb{R}^{S \times D_C}$
 - $\sigma \Bigl(\text{LayerNorm}(U^T) \times W_3^T \Bigr) \times W_4^T \in \mathbb{R}^{S \times C}$
 - $Y \in \mathbb{R}^{S \times C}$

$D_S$ and $D_C$ are tunable hidden widths in the token-mixing and channel-mixing MLPs, respectively. Note that DS is selected independently of the number of input patches. Therefore, the computational complexity of the network is linear in the number of input patches, unlike [[Vision Transformer|ViT]] whose complexity is quadratic. Since $D_C$ is independent of the patch size, the overall complexity is linear in the number of pixels in the image, as for a typical [[Convolutional Neural Networks (CNN)|CNN]].

The same channel-mixing MLP (token-mixing MLP) is applied to every row (column) of X. Tying the parameters of the channel-mixing MLPs (within each layer) is a natural choice - it provides positional invariance, a prominent feature of convolutions. However, tying parameters across channels (for the token-mixing MLP) is much less common. The parameter tying prevents the architecture from growing too fast when increasing the hidden dimension $C$ or the sequence length $S$ and leads to significant memory savings. Each layer in Mixer (except for the initial patch projection layer) takes an input of the same size similar to [[Vision Transformer|ViT]] and [[MetaFormer]].

## Resources

- <https://arxiv.org/pdf/2105.01601> (MLP-Mixer: An all-MLP Architecture for Vision)
- <https://raw.githubusercontent.com/google-research/vision_transformer/>
