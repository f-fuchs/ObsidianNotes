---
dg-publish: true
dg-home: true
---

# Overview

Home page of my Computer Vision notes. These notes are a work in progress!

The notes are created via Obsidian and published with Obsidian Digital Garden.

The source files of the notes are available on [GitHub](https://github.com/f-fuchs/ObsidianNotes).

## Table of Contents

```dataview
TABLE
	join(rows.file.link, " | ") as Notes
WHERE contains(file.folder, this.file.folder)
SORT file.name ASC
GROUP BY file.folder as Topic
```

## TODOs

 - [ ] Rework Attention Note
 - [ ] Consistent mathematical notation between notes
 - [ ] Incomplete Notes:
	- [ ] CNN
	- [ ] FNN
	- [ ] Understanding Diffusion Models A Unified Perspective
	- [ ] Generative Models
	- [ ] Pooling Layers
	- [ ] Stochastic Process
	- [ ] Adam
	- [ ] SGD
- [ ] New Topics:
	- [ ] Segment Anything:
		- [ ] <https://github.com/facebookresearch/segment-anything>
		- [ ] <https://github.com/SysCV/sam-hq>
		- [ ] <https://github.com/pytorch-labs/segment-anything-fast>
		- [ ] <https://github.com/IDEA-Research/Grounded-Segment-Anything>
	- [ ] Mamba:
		- [ ] <https://github.com/MzeroMiko/VMamba>
		- [ ] <https://github.com/kyegomez/VisionMamba>
		- [ ] <https://github.com/wurenkai/UltraLight-VM-UNet/>
		- [ ] <https://github.com/JCruan519/VM-UNet>
	- [ ] Diffusion:
		- [ ] <https://arxiv.org/abs/2208.11970> (Understanding Diffusion Models: A Unified Perspective)
	- [ ] General:
		- [ ] <https://github.com/zengwang430521/TCFormer>
		- [ ] <https://github.com/sunjiahao1999/SPFormer>
		- [ ] <https://github.com/CSAILVision/unifiedparsing>
