Masked-attention Mask Transformer (Mask2Former)  is a universal image segmentation architecture consisting of a simple meta architecture consisting of a backbone feature extractor, a pixel decoder and a Transformer decoder. The backbone extracts low-resolution features from an image. The pixel decoder gradually upsamples low-resolution features from the output of the backbone to generate high-resolution per-pixel embeddings. And finally the Transformer decoder  operates on image features to process object queries. The final binary mask predictions are decoded from per-pixel embeddings with object queries.



![[Mask2Former.PNG]]

## Backbone

Both [[CNN]] and [[Vision Transformer]] backbones are fine.

## Pixel Decoder

Both [[CNN]] and Transformer pixel decoders are fine.

## Transformer Decoder

Recent studies suggest that the slow convergence of Transformer-based models is due to global context in the cross-attention layer, as it takes many training epochs for cross-attention to learn
to attend to localized object regions. Masked attention, a variant of cross-
attention that only attends within the foreground region of
the predicted mask for each query.
## Resources
- https://arxiv.org/pdf/2112.01527.pdf