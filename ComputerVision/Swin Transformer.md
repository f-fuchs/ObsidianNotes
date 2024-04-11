## Overview
Swin Transformer are a kind of [[Vision Transformer]]  that tries to solve the problems of scale variations and a high resolution of pixels via hierarchical feature maps and  calculating the representation with **S**hifted **win**dows.
![[SwinTransformer_model.jpg]]
An overview of the architecture is shown in the image above. Similar to the [[Vision Transformer]] the first step is to split the image into image patches $X_p \in \mathbb{R}^{N ×(P^2 \cdot C)}$ where $N=\frac{H}{4} \cdot \frac{W}{4}$, $P=4$ and $C=3$ ($X_p \in \mathbb{R}^{\frac{H}{4} \cdot \frac{W}{4} × 48}$ ). Afterwards a linear embedding layer is used to project the raw features into an arbitrary dimension $D$ ($X_{emb}=X_p \times E \in \mathbb{R}^{\frac{H}{4} \cdot \frac{W}{4} × D}$, where $E \in \mathbb{R}^{48 \times D}$ ). One important difference compared to [[Vision Transformer]]s is that no positional embeddings are added. The last step of State 1 (see image above) are several Swin Transformer Blocks, which are depicted on the right in the image above. The main difference to the standard [[Transformer Encoder#Transformer Block| Transformer Block]] is that the [[Transformer Encoder#Self-Attention in Transformers| standard multi-head self attention module]] is replaced by a shifted window based multi-head self attention module.

## Shifted Window based Self-Attention

The [[Transformer Encoder|standard Transformer architecture]] and its [[Vision Transformer|adaptation for image classification]] both conduct global self attention, where the relationships between a token and all other tokens are computed. The global computation leads to quadratic complexity with respect to the number of tokens, making it unsuitable for many vision problems requiring an immense set of tokens for dense prediction or to represent a high-resolution image.

An alternative is to compute self-attention within local windows. The windows are arranged to evenly partition the image in a non-overlapping manner. Supposing each window contains $M \times M$ patches, the computational complexity of a global multi-head self attention module (MSA) and a window based one (W-MSA) on an image of $N$ patches are (*the first part $4ND^2$ comes from the three linear transformation of the input to key, query and value plus the output projection, the latter part $2N^2D$ comes from multiplying the query and key matrices to get the weight matrix and then multiplying the weight matrix with the value matrix*):
$$
\begin{aligned}
\Omega(MSA) &= 4ND^2 + 2N^2D \\
\Omega(W-MSA) &= 4ND^2 + 2M^2ND
\end{aligned}
$$
where the former is quadratic to number of patches $N$, and the latter is linear when $M$ is fixed (set to 7 by default). Global self-attention computation is generally unaffordable for a large number of patches, while the window based self-attention is scalable.

The window-based self-attention module lacks connections across windows, which limits its modeling power. To introduce cross-window connections while maintaining the efficient computation of non-overlapping windows, Swin Transformer use a shifted window partitioning approach which alternates between two partitioning configurations in consecutive Swin Transformer blocks.

![[SwinTransformer_shifted_window.jpg|700]]

As illustrated in the image above, the first module uses a regular window partitioning strategy which starts from the top-left pixel, and the $8 × 8$ feature map is evenly partitioned into
$2 × 2$ windows of size $4 × 4$ ($M = 4$). Then, the next module adopts a windowing configuration that is shifted from that of the preceding layer, by displacing the windows by ($|\frac{M}{2}|$, $|\frac{M}{2}|$) pixels from the regularly partitioned windows

Instead of adding linear embeddings to the input, Swin Transformer use relative position bias when computing self-attention,

$$
Attention(Q, K, V ) = SoftMax\left(\frac{Q \times K^T}{\sqrt{d}} + B \right) \times V
$$
where $Q, K, V \in \mathbb{R}^{M^2 \times d}$ are the query, key and value matrices; $d$ is the query/key dimension, and $M^2$ is the number of patches in a window and $B \in \mathbb{R}^{M^2 \times M^2}$.

## Patch Merging

Between every stage Swin Transformer uses patch merging to produce a hierarchical representation of the features, see image below.

![[SwinTransformer_hierarchical_featue_maps.jpg|700]]
A patch merging layer concatenates the features of each group of $2 \times 2$ neighboring patches, and applies a linear layer on the $4C$-dimensional concatenated features to reduce the resolution to $2C$ ($2\times$ downsampling). Swin Transformer blocks are applied afterwards for feature transformation, with the resolution kept at $\frac{H}{8} \times \frac{H}{8}$. This first block of patch merging and feature transformation is denoted as “Stage 2”. The procedure is repeated twice, as “Stage 3” and “Stage 4”, with output resolutions of $\frac{H}{16} \times \frac{H}{16}$ and $\frac{H}{32} \times \frac{H}{32}$ , respectively.