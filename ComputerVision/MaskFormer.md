---
dg-publish: true
---

# MaskFormer

Mask classification is an alternative paradigm that disentangles the image partitioning and classification aspects of segmentation. Instead of classifying each pixel, mask classification-based methods predict a set of binary masks, each associated with a single class prediction. In contrast, per-pixel classification assumes a static number of outputs and cannot return a variable number of predicted regions/segments, which is required for instance-level tasks.

![[MaskFormer_per_pixel_vs_per_mask.png]]

*MaskFormer* uses a backbone to extract image features $F$. A pixel decoder gradually upsamples image features to extract per-pixel embeddings $E_{pixel}$. A transformer decoder, similar to [[Detection Transformer (DETR)]], attends to image features and produces $N$ per-segment embeddings $Q$. The embeddings independently generate $N$ class predictions with $N$ corresponding mask embeddings $E_{mask}$. Then, the model predicts $N$ possibly overlapping binary mask predictions via a dot product between pixel embeddings $E_{pixel}$ and mask embeddings $E_{mask}$ followed by a sigmoid activation. For semantic segmentation task we can get the final prediction by combining $N$ binary masks with their class predictions using a simple matrix multiplication.

![[MaskFormer.png]]

## Resources

- <https://arxiv.org/pdf/2107.06278.pdf>
