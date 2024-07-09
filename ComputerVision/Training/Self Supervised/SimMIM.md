# SimMIM

SimMIM learns representations through masked image modeling, which masks a portion of the input image signals and predicts the original signals at the masked area. The framework consists of 4 main components:

## Masking Strategy

Like in [[Masked Autoencoder (MAE)|MAEs]], masking is done at the patch level, but the patch size is larger at 32x32 pixels. Also similarly, each masked patch is replaced by a learnable mask token.

## Encoder Architecture
