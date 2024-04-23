
DEtection TRansformer (DETR) is a model for [[Object Detection#Object Detection|Object Detection]]. It uses an encoder-decoder architecture wit a [[Convolutional Neural Networks (CNN)]] based vision backbone, a [[Transformer Encoder]] as encoder, a modified [[Transformer Decoder]] and a simple [[Feedforward Neural Network (FNN)|FNN]] that makes the final detection prediction. 

![[DETR.png]]

## Vision Backbone

Starting from the initial image $x_{img} \in \mathbb{R}^{3\times H_0 \times W_0}$ (with 3 color channels), a conventional CNN backbone generates a lower-resolution activation map $f \in \mathbb{R}^{C\times H \times W}$.

## Transformer Encoder & Decoder

The decoder first applies a 1x1 convolution to reduces the channel dimension of the features from the [[Convolutional Neural Networks (CNN)]] backbone. Afterwards the  spatial dimensions  of the features  $f \in \mathbb{R}^{d\times H \times W}$ are collapsed into one dimension, resulting in a features of dimension $d\times H \cdot W$ . Finally,  since the transformer architecture is permutation-invariant, we supplement it with fixed positional encodings that are added to the input of each attention layer. 

![[DETR_Decoder.png]]

The decoder follows the standard architecture of the transformer, transforming $K$ embeddings of size $d$ using multi-headed self- and encoder-decoder attention mechanisms. The difference with the original transformer is that all the embeddings are decoded in parallel at each decoder layer,
while the original [[Transformer Decoder]] uses an autoregressive model that predicts the output sequence one element at a time. Since the decoder is also permutation-invariant, the input embeddings must be different to produce different results. These input embeddings are learnt positional encodings that are referred to as object queries, and similarly to the encoder, are added to the input of each attention layer.

Query, Key and Value for the second Attention Layer:
$$
\begin{aligned}
Q & \coloneqq \text{Object Queries + Output from first Attention Layer} \in \mathbb{R}^{K \times d} \\
K & \coloneqq \text{Spatial Positional Encoding + Encoder Memory} \in \mathbb{R}^{H \cdot W \times d} \\
V & \coloneqq \text{Encoder Memory} \in \mathbb{R}^{H \cdot W \times d} \\
Q K^T &\in \mathbb{R}^{K \times H \cdot W} \\
(Q K^T) V &\in \mathbb{R}^{K \times d}
\end{aligned} 
$$

In the cross-attention modules, object queries extract features from the feature maps and in the self-attention modules, object queries interact with each other, so as to capture their relations. 
## FNN

The output of the decoder gets fed into two [[Feedforward Neural Network (FNN)|FNNs]], one to predict the *class* and one to predict the bounding box, consisting of the normalized center coordinates, height and width of the box. Since a fixed-size set of $H \cdot W$  bounding boxes, where $H \cdot W$ is usually much larger than the
actual number of objects of interest in an image are predicted, an additional special class la-
bel ∅ is used to represent that no object is detected within a slot. 

## Resources
- https://arxiv.org/pdf/2005.12872.pdf
- https://amaarora.github.io/posts/2021-07-26-annotateddetr.html#the-detr-architecture
- https://github.com/facebookresearch/detr