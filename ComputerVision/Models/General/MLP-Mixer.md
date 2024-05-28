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


Mixer consists of multiple layers of identical size, and each layer consists of two MLP blocks. The first one is the token-mixing MLP: it acts on columns of $X$ (i.e. it is applied to a transposed input table $X$), maps $\mathbb{R}^S  \rightarrow \mathbb{R}^S$ , and is shared across all columns. The second one is the channel-mixing MLP: it acts on rows of $X$, maps $\mathbb{R}^C  \rightarrow \mathbb{R}^C$, and is shared across all rows.

![[mixer_figure.png]]

Each MLP block contains two fully-connected layers and a nonlinearity applied independently to each row of its input data tensor. Mixer layers can be written as follows (omitting layer indices):

$$
\begin{align}
U_{∗,i} &= X_{∗,i} + W_2 \sigma \Bigl( W_1 \text{LayerNorm}(X_{∗,i}) \Bigr), \text{ for i }= 1 … C, \\
Y_{j,∗} &= U_{j,∗} + W_4 \sigma \Bigl( W_3 \text{LayerNorm}(U_{j,∗}) \Bigr), \text{ for j }= 1 … S.
\end{align}
$$

Here $\sigma$ is an element-wise nonlinearity ([[GELU]]).

```python
from functools import partial

from einops.layers.torch import Rearrange, Reduce
from torch import nn

pair = lambda x: x if isinstance(x, tuple) else (x, x)


class PreNormResidual(nn.Module):
    def __init__(self, dim, fn):
        super().__init__()
        self.fn = fn
        self.norm = nn.LayerNorm(dim)

    def forward(self, x):
        return self.fn(self.norm(x)) + x


def FeedForward(dim, expansion_factor=4, dropout=0.0, dense=nn.Linear):
    inner_dim = int(dim * expansion_factor)
    return nn.Sequential(
        dense(dim, inner_dim),
        nn.GELU(),
        nn.Dropout(dropout),
        dense(inner_dim, dim),
        nn.Dropout(dropout),
    )


def MLPMixer(
    *,
    image_size,
    channels,
    patch_size,
    dim,
    depth,
    num_classes,
    expansion_factor=4,
    expansion_factor_token=0.5,
    dropout=0.0,
):
    image_h, image_w = pair(image_size)
    num_patches = (image_h // patch_size) * (image_w // patch_size)
    chan_first, chan_last = partial(nn.Conv1d, kernel_size=1), nn.Linear

    return nn.Sequential(
        Rearrange(
            "b c (h p1) (w p2) -> b (h w) (p1 p2 c)",
            p1=patch_size,
            p2=patch_size,
        ),
        nn.Linear((patch_size**2) * channels, dim),
        *[
            nn.Sequential(
                PreNormResidual(
                    dim,
                    FeedForward(
                        num_patches,
                        expansion_factor,
                        dropout,
                        chan_first,
                    ),
                ),
                PreNormResidual(
                    dim,
                    FeedForward(
                        dim,
                        expansion_factor_token,
                        dropout,
                        chan_last,
                    ),
                ),
            )
            for _ in range(depth)
        ],
        nn.LayerNorm(dim),
        Reduce("b n c -> b c", "mean"),
        nn.Linear(dim, num_classes),
    )

```
## Resources

- https://arxiv.org/pdf/2105.01601 (MLP-Mixer: An all-MLP Architecture for Vision)
- https://raw.githubusercontent.com/google-research/vision_transformer/
