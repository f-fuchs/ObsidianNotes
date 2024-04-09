### Semantic Image Segmentation

Semantic image segmentation is the technique that involves detecting objects within an image and grouping them based on defined categories. Which is simply labeling each pixel of an image with a corresponding class of what is being represented.
### Instance Image Segmentation

Instance segmentation consists of the localization of specific objects based on the association of their belonging pixels. 
### Panoptic Segmentation

Panoptic Segmentation is a computer vision task that combines semantic segmentation and instance segmentation to provide a comprehensive understanding of the scene. The goal of panoptic segmentation is to segment the image into semantically meaningful parts or regions, while also detecting and distinguishing individual instances of objects within those regions. In a given image, every pixel is assigned a semantic label, and pixels belonging to "things" classes (countable objects with instances, like cars and people) are assigned unique instance IDs.

![](https://production-media.paperswithcode.com/thumbnails/task/task-0000000895-b36c6778.jpg)
## Resources
- Paper: https://arxiv.org/pdf/2304.06718.pdf
- GitHub: https://github.com/facebookresearch/segment-anything