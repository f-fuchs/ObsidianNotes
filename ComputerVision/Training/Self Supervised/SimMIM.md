# SimMIM

SimMIM learns representations through masked image modeling, which masks a portion of the input image signals and predicts the original signals at the masked area. The framework consists of 4 main components:
![[simmim.png]]

## Masking Strategy

Like in [[Masked Autoencoder (MAE)|MAEs]], masking is done at the patch level, but the patch size is larger at 32x32 pixels. Also similarly, each masked patch is replaced by a learnable mask token.

## Encoder Architecture

Any [[Vision Transformer|ViT]] based encoder can be used as long as the final patch size is 32x32 pixels.

> [!info]
> One important difference to [[Masked Autoencoder (MAE)]] and [[Fully Convolutional Masked Autoencoder (FCMAE)]] is that the encoder processes the mask tokens.

## Prediction Head

The prediction head is applied to the latent feature representation to produce a form of the original signals at the masked area. It can be of any form and capacity, as long as its input matches the encoder output and its output achieves the prediction target.

To predict all pixel values at a full resolution of input images, we map each feature vector in the feature map back to the original resolution and let that vector do the prediction of the corresponding raw pixels. For example, on the 32× downsampled feature maps produced by a [[Swin Transformer]] encoder, we apply a 1×1 convolution (linear) layer with a channel size (an output dimension) of 3072 =32×32×3 to represent the RGB values of 32×32 pixels.
