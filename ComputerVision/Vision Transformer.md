The standard [[Transformer]] receives as input a 1D sequence of token embeddings. To handle 2D images, we reshape the image $x \in \mathbb{R}^{H×W ×C}$ into a sequence of flattened 2D patches $x_p \in \mathbb{R}^{N ×(P^2 \cdot C)}$, where $(H, W)$ is the resolution of the original image, $C$ is the number of channels, $(P, P)$ is the resolution of each image patch, and $N = HW/P^2$ is the resulting number of patches, which also serves as the effective input sequence length for the Transformer. The Transformer uses constant latent vector size $D$ through all of its layers, so we flatten the patches and map to $D$ dimensions with a trainable linear projection (Eq. 1). We refer to the output of this projection as the patch embeddings.
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