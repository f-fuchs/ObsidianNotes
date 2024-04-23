
*SEEM* uses a generic encoder-decoder architecture.  
![[SEEM.svg|700]]
The encoder encompasses the: 
- Image Encoder,
- Text Encoder,
- Visual Sampler,

and the decoder consists of:
- cross-attention of the queries and memory prompt with the image features,
- self-attention of the queries and prompts,
- a pixel decoder and transformer decoder to generate mask and class embeddings.


## Image Encoder and Text Encoder

The image encoder is either a [[Focal Transformer]] or a [[Dual Attention Vision Transformer (DaViT)]] and the Text Encoder is a Transformer Encoder.

$\Rightarrow Z = ImageEncoder(I), I\in \mathbb{R}^{H \times W \times 3}$ 

$\Rightarrow P_t=TextEncoder(T)$


## Combine Image and Text Encodings into Image-Text Representation Space

To combine the image and text encoding into a shared feature space [[Unified Contrastive Learning (UniCL)]]  is used.

$\Rightarrow$ allows Zero-Shot Image Classification

 $\Rightarrow$ improves Linear-Probing, Fine-Tuning and Transfer Learning


## Visual Sampler

The Visual Sampler generates the visual prompts given the feature maps of the target or referred image $\hat{Z}$ and the sampling locations $s \in {points, box, scribbles, polygons}$ of the user.

$$
P_v = VisualSampler(s, \hat{Z})
$$

1. Extract the corresponding region from the image features through point sampling
2. Interpolate 512 point feature vectors uniformly from that region.
![[SEEM_VisualSampler.png|700]]


## SEEM-Decoder

SEEM-Decoder predicts the masks $M$ and semantic concepts $C$ based on the query outputs $O^m_h$ (mask embeddings) and $O^c_h$ (class embeddings), which interact with text, visual, and memory prompts $⟨P_t, P_v , P_m⟩$:

$$
\begin{aligned}
⟨O^m_h, O^c_h⟩ &= Decoder(Q_h; ⟨P_t, P_v , P_m⟩|Z) \\\\
M &= MaskPredictor(O^m_h) \\\\
C &= ConceptClassifier(O^c_h)
\end{aligned}
$$

![[SEEM_Decoder.png|700]]

### Pixel Decoder and Transformer Decoder 

The *SEEM* Decoder uses a similar architecture to the decoder of [[Mask2Former]]  consisting of a pixel decoder and a Transformer decoder. 

$\Rightarrow$ The pixel decoder gradually upsamples low-resolution features from the output of the backbone to generate high-resolution per-pixel embeddings. 

$\Rightarrow$ The Transformer decoder  operates on image features to process object queries. 

$\Rightarrow$ The final binary mask predictions are decoded from per-pixel embeddings with object queries.

![[Mask2Former.PNG|700]]

## Queries and prompt interaction

Training:
- $Q_h$ is duplicated for generic, referring, and interactive segmentation $Q_h \Rightarrow Q_o, Q_t, Q_v$
- The corresponding prompts interact with their queries through self-attention
	- Generic segmentation with no prompt
	- Referring segmentation with the textual prompt
	- Interactive segmentation with the visual and memory prompt

Inference:
- learnable queries $Q_h$ can freely interact with all prompts
![[SEEM_Decoder_Queries.PNG|700]]

## Human-Model Interaction

During interactive segmentation the prompts are updated every iteration:

1. Textual and visual prompts are updated by the User.
2. Memory prompts $P_m$ , to convey the knowledge of the masks from the previous iteration to the current one, are updated through masked cross attention:
$\Rightarrow P^l_m = MaskedCrossAtt(P^{l−1}_m ; M_p|Z)$
where $P^{l-1}_m$ is the memory prompt of the iteration before and $M_p$ is the mask of the iteration before.

![[SEEM_MemoryPrompt.PNG|700]]

## Resources
- https://arxiv.org/pdf/2304.06718.pdf (Segment Everything Everywhere All at Once Paper)
- https://github.com/UX-Decoder/Segment-Everything-Everywhere-All-At-Once/tree/v1.0 (Segment Everything Everywhere All at Once GitHub)
- http://semantic-sam.xyzou.net:6090/ (SEEM Demo)
- https://segment-anything.com/demo# (SAM Demo)
- http://deepscene.cs.uni-freiburg.de/index.html (DeepScene Demo)
- https://arxiv.org/pdf/2204.03610.pdf (UniCL Paper)
- https://arxiv.org/pdf/2212.11270.pdf (XDecoder Paper)
- https://arxiv.org/pdf/2112.01527.pdf (Mask2Former Paper)



