
DEtection TRansformer (DETR) is a model for [[Glossary#Object Detection|Object Detection]]. It uses an encoder-decoder architecture wit a [[CNN]] based encoder, a [[Transformer Encoder]] as decoder and a simple [[Feedforward Neural Network (FNN)|FNN]] that makes the final detection prediction. 

![[DETR.png|700]]

## Transformer Encoder

The decoder first applies a 1x1 convolution to reduces the channel dimension of the features from the [[CNN]] backbone. Afterwards the  spatial dimensions  of the features  $f \in \mathbb{R}^{C\times W \times D}$ are collapsed into one dimension, resulting in a features of dimension $C\times W \cdot D$ . Finally,  since the
transformer architecture is permutation-invariant, we supplement it with fixed
positional encodings that are added to the input of each attention layer. 