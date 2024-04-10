---
theme: moon
width: 1920
height: 1080
---

## Segment Everything Everywhere All at Once 


Fabian Fuchs

---
## Segmentation

Three types of segmentation:
 - generic segmentation
 - referring segmentation
 - interactive segmentation
note: The model was trained on panoptic segmentation, referring segmentation, and interactive segmentation and evaluated on generic segmentation (instance/panoptic/semantic), referring segmentation, and interactive segmentation.
---
### Generic  segmentation

Generic segmentation segments the image without any prompts. Can be further divided into:
- Semantic Image Segmentation
- Instance Image Segmentation
- Panoptic Segmentation

---
<!-- slide template="[[tpl-con-2-1-box]]" -->

::: title
#### Semantic Image Segmentation
:::

::: left
![[cityscape_semantic.png|1200]]
:::

::: right
Label semantic categories independent of distinct objects.
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
![[cityscape_instance.png|1200]]
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
![[cityscape_panoptic.png|1200]]
:::

note:Panoptic Segmentation is a computer vision task that combines semantic segmentation and instance segmentation to provide a comprehensive understanding of the scene. The goal of panoptic segmentation is to segment the image into semantically meaningful parts or regions, while also detecting and distinguishing individual instances of objects within those regions. In a given image, every pixel is assigned a semantic label, and pixels belonging to "things" classes (countable objects with instances, like cars and people) are assigned unique instance IDs. used by SEEM: Segment Everything Everywhere All At Once. http://semantic-sam.xyzou.net:6090/

---
<!-- slide template="[[tpl-title-image]]" -->

::: title
#### Comparison
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

### Referring segmentation

Segment image with a given prompt can be either a text or visual prompt or both.

### Text referring segmentation

Segment image with a text prompt.

### Visual referring segmentation

Segment image with a visual prompt, including points, boxes, scribbles and masks, which can
further generalize to a different referring image

---

### Interactive segmentation

Segment objects of interest by simply clicking or drawing a scribble on the input image.

---
## Model

*SEEM* uses a generic encoder-decoder architecture. 
![[SEEM.svg|700]]

---

The image encoder is either a [[Focal Transformer]] or a [[Dual Attention Vision Transformer]].


## Resources
- Paper: https://arxiv.org/pdf/2304.06718.pdf
- GitHub: https://github.com/facebookresearch/segment-anything