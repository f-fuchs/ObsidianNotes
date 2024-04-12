
DEtection TRansformer (DETR) is a model for [[Glossary#Object Detection|Object Detection]]. It uses an encoder-decoder architecture wit a [[CNN]] based vision backbone, a [[Transformer Encoder]] as encoder, a modified [[Transformer Decoder]] and a simple [[Feedforward Neural Network (FNN)|FNN]] that makes the final detection prediction. 

![[DETR.png]]

## Vision Backbone

Starting from the initial image $x_{img} \in \mathbb{R}^{3\times H_0 \times W_0}$ (with 3 color
channels), a conventional CNN backbone generates a lower-resolution activation
map $f \in \mathbb{R}^{C\times H \times W}$.

## Transformer Encoder & Decoder

The decoder first applies a 1x1 convolution to reduces the channel dimension of the features from the [[CNN]] backbone. Afterwards the  spatial dimensions  of the features  $f \in \mathbb{R}^{d\times H \times W}$ are collapsed into one dimension, resulting in a features of dimension $d\times H \cdot W$ . Finally,  since the
transformer architecture is permutation-invariant, we supplement it with fixed
positional encodings that are added to the input of each attention layer. 

![[DETR_Decoder.png]]

The decoder follows the standard architecture of the transformer, transforming $H \cdot W$ embeddings of size $d$ using multi-headed self- and encoder-decoder attention mechanisms. The difference with the original transformer is that all the embeddings are decoded in parallel at each decoder layer,
while the original [[Transformer Decoder]] uses an autoregressive model that predicts the output sequence one element at a time. 

Since the decoder is also permutation-invariant, the input embeddings must be different to produce different results. These input embeddings are learnt positional encodings that are  referred to as object queries, and similarly to the encoder, are added to the input of each attention layer.
The decoder receives queries (initially set to zero), output positional encoding (object queries), and encoder memory, and produces the final set of predicted class labels and bounding boxes through multiple multihead self-attention and decoder-encoder attention.