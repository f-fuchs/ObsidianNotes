---
dg-publish: true
---

# ConvNeXt

ConvNeXt are a modernized version of [[Convolutional Neural Networks (CNN)|ConvNets]] based on the improvements of hierarchical [[Vision Transformer]]s ([[Swin Transformer]]). The first mayor performance increase is a result of an increased training recipe, inspired by [[Swin Transformer]] and [[Data-Efficient Image Transformers (DeiT)]]. The next performance increases where achieved by architectural changes and are as follows:

 - Changing the stage compute ratio to 1:1:9:1 analog to [[Swin Transformer]].
 - Replacing the stem cell consisting of a 7x7 convolution with stride 2 and a 2x2 max pool with a *Patchify* layer consisting of a 4x4 convolution with stride 4 (*both approaches downsample by four*).
 - Creation of separate downsampling layers, consisting of a [[Normalization Layers#Layer Norm|layer norm]] and a 2x2 conv with stride 2
![[convnext_architecture.png]]

## ConvNeXt Block

Additional performance gains were achieved by updating the [[ResNet]] block, as shown in the figure below. First, the 3x3 convolution layer of the ResNet block was replaced by a 7x7 [[Convolutional Layer|depthwise convolution]] and moved up. Due to the depthwise convolution, there is a clear separation between the mixing of spatial and of channel information, similar to [[Vision Transformer|ViT]]s with their attention and MLP layers. Additionally, due to the larger kernel size, the receptive field is larger. The computation cost stays similar though due to using a depthwise convolution.

The next changes are to the channel dimensions, see image below. The new ConvNeXt block uses an inverted bottleneck design, similar to [[Transformer]]s, where the MLP block is four times wider than the input dimension. This step, together with the moving up of the depthwise convolution layer, mirrors the design of [[Transformer]]s where the MSA block is placed prior to the MLP layers. This is a natural design choice, as the complex modules (MSA, large-kernel conv) will have fewer channels, while the efficient modules (1x1 conv, MLP) will have more channels.
![[convnext_block.png]]
The last changes are to the activation functions and normalization layers. First, replacing [[ReLU]] with [[GELU]] and reducing the number of activation functions to just one between the 1x1 conv layers. Second, replacing [[Normalization Layers#Batch Norm|batch norm]] with [[Normalization Layers#Layer Norm|layer norm]] and also reducing the number of normalization layers as well to just one prior the two 1x1 conv layers.

## ConvNeXt V2

Building on the success of ConvNeXt the authors have released an updated version of the model. The first change was again to the training regimen. This time switching from supervised training to self-supervised training by designing a [[Fully Convolutional Masked Autoencoder (FCMAE)]] inspired by [[Masked Autoencoder (MAE)]] training for [[Transformer]]s.

However, training the ConvNeXt V1 in this way resulted in feature collapse, i.e. there were many dead or saturated feature maps and activation became redundant across channels. In the figure below, the feature cosine distance is plotted and the severe feature collapse behaviour of the ConvNeXt V1 FCMAE pre-trained model can be observed. The supervised model also shows a reduction in feature diversity, but only in the final layers. This decrease in diversity in the supervised model is likely due to the use of cross-entropy loss, which encourages the model to focus on class-discriminative features while suppressing the others.
![[convnext_feature_collapse.png]]
To combat this feature collapse ConvNeXt V2 introduces Global Response Normalization.

### Global Response Normalization (GRN)

Given an input feature, $X \in \mathbb{R}^{H×W×C}$, the proposed GRN unit consists of three
steps:

1. global feature aggregation,
2. feature normalization,
3. feature calibration.

#### Global Feature Aggregation

To aggregate a spatial feature map $X_i$ into a vector $gx$ the global function $G(X) := X \in \mathbb{R}^{H \times W \times C} \rightarrow gx \in \mathbb{R}^{C}$ is used. This can be viewed as a simple pooling layer. Concretely, a norm-based feature aggregation, specifically the $L2$-norm is used. This results in a set of aggregated values $G(X) = gx = \begin{bmatrix}||X_1||_2 \\ ||X_2||_2\\ … \\ ||X_C||_2\end{bmatrix} \in \mathbb{R}^{C}$, where $||X_i||_2$ is a scalar that aggregates the statistics of the i-th channel.

#### Feature Normalization

Next, a response normalization function $N(·)$ is applied to the aggregated values. Concretely, we use a standard divisive normalization as follows:

$$
N(||X_i||_2) := ||X_i|| \in \mathbb{R} \rightarrow \frac{||X_i||}
j=1,…,C ||Xj||
∈ R
$$

## Resources

- [GitHub - facebookresearch/ConvNeXt: Code release for ConvNeXt model](https://github.com/facebookresearch/ConvNeXt?tab=readme-ov-file)
- [GitHub - facebookresearch/ConvNeXt-V2: Code release for ConvNeXt V2 model](https://github.com/facebookresearch/ConvNeXt-V2)
- [(PDF) Large-scale individual building extraction from open-source satellite imagery via super-resolution-based instance segmentation approach (researchgate.net)](https://www.researchgate.net/publication/365870304_Large-scale_individual_building_extraction_from_open-source_satellite_imagery_via_super-resolution-based_instance_segmentation_approach)
