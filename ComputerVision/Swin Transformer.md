Swin Transformer are a kind of [[Vision Transformer]]  that tries to solve the problems of scale variations and a high resolution of pixels via hierarchical feature maps and  calculating the representation with **S**hifted **win**dows.
![[SwinTransformer_model.jpg]]
An overview of the architecture is shown in the image above. Similar to the [[Vision Transformer]] the first step is to split the image into image patches $X_p \in \mathbb{R}^{N ×(P^2 \cdot C)}$ where $N=\frac{H}{4} \cdot \frac{W}{4}$, $P=4$ and $C=3$ ($X_p \in \mathbb{R}^{\frac{H}{4} \cdot \frac{W}{4} × 48}$ ). Afterwards a linear embedding layer is used to project the raw features into an arbitrary dimension $C$ ($X_{emb}=X_p \times E \in \mathbb{R}^{\frac{H}{4} \cdot \frac{W}{4} × C}$, where $E \in \mathbb{R}^{48 \times C}$ ). One important difference compared to [[Vision Transformer]]s is that no positional embeddings are added. The last step of State 1 (see image above) are several Swin Transformer Blocks, which are depicted on the right in the image above. The difference to the original [[Transformer#Transformer Block]] 





![[SwinTransformer_hierarchical_featue_maps.jpg|700]]
![[SwinTransformer_shifted_window.jpg|700]]