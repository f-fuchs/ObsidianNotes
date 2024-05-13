---
dg-publish: true
---

# Swin-Unet

Swin-Unet is a Unet-like pure Transformer. This mean it has a U-shaped Encoder-Decoder architecture with skip-connections for local-global semantic feature learning. Specifically, hierarchical [[Swin Transformer]] are used as the encoder to extract context features. And a symmetric Swin Transformer-based, with patch expanding layers to perform the up-sampling operation to restore the spatial resolution of the feature maps, is used as decoder.

![[swin_unet_overview.jpg]]
