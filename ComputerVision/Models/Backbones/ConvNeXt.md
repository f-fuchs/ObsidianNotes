---
dg-publish: true
---

# ConvNeXt

ConvNeXt are a modernized version of [[Convolutional Neural Networks (CNN)|ConvNets]] based on the improvements of hierarchical [[Vision Transformer]]s ([[Swin Transformer]]). The first mayor performance increase is a result of an increased training recipe, inspired by [[Swin Transformer]] and [[Data-Efficient Image Transformers (DeiT)]]. The next performance increases where achieved by architectural changes and are as follows:

 - Changing the stage compute ratio to 1:1:9:1 analog to [[Swin Transformer]].
 - Replacing the stem cell consisting of a 7x7 convolution with stride 2 and a 2x2 max pool with a *Patchify* layer consisting of a 4x4 convolution with stride 4 (*both approaches downsample by four*).
![[convnext_architecture.png]]

## ConvNeXt Block

Additional performance gains were achieved by updating the [[ResNet]] block, as shown in the figure below. First, the 3x3 convolution layer of the ResNet block was replaced by a 7x7 [[Convolutional Layer|depthwise convolution]] and moved up. Due to the depthwise convolution, there is a clear separation between the mixing of spatial and of channel information, similar to [[Vision Transformer|ViT]]s with their attention and MLP layers. Additionally, due to the larger kernel size, the receptive field is larger. The computation cost stays similar though due to using a depthwise convolution.

The next changes are to the channel dimensions, see image below. The new ConvNeXt block uses an inverted bottleneck design, similar to [[Transformer]]s, where the MLP block is four times wider than the input dimension. This step, together with the moving up of the depthwise convolution layer, mirrors the design of [[Transformer]]s where the MSA block is placed prior to the MLP layers. This is a natural design choice because the complex modules (MSA, large-kernel conv) will have fewer channels, while the efficient modules (1x1 conv, MLP) have more channels.
![[convnext_block.png]]

## Resources

- [GitHub - facebookresearch/ConvNeXt: Code release for ConvNeXt model](https://github.com/facebookresearch/ConvNeXt?tab=readme-ov-file)
- [GitHub - facebookresearch/ConvNeXt-V2: Code release for ConvNeXt V2 model](https://github.com/facebookresearch/ConvNeXt-V2)
- [(PDF) Large-scale individual building extraction from open-source satellite imagery via super-resolution-based instance segmentation approach (researchgate.net)](https://www.researchgate.net/publication/365870304_Large-scale_individual_building_extraction_from_open-source_satellite_imagery_via_super-resolution-based_instance_segmentation_approach)
