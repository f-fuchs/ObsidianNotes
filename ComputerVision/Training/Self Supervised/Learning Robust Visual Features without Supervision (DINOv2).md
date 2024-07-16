# Learning Robust Visual Features without Supervision (DINOv2)

Dinov2 shows that existing pre-training methods, especially self-supervised methods, can produce general-purpose visual features if trained on enough curated data from different sources. It revisits existing approaches and combines different techniques to scale pre-training in terms of data and model size. Most of the technical contributions aim at accelerating and stabilizing training at scale. In terms of data, it proposes an automatic pipeline to build a dedicated, diverse, and curated image dataset instead of uncurated data, as typically done in the self-supervised literature.

## Data Processing

Regarding pre-training data, an automatic pipeline to filter and rebalance datasets from a large collection of uncurated images was build. This pipeline was inspired by pipelines used in NLP, where data similarities are used instead of external metadata and do not require manual annotation. A major difficulty in dealing with images in the wild is to rebalance concepts and avoid overfitting on a few dominant modes.

![[dinov2_data_pipeline.png]]

> [!question]
> @mario can we use this to build a seismic pre training dataset?

### Embedding

A self-supervised ViT-H/16 network pre-trained on ImageNet-22k is used to compute the image embedding.

### Deduplication

To remove near-duplicate images, the copy detection pipeline of [A Self-Supervised Descriptor for Image Copy Detection (SSCD).](https://github.com/facebookresearch/sscd-copy-detection) was used on the uncurated data. This reduces redundancy and increases diversity among images. This was done on the training, validation, and test sets.

### Retrieval

The curated pretraining dataset is built by retrieving images from the uncurated data source that are close to images in the curated sources. This is done by using the cosine similarity of the embeddings as a distance measure between images. Then, k-means clustering is performed on the uncurated data. Given a query dataset for retrieval, if it is large enough, $N$ (typically 4) nearest neighbors are retrieved for each query image. If it is small, $M$ images from the cluster corresponding to each query image are sampled instead. Although visual inspection seemed to indicate good retrieval quality for $N$ much larger than 4, this leads to more collisions (images that are nearest neighbors of multiple queries).

## Discriminative Self-supervised Pre-training

The original training pipeline was updated and can be seen as a combination of [[Emerging Properties in Self-Supervised Vision Transformers (DINO)]] and [Image BERT Pre-Training with Online Tokenizer (iBOT)](https://github.com/bytedance/ibot?tab=readme-ov-file) losses with the centering of [Unsupervised Learning of Visual Features by Contrasting Cluster Assignments (SwAV)](https://github.com/facebookresearch/swav?tab=readme-ov-file) with an additional regularizer to spread the features and a short high resolution training phase.

> [!question]
> [[Data-Efficient Image Transformers (DeiT)]] found training at lower resolution had an regularizing effect and increased performance?

$L_{DINO}$, defined as $− \sum p_t log(p_s)$, is the cross-entropy loss between the students $p_s$ and the teachers $p_t$ prototype scores. These scores are obtained by passing the [class] token to the corresponding heads and applying a softmax. Additionally, the output of the teacher head is centered using Sinkhorn-Knopp instead of the centering with moving average as in [[Emerging Properties in Self-Supervised Vision Transformers (DINO)|DINO]]. As before the parameters of the students are learned directly and the teacher is build with an exponential moving average.

For the $L_{iBOT}$, defined as $− \sum_i p_{t_i} log(p_{s_i})$, some input patches are randomly masked for the student network, but not the teacher. Then the *iBOT*
