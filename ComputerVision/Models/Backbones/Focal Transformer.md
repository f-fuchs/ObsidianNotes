---
dg-publish: true
---

# Focal Transformer

Focal Transformer is a [[Vision Transformer]] variant that uses **focal self-attention**. Therefore instead of each token attending all other tokens as in global self attention, each token attends the closest surrounding tokens at fine granularity but the tokens far away at coarse granularity, and thus can capture both short and long-range visual dependencies efficiently and effectively.

![[focal-transformer.png]]

The focal mechanism enables long-range self-attention with much less time and memory cost, because it attends a much smaller number of surrounding (summarized) tokens. In practice, however, extracting the surrounding tokens for each query position suffers from high time and memory cost since we need to duplicate each token for all queries that can get access to it. Therefore focal self-attention is computed at the window level.

![[focal_attention.png]]
