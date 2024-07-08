# Masked Autoencoder (MAE)

Masked autoencoders (MAE) are scalable self-supervised learners for computer vision with a simple approach: mask random patches of the input image and reconstruct the missing pixels. It is based on two core designs. First, an asymmetric encoder-decoder architecture, with an encoder that operates only on the visible subset of patches (without mask tokens), and a lightweight decoder that reconstructs the original image from the latent representation and mask tokens.

![[masked_autoencoders.png]]

## Masking

First, a token is generated for each input patch (by linear projection with added positional embedding, analogous to [[Vision Transformer|ViT]]). Next, these tokens are randomly shuffled and the last part of the list is removed based on the masking ratio (i.e., the ratio of patches removed).

A ratio of 75% has been found to be good for both linear probing and fine tuning. A high masking ratio largely eliminates redundancy, creating a task that cannot be easily solved by extrapolation from visible neighboring patches, and instead promotes the learning of useful representations. Finally, the highly sparse input provides an opportunity to design an efficient encoder.

## Encoder

The encoder is a *vanilla* [[Vision Transformer|ViT]] that is only applied to unmasked patches. This allows very large encoders to be trained with a fraction of the computation and memory.

## Decoder

The decoder can be designed independently of the encoder design. What is required is that the input to the decoder is the full set of tokens consisting of (i) encoded visible patches and (ii) mask tokens. Each mask token is a shared, learned vector indicating the presence of a missing patch to be predicted. Before the full list of tokens is passed through the transformer blocks, the list is unshuffled and positional embeddings are added. Without this, the mask tokens would have no information about their location in the image.

The number of transformer blocks in the decoder depends on the task. While a sufficiently deep decoder is important for linear probing, a single block decoder can perform well with ﬁne tuning. Note that a single transformer block is the minimum requirement for propagating information from visible tokens to mask tokens. The final decoder has eight transformer blocks and thus <10% computation per token compared to the ViT-L encoder with its 24 blocks. This asymmetric design, where the full set of tokens is only processed by the lightweight decoder, significantly reduces pre-training time.

## Resources

- [[2111.06377] Masked Autoencoders Are Scalable Vision Learners (arxiv.org)](https://arxiv.org/abs/2111.06377)
- [GitHub - facebookresearch/mae: PyTorch implementation of MAE https//arxiv.org/abs/2111.06377](https://github.com/facebookresearch/mae)
