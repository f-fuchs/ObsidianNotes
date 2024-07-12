# Emerging Properties in Self-Supervised Vision Transformers (DINO)

DINO is a simple self-supervised training method, which can be interpreted as a form of self-
*di*stillation with *no* labels. 


Self-supervised ViT features contain explicit information about the semantic segmentation of an image, which does not emerge as clearly with supervised [[Vision Transformer|ViT]]s or [[Convolutional Neural Networks (CNN)|ConvNets]]. The features include the scene layout and, in particular, object boundaries, as shown in the image below. This information is directly accessible in the self-attention modules of the last block. The emergence of these semantic segmentation masks seems to be a property shared across self-supervised methods.

|                                                                                                      ![[dino_attention_maps.png]]                                                                                                       |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Self-attention of the [CLS] token on the heads of the last layer of a ViT with 8 × 8 patches trained with DINO. These maps show that the model automatically learns class-specific features, allowing unsupervised object segmentation. |

Furthermore, by adding certain components such as a momentum encoder and multi-crop augmentations to the self-supervised training pipeline, the performance with only a k-NN classifier reaches 78.3% top-1 on ImageNet with a small ViT.
![[dino.gif]]

## Resources

- [GitHub - facebookresearch/dino: PyTorch code for Vision Transformers training with the Self-Supervised learning method DINO](https://github.com/facebookresearch/dino?tab=readme-ov-file)
- [[2104.14294] Emerging Properties in Self-Supervised Vision Transformers (arxiv.org)](https://arxiv.org/abs/2104.14294)
