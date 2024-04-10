---
theme: moon
width: 1920
height: 1080
---

## Segment Everything Everywhere All at Once 


Fabian Fuchs

---
<!-- slide template="[[tpl-title-text]]" -->
::: title
## Segmentation
:::

::: text
Segmentation can be divided into three types:
 - Generic Segmentation: Segment image without any prompt. This can be further divided into:
	- Semantic Image Segmentation
	- Instance Image Segmentation
	- Panoptic Segmentation
 - Referring Segmentation: Segment image with a textual or visual prompt.
 - Interactive Segmentation: Segment image with user interaction (can be iterative)
 :::
 note: The model was trained on panoptic segmentation, referring segmentation, and interactive segmentation and evaluated on generic segmentation (instance/panoptic/semantic), referring segmentation, and interactive segmentation. Segment image with a visual prompt, including points, boxes, scribbles and masks, which can further generalize to a different referring image

---
<!-- slide template="[[tpl-con-2-1-box]]" -->

::: title
#### Semantic Image Segmentation
:::

::: left
![[cityscape_semantic.png|1100]]
:::

::: right
Label semantic categories independent of distinct objects.
:::

::: source
http://deepscene.cs.uni-freiburg.de/index.html
:::
note: Semantic image segmentation is the technique that involves detecting objects within an image and grouping them based on defined categories. Which is simply labeling each pixel of an image with a corresponding class of what is being represented. http://deepscene.cs.uni-freiburg.de/index.html

---
<!-- slide template="[[tpl-con-2-1-box]]" -->

::: title
#### Instance Image Segmentation
:::

::: right
Label distinct objects independent of semantic categories.
:::

::: left
![[cityscape_instance.png|1100]]
:::

::: source
https://segment-anything.com/demo#
:::
note: Instance segmentation consists of the localization of specific objects based on the association of their belonging pixels. used by the Segment Anything Model (SAM). https://segment-anything.com/demo#

---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
#### Panoptic Segmentation
:::

::: right
Label distinct objects but keep category association.
:::

::: left
![[cityscape_panoptic.png|1100]]
:::

::: source
http://semantic-sam.xyzou.net:6090/
:::

note:Panoptic Segmentation is a computer vision task that combines semantic segmentation and instance segmentation to provide a comprehensive understanding of the scene. The goal of panoptic segmentation is to segment the image into semantically meaningful parts or regions, while also detecting and distinguishing individual instances of objects within those regions. In a given image, every pixel is assigned a semantic label, and pixels belonging to "things" classes (countable objects with instances, like cars and people) are assigned unique instance IDs. used by SEEM: Segment Everything Everywhere All At Once. http://semantic-sam.xyzou.net:6090/

---
<!-- slide template="[[tpl-title-image]]" -->

::: title
#### Comparison of Generic Segmentation
:::

::: left
<split even gap="1">
![[cityscape.png|500]]
![[cityscape_semantic.png|500]]
</split>
<split even gap="1">
![[cityscape_instance.png|500]]
![[cityscape_panoptic.png|500]]
</split>
:::

---
<!-- slide template="[[tpl-con-2-1-box]]" -->

::: title
## Model
:::

::: right
*SEEM* uses a generic encoder-decoder architecture. 
:::

::: left
![[SEEM.svg|1300]]
:::

---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Image Encoder
:::

::: left
<split even gap="1">
![Focal Transformer|600](https://github.com/microsoft/Focal-Transformer/raw/main/figures/focal-transformer-teaser.png)
![Dual Attention Vision Transformer|600](https://github.com/dingmyu/davit/raw/main/figures/teaser.png)
</split>
:::

::: right
The image encoder is either a [[Focal Transformer]] or a [[Dual Attention Vision Transformer]].
:::

note: focal transformer in smallest model, dual attention vision transformer in both bigger model.

---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Text Encoder
:::

::: left
<split even gap="1">
![Focal Transformer|600](https://github.com/microsoft/Focal-Transformer/raw/main/figures/focal-transformer-teaser.png)
![Dual Attention Vision Transformer|600](https://github.com/dingmyu/davit/raw/main/figures/teaser.png)
</split>
:::

::: right
The text encoder is Transformer Encoder and uses *Unified Contrastive Learning in Image-Text-Label Space* (UniCL) to combine image and text data into the joint *Image-Text Representation Space*.
:::

::: source
https://github.com/microsoft/UniCL
:::
note: focal transformer in smallest model, dual attention vision transformer in both bigger model.

---
<!-- slide template="[[tpl-title-text]]" -->

::: title
## Resources
:::

::: text
Resources used to create this presentation:
- https://arxiv.org/pdf/2304.06718.pdf (Original Paper)
- https://github.com/UX-Decoder/Segment-Everything-Everywhere-All-At-Once/tree/v1.0 (Official GitHub)
- http://semantic-sam.xyzou.net:6090/ (SEEM Demo)
- https://segment-anything.com/demo# (SAM Demo)
- http://deepscene.cs.uni-freiburg.de/index.html (DeepScene Demo)
:::