## Overview
Swin Transformer are a kind of [[Vision Transformer]]  that tries to solve the problems of scale variations and a high resolution of pixels via hierarchical feature maps and  calculating the representation with **S**hifted **win**dows.
![[SwinTransformer_model.jpg]]
An overview of the architecture is shown in the image above. Similar to the [[Vision Transformer]] the first step is to split the image into image patches $X_p \in \mathbb{R}^{N ×(P^2 \cdot C)}$ where $N=\frac{H}{4} \cdot \frac{W}{4}$, $P=4$ and $C=3$ ($X_p \in \mathbb{R}^{\frac{H}{4} \cdot \frac{W}{4} × 48}$ ). Afterwards a linear embedding layer is used to project the raw features into an arbitrary dimension $D$ ($X_{emb}=X_p \times E \in \mathbb{R}^{\frac{H}{4} \cdot \frac{W}{4} × D}$, where $E \in \mathbb{R}^{48 \times D}$ ). One important difference compared to [[Vision Transformer]]s is that no positional embeddings are added. The last step of State 1 (see image above) are several Swin Transformer Blocks, which are depicted on the right in the image above. The main difference to the standard [[Transformer#Transformer Block| Transformer Block]] is that the [[Transformer#Self-Attention in Transformers| standard multi-head self attention module]] is replaced by a shifted window based multi-head self attention module.

## Shifted Window based Self-Attention

The [[Transformer|standard Transformer architecture]] and its [[Vision Transformer|adaptation for image classification]] both conduct global self attention, where the relationships between a token and all other tokens are computed. The global computation leads to quadratic complexity with respect to the number of tokens, making it unsuitable for many vision problems requiring an immense set of tokens for dense prediction or to represent a high-resolution image.

An alternative is to compute self-attention within local windows. The windows are arranged to evenly partition the image in a non-overlapping manner. Supposing each window contains $M \times M$ patches, the computational complexity of a global multi-head self attention module (MSA) and a window based one (W-MSA) on an image of $H × W$ patches (*each pixel is one patch*) are:
$$
\begin{aligned}
\Omega(MSA) &= 4HWC^2 + 2(HW)^2C \\

\end{aligned}
$$


![[SwinTransformer_hierarchical_featue_maps.jpg|700]]
![[SwinTransformer_shifted_window.jpg|700]]