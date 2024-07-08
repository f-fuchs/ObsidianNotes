# Masked Autoencoder (MAE)

Masked autoencoders (MAE) are scalable self-supervised learners for computer vision with a simple approach: mask random patches of the input image and reconstruct the missing pixels. It is based on two core designs. First, an asymmetric encoder-decoder architecture, with an encoder that operates only on the visible subset of patches (without mask tokens), and a lightweight decoder that reconstructs the original image from the latent representation and mask tokens.

![[masked_autoencoders.png]]

## Masking

First, a token is generated for each input patch (by linear projection with added positional embedding, analogous to [[Vision Transformer|ViT]]). Next, these tokens are randomly shuffled and the last part of the list is removed based on the masking ratio (i.e., the ratio of patches removed).

A ratio of 75% has been found to be good for both linear probing and fine tuning. A high masking ratio largely eliminates redundancy, creating a task that cannot be easily solved by extrapolation from visible neighboring patches, and instead promotes the learning of useful representations. Finally, the highly sparse input provides an opportunity to design an efficient encoder.

## Encoder

The encoder is a *vanilla* [[Vision Transformer|ViT]] that is only applied to unmasked patches. This allows very large encoders to be trained with a fraction of the computation and memory.
## Decoder

## Resources

- [[2111.06377] Masked Autoencoders Are Scalable Vision Learners (arxiv.org)](https://arxiv.org/abs/2111.06377)
