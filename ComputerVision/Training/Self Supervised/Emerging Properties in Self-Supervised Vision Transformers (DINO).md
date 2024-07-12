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

| ![[dino_overview.png]]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Self-distillation with no labels. We illustrate DINO in<br>the case of one single pair of views (x1, x2) for simplicity. The<br>model passes two different random transformations of an input<br>image to the student and teacher networks. Both networks have<br>the same architecture but different parameters. The output of the<br>teacher network is centered with a mean computed over the batch.<br>Each networks outputs a K dimensional feature that is normalized<br>with a temperature softmax over the feature dimension. Their<br>similarity is then measured with a cross-entropy loss. We apply a<br>stop-gradient (sg) operator on the teacher to propagate gradients<br>only through the student. The teacher parameters are updated with<br>an exponential moving average (ema) of the student parameters. |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <br><br><br><br><br><br>````python<br># gs, gt: student and teacher networks# C: center (K)<br># tps, tpt: student and teacher temperatures<br># l, m: network and center momentum rates<br>gt.params = gs.params<br>for x in loader: # load a minibatch x with n samples<br>	x1, x2 = augment(x), augment(x) # random views<br>	s1, s2 = gs(x1), gs(x2) # student output n-by-K<br>	t1, t2 = gt(x1), gt(x2) # teacher output n-by-K<br>	loss = H(t1, s2)/2 + H(t2, s1)/2<br>	loss.backward() # back-propagate<br>	# student, teacher and center updates<br>	update(gs) # SGD<br>	gt.params = l*gt.params + (1-l)*gs.params<br>	C = m*C + (1-m)*cat([t1, t2]).mean(dim=0)<br>	<br>def H(t, s):<br>	t = t.detach() # stop gradient<br>	s = softmax(s / tps, dim=1)<br>	t = softmax((t - C) / tpt, dim=1) # center + sharpen<br>	return - (t * log(s)).sum(dim=1).mean()<br>````<br><br><br><br><br><br><br><br><br><br><br><br><br><br> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |


```python
# gs, gt: student and teacher networks# C: center (K)
# tps, tpt: student and teacher temperatures
# l, m: network and center momentum rates
gt.params = gs.params
for x in loader: # load a minibatch x with n samples
	x1, x2 = augment(x), augment(x) # random views
	s1, s2 = gs(x1), gs(x2) # student output n-by-K
	t1, t2 = gt(x1), gt(x2) # teacher output n-by-K
	loss = H(t1, s2)/2 + H(t2, s1)/2
	loss.backward() # back-propagate
	# student, teacher and center updates
	update(gs) # SGD
	gt.params = l*gt.params + (1-l)*gs.params
	C = m*C + (1-m)*cat([t1, t2]).mean(dim=0)
	
def H(t, s):
	t = t.detach() # stop gradient
	s = softmax(s / tps, dim=1)
	t = softmax((t - C) / tpt, dim=1) # center + sharpen
	return - (t * log(s)).sum(dim=1).mean()
```
## Resources

- [GitHub - facebookresearch/dino: PyTorch code for Vision Transformers training with the Self-Supervised learning method DINO](https://github.com/facebookresearch/dino?tab=readme-ov-file)
- [[2104.14294] Emerging Properties in Self-Supervised Vision Transformers (arxiv.org)](https://arxiv.org/abs/2104.14294)
