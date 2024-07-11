# SimMIM

SimMIM learns representations through masked image modeling, which masks a portion of the input image signals and predicts the original signals at the masked area. The framework consists of 4 main components:

- Masking Strategy,
- Encoder Architecture,
- Prediction Head,
- Prediction Target.
![[simmim.png]]

## Masking Strategy

Like in [[Masked Autoencoder (MAE)|MAEs]], masking is done at the patch level, but the patch size is larger at 32x32 pixels. Also similarly, each masked patch is replaced by a learnable mask token.

## Encoder Architecture

Any [[Vision Transformer|ViT]] based encoder can be used as long as the final patch size is 32x32 pixels.

> [!info]
> One important difference to [[Masked Autoencoder (MAE)]] and [[Fully Convolutional Masked Autoencoder (FCMAE)]] is that the encoder processes the mask tokens.

## Prediction Head

The prediction head is applied to the latent feature representation to produce a form of the original signals at the masked area. It can be of any form and capacity, as long as its input matches the encoder output and its output achieves the prediction target.

For example, on the 32× downsampled feature maps produced by a [[Swin Transformer]] encoder, a 1×1 convolution (linear) layer with a channel size (output dimension) of 3072 =32×32×3 is applied to represent the RGB values of 32×32 pixels.

> [!info]
> Heaver prediction heads were tested but fine tuning performance stayed about the same. This is similar to the results of [[Masked Autoencoder (MAE)]] and [[Fully Convolutional Masked Autoencoder (FCMAE)]].

> [!question]
> Relationship between decoder depth and linear probing performance? For [[Masked Autoencoder (MAE)]] one block seems fine for fine tuning but more are needed for linear probing.

## Prediction Target

Since pixel values are continuous in color space, a straightforward option is to predict the raw pixels of *only* the masked area by regression. Then, an $L_1$ loss is applied only to the masked pixels. $L_2$ and smooth $L_1$ loss work similarly well.

> [!info]
> Different from [[Masked Autoencoder (MAE)]] and [[Fully Convolutional Masked Autoencoder (FCMAE)]] as well. The decoder of the other two approaches predicts the whole image.

While both auto-encoders and masked image modeling approaches learn a network by recovering the original signals, they are based on different philosophies of *reconstructing visible signals* and *predicting invisible signals*. In this framework, a reconstruction task can be instantiated by also regressing the raw pixel values of visible patches in the input. But the approach that predicts only the masked area performs significantly better than the one that recovers all image pixels, 82.8% vs. 81.7%. This implies that the two tasks are fundamentally different in their mechanisms, and the prediction task may be a more promising approach for representation learning.
