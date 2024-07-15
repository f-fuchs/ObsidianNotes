# Emerging Properties in Self-Supervised Vision Transformers (DINO)

Self-supervised ViT features contain explicit information about the semantic segmentation of an image, which does not emerge as clearly with supervised [[Vision Transformer|ViT]]s or [[Convolutional Neural Networks (CNN)|ConvNets]]. The features include the scene layout and, in particular, object boundaries, as shown in the image below. This information is directly accessible in the self-attention modules of the last block. The emergence of these semantic segmentation masks seems to be a property shared across self-supervised methods.

|                                                                                                      ![[dino_attention_maps.png]]                                                                                                       |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Self-attention of the [CLS] token on the heads of the last layer of a ViT with 8 × 8 patches trained with DINO. These maps show that the model automatically learns class-specific features, allowing unsupervised object segmentation. |

Furthermore, by adding certain components such as a momentum encoder and multi-crop augmentations to the self-supervised training pipeline, the performance with only a k-NN classifier reaches 78.3% top-1 on ImageNet with a small ViT.

## Overall Framework

DINO is a simple self-supervised training method that can be interpreted as a form of knowledge distillation with no labels. It simpliﬁes self-supervised training by directly predicting the output of a teacher network. The overall process is illustrated in the GIF below.

|                ![[dino.gif]]                |
|:-------------------------------------------:|
| Illustration of the DINO training workflow. |

### Mathematical Formulation

Knowledge distillation is a learning paradigm where a student network $g_{\theta_s}$ is trained
to match the output of a given teacher network $g_{\theta_t}$ , parameterized by $\theta_s$ and $\theta_t$ respectively.
Given an input image $X$, both networks output probability distributions over $K$ dimensions denoted by $P_s$ and $P_t$. The probability $P$ is obtained by normalizing the output of the network $g$ with a softmax function. More precisely,

$$
P_s(x)^{(i)} = \frac{\exp \left(\frac{g_{\theta_s}(x)^{(i)}}{\tau_s}\right)}{\sum_{k=1}^K \exp \left(\frac{g_{\theta_s}(x)^{(k)}}{\tau_s}\right)}
,
$$

with $\tau_s > 0$ a temperature parameter that controls the sharpness of the output distribution and $i$ is the channel number. The formula for $P_t$ is analogous with temperature $\tau_t$.

The loss function is a kind of cross-entropy loss defined as:

$$
\min_{\theta_s} \sum_{X \in {X_1^g, X_2^g}} \left( - \sum_{X^{´} \in V \wedge X^{´} \ne X}  P_t(X) \log \left((P_s(X^´) \right) \right),
$$

where $V$ is a set of different views with two global views $X_1^g , X_2^g$ and several local views of smaller resolution. As the definition specifies, all views are passed through the student, while only the global views pass through the teacher, thus encouraging "local-to-global" correspondences. The standard setting for multi-crop with 2 global views at resolution $224^2$ covering a large (for example greater than 50%) area of the original image, and several local views of resolution $96^2$ covering only small areas (for example less than 50%) of the original image is used.

> [!question]
> why condition $X^{´} \ne X$ in the second sum? why not show student and teacher the same view
> -> very small loss and therefore insignificant training and basically waste of resources?

While the student is trained directly via stochastic gradient descent the teacher network is trained using an exponential moving average (EMA), i.e. a momentum encoder. The update rule is
$\theta_t ← \lambda \theta_t + (1 − \lambda)\theta_s$, with $λ$ following a cosine schedule from $0.996$ to $1$ during training. Due to this the teacher has a better performance than the student throughout the training and therefore guides the student's training by providing target features of higher quality.

Finally, to prevent model collapse, centering and sharpening are applied to the output of the teacher network. Centering prevents one dimension from dominating but encourages collapse to a uniform distribution, while sharpening has the opposite effect. Applying both operations balances their effects. Choosing this method over batch normalizations trades stability for less dependence over the batch: the centering operation only depends on ﬁrst-order batch statistics and can be interpreted as adding a bias term $c$ to the output of the teacher $g$: $g_t(x) ← g_t(x) +c$.
The center $c$ is updated with an exponential moving average, which allows the approach to work
well across different batch sizes:

$$
c ← mc + (1-m) \frac{1}{B} \sum_{i=1}^{B} g_{\theta_t}(X_i),
$$

where $m \gt 0$ is a rate parameter and $B$ is the batch size. Output sharpening is simply obtained by using a low value for the temperature $\tau_t$ in the teacher softmax normalization.

### Example

| ![[dino_overview.png\|340]]![[dino_algorithm1.png\|340]]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Self-distillation with no labels. We illustrate DINO in the case of one single pair of views (x1, x2) for simplicity. The model passes two different random transformations of an input image to the student and teacher networks. Both networks have the same architecture but different parameters. The output of the teacher network is centered with a mean computed over the batch. Each networks outputs a K dimensional feature that is normalized with a temperature softmax over the feature dimension. Their similarity is then measured with a cross-entropy loss. We apply a stop-gradient (sg) operator on the teacher to propagate gradients only through the student. The teacher parameters are updated with an exponential moving average (ema) of the student parameters. |

## Resources

- [GitHub - facebookresearch/dino: PyTorch code for Vision Transformers training with the Self-Supervised learning method DINO](https://github.com/facebookresearch/dino?tab=readme-ov-file)
- [[2104.14294] Emerging Properties in Self-Supervised Vision Transformers (arxiv.org)](https://arxiv.org/abs/2104.14294)
