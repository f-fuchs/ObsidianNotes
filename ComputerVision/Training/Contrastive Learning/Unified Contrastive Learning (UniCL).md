---
dg-publish: true
---

# Unified Contrastive Learning (UniCL)

To combine the image and text encoding into a shared feature space *Unified Contrastive Learning in Image-Text-Label Space* (UniCL) is used.

Combine feature spaces by transposing image space and multiplying with textual space. train image and text encoder together via shared loss. Linear probing holds the model fixed, and you train a small model on top of it that takes the features and produces a label for your task.

![[UniCL.svg|300]]![[UniCL_algorithm.svg]]

## Resources

- <https://github.com/microsoft/UniCL,>
- <https://arxiv.org/pdf/2204.03610.pdf>
