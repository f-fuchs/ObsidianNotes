The standard [[Transformer]] receives as input a 1D sequence of token embeddings. To handle 2D images, we reshape the image $x \in \mathbb{R}^{H×W ×C}$ into a sequence of flattened 2D patches $x_p \in \mathbb{R}^{N ×(P^2 \cdot C)}$, where $(H, W)$ is the resolution of the original image, $C$ is the number of channels, $(P, P)$ is the resolution of each image patch, and $N = HW/P^2$ is the resulting number of patches, which also serves as the effective input sequence length for the Transformer. The Transformer uses constant latent vector size $D$ through all of its layers, so we flatten the patches and map to $D$ dimensions with a trainable linear projection. We refer to the output of this projection as the patch embeddings.

Similar to BERT’s [class] token, the original Vision Transformer prepends a learnable embedding to the sequence of embedded patches ($z^0_0 = x_{class}$), whose state at the output of the Transformer encoder ($z^0_L$) serves as the image representation $y$. Both during pre-training and fine-tuning, a classification head is attached to $z^0_L$. The classification head is implemented by a [[Feedforward Neural Network (FNN)|MLP]] with one hidden layer at pre-training
time and by a single linear layer at fine-tuning time.
Position embeddings are added to the patch embeddings to retain positional information. We use
standard learnable 1D position embeddings, since we have not observed significant performance
gains from using more advanced 2D-aware position embeddings (Appendix D.4). The resulting
sequence of embedding vectors serves as input to the encoder.

![[vision-transformer.svg|700]]
## Resources

### Used
- 
### Interesting other resources
- Paper:
	- https://arxiv.org/pdf/2010.11929.pdf
- GitHub:
	- https://github.com/dk-liang/Awesome-Visual-Transformer
- Tutorials:
	- https://uvadlc-notebooks.readthedocs.io/en/latest/tutorial_notebooks/tutorial15/Vision_Transformer.html