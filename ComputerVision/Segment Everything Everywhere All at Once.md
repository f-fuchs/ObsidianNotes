
## Segmentation

The model was trained on panoptic segmentation, referring segmentation, and interactive segmentation and evaluated on generic segmentation (instance/panoptic/semantic), referring segmentation, and interactive segmentation.
### Generic  segmentation

Segment image without any prompts.
#### Semantic Image Segmentation

Semantic image segmentation is the technique that involves detecting objects within an image and grouping them based on defined categories. Which is simply labeling each pixel of an image with a corresponding class of what is being represented.
-> label distinct categories

![](https://cdn.labellerr.com/semantic%20segmentation/Semantic%20segmentation.webp)
#### Instance Image Segmentation

Instance segmentation consists of the localization of specific objects based on the association of their belonging pixels. 
-> label distinct object
![](https://cdn.labellerr.com/semantic%20segmentation/Instance%20Segmentation.webp)
#### Panoptic Segmentation

Panoptic Segmentation is a computer vision task that combines semantic segmentation and instance segmentation to provide a comprehensive understanding of the scene. The goal of panoptic segmentation is to segment the image into semantically meaningful parts or regions, while also detecting and distinguishing individual instances of objects within those regions. In a given image, every pixel is assigned a semantic label, and pixels belonging to "things" classes (countable objects with instances, like cars and people) are assigned unique instance IDs.
-> label distinct objects but keep category association
![](https://cdn.labellerr.com/semantic%20segmentation/Panoptic%20Segmentation.webp)

### Referring segmentation

### Text referring segmentation

Segment with a text prompt.

### Visual referring segmentation

## Resources
- Paper: https://arxiv.org/pdf/2304.06718.pdf
- GitHub: https://github.com/facebookresearch/segment-anything