The standard [[Transformer]] receives as input a 1D sequence of token embeddings. To handle 2D images, we reshape the image $X \in \mathbb{R}^{H×W ×C}$ into a sequence of flattened 2D patches $\vec{x}_p \in \mathbb{R}^{N ×(P^2 \cdot C)}$, where $(H, W)$ is the resolution of the original image, $C$ is the number of channels, $(P, P)$ is the resolution of each image patch, and $N = HW/P^2$ is the resulting number of patches, which also serves as the effective input sequence length for the Transformer. The Transformer uses constant latent vector size $D$ through all of its layers, so we flatten the patches and map to $D$ dimensions with a trainable linear projection (each image patch $\vec{x}_p^i \in \mathbb{R}^{(P^2 \cdot C)}$ is multiplied with a learnable Matrix $E \in \mathbb{R}^{DxD}$). We refer to the output of this projection as the patch embeddings $\vec{x}_{patch}^i \in \mathbb{R}^{D} \land 0 \leq i \leq N$. 

Position embeddings $\vec{x}_{pos}^i \in \mathbb{R}^{D} \land 0 \leq i \leq N$ are added to the patch embeddings to retain positional information. The original paper uses standard learnable 1D position embeddings, since they have not observed significant performance gains from using more advanced 2D-aware position embeddings. The resulting sequence of embedding vectors $\vec{x}_{emb}^i=\vec{x}_{patch}^i+\vec{x}_{pos}^i\in \mathbb{R}^{D} \land 0 \leq i \leq N$ serves as input to the encoder.

### Classification

Similar to BERT’s [class] token, the original Vision Transformer prepends a learnable embedding to the sequence of embedded patches ($z^0_0 = x_{class}$), whose state at the output of the Transformer encoder ($z^0_L$) serves as the image representation $y$. Both during pre-training and fine-tuning, a classification head is attached to $z^0_L$. (*Using a “blank slate” token as the sole input to a classification head pushes the transformer to learn to encode a “general representation” of the entire image into that embedding. The model must do this to enable accurate classifier predictions.*) The classification head is implemented by a [[Feedforward Neural Network (FNN)#Multilayer Perceptron (MLP)|MLP]] with one hidden layer at pre-training time and by a single linear layer at fine-tuning time. 


![[vision-transformer.svg|700]]
## Resources
### Used
- Paper:
	- https://arxiv.org/pdf/2010.11929.pdf
### Interesting other resources
- Paper:
- GitHub:
	- https://github.com/dk-liang/Awesome-Visual-Transformer
- Tutorials:
	- https://uvadlc-notebooks.readthedocs.io/en/latest/tutorial_notebooks/tutorial15/Vision_Transformer.html