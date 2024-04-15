
Focal Transformer is a [[Vision Transformer]] variant that uses **focal self-attention**. Therefore instead of each token attending all other tokens as in global self attention, each token attends the closest surrounding tokens at fine granularity but the tokens far away at coarse granularity, and thus can capture both short- and long-range visual dependencies efficiently and effectively.

![[focal-transformer.png]]