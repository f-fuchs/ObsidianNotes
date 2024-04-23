Masked-attention Mask Transformer (*Mask2Former*)  is a universal image segmentation architecture consisting of a simple meta architecture consisting of a backbone feature extractor, a pixel decoder and a Transformer decoder. The backbone extracts low-resolution features from an image. The pixel decoder gradually upsamples low-resolution features from the output of the backbone to generate high-resolution per-pixel embeddings. And finally the Transformer decoder  operates on image features to process object queries. The final binary mask predictions are decoded from per-pixel embeddings with object queries.

![[Mask2Former.PNG]]

## Backbone

Both [[Convolutional Neural Networks (CNN)]] and [[Vision Transformer]] backbones are fine.

## Pixel Decoder

Both [[Convolutional Neural Networks (CNN)]] and Transformer pixel decoders are fine.

## Transformer Decoder

Recent studies suggest that the slow convergence of Transformer-based models is due to global context in the cross-attention layer, as it takes many training epochs for cross-attention to learn to attend to localized object regions. Therefore masked attention is a variant of cross-attention that only attends within the foreground region of the predicted mask for each query.

Standard cross-attention (with residual path) computes: $X_l = softmax(Q_l K^T_l ) V_l + X_{l−1}$. 
Masked attention  (with residual path) computes: $X_l = softmax(\mathcal{M}_{l−1} + Q_l K^T_l )V_l + X_{l−1}$.

Where $l$ is the layer index, $X_l \in \mathbb{R}^{N ×C}$ refers to the query features at the $l$th layer and $Q_l =f_Q(X_{l−1}) \in \mathbb{R}^{N ×C}$. $X_0$ denotes the input query features to the Transformer decoder. $K_l, V_l \in \mathbb{R}^{H_l \cdot W_l×C}$ are the image features under transformation $f_K(·)$ and $f_V (·)$ respectively, and $H_l$ and $W_l$ are the spatial resolution of image features of stage $k$ of the Transformer Decoder Layer. Moreover, the attention mask $\mathcal{M}_{l−1}$ at feature location $(x, y)$ is:
$$
\mathcal{M}_{l−1}(x, y) =
\begin{cases}
0 \text{ if } M_{l−1}(x, y) = 1 \\
−∞ \text{ otherwise}
\end{cases}
$$
Here, $M_{l−1} \in {0, 1}^{N\times H_lW_l}$ is the binarized output (thresholded at 0.5) of the resized mask prediction of the previous ($l − 1$)-th Transformer decoder layer. It is resized to the same resolution of $K_l$. $M_0$ is the binary mask prediction obtained from $X_0$, i.e., before feeding query features into the Transformer decoder.
## Resources
- https://arxiv.org/pdf/2112.01527.pdf