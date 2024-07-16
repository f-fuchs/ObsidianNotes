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
