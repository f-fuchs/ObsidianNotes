---
theme: moon
width: "1920"
height: "1080"
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
	- Semantic Image Segmentation: Label semantic categories independent of distinct objects.
	- Instance Image Segmentation: Label distinct objects independent of semantic categories.
	- Panoptic Segmentation
 - Referring Segmentation: Segment image with a textual or visual prompt.
 - Interactive Segmentation: Segment image with user interaction (can be iterative)
 :::
 note: The model was trained on panoptic segmentation, referring segmentation, and interactive segmentation and evaluated on generic segmentation (instance/panoptic/semantic), referring segmentation, and interactive segmentation. Segment image with a visual prompt, including points, boxes, scribbles and masks, which can further generalize to a different referring image

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

::: source
http://deepscene.cs.uni-freiburg.de/index.html, https://segment-anything.com/demo#, http://semantic-sam.xyzou.net:6090/
:::

note: 
- Semantic image segmentation is the technique that involves detecting objects within an image and grouping them based on defined categories. Which is simply labeling each pixel of an image with a corresponding class of what is being represented. http://deepscene.cs.uni-freiburg.de/index.html
- Instance segmentation consists of the localization of specific objects based on the association of their belonging pixels. used by the Segment Anything Model (SAM). https://segment-anything.com/demo#
- Panoptic Segmentation is a computer vision task that combines semantic segmentation and instance segmentation to provide a comprehensive understanding of the scene. The goal of panoptic segmentation is to segment the image into semantically meaningful parts or regions, while also detecting and distinguishing individual instances of objects within those regions. In a given image, every pixel is assigned a semantic label, and pixels belonging to "things" classes (countable objects with instances, like cars and people) are assigned unique instance IDs. used by SEEM: Segment Everything Everywhere All At Once. http://semantic-sam.xyzou.net:6090/

---
<!-- slide template="[[tpl-con-2-1-box]]" -->

::: title
## Model
:::

::: right
*SEEM* uses a generic encoder-decoder architecture.  
The encoder encompasses the: 
- Image Encoder,
- Text Encoder,
- Visual Sampler,

and the decoder consists of:
- cross-attention of the queries with the image features,
- self-attention of the queries and prompts,
- a pixel decoder and transformer decoder to generate mask and class embeddings.
:::

::: left
<grid drag="100 100" drop="center">
![[SEEM.svg|900]]
</grid>
:::

::: source
https://arxiv.org/pdf/2304.06718.pdf
:::

---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Image Encoder and Text Encoder
:::

::: left
![Focal Transformer|900](https://github.com/microsoft/Focal-Transformer/raw/main/figures/focal-transformer-teaser.png)


![Dual Attention Vision Transformer|900](https://github.com/dingmyu/davit/raw/main/figures/teaser.png)
:::

::: right
The image encoder is either a [[Focal Transformer]] or a [[Dual Attention Vision Transformer]] and the Text Encoder is a Transformer Encoder.

$\Rightarrow Z = ImageEncoder(I), I\in \mathbb{R}^{H \times W \times 3}$ 

$\Rightarrow P_t=TextEncoder(T)$
:::

::: source
https://github.com/microsoft/Focal-Transformer    
https://github.com/dingmyu/davit
:::

note: focal transformer in smallest model, dual attention vision transformer in both bigger model. in the configs on github additionally ViT is used as image encoder and CLIP as text encoder

---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Combine Image and Text Encodings into Image-Text Representation Space
:::

::: left
<split even gap="1">
![[UniCL.svg|450]]
![[UniCL_algorithm.svg|450]]
</split>
:::

::: right
To combine the image and text encoding into a shared feature space *Unified Contrastive Learning in Image-Text-Label Space* (UniCL) is used.

$\Rightarrow$ allows Zero-Shot Image Classification

 $\Rightarrow$ improves Linear-Probing, Fine-Tuning and Transfer Learning
:::

::: source
https://github.com/microsoft/UniCL,    
https://arxiv.org/pdf/2204.03610.pdf
:::
note: combine feature spaces by transposing image space and multiplying with textual space. train image and text encoder together via shared loss. Linear probing holds the model fixed, and you train a small model on top of it that takes the features and produces a label for your task.

---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Visual Sampler
:::

::: left
<grid drag="100 100" drop="center">
![[SEEM_VisualSampler.png|900]]
</grid>
:::
::: right
The Visual Sampler generates the visual prompts given the feature maps of the target or referred image $\hat{Z}$ and the sampling locations $s \in {points, box, scribbles, polygons}$ of the user.

$$
P_v = VisualSampler(s, \hat{Z})
$$

1. Extract the corresponding region from the image features through point sampling
2. Interpolate 512 point feature vectors uniformly from that region.
:::

::: source
https://arxiv.org/pdf/2304.06718.pdf
:::

note: 

---
<!-- slide template="[[tpl-title-text]]" -->
::: title
## SEEM-Decoder
:::

::: text
SEEM-Decoder predicts the masks $M$ and semantic concepts $C$ based on the query outputs $O^m_h$ (mask embeddings) and $O^c_h$ (class embeddings), which interact with text, visual, and memory prompts $⟨P_t, P_v , P_m⟩$:

</br>

$$
\begin{aligned}
⟨O^m_h, O^c_h⟩ &= Decoder(Q_h; ⟨P_t, P_v , P_m⟩|Z) \\\\
M &= MaskPredictor(O^m_h) \\\\
C &= ConceptClassifier(O^c_h)
\end{aligned}
$$
:::


note: 
---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Queries and prompt interaction
:::

::: left
![[SEEM_Decoder_Queries.PNG|900]]
:::
::: right
Training:
- $Q_h$ is duplicated for generic, referring, and interactive segmentation
- The corresponding prompts interact with their queries through self-attention

Inference:
- earnable queries $Q_h$ can freely interact with all prompts
:::


note: 
---
<!-- slide template="[[tpl-con-2-1-box]]" -->
::: title
### Human-Model Interaction
:::

::: left
![[SEEM_MemoryPrompt.PNG|900]]
:::

::: right
During interactive segmentation the prompts are updated every iteration:

1. Textual and visual prompts are updated by the User.
2. Memory prompts $P_m$ , to convey the knowledge of the masks from the previous iteration to the current one, are updated through masked cross attention:
$\Rightarrow P^l_m = MaskedCrossAtt(P^{l−1}_m ; M_p|Z)$
where $P^{l-1}_m$ is the memory prompt of the iteration before and $M_p$ is the mask of the iteration before.


:::

::: source
https://arxiv.org/pdf/2304.06718.pdf
:::
note: 
---
<!-- slide template="[[tpl-title-text]]" -->

::: title
## Resources
:::

::: text
Resources used to create this presentation:
- https://arxiv.org/pdf/2304.06718.pdf (Segment Everything Everywhere All at Once Paper)
- https://github.com/UX-Decoder/Segment-Everything-Everywhere-All-At-Once/tree/v1.0 (Segment Everything Everywhere All at Once GitHub)
- http://semantic-sam.xyzou.net:6090/ (SEEM Demo)
- https://segment-anything.com/demo# (SAM Demo)
- http://deepscene.cs.uni-freiburg.de/index.html (DeepScene Demo)
- https://arxiv.org/pdf/2204.03610.pdf (UniCL Paper)
:::